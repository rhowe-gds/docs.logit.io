---
date: 2017-03-06T21:07:13+01:00
title: .NET / Mono - log4net
---

We provide a log4net appender. We recommend reading this document in parallel with the {{< link text="log4net documentation" url="https://logging.apache.org/log4net/" >}}.

## Installing log4net and Logit appender

```
Install-Package log4net
Install-Package log4net.Logit
```

## Configuring log4net

Configuring log4net can be done in your application `app.config`, `web.config` or specific log4net configuration file. You will configure the log4net appender. You will need your `API key`. Settings are located in your {{< link text="dashboard" url="https://logit.io/dashboard" >}}, identify the stack you wish to log to, click settings and then logstash.

```
<appender name="LogitAppender" type="log4net.Logit.LogitAppender, log4net.Logit">
    <apikey value="YOUR-API-KEY" />
    <layout type="log4net.Layout.PatternLayout">
        <conversionpattern value="%property{log4net:HostName} %-5p %d %5rms %-22.22c{1} %-18.18M - %m%n" />
    </layout>
</appender>
...
<root>
    <level value="ALL" />
    <appender-ref ref="LogitAppender" />
</root>
```

## Next steps

#### log4net documentation	

log4net is a logging framework and has many other capabilities that are not detailed here, please see the {{% link text="log4net documentation" url="https://logging.apache.org/log4net/" %}} for more information.

#### Strutured event data

If you wish to visualise your data in Kibana it may need to be structured. log4net support for structured data is limited. You may need to create filters in logstash to parse and structure log message.

For example if you consider the below log line.

```sh
2017-01-10 12:53:48,062 [1216] INFO  DbQueryRunner  - SELECT query ... took 132ms.
```

If you wish to visualise the time taken in graphs and metrics, elasticsearch will need to store the millisecond value in a numeric datatype field. This could be achieved with the following filer.

```
filter
{
  if [type] == "log4net"
  {
    # Capture DbQueryRunner time taken
    if [message] =~ /took ([\d]+)ms/ {
      grok {
        match => { "message" => "took (?<query_timetaken>([\d]+))ms" }
        mutate {
          convert => { "query_timetaken" => "integer" }
        }
      }
    }
  }
}
```
