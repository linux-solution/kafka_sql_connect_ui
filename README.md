# Kafka SQL connect UI docker composer

This docker composer file automatically deploy the kafka sql connect services and monitoring UI.

## Running Kafka connect and monitoring UI services
```
docker-compose -f docker-compose.yml up
```
*This will display the log which shows how the services are working and will be broken down if you show down the terminal or send a terminate signal.*
*To run this composer in the background and prevent the unexpected terminate, give the -d option*
```
docker-compose -f docker-compose.yml up -d
```
*In this case, to see how the composer is working, run the following command.*
```
docker-compose logs -f
```

## Stop the cluster
```
docker-compose -f docker-compose.yml down
```

## Start MySQL connector
```
curl -i -X POST -H "Accept:application/json" -H  "Content-Type:application/json" http://localhost:8083/connectors/ -d @register-mysql.json
```

## Start SQL Server connector
```
curl -i -X POST -H "Accept:application/json" -H  "Content-Type:application/json" http://localhost:8083/connectors/ -d @register-sqlserver.json
```
