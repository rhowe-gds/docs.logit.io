---
date: 2016-03-08T21:07:13+01:00
title: Sending logs
menu:
  main:
    weight: 20
---

## Beats

To set up beats just follow the steps 1, 2 and 3 (we will be changing the output from elastic search to logstash) from the relevant links:

You can ignore the steps about templates (step 4) and dashboards (step 6), this has already been setup for you!

* [FileBeat] (https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-installation.html)
* [PacketBeat] (https://www.elastic.co/guide/en/beats/packetbeat/current/packetbeat-installation.html)
* [Topbeat] (https://www.elastic.co/guide/en/beats/topbeat/current/topbeat-installation.html)
* [Winlogbeat] (https://www.elastic.co/guide/en/beats/winlogbeat/current/winlogbeat-installation.html)

Below is the configuration changes you need:

Change (comment out), the lines found below, ### Elasticsearch as output
```sh
#elasticsearch:
#hosts: ["localhost:9200"]:
```
Then under ### Logstash as output:
```sh
hosts: ["d7f8e807-6dc8-40bb-9569-a1f4486c4991-ls.logit.io:11004"]
compression_level: 3
```
Finally now just restart beats (some links to help)

* [FileBeat] (https://www.elastic.co/guide/en/beats/filebeat/current/_step_5_starting_filebeat.html#_step_5_starting_filebeat)
* [PacketBeat] (https://www.elastic.co/guide/en/beats/packetbeat/current/_step_5_starting_packetbeat.html#_step_5_starting_packetbeat)
* [Topbeat] (https://www.elastic.co/guide/en/beats/topbeat/current/_step_5_starting_topbeat.html#_step_5_starting_topbeat)
* [Winlogbeat] (https://www.elastic.co/guide/en/beats/winlogbeat/current/_step_5_starting_winlogbeat.html#_step_5_starting_winlogbeat)

## Windows

To set up the windows agent just follow the steps below:

Copy your API Key from your [dashboard] (https://logit.io/Dashboard)

[Download our Agent] (ihttps://logit.io/LogitAgent.exe)

Stay on this page and install the Agent on your server, follow the install wizard, dont forget your API Key!

Once installed we will show a sucess message if you dont see this please check the event logs on the server

## Heroku

To send us a logs all you need to do is:

```sh
heroku drains:add https://api.logit.io/heroku?apikey=cd432e81-6472-4957-a4b0-0df3b0e0ca32 -a appname
```

We automatically parse the logs into a structured format for you so all you need to do it analyse them

For more information see the heroku site: [Log Drains] (https://devcenter.heroku.com/articles/log-drains#https-drains)

## AppHarbour

To send us a logs all you need to do is add this endpoint as a logdrain in your appharbor account:
```sh
https://api.logit.io/appharbor?apikey=cd432e81-6472-4957-a4b0-0df3b0e0ca32
```

We automatically parse the logs into a structured format for you so all you need to do it analyse them

For more information see the Appharbor site: [Log Drains] (https://support.appharbor.com/kb/tips-and-tricks/logging) or visit the Logplex HTTP Drains docs in github [HTTP Drains] (https://github.com/heroku/logplex/blob/master/doc/README.http_drains.md)

## Http

To send us a log all we required is:

* Valid JSON content
* ApiKey sent in the headers for ease, your key is - `cd432e81-6472-4957-a4b0-0df3b0e0ca32`
* Content type set to application/json
* You can POST or PUT your data
If you want to try it out copy this below and send it in!

```sh
curl -i -H "ApiKey: cd432e81-6472-4957-a4b0-0df3b0e0ca32" -i -H "Content-Type: application/json" http://api.logit.io/v2 -d '{"username":"xyz","password": { "a": 1, "b": 2 } }'
```

Remember if you structure your data correctly you will have much easier life!

Optionally you can define the type of your data, this is important if you want to reuse the same fields but with different underlying types. Dont /worry if you dont set it we will set it to 'general' `LogType` is all you need to set in the headers e.g. `-H "LogType: example"`

You should get a response code of `202` from us otherwise you will get a `500`

```sh
HTTP/1.1 202 ACCEPTED
Server: nginx/1.6.0
Date: Mon, 02 May 2016 19:15:29 GMT
Content-Type: application/json
Content-Length: 25
{
  "message": "Thanks"
}
```
## .Net

To set up Log4net you can choose to install the nuget package, or directly use the [dlls] (https://www.nuget.org/packages/log4net.Logit/)
```
    Install-Package log4net.Logit
```


Once you have installed the Nuget or the indvidual DLLs (extracted from the Nuget package) you can use the appender configuration below
```sh
<appender name="LogitAppender" type="log4net.Logit.LogitAppender, log4net.Logit">
    <apikey value="YOUR-API-KEY" />
    <layout type="log4net.Layout.PatternLayout">
        <conversionpattern value="%property{log4net:HostName} %-5p %d %5rms %-22.22c{1} %-18.18M - %m%n" />
    </layout>
</appender>
```
You can decide what level you require!
```sh
<root>
    <level value="ALL" />
    <appender-ref ref="LogitAppender" />
</root>
```
Finally open kibana and we will have parsed the messages automatically for you!

## Cordova/PhoneGap

Our repository and instructions can be found [here] (https://github.com/logit-io/cordova-logitio)

## Browser

Our repository and instructions can be found [here] (https://github.com/logit-io/javascript-logitio)

## Node

Our repository and instructions can be found [here] (https://github.com/logit-io/node-logitio)
