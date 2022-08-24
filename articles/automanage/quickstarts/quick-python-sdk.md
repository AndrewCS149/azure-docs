---
title: Quickstart - Python SDK
description: Create configuration profile assignments using the Python SDK for Automanage.
author: andrsmith
ms.service: automanage
ms.workload: infrastructure
ms.topic: quickstart
ms.date: 08/24/2022
ms.author: andrsmith
---

# Quickstart: Enable Azure Automanage for virtual machines using Python

Get started creating profile assignments using the [azure-sdk-for-python](https://github.com/Azure/azure-sdk-for-python).

## Prerequisites 

- An active [Azure Subscription](https://azure.microsoft.com/en-us/pricing/purchase-options/pay-as-you-go/)
- An existing [Virtual Machine](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/quick-create-portal)

> [!NOTE]
> Free trial accounts do not have access to the virtual machines used in this tutorial. Please upgrade to a Pay-As-You-Go subscription.

> [!IMPORTANT]
> You need to have the **Contributor** role on the resource group containing your VMs to enable Automanage. If you are enabling Automanage for the first time on a subscription, you need the following permissions: **Owner** role or **Contributor** along with **User Access Administrator** roles on your subscription.

## Install Required Packages 

For this demo, both the **Azure Identity** and **Azure Automanage** packages are required.

Use `pip` to install these packages: 

`pip install azure-identity`
`pip install azure-mgmt-automanage`

## Import Packages 

Import the **Azure Identity** and **Azure Automanage** packages into the script: 

```python
from azure.identity import DefaultAzureCredential
from azure.mgmt.automanage import AutomanageClient
```

## Authenticate to Azure & Create an Automanage Client

Use the **Azure Identity** package to authenticate to Azure and then create an Automanage Client:

```python 
credential = DefaultAzureCredential()
client = AutomanageClient(credential, "<subscription ID>")
```

## Enable Best Practices Configuration Profile to an Existing Virtual Machine

```python 
assignment = {
    "properties": {
        "configurationProfile": "/providers/Microsoft.Automanage/bestPractices/AzureBestPracticesProduction",
    }
}

client.configuration_profile_assignments.create_or_update("default", "resourceGroupName", "vmName", assignment)
```

## Next Steps

Learn how to conduct more operations with the Automanage Client by visiting the [azure-samples-python-management repo](https://github.com/Azure-Samples/azure-samples-python-management/tree/main/samples/automanage).

