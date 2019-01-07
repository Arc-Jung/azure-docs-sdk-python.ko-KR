---
title: Azure HDInsight Python SDK 미리 보기
description: Azure HDInsight Python SDK 참조 HDInsight Python SDK는 HDInsight 클러스터 관리를 위한 클래스 및 메서드를 제공합니다.
ms.service: hdinsight
author: tylerfox
ms.author: tyfox
ms.date: 09/18/2018
ms.topic: reference
ms.devlang: python
ms.openlocfilehash: 9447d50fd734bd9221accbf470a456210bb57a7f
ms.sourcegitcommit: e2e4b1ecfac9804a72973477634128061c1ec990
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/17/2018
ms.locfileid: "53455110"
---
# <a name="hdinsight-python-management-sdk-preview"></a><span data-ttu-id="c79c1-104">HDInsight Python 관리 SDK 미리 보기</span><span class="sxs-lookup"><span data-stu-id="c79c1-104">HDInsight Python Management SDK Preview</span></span>

## <a name="overview"></a><span data-ttu-id="c79c1-105">개요</span><span class="sxs-lookup"><span data-stu-id="c79c1-105">Overview</span></span>

<span data-ttu-id="c79c1-106">HDInsight Python SDK는 HDInsight 클러스터 관리를 위한 클래스 및 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-106">The HDInsight Python SDK provides classes and methods that allow you to manage your HDInsight clusters.</span></span> <span data-ttu-id="c79c1-107">여기에는 HDInsight 클러스터의 속성 만들기, 삭제, 업데이트, 나열, 크기 조정, 스크립트 작업 실행, 모니터링, 가져오기 작업을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-107">It includes operations to create, delete, update, list, resize, execute script actions, monitor, get properties of HDInsight clusters, and more.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c79c1-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="c79c1-108">Prerequisites</span></span>

