---
date: 2016-03-08T21:07:13+01:00
title: Other Beats
menu:
  main:
    parent: 'sending-data'
    weight: 10
---

## What are Beats?

Beats are open source lightweight data shippers. They are the easy, fast and reliable way to ship data. Each beat is a single-purpose data shipper. You can install and run as many as required. They all share libbeat to ship data directly to Logstash hosted by Logit. They are modular component in your infrastructure, there is no single point of failure.

[How to Configure Beats]({{< relref "filebeat.md#step-3" >}})

Below are a list of beats.

Name | Description
--- | ---
[filebeat](https://www.elastic.co/products/beats/filebeat) | Ship log files
[packetbeat](https://www.elastic.co/products/beats/packetbeat) | Ship network data
[metricbeat](https://www.elastic.co/products/beats/metricbeat) | Ship metrics from systems and services
[winlogbeat](https://www.elastic.co/products/beats/winlogbeat) | Winlogbeat ships Windows event logs
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
