---
title: "Python용 Azure CDN 라이브러리"
description: "Python용 Azure CDN 라이브러리에 대한 참조"
keywords: Azure, Python, SDK, API, CDN
author: sptramer
ms.author: sttramer
manager: douge
ms.date: 07/10/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: c704b32ff5fd6db922ef9c296142832455088562
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cdn-libraries-for-python"></a><span data-ttu-id="b9e26-104">Python용 Azure CDN 라이브러리</span><span class="sxs-lookup"><span data-stu-id="b9e26-104">Azure CDN libraries for python</span></span>

## <a name="overview"></a><span data-ttu-id="b9e26-105">개요</span><span class="sxs-lookup"><span data-stu-id="b9e26-105">Overview</span></span>

<span data-ttu-id="b9e26-106">[CDN(Azure Content Delivery Network)](https://docs.microsoft.com/en-us/azure/cdn/cdn-overview)을 사용하면 전 세계에서 고대역폭 가용성을 보장하기 위해 웹 콘텐츠 캐시를 제공할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b9e26-106">[Azure Content Delivery Network (CDN)](https://docs.microsoft.com/en-us/azure/cdn/cdn-overview) allows you to provide web content caches to ensure high-bandwidth availability across the globe.</span></span>

<span data-ttu-id="b9e26-107">Azure CDN을 시작하려면 [Azure CDN 시작](https://docs.microsoft.com/en-us/azure/cdn/cdn-create-new-endpoint)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="b9e26-107">To get started with Azure CDN, see [Getting started with Azure CDN](https://docs.microsoft.com/en-us/azure/cdn/cdn-create-new-endpoint).</span></span>

## <a name="management-apis"></a><span data-ttu-id="b9e26-108">관리 API</span><span class="sxs-lookup"><span data-stu-id="b9e26-108">Management APIs</span></span>

<span data-ttu-id="b9e26-109">관리 API를 사용하여 Azure CDN을 생성, 쿼리 및 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="b9e26-109">Create, query, and manage Azure CDNs with the management API.</span></span>

<span data-ttu-id="b9e26-110">pip를 통해 관리 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="b9e26-110">Install the management package via pip.</span></span>

```bash
pip install azure-mgmt-cdn
```

### <a name="example"></a><span data-ttu-id="b9e26-111">예제</span><span class="sxs-lookup"><span data-stu-id="b9e26-111">Example</span></span>

<span data-ttu-id="b9e26-112">정의된 단일 끝점이 있는 CDN 프로필 만들기:</span><span class="sxs-lookup"><span data-stu-id="b9e26-112">Creating a CDN profile with a single defined endpoint:</span></span>

```python
from azure.mgmt.cdn import CdnManagementClient

cdn_client = CdnManagementClient(credentials, 'your-subscription-id')
profile_poller = cdn_client.profiles.create('my-resource-group',
                                            'cdn-name',
                                            {
                                                "location": "some_region", 
                                                "sku": {
                                                    "name": "sku_tier"
                                                } 
                                            })
profile = profile_poller.result()

endpoint_poller = client.endpoints.create('my-resource-group',
                                          'cdn-name',
                                          'unique-endpoint-name', 
                                          { 
                                              "location": "any_region", 
                                              "origins": [
                                                  {
                                                      "name": "origin_name", 
                                                      "host_name": "url"
                                                  }]
                                          })
endpoint = endpoint_poller.result()
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="b9e26-113">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="b9e26-113">Explore the Management APIs</span></span>](/python/api/overview/azure/cdn/managementlibrary)
