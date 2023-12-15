# azure-database-migration78

## Milestone 2
Set up a virtual machine on Azure and connect to it.
Install SQL Server and SSMS on the virtual machine.
Create a production database on the virtual machine localhost and restore the back up file for the database that is called AdventureWorks.

## Milestone 3
Create an Azure SQL Database and server with a firewall for the virtual machines IP address.
Download Azure Data Studio on the virtual machine if not already installed.
Connect to the Azure SQl Database and on-premise database on Azure Data Studio.
Install the SQL Server Schema Compare extension within Azure Data Studio.
Compare and migrate the schema AdventureWorks from the on-premise database to the Azure SQL Database.
Install the Azure SQL Migration extension within Azure Data Studio.
Use the Azure SQl Migration extension to migrate these two environments by following the steps.
Set the Azure SQL database as the target.
You will need to first create an Azure Database Migration Service on Azure, which will orchestrate the database migration.
You will also need to download and install integration runtime.
Select the tables that you want to migrate from. 
Run the validation to check for any errors and when successful start the migration.

## Milestone 4
Complete a full backup of the production database hosted on the Windows virtual machine.
onfiguring an Azure Blob Storage account and container on Azure.
Upload the previously created database backup file to the Blob Storage container.
Provision a new Windows virtual machine that mirrors the setup to be used as a development environment.
Restore the database backup onto this new environment.
Create a management task that automates regular backups weekly of your development database.

## Milestone 5
```
SELECT *
FROM Person.EmailAddress;
```
![Captureoriginal](https://github.com/sgsophiegriffiths/azure-database-migration78/assets/146441873/4173c7d3-c671-4ec4-8caa-eb839f356004)
There are 19972 rows in total. <br />
Deliberately remove critical data from your production database to replicate a scenario where data integrity is compromised. 
```
DELETE TOP (100)
FROM Person.EmailAddress;
```
![Capture](https://github.com/sgsophiegriffiths/azure-database-migration78/assets/146441873/270d7f07-4caa-42b8-b8ef-c3edc916a44c)
19872 rows remain. <br />
Use Azure SQL Database Backup to restore the production database to a point just before the simulated data loss occurred. <br />
Examine the restored data through a new connection in Azure Data Studio to the restored database. <br />
The 100 rows have been restored and there are 19972 rows. <br />
![Capturefinal](https://github.com/sgsophiegriffiths/azure-database-migration78/assets/146441873/c8e3a700-dec6-48ff-ba73-34d0bdb59f05)

## Milestone 6
Set up geo-replication for your restored Azure SQL Database by creating a new server in a different geographical region from your primary database server.
This provides data redundancy and high availability by asynchronously replicating your primary database to a secondary region.
Orchestrate a planned failover to the secondary region by creating a failover group in the primary server with the geo-replicated server set as the secondary server.
Failover ensures high availability and business continuity by allowing applications to continue running from the secondary region.
Testing these processes regularly ensures the readiness of your disaster recovery plan and boosts confidence in your organization's ability to handle unexpected incidents.

![Capturebefore](https://github.com/sgsophiegriffiths/azure-database-migration78/assets/146441873/a92a906b-836c-46ed-ad0c-5bbcc846202b)

Initiate a planned failover on Azure.


![Capturegeo](https://github.com/sgsophiegriffiths/azure-database-migration78/assets/146441873/93878568-1102-4a1c-85ff-c848b7ec947f)

Note which server is now primary and which server is secondary. If failover succeeded, the two servers should have swapped roles. 
Perform a failback to the primary region after reviewing the database availability and consistency.



