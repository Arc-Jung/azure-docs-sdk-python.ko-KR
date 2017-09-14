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
# <a name="azure-redis-cache-libraries-for-python"></a>Python용 Azure Redis Cache 라이브러리

## <a name="overview"></a>개요

Azure Redis Cache는 인기 있는 Redis 프로젝트 오픈 소스를 기반으로 합니다. Microsoft에서 관리하고 Azure 앱에서 액세스할 수 있는 안전한 전용 Redis 인스턴스에 대한 액세스를 제공합니다.

Redis는 고급 키-값 저장소이며, 키에는 문자열, 해시, 목록, 집합, 정렬된 집합과 같은 데이터 구조가 포함될 수 있습니다. Redis는 이러한 데이터 유형에 대한 소규모 작업 집합을 지원합니다.

[Azure Redis Cache](https://docs.microsoft.com/azure/redis-cache/)에 대해 자세히 알아보세요.

## <a name="management-api"></a>관리 API

Redis 관리 API를 사용하여 구독의 Redis 리소스를 만들고 관리합니다.

```bash
pip install redis
pip install azure-mgmt-redis
```

### <a name="example"></a>예제

다음 예제에서는 새 Redis 캐시를 만듭니다.

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
> [관리 API 탐색](/python/api/overview/azure/redis/managementlibrary)

