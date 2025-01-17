# screepsmod-mongo

## MongoDB And Redis for the Screeps Private Server

[![JavaScript Style Guide](https://img.shields.io/badge/code_style-standard-brightgreen.svg)](https://standardjs.com)
[![CircleCI](https://circleci.com/gh/ScreepsMods/screepsmod-mongo/tree/master.svg?style=shield)](https://circleci.com/gh/ScreepsMods/screepsmod-mongo/tree/master)

## Requirements

* nodejs 8+ (Current LTS heavily recommended)
* screeps 3.0+
* mongodb 2.6+
* redis 3.0.6+  For Windows installs, you can follow these steps: https://github.com/ServiceStack/redis-windows#option-3-running-microsofts-native-port-of-redis

## Installation

Installing on Ubuntu? Checkout the community guide in the official Docs [Private server on Ubuntu using MongoDB and Redis](http://docs.screeps.com/contributed/ps_ubuntu.html)

1. Ensure both mongodb and redis are already installed and running
2. `npm install screepsmod-mongo` inside your server's mods folder
3. Edit mods.json to point to the index.js such as:

```
  "mods": [
    "node_modules\\screepsmod-mongo\\index.js"
  ],
```

4. Start server!  
5. DB Population
    1. `mongo.importDB()` in the screeps cli imports your existing DB
    2. `system.resetAllData()` in the screeps cli for a completely fresh DB
6. Once done restart the server
7. Done! 

## Usage

With this mod installed you can continue to manage the server as usual,
all CLI commands still function and bahave functionally identical.
The original storage module will still run, but is completely ignored.

Keep in mind that RAM requirements are slightly higher, by default mongo
uses 50% - 1G of your system RAM. Redis on the other hand, uses very little.

Mongo and Redis CLIs can be used to see and modify the data as usual,
backups and restores should be done via normal mongo and redis tools.

https://docs.mongodb.com/manual/tutorial/backup-and-restore-tools/  
https://redis.io/topics/persistence

## Configuration

All options and defaults are listed below

### Mongo

* host: localhost
* port: 27017
* database: screeps
* uri: mongodb://localhost:27017/screeps

If the uri Parameter is supplied it will overwrite all other settings. Use it for Authentication, passing extra options, etc.

### Redis

* host: localhost
* port: 6379

## Examples

Config can be applied in several ways:

### .screepsrc (Recommended)

Add to the bottom of your .screepsrc file
```
[mongo]
host = 192.168.0.222

[redis]
host = 192.168.0.222
```

### ENV Method

Please note that this method only works when launching modules directly, when launched via the default launcher they will be ignored.

```
MONGO_HOST='192.168.0.222'
MONGO_CONN='mongodb://username:password@hostname.com/database_name?ssl=true'
```
