---
title: "Python용 Azure Redis 라이브러리"
description: "Python용 Redis 라이브러리에 대한 참조 설명서"
keywords: "Azure, Python, Redis, API, SDK, 데이터베이스, NoSQL"
author: sptramer
ms.author: sttramer
manager: douge
ms.date: 06/26/2017
ms.topic: article
ms.devlang: python
ms.service: redis
ms.openlocfilehash: 3ba8d972e91fad229c1489800edeca08760254e6
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-redis-cache-libraries-for-python"></a><span data-ttu-id="54331-104">Python용 Azure Redis Cache 라이브러리</span><span class="sxs-lookup"><span data-stu-id="54331-104">Azure Redis Cache libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="54331-105">개요</span><span class="sxs-lookup"><span data-stu-id="54331-105">Overview</span></span>

<span data-ttu-id="54331-106">Azure Redis Cache는 인기 있는 Redis 프로젝트 오픈 소스를 기반으로 합니다.</span><span class="sxs-lookup"><span data-stu-id="54331-106">Azure Redis Cache is based on the popular open source Redis project.</span></span> <span data-ttu-id="54331-107">Microsoft에서 관리하고 Azure 앱에서 액세스할 수 있는 안전한 전용 Redis 인스턴스에 대한 액세스를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="54331-107">It gives you access to a secure, dedicated Redis instance, managed by Microsoft and accessible from your Azure apps.</span></span>

<span data-ttu-id="54331-108">Redis는 고급 키-값 저장소이며, 키에는 문자열, 해시, 목록, 집합, 정렬된 집합과 같은 데이터 구조가 포함될 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="54331-108">Redis is an advanced key-value store, where keys can contain data structures such as strings, hashes, lists, sets, and sorted sets.</span></span> <span data-ttu-id="54331-109">Redis는 이러한 데이터 유형에 대한 소규모 작업 집합을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="54331-109">Redis supports a set of atomic operations on these data types.</span></span>

<span data-ttu-id="54331-110">[Azure Redis Cache](https://docs.microsoft.com/azure/redis-cache/)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="54331-110">Learn more about [Azure Redis Cache](https://docs.microsoft.com/azure/redis-cache/).</span></span>

## <a name="management-api"></a><span data-ttu-id="54331-111">관리 API</span><span class="sxs-lookup"><span data-stu-id="54331-111">Management API</span></span>

<span data-ttu-id="54331-112">Redis 관리 API를 사용하여 구독의 Redis 리소스를 만들고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="54331-112">Create and manage your Redis resources in your subscription with the Redis management API.</span></span>

```bash
pip install redis
pip install azure-mgmt-redis
```

### <a name="example"></a><span data-ttu-id="54331-113">예제</span><span class="sxs-lookup"><span data-stu-id="54331-113">Example</span></span>

<span data-ttu-id="54331-114">다음 예제에서는 새 Redis 캐시를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="54331-114">The following example creates a new Redis cache:</span></span>

```python
from azure.mgmt.redis import RedisManagementClient
from azure.mgmt.redis.models import Sku, RedisCreateOrUpdateParameters

redis_client = RedisManagementClient(
    credentials,
    subscription_id
)
group_name = 'myresourcegroup'
cache_name = 'mycachename'
redis_cache = redis_client.redis.create_or_update(
    group_name,
    cache_name,
    RedisCreateOrUpdateParameters(
        sku = Sku(name = 'Basic', family = 'C', capacity = '1'),
        location = "East US"
    )
)
# redis_cache is a RedisResourceWithAccessKey instance
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="54331-115">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="54331-115">Explore the Management APIs</span></span>](/python/api/overview/azure/redis/managementlibrary)

