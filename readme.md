## Debezium and Postgres with Kafka extra inc. Kafka Ui 
* Kafka Broker - localhost:9092
* Zookeeper - localhost:2181
* Postgres - localhost:5432
* Debezium Connector - localhost:8083
* Schema Registry - localhost:8081
* Debezium UI - localhost:8080
* Kafka Ui - localhost:8084 
````
docker compose -f docker-compose.yml up -d
````


## Configure Postgres Connector

````
curl -X POST --location "http://localhost:8083/connectors" -H "Content-Type: application/json" -H "Accept: application/json" -d @connector.json
````

````
{
  "config": {
    "connector.class": "io.debezium.connector.postgresql.PostgresConnector",
    "database.dbname": "debezium",
    "database.history.kafka.bootstrap.servers": "kafka:9092",
    "database.history.kafka.topic": "schema-changes.projects",
    "database.hostname": "postgres",
    "database.password": "postgres",
    "database.port": "5432",
    "database.server.name": "postgres",
    "database.user": "postgres",
    "name": "debezium-connector",
    "plugin.name": "pgoutput",
    "table.include.list": "public.projects",
    "tasks.max": "1",
    "topic.creation.default.cleanup.policy": "delete",
    "topic.creation.default.partitions": "1",
    "topic.creation.default.replication.factor": "1",
    "topic.creation.default.retention.ms": "604800000",
    "topic.creation.enable": "true",
    "topic.prefix": "postgres"
  },
  "name": "debezium-connector"
}

````
## Configs 
### Kafka Ui Config 
![kafka-ui.png](assets%2Fkafka-ui.png)
### Create Debezium Connector
![connector-create.png](assets%2Fconnector-create.png)
![debezium-connector.png](assets%2Fdebezium-connector.png)
## Debezium Changes Sync with Kafka
![debezium-table.png](assets%2Fdebezium-table.png)
