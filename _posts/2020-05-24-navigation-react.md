---
layout: post
title:  "Navigation in React"
author: david
categories: [ engineering, ui ]
---
[Uclusion](https://www.uclusion.com/?utm_source=devto&utm_medium=blog&utm_campaign=devnavigation) usually avoids creating our own way of doing things but for React navigation we need absolute control of what was loaded and what not. Out of the box navigation solutions tend to remove from the DOM all but the current page — see for instance this [issue](https://github.com/react-navigation/react-navigation/issues/7140). So at that point the utility offered by most React navigation libraries was too undercut by our need for control. So instead we did something very simple:

    return (
      <div>
        <CssBaseline/>
        <div className={classes.body}>
          <div className={classes.root}>
            <div className={classes.content}>
              <SignupWizard hidden={isOnboardingHidden()}/>
              <Home hidden={isHomeHidden()}/>
              <Market hidden={isMarketHidden()}/>
              <Support hidden={isSupportHidden()}/>
              ...
              <PageNotFound hidden={isAllHidden()}/>
            </div>
          </div>
        </div>
      </div>
    );
See [in GitHub](https://github.com/Uclusion/uclusion_web_ui/blob/master/src/containers/Root/Root.js).

Where the hide functions work from knowing the current URL via react-router:

    function Root() {
      const history = useHistory();
      const classes = useStyles();
      const { location } = history;
      const { pathname } = location;

Note that in this scheme the individual pages can use the same methods to read the URL or to get the hash out of the “location” as well if necessary. There is no need to pass all of this information down. You could even dispense with the Root we are using and have each page make its own decision to hide or not but it is nice to have the decision centralized to prevent name space collisions and allow for page not found.

Putting performance aside if you have code like

    const [idLoaded, setIdLoaded] = useState(undefined);
    const [storedState, setStoredState] = useState(undefined);

and you use the default sort of routing system like

    <Router>
     <div>
      <Route path=”/users” component={Users} />
      <Route path=”/contact” component={Contact} />
     </div>
    </Router>

then your stored state will be removed whenever your route is not in use. Instead in our version all pages load all the time but the property “hidden” controls whether or not they display — and so state is preserved.

For performance our claim is that each individual page should load all of its data into memory but instead of rendering just

    if (hidden) {
      return <React.Fragment/>
    }

You could go so far as to render the page as well but that’s likely just wasting CPU and DOM space as the page will re-render when the “hidden” property changes anyway.

Another advantage to hiding instead of removing is sometimes you need to be aware of the transition and take some action:

    useEffect(() => {
      if (!hidden && firstOpen) {
        editorFocusFunc();
        setFirstOpen(false);
      }

Uclusion also had the common requirement to detect when navigation occurs so page specific actions can be taken. That’s not as simple as it sounds as page could be navigated to by switching tabs, back button, etc.

    useEffect(() => {
      function pegView(isEntry) {
        const currentPath = window.location.pathname;
        const { action, marketId, investibleId } = decomposeMarketPath(currentPath);
        broadcastView(marketId, investibleId, isEntry, action);
      }
    
      const perfEntries = performance.getEntriesByType("navigation");
    
      let reloaded = false;
      for (let i = 0; i < perfEntries.length; i++) {
        reloaded = perfEntries[i].type === 1;
        if (reloaded) {
          break;
        }
      }
      if (reloaded) {
        refreshVersions();
        refreshNotifications();
      }
      if (!window.myListenerMarker) {
        window.myListenerMarker = true;
        window.addEventListener('load', () => {
          pegView(true);
        });
        window.addEventListener('focus', () => {
          pegView(true);
        });
        window.addEventListener('blur', () => {
          pegView(false);
        });
        window.addEventListener('online', () => {
          setOnline(true);
          setOperationsLocked(false);
          pegView(true);
        });
        window.addEventListener('offline', () => {
          setOnline(false);
          pegView(false);
        });
        window.addEventListener('popstate', () => {
          pegView(true);
        });
        document.addEventListener('visibilitychange', () => {
          const isEntry = document.visibilityState === 'visible';
          pegView(isEntry);
        });
      }
    ...

Above we are also detecting a user driven browser reload event so we can refresh from the API (since the user thinks its necessary).

Finally what about page navigation initiated from within Javascript? For that we use this function (which is [here](https://github.com/Uclusion/uclusion_web_ui/blob/master/src/utils/marketIdPathFunctions.js) in GitHub)

    export function navigate(history, to) {
      const {
        action: fromAction,
        marketId: fromMarketId,
        investibleId: fromInvestibleId,
      } = decomposeMarketPath(history.location.pathname);
      broadcastView(fromMarketId, fromInvestibleId, false, fromAction);
      if (to) {
        history.push(to);
      } else {
        history.goBack();
      }
      const {
        action: toAction,
        marketId: toMarketId,
        investibleId: toInvestibleId,
      } = decomposeMarketPath(history.location.pathname);
      broadcastView(toMarketId, toInvestibleId, true, toAction);
    }

which makes sure that the same navigation is broadcast leaving and entering pages that way.

None of the above code is complicated but we hope sharing it can avoid the rather lengthy trial and error process required to come to this solution.
