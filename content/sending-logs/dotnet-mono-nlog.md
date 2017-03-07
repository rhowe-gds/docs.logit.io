---
date: 2017-03-06T21:07:13+01:00
title: .NET / Mono - NLog
---

We recommend reading this document in parallel with the {{< link text="NLog documentation" url="https://github.com/NLog/NLog/wiki" >}}.

## Installing NLog

You will need to add the NLog, NLog.Schema and NLog.Config packages. This command will install the required dependencies.

```sh
Install-Package NLog.Config
```

## Configuring NLog

Configuring NLog can be done in your application `app.config` or `web.config`. You will need your `Logstash hostname` and `TCP port`. Settings are located in your {{< link text="dashboard" url="https://logit.io/dashboard" >}}, identify the stack you wish to log to, click settings and then logstash.

```
<configuration>
  <configSections>
    <section name="nlog" type="NLog.Config.ConfigSectionHandler, NLog" />
  </configSections>
  <nlog throwExceptions="true">
    <targets>
      <target
        type="Network"
        name="LogitTarget"
        address="tcp://STACK_ID-ls.logit.io:STACK_TCP_PORT"
        newLine="True">
        <layout type="JsonLayout">
          <attribute name="timestamp" layout="${longdate}" />
          <attribute name="logger" layout="${logger}" />
          <attribute name="machinename" layout="${machinename}" />
          <attribute name="threadid" layout="${threadid}" />
          <attribute name="level" layout="${level}"/>
          <attribute name="message" layout="${message}" />
          <attribute name="exception" layout="${exception}" />
        </layout>
      </target>
    </targets>
    <rules>
      <logger name="*" minlevel="Trace" writeTo="LogitTarget" />
    </rules>
  </nlog>
</configuration>
```

## Using NLog

In order to emit log message you can simply call one of the methods on the `Logger`.

```
using NLog;

public class MyClass
{
  private static Logger logger = LogManager.GetCurrentClassLogger();

  public void MyMethod1()
  {
    logger.Info("Sample trace message");
  }
}
```

## Next steps

NLog is a fully featured logging framework and has many other capabilities that are not detailed here, please see the {{% link text="NLog documentation" url="https://github.com/NLog/NLog/wiki" %}} for more information.

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
