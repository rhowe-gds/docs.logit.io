---
date: 2017-02-17T16:07:13+01:00
title: Cloud Foundry
menu:
  main:
    parent: 'sending-data'
    weight: 20
---

From your Logit.io dashboard:

1. Identify the Logit ELK stack you want to use.

1. Click Logstash **Configuration**.

1. Note your Logstash **Endpoint**.

1. Note your TCP-SSL, TCP or UDP **Port** (not the syslog port).

1. Create the log drain service in Cloud Foundry.
    
    <pre class='terminal'>
    $ cf cups logit-ssl-drain -l syslog-tls://ENDPOINT:PORT
    </pre>   
    or
    <pre class='terminal'>
    $ cf cups logit-drain -l syslog://ENDPOINT:PORT
    </pre>

1. Bind the service to an app.

    <pre class='terminal'>
    $ cf bind-service YOUR-CF-APP-NAME logit-ssl-drain
    </pre>
    or
    <pre class='terminal'>
    $ cf bind-service YOUR-CF-APP-NAME logit-drain
    </pre>

1. Restage or push the app using one of the following commands:

    <pre class='terminal'>$ cf restage YOUR-CF-APP-NAME</pre>

    <pre class='terminal'>$ cf push YOUR-CF-APP-NAME</pre>

    After a short delay, logs begin to appear in Kibana.

For more information see the cloud foundry documentation: [Log Streaming] (https://docs.cloudfoundry.org/devguide/services/log-management-thirdparty-svc.html#logit)
