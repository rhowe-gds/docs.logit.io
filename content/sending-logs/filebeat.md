---
date: 2016-03-08T21:07:13+01:00
title: Filebeat (Recommended)
menu:
  main:
    parent: 'sending-data'
    weight: 0
---

## What is File Beat?

Filebeat is a lightweight data shipper. Filebeat will help you keep things really simple and allows you to ship data directly to Logstash hosted by Logit. They are modular component in your infrastructure, there is no single point of failure.

## Step 1. 

Installing filebeat:

Please see the {{% link text="installation instructions" url="https://www.elastic.co/guide/en/beats/filebeat/current/filebeat-installation.html" %}}

## Step 2.

This step is only required for filebeat v1.3 or less.

```sh
wget https://cdn.logit.io/logit-intermediate.crt -O /etc/pki/tls/certs/logit-intermediate.crt
```

## Step 3.

To configure Filebeat, you will edit the configuration file. For rpm and deb, you’ll find the configuration file at /etc/filebeat/filebeat.yml. For mac and win, look in the archive that you just extracted. There’s also a full example configuration file called filebeat.full.yml that shows all non-deprecated options.

1. Setup the data you wish to send us.

    ```yml
    filebeat:
      prospectors:
        - 
          paths:
            - /var/log/nginx/*.log
            - /var/log/nginx-2/access.log.*
          ignore_older: 3h
          input_type: log
          document_type: nginx-access
    ```

1. We will be shipping to Logstash. _Comment out_ the `Elasticsearch output` configuration.

    ```yml
    ## Comment out elasticsearch output
    #output.elasticsearch:
    #  hosts: ["localhost:9200"]
    ```

1. Find `Logstash output` section. Configure `hosts` to with your `stack id` and `beat port`. We recommend TLS but this is optional. Your configure should look like the below

    ```yml
    output.logstash:
      ## Find your stack ID and port in your dashboard
      hosts: ["STACK_ID-ls.logit.io:BEATS_SSL_PORT"]
      loadbalance: true

      ## The below configuration is used for Filebeat 1.3 or lower
      tls:
        certificate_authorities: ['/etc/pki/tls/certs/logit-intermediate.crt']
        enabled: true
      ##  The below configuration is used for Filebeat 5.0 or higher 
      ssl.enabled: true
    ```

1. Optionally, test your beat. For filebeat on Debian you would run

    ```sh
    # Test filebeat
    /usr/share/filebeat/bin/filebeat -e -c /etc/filebeat/filebeat.yml
    ```

1. Start your beat service. For example with filebeat

    ```sh
# Filebeat on Debian
$ sudo service filebeat restart
# Filebeat on Windows
PS C:\Program Files\Filebeat> Start-Service filebeat
    ```

## Your filebeat configuration file should look like:

#### For Filebeat 5.0 or Higher:

```yml
## Filebeat Configuration Example
filebeat.prospectors:
- paths:
    - /var/log/nginx/*.log
    - /var/log/nginx-2/access.log.*
  ignore_older: 3h
  input_type: log
  document_type: nginx-access

## Optional additional fields or tags
#fields:
#  env: production
#  cluster: usa-prod-1a
#  rack: a1234
#tags: ["enterprise-client-service", "middleware"]

## Send to Logit
output.logstash:
  hosts: ["YOUR-LOGSTASH-ENDPOINT:YOUR-BEATS-SSL-PORT"]
  ssl.enabled: true
```

#### For Filebeat 1.3 or Lower:

```yml
## Filebeat Configuration Example
filebeat.prospectors:
- paths:
    - /var/log/nginx/*.log
    - /var/log/nginx-2/access.log.*
  ignore_older: 3h
  input_type: log
  document_type: nginx-access

## Optional additional fields or tags
#fields:
#  env: production
#  cluster: usa-prod-1a
#  rack: a1234
#tags: ["enterprise-client-service", "middleware"]

## Send to Logit
output.logstash:
  hosts: ["YOUR-LOGSTASH-ENDPOINT:YOUR-BEATS-SSL-PORT"]
  tls:
    certificate_authorities: ['/etc/pki/tls/certs/logit-intermediate.crt']
    enabled: true
```