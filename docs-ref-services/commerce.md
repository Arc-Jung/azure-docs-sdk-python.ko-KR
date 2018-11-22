---
title: Python용 Azure 상거래 라이브러리
description: Python용 Azure 상거래 라이브러리에 대한 참조
keywords: Azure, Python, SDK, API, 상거래
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 02/21/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 27b826c1f11aca0d8c49c4e8eab4277b857eea37
ms.sourcegitcommit: f439ba940d5940359c982015db7ccfb82f9dffd9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2018
ms.locfileid: "52277235"
---
# <a name="azure-commerce-libraries-for-python"></a><span data-ttu-id="f8ee1-104">Python용 Azure 상거래 라이브러리</span><span class="sxs-lookup"><span data-stu-id="f8ee1-104">Azure Commerce libraries for python</span></span>

## <a name="management-apipythonapioverviewazurecommercemanagement"></a>[<span data-ttu-id="f8ee1-105">관리 API</span><span class="sxs-lookup"><span data-stu-id="f8ee1-105">Management API</span></span>](/python/api/overview/azure/commerce/management)

```bash
pip install azure-mgmt-commerce
```
## <a name="create-the-commerce-client"></a><span data-ttu-id="f8ee1-106">상거래 클라이언트 만들기</span><span class="sxs-lookup"><span data-stu-id="f8ee1-106">Create the commerce client</span></span>

<span data-ttu-id="f8ee1-107">다음 코드는 관리 클라이언트의 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f8ee1-107">The following code creates an instance of the management client.</span></span>

<span data-ttu-id="f8ee1-108">[구독 목록](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping)에서 검색할 수 있는 ``subscription_id``를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f8ee1-108">You will need to provide your ``subscription_id`` which can be retrieved from [your subscription list](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span></span>

<span data-ttu-id="f8ee1-109">Python SDK를 사용하여 Azure Active Directory 인증을 처리하고 ``Credentials`` 인스턴스를 만드는 방법에 대한 자세한 내용은 [리소스 관리 인증](/python/azure/python-sdk-azure-authenticate)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f8ee1-109">See [Resource Management Authentication](/python/azure/python-sdk-azure-authenticate) for details on handling Azure Active Directory authentication with the Python SDK, and creating a ``Credentials`` instance.</span></span>

```python
from azure.mgmt.commerce import UsageManagementClient
from azure.common.credentials import UserPassCredentials

# Replace this with your subscription id
subscription_id = '33333333-3333-3333-3333-333333333333'

# See above for details on creating different types of AAD credentials
credentials = UserPassCredentials(
    'user@domain.com',  # Your user
    'my_password',      # Your password
)

commerce_client = UsageManagementClient(
    credentials,
    subscription_id
)
``` 

## <a name="get-rate-card"></a><span data-ttu-id="f8ee1-110">요금표 가져오기</span><span class="sxs-lookup"><span data-stu-id="f8ee1-110">Get rate card</span></span>

```python
# OfferDurableID: https://azure.microsoft.com/en-us/support/legal/offer-details/
rate = commerce_client.rate_card.get(
    "OfferDurableId eq 'MS-AZR-0062P' and Currency eq 'USD' and Locale eq 'en-US' and RegionInfo eq 'US'"
)
```

## <a name="get-usage"></a><span data-ttu-id="f8ee1-111">사용량 가져오기</span><span class="sxs-lookup"><span data-stu-id="f8ee1-111">Get Usage</span></span>

```python
from datetime import date, timedelta

# Takes onky dates in full ISO8601 with 'T00:00:00Z'
# Return an iterator like object: https://docs.python.org/3/library/stdtypes.html#iterator-types
usage_iterator = commerce_client.usage_aggregates.list(
    str(date.today() - timedelta(days=1))+'T00:00:00Z',
    str(date.today())+'T00:00:00Z'
)
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="f8ee1-112">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="f8ee1-112">Explore the Management APIs</span></span>](/python/api/overview/azure/commerce/management)