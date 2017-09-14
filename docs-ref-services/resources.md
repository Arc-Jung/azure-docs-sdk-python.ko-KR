---
title: "Python용 Azure 리소스 라이브러리"
description: "Python용 Azure 리소스 라이브러리에 대한 참조"
keywords: "Azure, Python, SDK, API, 리소스"
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 08/11/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: f341e9066f48b35e182b4aba52b2f69e2b33e984
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-resources-libraries-for-python"></a><span data-ttu-id="c2283-104">Python용 Azure 리소스 라이브러리</span><span class="sxs-lookup"><span data-stu-id="c2283-104">Azure Resources libraries for python</span></span>

## <a name="overview"></a><span data-ttu-id="c2283-105">개요</span><span class="sxs-lookup"><span data-stu-id="c2283-105">Overview</span></span> 
<span data-ttu-id="c2283-106">[Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview)를 사용하여 그룹에서 리소스를 배포, 모니터링 및 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="c2283-106">Deploy, monitor, and manage resources in groups with [Azure Resource Manager](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-group-overview).</span></span>

## <a name="management-api"></a><span data-ttu-id="c2283-107">관리 API</span><span class="sxs-lookup"><span data-stu-id="c2283-107">Management API</span></span>
<span data-ttu-id="c2283-108">관리 API를 사용하여 리소스 그룹을 만들고, 템플릿에서 리소스를 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="c2283-108">Use the management API to create resource groups and deploy resources from templates.</span></span>

```bash
pip install azure-mgmt-resource
```
### <a name="example"></a><span data-ttu-id="c2283-109">예제</span><span class="sxs-lookup"><span data-stu-id="c2283-109">Example</span></span> 
<span data-ttu-id="c2283-110">Azure Eastern US 지역에 새 리소스 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c2283-110">Create a new resource group in the Azure Eastern US region.</span></span>

```python
from azure.mgmt.resource import ResourceManagementClient

LOCATION = 'eastus'
GROUP_NAME ='sample_resource_group'

resource_client = ResourceManagmentClient(credentials, subscription_id)
resource_client.resource_groups.create_or_update(GROUP_NAME, {'location': LOCATION})
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="c2283-111">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="c2283-111">Explore the Management APIs</span></span>](/python/api/overview/azure/resources/managementlibrary)

## <a name="samples"></a><span data-ttu-id="c2283-112">샘플</span><span class="sxs-lookup"><span data-stu-id="c2283-112">Samples</span></span>
[<span data-ttu-id="c2283-113">Azure 리소스 및 리소스 그룹 관리</span><span class="sxs-lookup"><span data-stu-id="c2283-113">Manage Azure resources and resource groups</span></span>](https://github.com/Azure-Samples/resource-manager-python-resources-and-groups)

<span data-ttu-id="c2283-114">Azure Resource Manager 샘플의 [전체 목록](https://azure.microsoft.com/resources/samples/?platform=python&term=resource)을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="c2283-114">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=python&term=resource) of Azure Resource Manager samples.</span></span>
