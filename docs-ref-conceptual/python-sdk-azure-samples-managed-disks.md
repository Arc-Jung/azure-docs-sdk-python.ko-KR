---
title: Managed Disks
description: 관리 디스크를 생성, 크기 조정 및 업데이트합니다.
author: lisawong19
manager: douge
ms.assetid: ''
ms.devlang: python
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 6/15/2017
ms.author: liwong
ms.openlocfilehash: 733bd0ffce6ddb10219dae40bad6ea54e1efcd70
ms.sourcegitcommit: 560362db0f65307c8b02b7b7ad8642b5c4aa6294
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/07/2018
---
# <a name="managed-disks"></a><span data-ttu-id="6c28e-103">Managed Disks</span><span class="sxs-lookup"><span data-stu-id="6c28e-103">Managed Disks</span></span>

<span data-ttu-id="6c28e-104">이제 하나의 확장 집합에서 Azure Managed Disks 및 1,000개 VM을 [일반적으로 사용](https://azure.microsoft.com/en-us/blog/announcing-general-availability-of-managed-disks-and-larger-scale-sets/)할 수 있습니다. Azure Managed Disks는 간소화된 디스크 관리, 향상된 확장성, 더 효율적인 보안 및 크기 조정 기능을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6c28e-104">Azure Managed Disks and 1000 VMs in a Scale Set are now [generally available](https://azure.microsoft.com/en-us/blog/announcing-general-availability-of-managed-disks-and-larger-scale-sets/) Azure Managed Disks provide a simplified disk Management, enhanced Scalability, better Security and Scale.</span></span> <span data-ttu-id="6c28e-105">디스크에 대한 저장소 계정의 개념을 없앰으로써 고객이 저장소 계정과 관련된 제한을 걱정하지 않고 크기 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c28e-105">It takes away the notion of storage account for disks, enabling customers to scale without worrying about the limitations associated with storage accounts.</span></span> <span data-ttu-id="6c28e-106">이 게시물에서는 Python에서 서비스를 사용하는 방법에 대한 간단한 소개와 참조를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="6c28e-106">This post provides a quick introduction and reference on consuming the service from Python.</span></span>



<span data-ttu-id="6c28e-107">개발자 관점에서 Azure CLI의 Managed Disks 환경은 다른 플랫폼 간 도구의 CLI 환경에 관용적입니다.</span><span class="sxs-lookup"><span data-stu-id="6c28e-107">From a developer perspective, the Managed Disks experience in Azure CLI is idomatic to the CLI experience in other cross-platform tools.</span></span> <span data-ttu-id="6c28e-108">[Azure Python](https://azure.microsoft.com/develop/python/) SDK와 [azure-mgmt-compute 패키지 0.33.0](https://pypi.python.org/pypi/azure-mgmt-compute)을 사용하여 Managed Disks를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c28e-108">You can use the [Azure Python](https://azure.microsoft.com/develop/python/) SDK and the [azure-mgmt-compute package 0.33.0](https://pypi.python.org/pypi/azure-mgmt-compute) to administer Managed Disks.</span></span> <span data-ttu-id="6c28e-109">이 [자습서](https://docs.microsoft.com/python/api/overview/azure/virtualmachines?view=azure-python)를 사용하여 계산 클라이언트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c28e-109">You can create a compute client using this [tutorial](https://docs.microsoft.com/python/api/overview/azure/virtualmachines?view=azure-python).</span></span>


## <a name="standalone-managed-disks"></a><span data-ttu-id="6c28e-110">독립 실행형 Managed Disks</span><span class="sxs-lookup"><span data-stu-id="6c28e-110">Standalone Managed Disks</span></span>

<span data-ttu-id="6c28e-111">독립 실행형 Managed Disks는 다양한 방법으로 쉽게 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c28e-111">You can easily create standalone Managed Disks in a variety of ways.</span></span>

### <a name="create-an-empty-managed-disk"></a><span data-ttu-id="6c28e-112">빈 관리 디스크 만들기</span><span class="sxs-lookup"><span data-stu-id="6c28e-112">Create an empty Managed Disk.</span></span>
```python
from azure.mgmt.compute.models import DiskCreateOption

async_creation = compute_client.disks.create_or_update(
    'my_resource_group',
    'my_disk_name',
    {
        'location': 'eastus',
        'disk_size_gb': 20,
        'creation_data': {
            'create_option': DiskCreateOption.empty
        }
    }
)
disk_resource = async_creation.result()
```

### <a name="create-a-managed-disk-from-blob-storage"></a><span data-ttu-id="6c28e-113">Blob Storage에서 관리 디스크 만들기</span><span class="sxs-lookup"><span data-stu-id="6c28e-113">Create a Managed Disk from Blob Storage.</span></span>
```python
from azure.mgmt.compute.models import DiskCreateOption

async_creation = compute_client.disks.create_or_update(
    'my_resource_group',
    'my_disk_name',
    {
        'location': 'eastus',
        'creation_data': {
            'create_option': DiskCreateOption.import_enum,
            'source_uri': 'https://bg09.blob.core.windows.net/vm-images/non-existent.vhd'
        }
    }
)
disk_resource = async_creation.result()
```

### <a name="create-a-managed-disk-from-your-own-image"></a><span data-ttu-id="6c28e-114">사용자 고유의 이미지에서 관리 디스크 만들기</span><span class="sxs-lookup"><span data-stu-id="6c28e-114">Create a Managed Disk from your own Image</span></span>
```python
from azure.mgmt.compute.models import DiskCreateOption

# If you don't know the id, do a 'get' like this to obtain it
managed_disk = compute_client.disks.get(self.group_name, 'myImageDisk')
async_creation = compute_client.disks.create_or_update(
    'my_resource_group',
    'my_disk_name',
    {
        'location': 'eastus',
        'creation_data': {
            'create_option': DiskCreateOption.copy,
            'source_resource_id': managed_disk.id
        }
    }
)

disk_resource = async_creation.result()
```

## <a name="virtual-machine-with-managed-disks"></a><span data-ttu-id="6c28e-115">Managed Disks가 있는 Virtual Machine</span><span class="sxs-lookup"><span data-stu-id="6c28e-115">Virtual Machine with Managed Disks</span></span>

<span data-ttu-id="6c28e-116">특정 디스크 이미지에 대한 암시적 관리 디스크가 있는 Virtual Machine을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c28e-116">You can create a Virtual Machine with an implicit Managed Disk for a specific disk image.</span></span> <span data-ttu-id="6c28e-117">간단히 만들려면 모든 디스크 세부 정보를 지정하지 않고 관리 디스크를 암시적으로 만들면 됩니다.</span><span class="sxs-lookup"><span data-stu-id="6c28e-117">Creation is simplified with implicit creation of managed disks without specifying all the disk details.</span></span> <span data-ttu-id="6c28e-118">이 경우 저장소 계정을 만들고 관리하는 것에 대해 걱정할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6c28e-118">You do not have to worry about creating and managing Storage Accounts.</span></span>

<span data-ttu-id="6c28e-119">관리 디스크는 Azure의 OS 이미지에서 VM을 만들 때 암시적으로 만들어집니다.</span><span class="sxs-lookup"><span data-stu-id="6c28e-119">A Managed Disk is created implicitly when creating VM from an OS image in Azure.</span></span> <span data-ttu-id="6c28e-120">``storage_profile`` 매개 변수에서 ``os_disk``는 이제 선택적 요소이며 Virtual Machine을 만드는 데 필요한 전제 조건으로 저장소 계정을 만들 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6c28e-120">In the ``storage_profile`` parameter, ``os_disk`` is now optional and you don't have to create a storage account as required precondition to create a Virtual Machine.</span></span>

```python
storage_profile = azure.mgmt.compute.models.StorageProfile(
    image_reference = azure.mgmt.compute.models.ImageReference(
        publisher='Canonical',
        offer='UbuntuServer',
        sku='16.04-LTS',
        version='latest'
    )
)
``` 
<span data-ttu-id="6c28e-121">이 ``storage_profile`` 매개 변수는 이제 유효합니다.</span><span class="sxs-lookup"><span data-stu-id="6c28e-121">This ``storage_profile`` parameter is now valid.</span></span> <span data-ttu-id="6c28e-122">Python(네트워크 등 포함)에서 VM을 만드는 방법에 대한 완전한 예제를 얻으려면 [Python의 VM 자습서](https://github.com/Azure-Samples/virtual-machines-python-manage) 전체를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="6c28e-122">To get a complete example on how to create a VM in Python (including network, etc), check the full [VM tutorial in Python](https://github.com/Azure-Samples/virtual-machines-python-manage).</span></span>

<span data-ttu-id="6c28e-123">이전에 프로비전된 관리 디스크를 쉽게 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c28e-123">You can easily attach a previously provisioned Managed Disk.</span></span>
```python
vm = compute.virtual_machines.get(
    'my_resource_group',
    'my_vm'
)
managed_disk = compute_client.disks.get('my_resource_group', 'myDisk')
vm.storage_profile.data_disks.append({
    'lun': 12, # You choose the value, depending of what is available for you
    'name': managed_disk.name,
    'create_option': DiskCreateOptionTypes.attach,
    'managed_disk': {
        'id': managed_disk.id
    }
})
async_update = compute_client.virtual_machines.create_or_update(
    'my_resource_group',
    vm.name,
    vm,
)
async_update.wait()
```

## <a name="virtual-machine-scale-sets-with-managed-disks"></a><span data-ttu-id="6c28e-124">Managed Disks를 포함하는 Virtual Machine Scale Sets</span><span class="sxs-lookup"><span data-stu-id="6c28e-124">Virtual Machine Scale Sets with Managed Disks</span></span>

<span data-ttu-id="6c28e-125">Managed Disks 이전에는 필요한 모든 VM에 대한 저장소 계정을 확장 집합 내에서 수동으로 만든 다음 ``vhd_containers`` list 매개 변수를 사용하여 모든 저장소 계정 이름을 확장 집합 Rest API에 제공해야 했습니다.</span><span class="sxs-lookup"><span data-stu-id="6c28e-125">Before Managed Disks, you needed to create a storage account manually for all the VMs you wanted inside your Scale Set, and then use the list parameter ``vhd_containers`` to provide all the storage account name to the Scale Set RestAPI.</span></span> <span data-ttu-id="6c28e-126">공식적인 전환 가이드는 이 문서의 내용 `<https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-convert-template-to-md>`에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c28e-126">The official transition guide is available in this article `<https://docs.microsoft.com/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-convert-template-to-md>`.</span></span>

<span data-ttu-id="6c28e-127">이제 관리 디스크를 사용하면 저장소 계정을 전혀 관리할 필요가 없습니다.</span><span class="sxs-lookup"><span data-stu-id="6c28e-127">Now with Managed Disk, you don't have to manage any storage account at all.</span></span> <span data-ttu-id="6c28e-128">VMSS Python SDK에 익숙하다면 ``storage_profile``은 이제 VM을 만드는 데 사용된 매개 변수와 똑같을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="6c28e-128">If you're are used to the VMSS Python SDK, your ``storage_profile`` can now be exactly the same as the one used in VM creation:</span></span>

```python
'storage_profile': {
    'image_reference': {
        "publisher": "Canonical",
        "offer": "UbuntuServer",
        "sku": "16.04-LTS",
        "version": "latest"
    }
},
```

<span data-ttu-id="6c28e-129">전체 샘플은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="6c28e-129">The full sample being:</span></span>

```python
naming_infix = "PyTestInfix"
vmss_parameters = {
    'location': self.region,
    "overprovision": True,
    "upgrade_policy": {
        "mode": "Manual"
    },
    'sku': {
        'name': 'Standard_A1',
        'tier': 'Standard',
        'capacity': 5
    },
    'virtual_machine_profile': {
        'storage_profile': {
            'image_reference': {
                "publisher": "Canonical",
                "offer": "UbuntuServer",
                "sku": "16.04-LTS",
                "version": "latest"
            }
        },
        'os_profile': {
            'computer_name_prefix': naming_infix,
            'admin_username': 'Foo12',
            'admin_password': 'BaR@123!!!!',
        },
        'network_profile': {
            'network_interface_configurations' : [{
                'name': naming_infix + 'nic',
                "primary": True,
                'ip_configurations': [{
                    'name': naming_infix + 'ipconfig',
                    'subnet': {
                        'id': subnet.id
                    } 
                }]
            }]
        }
    }
}

# Create VMSS test
result_create = compute_client.virtual_machine_scale_sets.create_or_update(
    'my_resource_group',
    'my_scale_set',
    vmss_parameters,
)
vmss_result = result_create.result()
``` 

## <a name="other-operations-with-managed-disks"></a><span data-ttu-id="6c28e-130">기타 Managed Disks 작업</span><span class="sxs-lookup"><span data-stu-id="6c28e-130">Other Operations with Managed Disks</span></span>

### <a name="resizing-a-managed-disk"></a><span data-ttu-id="6c28e-131">관리 디스크 크기 조정</span><span class="sxs-lookup"><span data-stu-id="6c28e-131">Resizing a managed disk.</span></span>

```python
managed_disk = compute_client.disks.get('my_resource_group', 'myDisk')
managed_disk.disk_size_gb = 25
async_update = self.compute_client.disks.create_or_update(
    'my_resource_group',
    'myDisk',
    managed_disk
)
async_update.wait()
```

### <a name="update-the-storage-account-type-of-the-managed-disks"></a><span data-ttu-id="6c28e-132">Managed Disks의 저장소 계정 유형 업데이트</span><span class="sxs-lookup"><span data-stu-id="6c28e-132">Update the Storage Account type of the Managed Disks.</span></span>
```python
from azure.mgmt.compute.models import StorageAccountTypes

managed_disk = compute_client.disks.get('my_resource_group', 'myDisk')
managed_disk.account_type = StorageAccountTypes.standard_lrs
async_update = self.compute_client.disks.create_or_update(
    'my_resource_group',
    'myDisk',
    managed_disk
)
async_update.wait()
```

### <a name="create-an-image-from-blob-storage"></a><span data-ttu-id="6c28e-133">Blob 저장소에서 이미지 만들기</span><span class="sxs-lookup"><span data-stu-id="6c28e-133">Create an image from Blob Storage.</span></span>
```python
async_create_image = compute_client.images.create_or_update(
    'my_resource_group',
    'myImage',
    {
        'location': 'westus',
        'storage_profile': {
            'os_disk': {
                'os_type': 'Linux',
                'os_state': "Generalized",
                'blob_uri': 'https://bg09.blob.core.windows.net/vm-images/non-existent.vhd',
                'caching': "ReadWrite",
            }
        }
    }
)
image = async_create_image.result()
```

### <a name="create-a-snapshot-of-a-managed-disk-that-is-currently-attached-to-a-virtual-machine"></a><span data-ttu-id="6c28e-134">현재 Virtual Machine에 연결된 관리 디스크의 스냅숏 만들기</span><span class="sxs-lookup"><span data-stu-id="6c28e-134">Create a snapshot of a Managed Disk that is currently attached to a Virtual Machine.</span></span>
```python
managed_disk = compute_client.disks.get('my_resource_group', 'myDisk')
async_snapshot_creation = self.compute_client.snapshots.create_or_update(
        'my_resource_group',
        'mySnapshot',
        {
            'location': 'westus',
            'creation_data': {
                'create_option': 'Copy',
                'source_uri': managed_disk.id
            }
        }
    )
snapshot = async_snapshot_creation.result()
```
