# Resource Creation
* Storage: in creation select the option of anonyomous container
    * create two blob_container name input and output. select the container anonymous access during their creation.
    * copy the connection string in a notepad
* Azure Ai Service : 
    * go to IAM, 
    * create role assignment, 
    * search for the "cognitive service openai contributor" and click next choose if the user, group or service principal is not available choose managed identity
        * if managed identity, select member and chose for all system managed identities.
        * select for the ai service and the resource group ai service
    * Go to the resource, go to azure ai foundry
        * search the ai language service in the model catalog - choose the analyze sentiments
        * copy the key and endpoint in a notepad
* Eventhub name space :
    * create an event hub namespace
    * go to entities, choose eventhub, create eventhub
    * go to settings, go shared policy - add new policy , create a manage policy and listen policy
    * copy both connection strings to a notepad.

* function App :
    * choose the flex comsumption plan
    * choose the resource group other settings important to the project

# Creation of functions locally on Vscode
    * create a github repo for the functions
    * clone repo to your local environment
    * login into the azure account to deploy  the solution. note the same account that you create the solution from.
    * choose the right subscription.
    * install the azure function extension on vscode
    * install the azure account extension on vscode.
    * install the function cli tools on your local machine. install the one for your OS. [https://github.com/Azure/azure-functions-core-tools]
    * for windows install the dot.net

# Functions Creation :
    * from the command pallete search Azure Function of just hit f1, select azure function: new project
    * create a new function project. select the eventhub you have created, chose the prefered acess policy - send/manage, choose the eventhub name 
    * write your functions in the project in your preferred language
    * start up the function to see how they work using "funct start" - to check the pipeline
    * it is successful deploy using the vscode command pallete to azure function: deploy to azure, 
    * go to azure portal to check your functions app. you should see your function in overview pane. 
    * if they are not their Do the next step below and refresh. i.e had the enviroment variable to the application setting  and refresh

# Hosting Environment Variable on Azure Function App in Enviroment variable in app settings.

* To run your PowerShell script (p.ps1) and sync the key-value pairs from your local.settings.json into your Azure Function App's Application settings, follow these steps:

* Open a PowerShell terminal in your project directory (real-time-sentiment).

* Before you run the app - comment out or remove the "FUNCTIONS_WORKER_RUNTIME": "python", and return to where it was in your code  after running the sript

* Run the script with your Function App name and Resource Group name. For example:

```
    .\p.ps1 -functionAppName "bet9jaFApp" -resourceGroup "rg-real_time_sentiments_scoring"

```

* Replace "bet9jaFApp" and "rg-real_time_sentiments_scoring" with your actual Function App and Resource Group names.

* The script will loop through all settings in your local.settings.json and set them in Azure.
__Note__:

* You must have the Azure CLI installed and be logged in (az login).
* If you get an execution policy error, run:
```
    Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
```
before running the script.
* This will automatically sync all your local environment variables to your Azure Function App’s Application settings.
* Refresh and you should the functions you created in the overview pane

# Event Grid Trigger Subscription for the blob storage :
    * go to the blob storage created earlier
    * go  to event, create an event subscription
    * fill and select the endpoint as azure function, select the configure endpoint. it should pick your eventgrid trigger
    * comfirm selection and create the subscription

# Moment of Truth - Test the pipeline
    * go to the input container and upload your file or connection to your source in input
    * check the output in the output to see the result of the setiments.
    * You can checks log, applicatioin insight, to check your performance

# Result Consumption
    *  integrate the output to power bi for real time dashboard, streamlit or other use cases



