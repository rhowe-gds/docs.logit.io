---
date: 2016-03-09T00:11:02+01:00
title: Security
menu:
  main:
    weight: 30
---

We understand that trusting a 3rd party with your data or your customers data is an important decision. We take the responsibility of protecting your data extremely seriously.

If you have any questions, queries or security concerns, please do not hesitate to get in touch with us at <support@logit.io>

## High security data centres

* Systems are hosted data centers managed by OVH.
* Physical access is strictly controlled.
* Data centers employ onsite security staff, video surveillance, and intrusion detection systems.
* Access rights are reassessed regularly, according to remit.

For more information see https://www.ovh.co.uk/aboutus/security.xml

## System and operational security

* Systems access logged and tracked for auditing purposes.
* Regular system patching processes to provide ongoing protection from exploits.
* Firewall to prohibit unauthorised system access.

## File systems and communication

All access to the Logit website, Kibana and Elasticsearch HTTP API is restricted to HTTPS encrypted connections.

Logit use federated authentication and therefore do not store user passwords. We encourage users to add two-factor authentication to their Google or GitHub accounts.

Data you log may include passwords, we will endeavour to identify this and inform you. Where possible, and with your agreement, we will add Logstash configuration to remove passwords and other sensitive data.

While we encourage all customers to use encryption, it is possible to send data to Logstash unencrypted. We will endeavour to identify this, inform you and assist you in making all data transfer secure. We accept that there will be situations where this is not practically feasible and rely entirely on your judgement in these circumstances.

We do not encrypt data on disk because it would not increase security. Elasticsearch instances and employees would need to decrypt the indexes on demand, slowing down updates and page response times. Any user with shell access to the file system would have access to the decryption routine, thus negating any security it provides. Therefore, we focus on making our machines and network as secure as possible.

Elasticsearch indexes are stored on Logit’s production servers until deleted by the user. This will be done by the retention policies, directly using the Elasticsearch HTTP API or by request. We do not store any other copy of your data unless you have requested Elasticsearch index snapshots or 3rd party offsite replication direct from Logstash. Where data is replicated to 3rd party systems, we will not delete data and leave this management to you.

## Employee access

No Logit employee will access your data unless required for support reasons. The majority of support requests require Logit employees to access your data, for example to test Logstash configuration is working. We will not ask you each time we require access as this would be impractical.  We may also access your data when responding to a critical security issue or suspected abuse.

When working a support issue we do our best to respect your privacy as much as possible, we only access the minimum files and settings needed to resolve your issue.

Finally, it's worth noting that Logit's staff is quite small, limiting the number of individuals who would provide you support.

## Credit card safety

When you purchase a Logit subscription, your credit card data is not transmitted through nor stored on our systems. Instead, we depend on Stripe, a company dedicated to this task. Stripe is certified to PCI Service Provider Level 1, the most stringent level of certification available.

For more information see https://stripe.com/docs/security
