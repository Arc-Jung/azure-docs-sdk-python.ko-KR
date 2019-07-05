---
title: Python용 Azure 리소스 라이브러리
description: ''
keywords: Azure, Python, SDK, API, 리소스
author: lisawong19
ms.author: routlaw
manager: douge
ms.date: 06/19/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: resources
ms.openlocfilehash: d708a5e7296b166b6e55b9b7b0d995e72e264267
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534374"
---
# <a name="azure-resources-libraries-for-python"></a><span data-ttu-id="4b8e1-103">Python용 Azure 리소스 라이브러리</span><span class="sxs-lookup"><span data-stu-id="4b8e1-103">Azure Resources libraries for Python</span></span> 

## <a name="overview"></a><span data-ttu-id="4b8e1-104">개요</span><span class="sxs-lookup"><span data-stu-id="4b8e1-104">Overview</span></span> 
<span data-ttu-id="4b8e1-105">리소스 그룹에서 Azure 리소스를 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="4b8e1-105">Manage Azure resources in resource groups.</span></span>

| <span data-ttu-id="4b8e1-106">패키지</span><span class="sxs-lookup"><span data-stu-id="4b8e1-106">Package</span></span>  |  <span data-ttu-id="4b8e1-107">설명</span><span class="sxs-lookup"><span data-stu-id="4b8e1-107">Description</span></span> |
|---|---|
|<span data-ttu-id="4b8e1-108">[azure.mgmt.resource.features][1]</span><span class="sxs-lookup"><span data-stu-id="4b8e1-108">[azure.mgmt.resource.features][1]</span></span>|<span data-ttu-id="4b8e1-109">AFEC(Azure Feature Exposure Control)는 리소스 공급자가 사용자에 대한 기능 노출을 제어하는 메커니즘을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4b8e1-109">Azure Feature Exposure Control (AFEC) provides a mechanism for the resource providers to control feature exposure to users.</span></span>|
|<span data-ttu-id="4b8e1-110">[azure.mgmt.resource.links][2]</span><span class="sxs-lookup"><span data-stu-id="4b8e1-110">[azure.mgmt.resource.links][2]</span></span>|<span data-ttu-id="4b8e1-111">Azure 리소스는 서로 연결되어 논리적 관계를 형성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b8e1-111">Azure resources can be linked together to form logical relationships.</span></span> <span data-ttu-id="4b8e1-112">서로 다른 리소스 그룹에 속한 리소스 간의 연결을 설정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b8e1-112">You can establish links between resources belonging to different resource groups.</span></span>|
|<span data-ttu-id="4b8e1-113">[azure.mgmt.resource.locks][3]</span><span class="sxs-lookup"><span data-stu-id="4b8e1-113">[azure.mgmt.resource.locks][3]</span></span>|<span data-ttu-id="4b8e1-114">조직의 다른 사용자가 Azure 리소스를 삭제하거나 수정하지 못하도록 해당 리소스를 잠글 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b8e1-114">Azure resources can be locked to prevent other users in your organization from deleting or modifying resources.</span></span>|
|<span data-ttu-id="4b8e1-115">[azure.mgmt.resource.managedapplications][4]</span><span class="sxs-lookup"><span data-stu-id="4b8e1-115">[azure.mgmt.resource.managedapplications][4]</span></span>|<span data-ttu-id="4b8e1-116">ARM 관리형 애플리케이션(어플라이언스)입니다.</span><span class="sxs-lookup"><span data-stu-id="4b8e1-116">ARM managed applications (appliances).</span></span>|
|<span data-ttu-id="4b8e1-117">[azure.mgmt.resource.policy][5]</span><span class="sxs-lookup"><span data-stu-id="4b8e1-117">[azure.mgmt.resource.policy][5]</span></span>|<span data-ttu-id="4b8e1-118">리소스에 대한 액세스를 관리하고 제어하려면 사용자 지정 정책을 정의하고 범위에 할당할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b8e1-118">To manage and control access to your resources, you can define customized policies and assign them at a scope.</span></span>|
|<span data-ttu-id="4b8e1-119">[azure.mgmt.resource.resources][6]</span><span class="sxs-lookup"><span data-stu-id="4b8e1-119">[azure.mgmt.resource.resources][6]</span></span>| <span data-ttu-id="4b8e1-120">리소스 및 리소스 그룹을 사용하기 위한 작업을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="4b8e1-120">Provides operations for working with resources and resource groups.</span></span>|
|<span data-ttu-id="4b8e1-121">[azure.mgmt.resource.subscriptions][7]</span><span class="sxs-lookup"><span data-stu-id="4b8e1-121">[azure.mgmt.resource.subscriptions][7]</span></span>|<span data-ttu-id="4b8e1-122">모든 리소스 그룹 및 리소스는 구독 내에 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="4b8e1-122">All resource groups and resources exist within subscriptions.</span></span> <span data-ttu-id="4b8e1-123">이러한 작업을 통해 구독 및 테넌트에 대한 정보를 얻을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4b8e1-123">These operation enable you get information about your subscriptions and tenants.</span></span>|

[1]: /python/api/azure.mgmt.resource.features
[2]: /python/api/azure.mgmt.resource.links
[3]: /python/api/azure.mgmt.resource.locks
[4]: /python/api/azure.mgmt.resource.managedapplications
[5]: /python/api/azure.mgmt.resource.policy
[6]: /python/api/azure.mgmt.resource.resources
[7]: /python/api/azure.mgmt.resource.subscriptions

## <a name="install-the-libraries"></a><span data-ttu-id="4b8e1-124">라이브러리 설치</span><span class="sxs-lookup"><span data-stu-id="4b8e1-124">Install the libraries</span></span> 
```bash
pip install azure-mgmt-resource
```

## <a name="example"></a><span data-ttu-id="4b8e1-125">예</span><span class="sxs-lookup"><span data-stu-id="4b8e1-125">Example</span></span>
<span data-ttu-id="4b8e1-126">다음 예제에서는 리소스 그룹을 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="4b8e1-126">The following is an example of how to create a resource group.</span></span> 

```python
from azure.mgmt.resource import ResourceManagementClient
client = ResourceManagementClient(credentials, subscription_id)
client.resource_groups.create(RESOURCE_GROUP_NAME, {'location':'eastus'})
```

<span data-ttu-id="4b8e1-127">앱에서 사용할 수 있는 [Python 샘플 코드](https://azure.microsoft.com/resources/samples/?platform=python)를 추가로 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="4b8e1-127">Explore more [sample Python code](https://azure.microsoft.com/resources/samples/?platform=python) you can use in your apps.</span></span> 