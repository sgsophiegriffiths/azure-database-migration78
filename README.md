# azure-database-migration78

Milestone 2
Set up and connect to VM
Installed SQL Server and SSMS
Created production database and restored the back up file for the database AdventureWorks

Milestone 3
Created Azure SQL Database and server with firewall for VM IP address
Download Azure Data Studio
Connect to Azure SQl Database and on-premise database on Azure Data Studio
Install the SQL Server Schema Compare extension within Azure Data Studio
Compare and subsequently migrate the schema AdventureWorks from the on-premise database to the Azure SQL Database
Install the Azure SQL Migration extension within Azure Data Studio

Milestone 4
Full backup of the production database hosted on the Windows VM
onfiguring an Azure Blob Storage account and container
Upload the previously created database backup file to the Blob Storage container
Provisioned a new Windows VM that mirrors the development setup
restore the database backup onto this new environment
Created management task that automates regular backups weekly of your development database

Milestone 5
Deliberately remove critical data from your production database to replicate a scenario where data integrity is compromised. 

DELETE TOP (100)
FROM Person.EmailAddress;

Use Azure SQL Database Backup to restore the production database to a point just before the simulated data loss occurred.
Examine the restored data through a new connection in Azure Data Studio to the restored database.

