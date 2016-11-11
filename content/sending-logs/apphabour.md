---
date: 2016-03-08T21:07:13+01:00
title: AppHarbour
menu:
  main:
    parent: 'sending-data'
    weight: 20
---

To send us a log all you need to do is add this endpoint as a logdrain in your appharbor account:
```sh
https://api.logit.io/appharbor?apikey=YOUR-API-KEY
```

We automatically parse the logs into a structured format for you so all you need to do is analyse them

For more information see the Appharbor site: [Log Drains] (https://support.appharbor.com/kb/tips-and-tricks/logging) or visit the Logplex HTTP Drains docs in github [HTTP Drains] (https://github.com/heroku/logplex/blob/master/doc/README.http_drains.md)

