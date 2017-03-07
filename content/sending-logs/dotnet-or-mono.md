---
date: 2016-03-08T21:07:13+01:00
title: .NET / Mono logging
menu:
  main:
    parent: 'sending-data'
    weight: 20
---

You can ship logs from .NET and MONO applications using common logging frameworks. We have documentation for Serilog, NLog and log4net.

- [Serilog configuration]({{< relref "dotnet-mono-serilog.md" >}})
- [NLog configuration]({{< relref "dotnet-mono-nlog.md" >}})
- [log4net configuration]({{< relref "dotnet-mono-log4net.md" >}})

{{% well %}}
*I'm choosing a framework, which should I use?*

We recommend Serilog as it has structured logging support.

*I can't use Serilog, NLog or log4net!*

If you are not using a framework listed above there are a number of options you can consider

- Log to file and use [Filebeat]({{< relref "filebeat.md" >}}) to ship logs
- Modify logging framework to output to [HTTP]({{< relref "http.md" >}})
- Modify logging framework to output to TCP
{{% /well %}}
