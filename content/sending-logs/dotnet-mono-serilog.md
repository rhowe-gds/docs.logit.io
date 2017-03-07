---
date: 2017-03-06T21:07:13+01:00
title: .NET / Mono - Serilog
---

{{% link text="" url="" %}}

We recommend reading this document in parallel with the {{< link text="Serilog documentation" url="https://github.com/serilog/serilog/wiki/Getting-Started" >}}.

## Installing Serilog

You will need to add the Serilog and Serilog.Sinks.Network packages. This guide will also use appSettings to configure Serilog.

```sh
Install-Package Serilog
Install-Package Serilog.Sinks.Network
Install-Package Serilog.Settings.AppSettings
```

## Configuring Serilog

Add AppSettings to your app.config or web.config. You will need your `Logstash hostname` and `TCP port`. Settings are located in your {{< link text="dashboard" url="https://logit.io/dashboard" >}}, identify the stack you wish to log to, click settings and then logstash.

```
<configuration>
  <appSettings>
    <!-- Level of logging -->
    <add key="serilog:minimum-level" value="Verbose" />
    <!-- Use the TCP Network sink -->
    <add key="serilog:using:TCPSink" value="Serilog.Sinks.Network" />
    <!-- Your logstash configuration -->
    <add key="serilog:write-to:TCPSink.uri" value="YOUR_STACK_ID-ls.logit.io" />
    <add key="serilog:write-to:TCPSink.port" value="YOUR_PORT" />
  </appSettings>
</configuration>
```

## Using Serilog

Create a statically accessible Logger configured from AppSettings.

```cs
Log.Logger = new LoggerConfiguration()
    .ReadFrom.AppSettings()
    .CreateLogger();
```

You can now log from anywhere in your application.

```
Log.Information("The global logger has been configured");
```

## Next steps

Serilog is a fully featured logging framework and has many other capabilities that are not detailed here, please see the {{% link text="Serilog documentation" url="https://github.com/serilog/serilog/wiki/Getting-Started#setup" %}} for more information.
