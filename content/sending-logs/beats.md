---
date: 2016-03-08T21:07:13+01:00
title: Beats
menu:
  main:
    parent: 'sending-data'
    weight: 10
---

## What are Beats?

Beats are open source data shippers and one of the easiest / fastest ways to get started. There are many beats available:

Beat | Description
--- | ---
[FileBeat](https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-installation.html) | Filebeat monitors the log directories or specific log files, tails the files, and forwards them
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

## Install and configure

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

## Example configuration file

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
