# Reporting  on IoT data

In this part we will make a dashboard that can report on the data from the Beer Blades (let's call them Taps from now on). Think about metrics like Temperature of the beer keg, the volume of the beer keg, ambient temperature, air pressure etc.

### What services in Azure are Used:
- IoT-Hub
- Azure Stream Analytics Job
- SQL DB (SQL-Server)
- Grafana (Open Source Dashboard/reporting tool as an alternative for PowerBI)
- Supporting services (storage accounts etc.)

### What services didn't we use?:

#### PowerBI
PowerBI didn't make the workshop, needed accounts for everybody and realtime was only in paid subscription.

#### InfluxDB, or simular time series database
Ideally you would use a time series database for Grafana. Azure's CosmosDB would be the ideal candidate for this. However there is no Grafana datasource plugin yet for CosmosDB so we decided not the use this.A more suitable solition could be to use the TimescaleDB plugin for Azure Database for PostgreSQL.

Azure Stream Analytics does not support InfluxDB as an output either. So we would need something like Azure Databricks or an container running some code between the IoT-Hub and the InfluxDB. Where Databricks is way more expensive just for this workshop. Besides that Eelco has more experience with SQL, so it was easier to put together.

All in all this would make the setup more complex then needed for the workshop.

## Small Architecture sketch
![High Level Architecture](img/high_level_architecture.jpg "Architecture")

## Setup per table
Each Table has its own resource group with the per-table shared azure resources (e.g. IoTHub)
You can find credentials that you can use to login to portal.azure.com on each table.
Please do not deploy additional IoT Hubs, as they won't be able to receive data from the Beer taps. Each deployed IoT Hub needs to be configured on the Beer Taps and the ones we deployed have been configured on our Beer Taps.

## Setup per Workshop attendeed
Each workshop attendee wil also receive an own Resource group in which he/she can deploy the neccesary resources. The resource group that belongs to you can be found on the table as well.
Please do not deploy things to resource groups that are not your own. Thank you on behalf of your fellow workshop mates for understanding ;)

## What You will Create
1. A [Consumergroup](1_iothub.md) for yourself on the IoT Hub of your table.
2. An [Azure SQL DB](2_sql_database.md) and create the tables (we have a script for the tables ;) )
3. An [Azure Stream Analytics Job](3_azure_stream_analytics.md) and configure the Inputs and Outputs
4. A Dashboard in [Grafana](4_grafana.md) (SQL Queries to get some nice data are available)
