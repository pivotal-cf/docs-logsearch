---
title: Troubleshooting Pivotal Cloud Foundry&reg; Log Search
owner: London Services
---

## No logs on Kibana

There are several reasons for logs not showing on Kibana. Find below some common problems and how to solve it.

<a id="queue-overflow"></a>
### Queue Overflow

#### Possible reasons:

* Not enough parsers: more data coming in that getting out.
* Parsers can't connect to the queue: no data getting out.
* Elasticsearch disks are full: parsers cannot insert new logs.
* Elasticsearch is in a red state: it doesn't accept new data.

#### Detecting a queue overflow:

* Constant increase in memory usage by the queue
* SWAP usage in the queue
* Constant increase in disk usage by the queue
* Queue Persistent Disk is full
* Queue VM is failing

#### The Backup file

The Queue (redis) keeps a backup file on `/var/vcap/store/queue/reddis-appendonly.aof` which contains every operation that happened on it. Once in a while, it will purge redundant entries from the file, keeping it small enough to be loaded by Redis (it purges by removing entries with entries that were removed from the queue).

When the queue is overflowing, it means that there are more data getting into the queue than being removed from it, which makes the backup file larger, and larger. Eventually, the file will be bigger than the available RAM and the queue will fail to start, as redis cannot load such large file in memory. The only recovery is to remove the file and restart the queue with monit:

```
monit restart queue
```

---
