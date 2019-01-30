---
title: Azure HDInsight Python SDK 미리 보기
description: Azure HDInsight Python SDK 참조 HDInsight Python SDK는 HDInsight 클러스터 관리를 위한 클래스 및 메서드를 제공합니다.
ms.service: hdinsight
author: tylerfox
ms.author: tyfox
ms.date: 09/18/2018
ms.topic: reference
ms.devlang: python
ms.openlocfilehash: 8d081739a3984e1cd3f7bbf31fcb44d63cfb6947
ms.sourcegitcommit: fba77bdf8eb9f49621be94544d9fef88aff98c14
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54747713"
---
# <a name="hdinsight-python-management-sdk-preview"></a>HDInsight Python 관리 SDK 미리 보기

## <a name="overview"></a>개요

HDInsight Python SDK는 HDInsight 클러스터 관리를 위한 클래스 및 메서드를 제공합니다. 여기에는 HDInsight 클러스터의 속성 만들기, 삭제, 업데이트, 나열, 크기 조정, 스크립트 작업 실행, 모니터링, 가져오기 작업을 포함합니다.

## <a name="prerequisites"></a>필수 조건

* Azure 계정. 계정이 없으면 [체험 계정을 얻습니다](https://azure.microsoft.com/free/).
* [Python](https://www.python.org/downloads/)
* [pip](https://pypi.org/project/pip/#description)

## <a name="sdk-installation"></a>SDK 설치

HDInsight Python SDK는 [Python 패키지 인덱스](https://pypi.org/project/azure-mgmt-hdinsight/)에 있으며 다음을 실행하여 설치할 수 있습니다. 

`pip install azure-mgmt-hdinsight`

## <a name="authentication"></a>인증

Azure 구독을 사용해서 SDK를 먼저 인증해야 합니다.  아래 예제에 따라 서비스 주체를 만들고 이를 인증에 사용합니다. 완료되었으면 관리 작업 수행을 위해 사용할 수 있는 여러 메서드(아래 섹션 참조)가 포함된 `HDInsightManagementClient` 인스턴스가 준비됩니다.

> [!NOTE]
> 아래 설명된 예제 외에도 사용자 요구에 더 적합할 수 있는 다른 인증 방법이 있습니다. 모든 메서드는 여기에 설명되어 있습니다. [Python용 Azure 관리 라이브러리를 사용하여 인증](https://docs.microsoft.com/en-us/python/azure/python-sdk-azure-authenticate?view=azure-python)

### <a name="authentication-example-using-a-service-principal"></a>서비스 주체를 사용한 인증 예제

먼저, [Azure Cloud Shell](https://shell.azure.com/bash)에 로그인합니다. 서비스 주체를 만들려는 구독을 현재 사용하고 있는지 확인합니다. 

```azurecli-interactive
az account show
```

구독 정보는 JSON으로 표시됩니다.

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

올바른 구독으로 로그인되지 않은 경우 다음을 실행하여 올바른 구독을 선택합니다. 
```azurecli-interactive
az account set -s <name or ID of subscription>
```

> [!IMPORTANT]
> Azure Portal을 통해 HDInsight Cluster를 만드는 등 다른 방법을 사용해서 HDInsight Resource Provider를 등록하지 않은 경우, 이를 먼저 수행해야 인증할 수 있습니다. 이 작업은 [Azure Cloud Shell](https://shell.azure.com/bash)에서 다음 명령을 실행하여 수행할 수 있습니다.
>```azurecli-interactive
>az provider register --namespace Microsoft.HDInsight
>```

그런 다음 서비스 주체 이름을 선택하고 다음 명령을 사용해서 만듭니다.

```azurecli-interactive
az ad sp create-for-rbac --name <Service Principal Name> --sdk-auth
```

서비스 주체 정보는 JSON으로 표시됩니다.

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
아래 Python 코드 조각을 복사하고 서비스 주체를 만들기 위해 명령을 실행한 후 반환된 JSON 문자열을 `TENANT_ID`, `CLIENT_ID`, `CLIENT_SECRET` 및 `SUBSCRIPTION_ID`에 채웁니다.

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


## <a name="cluster-management"></a>클러스터 관리

> [!NOTE]
> 이 섹션에서는 이미 인증이 수행되었고 `HDInsightManagementClient` 인스턴스가 생성되었으며, `client`라는 변수로 저장되었다고 가정합니다. `HDInsightManagementClient` 인증 및 가져오기 지침은 위에 표시된 인증 섹션에서 찾을 수 있습니다.

### <a name="create-a-cluster"></a>클러스터 만들기

`client.clusters.create()`을(를) 호출하여 새 클러스터를 만들 수 있습니다. 

#### <a name="example"></a>예

이 예제에서는 2개의 헤드 노드 및 1개의 작업자 노드를 사용하여 Spark 클러스터를 만드는 방법을 보여줍니다.

> [!NOTE]
> 먼저 아래 설명된 대로 리소스 그룹 및 저장소 계정을 만들어야 합니다. 이미 만든 경우에는 이 단계를 건너뛸 수 있습니다.

##### <a name="creating-a-resource-group"></a>리소스 그룹 만들기

다음을 실행하여 [Azure Cloud Shell](https://shell.azure.com/bash)을 사용해서 리소스 그룹을 만들 수 있습니다.
```azurecli-interactive
az group create -l <Region Name (i.e. eastus)> --n <Resource Group Name>
```
##### <a name="creating-a-storage-account"></a>저장소 계정 만들기

다음을 실행하여 [Azure Cloud Shell](https://shell.azure.com/bash)을 사용해서 저장소 계정을 만들 수 있습니다.
```azurecli-interactive
az storage account create -n <Storage Account Name> -g <Existing Resource Group Name> -l <Region Name (i.e. eastus)> --sku <SKU i.e. Standard_LRS>
```
이제 다음 명령을 사용해서 저장소 계정에 대한 키를 가져옵니다(클러스터를 만들기 위해 필요).
```azurecli-interactive
az storage account keys list -n <Storage Account Name>
```
---
아래의 Python 코드 조각은 2개의 헤드 노드 및 1개의 작업자 노드를 사용해서 Spark 클러스터를 만듭니다. 주석 설명에 따라 빈 변수를 채우고 특정 요구에 따라 다른 매개변수를 변경합니다.

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

### <a name="get-cluster-details"></a>클러스터 세부 정보 가져오기

지정된 클러스터에 대한 속성을 가져오려면:

```python
client.clusters.get("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a>예

`get`을(를) 사용하여 클러스터 만들기가 성공했는지 확인할 수 있습니다.

```python
my_cluster = client.clusters.get("<Resource Group Name>", "<Cluster Name>")
print(my_cluster)
```

출력은 다음과 같습니다.

```
{'additional_properties': {}, 'id': '/subscriptions/XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX/resourceGroups/<Resource Group Name>/providers/Microsoft.HDInsight/clusters/<Cluster Name>', 'name': '<Cluster Name>', 'type': 'Microsoft.HDInsight/clusters', 'location': '<Location>', 'tags': {}, 'etag': 'XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX', 'properties': <azure.mgmt.hdinsight.models.cluster_get_properties_py3.ClusterGetProperties object at 0x0000013766D68048>}
```

### <a name="list-clusters"></a>클러스터 나열

#### <a name="list-clusters-under-the-subscription"></a>구독 아래에 클러스터 나열

```python
client.clusters.list()
```
#### <a name="list-clusters-by-resource-group"></a>리소스 그룹별로 클러스터 나열

```python
client.clusters.list_by_resource_group("<Resource Group Name>")
```
> [!NOTE]
> `list()` 및 `list_by_resource_group()` 모두 `ClusterPaged` 개체를 반환합니다. `advance_page()`를 호출하면 해당 페이지의 클러스터 목록이 반환되고 `ClusterPaged` 개체가 다음 페이지로 이동합니다. `StopIteration` 예외가 제기될 때까지 반복할 수 있으며, 더 이상 페이지가 없음을 나타냅니다.

#### <a name="example"></a>예

다음 예제는 현재 구독에 대해 모든 클러스터 속성을 출력합니다.

```python
clusters_paged = client.clusters.list()
while True:
  try:
    for cluster in clusters_paged.advance_page():
      print(cluster)
  except StopIteration: 
    break
```

### <a name="delete-a-cluster"></a>클러스터 삭제

클러스터를 삭제하려면:

```python
client.clusters.delete("<Resource Group Name>", "<Cluster Name>")
```

### <a name="update-cluster-tags"></a>클러스터 태그 업데이트

지정된 클러스터의 태그를 다음과 같이 업데이트할 수 있습니다.

```python
client.clusters.update("<Resource Group Name>", "<Cluster Name>", tags={<Dictionary of Tags>})
```

#### <a name="example"></a>예

```python
client.clusters.update("<Resource Group Name>", "<Cluster Name>", tags={"tag1Name" : "tag1Value", "tag2Name" : "tag2Value"})
```

### <a name="resize-cluster"></a>클러스터 크기 조정

새 크기를 지정하여 작업자 노드의 지정된 클러스터 번호를 크기 조정할 수 있습니다.

```python
client.clusters.resize("<Resource Group Name>", "<Cluster Name>", target_instance_count=<Num of Worker Nodes>)
```

## <a name="cluster-monitoring"></a>클러스터 모니터링

또한 HDInsight 관리 SDK를 사용하여 OMS(Operations Management Suite)를 통해 클러스터에서 모니터링을 관리할 수 있습니다.

### <a name="enable-oms-monitoring"></a>OMS 모니터링 사용

> [!NOTE]
> OMS 모니터링을 사용하려면 기존 Log Analytics 작업 영역이 있어야 합니다. 아직 작업 영역을 만들지 않은 경우 다음에서 작업 영역을 만드는 방법을 알아볼 수 있습니다. [Azure Portal에서 Log Analytics 작업 영역 만들기](https://docs.microsoft.com/en-us/azure/log-analytics/log-analytics-quick-create-workspace).

클러스터에서 OMS 모니터링을 사용하려면:

```python
client.extension.enable_monitoring("<Resource Group Name>", "<Cluster Name>", workspace_id="<Workspace Id>")
```

### <a name="view-status-of-oms-monitoring"></a>OMS 모니터링의 상태 보기

클러스터에서 OMS 상태를 가져오려면:

```python
client.extension.get_monitoring_status("<Resource Group Name", "Cluster Name")
```

### <a name="disable-oms-monitoring"></a>OMS 모니터링 사용 안 함

클러스터에서 OMS를 사용하지 않으려면:

```python
client.extension.disable_monitoring("<Resource Group Name>", "<Cluster Name>")
```

## <a name="script-actions"></a>스크립트 동작

HDInsight는 클러스터 사용자 지정을 위해 사용자 지정 스크립트를 호출하는 스크립트 작업이라고 부르는 구성 메서드를 제공합니다.
> [!NOTE]
> 스크립트 작업을 사용하는 방법에 대한 자세한 내용은 다음에서 찾을 수 있습니다. [스크립트 작업을 사용하여 Linux 기반 HDInsight 클러스터 사용자 지정](https://docs.microsoft.com/en-us/azure/hdinsight/hdinsight-hadoop-customize-cluster-linux).

### <a name="execute-script-actions"></a>스크립트 작업 실행
지정된 클러스터에서 스크립트 작업을 실행하려면 다음을 수행합니다.

```python
script_action1 = RuntimeScriptAction(name="<Script Name>", uri="<URL To Script>", roles=[<List of Roles>]) #valid roles are "headnode", "workernode", "zookeepernode", and "edgenode"

client.clusters.execute_script_actions("<Resource Group Name>", "<Cluster Name>", <persist_on_success (bool)>, script_actions=[script_action1]) #add more RuntimeScriptActions to the list to execute multiple scripts
```

### <a name="delete-script-action"></a>스크립트 작업 삭제

지정된 클러스터에서 지정된 지속형 스크립트 작업을 삭제하려면:

```python
client.script_actions.delete("<Resource Group Name>", "<Cluster Name", "<Script Name>")
```

### <a name="list-persisted-script-actions"></a>지속형 스크립트 작업 나열

> [!NOTE]
> `list()` 및 `list_persisted_scripts()`는 `RuntimeScriptActionDetailPaged` 개체를 반환합니다. `advance_page()`를 호출하면 해당 페이지의 `RuntimeScriptActionDetail` 목록이 반환되고 `RuntimeScriptActionDetailPaged` 개체가 다음 페이지로 이동합니다. `StopIteration` 예외가 제기될 때까지 반복할 수 있으며, 더 이상 페이지가 없음을 나타냅니다. 아래 예제를 참조하세요.

지정된 클러스터에 대해 모든 지속형 스크립트 작업을 나열하려면:
```python
client.script_actions.list_persisted_scripts("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a>예

```python
scripts_paged = client.script_actions.list_persisted_scripts(resource_group_name, cluster_name)
while True:
  try:
    for script in scripts_paged.advance_page():
      print(script)
  except StopIteration:
    break
```

### <a name="list-all-scripts-execution-history"></a>모든 스크립트 실행 기록 나열

지정된 클러스터에 대해 모든 스크립트 실행 기록을 나열하려면:

```python
client.script_execution_history.list("<Resource Group Name>", "<Cluster Name>")
```

#### <a name="example"></a>예

이 예제는 모든 과거 스크립트 실행에 대한 모든 세부 정보를 출력합니다.

```python
script_executions_paged = client.script_execution_history.list("<Resource Group Name>", "<Cluster Name>")
while True:
  try:
    for script in script_executions_paged.advance_page():            
      print(script)
    except StopIteration:       
      break
```
