# Azure Terraform Environment

## Overview

* Terraform setup of Azure Environment
* Suitable for a production-like environment setup or for ci/cd environment initialization
* Terraform state is stored in Azure Storage Account to support a team environment
* Terraform remote state cannot use terraform variables, a bash search & replace is used instead

## Azure Portal Setup

* One-time per subscription: terraform remote step
* Create a new `resource group`, `storage account` and `container` for the [remote state](./remote-state.tf)

## Local Setup

* Once per local environment
* Install [Azure CLI](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest), not required when using Visual Studio Online
* Azure cli authentication: `az login`
* One-time per local environment after repository has been cloned
* Enable scripts execution: `chmod +x ./scripts/*.sh && chmod +x ./env/*.sh`
* Install terraform: `./scripts/local-setup-ubuntu-18.04.sh`

## Secrets Setup

```
export TF_VAR_function_app_authn_AppClientId='azure ad app client id'
export TF_VAR_function_app_authn_ClientSecret='azure ad app client secret'
```

## Environment setup

* Create a new file under ./env folder or update an existing file
* To select/change subscription: `az account set --subscription="SUBSCRIPTION_ID"`
* Verify the plan: `./scripts/plan.sh poc`
* Apply the plan: `./scripts/apply.sh poc`
* Destroy the plan: `./scripts/destroy.sh poc`

## TODO:

* Artifact download from Bitbucket - add uid/pwd to the url for private repos
