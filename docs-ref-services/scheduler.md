---
title: Python용 Azure Scheduler 라이브러리
description: Python용 Azure Scheduler 라이브러리에 대한 참조
keywords: Azure, Python, SDK, API, Scheduler
author: lisawong19
ms.author: liwong
manager: mbaldwin
ms.date: 02/21/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 3d2691ae1ba84c41f25de2b099aacefaa92152ed
ms.sourcegitcommit: d7c26ac167cf6a6491358ac3153f268bc90e55e9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/24/2018
ms.locfileid: "29551616"
---
# <a name="azure-scheduler-libraries-for-python"></a><span data-ttu-id="e746e-104">Python용 Azure Scheduler 라이브러리</span><span class="sxs-lookup"><span data-stu-id="e746e-104">Azure Scheduler libraries for python</span></span>

## <a name="install-the-libraries"></a><span data-ttu-id="e746e-105">라이브러리 설치</span><span class="sxs-lookup"><span data-stu-id="e746e-105">Install the libraries</span></span>

## <a name="management"></a><span data-ttu-id="e746e-106">관리</span><span class="sxs-lookup"><span data-stu-id="e746e-106">Management</span></span>

```bash
pip install azure-mgmt-scheduler
```
## <a name="example"></a><span data-ttu-id="e746e-107">예</span><span class="sxs-lookup"><span data-stu-id="e746e-107">Example</span></span>

### <a name="create-the-management-client"></a><span data-ttu-id="e746e-108">관리 클라이언트 만들기</span><span class="sxs-lookup"><span data-stu-id="e746e-108">Create the management client</span></span>

<span data-ttu-id="e746e-109">다음 코드는 관리 클라이언트의 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e746e-109">The following code creates an instance of the management client.</span></span>

<span data-ttu-id="e746e-110">[구독 목록](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping)에서 검색할 수 있는 ``subscription_id``를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e746e-110">You will need to provide your ``subscription_id`` which can be retrieved from [your subscription list](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span></span>

<span data-ttu-id="e746e-111">Python SDK를 사용하여 Azure Active Directory 인증을 처리하고 ``Credentials`` 인스턴스를 만드는 방법에 대한 자세한 내용은 [리소스 관리 인증](/python/azure/python-sdk-azure-authenticate)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e746e-111">See [Resource Management Authentication](/python/azure/python-sdk-azure-authenticate) for details on handling Azure Active Directory authentication with the Python SDK, and creating a ``Credentials`` instance.</span></span>

```python
from azure.mgmt.scheduler import SchedulerManagementClient
from azure.common.credentials import UserPassCredentials

# Replace this with your subscription id
subscription_id = '33333333-3333-3333-3333-333333333333'

# See above for details on creating different types of AAD credentials
credentials = UserPassCredentials(
    'user@domain.com',  # Your user
    'my_password',      # Your password
)

scheduler_client = SchedulerManagementClient(
    credentials,
    subscription_id
)
```

### <a name="create-a-job-collection"></a><span data-ttu-id="e746e-112">작업 컬렉션 만들기</span><span class="sxs-lookup"><span data-stu-id="e746e-112">Create a job collection</span></span>

<span data-ttu-id="e746e-113">다음 코드는 기존 리소스 그룹 아래에서 작업 컬렉션을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e746e-113">The following code creates a job collection under an existing resource group.</span></span>
<span data-ttu-id="e746e-114">리소스 그룹을 만들거나 관리하려면 [리소스 관리](/python/api/overview/azure/azure.mgmt.resource)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e746e-114">To create or manage resource groups, see [Resource Management](/python/api/overview/azure/azure.mgmt.resource).</span></span>

```python
from azure.mgmt.scheduler.models import JobCollectionDefinition, JobCollectionProperties, Sku

group_name = 'myresourcegroup'
job_collection_name = "myjobcollection"
scheduler_client.job_collections.create_or_update(
    group_name,
    job_collection_name,
    JobCollectionDefinition(
        location = "West US",
        properties = JobCollectionProperties(
            sku = Sku(
                name="Free"
            )
        )
    )
)
# scheduler_client is a JobCollectionDefinition instance
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="e746e-115">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="e746e-115">Explore the Management APIs</span></span>](/python/api/overview/azure/scheduler/management)