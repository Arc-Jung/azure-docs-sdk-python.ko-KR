---
title: Python용 Azure 리소스 라이브러리
description: Python용 Azure 리소스 라이브러리에 대한 참조
keywords: Azure, Python, SDK, API, 리소스
author: lisawong19
ms.author: routlaw
manager: routlaw
ms.date: 08/11/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: cef1f2bad7dcb3ff73aeae9c56000fb949541df9
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534221"
---
# <a name="azure-resources-libraries-for-python"></a>Python용 Azure 리소스 라이브러리

## <a name="overview"></a>개요 
[Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview)를 사용하여 그룹에서 리소스를 배포, 모니터링 및 관리합니다.

## <a name="management-api"></a>관리 API
관리 API를 사용하여 리소스 그룹을 만들고, 템플릿에서 리소스를 배포합니다.

```bash
pip install azure-mgmt-resource
```
### <a name="example"></a>예 
Azure Eastern US 지역에 새 리소스 그룹을 만듭니다.

```python
from azure.mgmt.resource import ResourceManagementClient

LOCATION = 'eastus'
GROUP_NAME ='sample_resource_group'

resource_client = ResourceManagementClient(credentials, subscription_id)
resource_client.resource_groups.create_or_update(GROUP_NAME, {'location': LOCATION})
```

> [!div class="nextstepaction"]
> [관리 API 탐색](/python/api/overview/azure/azure.mgmt.resource)

## <a name="samples"></a>샘플
[Azure 리소스 및 리소스 그룹 관리](https://github.com/Azure-Samples/resource-manager-python-resources-and-groups)

Azure Resource Manager 샘플의 [전체 목록](https://azure.microsoft.com/resources/samples/?platform=python&term=resource)을 봅니다.
