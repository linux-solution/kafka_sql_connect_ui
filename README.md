# kafka_sql_connect_ui
Kafka SQL connect UI docker composer
This docker composer file automatically deploy the kafka sql connect services and monitoring UI.

## Running Kafka connect and monitoring UI services
```
docker-compose -f sql_connect_ui.yml up
```

## Start MySQL connector
```
curl -i -X POST -H "Accept:application/json" -H  "Content-Type:application/json" http://localhost:8083/connectors/ -d @register-mysql.json
```

## Start SQL Server connector
```
curl -i -X POST -H "Accept:application/json" -H  "Content-Type:application/json" http://localhost:8083/connectors/ -d @register-sqlserver.json
```
