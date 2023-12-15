# azure-database-migration78
## Azure Database Migration Project 
## Overview

In this project, you'll be tasked with designing and implementing a cloud-based database system using Microsoft Azure. You will establish a robust production environment database. Following this, you'll manage the migration of the database to Azure SQL Database, focusing on key aspects such as data backup, restoration, and automated scheduling. You will also simulate a disaster recovery scenario to gain insights into potential data loss mitigation. Furthermore, you'll explore the complexities of geo-replication and failover configuration to ensure the resilience of your data infrastructure. To enhance security measures, the project will incorporate Microsoft Entra ID for defining access roles, adding an extra layer of control and protection to the database environment.
## Milestone 1 - Set up the Environment
Set up a GitHub repo and an Azure account for the project.

## Milestone 2 - Set up the Production Environment
Set up a virtual machine on Azure and connect to it using Remote Desktop Connection. <br />
Install SQL Server and SSMS on the virtual machine. <br />
Create an on-premise production database on the virtual machine and restore the back up file from [here.](https://aicore-portal-public-prod-307050600709.s3.eu-west-1.amazonaws.com/project-files/93dd5a0c-212d-48eb-ad51-df521a9b4e9c/AdventureWorks2022.bak)

## Milestone 3 - Migrate to Azure SQL Database
Create an Azure SQL Database and server with a firewall for the virtual machine's IP address. <br />
Download Azure Data Studio on the virtual machine if not already installed. <br />
Connect to the Azure SQl Database and on-premise database on Azure Data Studio. <br />
Install the SQL Server Schema Compare extension within Azure Data Studio. <br />
Compare and migrate the schema AdventureWorks from the on-premise database to the Azure SQL Database. <br />
Install the Azure SQL Migration extension within Azure Data Studio. <br />
Use the Azure SQl Migration extension to migrate these two environments by following the steps. <br />
Set the Azure SQL database as the target. <br />
You will need to create an Azure Database Migration Service on Azure, which will orchestrate the database migration. <br />
You will also need to download and install integration runtime. <br />
Select the tables that you want to migrate from. <br />
Run the validation to check for any errors, and when successful, start the migration.

## Milestone 4 - Data Backup and Restore
Complete a full backup of the production database hosted on the Windows virtual machine. <br />
Configure an Azure Blob Storage account and container on Azure. <br />
Upload the previously created database backup file to the Blob Storage container. <br />
Provision a new Windows virtual machine that mirrors the setup to be used as a development environment. <br />
Restore the database backup onto this new environment. <br />
Create a management task that automates regular backups weekly of your development database.

## Milestone 5 - Disaster Recovery Simulation
View a table in your production database.
```
SELECT *
FROM Person.EmailAddress;
```
![Captureoriginal](https://github.com/sgsophiegriffiths/azure-database-migration78/assets/146441873/4173c7d3-c671-4ec4-8caa-eb839f356004)
For example there are 19972 rows in total. <br />
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

## Milestone 6 - Geo Replication and Failover
Set up geo-replication for your restored Azure SQL Database by creating a new server in a different geographical region from your primary database server. <br />
This provides data redundancy and high availability by asynchronously replicating your primary database to a secondary region. <br />
Orchestrate a planned failover to the secondary region by creating a failover group in the primary server with the geo-replicated server set as the secondary server. <br />
Failover ensures high availability and business continuity by allowing applications to continue running from the secondary region. <br />
Testing these processes regularly ensures the readiness of your disaster recovery plan and boosts confidence in your organization's ability to handle unexpected incidents.

![Capturebefore](https://github.com/sgsophiegriffiths/azure-database-migration78/assets/146441873/a92a906b-836c-46ed-ad0c-5bbcc846202b)

Initiate a planned failover on Azure.


![Capturegeo](https://github.com/sgsophiegriffiths/azure-database-migration78/assets/146441873/93878568-1102-4a1c-85ff-c848b7ec947f)

Note which server is now primary and which server is secondary. If failover succeeded, the two servers should have swapped roles. <br />
Perform a failback to the primary region after reviewing the database availability and consistency.

## Milestone 7 - Microsoft Entra Directory Integration
Enable Microsoft Entra ID authentication for the SQL Server and choose an Microsoft Entra admin who holds privileged permissions within your Azure SQL Database. <br />
Next, generate a new user account in Microsoft Entra ID which will have reader access. <br />
Connect to the production database using the Microsoft Entra admin credentials. <br />
Run the following SQL query to grant the db_datareader role to the DB_Reader user replacing DB_Reader@yourdomain.com with the credentials of the reader user just created:
```
CREATE USER [DB_Reader@yourdomain.com] FROM EXTERNAL PROVIDER;
ALTER ROLE db_datareader ADD MEMBER [DB_Reader@yourdomain.com];
```
In Azure Data Studio re-connect to the Azure SQL Server you are currently connected to using the new user credentials. <br />
Test the user access by right-clicking on a table and clicking Select Top 1000 and you should see 1000 rows or less if there aren't 1000. <br />
Now run this query to delete the first entry in the table replacing TABLENAME with your table's name:
```
DELETE TOP (1) FROM TABLENAME
```
You should get an error indicating the user doesn't have access to modify the data as expected.

## DB UML

[Azure Project Diagram.pdf](https://github.com/sgsophiegriffiths/azure-database-migration78/files/13686731/Azure.Project.Diagram.pdf)

