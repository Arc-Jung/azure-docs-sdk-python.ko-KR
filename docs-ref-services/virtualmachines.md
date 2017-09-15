---
title: "Python용 Azure Virtual Machine 라이브러리"
description: 
keywords: Azure, Python, SDK, API, Compute, Virtual Machines
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/09/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: compute
ms.openlocfilehash: e2f2ad4e42bd847c9286333bacd583c3cd3f1b8c
ms.sourcegitcommit: 79afc8a1b427e26ecea7bdc0b7b3c898f143360f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2017
---
# <a name="azure-virtual-machine-libraries"></a>Azure 가상 컴퓨터 라이브러리

## <a name="overview"></a>개요

Linux 또는 Windows를 실행하는 요청 시 확장 가능한 컴퓨팅 리소스입니다.

Azure Virtual Machines를 시작하려면 [Azure Portal을 사용하여 Linux 가상 컴퓨터 만들기](/azure/virtual-machines/linux/quick-create-portal)를 참조하세요.

## <a name="management-api"></a>관리 API

관리 API를 사용하여 코드에서 Azure의 Windows 및 Linux 가상 컴퓨터를 생성, 구성, 관리 및 크기 조정할 수 있습니다.

pip를 통해 라이브러리를 설치합니다.

```bash
pip install azure-mgmt-compute 
```   

### <a name="example"></a>예제

관리되는 서비스 ID(MSI) 인증을 사용하여 기존 Azure 리소스 그룹에 새 Linux 가상 컴퓨터를 만듭니다.

```python
VM_PARAMETERS={
        'location': 'LOCATION',
        'os_profile': {
            'computer_name': 'VM_NAME',
            'admin_username': 'USERNAME',
            'admin_password': 'PASSWORD'
        },
        'hardware_profile': {
            'vm_size': 'Standard_DS1_v2'
        },
        'storage_profile': {
            'image_reference': {
                'publisher': 'Canonical',
                'offer': 'UbuntuServer',
                'sku': '16.04.0-LTS',
                'version': 'latest'
            },
        },
        'network_profile': {
            'network_interfaces': [{
                'id': 'NIC_ID',
            }]
        },
    }

def create_vm()
    compute_client.virtual_machines.create_or_update(
        'RESOURCE_GROUP_NAME', 'VM_NAME', VM_PARAMETERS)
```

> [!div class="nextstepaction"]
> [관리 API 탐색](/python/api/overview/azure/virtualmachines/managementlibrary)

## <a name="samples"></a>샘플

* [가상 컴퓨터 관리][1]
* [관리되는 서비스 ID를 사용하여 인증][2]
* [부하 분산 장치 관리(영문)][3]
* [관리 디스크 만들기 및 구성][4]
* [이미지 나열][5] 
* [가상 컴퓨터 모니터링][6]

가상 컴퓨터 샘플의 [전체 목록](https://azure.microsoft.com/resources/samples/?platform=python&term=virtual-machines)을 봅니다.

[1]: https://azure.microsoft.com/resources/samples/virtual-machines-python-manage/
[2]: https://github.com/Azure-Samples/resource-manager-python-manage-resources-with-msi
[3]: https://azure.microsoft.com/resources/samples/network-python-manage-loadbalancer
[4]: ../docs-ref-conceptual/python-sdk-azure-samples-managed-disks.md
[5]: ../docs-ref-conceptual/python-sdk-azure-samples-list-images.md
[6]: ../docs-ref-conceptual/python-sdk-azure-samples-monitor-vms.md