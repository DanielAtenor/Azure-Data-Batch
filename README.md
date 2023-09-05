# Links to follow
https://azuredevopslabs.com/labs/vstsextend/terraform/     
https://www.youtube.com/watch?v=iQ41WqhHglk&ab_channel=Mr.KTalksTech

# Architecture

# Tools
## Local machine / On-premises
SQL Server 2019     

## Azure
Data Factory     
Databricks     
Key Vault     
Power BI

# ETL/ELT
## Bronze layer
Batch processing using Data Factory:     
SQL Server on-premises     
CSV Files     
API     
Output: Parquet format     

## Silver layer
Build Data Vault
Delta format

## Gold layer
Build star schema
Delta format

# In progress
Azure infrastructure with Terraform
·        Data Factory
·        Databricks
·        Storage gen 2

# Data Visualization in Power BI

# Simple webapp that consumes Power BI Embedded reports

 

# 1 - Instal SQL Server and local tools
Install SQL Server 2019 Developer Edition     
     Cost: Free     
     Localhost     
Download AdventureWorks compatible database (2019) and restore the database in the local instance     
Install SSMS to access the database     
Visual Studio Code     

# 2 - Create a new resource group and Key Vault
![Screenshot](/Images/RG%20and%20Key%20Vault%20Creation.png)

# 3 - Create and configure ADF connection to SQL Server

(1) - Create the user 

```
CREATE LOGIN azure_sql_user WITH PASSWORD = '1qaz"WSX'
create user azure_sql_user for login azure_sql_user
```




