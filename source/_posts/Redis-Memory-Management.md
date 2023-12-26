---
title: Redis Memory Management
date: 2023-12-26 16:31:03
tags:
---


## Key Expiration

Redis allows to set an expiration time for keys using the `EXPIRE` command or by providing a TTL (Time-to-Live) value when setting the key.
This feature is beneficial for managing data expiration and automatic cleanup, saving storage space, and improving performance.
Also, there is some data only valid for a period of time, i.e. verify code, login token, etc.

Redis has another dictionary(hashtable) for saving expiration time of keys, which stores unix timestamps in milliseconds (`long long` data type).

{% asset_img redis-expired-dictionary.png Redis Expires Dictionary %}

<!-- more -->

Key removal mechanism is semi-lazy.
Redis keys are expired in two ways, passive, and active way:

A key is passively expired simply when some client tries to access it, and the key is found to be timed out.
But if a key is never accessed, it just takes up memory for no reason.

Redis added a second layer of expiration. It reads random keys periodly, and if an expired key is touched, it is deleted by the lazy mechanism as above.
Specifically what Redis does 10 times per second (hz):
1. Test 20 random keys from the set of keys with an associated expire.
2. Delete all the keys found expired.
3. If more than 25% of keys were expired, start again from step 1.

{% asset_img redis-ttl-mechanism.drawio.png Active Expiration Loop %}

Obviously, active way benefits memory and passive way benefits CPU.
Redis uses mixed strategy to optimize memory usage.

## Max Memory Policy

Though there is expire mechanism, it is still possible to fill up memory with keys.
We need `Eviction Policies` to determine the behavior Redis follows when the `maxmemory` limit is reached.

The following policies are available:
 + `noeviction`: New values are not saved when memory limit is reached. When a database uses replication, this applies to the primary database
 + `allkeys-lru` (most common): Removes least recently used (LRU) keys
 + `allkeys-lfu`: Removes least frequently used (LFU) keys
 + `volatile-lru`: Removes least recently used keys with the expire field set to true.
 + `volatile-lfu`: Removes least frequently used keys with the expire field set to true.
 + `allkeys-random`: Randomly removes keys to make space for the new data added.
 + `volatile-random`: Randomly removes keys with expire field set to true.
 + `volatile-ttl`: Removes keys with expire field set to true and the shortest remaining time-to-live (TTL) value.
 
The policies `volatile-lru`, `volatile-lfu`, `volatile-random`, and `volatile-ttl` behave like `noeviction` if there are no keys to evict matching the prerequisites (no keys with expiration time).

The best practice is NOT to trigger max memory policy by managing keys with proper TTL, monitoring and analyzing memory usage.

# Reference
> https://javaguide.cn/database/redis/redis-questions-01.html
> https://redis.io/docs/
> https://stackoverflow.com/questions/36172745/how-does-redis-expire-keys
