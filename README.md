# Kafka SQL connect UI docker composer
This docker composer file automatically deploy the kafka sql connect services and monitoring UI.

## Pre-requirements
Before running of the kafka connector, the SQL servers must be configure to allow the monitoring of the kafka connector.
### MySQL server configuration
Before the Debezium MySQL connector can be used to monitor the changes committed on a MySQL server, the server must be set up to use row-level binary logging and have a database user with appropriate privileges.
**In /etc/mysql/mysql.conf.d/mysqld.cnf (in case of ubuntu)**
```
[mysqld]
server-id         = 1111
log_bin           = mysql-bin
binlog_format     = row
binlog_row_image  = full
expire_logs_days  = 10
```

### SQLServer configuration
Before using the Debezium SQL Server connector to monitor the changes committed on SQL Server, first enable CDC on a monitored database. Please bear in mind that CDC cannot be enabled for master database.
```
-- ====
-- Enable Database for CDC template
-- ====
USE MyDB
GO
EXEC sys.sp_cdc_enable_db
GO
Then enable CDC for each table that you plan to monitor

-- =========
-- Enable a Table Specifying Filegroup Option Template
-- =========
USE MyDB
GO

EXEC sys.sp_cdc_enable_table
@source_schema = N'dbo',
@source_name   = N'MyTable',
@role_name     = N'MyRole',
@filegroup_name = N'MyDB_CT',
@supports_net_changes = 1
GO
```


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
