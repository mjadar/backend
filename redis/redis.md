# REDIS

## Sommaire

- What is Redis? Use Cases && Benefits of Redis
- Why Redis is suitable for microservices apps?
- How redis supports multiple data formats
- Data persistence and recovery with redis
- How to optimize memory cost with redis
- Scaling redis && High availability accross multiple geographic locations

## What is Redis? Use Cases && Benefits of Redis

- Remote Dictionary Server
- In-Memory Datase (Fast and performant, faster tests)
- Data is stored on computer's memory
- often used as Cache to improve performance
- Redis is a Multi-Model Database
- Less complex, no need to implement a caching layer

## Benefits of Multi-Model DB (redis)

- run and maintain just 1 DB.
- requires only one programmatic interface for that data service.
- reduce latency by eliminating several internal network hubs
- useful in case of microservices that run different types of db (cache, graph, elasticsearch)

## How redis supports multiple data formats?

- You have Redis core which is a key value store, and you can extend that core with modules for different data types which your application needs. (RediSearch, RedisJson, RedisGraph)
- It is modular.

## Data Persistence and Durability

1- Snapshotting (RDB) = produces single-file point-in-time snapshots of your dataset.
2- Append Only File (AOF) = Logs every write operation continuoulsy; So when restarting Redis, it will re-play the AOF to rebuild the state. (More durable, but slower than snapshots)

- **Where are these persistence files stored?**
  - Separate Persistent Storage from Data Service

## How to optimize memory cost with Redis?

- with `Redis on Flash`
- [Standard] : Store everything on RAM.
- [Redis_on_Flash] :
  - Store frequently used values on RAM.
  - Store infrequently used values on SSD.
- so redis also use the underlying infrastructure resources and save infrastructure costs.

## How to scale redis DB?

- supports clustering:
  - one master (to read/write) and many replicas (to read)
  - like this you can handle more requests
  - assure high availability
  - all replicas will hold complete copies of Primary instance's data.
  - distribute replicas among multiple servers
- Supports sharding:
  - divide your datasets into smaller shards
  - split n shards each of them is responsible for read:write of a certain data, and like this you can distribute shards into smaller nodes.
  - each shard needs less memory.
- but you need to run and maintain these Redis clusters.

## Scaling Redis and high availability

- `Users geographically distributed` : distribute our data service close to the users.
- `Disaster recovery` : switch over to another data center, when one goes down.
- [+] Replicas of Redis cluster in different regions
- [+] data should be replicated to all clusters
- [+] each cluster should be able to accept reads/writes

## How does redis resolve changes in the same dataset, and ensure data consistency?

- use concept called CRDT (conflict-free replicated data types)
- resolve any conflict automatically at DB level without data loss
- so redis have mechanism to merge the changes that you have to the same DB from multiple sources.
