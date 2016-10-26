---
author: admin
comments: true
date: 2013-10-13 14:24:25+00:00
layout: post
link: http://www.lambdacurry.com/2013/10/quick-and-dirty-nosql-cheatsheet/
slug: quick-and-dirty-nosql-cheatsheet
title: Quick and dirty NoSQL cheatsheet
wordpress_id: 834
categories:
- technology
---




 **Mongodb**




data-model_: _











	
  * document-oriented database - not key-value database

	
  * maximum value size is 16mb kept in the BSON binary format.

	
  * for any sharded or clustered setup, all reasonable queries must happen through map-reduce rather than the query framework.










performance:











	
  * biggest con is the database level write lock, which starts impacting fairly quickly as your data size grows.

	
  * must finely tune indexes for performance - all other queries must happen through map-reduce.










replication and clustering: Master/slave replication with datacenter level failover ([http://docs.mongodb.org/manual/data-center-awareness/](http://docs.mongodb.org/manual/data-center-awareness/))







CAP tradeoffs:











	
  * MongoDB tunes for consistency over availability - via its locking and a single master for accepting writes.

	
  * There is no versioning.










consistency:











	
  * warning: default configuration does not acknowledge write and is the reason for its performance. on turning on acknowledged writes, performance  drops to be same or worse as other nosql systems.













**Couchbase**




data-model_: _








	
  * document-oriented database - not key-value database

	
  * biggest pro - memcached compliant api.

	
  * You can store values up to 1 MB in memcached buckets and up to 20 MB in Couchbase buckets. Values can be any arbitrary binary data or it can be a JSON-encoded document.







Performance:











	
  * uses indexes called "views" for performance.





Replication and clustering:











	
  * master-slave replication. All writes must happen on the master.










 




CAP tradeoffs:











	
  * prefers consistency over availability. all writes go to single master.

	
  * biggest con: Has eventual persistence - Writes are *not* flushed to disk immediately for performance (kept in RAM).













consistency:











	
  * does not support transactions or MVCC. it is ACID compliant on a single operation, however eventual persistence means that data can still be lost.



















**CouchDB+BigCouch**




data-model_: _document-oriented database - not key-value database




replication and clustering: master-master replication as well as the most seamless cluster setup among all nosql (bigcouch merged into couchdb)







performance:








	
  * CouchDB allows for creation of indexes on separate disks (SSD?) called "views" that speeds up queries by many orders of magnitude.

	
  * biggest con - only access is through an inbuilt REST api which adds about 100ms to each request. All data interchange is through JSON which means performance for large documents will suffer (due to serialization)

	
  * queries are implicitly map-reduce.

	
  * relies on page-cache for performance.







consistency: biggest pro is that it has built in MVCC and transactions, so there will *never* be race conditions between read and write.




CAP tradeoffs:











	
  * prefers availability to consistency - especially in its multi-datacenter setup. All checks and balances happen through revision numbers that means disk usage increases pretty fast (due to previous revision numbers).

	
  * needs periodic compaction to clean up.
















**Cassandra**




data-model_: _











	
  * key-value database   - not document-oriented database

	
  * 2GB column value. maximum number of cells in a single partition is 2 billion. however different partitions can be on different machines/vms.










replication and clustering:  Cassandra is aware of network topology and does cross-datacenter replication fairly robustly among all the nosql systems ([http://www.datastax.com/docs/0.8/cluster_architecture/cluster_planning](http://www.datastax.com/docs/0.8/cluster_architecture/cluster_planning))










Performance:











	
  * Cassandra tends to sacrifice read performance in order to improve write performance. Because of the log structured design of Cassandra, a single row is spread across multiple sstables. Reading one row requires reading pieces from multiple sstables. However, this comes with a much, much higher fine tuning control on disk layout and data locality.

	
  * Cassandra also relies on OS page cache for caching the index entries.

	
  * 

Consistency:











	
  * Cassandra does not offer fully ACID-compliant transactions, however the cluster itself can audit success/failure. For example, if using a write consistency level of QUORUM with a replication factor of 3, Cassandra will send the write to 2 replicas. If the write fails on one of the replicas but succeeds on the other, Cassandra will report a write failure to the client. However, the write is not automatically rolled back on the other replica. However, your application does get to know the failure condition.

	
  * There are no locks

	
  * no MVCC - Cassandra uses timestamps to determine the most recent update to a column. The timestamp is provided by the client application. The latest timestamp always wins when requesting data, so if multiple client sessions update the same columns in a row concurrently, the most recent update is the one that will eventually persist.













CAP tradeoffs:











	
  * Cassandra supports tuning between availability and consistency, and always gives you partition tolerance. Cassandra can be tuned to give you strong consistency in the CAP sense where data is made consistent across all the nodes in a distributed database cluster. A user can pick and choose on a per operation basis how many nodes must receive a DML command or respond to a SELECT query.

	
  * Writes in Cassandra are durable. All writes to a replica node are recorded both in memory and in a commit log before they are acknowledged as a success. If a crash or server failure occurs before the memory tables are flushed to disk, the commit log is replayed on restart to recover any lost writes.









