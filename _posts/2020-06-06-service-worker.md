---
layout: post
title:  "Gotchas with Service Workers and SPAs"
author: ben
categories: [ engineering, ui ]
---
[Uclusion](https://www.uclusion.com/?utm_source=devto&utm_medium=blog&utm_campaign=devservicepwa) is a single page app (SPA), which means the browser doesn’t see very many navigation events while the user is going about their business. Service workers, by default, have the rule that only pages loaded by a service worker will handle their requests via that service worker. These two things combine such that even if you register a service worker on entrance to your SPA, it won’t work until the user hits reload.

Additionally, by default, service workers will wait until a page close and page reopen to load a new version of a service worker. This means that unless the user closes your app and comes back in, your new service worker code won’t take effect.

**So how do we override the defaults?**

Perversely, because of the event chain, to solve the first problem, you first should solve the second. Namely, you need to make your service worker [immediately activate](https://developer.mozilla.org/en-US/docs/Web/API/ServiceWorkerGlobalScope/skipWaiting) as soon as it’s registered with the browser. That can be done by the following code in your service worker file (not the [register service worker](https://gist.github.com/camwhite/2f33f7c33e2495b01614f209399703ee)). See our production file [here](https://github.com/Uclusion/uclusion_web_ui/blob/master/public/image-url-rewriter-service-worker.js).

    self.addEventListener('install', (event) => {
      return self.skipWaiting();
    });

Now that the service worker is activating reliably, we can force it to claim every page fetch for the domain and path it’s been registered for. You can do that by:

    self.addEventListener('activate', (event) => {
      self.clients.claim();
    });

I would recommend that, at least in development, you output some log statements in your service worker that fire every time it runs. That way you can see in tools like [LogRocket](https://www.logrocket.com) that your worker really is taking effect when you think it is.
