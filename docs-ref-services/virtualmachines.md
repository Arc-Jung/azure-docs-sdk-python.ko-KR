---
title: Python용 Azure Virtual Machine 라이브러리
description: ''
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
ms.openlocfilehash: 78750d5f98ab81401c48493aff98d4268c01850d
ms.sourcegitcommit: 434186988284e0a8268a9de11645912a81226d6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/29/2019
ms.locfileid: "66376705"
---
# <a name="azure-virtual-machine-libraries"></a><span data-ttu-id="79788-103">Azure 가상 머신 라이브러리</span><span class="sxs-lookup"><span data-stu-id="79788-103">Azure virtual machine libraries</span></span>

## <a name="overview"></a><span data-ttu-id="79788-104">개요</span><span class="sxs-lookup"><span data-stu-id="79788-104">Overview</span></span>

<span data-ttu-id="79788-105">Linux 또는 Windows를 실행하는 요청 시 확장 가능한 컴퓨팅 리소스입니다.</span><span class="sxs-lookup"><span data-stu-id="79788-105">On-demand, scalable computing resources running Linux or Windows.</span></span>

<span data-ttu-id="79788-106">Azure Virtual Machines를 시작하려면 [Azure Portal을 사용하여 Linux 가상 머신 만들기](/azure/virtual-machines/linux/quick-create-portal)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="79788-106">To get started with Azure Virtual Machines, see [Create a Linux virtual machine with the Azure portal](/azure/virtual-machines/linux/quick-create-portal).</span></span>

## <a name="management-api"></a><span data-ttu-id="79788-107">관리 API</span><span class="sxs-lookup"><span data-stu-id="79788-107">Management API</span></span>

<span data-ttu-id="79788-108">관리 API를 사용하여 코드에서 Azure의 Windows 및 Linux 가상 머신을 생성, 구성, 관리 및 크기 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="79788-108">Create, configure, manage and scale Windows and Linux virtual machines in Azure from your code with the management API.</span></span>

<span data-ttu-id="79788-109">pip를 통해 라이브러리를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="79788-109">Install the library via pip.</span></span>

```bash
pip install azure-mgmt-compute
```

### <a name="example"></a><span data-ttu-id="79788-110">예</span><span class="sxs-lookup"><span data-stu-id="79788-110">Example</span></span>

<span data-ttu-id="79788-111">관리되는 서비스 ID(MSI) 인증을 사용하여 기존 Azure 리소스 그룹에 새 Linux 가상 컴퓨터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="79788-111">Create a new Linux virtual machine in an existing Azure resource group with Managed Service Identity(MSI) authentication.</span></span>

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
> [<span data-ttu-id="79788-112">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="79788-112">Explore the Management APIs</span></span>](/python/api/overview/azure/virtualmachines/management)

## <a name="samples"></a><span data-ttu-id="79788-113">샘플</span><span class="sxs-lookup"><span data-stu-id="79788-113">Samples</span></span>

* <span data-ttu-id="79788-114">[가상 머신 관리][1]</span><span class="sxs-lookup"><span data-stu-id="79788-114">[Manage virtual machines][1]</span></span>
* <span data-ttu-id="79788-115">[관리되는 서비스 ID를 사용하여 인증][2]</span><span class="sxs-lookup"><span data-stu-id="79788-115">[Authenticate with Managed Service Identity][2]</span></span>
* <span data-ttu-id="79788-116">[관리되는 서비스 ID 확장을 사용하여 가상 머신 만들기][3]</span><span class="sxs-lookup"><span data-stu-id="79788-116">[Create a virtual machine with Managed Service Identity Extension][3]</span></span>
* <span data-ttu-id="79788-117">[부하 분산 장치 관리(영문)][4]</span><span class="sxs-lookup"><span data-stu-id="79788-117">[Manage a load balancer][4]</span></span>
* <span data-ttu-id="79788-118">[관리 디스크 만들기 및 구성][5]</span><span class="sxs-lookup"><span data-stu-id="79788-118">[Create and configure managed disks][5]</span></span>
* <span data-ttu-id="79788-119">[이미지 나열][6]</span><span class="sxs-lookup"><span data-stu-id="79788-119">[List images][6]</span></span> 
* <span data-ttu-id="79788-120">[가상 머신 모니터링][7]</span><span class="sxs-lookup"><span data-stu-id="79788-120">[Monitor virtual machines][7]</span></span>

<span data-ttu-id="79788-121">가상 머신 샘플의 [전체 목록](https://azure.microsoft.com/resources/samples/?platform=python&term=virtual-machines)을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="79788-121">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=python&term=virtual-machines) of virtual machine samples.</span></span>

[1]: https://azure.microsoft.com/resources/samples/virtual-machines-python-manage/
[2]: https://github.com/Azure-Samples/resource-manager-python-manage-resources-with-msi
[3]: https://github.com/Azure-Samples/compute-python-msi-vm
[4]: https://azure.microsoft.com/resources/samples/network-python-manage-loadbalancer
[5]: ../docs-ref-conceptual/python-sdk-azure-samples-managed-disks.md
[6]: ../docs-ref-conceptual/python-sdk-azure-samples-list-images.md
[7]: ../docs-ref-conceptual/python-sdk-azure-samples-monitor-vms.md
