# Azure Infra Deployment

This repository contains an Azure Resource Manager (ARM) template that deploys a single Azure Storage Account.

## What is included

- `Infra/template.json`
  - Defines a `Microsoft.Storage/storageAccounts` resource.
  - Uses parameters for:
    - `storageAccountName`
    - `location`
    - `skuName`
    - `kind`
    - `accessTier`
  - Enforces `supportsHttpsTrafficOnly` and `minimumTlsVersion` set to `TLS1_2`.
  - Exposes an output `storageAccountId`.

- `Infra/parameters.json`
  - Provides default parameter values used by the deployment:
    - `storageAccountName`: `ameylatkargha006`
    - `location`: `eastus`
    - `skuName`: `Standard_LRS`
    - `kind`: `StorageV2`
    - `accessTier`: `Hot`

## Deploying the template

Use Azure CLI to deploy the template with the parameters file, for example:

```bash
az deployment group create \
  --resource-group <your-resource-group> \
  --template-file Infra/template.json \
  --parameters Infra/parameters.json
```

## Service principal

Use this command to generate a service principal for deployment authentication:

```bash
az ad sp create-for-rbac --name "azureinfradeployment" --sdk-auth --role Contributor --scopes /subscriptions/b59e0370-1804-4bde-b8be-889ebbb7d72c
```
