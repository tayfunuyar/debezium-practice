Kafka Broker - localhost:9092
Zookeeper - localhost:2181
Postgres - localhost:5432
Debezium Connector - localhost:8083
Schema Registry - localhost:8081
Debezium UI - localhost:8080
Kafka Ui - localhost:8084 
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
    "database.dbname": "db_name",
    "database.history.kafka.bootstrap.servers": "kafka:9092",
    "database.history.kafka.topic": "schema-changes.table_name",
    "database.hostname": "postgres",
    "database.password": "postgres",
    "database.port": "5432",
    "database.server.name": "postgres",
    "database.user": "postgres",
    "name": "table_name-db-connector",
    "plugin.name": "pgoutput",
    "table.include.list": "public.table_name",
    "tasks.max": "1",
    "topic.creation.default.cleanup.policy": "delete",
    "topic.creation.default.partitions": "1",
    "topic.creation.default.replication.factor": "1",
    "topic.creation.default.retention.ms": "604800000",
    "topic.creation.enable": "true",
    "topic.prefix": "postgres"
  },
  "name": "table_name-db-connector",
  "tasks": [],
  "type": "source"
}
````