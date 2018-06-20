---
title: Python용 Azure 리소스 라이브러리
description: Python용 Azure 리소스 라이브러리에 대한 참조
keywords: Azure, Python, SDK, API, 리소스
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 08/11/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: d924a8aea18d9b59ec8c78d85dce8fe0ce7c8d6c
ms.sourcegitcommit: d521a7350216461eb2fa68152c4975f55152f831
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/06/2017
ms.locfileid: "26327991"
---
# <a name="azure-resources-libraries-for-python"></a><span data-ttu-id="d095b-104">Python용 Azure 리소스 라이브러리</span><span class="sxs-lookup"><span data-stu-id="d095b-104">Azure Resources libraries for python</span></span>

## <a name="overview"></a><span data-ttu-id="d095b-105">개요</span><span class="sxs-lookup"><span data-stu-id="d095b-105">Overview</span></span> 
<span data-ttu-id="d095b-106">[Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview)를 사용하여 그룹에서 리소스를 배포, 모니터링 및 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="d095b-106">Deploy, monitor, and manage resources in groups with [Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span></span>

## <a name="management-api"></a><span data-ttu-id="d095b-107">관리 API</span><span class="sxs-lookup"><span data-stu-id="d095b-107">Management API</span></span>
<span data-ttu-id="d095b-108">관리 API를 사용하여 리소스 그룹을 만들고, 템플릿에서 리소스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="d095b-108">Use the management API to create resource groups and deploy resources from templates.</span></span>

```bash
pip install azure-mgmt-resource
```
### <a name="example"></a><span data-ttu-id="d095b-109">예제</span><span class="sxs-lookup"><span data-stu-id="d095b-109">Example</span></span> 
<span data-ttu-id="d095b-110">Azure Eastern US 지역에 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="d095b-110">Create a new resource group in the Azure Eastern US region.</span></span>

```python
from azure.mgmt.resource import ResourceManagementClient

LOCATION = 'eastus'
GROUP_NAME ='sample_resource_group'

resource_client = ResourceManagementClient(credentials, subscription_id)
resource_client.resource_groups.create_or_update(GROUP_NAME, {'location': LOCATION})
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="d095b-111">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="d095b-111">Explore the Management APIs</span></span>](/python/api/overview/azure/azure.mgmt.resource)

## <a name="samples"></a><span data-ttu-id="d095b-112">샘플</span><span class="sxs-lookup"><span data-stu-id="d095b-112">Samples</span></span>
[<span data-ttu-id="d095b-113">Azure 리소스 및 리소스 그룹 관리</span><span class="sxs-lookup"><span data-stu-id="d095b-113">Manage Azure resources and resource groups</span></span>](https://github.com/Azure-Samples/resource-manager-python-resources-and-groups)

<span data-ttu-id="d095b-114">Azure Resource Manager 샘플의 [전체 목록](https://azure.microsoft.com/resources/samples/?platform=python&term=resource)을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="d095b-114">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=python&term=resource) of Azure Resource Manager samples.</span></span>
