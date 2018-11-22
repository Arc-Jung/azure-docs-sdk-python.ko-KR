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
ms.openlocfilehash: f468f844becc2f0fe07d892c725c00df4669f4e3
ms.sourcegitcommit: f439ba940d5940359c982015db7ccfb82f9dffd9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2018
ms.locfileid: "52273029"
---
# <a name="azure-network-libraries-for-python"></a>Python용 Azure Network 라이브러리

## <a name="overview"></a>개요

[Azure Virtual Network](/azure/virtual-network/virtual-networks-overview)를 사용하면 Azure 리소스를 연결하고, 온-프레미스 네트워크에도 연결할 수 있습니다.

Azure Virtual Network를 시작하려면 [첫 번째 가상 네트워크 만들기](/azure/virtual-network/virtual-network-get-started-vnet-subnet)를 참조하세요.

## <a name="management-apis"></a>관리 API

관리 API를 사용하여 Azure 가상 네트워크를 검사, 관리 및 구성합니다.

다른 Azure Python API와 달리 네트워킹 API는 명시적으로 별도의 패키지로 버전 관리됩니다. 패키지 정보가 클라이언트 생성자에 지정되어 있으므로 개별적으로 가져올 필요가 없습니다.

pip를 사용하여 관리 패키지를 설치합니다.

```bash
pip install azure-mgmt-network
```

### <a name="example"></a>예

가상 네트워크 및 관련 서브넷을 만듭니다.

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
> [관리 API 탐색](/python/api/overview/azure/network/management)

### <a name="samples"></a>샘플

* [Python에서부하 분산 장치에 대한 Azure Resource Manager 시작](https://azure.microsoft.com/en-us/resources/samples/network-python-manage-loadbalancer/)

Azure Virtual Network 샘플의 [전체 목록](https://azure.microsoft.com/en-us/resources/samples/?platform=python&term=virtual%20network)을 봅니다.
