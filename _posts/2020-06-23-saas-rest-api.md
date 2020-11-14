---
layout: post
title:  "Designing SaaS Rest APIs for web clients"
author: david
categories: [ engineering, backend ]
---
For a typical browser IndexedDB storage gives you access to as much as half the free disk space. Once you convince yourself to use Rest, having that much storage makes your basic flow:

1. Have an API that returns all changed items for a client.

1. Have APIs that return the items for anything that changed.

1. Any create or update API will need to return the back end stored object so that the front end can update its IndexedDB cache.

1. In general do not expose individual item read APIs or APIs that filter, sort or search — do all of that on the web client.

In graphical terms 1 and 2 look like this:

![](https://cdn-images-1.medium.com/max/2000/1*9Xy2i3yHDO9WyEB4GMrcVA.png)

So far very simple but 3 is where we fall down the rabbit hole. If any single one of your APIs is eventually consistent then answering “Client up to date?” is hard.

[Uclusion](https://www.uclusion.com/?utm_source=uclusion&utm_medium=blog&utm_campaign=devapi) uses DynamoDB and asynchronous workflows built on DynamoDB streams so of course there is eventually consistent everywhere. Even with a SQL DB you could be reading from a slave or multi-master database where replication lag will be eventually consistent. If you rely on a read immediately following a write returning the data you just wrote then the front end client is dictating back end implementation.

If because of client space or compute limitations filter, sort and search capabilities must have APIs then run them outside your main transactional database. Otherwise long running queries against the same database requiring lightning fast create and updates is a use case mismatch. So these kinds of querying APIs require eventual consistency as traffic and volume of data scales.

With eventual consistency a call to refresh the client with the latest data can overwrite newer data that it already has from create and update operations. So a user might see his newly created object disappear for a while unless you are careful.

Traditional CRUD where a page loads from the back end dynamically or hoping to get by with an all synchronous API are strategies that user performance expectations and SaaS traffic loads have obsoleted. Our strategy for handling syncing eventually consistent objects:

1. All objects are versioned and these versions are used for signatures.

1. When the back end sends the object signatures it records an ID in a look up table for what was sent to the client.

1. If the client is successful in retrieving the object signatures it uses the signature ID in subsequent calls to inform the back end what object versions it has.
