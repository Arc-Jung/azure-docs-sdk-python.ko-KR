---
title: Python용 Azure 권한 부여 라이브러리
description: Python용 Azure 권한 부여 라이브러리에 대한 참조
keywords: Azure, Python, SDK, API, 권한 부여
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 02/21/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 8709bbd3cff448c7beb394621b163a4b3e3c3cd8
ms.sourcegitcommit: f439ba940d5940359c982015db7ccfb82f9dffd9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2018
ms.locfileid: "52276767"
---
# <a name="azure-authorization-libraries-for-python"></a><span data-ttu-id="4036d-104">Python용 Azure 권한 부여 라이브러리</span><span class="sxs-lookup"><span data-stu-id="4036d-104">Azure Authorization libraries for python</span></span>

## <a name="management-apipythonapioverviewazureauthorizationmanagement"></a>[<span data-ttu-id="4036d-105">관리 API</span><span class="sxs-lookup"><span data-stu-id="4036d-105">Management API</span></span>](/python/api/overview/azure/authorization/management)

```bash
pip install azure-mgmt-authorization
```

## <a name="create-the-management-client"></a><span data-ttu-id="4036d-106">관리 클라이언트 만들기</span><span class="sxs-lookup"><span data-stu-id="4036d-106">Create the management client</span></span>

<span data-ttu-id="4036d-107">다음 코드는 관리 클라이언트의 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4036d-107">The following code creates an instance of the management client.</span></span>

<span data-ttu-id="4036d-108">[구독 목록](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping)에서 검색할 수 있는 ``subscription_id``를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4036d-108">You will need to provide your ``subscription_id`` which can be retrieved from [your subscription list](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span></span>

<span data-ttu-id="4036d-109">Python SDK를 사용하여 Azure Active Directory 인증을 처리하고 ``Credentials`` 인스턴스를 만드는 방법에 대한 자세한 내용은 [리소스 관리 인증](/python/azure/python-sdk-azure-authenticate)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4036d-109">See [Resource Management Authentication](/python/azure/python-sdk-azure-authenticate) for details on handling Azure Active Directory authentication with the Python SDK, and creating a ``Credentials`` instance.</span></span>

```python
from azure.mgmt.authorization import AuthorizationManagementClient
from azure.common.credentials import UserPassCredentials

# Replace this with your subscription id
subscription_id = '33333333-3333-3333-3333-333333333333'

# See above for details on creating different types of AAD credentials
credentials = UserPassCredentials(
    'user@domain.com',  # Your user
    'my_password'       # Your password
)

authorization_client = AuthorizationManagementClient(
    credentials,
    subscription_id
)
``` 

## <a name="check-permissions-for-a-resource-group"></a><span data-ttu-id="4036d-110">리소스 그룹의 사용 권한 확인</span><span class="sxs-lookup"><span data-stu-id="4036d-110">Check permissions for a resource group</span></span>

<span data-ttu-id="4036d-111">다음 코드는 지정된 리소스 그룹에서 사용 권한을 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4036d-111">The following code checks permissions in a given resource group.</span></span>
<span data-ttu-id="4036d-112">리소스 그룹을 만들거나 관리하려면 [리소스 관리](/python/api/overview/azure/azure.mgmt.resource)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4036d-112">To create or manage resource groups, see [Resource Management](/python/api/overview/azure/azure.mgmt.resource).</span></span>

```python
from azure.mgmt.redis.models import Sku, RedisCreateOrUpdateParameters

group_name = 'myresourcegroup'
permissions = self.authorization_client.permissions.list_for_resource_group(
    group_name
)
# permissions is a iterable of Permissions instances
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="4036d-113">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="4036d-113">Explore the Management APIs</span></span>](/python/api/overview/azure/authorization/management)

