---
title: Python용 Azure DNS 라이브러리
description: Python용 Azure DNS 라이브러리에 대한 참조
keywords: Azure, Python, SDK, API, DNS
author: sptramer
ms.author: sttramer
manager: douge
ms.date: 07/10/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: c70c3d44911b28b0a8c92b5f7efeca3bf1611f43
ms.sourcegitcommit: f439ba940d5940359c982015db7ccfb82f9dffd9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2018
ms.locfileid: "52277255"
---
# <a name="azure-dns-libraries-for-python"></a><span data-ttu-id="9a3fa-104">Python용 Azure DNS 라이브러리</span><span class="sxs-lookup"><span data-stu-id="9a3fa-104">Azure DNS libraries for python</span></span>

## <a name="overview"></a><span data-ttu-id="9a3fa-105">개요</span><span class="sxs-lookup"><span data-stu-id="9a3fa-105">Overview</span></span>

<span data-ttu-id="9a3fa-106">[Azure DNS](/azure/dns/dns-overview)는 Azure 인프라를 통해 DNS 확인을 제공하는 DNS 도메인에 대한 호스팅 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="9a3fa-106">[Azure DNS](/azure/dns/dns-overview) is a hosting service for DNS domains that provides DNS resolution via the Azure infrastructure.</span></span>

<span data-ttu-id="9a3fa-107">Azure DNS를 시작하려면 [Azure Portal을 사용하여 Azure DNS 시작](/azure/dns/dns-getstarted-portal)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9a3fa-107">To get started with Azure DNS, see [Get started with Azure DNS using the Azure portal](/azure/dns/dns-getstarted-portal).</span></span>

## <a name="management-apipythonapioverviewazurednsmanagement"></a>[<span data-ttu-id="9a3fa-108">관리 API</span><span class="sxs-lookup"><span data-stu-id="9a3fa-108">Management API</span></span>](/python/api/overview/azure/dns/management)

```bash
pip install azure-mgmt-dns
```

## <a name="create-the-management-client"></a><span data-ttu-id="9a3fa-109">관리 클라이언트 만들기</span><span class="sxs-lookup"><span data-stu-id="9a3fa-109">Create the management client</span></span>

<span data-ttu-id="9a3fa-110">다음 코드는 관리 클라이언트의 인스턴스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="9a3fa-110">The following code creates an instance of the management client.</span></span>

<span data-ttu-id="9a3fa-111">[구독 목록](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping)에서 검색할 수 있는 ``subscription_id``를 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="9a3fa-111">You will need to provide your ``subscription_id`` which can be retrieved from [your subscription list](https://manage.windowsazure.com/#Workspaces/AdminTasks/SubscriptionMapping).</span></span>

<span data-ttu-id="9a3fa-112">Python SDK를 사용하여 Azure Active Directory 인증을 처리하고 ``Credentials`` 인스턴스를 만드는 방법에 대한 자세한 내용은 [리소스 관리 인증](/python/azure/python-sdk-azure-authenticate)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="9a3fa-112">See [Resource Management Authentication](/python/azure/python-sdk-azure-authenticate) for details on handling Azure Active Directory authentication with the Python SDK, and creating a ``Credentials`` instance.</span></span>

```python 
from azure.mgmt.dns import DnsManagementClient
from azure.common.credentials import UserPassCredentials

# Replace this with your subscription id
subscription_id = '33333333-3333-3333-3333-333333333333'

# See above for details on creating different types of AAD credentials
credentials = UserPassCredentials(
    'user@domain.com',  # Your user
    'my_password',      # Your password
)

dns_client = DnsManagementClient(
    credentials,
    subscription_id
)
```

## <a name="create-dns-zone"></a><span data-ttu-id="9a3fa-113">DNS 영역 만들기</span><span class="sxs-lookup"><span data-stu-id="9a3fa-113">Create DNS zone</span></span>
```python
# The only valid value is 'global', otherwise you will get a:
# The subscription is not registered for the resource type 'dnszones' in the location 'westus'.
zone = dns_client.zones.create_or_update(
    'MyResourceGroup',
    'pydns.com',
    {
            'zone_type': 'Public', # or Private
        'location': 'global'
    }
)
```
    
## <a name="create-a-record-set"></a><span data-ttu-id="9a3fa-114">레코드 집합 만들기</span><span class="sxs-lookup"><span data-stu-id="9a3fa-114">Create a Record Set</span></span>
```python
record_set = dns_client.record_sets.create_or_update(
    'MyResourceGroup',
    'pydns.com',
    'MyRecordSet',
    'A',
    {
            "ttl": 300,
            "arecords": [
                {
                "ipv4_address": "1.2.3.4"
                },
                {
                "ipv4_address": "1.2.3.5"
                }
            ]
    }
)
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="9a3fa-115">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="9a3fa-115">Explore the Management APIs</span></span>](/python/api/overview/azure/dns/management)
