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

In progress
Azure infrastructure with Terraform
·        Data Factory
·        Databricks
·        Storage gen 2

Data Visualization in Power BI

Simple webapp that consumes Power BI Embedded reports

 

# 1) Local machine

## 1.1) Instal local tools
Install SSMS to access the database     
Visual Studio Code     
Install Bicep plugin on VSC     
Install Azure CLI on Windows     
Download and install Java Runtime Environment (JRE) (Data factory copy activity makes use of Java to extract the data from SQL Server)

## 1.2 Download and install SQL Server
Install SQL Server 2019 Developer Edition     
     Cost: Free     
     Localhost     
Download AdventureWorks compatible database (2019) and restore the database in the local instance    

### 1.2.1) Create a SQL Server user

```
CREATE LOGIN azure_sql_user WITH PASSWORD = '1qaz"WSX'
create user azure_sql_user for login azure_sql_user
```

### 1.2.2) Give read access to the user

```
ALTER ROLE db_datareader ADD MEMBER azure_sql_user
```

### 1.2.3) Allow SQL Server logins

In SSMS, go to the instance properties > Security > Server authentication: SQL Server and Windows Authentication mode

# 2) Azure
Create and manage Resource Group, Key Vault, Storage Account

## 2.1) Create a new resource group, Key Vault and configure RBAC role, store secrets from SQL Server     
     
### 2.1.1) Create KV resource. Since we don't have a RG yet, we create it at the same time     
**Resource group:** (New) Azure-Data-Batch     
**Key vault name:** Azure-Data-Batch-KV    
**Region: France:** Central     
**Pricing tier:** Standard     
     
### 2.1.2) Assign RBAC role <u>Key vault Administrator</u> to the user who is going to manage the KV secrets     
Home > Azure-Data-Batch-KV | Access control (IAM)     
Search for **Key vault Administrator** role and select it     
Add desired users to the member list     

### 2.1.3) Store SQL Server secrets in KV
     
**Secret 1. Name:** sqluser, **Secret value:** azure_sql_user     
**Secret 2. Name:** sqlpassword, **Secret value:** 1qaz"WSX     

## 2.2) Create Storage Account
Resource group: Azure-Data-Batch     
Storage account name: azuredatabatchlake     
Region: France central     
Performance: Standard     
Redundancy: LRS     
Enable hierarchical namespace

## 2.3) Create repositories in the Datalake
Create bronze, silver and gold repositories

## 2.4) Give the user read acess to the container
In order to see the data through the Azure portal, give access to your own user at the container level adding the user to the role IAM **Storage Blob Data Reader**     

# 3) Data Factory

## 3.1) Create Data Factory DEV
**Name:** Azure-Data-Batch-ADF-DEV     
**Region:** France Central     
**Version:** V2     
No GIT Configuration. We will configure it later.

## 3.2) Create Self-Hosted integration runtime

Open **Azure-Data-Batch-ADF-DEV** resource -> Integration runtimes > New > Azure, Self-Hosted > Self-Hosted     
**Name:** Azure-Data-Batch-SHIR     
Install the launcher either Express or Manual

## 3.3) Configure read access from ADF to KV

Go to **Azure-Data-Batch-KV** > Access control (IAM) > select **Key Vault Reader** role > Members > **+ Select members** > Search for the ADF resource **Azure-Data-Batch-ADF-DEV**     

## 3.4) Create and configure a pipeline to copy data from SQL Server

At this point we are going to create:     
Three linked services, one for **Key Vault** and another for **SQL Server** source, another for **Azure Datalake Storage**;     
     
To see the full pipeline implementation consult the repository or the data factory resource.
