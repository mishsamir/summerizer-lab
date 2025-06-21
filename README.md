# CST8917-Lab Work
## Lab 2: Build an Intelligent PDF Summarizer using Azure Durable Functions
## View Demo Video
[Video Demo Link ](https://www.youtube.com/watch?v=v4vDoacWnQM)

### Azure Durable Functions
#### Azure Durable Functions is an extension of Azure Functions that lets you write stateful workflows in a serverless environment. In short, they make it easy to orchestrate long-running, stateful, and reliable workflows using code—without worrying about the underlying infrastructure.

#### Core Concepts Durable Functions = Serverless + Orchestration + State

#### Serverless: 
#### You only pay for what you use, and Microsoft manages the servers.

#### Orchestration: 
You can coordinate the execution of other functions, including sequential, parallel, or even human-interaction steps.

#### Stateful:
 Durable Functions keep track of the workflow's progress and state, so you don’t have to manage this yourself.

#### The application's workflow is as follows:

Trigger: Listens for new blobs (PDFs) in the input container.

#### Durable Orchestration:

Step 1: Analyze the PDF with Document Intelligence (OCR/structure extraction).
Step 2: Summarize the extracted text using Azure OpenAI.
Prerequsites
Install the latest Azure Functions Core Tools to use the CLI
Python 3.9 or greater
Access permissions to create Azure OpenAI resources and to deploy models.
Start and configure an Azurite storage emulator for local storage.
Search for the Document intelligence and create Document Intelligence under AI Foundry.
local.settings.json
You will need to configure a local.settings.json file at the root of the repo that looks similar to the below. Make sure to replace the placeholders with your specific values.
```
{
  "Values": {
    "AzureWebJobsStorage": "UseDevelopmentStorage=true",
    "AzureWebJobsFeatureFlags": "EnableWorkerIndexing",
    "FUNCTIONS_WORKER_RUNTIME": "python",
    "BLOB_STORAGE_ENDPOINT": "<BLOB-STORAGE-ENDPOINT>",
    "COGNITIVE_SERVICES_ENDPOINT": "<COGNITIVE-SERVICE-ENDPOINT>",
    "AZURE_OPENAI_ENDPOINT": "AZURE-OPEN-AI-ENDPOINT>",
    "AZURE_OPENAI_KEY": "<AZURE-OPEN-AI-KEY>",
    "CHAT_MODEL_DEPLOYMENT_NAME": "<AZURE-OPEN-AI-MODEL>"
  }
}
```
#### Running the app locally
Start Azurite: Begin by starting Azurite, the local Azure Storage emulator.

#### Install the Requirements: Open your terminal and run the following command to install the necessary packages:

```python3 -m pip install -r requirements.txt```
#### Create two containers in your storage account. One called input and the other called output.

Start the Function App: Start the function app to run the application locally.

``` func start --verbose ```
Upload PDFs to the input container. That will execute the blob storage trigger in your Durable Function.

After several seconds, your appliation should have finished the orchestrations. Switch to the output container and notice that the PDFs have been summarized as new files.

