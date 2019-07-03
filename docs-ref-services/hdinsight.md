---
title: Python용 Azure HDInsight SDK
description: Python용 Azure HDInsight SDK에 대한 참조입니다. Python용 HDInsight SDK는 HDInsight 클러스터를 관리할 수 있는 클래스와 메서드를 제공합니다.
ms.service: hdinsight
author: tylerfox
ms.author: tyfox
ms.date: 04/10/2019
ms.topic: reference
ms.devlang: python
ms.openlocfilehash: 3b0799dd77f7ff447ef997b2d142a6744c4a6858
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534262"
---
# <a name="hdinsight-sdk-for-python"></a><span data-ttu-id="e6930-104">Python용 HDInsight SDK</span><span class="sxs-lookup"><span data-stu-id="e6930-104">HDInsight SDK for Python</span></span>

## <a name="overview"></a><span data-ttu-id="e6930-105">개요</span><span class="sxs-lookup"><span data-stu-id="e6930-105">Overview</span></span>

<span data-ttu-id="e6930-106">Python용 HDInsight SDK는 HDInsight 클러스터를 관리할 수 있는 클래스와 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-106">The HDInsight SDK for Python provides classes and methods that allow you to manage your HDInsight clusters.</span></span> <span data-ttu-id="e6930-107">여기에는 HDInsight 클러스터의 속성 만들기, 삭제, 업데이트, 나열, 크기 조정, 스크립트 작업 실행, 모니터링, 가져오기 작업을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-107">It includes operations to create, delete, update, list, resize, execute script actions, monitor, get properties of HDInsight clusters, and more.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e6930-108">필수 조건</span><span class="sxs-lookup"><span data-stu-id="e6930-108">Prerequisites</span></span>

