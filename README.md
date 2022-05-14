# azure-resume
My own azure resume to understand and implement azure services for FRT
# Azure Cloud Resume Future Ready talent
## Project Info
resume and portfolio using azure, cosmos db, on azure blob storage . by using their css html js skills . the basic idea is to use the azure web services to host our website and display their skills and resume at the same time using this project  . The front-end is a static site with HTML, CSS, and JavaScript. It's static and has a visitor counter. The visitor counter data fetched via an API call to an Azure Function.The back-end is an HTTP triggered Azure Functions with Cosmos DB input and output binding. 
##Project Link=[website.](https://azureresumefrt.z20.web.core.windows.net/#about/)
##Code=  
![Screenshot 2022-05-14 154512](https://user-images.githubusercontent.com/59210188/168421876-8d76b68b-da8f-4891-b647-8aefae89432b.png)
![Screenshot 2022-05-14 154446](https://user-images.githubusercontent.com/59210188/168421878-bbfae720-2351-473d-b32c-b4d4d29cb6aa.png)

##Output
#Home
![Screenshot 2022-05-14 154708](https://user-images.githubusercontent.com/59210188/168421669-71db2775-faf6-45e9-a687-1df58d60dcf1.png)
#About
![Screenshot 2022-05-14 154617](https://user-images.githubusercontent.com/59210188/168421673-ab7e0e90-1ea7-4a38-8aee-e87455374468.png)
#Resume
![Screenshot 2022-05-14 154640](https://user-images.githubusercontent.com/59210188/168421672-4c8fafaa-8f80-47e0-8fae-cce72362097d.png)



## Table of Contents
1. [Project Description](#introduction)
2. [To be done](#next)
3. [Building Static Website](#buildsite)
4. [Deployment of Azure Function](#DAzureFunction)
5. [Deployment of Website to Azure](#DWebsiteAzure)
6. [Building CI/CD pipeline](#CI/CD)

## Description <a name="introduction"></a>

- The Cloud Resume Challenge is a hands-on project designed to help bridge the gap from cloud certification to cloud job. It incorporates many of the skills that real cloud and DevOps engineers use in their daily work. Cloud challenge was designed by [Forrest Brazeal.](https://forrestbrazeal.com/) More information about the challenge can be found on official [website.](https://cloudresumechallenge.dev/)
- Key objectives for the project
    - Write static website in HTLM and styled in CSS
    - Deploy static website in Azure storage
    - Setup access to website via secure protocol HTTPS
    - Connect website to custom DNS domain name
    - Create visitor counter for the website with JavaScript and Azure’s Functions in Python
    - Store visit counts in Azure CosmosDB
    - Use API to establish communication between CosmosDB, Azure Functions and website
    - Create unit tests for Azure’s Functions in Python
    - Set up GitHub Actions for CI/CD deployment

## To be done <a name="next"></a>

- Create resume and host it in Azure’s General Purpose v2 storage
- Create Azure Key Vault and store all secrets securely
- Incorporate Terraform to build resources in Azure

## Building Static Website <a name="buildsite"></a>

- Create project in [GitHub](https://github.com/join)
    - clone repository locally
    
    ```
    git clone git@github.com:Pavel-Hrabec/Azure-Resume-Challenge.git
    ```
    
- [Download website template](https://www.styleshout.com/) to not start from complete scratch
- [Use Visual Studio Code](https://code.visualstudio.com/) to edit your web page
    - Once you made all the changes to the code and want to save your changes in GitHub
    
    ```
    git add -A
    git commit -m "What changes did you make"
    git push
    ```
    
- Create [JavaScript code](https://www.digitalocean.com/community/tutorials/how-to-use-the-javascript-fetch-api-to-get-data) for Counter every time page is loaded
    - [Trigger](https://developer.mozilla.org/en-US/docs/Web/API/Document/DOMContentLoaded_event) when initial HTLM document has been loaded
    - [Get data](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch) from API function in JSON

Creation of Azure Function

- [Azure Account](https://azure.microsoft.com/en-us/free) needs to be created
- [Build ComosDB](https://docs.microsoft.com/en-us/azure/cosmos-db/sql/create-cosmosdb-resources-portal) database via [Azure Portal](https://portal.azure.com/?quickstart=true#home)
    - [Resource Group](https://azuresdkdocs.blob.core.windows.net/$web/python/azure-cosmos/4.2.0/index.html#query-the-database) needs to be created first or as part of CosmosDB creation process
- [Create container](https://docs.microsoft.com/en-us/azure/cosmos-db/sql/how-to-create-container) in Azure Cosmos
    - On left board select > Data Explorer > New Database > In data section database will be created > click 3 dots > new container > partition key </id> > Go to items in container > create new row
        
        ```
        {
        	"id: "1",
        	"count": 0
        }
        ```
        
- [Create Azure Function](https://docs.microsoft.com/en-us/azure/azure-functions/functions-develop-vs-code?tabs=csharp) in Visual Studio Code
    - Install [Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)
        
        ```
        vscode:extension/ms-azuretools.vscode-azurefunctions
        ```
        
    - Install [Python extension](https://code.visualstudio.com/docs/python/python-tutorial)
    - Create local [Azure Function project](https://docs.microsoft.com/en-us/azure/azure-functions/create-first-function-vs-code-python)
    - Install package inside your project directory for Azure-Cosmos (make sure to update requirements.txt as well before function deployment to Azure)
        
        ```
        pip install azure-cosmos
        ```
        
    - Create an [HTTP trigger](https://docs.microsoft.com/en-us/azure/azure-functions/functions-reference-python?tabs=asgi%2Cazurecli-linux%2Capplication-level#http-trigger-and-bindings) in your Azure Function as well as [connection to CosmosDB](https://azuresdkdocs.blob.core.windows.net/$web/python/azure-cosmos/4.2.0/index.html) to [retrieve](https://azuresdkdocs.blob.core.windows.net/$web/python/azure-cosmos/4.2.0/index.html#query-the-database) and [update](https://github.com/Azure/azure-sdk-for-python/blob/main/sdk/cosmos/azure-cosmos/samples/examples.py) data inside container

## Deployment of Azure Function <a name="DAzureFunction"></a>

- [Publish](https://azuresdkdocs.blob.core.windows.net/$web/python/azure-cosmos/4.2.0/index.html#query-the-database) Azure function to Azure
    - Select the same resource group as for CosmosDB
    - Create new [Azure storage account](https://azuresdkdocs.blob.core.windows.net/$web/python/azure-cosmos/4.2.0/index.html#query-the-database) (can be done when publishing Azure function as well)
- Edit Azure Function’s [application settings](https://azuresdkdocs.blob.core.windows.net/$web/python/azure-cosmos/4.2.0/index.html#query-the-database) with your secrets
    - You can use Azure Key Vault to store them securely
- Get [Function URL](https://microsoftlearning.github.io/AZ-900T0x-MicrosoftAzureFundamentals/Instructions/Walkthroughs/08-Implement%20Azure%20Functions.html)
    - Add URL into your JavaScript code for counter
- Enable [Cross-Origin Resource Sharing](https://docs.microsoft.com/en-us/azure/azure-functions/functions-how-to-use-azure-function-app-settings?tabs=portal#cors) (CORS) for you function in Azure

## Deployment of Website to Azure <a name="DWebsiteAzure"></a>

- Install [Azure static Web Apps extension](https://docs.microsoft.com/en-us/azure/static-web-apps/getting-started?tabs=vanilla-javascript#install-azure-static-web-apps-extension) for Visual Studio Code and create static web app
- Create [Azure Content Delivery Network](https://docs.microsoft.com/en-us/azure/cdn/cdn-create-new-endpoint) (CDN) profile and endpoint for your website
- [Map your custom domain](https://docs.microsoft.com/en-us/azure/cdn/cdn-map-content-to-custom-domain?tabs=azure-dns%2Cazure-portal%2Cazure-portal-cleanup) to CDN profile
    - I’ve havent used custom domain for my custom domain
- Enforce [HTTPS traffic only](https://stackoverflow.com/questions/39244265/azure-web-app-redirect-http-to-https)
- Redirect [HTTP traffic to HTTPS](https://stackoverflow.com/questions/39244265/azure-web-app-redirect-http-to-https)
- Get your website URL and edit [CORS](https://docs.microsoft.com/en-us/azure/azure-functions/functions-how-to-use-azure-function-app-settings?tabs=portal#cors) for allowed origins

## Building CI/CD pipeline <a name="CI/CD"></a>

- Create [GitHub Actions workflows](https://docs.github.com/en/actions/quickstart) (Front End for static site deployment and Back End for unit testing)
- Generate [deployment credentials](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-blobs-static-site-github-actions?tabs=userlevel#generate-deployment-credentials) and add your workflow for static site
- Write Python code to [test Azure Functions](https://docs.microsoft.com/en-us/azure/azure-functions/functions-reference-python?tabs=asgi%2Cazurecli-linux%2Capplication-level#unit-testing)
    - [Pytest](https://docs.pytest.org/en/6.2.x/getting-started.html) can be used to run unit tests
- Set up a [Python workflow](https://docs.microsoft.com/en-us/azure/azure-functions/functions-how-to-github-actions?tabs=python#deploy-the-function-app) that uses a publish profile
