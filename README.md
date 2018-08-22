## Welcome to a hands-on workshop for **Machine Learning on Big Data** using Azure Databricks

### The datasets and base notebooks were provided by Azure Databricks
During the Azure Databricks Roadshow the following datasets and base notebooks were provided by Azure Databricks

The scenario is around a fictional Electronics Retail Company, "Initech", with brick & mortar locations as well as an online marketplace.  The architecture will look similar to this but will incorporate the use of a single Azure Databricks cluster instead of the 4 clusters in the diagram.  The workshop will also use an Azure SQL database instead of Cosmos DB.

![abd-uap](https://raw.githubusercontent.com/DataSnowman/ml-on-bigdata/master/images/adb-uap.png)


## Prerequisites

To deploy the Azure resources required for this lab, you will need:

1. An [Azure account](https://portal.azure.com)
2. Clone this GitHub repository using Git and the following commands: 

    `git clone https://github.com/DataSnowman/ml-on-bigdata.git`

**Note** that you will be deploying a number of Azure resources into your Azure Subscription when either clicking on the [Deploy to Azure](https://github.com/Azure/DataScienceVM/blob/master/Tutorials/MLADS-spring-2018/setup/README.md) button, or by alternatively deploying by using an ARM template and parameters file via the Azure CLI.

Note: If you encounter issues with resources please check by running the following commands in the Azure CLI (Note more information on using the CLI is found in the `Provisioning using the Azure CLI` section below):
  
  `az login`

  `az account show`

  `az account list-locations`
  
  `az provider show --namespace Microsoft.Databricks --query "resourceTypes[?resourceType=='workspaces'].locations | [0]" --out table`

## Choices for Provisioning

You can provision using the Deploy to Azure button or using the Azure CLI.

### Provisioning using the Deploy to Azure button

After you have checked for the availability of resources in your subscription.

1) Create a Resource Group using the [Azure Portal](https://portal.azure.com) or in the Azure CLI using a command like this:

  `az group create -n mlbigdata -l southcentralus`

2) Click on the [Deploy to Azure](https://github.com/DataSnowman/ml-on-bigdata/blob/master/setup/README.md) button on the README in the setup folder.

Choose your Subscription, and enter a Resource Group Name, Azure Databricks Workspace Name, SQL Server Username, and SQL Server Password.  Then click the `Next` button.

![setup](https://raw.githubusercontent.com/DataSnowman/ml-on-bigdata/master/images/setup.png)

Preview the Resource Types and click the `Deploy` button.

![preview](https://raw.githubusercontent.com/DataSnowman/ml-on-bigdata/master/images/preview.png)

After about 3 minutes the deployment should complete.  Click the green link `Manage` your resources to open the resource group in the Azure portal.

![deploy](https://raw.githubusercontent.com/DataSnowman/ml-on-bigdata/master/images/deploy.png)

### Provisioning using the Azure CLI

1. Download and install the [Azure CLI Installer (MSI) for Windows](https://aka.ms/InstallAzureCliWindows) or [Mac or Linux](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest) . Once the installation is complete open the command prompt and run `az login`, then copy the access code returned. In a browser, open a **private tab** and enter the URL `aka.ms/devicelogin`. When prompted, paste in the access code from above. You will be prompted to authenticate using our Azure account.  Go through the appropriate multifaction authenication.

2. Navigate to the folder `ml-on-bigdata\setup` If using **Windows Explorer** you can launch the command prompt by going to the address bar and typing `cmd` (for the Windows command prompt) or `bash` (for the Linux command prompt assuming it is installed already) and type `az --version` to check the installation.  Look for the `parameters-mlbigdata.json` file you cloned during the Prerequisites above.  

3. When you logged in to the CLI in step 1 above you will see a json list of all the Azure account you have access to. Run `az account show` to see you current active account.  Run `az account list -o table` if you want to see all of you Azure account in a table. If you would like to switch to another Azure account run `az account set --subscription <your SubscriptionId>` to set the active subcription.  Run `az group create -n mlbigdata -l southcentralus` to create a resource group called `mlbigdata`.

4. Next run the following command to provision the Azure resources:
```
az group deployment create -g mlbigdata --template-file azureclideploy.json --parameters @parameters-mlbigdata.json
```
Once the provisioning is finished, we can run `az resource list -g mlbigdata -o table` to check what resources were launched. Our listed resources includes: 
    * 2 storage accounts
    * 1 event hub
    * 1 Databricks workspace
    * 1 SQL Database.

## Copying the source data

1. Use Microsoft Azure Storage Explorer to copy the blob container

You can download Microsoft Azure Storage Explorer [HERE](https://azure.microsoft.com/en-us/features/storage-explorer/) for Linux, Mac, or Windows 

Once you install and open it click on the connection plug icon and choose `Use a connection string`.  Click `Next`

![connect](https://raw.githubusercontent.com/DataSnowman/ml-on-bigdata/master/images/connect.png)

Copy the following connection string
**FixThis**
```
**FixThis**SharedAccessSignature=sv=2018-03-28&ss=bfqt&srt=sco&sp=rl&st=2018-08-17T22%3A09%3A30Z&se=2020-08-18T22%3A09%3A00Z&sig=J1JF1HV7*FixThis*clhrQWiXfaKC2w8KFj2M%3D;BlobEndpoint=https://ainellarealta.blob.core.windows.net/;FileEndpoint=https://ainellarealta.file.core.windows.net/;QueueEndpoint=https://ainellarealta.queue.core.windows.net/;TableEndpoint=https://ainellarealta.table.core.windows.net/;
```
Paste it into the Connection string dialog box. Click `Next`

![attach](https://raw.githubusercontent.com/DataSnowman/ml-on-bigdata/master/images/attach.png)

Click `Connect`

![summary](https://raw.githubusercontent.com/DataSnowman/ml-on-bigdata/master/images/summary.png)

The Storage Account container should now be available under storage accounts.  Right click on the container named `source` and choose `Copy Blob Container`

![container](https://raw.githubusercontent.com/DataSnowman/ml-on-bigdata/master/images/container.png)

Click on the connection plug icon and this time choose `Add an Azure Account`.  Click `Sign in...`

![signin](https://raw.githubusercontent.com/DataSnowman/ml-on-bigdata/master/images/signin.png)

Sign in to your Azure Account and navigate to the `source`plus hash characters storage account created during the azure deployment.  Right click and choose `Paste Blob Container`

![paste](https://raw.githubusercontent.com/DataSnowman/ml-on-bigdata/master/images/paste.png)

The Activities section of Microsoft Azure Storage Explorer should look something like this

![activities](https://raw.githubusercontent.com/DataSnowman/ml-on-bigdata/master/images/activities.png)


## Configuring the event hub for streaming


## Importing and running Databricks notebooks

### Importing notebooks using the dbc file

### Running the Data Engineer notebooks

### Running the Data Scientist notebooks

### Running the Notebooks loading SQL

## Connecting to Databricks and SQL Database using Power BI



Hope you enjoyed this workshop.

## Thank you to the members of Databricks that created the notebooks for this tutorial:
* **Name One** 
* **Name Two**
