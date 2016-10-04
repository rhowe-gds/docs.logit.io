---
date: 2016-03-08T21:07:13+01:00
title: Sending logs
menu:
  main:
    weight: 20
---

## Beats

Beats are open source data shippers and one of the easiest / fastest ways to get started. There are many beats available:

Beat | Description
--- | ---
[FileBeat](https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-installation.html) | ilebeat monitors the log directories or specific log files, tails the files, and forwards them
[PacketBeat](https://www.elastic.co/guide/en/beats/packetbeat/current/packetbeat-installation.html) | Packetbeat is a real-time network packet analyzer
[Topbeat](https://www.elastic.co/guide/en/beats/topbeat/current/topbeat-installation.html) | Topbeat is a lightweight shipper  to read system-wide and per-process CPU and memory statistics
[Winlogbeat](https://www.elastic.co/guide/en/beats/winlogbeat/current/winlogbeat-installation.html) | Winlogbeat ships Windows event logs
[apachebeat](https://github.com/radoondas/apachebeat) | Reads status from Apache HTTPD server-status.
[burrowbeat](https://github.com/goomzee/burrowbeat) | Monitors Kafka consumer lag using Burrow.
[cassandrabeat](https://github.com/goomzee/cassandrabeat) | Uses Cassandra's nodetool cfstats utility to monitor Cassandra database nodes and lag.
[cloudtrailbeat](https://github.com/aidan-/cloudtrailbeat) | Reads events from Amazon Web Services' CloudTrail.
[dockbeat](https://github.com/Ingensi/dockbeat) | Reads Docker container statistics and indexes them in Elasticsearch.
[elasticbeat](https://github.com/radoondas/elasticbeat) | Reads status from an Elasticsearch cluster and indexes them in Elasticsearch.
[execbeat](https://github.com/christiangalsterer/execbeat) | Periodically executes shell commands and sends the standard output and standard error to Logstash or Elasticsearch.
[factbeat](https://github.com/jarpy/factbeat) | Collects facts from Facter.
[flowbeat](https://github.com/FStelzer/flowbeat) | Collects, parses, and indexes sflow samples.
[hsbeat](https://github.com/YaSuenag/hsbeat) | Reads all performance counters in Java HotSpot VM.
[httpbeat](https://github.com/christiangalsterer/httpbeat) | Polls multiple HTTP(S) endpoints and sends the data to Logstash or Elasticsearch. Supports all HTTP methods and proxies.
[hwsensorsbeat](https://github.com/jasperla/hwsensorsbeat) | Reads sensors information from OpenBSD.
[jmxproxybeat](https://github.com/radoondas/jmxproxybeat) | Reads Tomcat JMX metrics exposed over JMX Proxy Servlet to HTTP.
[journalbeat](https://github.com/mheese/journalbeat) | Used for log shipping from systemd/journald based Linux systems.
[lmsensorsbeat](https://github.com/eskibars/lmsensorsbeat) | Collects data from lm-sensors (such as CPU temperatures, fan speeds, and voltages from i2c and smbus).
[mysqlbeat](https://github.com/adibendahan/mysqlbeat) | Run any query on MySQL and send results to Elasticsearch.
[nagioscheckbeat](https://github.com/PhaedrusTheGreek/nagioscheckbeat) | For Nagios checks and performance data.
[nginxbeat](https://github.com/mrkschan/nginxbeat) | Reads status from Nginx.
[nginxupstreambeat](https://github.com/2Fast2BCn/nginxupstreambeat) | Reads upstream status from nginx upstream module.
[openconfigbeat](https://github.com/aristanetworks/openconfigbeat) | Streams data from OpenConfig-enabled network devices.
[packagebeat](https://github.com/joehillen/packagebeat) | Collects information about system packages from package managers.
[phpfpmbeat](https://github.com/kozlice/phpfpmbeat) | Reads status from PHP-FPM.
[pingbeat](https://github.com/joshuar/pingbeat) | Sends ICMP pings to a list of targets and stores the round trip time (RTT) in Elasticsearch.
[redisbeat](https://github.com/chrsblck/redisbeat) | Used for Redis monitoring.
[retsbeat](https://github.com/consulthys/retsbeat) | Collects counts of RETS resource/class records from Multiple Listing Service (MLS) servers.
[saltbeat](https://github.com/martinhoefling/saltbeat) | Reads events from salt master event bus.
[twitterbeat](https://github.com/buehler/go-elastic-twitterbeat) | Reads tweets for specified screen names.
[udpbeat](https://github.com/gravitational/udpbeat) | Ships structured logs via UDP.
[unifiedbeat](https://github.com/cleesmith/unifiedbeat) | Reads records from Unified2 binary files.
[uwsgibeat](https://github.com/mrkschan/uwsgibeat) | Reads stats from uWSGI.
[wmibeat](https://github.com/eskibars/wmibeat) | Uses WMI to grab your favorite, configurable Windows metrics.

To get started with any beat perform the following steps.

1. Install the beat using the specific installation instructions.
1. Follow the specific beat configuration guide.

1. Comment out or remove, the lines found below, ### Elasticsearch as output

    ```sh
    #elasticsearch:
    #hosts: ["localhost:9200"]:
    ```

2. Download the Certificate to a path or your choice (e.g. /etc/ssl/certs or /etc/pki/tls/certs):

    ```
    wget https://cdn.logit.io/logit-intermediate.crt -O /etc/ssl/certs/logit-intermediate.crt
    ```

3. Under `### Logstash as output` either configure TLS or non-TLS

    ```sh
    ### Logstash as output with TLS
      logstash:
        hosts: ["YOUR-LOGSTASH-ENDPOINT:YOUR-BEATS-SSL-PORT"]
        compression_level: 3
        tls:
          # List of root certificates for HTTPS server verifications
          certificate_authorities: ["/etc/ssl/certs/logit-intermediate.crt"]
    ```

    ```sh
    ### Logstash as output without TLS
    logstash:
      hosts: ["YOUR-LOGSTASH-ENDPOINT:YOUR-BEATS-PORT"]
      compression_level: 3
    ```

4. Now restart your beat service so the changes take effect. For example:

    ```
    # Filebeat on Debian
    $ sudo /etc/init.d/filebeat restart
    # Filebeat on Windows
    PS C:\Program Files\Filebeat> Start-Service filebeat
    ```

Your full filebeat.yml file should look similar to this example file.

```
################### Filebeat Configuration Example #########################
############################# Filebeat ######################################
filebeat:
  prospectors:
    -
      paths:
        - /var/log/nginx/access.log
        - /var/log/nginx/access.log.*

      ignore_older: 24h
      input_type: log
      document_type: nginx-access
    -
      paths:
        - /var/log/apache2/access.log

      ignore_older: 24h
      input_type: log
      document_type: apache

  registry_file: /var/lib/filebeat/registry

output:
### Logstash as output
  logstash:
    hosts: ["YOUR-LOGSTASH-ENDPOINT:YOUR-BEATS-SSL-PORT"]
    compression_level: 3
    tls:
      # List of root certificates for HTTPS server verifications
      certificate_authorities: ["/etc/ssl/certs/logit-intermediate.crt"]
shipper:
logging:
  files:
    rotateeverybytes: 10485760 # = 10MB
```

## Windows

To set up the windows agent just follow the steps below:

Copy your API Key from your [dashboard] (https://logit.io/Dashboard)

[Download our Agent] (https://logit.io/LogitAgent.exe)

Stay on this page and install the Agent on your server, follow the install wizard, dont forget your API Key!

Once installed we will show a sucess message if you dont see this please check the event logs on the server

## Heroku

To send us a logs all you need to do is:

```sh
heroku drains:add https://api.logit.io/heroku?apikey=YOUR-API-KEY -a appname
```

We automatically parse the logs into a structured format for you so all you need to do it analyse them

For more information see the heroku site: [Log Drains] (https://devcenter.heroku.com/articles/log-drains#https-drains)

## AppHarbour

To send us a logs all you need to do is add this endpoint as a logdrain in your appharbor account:
```sh
https://api.logit.io/appharbor?apikey=YOUR-API-KEY
```

We automatically parse the logs into a structured format for you so all you need to do it analyse them

For more information see the Appharbor site: [Log Drains] (https://support.appharbor.com/kb/tips-and-tricks/logging) or visit the Logplex HTTP Drains docs in github [HTTP Drains] (https://github.com/heroku/logplex/blob/master/doc/README.http_drains.md)

## Http

To send us a log all we required is:

* Valid JSON content
* ApiKey sent in the headers for ease
* Content type set to application/json
* You can POST or PUT your data
If you want to try it out copy this below and send it in!

```sh
curl -i -H "ApiKey: YOUR-API-KEY" -i -H "Content-Type: application/json" http://api.logit.io/v2 -d '{"test":"test","example": { "a": 1, "b": 2 } }'
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

Quickstart snippet

```html
<script src="https://resources.logit.io/logit.js"></script>
<script>
    window.logit.init(apiKey, options);
    logit.emergency(message, dimension);
</script>
```

To install with bower and for more library options checkout our github repo [here] (https://github.com/logit-io/javascript-logitio).
Issues and pull requests welcome!

## Node

Our repository and instructions can be found [here] (https://github.com/logit-io/node-logitio)

## Syslog

A syslog endpoint has been created for you in your logstash input config.

Click the configuration link on the stack you wish to log too in your [dashboard] (https://logit.io/Dashboard).

Your logstash endpoint link and input configuration input is written out for you. Note you can send syslog over udp or tcp.
