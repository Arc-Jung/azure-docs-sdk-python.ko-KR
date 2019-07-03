---
title: Python용 Azure Batch 라이브러리
description: Python용 Batch에 대한 참조 설명서
keywords: Azure, Python, SDK, API, Batch, 처리, 일정 계획, 장기 실행
author: lisawong19
ms.author: routlaw
manager: douge
ms.date: 07/31/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: batch
ms.openlocfilehash: bbc691a8db6597c77575900b4e2a06f34ebb179c
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534350"
---
# <a name="azure-batch-libraries-for-python"></a><span data-ttu-id="327de-104">Python용 Azure Batch 라이브러리</span><span class="sxs-lookup"><span data-stu-id="327de-104">Azure Batch libraries for python</span></span>

## <a name="overview"></a><span data-ttu-id="327de-105">개요</span><span class="sxs-lookup"><span data-stu-id="327de-105">Overview</span></span>

<span data-ttu-id="327de-106">[Azure Batch](/azure/batch/batch-technical-overview)를 사용하여 클라우드에서 대규모 병렬 및 고성능 컴퓨팅 애플리케이션을 효율적으로 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="327de-106">Run large-scale parallel and high-performance computing applications efficiently in the cloud with [Azure Batch](/azure/batch/batch-technical-overview).</span></span>

<span data-ttu-id="327de-107">Azure Batch를 시작하려면 [Azure Portal에서 Batch 계정 만들기](/azure/batch/batch-account-create-portal)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="327de-107">To get started with Azure Batch, see [Create a Batch account with the Azure portal](/azure/batch/batch-account-create-portal).</span></span>

## <a name="install-the-libraries"></a><span data-ttu-id="327de-108">라이브러리 설치</span><span class="sxs-lookup"><span data-stu-id="327de-108">Install the libraries</span></span>

## <a name="client-library"></a><span data-ttu-id="327de-109">클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="327de-109">Client library</span></span>
<span data-ttu-id="327de-110">Azure Batch 클라이언트 라이브러리를 사용하여 계산 노드와 풀을 구성하고, 태스크를 정의하고 작업에서 실행되도록 구성하고, 작업 실행을 제어하고 모니터링하도록 작업 관리자를 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="327de-110">The Azure Batch client libraries let you configure compute nodes and pools, define tasks and configure them to run in jobs, and set up a job manager to control and monitor job execution.</span></span> <span data-ttu-id="327de-111">이러한 개체를 사용하여 대규모 병렬 계산 솔루션을 실행하는 방법에 대해 [자세히 알아보세요](/azure/batch/batch-api-basics).</span><span class="sxs-lookup"><span data-stu-id="327de-111">[Learn more](/azure/batch/batch-api-basics) about using these objects to run large-scale parallel compute solutions.</span></span>

```bash
pip install azure-batch
```
### <a name="example"></a><span data-ttu-id="327de-112">예</span><span class="sxs-lookup"><span data-stu-id="327de-112">Example</span></span>

<span data-ttu-id="327de-113">배치 계정에 Linux 계산 노드 풀을 설정하려면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="327de-113">Set up a pool of Linux compute nodes in a batch account:</span></span>

```python
# create the batch client for an account using its URI and keys
creds = batchauth.SharedKeyCredentials(account, key)
config = batch.BatchServiceClientConfiguration(creds, base_url = batch_url)
client = batch.BatchServiceClient(config)

# Create the VirtualMachineConfiguration, specifying
# the VM image reference and the Batch node agent to
# be installed on the node.
vmc = batchmodels.VirtualMachineConfiguration(
    image_reference = ir,
    node_agent_sku_id = "batch.node.ubuntu 14.04")

# Assign the virtual machine configuration to the pool
new_pool.virtual_machine_configuration = vmc

# Create pool in the Batch service
client.pool.add(new_pool)
```

## <a name="management-api"></a><span data-ttu-id="327de-114">관리 API</span><span class="sxs-lookup"><span data-stu-id="327de-114">Management API</span></span>
<span data-ttu-id="327de-115">Azure Batch 관리 라이브러리를 사용하여 Batch 계정을 만들고 삭제하고, Batch 계정 키를 읽고 다시 생성하며, Batch 계정 저장소를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="327de-115">Use the Azure Batch management libraries to create and delete batch accounts, read and regenerate batch account keys, and manage batch account storage.</span></span>

```bash
pip install azure-mgmt-batch
```
> [!div class="nextstepaction"]
> [<span data-ttu-id="327de-116">클라이언트 API 탐색</span><span class="sxs-lookup"><span data-stu-id="327de-116">Explore the Client APIs</span></span>](/python/api/overview/azure/batch/client)

### <a name="example"></a><span data-ttu-id="327de-117">예</span><span class="sxs-lookup"><span data-stu-id="327de-117">Example</span></span>
<span data-ttu-id="327de-118">Azure Batch 계정을 만들고, 새 애플리케이션 및 Azure Storage 계정을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="327de-118">Create an Azure Batch account and configure a new application and Azure storage account for it.</span></span>

```python
from azure.mgmt.batch import BatchManagementClient
from azure.mgmt.resource import ResourceManagementClient
from azure.mgmt.storage import StorageManagementClient

LOCATION ='eastus'
GROUP_NAME ='batchresourcegroup'
STORAGE_ACCOUNT_NAME ='batchstorageaccount'

# Create Resource group
print('Create Resource Group')
resource_client.resource_groups.create_or_update(GROUP_NAME, {'location': LOCATION})

# Create a storage account
storage_async_operation = storage_client.storage_accounts.create(
    GROUP_NAME,
    STORAGE_ACCOUNT_NAME,
    StorageAccountCreateParameters(
        sku=Sku(SkuName.standard_ragrs),
        kind=Kind.storage,
        location=LOCATION
    )
)
storage_account = storage_async_operation.result()

# Create a Batch Account, specifying the storage account we want to link
storage_resource = storage_account.id
batch_account = azure.mgmt.batch.models.BatchAccountCreateParameters(
    location=LOCATION,
    auto_storage=azure.mgmt.batch.models.AutoStorageBaseProperties(storage_resource)
)
creating = batch_client.account.create('MyBatchAccount', LOCATION, batch_account)
creating.wait()
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="327de-119">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="327de-119">Explore the Management APIs</span></span>](/python/api/overview/azure/batch/management)
