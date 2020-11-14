---
layout: post
title:  "Multiple tabs in your app"
author: david
categories: [ engineering, ui ]
---
We had some problems with multiple tabs that are pretty common:
* Writing to storage could collide or not get picked up
* Logout in one tab would not be noticed in the other
* Sync with the backend would be done independently by all

Being [Uclusion](https://www.uclusion.com/?utm_source=devto&utm_medium=blog&utm_campaign=multitab) we of course used a Uclusion Dialog to decide and the options were:
* [broadcast-channel](https://www.npmjs.com/package/broadcast-channel) the NPM package
* [Broadcast channel API](https://developer.mozilla.org/en-US/docs/Web/API/Broadcast_Channel_API)
* [Service worker communication](https://felixgerschau.com/how-to-communicate-with-service-workers/#:~:text=Service%20Workers%20can%20intercept%20requests,when%20all%20tabs%20are%20closed)

Pretty easy decision because in addition to using broadcast channel API when available the NPM package supported leader selection. That allowed us to set up a React context to let us know anywhere in the code whether our tab was leader or not - see code [here](https://github.com/Uclusion/uclusion_web_ui/blob/a013f9327700f2d67d56df2d9154575b18cddde2/src/contexts/LeaderContext/LeaderContext.js).

We could also send messages to the other tabs telling them to refresh from IndexedDB [like so](https://github.com/Uclusion/uclusion_web_ui/blob/0523b6fd43d8a696082b2ac1530c4081a3594f4b/src/contexts/CommentsContext/commentsContextReducer.js)
```
const myChannel = new BroadcastChannel(COMMENTS_CHANNEL);
      return myChannel.postMessage('comments').then(() => myChannel.close())
        .then(() => console.info('Update comment context sent.'));
```

Now the basic idea we followed was the leader syncs from the backend and stores in an IndexedDB namespace and all other tabs store their local edits in a differently named IndexedDB namespace. Its very unlikely more than one tab is doing local edits at a time and even if somehow they were the sync from the network is the eventual master.

Also very simple [logout](https://github.com/Uclusion/uclusion_web_ui/blob/fdab31beb38bac3c1cc581a9c38fe06798dfe422/src/pages/Authentication/SignOut.js) broadcasts a message which is listened for by the other tabs [here](https://github.com/Uclusion/uclusion_web_ui/blob/b73290bcaf7ad8be153ff8dc31f253378e30a21f/src/containers/Header/index.js)
```
const [logoutChannel, setLogoutChannel] = useState(undefined);

  useEffect(() => {
    console.info('Setting up logout channel');
    const myLogoutChannel = new BroadcastChannel('logout');
    myLogoutChannel.onmessage = () => {
      console.info('Logging out from message');
      onSignOut().then(() => console.info('Done logging out'));
    }
    setLogoutChannel(myLogoutChannel);
    return () => {};
  }, []);
```
