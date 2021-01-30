---
layout: post
title:  "Towards better notifications"
author: ben
categories: [ engineering ]
image: assets/images/better_notifications_3_bells.png
featured: true
---

Notifications in Uclusion used to be based on a model similar to slack: A notification would tell
you of a change, upon clicking the notification the user is navigated somewhere, and the notification
would disappear.

This works well for informing you of events, but doens't work well for making sure anything gets done.
To accomplish the latter you need two things:
1. A notification must be *persistent* until some set of criteria is met. E.G. a notification of a new
poll has opened should stick around until you've replied to the poll.
2. Notifications should be *prioritized*, and that prioritization should be exposed to the user to enable
them to make intelligent decisions about what to respond to.

### Persistence ###
Persistence is surprisingly tricky to implement. To do it properly you have think deeply about every
notification you send out and consider all the possible ways the user could reasonably respond.
For example, if you have a notification that story was just created (Uclusion does), you can be
reasonably certain the user has read the story if they vote for it (there are about 5 other ways too).

Once you know what user actions can retire a notification you now have to *detect* the event happening,
preferably without littering function calls all over your code.

What we wound up doing was creating DynamoDB stream listener that captured updates on our core model
objects and fires a series of event handlers to make sure notifications are created or destroyed.

Here's an except from the stream listener and one of the simplest such handler that fires when a comment is converted into a story


From the listener attached to the comment stream:
```
new_image = unpack_record(record['dynamodb']['NewImage'])
comment_id = record['dynamodb']['Keys']['id']['S']
payload = {
                'new_image': new_image,
                'comment_id': comment_id
            }
handle_comment_moved(payload)
```
And the handler it calls
```
def handle_comment_moved(payload):
    new_image = payload['new_image']
    comment_id = payload['comment_id']
    market_id = new_image['market_id']
    children = new_image.get('children')
    everyone_not_hidden = get_users_for_object(market_id, 'market')
    for user_id in everyone_not_hidden:
        delete_notification(NotificationEventType.ISSUE, market_id, user_id, comment_id)
        delete_notification(NotificationEventType.UNREAD, market_id, user_id, comment_id)
```

`delete_notification` itself is fairly simple, and searches the notification DB and GSIs
for notifications that match the correct event type, user, comment, and market
(market is our name for top level objects since they represent a 'market' of ideas).

Sometimes events create new notifications too, and we insert new rows into the notification DB with `notify`:

```
for user_id in response['assigned']:
    notify(user_id, investible_id, market_id, NotificationEventType.REPORT_REQUIRED.name, link_map)
```


### Prioritization ###
Prioritization is very simple to implement but very hard to make usable. You have to think very carefully about
why a notification is going out, who it serves, and what happens if it doesn't get responded to. In Uclusion's case
we made a very simple rubric: Are you preventing anyone else from getting anything done if you don't respond.
If the answer is yes, then we assign the highest priority, RED. If no, then we will assign either YELLOW or BLUE,
depending on if there's the potential to stop work in the future.
For example, someone declaring they've hit a blocking issue is a request for help, and hence is RED, a notification
that someone has asked a question in your story is YELLOW, while a notice that someone has updated a story you've voted
for is BLUE.

As mentioned before, implementation is simple in that we created a LEVEL enum, and tag notifications with it:
```
notify(...,..., level=NotificationLevelType.RED.name)
```
On the front end we bucketize the notifications based on levels, and then feed each level into a distinct alert box,
which get represented by 3 indicators on our top bar:
![Top Bar]({{ site.baseurl }}/assets/images/better_notifications_top_bar.png)

That's done by the code below, which also handles space constraints on mobile:
```
function NotificationsContainer (props) {

  const classes = useStyles();
  const [activeLevel, setActiveLevel] = useState(null);
  const [messagesState] = useContext(NotificationsContext);
  const redMessages = levelMessages(messagesState, RED_LEVEL);
  const yellowMessages = levelMessages(messagesState, YELLOW_LEVEL);
  const blueMessages = levelMessages(messagesState, BLUE_LEVEL);

  // on small windows we only have room for one, so drop blue and yellow if we have red
  const showYellowMessages = !_.isEmpty(yellowMessages) && (!isTinyWindow() || _.isEmpty(redMessages));
  const showBlueMessages = !_.isEmpty(blueMessages) && (!isTinyWindow() || _.isEmpty(redMessages) || _.isEmpty(yellowMessages));
  return (
    <React.Fragment>
      {!_.isEmpty(redMessages) && (
        <div className={classes.bellButton}>
          <Notifications
            level={RED_LEVEL}
            messages={redMessages}
            active={activeLevel}
            setActive={setActiveLevel}/>
        </div>)}
      {showYellowMessages && (
        <div className={classes.bellButton}>
          <Notifications
            level={YELLOW_LEVEL}
            messages={yellowMessages}
            active={activeLevel}
            setActive={setActiveLevel}/>
        </div>)}
      {showBlueMessages && (
        <div className={classes.bellButton}>
          <Notifications
            level={BLUE_LEVEL}
            messages={blueMessages}
            active={activeLevel}
            setActive={setActiveLevel}/>
        </div>)}
    </React.Fragment>
  );
}
```

As always, if you have questions feel free to drop us a line.
