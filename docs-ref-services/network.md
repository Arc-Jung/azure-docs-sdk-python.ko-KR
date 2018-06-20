---
title: Python용 Azure Network 라이브러리
description: Python용 Azure Network 라이브러리에 대한 참조
keywords: Azure, Python, SDK, API, Network
author: sptramer
ms.author: sttramer
manager: douge
ms.date: 07/10/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 47252ca3b2f5c6087277bac3735025f0dbabbdd8
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/23/2018
ms.locfileid: "29479076"
---
# <a name="azure-network-libraries-for-python"></a><span data-ttu-id="e002f-104">Python용 Azure Network 라이브러리</span><span class="sxs-lookup"><span data-stu-id="e002f-104">Azure Network libraries for python</span></span>

## <a name="overview"></a><span data-ttu-id="e002f-105">개요</span><span class="sxs-lookup"><span data-stu-id="e002f-105">Overview</span></span>

<span data-ttu-id="e002f-106">[Azure Virtual Network](/azure/virtual-network/virtual-networks-overview)를 사용하면 Azure 리소스를 연결하고, 온-프레미스 네트워크에도 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e002f-106">[Azure Virtual Network](/azure/virtual-network/virtual-networks-overview) allows you to connect Azure resources, and also connect them to your on-premises network.</span></span>

<span data-ttu-id="e002f-107">Azure Virtual Network를 시작하려면 [첫 번째 가상 네트워크 만들기](/azure/virtual-network/virtual-network-get-started-vnet-subnet)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e002f-107">To get started with Azure Virtual Network, see [Create your first virtual network](/azure/virtual-network/virtual-network-get-started-vnet-subnet).</span></span>

## <a name="management-apis"></a><span data-ttu-id="e002f-108">관리 API</span><span class="sxs-lookup"><span data-stu-id="e002f-108">Management APIs</span></span>

<span data-ttu-id="e002f-109">관리 API를 사용하여 Azure 가상 네트워크를 검사, 관리 및 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="e002f-109">Inspect, manage, and configure Azure virtual networks with the management APIs.</span></span>

<span data-ttu-id="e002f-110">다른 Azure Python API와 달리 네트워킹 API는 명시적으로 별도의 패키지로 버전 관리됩니다.</span><span class="sxs-lookup"><span data-stu-id="e002f-110">Unlike other Azure python APIs, the networking APIs are explicitly versioned into separage packages.</span></span> <span data-ttu-id="e002f-111">패키지 정보가 클라이언트 생성자에 지정되어 있으므로 개별적으로 가져올 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="e002f-111">You do not need to import them individually since the package information is specified in the client constructor.</span></span>

<span data-ttu-id="e002f-112">pip를 사용하여 관리 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="e002f-112">Install the management package with pip.</span></span>

```bash
pip install azure-mgmt-network
```

### <a name="example"></a><span data-ttu-id="e002f-113">예</span><span class="sxs-lookup"><span data-stu-id="e002f-113">Example</span></span>

<span data-ttu-id="e002f-114">가상 네트워크 및 관련 서브넷을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e002f-114">Create a virtual network and an associated subnet.</span></span>

```python
from azure.mgmt.network import NetworkManagementClient

GROUP_NAME = 'resource-group'
VNET_NAME = 'your-vnet-identifier'
LOCATION = 'region'
SUBNET_NAME = 'your-subnet-identifier'

network_client = NetworkManagementClient(credentials, 'your-subscription-id')

async_vnet_creation = network_client.virtual_networks.create_or_update(
    GROUP_NAME,
    VNET_NAME,
    {
        'location': LOCATION,
        'address_space': {
            'address_prefixes': ['10.0.0.0/16']
        }
    }
)
async_vnet_creation.wait()

# Create Subnet
async_subnet_creation = network_client.subnets.create_or_update(
    GROUP_NAME,
    VNET_NAME,
    SUBNET_NAME,
    {'address_prefix': '10.0.0.0/24'}
)
subnet_info = async_subnet_creation.result()
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="e002f-115">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="e002f-115">Explore the Management APIs</span></span>](/python/api/overview/azure/network/management)

### <a name="samples"></a><span data-ttu-id="e002f-116">샘플</span><span class="sxs-lookup"><span data-stu-id="e002f-116">Samples</span></span>

* [<span data-ttu-id="e002f-117">Python에서부하 분산 장치에 대한 Azure Resource Manager 시작</span><span class="sxs-lookup"><span data-stu-id="e002f-117">Getting started with Azure Resource Manager for load balancers in Python</span></span>](https://azure.microsoft.com/en-us/resources/samples/network-python-manage-loadbalancer/)

<span data-ttu-id="e002f-118">Azure Virtual Network 샘플의 [전체 목록](https://azure.microsoft.com/en-us/resources/samples/?platform=python&term=virtual%20network)을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="e002f-118">View the [complete list](https://azure.microsoft.com/en-us/resources/samples/?platform=python&term=virtual%20network) of Azure Virtual Network samples.</span></span>
