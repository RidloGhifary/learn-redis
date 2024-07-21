# Learn Redis

This repository is designed to help you learn about Redis, a powerful in-memory data store.

## Why Redis?

Redis offers a wide range of data structures and features, making it suitable for various use cases:

- **Caching:** Improve application performance by storing frequently accessed data in memory.
- **Session Management:** Store user sessions efficiently and securely.
- **Real-time Data:** Handle real-time data updates and notifications.
- **Leaderboards and Rankings:** Implement leaderboards and ranking systems.
- **Queues and Pub/Sub:** Build robust messaging and event-driven systems.

## Getting Started

1. **Install Redis:** Follow the instructions for your operating system: [https://redis.io/download](https://redis.io/download)
2. **Start Redis Server:** Run `redis-server` in your terminal.
3. **Connect to Redis:** Use a Redis client library or tool (e.g., `redis-cli`).

### Strings

```sh
# insert and retrieve and delete data on redis
set key value
get key
  - value #this is a command result
del key

# append command: it will replace/update existing key with the value provided, if key key doesn`t exist redis will create it
append key value

# keys command: get all the value with regex pattern
keys key_with_regex
keys data* # redis gives all the value of keys if the key name match with the regex
  - value_data1
  - value_data2
  - value_data2

# getrange command: get value of the key but you can set how many length it will come up, the index start from 0
getrange data1 0 3
  - hell # "hello from redis"

# mget & mset commands: get * set multiple key
mset key1 hallo key2 hallo2 key3 hallo3
mget key1 key2 key3
```

### Expiration

```sh
# expire command: set expiration time on the key, the time will be on seconds
expire data1 60 # data1 will be removed automatically after a minute
setex data10 60 "data10 example" #create key and value with expire set up, will be removed after a minute
ttl data1 # check how many expire second left
```

### Increment & Decrement

```sh
# In order to do increment & decrement, the value should be a number
incr counter # This command do create a key name counter and incremented it into 1, the default value is 0
get counter # -> 1
incr counter # -> 2
decr counter # -> 1

incrby counter 10 # This command do increment the value of the key by the number provided -> 1 + 10 = 11
decr counter 5 # 11 - 5 = 6

set keystr hallo
incr keyst # You`ll get (error) ERR value is not an integer or out of range
```

### Flush

```sh
# flushdb > remove all keys from current database
# flushall > remove all keys from all databases

select 0 # Switch to database 0
mset key1 key1 key2 key2 key3 key3
keys * # Get all of data from database 0

select 1 # Switch to database 0
keys * # -> (empty array)
mset key1 key1 key2 key2 key3 key3
keys * # -> key1, key2, key3
flushdb # remove all the data from database 1

flushall # remove all data from all database
select 0
keys * # -> (empty array) because of you did flushall command
```
