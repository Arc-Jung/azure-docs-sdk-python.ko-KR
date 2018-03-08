---
title: "Python용 Azure 상거래 라이브러리"
description: "Python용 Azure 상거래 라이브러리에 대한 참조"
keywords: "Azure, Python, SDK, API, 상거래"
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 02/21/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 77008eb76c3a925d9c7e63fe9360ea5b25da49de
ms.sourcegitcommit: d7c26ac167cf6a6491358ac3153f268bc90e55e9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/24/2018
---
# <a name="azure-commerce-libraries-for-python"></a>Python용 Azure 상거래 라이브러리

## <a name="management-apipythonapioverviewazurecommercemanagement"></a>[관리 API](/python/api/overview/azure/commerce/management)

```bash
pip install azure-mgmt-commerce
```
## <a name="create-the-commerce-client"></a>상거래 클라이언트 만들기

다음 코드는 관리 클라이언트의 인스턴스를 만듭니다.

[구독 목록](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping)에서 검색할 수 있는 ``subscription_id``를 제공해야 합니다.

Python SDK를 사용하여 Azure Active Directory 인증을 처리하고 ``Credentials`` 인스턴스를 만드는 방법에 대한 자세한 내용은 [리소스 관리 인증](/python/azure/python-sdk-azure-authenticate)을 참조하세요.

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

## <a name="get-rate-card"></a>요금표 가져오기

```python
# OfferDurableID: https://azure.microsoft.com/en-us/support/legal/offer-details/
rate = commerce_client.rate_card.get(
    "OfferDurableId eq 'MS-AZR-0062P' and Currency eq 'USD' and Locale eq 'en-US' and RegionInfo eq 'US'"
)
```

## <a name="get-usage"></a>사용량 가져오기

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
> [관리 API 탐색](/python/api/overview/azure/commerce/management)