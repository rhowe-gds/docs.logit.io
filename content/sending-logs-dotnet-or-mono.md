---
date: 2016-03-08T21:07:13+01:00
title: .NET / Mono
menu:
  main:
    parent: 'Sending Data'
    weight: 20
---

To set up Log4net you can choose to install the nuget package, or directly use the [DLLs] (https://www.nuget.org/packages/log4net.Logit/)

```
    Install-Package log4net.Logit
```

Once you have installed the Nuget or the indvidual DLLs (extracted from the Nuget package) you can use the appender configuration below

```
<appender name="LogitAppender" type="log4net.Logit.LogitAppender, log4net.Logit">
    <apikey value="YOUR-API-KEY" />
    <layout type="log4net.Layout.PatternLayout">
        <conversionpattern value="%property{log4net:HostName} %-5p %d %5rms %-22.22c{1} %-18.18M - %m%n" />
    </layout>
</appender>
```

You can decide what level you require!

```
<root>
    <level value="ALL" />
    <appender-ref ref="LogitAppender" />
</root>
```

Finally open kibana and we will have parsed the messages automatically for you!

