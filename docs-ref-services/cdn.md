---
title: Python용 Azure CDN 라이브러리
description: Python용 Azure CDN 라이브러리에 대한 참조
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
ms.openlocfilehash: 92d6dd6ce55964bc48bb9bc654e8dec25f6b8344
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/23/2018
ms.locfileid: "29478886"
---
# <a name="azure-cdn-libraries-for-python"></a>Python용 Azure CDN 라이브러리

## <a name="overview"></a>개요

[CDN(Azure Content Delivery Network)](https://docs.microsoft.com/en-us/azure/cdn/cdn-overview)을 사용하면 전 세계에서 고대역폭 가용성을 보장하기 위해 웹 콘텐츠 캐시를 제공할 수 있습니다.

Azure CDN을 시작하려면 [Azure CDN 시작](https://docs.microsoft.com/en-us/azure/cdn/cdn-create-new-endpoint)을 참조하세요.

## <a name="management-apis"></a>관리 API

관리 API를 사용하여 Azure CDN을 생성, 쿼리 및 관리합니다.

pip를 통해 관리 패키지를 설치합니다.

```bash
pip install azure-mgmt-cdn
```

### <a name="example"></a>예

정의된 단일 끝점이 있는 CDN 프로필 만들기:

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
> [관리 API 탐색](/python/api/overview/azure/cdn/management)
