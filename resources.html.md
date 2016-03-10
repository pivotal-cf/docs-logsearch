---
title: Pivotal Cloud Foundry&reg; Log Search
owner: London Services
---

# Resource requirements for Pivotal Cloud Foundry&reg Log Search;

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

