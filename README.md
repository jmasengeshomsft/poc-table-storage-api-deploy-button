
## How to run the deploy the function app infrastructure in your Azure Subscription using Azure CLI


Configure the variables.

```bash
# Global
export RG_NAME=demo-deploy-button
export RG_REGION=centralus
export TEMPLATE_FILE=infrastructure/azuredeploy.json
export PARAMETER_FILE=infrastructure/azuredeploy.parameters.json

```

Create a resource group for this project

```bash
az group create --name $RG_NAME --location $RG_REGION
```

Deploy the function app with a storage account and app insights 

```bash
az deployment group create --name createFunctionApp -g $RG_NAME --template-file $TEMPLATE_FILE --parameters $PARAMETER_FILE
```

## How to run the deploy the function app infrastructure in your Azure Subscription using Deploy Button

[![Deploy to Azure](https://aka.ms/deploytoazurebutton)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2Fjmasengeshomsft%2Fpoc-table-storage-api-deploy-button%2Fmain%2Fpoc-table-storage-api-deploy-button%2Finfrastructure%2Fazuredeploy.json)

<!-- 
Under app/src, if not present, create a settings file for the function app named **local.settings.json** in app/src with the following configurations:

```bash
{
    "IsEncrypted": false,
    "Values": {
      "ScrapAppOptions:ChromeDriverExecutablePath": "<LOCATION OF THE CHROMIUM EXECUTABLE>",
      "ScrapAppOptions:OutputFolderPath": "<LOCATION OF THE OUTPUT FILE IF FUBLISHING LOCALLY>",
      "ScrapAppOptions:PublishEnvironment": "<AZURE | LOCAL | any other value>",
      "AzureWebJobsStorage": "<AZURE STORAGE CONNECTION STRING>",
      "AzureStorageOptions:StorageAccountName": "<AZURE STORAGE ACCOUNT NAME>",
      "AzureStorageOptions:SkillTableStorageName": "<AZURE TABLE STORAGE : FacetSkills>",
      "AzureStorageOptions:StorageAccountKey": "<STORAGE ACCOUNT KEY>",
      "FUNCTIONS_WORKER_RUNTIME": "dotnet"
    }
  }
```

**Downloading the Chrome Driver**

* Based on the version of Chrome you have on your workstation, download the corresponding Chromium version here: https://chromedriver.chromium.org/downloads
* Extract the executable in ScrapAppOptions:ChromeDriverExecutablePath

**Specify how and where to publishing the output**

* Specify ScrapAppOptions:PublishEnvironment:
   * **AZURE**: To publish to an azure table storage specified in **AzureStorageOptions:SkillTableStorageName**
   * **LOCAL**: To publish to a local folder specified in **ScrapAppOptions:OutputFolderPath** (under OutputFiles folder). Choose a location outside of the project repo
   * Any other value: Publish to Console

**Running the project**
* Make sure your environment is set up to run .Net core functions (Install .net SDK, and Functions Core Tools)
* Kick of the project by running:

```bash
cd app/src
func start
```

Once the functions are up and running, using tools such as Postman, make the following calls:

1. **GET: http://localhost:7071/api/ScrapUrlLocalFunc?scrapingSession=false**. 
  * Adjust the port if your function started on a different port other than 7071 
  * With the newely opened Chrome session, login into your LinkedId account as you normally do. Leave the window open
2.  Using another window in Postman
  * **GET: http://localhost:7071/api/ScrapUrlLocalFunc?company=<COMPANYKEY>&scrapingSession=true**
  * To find a company key, visit the company page and find which string LinkedIn uses in the url. For example, Caterpillar is "caterpillar-inc"
  * Let the app running until finished -->
