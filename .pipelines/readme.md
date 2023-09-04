[[_TOC_]]

# .pipelines folder

This folder is meant for all files related to build- and deployment pipelines. 

## Description of files

```txt
.pipelines
 ┣ deploy
 ┃ ┣ bicep
 ┃ ┃ ┣ azure-deployment.bicep                # Add resources for within a resource group here.
 ┃ ┃ ┣ azure-deployment.parameters.d.json    # Add Deployment parameters that should be in source control here.
 ┃ ┃ ┣ azure-deployment.subscription.bicep   # Add any resource groups here
 ┃ ┃ ┗ bicepconfig.json                      # Required. Setup the subscription and resource group for using template specs here.
 ┃ ┗ ?? TODO
 ┣ authors.yml                             # Optional. Variables are used in Directory.Build.props to set author and copyright in assemblies.
 ┣ azure-pipelines.yml                     # Starter pipeline. Computes GitVersion.
 ┣ deploy.ps1                              # Local deployment helper script
 ┣ GitVersion.yml                          # Optional. Config for GitVersion
 ┣ nuget.azure-pipelines.yml               # Optional. Prefab Pipeline for creating and publishing nuget packages.
 ┗ readme.md                               # This file.
```

# Deployment to Azure from local machine

Run the ```deploy.ps1``` to deploy the .bicep template to azure from your local system.

## Prerequisites

- When using template specs: your login should have access to the template specs
- Your login needs the rights to deploy to Azure.
- Azure CLI must be installed on your local system
https:#aka.ms/installazurecliwindows

## Powershell deployment script

**Note**: _If there is any trouble with the az commands below - always  use 'az logout' before trying again to start with a clean login._

1. log into your azure account using  
   ```az login```
1. Select the right subscription NAME to connect to: see all the subscriptions available to your login using  
   ```az account list```
1. Run the script. It will will select the target subscription using  
   ```az account set --subscription "name of your subscription"```
   - Existing resource group

     ```Powershell
     .\deploy.ps1 -subscriptionName "..." -resourceGroupName "..."
     ```

   - Deploy to a subscription and create the containing resource group(s) as well

     ```Powershell
     .\deploy.ps1 -subscriptionName "..." -resourceGroupName "..." -includeResourceGroup
     ```

 For full help on all the parameters, run ```Get-Help -Name .\deploy.ps1 -Full```
