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
# <a name="azure-virtual-machine-libraries"></a><span data-ttu-id="7639a-103">Azure 가상 컴퓨터 라이브러리</span><span class="sxs-lookup"><span data-stu-id="7639a-103">Azure virtual machine libraries</span></span>

## <a name="overview"></a><span data-ttu-id="7639a-104">개요</span><span class="sxs-lookup"><span data-stu-id="7639a-104">Overview</span></span>

<span data-ttu-id="7639a-105">Linux 또는 Windows를 실행하는 요청 시 확장 가능한 컴퓨팅 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="7639a-105">On-demand, scalable computing resources running Linux or Windows.</span></span>

<span data-ttu-id="7639a-106">Azure Virtual Machines를 시작하려면 [Azure Portal을 사용하여 Linux 가상 컴퓨터 만들기](/azure/virtual-machines/linux/quick-create-portal)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="7639a-106">To get started with Azure Virtual Machines, see [Create a Linux virtual machine with the Azure portal](/azure/virtual-machines/linux/quick-create-portal).</span></span>

## <a name="management-api"></a><span data-ttu-id="7639a-107">관리 API</span><span class="sxs-lookup"><span data-stu-id="7639a-107">Management API</span></span>

<span data-ttu-id="7639a-108">관리 API를 사용하여 코드에서 Azure의 Windows 및 Linux 가상 컴퓨터를 생성, 구성, 관리 및 크기 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7639a-108">Create, configure, manage and scale Windows and Linux virtual machines in Azure from your code with the management API.</span></span>

<span data-ttu-id="7639a-109">pip를 통해 라이브러리를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="7639a-109">Install the library via pip.</span></span>

```bash
pip install azure-mgmt-compute 
```   

### <a name="example"></a><span data-ttu-id="7639a-110">예제</span><span class="sxs-lookup"><span data-stu-id="7639a-110">Example</span></span>

<span data-ttu-id="7639a-111">관리되는 서비스 ID(MSI) 인증을 사용하여 기존 Azure 리소스 그룹에 새 Linux 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7639a-111">Create a new Linux virtual machine in an existing Azure resource group with Managed Service Identity(MSI) authentication.</span></span>

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
> [<span data-ttu-id="7639a-112">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="7639a-112">Explore the Management APIs</span></span>](/python/api/overview/azure/virtualmachines/managementlibrary)

## <a name="samples"></a><span data-ttu-id="7639a-113">샘플</span><span class="sxs-lookup"><span data-stu-id="7639a-113">Samples</span></span>

* <span data-ttu-id="7639a-114">[가상 컴퓨터 관리][1]</span><span class="sxs-lookup"><span data-stu-id="7639a-114">[Manage virtual machines][1]</span></span>
* <span data-ttu-id="7639a-115">[관리되는 서비스 ID를 사용하여 인증][2]</span><span class="sxs-lookup"><span data-stu-id="7639a-115">[Authenticate with Managed Service Identity][2]</span></span>
* <span data-ttu-id="7639a-116">[부하 분산 장치 관리(영문)][3]</span><span class="sxs-lookup"><span data-stu-id="7639a-116">[Manage a load balancer][3]</span></span>
* <span data-ttu-id="7639a-117">[관리 디스크 만들기 및 구성][4]</span><span class="sxs-lookup"><span data-stu-id="7639a-117">[Create and configure managed disks][4]</span></span>
* <span data-ttu-id="7639a-118">[이미지 나열][5]</span><span class="sxs-lookup"><span data-stu-id="7639a-118">[List images][5]</span></span> 
* <span data-ttu-id="7639a-119">[가상 컴퓨터 모니터링][6]</span><span class="sxs-lookup"><span data-stu-id="7639a-119">[Monitor virtual machines][6]</span></span>

<span data-ttu-id="7639a-120">가상 컴퓨터 샘플의 [전체 목록](https://azure.microsoft.com/resources/samples/?platform=python&term=virtual-machines)을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="7639a-120">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=python&term=virtual-machines) of virtual machine samples.</span></span>

[1]: https://azure.microsoft.com/resources/samples/virtual-machines-python-manage/
[2]: https://github.com/Azure-Samples/resource-manager-python-manage-resources-with-msi
[3]: https://azure.microsoft.com/resources/samples/network-python-manage-loadbalancer
[4]: ../docs-ref-conceptual/python-sdk-azure-samples-managed-disks.md
[5]: ../docs-ref-conceptual/python-sdk-azure-samples-list-images.md
[6]: ../docs-ref-conceptual/python-sdk-azure-samples-monitor-vms.md