* <span data-ttu-id="e6930-109">Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="e6930-109">An Azure account.</span></span> <span data-ttu-id="e6930-110">계정이 없으면 [체험 계정을 얻습니다](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="e6930-110">If you don't have one, [get a free trial](https://azure.microsoft.com/free/).</span></span>
* [<span data-ttu-id="e6930-111">Python</span><span class="sxs-lookup"><span data-stu-id="e6930-111">Python</span></span>](https://www.python.org/downloads/)
* [<span data-ttu-id="e6930-112">pip</span><span class="sxs-lookup"><span data-stu-id="e6930-112">pip</span></span>](https://pypi.org/project/pip/#description)

## <a name="sdk-installation"></a><span data-ttu-id="e6930-113">SDK 설치</span><span class="sxs-lookup"><span data-stu-id="e6930-113">SDK Installation</span></span>

<span data-ttu-id="e6930-114">Python용 HDInsight SDK는 [Python 패키지 인덱스](https://pypi.org/project/azure-mgmt-hdinsight/)에 있으며 다음을 실행하여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-114">The HDInsight SDK for Python can be found in the [Python Package Index](https://pypi.org/project/azure-mgmt-hdinsight/) and can be installed by running:</span></span> 

`pip install azure-mgmt-hdinsight`

## <a name="authentication"></a><span data-ttu-id="e6930-115">인증</span><span class="sxs-lookup"><span data-stu-id="e6930-115">Authentication</span></span>

<span data-ttu-id="e6930-116">Azure 구독을 사용해서 SDK를 먼저 인증해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-116">The SDK first needs to be authenticated with your Azure subscription.</span></span>  <span data-ttu-id="e6930-117">아래 예제에 따라 서비스 주체를 만들고 이를 인증에 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-117">Follow the example below to create a service principal and use it to authenticate.</span></span> <span data-ttu-id="e6930-118">완료되었으면 관리 작업 수행을 위해 사용할 수 있는 여러 메서드(아래 섹션 참조)가 포함된 `HDInsightManagementClient` 인스턴스가 준비됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-118">After this is done, you will have an instance of an `HDInsightManagementClient`, which contains many methods (outlined in below sections) that can be used to perform management operations.</span></span>

> [!NOTE]
> <span data-ttu-id="e6930-119">아래 설명된 예제 외에도 사용자 요구에 더 적합할 수 있는 다른 인증 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-119">There are other ways to authenticate besides the below example that could potentially be better suited for your needs.</span></span> <span data-ttu-id="e6930-120">모든 메서드는 여기에 설명되어 있습니다. [Python용 Azure 관리 라이브러리를 사용하여 인증](https://docs.microsoft.com/en-us/python/azure/python-sdk-azure-authenticate?view=azure-python)</span><span class="sxs-lookup"><span data-stu-id="e6930-120">All methods are outlined here: [Authenticate with the Azure Management Libraries for Python](https://docs.microsoft.com/en-us/python/azure/python-sdk-azure-authenticate?view=azure-python)</span></span>

### <a name="authentication-example-using-a-service-principal"></a><span data-ttu-id="e6930-121">서비스 주체를 사용한 인증 예제</span><span class="sxs-lookup"><span data-stu-id="e6930-121">Authentication Example Using a Service Principal</span></span>

<span data-ttu-id="e6930-122">먼저, [Azure Cloud Shell](https://shell.azure.com/bash)에 로그인합니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-122">First, login to [Azure Cloud Shell](https://shell.azure.com/bash).</span></span> <span data-ttu-id="e6930-123">서비스 주체를 만들려는 구독을 현재 사용하고 있는지 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-123">Verify you are currently using the subscription in which you want the service principal created.</span></span> 

```azurecli-interactive
az account show
```

<span data-ttu-id="e6930-124">구독 정보는 JSON으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-124">Your subscription information is displayed as JSON.</span></span>

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

<span data-ttu-id="e6930-125">올바른 구독으로 로그인되지 않은 경우 다음을 실행하여 올바른 구독을 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-125">If you're not logged into the correct subscription, select the correct one by running:</span></span> 
```azurecli-interactive
az account set -s <name or ID of subscription>
```

> [!IMPORTANT]
> <span data-ttu-id="e6930-126">Azure Portal을 통해 HDInsight Cluster를 만드는 등 다른 방법을 사용해서 HDInsight Resource Provider를 등록하지 않은 경우, 이를 먼저 수행해야 인증할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-126">If you have not already registered the HDInsight Resource Provider by another method (such as by creating an HDInsight Cluster through the Azure Portal), you need to do this once before you can authenticate.</span></span> <span data-ttu-id="e6930-127">이 작업은 [Azure Cloud Shell](https://shell.azure.com/bash)에서 다음 명령을 실행하여 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-127">This can be done from the [Azure Cloud Shell](https://shell.azure.com/bash) by running the following command:</span></span>
>```azurecli-interactive
>az provider register --namespace Microsoft.HDInsight
>```

<span data-ttu-id="e6930-128">그런 다음 서비스 주체 이름을 선택하고 다음 명령을 사용해서 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-128">Next, choose a name for your service principal and create it with the following command:</span></span>

```azurecli-interactive
az ad sp create-for-rbac --name <Service Principal Name> --sdk-auth
```

<span data-ttu-id="e6930-129">서비스 주체 정보는 JSON으로 표시됩니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-129">The service principal information is displayed as JSON.</span></span>

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
<span data-ttu-id="e6930-130">아래 Python 코드 조각을 복사하고 서비스 주체를 만들기 위해 명령을 실행한 후 반환된 JSON 문자열을 `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET` 및 `SUBSCRIPTION_ID`에 채웁니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-130">Copy the below Python snippet and fill in `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET`, and `SUBSCRIPTION_ID` with the strings from the JSON that was returned after running the command to create the service principal.</span></span>

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


## <a name="cluster-management"></a><span data-ttu-id="e6930-131">클러스터 관리</span><span class="sxs-lookup"><span data-stu-id="e6930-131">Cluster Management</span></span>

> [!NOTE]
> <span data-ttu-id="e6930-132">이 섹션에서는 이미 인증이 수행되었고 `HDInsightManagementClient` 인스턴스가 생성되었으며, `client`라는 변수로 저장되었다고 가정합니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-132">This section assumes you have already authenticated and constructed an `HDInsightManagementClient` instance and store it in a variable called `client`.</span></span> <span data-ttu-id="e6930-133">`HDInsightManagementClient` 인증 및 가져오기 지침은 위에 표시된 인증 섹션에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-133">Instructions for authenticating and obtaining an `HDInsightManagementClient` can be found in the Authentication section above.</span></span>

### <a name="create-a-cluster"></a><span data-ttu-id="e6930-134">클러스터 만들기</span><span class="sxs-lookup"><span data-stu-id="e6930-134">Create a Cluster</span></span>

<span data-ttu-id="e6930-135">`client.clusters.create()`을(를) 호출하여 새 클러스터를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-135">A new cluster can be created by calling `client.clusters.create()`.</span></span>

#### <a name="samples"></a><span data-ttu-id="e6930-136">샘플</span><span class="sxs-lookup"><span data-stu-id="e6930-136">Samples</span></span>

<span data-ttu-id="e6930-137">몇 가지 일반적인 유형의 HDInsight 클러스터를 만드는 코드 샘플([HDInsight Python 샘플](https://github.com/Azure-Samples/hdinsight-python-sdk-samples))도 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-137">Code samples for creating several common types of HDInsight clusters are available: [HDInsight Python Samples](https://github.com/Azure-Samples/hdinsight-python-sdk-samples).</span></span>

#### <a name="example"></a><span data-ttu-id="e6930-138">예</span><span class="sxs-lookup"><span data-stu-id="e6930-138">Example</span></span>

<span data-ttu-id="e6930-139">이 예제에서는 2개의 헤드 노드 및 1개의 작업자 노드를 사용하여 Spark 클러스터를 만드는 방법을 보여줍니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-139">This example demonstrates how to create a Spark cluster with 2 head nodes and 1 worker node.</span></span>

> [!NOTE]
> <span data-ttu-id="e6930-140">먼저 아래 설명된 대로 리소스 그룹 및 저장소 계정을 만들어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-140">You first need to create a Resource Group and Storage Account, as explained below.</span></span> <span data-ttu-id="e6930-141">이미 만든 경우에는 이 단계를 건너뛸 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-141">If you have already created these, you can skip these steps.</span></span>

##### <a name="creating-a-resource-group"></a><span data-ttu-id="e6930-142">리소스 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="e6930-142">Creating a Resource Group</span></span>

<span data-ttu-id="e6930-143">다음을 실행하여 [Azure Cloud Shell](https://shell.azure.com/bash)을 사용해서 리소스 그룹을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-143">You can create a resource group using the [Azure Cloud Shell](https://shell.azure.com/bash) by running</span></span>
```azurecli-interactive
az group create -l <Region Name (i.e. eastus)> --n <Resource Group Name>
```
##### <a name="creating-a-storage-account"></a><span data-ttu-id="e6930-144">저장소 계정 만들기</span><span class="sxs-lookup"><span data-stu-id="e6930-144">Creating a Storage Account</span></span>

<span data-ttu-id="e6930-145">다음을 실행하여 [Azure Cloud Shell](https://shell.azure.com/bash)을 사용해서 저장소 계정을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-145">You can create a storage account using the [Azure Cloud Shell](https://shell.azure.com/bash) by running:</span></span>
```azurecli-interactive
az storage account create -n <Storage Account Name> -g <Existing Resource Group Name> -l <Region Name (i.e. eastus)> --sku <SKU i.e. Standard_LRS>
```
<span data-ttu-id="e6930-146">이제 다음 명령을 사용해서 저장소 계정에 대한 키를 가져옵니다(클러스터를 만들기 위해 필요).</span><span class="sxs-lookup"><span data-stu-id="e6930-146">Now run the following command to get the key for your storage account (you will need this to create a cluster):</span></span>
```azurecli-interactive
az storage account keys list -n <Storage Account Name>
```
---
<span data-ttu-id="e6930-147">아래의 Python 코드 조각은 2개의 헤드 노드 및 1개의 작업자 노드를 사용해서 Spark 클러스터를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-147">The below Python snippet creates a Spark cluster with 2 head nodes and 1 worker node.</span></span> <span data-ttu-id="e6930-148">주석 설명에 따라 빈 변수를 채우고 특정 요구에 따라 다른 매개변수를 변경합니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-148">Fill in the blank variables as explained in the comments and feel free to change other parameters to suit your specific needs.</span></span>

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

### <a name="get-cluster-details"></a><span data-ttu-id="e6930-149">클러스터 세부 정보 가져오기</span><span class="sxs-lookup"><span data-stu-id="e6930-149">Get Cluster Details</span></span>

<span data-ttu-id="e6930-150">지정된 클러스터에 대한 속성을 가져오려면:</span><span class="sxs-lookup"><span data-stu-id="e6930-150">To get properties for a given cluster:</span></span>

```python
client.clusters.get("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a><span data-ttu-id="e6930-151">예</span><span class="sxs-lookup"><span data-stu-id="e6930-151">Example</span></span>

<span data-ttu-id="e6930-152">`get`을(를) 사용하여 클러스터 만들기가 성공했는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-152">You can use `get` to confirm that you have successfully created your cluster.</span></span>

```python
my_cluster = client.clusters.get("<Resource Group Name>", "<Cluster Name>")
print(my_cluster)
```

<span data-ttu-id="e6930-153">출력은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-153">The output should look like:</span></span>

```output
{'additional_properties': {}, 'id': '/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/<Resource Group Name>/providers/Microsoft.HDInsight/clusters/<Cluster Name>', 'name': '<Cluster Name>', 'type': 'Microsoft.HDInsight/clusters', 'location': '<Location>', 'tags': {}, 'etag': 'XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX', 'properties': <azure.mgmt.hdinsight.models.cluster_get_properties_py3.ClusterGetProperties object at 0x0000013766D68048>}
```

### <a name="list-clusters"></a><span data-ttu-id="e6930-154">클러스터 나열</span><span class="sxs-lookup"><span data-stu-id="e6930-154">List Clusters</span></span>

#### <a name="list-clusters-under-the-subscription"></a><span data-ttu-id="e6930-155">구독 아래에 클러스터 나열</span><span class="sxs-lookup"><span data-stu-id="e6930-155">List Clusters Under The Subscription</span></span>

```python
client.clusters.list()
```
#### <a name="list-clusters-by-resource-group"></a><span data-ttu-id="e6930-156">리소스 그룹별로 클러스터 나열</span><span class="sxs-lookup"><span data-stu-id="e6930-156">List Clusters By Resource Group</span></span>

```python
client.clusters.list_by_resource_group("<Resource Group Name>")
```
> [!NOTE]
> <span data-ttu-id="e6930-157">`list()` 및 `list_by_resource_group()` 모두 `ClusterPaged` 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-157">Both `list()` and `list_by_resource_group()` return a `ClusterPaged` object.</span></span> <span data-ttu-id="e6930-158">`advance_page()`를 호출하면 해당 페이지의 클러스터 목록이 반환되고 `ClusterPaged` 개체가 다음 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-158">Calling `advance_page()` returns a list of clusters on that page and advances the `ClusterPaged` object to the next page.</span></span> <span data-ttu-id="e6930-159">`StopIteration` 예외가 제기될 때까지 반복할 수 있으며, 더 이상 페이지가 없음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-159">This can be repeated until a `StopIteration` exception is raised, indicating that there are no more pages.</span></span>

#### <a name="example"></a><span data-ttu-id="e6930-160">예</span><span class="sxs-lookup"><span data-stu-id="e6930-160">Example</span></span>

<span data-ttu-id="e6930-161">다음 예제는 현재 구독에 대해 모든 클러스터 속성을 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-161">The following example prints the properties of all clusters for the current subscription:</span></span>

```python
clusters_paged = client.clusters.list()
while True:
  try:
    for cluster in clusters_paged.advance_page():
      print(cluster)
  except StopIteration: 
    break
```

### <a name="delete-a-cluster"></a><span data-ttu-id="e6930-162">클러스터 삭제</span><span class="sxs-lookup"><span data-stu-id="e6930-162">Delete a Cluster</span></span>

<span data-ttu-id="e6930-163">클러스터를 삭제하려면:</span><span class="sxs-lookup"><span data-stu-id="e6930-163">To delete a cluster:</span></span>

```python
client.clusters.delete("<Resource Group Name>", "<Cluster Name>")
```

### <a name="update-cluster-tags"></a><span data-ttu-id="e6930-164">클러스터 태그 업데이트</span><span class="sxs-lookup"><span data-stu-id="e6930-164">Update Cluster Tags</span></span>

<span data-ttu-id="e6930-165">지정된 클러스터의 태그를 다음과 같이 업데이트할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-165">You can update the tags of a given cluster like so:</span></span>

```python
client.clusters.update("<Resource Group Name>", "<Cluster Name>", tags={<Dictionary of Tags>})
```

#### <a name="example"></a><span data-ttu-id="e6930-166">예</span><span class="sxs-lookup"><span data-stu-id="e6930-166">Example</span></span>

```python
client.clusters.update("<Resource Group Name>", "<Cluster Name>", tags={"tag1Name" : "tag1Value", "tag2Name" : "tag2Value"})
```

### <a name="resize-cluster"></a><span data-ttu-id="e6930-167">클러스터 크기 조정</span><span class="sxs-lookup"><span data-stu-id="e6930-167">Resize Cluster</span></span>

<span data-ttu-id="e6930-168">새 크기를 지정하여 작업자 노드의 지정된 클러스터 번호를 크기 조정할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-168">You can resize a given cluster's number of worker nodes by specifying a new size like so:</span></span>

```python
client.clusters.resize("<Resource Group Name>", "<Cluster Name>", target_instance_count=<Num of Worker Nodes>)
```

## <a name="cluster-monitoring"></a><span data-ttu-id="e6930-169">클러스터 모니터링</span><span class="sxs-lookup"><span data-stu-id="e6930-169">Cluster Monitoring</span></span>

<span data-ttu-id="e6930-170">또한 HDInsight 관리 SDK를 사용하여 OMS(Operations Management Suite)를 통해 클러스터에서 모니터링을 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-170">The HDInsight Management SDK can also be used to manage monitoring on your clusters via the Operations Management Suite (OMS).</span></span>

### <a name="enable-oms-monitoring"></a><span data-ttu-id="e6930-171">OMS 모니터링 사용</span><span class="sxs-lookup"><span data-stu-id="e6930-171">Enable OMS Monitoring</span></span>

> [!NOTE]
> <span data-ttu-id="e6930-172">OMS 모니터링을 사용하려면 기존 Log Analytics 작업 영역이 있어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-172">To enable OMS Monitoring, you must have an existing Log Analytics workspace.</span></span> <span data-ttu-id="e6930-173">아직 작업 영역을 만들지 않은 경우 다음에서 작업 영역을 만드는 방법을 알아볼 수 있습니다. [Azure Portal에서 Log Analytics 작업 영역 만들기](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).</span><span class="sxs-lookup"><span data-stu-id="e6930-173">If you have not already created one, you can learn how to do that here: [Create a Log Analytics workspace in the Azure portal](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).</span></span>

<span data-ttu-id="e6930-174">클러스터에서 OMS 모니터링을 사용하려면:</span><span class="sxs-lookup"><span data-stu-id="e6930-174">To enable OMS Monitoring on your cluster:</span></span>

```python
client.extension.enable_monitoring("<Resource Group Name>", "<Cluster Name>", workspace_id="<Workspace Id>")
```

### <a name="view-status-of-oms-monitoring"></a><span data-ttu-id="e6930-175">OMS 모니터링의 상태 보기</span><span class="sxs-lookup"><span data-stu-id="e6930-175">View Status Of OMS Monitoring</span></span>

<span data-ttu-id="e6930-176">클러스터에서 OMS 상태를 가져오려면:</span><span class="sxs-lookup"><span data-stu-id="e6930-176">To get the status of OMS on your cluster:</span></span>

```python
client.extension.get_monitoring_status("<Resource Group Name", "Cluster Name")
```

### <a name="disable-oms-monitoring"></a><span data-ttu-id="e6930-177">OMS 모니터링 사용 안 함</span><span class="sxs-lookup"><span data-stu-id="e6930-177">Disable OMS Monitoring</span></span>

<span data-ttu-id="e6930-178">클러스터에서 OMS를 사용하지 않으려면:</span><span class="sxs-lookup"><span data-stu-id="e6930-178">To disable OMS on your cluster:</span></span>

```python
client.extension.disable_monitoring("<Resource Group Name>", "<Cluster Name>")
```

## <a name="script-actions"></a><span data-ttu-id="e6930-179">스크립트 동작</span><span class="sxs-lookup"><span data-stu-id="e6930-179">Script Actions</span></span>

<span data-ttu-id="e6930-180">HDInsight는 클러스터 사용자 지정을 위해 사용자 지정 스크립트를 호출하는 스크립트 작업이라고 부르는 구성 메서드를 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-180">HDInsight provides a configuration method called script actions that invokes custom scripts to customize the cluster.</span></span>
> [!NOTE]
> <span data-ttu-id="e6930-181">스크립트 작업을 사용하는 방법에 대한 자세한 내용은 다음에서 찾을 수 있습니다. [스크립트 작업을 사용하여 Linux 기반 HDInsight 클러스터 사용자 지정](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).</span><span class="sxs-lookup"><span data-stu-id="e6930-181">More information on how to use script actions can be found here: [Customize Linux-based HDInsight clusters using script actions](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux)</span></span>

### <a name="execute-script-actions"></a><span data-ttu-id="e6930-182">스크립트 작업 실행</span><span class="sxs-lookup"><span data-stu-id="e6930-182">Execute Script Actions</span></span>
<span data-ttu-id="e6930-183">지정된 클러스터에서 스크립트 작업을 실행하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-183">To execute script actions on a given cluster:</span></span>

```python
script_action1 = RuntimeScriptAction(name="<Script Name>", uri="<URL To Script>", roles=[<List of Roles>]) #valid roles are "headnode", "workernode", "zookeepernode", and "edgenode"

client.clusters.execute_script_actions("<Resource Group Name>", "<Cluster Name>", <persist_on_success (bool)>, script_actions=[script_action1]) #add more RuntimeScriptActions to the list to execute multiple scripts
```

### <a name="delete-script-action"></a><span data-ttu-id="e6930-184">스크립트 작업 삭제</span><span class="sxs-lookup"><span data-stu-id="e6930-184">Delete Script Action</span></span>

<span data-ttu-id="e6930-185">지정된 클러스터에서 지정된 지속형 스크립트 작업을 삭제하려면:</span><span class="sxs-lookup"><span data-stu-id="e6930-185">To delete a specified persisted script action on a given cluster:</span></span>

```python
client.script_actions.delete("<Resource Group Name>", "<Cluster Name", "<Script Name>")
```

### <a name="list-persisted-script-actions"></a><span data-ttu-id="e6930-186">지속형 스크립트 작업 나열</span><span class="sxs-lookup"><span data-stu-id="e6930-186">List Persisted Script Actions</span></span>

> [!NOTE]
> <span data-ttu-id="e6930-187">`list()` 및 `list_persisted_scripts()`는 `RuntimeScriptActionDetailPaged` 개체를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-187">`list()` and `list_persisted_scripts()` return a `RuntimeScriptActionDetailPaged` object.</span></span> <span data-ttu-id="e6930-188">`advance_page()`를 호출하면 해당 페이지의 `RuntimeScriptActionDetail` 목록이 반환되고 `RuntimeScriptActionDetailPaged` 개체가 다음 페이지로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-188">Calling `advance_page()` returns a list of `RuntimeScriptActionDetail` on that page and advances the `RuntimeScriptActionDetailPaged` object to the next page.</span></span> <span data-ttu-id="e6930-189">`StopIteration` 예외가 제기될 때까지 반복할 수 있으며, 더 이상 페이지가 없음을 나타냅니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-189">This can be repeated until a `StopIteration` exception is raised, indicating that there are no more pages.</span></span> <span data-ttu-id="e6930-190">아래 예제를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="e6930-190">See the example below.</span></span>

<span data-ttu-id="e6930-191">지정된 클러스터에 대해 모든 지속형 스크립트 작업을 나열하려면:</span><span class="sxs-lookup"><span data-stu-id="e6930-191">To list all persisted script actions for the specified cluster:</span></span>
```python
client.script_actions.list_persisted_scripts("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a><span data-ttu-id="e6930-192">예</span><span class="sxs-lookup"><span data-stu-id="e6930-192">Example</span></span>

```python
scripts_paged = client.script_actions.list_persisted_scripts(resource_group_name, cluster_name)
while True:
  try:
    for script in scripts_paged.advance_page():
      print(script)
  except StopIteration:
    break
```

### <a name="list-all-scripts-execution-history"></a><span data-ttu-id="e6930-193">모든 스크립트 실행 기록 나열</span><span class="sxs-lookup"><span data-stu-id="e6930-193">List All Scripts' Execution History</span></span>

<span data-ttu-id="e6930-194">지정된 클러스터에 대해 모든 스크립트 실행 기록을 나열하려면:</span><span class="sxs-lookup"><span data-stu-id="e6930-194">To list all scripts' execution history for the specified cluster:</span></span>

```python
client.script_execution_history.list("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a><span data-ttu-id="e6930-195">예</span><span class="sxs-lookup"><span data-stu-id="e6930-195">Example</span></span>

<span data-ttu-id="e6930-196">이 예제는 모든 과거 스크립트 실행에 대한 모든 세부 정보를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="e6930-196">This example prints all the details for all past script executions.</span></span>

```python
script_executions_paged = client.script_execution_history.list("<Resource Group Name>", "<Cluster Name>")
while True:
  try:
    for script in script_executions_paged.advance_page():            
      print(script)
    except StopIteration:       
      break
```
