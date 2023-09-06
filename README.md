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

 

# 1) Local machine

## 1.1) Instal SQL Server and local tools
Install SQL Server 2019 Developer Edition     
     Cost: Free     
     Localhost     
Download AdventureWorks compatible database (2019) and restore the database in the local instance     
Install SSMS to access the database     
Visual Studio Code     

## 1.2 SQL Server

### 1.2.1) Create a SQL Server user

```
CREATE LOGIN azure_sql_user WITH PASSWORD = '1qaz"WSX'
create user azure_sql_user for login azure_sql_user
```

### 1.2.2) Give read access to the user

```
ALTER ROLE db_datareader ADD MEMBER azure_sql_user
```

# 2) Azure     

## 2.1) Create a new resource group, Key Vault and configure RBAC role     
     
### 2.1.1) Create KV resource. Since we don't have a RG yet, we create it at the same time     
**Resource group:** (New) Azure-Data-Batch     
**Key vault name:** Azure-Data-Batch-KV    
**Region: France:** Central     
**Pricing tier:** Standard     
     
### 2.1.2) Assign RBAC role <u>Key vault Administrator</u> to the user who is going to manage the KV secrets     
Home > Azure-Data-Batch-KV | Access control (IAM)     
Search for **Key vault Administrator** role and select it     
Add desired users to the member list     

### 2.1.3) Create SQL Server secrets in KV
     
**Name:** sqluser, **Secret value:** azure_sql_user     
**Name:** sqlpassword, **Secret value:** 1qaz"WSX     




