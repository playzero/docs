# docs

# ZERO.IO infrastructure blueprint
*This is a document in continuous transition to reflect ongoing development of zero.io.*

## TL;DR
### I N F R A S T R U C T U R E  
#### development

rabbitmq event bus
```docker run -d -p 4369:4369 -p 5671:5671 -p 5672:5672 -p 15671:15671 -p 15672:15672 -p 25672:25672 --hostname zero-rabbitmq --name zero-rabbitmq rabbitmq:3-management```

standard management port: 15672, default username and password: guest/guest

redis user session storage
```docker run -d --name zero-redis-sessions -p 6379:6379 -d redis:alpine```

with persistent storage:
```docker run -d -v /my/own/datadir:/data/redis --name zero-redis-sessions -p 6379:6379 -d redis:alpine```

mongodb
```docker run -d --name zero-mongodb -p 27017:27017 mongo```

with persistent storage:
```docker run -d -v /my/own/datadir:/data/mongo --name zero-mongodb -p 27017:27017 mongo```


elasticsearch
```docker run -d -p 9200:9200 -p 9300:9300 --name zero-elasticsearch elasticsearch:latest```

persistent storage:
1. Create a mountable data directory <data-dir> on the host.
2. Create Elasticsearch config file at <data-dir>/elasticsearch.yml.
```yml
path:
  logs: /data/log
  data: /data/data
```
3. Start a container by mounting data directory and specifying the custom configuration file:
```sh
docker run -d -p 9200:9200 -p 9300:9300 -v <data-dir>:/data dockerfile/elasticsearch /elasticsearch/bin/elasticsearch -Des.config=/data/elasticsearch.yml
```

C O N T R A C T S

listen to contract events
NPM		https://github.com/simon991/ethereum-event-listener
SO		https://ethereum.stackexchange.com/questions/3780/how-can-i-create-a-listener-for-new-transaction-with-ethereum-rpc-calls
WEB3	https://ethereum.stackexchange.com/questions/21048/listen-to-blockchain-events-in-js

run local testnode
https://github.com/ethereumjs/testrpc
#### production
tbd

### C O N T R A C T S

listen to contract events
NPM		https://github.com/simon991/ethereum-event-listener
SO		https://ethereum.stackexchange.com/questions/3780/how-can-i-create-a-listener-for-new-transaction-with-ethereum-rpc-calls
WEB3	https://ethereum.stackexchange.com/questions/21048/listen-to-blockchain-events-in-js

run local testnode
https://github.com/ethereumjs/testrpc



## Overview

- Components and architecture

### Components and Architecture

The following components and services will be combined to create an environment for ongoing development, testing, deployment.

####Docker
.

####Ethereum TestNet
.

####Elasticsearch
Elasticsearch is a distributed, RESTful search and analytics engine capable of solving a growing number of use cases. As the heart of the Elastic Stack, it centrally stores your data so you can discover the expected and uncover the unexpected.

####PostgreSQL
.

####AMQP Event Bus
AMQP provides a platform-agnostic method for ensuring information is safely transported between applications, among organisations, within mobile infrastructures, and across the Cloud. AMQP is used in areas as varied as financial fryont office trading, ocean observation, transportation, smart grid, computer-generated animation, and online gaming. Many operating systems include AMQP implementations, and many application frameworks are AMQP-aware. There are Cloud-hosted offerings of AMQP, and it is embedded in virtualisation infrastructure.
