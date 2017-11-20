---
title: "Python용 Azure DNS 라이브러리"
description: "Python용 Azure DNS 라이브러리에 대한 참조"
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
ms.openlocfilehash: 59ae3628b4a810db8fee21aacf46c13054dc8cd3
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-dns-libraries-for-python"></a><span data-ttu-id="b476c-104">Python용 Azure DNS 라이브러리</span><span class="sxs-lookup"><span data-stu-id="b476c-104">Azure DNS libraries for python</span></span>

## <a name="overview"></a><span data-ttu-id="b476c-105">개요</span><span class="sxs-lookup"><span data-stu-id="b476c-105">Overview</span></span>

<span data-ttu-id="b476c-106">[Azure DNS](/azure/dns/dns-overview)는 Azure 인프라를 통해 DNS 확인을 제공하는 DNS 도메인에 대한 호스팅 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="b476c-106">[Azure DNS](/azure/dns/dns-overview) is a hosting service for DNS domains that provides DNS resolution via the Azure infrastructure.</span></span>

<span data-ttu-id="b476c-107">Azure DNS를 시작하려면 [Azure Portal을 사용하여 Azure DNS 시작](/azure/dns/dns-getstarted-portal)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b476c-107">To get started with Azure DNS, see [Get started with Azure DNS using the Azure portal](/azure/dns/dns-getstarted-portal).</span></span>

## <a name="management-apis"></a><span data-ttu-id="b476c-108">관리 API</span><span class="sxs-lookup"><span data-stu-id="b476c-108">Management APIs</span></span>

<span data-ttu-id="b476c-109">관리 API를 사용하여 DNS 영역 및 레코드를 만들고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="b476c-109">Create and manage DNS zones and records with the management API.</span></span>

<span data-ttu-id="b476c-110">pip를 사용하여 관리 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b476c-110">Install the management package with pip.</span></span>

```bash
pip install azure-mgmt-dns
```

### <a name="example"></a><span data-ttu-id="b476c-111">예제</span><span class="sxs-lookup"><span data-stu-id="b476c-111">Example</span></span>

<span data-ttu-id="b476c-112">새 DNS 영역을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="b476c-112">Create a new DNS zone.</span></span>

```python
from azure.mgmt.dns import DnsManagementClient

dns_client = DnsManagementClient(credentials, 'your-subscription-id')
zone = dns_client.zones.create_or_update('resource-group',
                                         'zone_name_no_dot',
                                         {
                                            "location": "global"
                                         })

```

> [!div class="nextstepaction"]
> [<span data-ttu-id="b476c-113">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="b476c-113">Explore the Management APIs</span></span>](/python/api/overview/azure/dns/managementlibrary)
