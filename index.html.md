---
title: Pivotal Cloud Foundry&reg; Log Search
owner: London Services
---

This is documentation for the [Pivotal Cloud Foundry Log Search](https://network.pivotal.io/products/logsearch) tile; which deploys
an Elastic ELK stack customised for analysing the logs of interest to Operators from other PCF tiles.

## Product snapshot

<dl>
<dt>Current [Pivotal Cloud Foundry Log Search](https://network.pivotal.io/products/logsearch) Details</dt>
<dd><strong>Version</strong>: v0.8-alpha </dd>
<dd><strong>Release Date</strong>: March 2016</dd>
<dd><strong>Software component version</strong>: Elasticsearch 2.2.0, Logstash 2.2.0, Kibana 4.4.0, Redis 2.8.4</dd>
<dd><strong>Compatible Ops Manager Version(s)</strong>: 1.7.x</dd>
<dd><strong>Compatible Elastic Runtime Version(s)</strong>:  1.7.x</dd>
<dd><strong>vSphere support?</strong> Yes</dd>
<dd><strong>AWS support?</strong> Yes</dd>
</dl>

## Resource requirements for Pivotal Cloud Foundry&reg; Log Search

These are the default resource and IP requirements for installing the tile:

| Component     | Job                                                         | Instances | CPU | Ram   | Ephemeral | Persistent |
|---------------|-------------------------------------------------------------|-----------|-----|-------|-----------|------------|
| Elasticsearch | Elasticsearch master node(s)                                | 1         | 2   | 4096  | 4096      | 32000      |
| Elasticsearch | Elasticsearch data nodes                                    | 2         | 2   | 32000 | 4096      | 500000     |
| Redis         | Queue                                                       | 1         | 2   | 16000 | 4096      | 32000      |
| Logstash      | Log parser                                                  | 4         | 1   | 4096  | 4096      | 0          |
| Logstash      | Ingestor                                                    | 1         | 2   | 2048  | 4096      | 0          |
| HAProxy       | Router                                                      | 1         | 2   | 1024  | 4096      | 0          |
| Kibana        | Kibana                                                      | 1         | 1   | 1024  | 4096      | 0          |
| Curator       | Maintenance                                                 | 1         | 1   | 1024  | 4096      | 0          |
| Curl          | Enable Shard Allocation (errand)                            | 1         | 1   | 1024  | 4096      | 0          |
| Tar, gzip     | Compiliation (only during initial install)                  | 4         | 2   | 1024  | 4096      | 0          |
| All           | Monitor                                                     | 0         | 2   | 32000 | 4096      | 500000     |


## Further Reading

* [Official Elastic Elasticsearch 2.2.0 Documentation](https://www.elastic.co/guide/en/elasticsearch/reference/2.2/index.html)
* [Official Elastic Logstash Documentation](https://www.elastic.co/guide/en/logstash/2.2/index.html)
* [Official Elastic Kibana 4.4 Documentation](https://www.elastic.co/guide/en/kibana/4.4/index.html)
