---
date: 2016-03-08T21:07:13+01:00
title: Heroku
menu:
  main:
    parent: 'sending-data'
    weight: 20
---

To send us a logs all you need to do is:

```sh
heroku drains:add https://api.logit.io/heroku?apikey=YOUR-API-KEY -a appname
```

We automatically parse the logs into a structured format for you so all you need to do it analyse them

For more information see the heroku site: [Log Drains] (https://devcenter.heroku.com/articles/log-drains#https-drains)