* <span data-ttu-id="c79c1-109">Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="c79c1-109">An Azure account.</span></span> <span data-ttu-id="c79c1-110">계정이 없으면 [체험 계정을 얻습니다](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="c79c1-110">If you don't have one, [get a free trial](https://azure.microsoft.com/free/).</span></span>
* [<span data-ttu-id="c79c1-111">Python</span><span class="sxs-lookup"><span data-stu-id="c79c1-111">Python</span></span>](https://www.python.org/downloads/)
* [<span data-ttu-id="c79c1-112">pip</span><span class="sxs-lookup"><span data-stu-id="c79c1-112">pip</span></span>](https://pypi.org/project/pip/#description)

## <a name="sdk-installation"></a><span data-ttu-id="c79c1-113">SDK 설치</span><span class="sxs-lookup"><span data-stu-id="c79c1-113">SDK Installation</span></span>

<span data-ttu-id="c79c1-114">HDInsight Python SDK는 [Python 패키지 인덱스](https://pypi.org/project/azure-mgmt-hdinsight/)에 있으며 다음을 실행하여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-114">The HDInsight Python SDK can be found in the [Python Package Index](https://pypi.org/project/azure-mgmt-hdinsight/) and can be installed by running:</span></span> 

`pip install azure-mgmt-hdinsight`

## <a name="authentication"></a><span data-ttu-id="c79c1-115">인증</span><span class="sxs-lookup"><span data-stu-id="c79c1-115">Authentication</span></span>

<span data-ttu-id="c79c1-116">Azure 구독을 사용해서 SDK를 먼저 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-116">The SDK first needs to be authenticated with your Azure subscription.</span></span>  <span data-ttu-id="c79c1-117">아래 예제에 따라 서비스 주체를 만들고 이를 인증에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-117">Follow the example below to create a service principal and use it to authenticate.</span></span> <span data-ttu-id="c79c1-118">완료되었으면 관리 작업 수행을 위해 사용할 수 있는 여러 메서드(아래 섹션 참조)가 포함된 `HDInsightManagementClient` 인스턴스가 준비됩니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-118">After this is done, you will have an instance of an `HDInsightManagementClient`, which contains many methods (outlined in below sections) that can be used to perform management operations.</span></span>

> [!NOTE]
> <span data-ttu-id="c79c1-119">아래 설명된 예제 외에도 사용자 요구에 더 적합할 수 있는 다른 인증 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-119">There are other ways to authenticate besides the below example that could potentially be better suited for your needs.</span></span> <span data-ttu-id="c79c1-120">모든 메서드는 여기에 설명되어 있습니다. [Python용 Azure 관리 라이브러리를 사용하여 인증](https://docs.microsoft.com/en-us/python/azure/python-sdk-azure-authenticate?view=azure-python)</span><span class="sxs-lookup"><span data-stu-id="c79c1-120">All methods are outlined here: [Authenticate with the Azure Management Libraries for Python](https://docs.microsoft.com/en-us/python/azure/python-sdk-azure-authenticate?view=azure-python)</span></span>

### <a name="authentication-example-using-a-service-principal"></a><span data-ttu-id="c79c1-121">서비스 주체를 사용한 인증 예제</span><span class="sxs-lookup"><span data-stu-id="c79c1-121">Authentication Example Using a Service Principal</span></span>

<span data-ttu-id="c79c1-122">먼저, [Azure Cloud Shell](https://shell.azure.com/bash)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-122">First, login to [Azure Cloud Shell](https://shell.azure.com/bash).</span></span> <span data-ttu-id="c79c1-123">서비스 주체를 만들려는 구독을 현재 사용하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-123">Verify you are currently using the subscription in which you want the service principal created.</span></span> 

```azurecli-interactive
az account show
```

<span data-ttu-id="c79c1-124">구독 정보는 JSON으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-124">Your subscription information is displayed as JSON.</span></span>

```json
{
  "environmentName": "AzureCloud",
  "id": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "isDefault": true,
  "name": "XXXXXXX",
  "state": "Enabled",
  "tenantId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "user": {
    "cloudShellID": true,
    "name": "XXX@XXX.XXX",
    "type": "user"
  }
}
```

<span data-ttu-id="c79c1-125">올바른 구독으로 로그인되지 않은 경우 다음을 실행하여 올바른 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-125">If you're not logged into the correct subscription, select the correct one by running:</span></span> 
```azurecli-interactive
az account set -s <name or ID of subscription>
```

> [!IMPORTANT]
> <span data-ttu-id="c79c1-126">Azure Portal을 통해 HDInsight Cluster를 만드는 등 다른 방법을 사용해서 HDInsight Resource Provider를 등록하지 않은 경우, 이를 먼저 수행해야 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-126">If you have not already registered the HDInsight Resource Provider by another method (such as by creating an HDInsight Cluster through the Azure Portal), you need to do this once before you can authenticate.</span></span> <span data-ttu-id="c79c1-127">이 작업은 [Azure Cloud Shell](https://shell.azure.com/bash)에서 다음 명령을 실행하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-127">This can be done from the [Azure Cloud Shell](https://shell.azure.com/bash) by running the following command:</span></span>
>```azurecli-interactive
>az provider register --namespace Microsoft.HDInsight
>```

<span data-ttu-id="c79c1-128">그런 다음 서비스 주체 이름을 선택하고 다음 명령을 사용해서 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-128">Next, choose a name for your service principal and create it with the following command:</span></span>

```azurecli-interactive
az ad sp create-for-rbac --name <Service Principal Name> --sdk-auth
```

<span data-ttu-id="c79c1-129">서비스 주체 정보는 JSON으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-129">The service principal information is displayed as JSON.</span></span>

```json
{
  "clientId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "clientSecret": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "subscriptionId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "tenantId": "XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX",
  "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
  "resourceManagerEndpointUrl": "https://management.azure.com/",
  "activeDirectoryGraphResourceId": "https://graph.windows.net/",
  "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
  "galleryEndpointUrl": "https://gallery.azure.com/",
  "managementEndpointUrl": "https://management.core.windows.net/"
}
```
<span data-ttu-id="c79c1-130">아래 Python 코드 조각을 복사하고 서비스 주체를 만들기 위해 명령을 실행한 후 반환된 JSON 문자열을 `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET` 및 `SUBSCRIPTION_ID`에 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-130">Copy the below Python snippet and fill in `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET`, and `SUBSCRIPTION_ID` with the strings from the JSON that was returned after running the command to create the service principal.</span></span>

```python
from azure.mgmt.hdinsight import HDInsightManagementClient
from azure.common.credentials import ServicePrincipalCredentials
from azure.mgmt.hdinsight.models import *

# Tenant ID for your Azure Subscription
TENANT_ID = ''
# Your Service Principal App Client ID
CLIENT_ID = ''
# Your Service Principal Client Secret
CLIENT_SECRET = ''
# Your Azure Subscription ID
SUBSCRIPTION_ID = ''

credentials = ServicePrincipalCredentials(
    client_id = CLIENT_ID,
    secret = CLIENT_SECRET,
    tenant = TENANT_ID
)

client = HDInsightManagementClient(credentials, SUBSCRIPTION_ID)
```


## <a name="cluster-management"></a><span data-ttu-id="c79c1-131">클러스터 관리</span><span class="sxs-lookup"><span data-stu-id="c79c1-131">Cluster Management</span></span>

> [!NOTE]
> <span data-ttu-id="c79c1-132">이 섹션에서는 이미 인증이 수행되었고 `HDInsightManagementClient` 인스턴스가 생성되었으며, `client`라는 변수로 저장되었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-132">This section assumes you have already authenticated and constructed an `HDInsightManagementClient` instance and store it in a variable called `client`.</span></span> <span data-ttu-id="c79c1-133">`HDInsightManagementClient` 인증 및 가져오기 지침은 위에 표시된 인증 섹션에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-133">Instructions for authenticating and obtaining an `HDInsightManagementClient` can be found in the Authentication section above.</span></span>

### <a name="create-a-cluster"></a><span data-ttu-id="c79c1-134">클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="c79c1-134">Create a Cluster</span></span>

<span data-ttu-id="c79c1-135">`client.clusters.create()`을(를) 호출하여 새 클러스터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-135">A new cluster can be created by calling `client.clusters.create()`.</span></span> 

#### <a name="example"></a><span data-ttu-id="c79c1-136">예</span><span class="sxs-lookup"><span data-stu-id="c79c1-136">Example</span></span>

<span data-ttu-id="c79c1-137">이 예제에서는 2개의 헤드 노드 및 1개의 작업자 노드를 사용하여 Spark 클러스터를 만드는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-137">This example demonstrates how to create a Spark cluster with 2 head nodes and 1 worker node.</span></span>

> [!NOTE]
> <span data-ttu-id="c79c1-138">먼저 아래 설명된 대로 리소스 그룹 및 저장소 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-138">You first need to create a Resource Group and Storage Account, as explained below.</span></span> <span data-ttu-id="c79c1-139">이미 만든 경우에는 이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-139">If you have already created these, you can skip these steps.</span></span>

##### <a name="creating-a-resource-group"></a><span data-ttu-id="c79c1-140">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="c79c1-140">Creating a Resource Group</span></span>

<span data-ttu-id="c79c1-141">다음을 실행하여 [Azure Cloud Shell](https://shell.azure.com/bash)을 사용해서 리소스 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-141">You can create a resource group using the [Azure Cloud Shell](https://shell.azure.com/bash) by running</span></span>
```azurecli-interactive
az group create -l <Region Name (i.e. eastus)> --n <Resource Group Name>
```
##### <a name="creating-a-storage-account"></a><span data-ttu-id="c79c1-142">저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="c79c1-142">Creating a Storage Account</span></span>

<span data-ttu-id="c79c1-143">다음을 실행하여 [Azure Cloud Shell](https://shell.azure.com/bash)을 사용해서 저장소 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-143">You can create a storage account using the [Azure Cloud Shell](https://shell.azure.com/bash) by running:</span></span>
```azurecli-interactive
az storage account create -n <Storage Account Name> -g <Existing Resource Group Name> -l <Region Name (i.e. eastus)> --sku <SKU i.e. Standard_LRS>
```
<span data-ttu-id="c79c1-144">이제 다음 명령을 사용해서 저장소 계정에 대한 키를 가져옵니다(클러스터를 만들기 위해 필요).</span><span class="sxs-lookup"><span data-stu-id="c79c1-144">Now run the following command to get the key for your storage account (you will need this to create a cluster):</span></span>
```azurecli-interactive
az storage account keys list -n <Storage Account Name>
```
---
<span data-ttu-id="c79c1-145">아래의 Python 코드 조각은 2개의 헤드 노드 및 1개의 작업자 노드를 사용해서 Spark 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-145">The below Python snippet creates a Spark cluster with 2 head nodes and 1 worker node.</span></span> <span data-ttu-id="c79c1-146">주석 설명에 따라 빈 변수를 채우고 특정 요구에 따라 다른 매개변수를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-146">Fill in the blank variables as explained in the comments and feel free to change other parameters to suit your specific needs.</span></span>

```python
# The name for the cluster you are creating
cluster_name = ""
# The name of your existing Resource Group
resource_group_name = ""
# Choose a username
username = ""
# Choose a password
password = ""
# Replace <> with the name of your storage account
storage_account = "<>.blob.core.windows.net"
# Storage account key you obtained above
storage_account_key = ""
# Choose a region
location = ""
container = "default"

params = ClusterCreateProperties(
    cluster_version="3.6",
    os_type=OSType.linux,
    tier=Tier.standard,
    cluster_definition=ClusterDefinition(
        kind="spark",
        configurations={
            "gateway": {
                "restAuthCredential.enabled_credential": "True",
                "restAuthCredential.username": username,
                "restAuthCredential.password": password
            }
        }
    ),
    compute_profile=ComputeProfile(
        roles=[
            Role(
                name="headnode",
                target_instance_count=2,
                hardware_profile=HardwareProfile(vm_size="Large"),
                os_profile=OsProfile(
                    linux_operating_system_profile=LinuxOperatingSystemProfile(
                        username=username,
                        password=password
                    )
                )
            ),
            Role(
                name="workernode",
                target_instance_count=1,
                hardware_profile=HardwareProfile(vm_size="Large"),
                os_profile=OsProfile(
                    linux_operating_system_profile=LinuxOperatingSystemProfile(
                        username=username,
                        password=password
                    )
                )
            )
        ]
    ),
    storage_profile=StorageProfile(
        storageaccounts=[StorageAccount(
            name=storage_account,
            key=storage_account_key,
            container=container,
            is_default=True
        )]
    )
)

client.clusters.create(
    cluster_name=cluster_name,
    resource_group_name=resource_group_name,
    parameters=ClusterCreateParametersExtended(
        location=location,
        tags={},
        properties=params
    ))
```

### <a name="get-cluster-details"></a><span data-ttu-id="c79c1-147">클러스터 세부 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="c79c1-147">Get Cluster Details</span></span>

<span data-ttu-id="c79c1-148">지정된 클러스터에 대한 속성을 가져오려면:</span><span class="sxs-lookup"><span data-stu-id="c79c1-148">To get properties for a given cluster:</span></span>

```python
client.clusters.get("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a><span data-ttu-id="c79c1-149">예</span><span class="sxs-lookup"><span data-stu-id="c79c1-149">Example</span></span>

<span data-ttu-id="c79c1-150">`get`을(를) 사용하여 클러스터 만들기가 성공했는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-150">You can use `get` to confirm that you have successfully created your cluster.</span></span>

```python
my_cluster = client.clusters.get("<Resource Group Name>", "<Cluster Name>")
print(my_cluster)
```

<span data-ttu-id="c79c1-151">출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-151">The output should look like:</span></span>

```
{'additional_properties': {}, 'id': '/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/<Resource Group Name>/providers/Microsoft.HDInsight/clusters/<Cluster Name>', 'name': '<Cluster Name>', 'type': 'Microsoft.HDInsight/clusters', 'location': '<Location>', 'tags': {}, 'etag': 'XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX', 'properties': <azure.mgmt.hdinsight.models.cluster_get_properties_py3.ClusterGetProperties object at 0x0000013766D68048>}
```

### <a name="list-clusters"></a><span data-ttu-id="c79c1-152">클러스터 나열</span><span class="sxs-lookup"><span data-stu-id="c79c1-152">List Clusters</span></span>

#### <a name="list-clusters-under-the-subscription"></a><span data-ttu-id="c79c1-153">구독 아래에 클러스터 나열</span><span class="sxs-lookup"><span data-stu-id="c79c1-153">List Clusters Under The Subscription</span></span>

```python
client.clusters.list()
```
#### <a name="list-clusters-by-resource-group"></a><span data-ttu-id="c79c1-154">리소스 그룹별로 클러스터 나열</span><span class="sxs-lookup"><span data-stu-id="c79c1-154">List Clusters By Resource Group</span></span>

```python
client.clusters.list_by_resource_group("<Resource Group Name>")
```
> [!NOTE]
> <span data-ttu-id="c79c1-155">`list()` 및 `list_by_resource_group()` 모두 `ClusterPaged` 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-155">Both `list()` and `list_by_resource_group()` return an `ClusterPaged` object.</span></span> <span data-ttu-id="c79c1-156">`advance_page()`를 호출하면 해당 페이지의 클러스터 목록이 반환되고 `ClusterPaged` 개체가 다음 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-156">Calling `advance_page()` returns the a list of clusters on that page and advances the `ClusterPaged` object to the next page.</span></span> <span data-ttu-id="c79c1-157">`StopIteration` 예외가 제기될 때까지 반복할 수 있으며, 더 이상 페이지가 없음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-157">This can be repeated until a `StopIteration` exception is raised, indicating that there are no more pages.</span></span>

#### <a name="example"></a><span data-ttu-id="c79c1-158">예</span><span class="sxs-lookup"><span data-stu-id="c79c1-158">Example</span></span>

<span data-ttu-id="c79c1-159">다음 예제는 현재 구독에 대해 모든 클러스터 속성을 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-159">The following example prints the properties of all clusters for the current subscription:</span></span>

```python
clusters_paged = client.clusters.list()
while True:
  try:
    for cluster in clusters_paged.advance_page():
      print(cluster)
  except StopIteration: 
    break
```

### <a name="delete-a-cluster"></a><span data-ttu-id="c79c1-160">클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="c79c1-160">Delete a Cluster</span></span>

<span data-ttu-id="c79c1-161">클러스터를 삭제하려면:</span><span class="sxs-lookup"><span data-stu-id="c79c1-161">To delete a cluster:</span></span>

```python
client.clusters.delete("<Resource Group Name>", "<Cluster Name>")
```

### <a name="update-cluster-tags"></a><span data-ttu-id="c79c1-162">클러스터 태그 업데이트</span><span class="sxs-lookup"><span data-stu-id="c79c1-162">Update Cluster Tags</span></span>

<span data-ttu-id="c79c1-163">지정된 클러스터의 태그를 다음과 같이 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-163">You can update the tags of a given cluster like so:</span></span>

```python
client.clusters.update("<Resource Group Name>", "<Cluster Name>", tags={<Dictionary of Tags>})
```

#### <a name="example"></a><span data-ttu-id="c79c1-164">예</span><span class="sxs-lookup"><span data-stu-id="c79c1-164">Example</span></span>

```python
client.clusters.update("<Resource Group Name>", "<Cluster Name>", tags={"tag1Name" : "tag1Value", "tag2Name" : "tag2Value"})
```

### <a name="resize-cluster"></a><span data-ttu-id="c79c1-165">클러스터 크기 조정</span><span class="sxs-lookup"><span data-stu-id="c79c1-165">Resize Cluster</span></span>

<span data-ttu-id="c79c1-166">새 크기를 지정하여 작업자 노드의 지정된 클러스터 번호를 크기 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-166">You can resize a given cluster's number of worker nodes by specifying a new size like so:</span></span>

```python
client.clusters.resize("<Resource Group Name>", "<Cluster Name>", target_instance_count=<Num of Worker Nodes>)
```

## <a name="cluster-monitoring"></a><span data-ttu-id="c79c1-167">클러스터 모니터링</span><span class="sxs-lookup"><span data-stu-id="c79c1-167">Cluster Monitoring</span></span>

<span data-ttu-id="c79c1-168">또한 HDInsight 관리 SDK를 사용하여 OMS(Operations Management Suite)를 통해 클러스터에서 모니터링을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-168">The HDInsight Management SDK can also be used to manage monitoring on your clusters via the Operations Management Suite (OMS).</span></span>

### <a name="enable-oms-monitoring"></a><span data-ttu-id="c79c1-169">OMS 모니터링 사용</span><span class="sxs-lookup"><span data-stu-id="c79c1-169">Enable OMS Monitoring</span></span>

> [!NOTE]
> <span data-ttu-id="c79c1-170">OMS 모니터링을 사용하려면 기존 Log Analytics 작업 영역이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-170">To enable OMS Monitoring, you must have an existing Log Analytics workspace.</span></span> <span data-ttu-id="c79c1-171">아직 작업 영역을 만들지 않은 경우 다음에서 작업 영역을 만드는 방법을 알아볼 수 있습니다. [Azure Portal에서 Log Analytics 작업 영역 만들기](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).</span><span class="sxs-lookup"><span data-stu-id="c79c1-171">If you have not already created one, you can learn how to do that here: [Create a Log Analytics workspace in the Azure portal](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).</span></span>

<span data-ttu-id="c79c1-172">클러스터에서 OMS 모니터링을 사용하려면:</span><span class="sxs-lookup"><span data-stu-id="c79c1-172">To enable OMS Monitoring on your cluster:</span></span>

```python
client.extension.enable_monitoring("<Resource Group Name>", "<Cluster Name>", workspace_id="<Workspace Id>")
```

### <a name="view-status-of-oms-monitoring"></a><span data-ttu-id="c79c1-173">OMS 모니터링의 상태 보기</span><span class="sxs-lookup"><span data-stu-id="c79c1-173">View Status Of OMS Monitoring</span></span>

<span data-ttu-id="c79c1-174">클러스터에서 OMS 상태를 가져오려면:</span><span class="sxs-lookup"><span data-stu-id="c79c1-174">To get the status of OMS on your cluster:</span></span>

```python
client.extension.get_monitoring_status("<Resource Group Name", "Cluster Name")
```

### <a name="disable-oms-monitoring"></a><span data-ttu-id="c79c1-175">OMS 모니터링 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="c79c1-175">Disable OMS Monitoring</span></span>

<span data-ttu-id="c79c1-176">클러스터에서 OMS를 사용하지 않으려면:</span><span class="sxs-lookup"><span data-stu-id="c79c1-176">To disable OMS on your cluster:</span></span>

```python
client.extension.disable_monitoring("<Resource Group Name>", "<Cluster Name>")
```

## <a name="script-actions"></a><span data-ttu-id="c79c1-177">스크립트 동작</span><span class="sxs-lookup"><span data-stu-id="c79c1-177">Script Actions</span></span>

<span data-ttu-id="c79c1-178">HDInsight는 클러스터 사용자 지정을 위해 사용자 지정 스크립트를 호출하는 스크립트 작업이라고 부르는 구성 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-178">HDInsight provides a configuration method called script actions that invokes custom scripts to customize the cluster.</span></span>
> [!NOTE]
> <span data-ttu-id="c79c1-179">스크립트 작업을 사용하는 방법에 대한 자세한 내용은 다음에서 찾을 수 있습니다. [스크립트 작업을 사용하여 Linux 기반 HDInsight 클러스터 사용자 지정](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span><span class="sxs-lookup"><span data-stu-id="c79c1-179">More information on how to use script actions can be found here: [Customize Linux-based HDInsight clusters using script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)</span></span>

### <a name="execute-script-actions"></a><span data-ttu-id="c79c1-180">스크립트 작업 실행</span><span class="sxs-lookup"><span data-stu-id="c79c1-180">Execute Script Actions</span></span>
<span data-ttu-id="c79c1-181">지정된 클러스터에서 스크립트 작업을 실행하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-181">To execute script actions on a given cluster:</span></span>

```python
script_action1 = RuntimeScriptAction(name="<Script Name>", uri="<URL To Script>", roles=[<List of Roles>]) #valid roles are "headnode", "workernode", "zookeepernode", and "edgenode"

client.clusters.execute_script_actions("<Resource Group Name>", "<Cluster Name>", <persist_on_success (bool)>, script_actions=[script_action1]) #add more RuntimeScriptActions to the list to execute multiple scripts
```

### <a name="delete-script-action"></a><span data-ttu-id="c79c1-182">스크립트 작업 삭제</span><span class="sxs-lookup"><span data-stu-id="c79c1-182">Delete Script Action</span></span>

<span data-ttu-id="c79c1-183">지정된 클러스터에서 지정된 지속형 스크립트 작업을 삭제하려면:</span><span class="sxs-lookup"><span data-stu-id="c79c1-183">To delete a specified persisted script action on a given cluster:</span></span>

```python
client.script_actions.delete("<Resource Group Name>", "<Cluster Name", "<Script Name>")
```

### <a name="list-persisted-script-actions"></a><span data-ttu-id="c79c1-184">지속형 스크립트 작업 나열</span><span class="sxs-lookup"><span data-stu-id="c79c1-184">List Persisted Script Actions</span></span>

> [!NOTE]
> <span data-ttu-id="c79c1-185">`list()` 및 `list_persisted_scripts()`는 `RuntimeScriptActionDetailPaged` 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-185">`list()` and `list_persisted_scripts()` return a `RuntimeScriptActionDetailPaged` object.</span></span> <span data-ttu-id="c79c1-186">`advance_page()`를 호출하면 해당 페이지의 `RuntimeScriptActionDetail` 목록이 반환되고 `RuntimeScriptActionDetailPaged` 개체가 다음 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-186">Calling `advance_page()` returns the a list of `RuntimeScriptActionDetail` on that page and advances the `RuntimeScriptActionDetailPaged` object to the next page.</span></span> <span data-ttu-id="c79c1-187">`StopIteration` 예외가 제기될 때까지 반복할 수 있으며, 더 이상 페이지가 없음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-187">This can be repeated until a `StopIteration` exception is raised, indicating that there are no more pages.</span></span> <span data-ttu-id="c79c1-188">아래 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="c79c1-188">See the example below.</span></span>

<span data-ttu-id="c79c1-189">지정된 클러스터에 대해 모든 지속형 스크립트 작업을 나열하려면:</span><span class="sxs-lookup"><span data-stu-id="c79c1-189">To list all persisted script actions for the specified cluster:</span></span>
```python
client.script_actions.list_persisted_scripts("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a><span data-ttu-id="c79c1-190">예</span><span class="sxs-lookup"><span data-stu-id="c79c1-190">Example</span></span>

```python
scripts_paged = client.script_actions.list_persisted_scripts(resource_group_name, cluster_name)
while True:
  try:
    for script in scripts_paged.advance_page():
      print(script)
  except StopIteration:
    break
```

### <a name="list-all-scripts-execution-history"></a><span data-ttu-id="c79c1-191">모든 스크립트 실행 기록 나열</span><span class="sxs-lookup"><span data-stu-id="c79c1-191">List All Scripts' Execution History</span></span>

<span data-ttu-id="c79c1-192">지정된 클러스터에 대해 모든 스크립트 실행 기록을 나열하려면:</span><span class="sxs-lookup"><span data-stu-id="c79c1-192">To list all scripts' execution history for the specified cluster:</span></span>

```python
client.script_execution_history.list("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a><span data-ttu-id="c79c1-193">예</span><span class="sxs-lookup"><span data-stu-id="c79c1-193">Example</span></span>

<span data-ttu-id="c79c1-194">이 예제는 모든 과거 스크립트 실행에 대한 모든 세부 정보를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="c79c1-194">This example prints all the details for all past script executions.</span></span>

```python
script_executions_paged = client.script_execution_history.list("<Resource Group Name>", "<Cluster Name>")
while True:
  try:
    for script in script_executions_paged.advance_page():            
      print(script)
    except StopIteration:       
      break
```
