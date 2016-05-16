---
date: 2016-03-08T21:07:13+01:00
title: Managing indexes
menu:
  main:
    weight: 21
---

## Data usage

You can view your ES index sizes by making use of your http API for ES, the url is on your dashboard.
Simply change the path to 

```sh
/_cat/indices?apikey=YOUR-API-KEY&pretty=true
```

## Automatic deletion

Based upon your retention plan we will automatically clean indexes after a certain amount of time.

Please note, currently any indexes not in the format indexname-yyyy.mm.dd will be automatically deleted.
If you need to use custom index names that are either not time based or need to use a different format please contact support.

## Manual deletion

You can use the ES http api to delete indexes by name.

https://www.elastic.co/guide/en/elasticsearch/reference/current/indices-delete-index.html
