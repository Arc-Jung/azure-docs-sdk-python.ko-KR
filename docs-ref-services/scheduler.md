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
ms.openlocfilehash: 98e32799a4240f9946caf1ab7b05e35605d89dc9
ms.sourcegitcommit: f439ba940d5940359c982015db7ccfb82f9dffd9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2018
ms.locfileid: "52277063"
---
# <a name="azure-scheduler-libraries-for-python"></a>Python용 Azure Scheduler 라이브러리

## <a name="install-the-libraries"></a>라이브러리 설치

## <a name="management"></a>관리

```bash
pip install azure-mgmt-scheduler
```
## <a name="example"></a>예

### <a name="create-the-management-client"></a>관리 클라이언트 만들기

다음 코드는 관리 클라이언트의 인스턴스를 만듭니다.

[구독 목록](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping)에서 검색할 수 있는 ``subscription_id``를 제공해야 합니다.

Python SDK를 사용하여 Azure Active Directory 인증을 처리하고 ``Credentials`` 인스턴스를 만드는 방법에 대한 자세한 내용은 [리소스 관리 인증](/python/azure/python-sdk-azure-authenticate)을 참조하세요.

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

### <a name="create-a-job-collection"></a>작업 컬렉션 만들기

다음 코드는 기존 리소스 그룹 아래에서 작업 컬렉션을 만듭니다.
리소스 그룹을 만들거나 관리하려면 [리소스 관리](/python/api/overview/azure/azure.mgmt.resource)를 참조하세요.

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
> [관리 API 탐색](/python/api/overview/azure/scheduler/management)