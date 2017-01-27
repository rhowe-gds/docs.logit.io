---
date: 2016-03-08T21:07:13+01:00
title: syslog
menu:
  main:
    parent: 'sending-data'
    weight: 22
---

A syslog endpoint has been created for you in your logstash input config.

Click the configuration link on the stack you wish to log too in your [dashboard] (https://logit.io/Dashboard).

Your logstash endpoint link and input configuration input is written out for you. Note you can send syslog over udp or tcp.

## rsyslog configuration

Replace `STACK_ID` and `SYSLOG_SSL_PORT` with the values from your [dashboard] (https://logit.io/Dashboard). Download [star.logit.io.crt file](https://cdn.logit.io/star.logit.io.crt) and place in `/etc/rsyslog.d/keys/ca.d/`.

```text
$DefaultNetstreamDriverCAFile /etc/rsyslog.d/keys/ca.d/star.logit.io.crt

$ActionSendStreamDriver gtls
$ActionSendStreamDriverMode 1
$ActionSendStreamDriverAuthMode x509/name
$ActionSendStreamDriverPermittedPeer *.logit.io

*.* @@STACK_ID-ls.logit.io:SYSLOG_SSL_PORT
```

##### Notes

1. If possible run the latest minor versions of rsyslog v7 or v8. There are many TLS bugs in past versions.
1. Ensure you have `@@` not a single `@` infront of the host. This is so TCP is used.
