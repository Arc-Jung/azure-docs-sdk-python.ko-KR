---
title: "Python용 Azure DevTest Labs 라이브러리"
description: "Python용 Azure DevTest Labs 라이브러리에 대한 참조"
keywords: Azure, Python, SDK, API, DevTest Labs
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 02/21/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 5807b85f02c05c2a767a2df2e89d9e98b7e6e05b
ms.sourcegitcommit: d7c26ac167cf6a6491358ac3153f268bc90e55e9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/24/2018
---
# <a name="azure-devtest-labs-libraries-for-python"></a><span data-ttu-id="04999-104">Python용 Azure DevTest Labs 라이브러리</span><span class="sxs-lookup"><span data-stu-id="04999-104">Azure DevTest Labs libraries for python</span></span>

## <a name="management-apipythonapioverviewazuredevtestlabsmanagement"></a>[<span data-ttu-id="04999-105">관리 API</span><span class="sxs-lookup"><span data-stu-id="04999-105">Management API</span></span>](/python/api/overview/azure/devtestlabs/management)

```bash
pip install azure-mgmt-devtestlabs
```

## <a name="create-the-management-client"></a><span data-ttu-id="04999-106">관리 클라이언트 만들기</span><span class="sxs-lookup"><span data-stu-id="04999-106">Create the management client</span></span>

<span data-ttu-id="04999-107">다음 코드는 관리 클라이언트의 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="04999-107">The following code creates an instance of the management client.</span></span>

<span data-ttu-id="04999-108">[구독 목록](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping)에서 검색할 수 있는 ``subscription_id``를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="04999-108">You will need to provide your ``subscription_id`` which can be retrieved from [your subscription list](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span></span>

<span data-ttu-id="04999-109">Python SDK를 사용하여 Azure Active Directory 인증을 처리하고 ``Credentials`` 인스턴스를 만드는 방법에 대한 자세한 내용은 [리소스 관리 인증](/python/azure/python-sdk-azure-authenticate)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="04999-109">See [Resource Management Authentication](/python/azure/python-sdk-azure-authenticate) for details on handling Azure Active Directory authentication with the Python SDK, and creating a ``Credentials`` instance.</span></span>

```python
from azure.mgmt.devtestlabs import DevTestLabsClient
from azure.common.credentials import UserPassCredentials

# Replace this with your subscription id
subscription_id = '33333333-3333-3333-3333-333333333333'

# See above for details on creating different types of AAD credentials
credentials = UserPassCredentials(
    'user@domain.com',  # Your user
    'my_password',      # Your password
)

devtestlabs_client = DevTestLabsClient(
    credentials,
    subscription_id
)
```

## <a name="create-lab"></a><span data-ttu-id="04999-110">랩 만들기</span><span class="sxs-lookup"><span data-stu-id="04999-110">Create lab</span></span>

```python
async_lab = self.client.lab.create_or_update_resource(
    'MyResourceGroup',
    'MyLab',
    {'location': 'westus'}
)
lab = async_lab.result() # Blocking wait
``` 

> [!div class="nextstepaction"]
> [<span data-ttu-id="04999-111">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="04999-111">Explore the Management APIs</span></span>](/python/api/overview/azure/devtestlabs/management)