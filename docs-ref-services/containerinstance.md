---
title: Python용 Azure Container Instances 라이브러리
description: Python용 Azure Container Instances 라이브러리에 대한 참조
keywords: Azure, python, SDK, API, ACI, 컨테이너, 인스턴스
author: dlepow
manager: jeconnoc
ms.date: 04/15/2019
ms.author: danlep
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: container-instances
ms.openlocfilehash: 88df9443efb98bc5cec26c5eb4b01a4956141d40
ms.sourcegitcommit: 1b45953f168cbf36869c24c1741d70153b88b9fc
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/17/2019
ms.locfileid: "59675938"
---
# <a name="azure-container-instances-libraries-for-python"></a>Python용 Azure Container Instances 라이브러리

Python용 Microsoft Azure Container Instances 라이브러리를 사용하여 Azure Container Instances를 만들고 관리합니다. 자세한 내용은 [Azure Container Instances 개요](/azure/container-instances/container-instances-overview)를 참조하세요.

## <a name="management-apis"></a>관리 API

Azure에서 관리 라이브러리를 사용하여 Azure Container Instances를 만들고 관리합니다.

pip를 통해 관리 패키지를 설치합니다.

```bash
pip install azure-mgmt-containerinstance
```

## <a name="example-source"></a>예제 소스

컨텍스트에서 다음 코드 예제를 보려는 경우, 다음 GitHub 리포지토리에서 찾을 수 있습니다.

[Azure-Samples/aci-docs-sample-python](https://github.com/Azure-Samples/aci-docs-sample-python)

## <a name="authentication"></a>Authentication

SDK 클라이언트(예: 다음 예제의 Azure Container Instance 및 Resource Manager 클라이언트를 인증하는 가장 쉬운 방법)은 [파일 기반 인증](/python/azure/python-sdk-azure-authenticate#mgmt-auth-file)입니다. 파일 기반 인증은 `AZURE_AUTH_LOCATION`자격 증명 파일의 경로 환경 변수를 쿼리합니다. 파일 기반 인증 사용:

1. [Azure CLI](/cli/azure) 또는 [Cloud Shell](https://shell.azure.com/)로 자격 증명 파일 만들기:

   `az ad sp create-for-rbac --sdk-auth > my.azureauth`

   [Cloud Shell](https://shell.azure.com/)을 사용하여 자격 증명 파일을 생성하려면 해당 내용을 Python 애플리케이션이 액세스할 수 있는 로컬 파일에 복사합니다.

2. `AZURE_AUTH_LOCATION` 환경 변수를 생성된 자격 증명 파일의 전체 경로로 설정합니다. 예(Bash에서):

   ```bash
   export AZURE_AUTH_LOCATION=/home/yourusername/my.azureauth
   ```

자격 증명 파일을 만들고 `AZURE_AUTH_LOCATION` 환경 변수를 채웠다면, [client_factory] [ client_factory] 모듈의 `get_client_from_auth_file` 메서드를 사용하여 [ResourceManagementClient] [ ResourceManagementClient] 및 [ContainerInstanceManagementClient] [ ContainerInstanceManagementClient] 개체를 초기화합니다.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[authenticate](~/aci-docs-sample-python/src/aci_docs_sample.py#L45-L58 "Authenticate ACI and Resource Manager clients")]

Python용 Azure 관리 라이브러리에 사용가능한 인증 방법에 대한 자세한 내용은 [Python용 Azure 관리 라이브러리로 인증하기](/python/azure/python-sdk-azure-authenticate)를 참조합니다.

## <a name="create-container-group---single-container"></a>컨테이너 그룹 만들기 - 단일 컨테이너

이 예에서는 단일 컨테이너로 컨테이너 그룹을 만듭니다.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[create_container_group](~/aci-docs-sample-python/src/aci_docs_sample.py#L94-L141 "Create single-container group")]

## <a name="create-container-group---multiple-containers"></a>컨테이너 그룹 만들기 - 여러 컨테이너

이 예에서는 애플리케이션 컨테이너와 사이드카 컨테이너라는 두 개의 컨테이너로 컨테이너 그룹을 만듭니다.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[create_container_group_multi](~/aci-docs-sample-python/src/aci_docs_sample.py#L144-L197 "Create multi-container group")]

## <a name="create-task-based-container-group"></a>작업 기반 컨테이너 그룹 만들기

이 예에서는 단일 작업 기반 컨테이너로 컨테이너 그룹을 만듭니다. 이 예제에서는 몇 가지 기능을 보여 줍니다.

* [명령줄 재정의](/azure/container-instances/container-instances-restart-policy#command-line-override) - 컨테이너의 Dockerfile `CMD` 줄에 지정된 것과 다른 사용자 지정 명령줄이 지정됩니다. 명령줄 재정의를 사용하면 컨테이너 시작 시 실행 하는 사용자 지정 명령줄을 지정할 수 있으며, 이는 컨테이너에 내장된 기본 명령줄을 재정의합니다. 컨테이너 시작 시 여러 명령을 실행하는 것과 관련하여 다음이 적용됩니다.

   `echo FOO BAR`에서와 같이 여러 명령줄 인수를 사용하여 **단일 명령**을 실행하려면 이들 인수를 문자열 배열로서 [ 컨테이너][Container]의 `command`속성에 제공해야 합니다. 예: 

   `command = ['echo', 'FOO', 'BAR']`

   그러나 (잠재적으로) 여러 인수를 사용하여 **여러 명령**을 실행하려는 경우, 셸을 실행하고 연결된 명령을 인수로서 전달해야 합니다. 예를 들어,이는 `echo` 및 `tail` 명령을 모두 실행합니다.

   `command = ['/bin/sh', '-c', 'echo FOO BAR && tail -f /dev/null']`
* [환경 변수](/azure/container-instances/container-instances-environment-variables) - 두 환경 변수가 컨테이너 그룹의 컨테이너에 대해 지정됩니다. 환경 변수를 사용 하여 런타임 시 스크립트 또는 애플리케이션 동작을 수정하거나, 컨테이너에서 실행 중인 애플리케이션에 동적 정보를 전달 합니다.
* [정책 다시 시작](/azure/container-instances/container-instances-restart-policy) - 해당 컨테이너는 "Never" 재시작 정책을 사용하여 구성되었으며, 이는 일괄 처리 작업의 일부로 실행되는 작업 기반 컨테이너에 유용합니다.
* [AzureOperationPoller] [ AzureOperationPoller]로 폴링하여 작업 - create 메서드가 호출된 후, 작업이 완료되고 컨테이너 그룹 로그를 얻을 수 있는 시기를 결정하기 위해 작업이 폴링됩니다.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[create_container_group_task](~/aci-docs-sample-python/src/aci_docs_sample.py#L200-L276 "Run a task-based container")]

## <a name="list-container-groups"></a>컨테이너 그룹 나열

이 예에서는 리소스 그룹의 컨테이너 그룹을 나열 한 다음 해당 속성 중 일부를 출력합니다.

컨테이너 그룹을 나열하는 경우 반환된 각 그룹의 [instance_view] [ instance_view]는 `None`입니다. 컨테이너 그룹에 있는 컨테이너의 세부 정보를 얻으려면, [get] [ containergroupoperations_get] 컨테이너 그룹을 실행해야 하며 이때 `instance_view`속성이 채워진 그룹이 반환됩니다. 다음 섹션을 참조 [기존 컨테이너 그룹 가져오기](#get-an-existing-container-group), 컨테이너 그룹의 컨테이너 `instance_view`에서 반복하기의 예제를 볼 수 있습니다.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[list_container_groups](~/aci-docs-sample-python/src/aci_docs_sample.py#L279-L293 "List container groups")]

## <a name="get-an-existing-container-group"></a>기존 컨테이너 그룹 가져오기

이 예에서는 리소스 그룹에 있는 특정 컨테이너 그룹을 가져와서 몇 가지 속성(해당 컨테이너 포함)과 그 값을 인쇄합니다.

[가져오기 작업] [ containergroupoperations_get]은 해당 [instance_view] [ instance_view]가 채워진 컨테이너 그룹을 반환합니다. 이때 각 그룹의 컨테이너에서 반복을 수행할 수 있습니다.  `get` 작업만이 컨테이너 그룹의 `instance_vew` 속성을 채웁니다 --구독 또는 리소스 그룹에 컨테이너 그룹을 나열하면 작업의 잠재적으로 비용이 많이 드는 특성으로 인해 인스턴스 보기가 채워지지 않습니다(예: 각각 잠재적으로 여러 컨테이너를 포함하는 수백 개의 컨테이너 그룹을 나열할 때). [컨테이너 그룹 목록](#list-container-groups)섹션에 설명한 것처럼, `list` 이후, `get`컨테이너 인스턴스 세부 정보를 얻기 위해 특정 컨테이너 그룹을 지정해야 합니다.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[get_container_group](~/aci-docs-sample-python/src/aci_docs_sample.py#L296-L325 "Get container group")]

## <a name="delete-a-container-group"></a>컨테이너 그룹 삭제

이 예에서는 리소스 그룹 및 리소스 그룹의 몇몇 컨테이너 그룹을 삭제합니다.

<!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python -->
[!code-python[delete_container_group](~/aci-docs-sample-python/src/aci_docs_sample.py#L83-L91 "Delete container groups and resource group")]

## <a name="next-steps"></a>다음 단계

* 앞의 예에 대한 소스 코드는 GitHub에서 찾을 수 있습니다.

  [Azure-Samples/aci-docs-sample-python][aci-docs-sample-python]

* 더 많은 Azure Container Instances 코드 샘플:

  [Azure 코드 샘플][samples-aci]

* 앱에서 사용할 수 있는 [Python 샘플 코드][samples-python]를 추가로 탐색합니다.

> [!div class="nextstepaction"]
> [관리 API 탐색](/python/api/overview/azure/containerinstance/management)

<!-- LINKS - External -->
[aci-docs-sample-python]: https://github.com/Azure-Samples/aci-docs-sample-python
[samples-aci]: https://azure.microsoft.com/resources/samples/?sort=0&term=ACI
[samples-python]: https://azure.microsoft.com/resources/samples/?platform=python

<!-- TYPES -->
[AzureOperationPoller]: /python/api/msrestazure.azure_operation.AzureOperationPoller
[client_factory]: /python/api/azure.common.client_factory
[Container]: /python/api/azure.mgmt.containerinstance.models.container
[ContainerGroupInstanceView]: /python/api/azure.mgmt.containerinstance.models.containergrouppropertiesinstanceview
[containergroupoperations_get]: /python/api/azure.mgmt.containerinstance.operations.containergroupsoperations#get
[ContainerInstanceManagementClient]: /python/api/azure.mgmt.containerinstance.containerinstancemanagementclient
[instance_view]: /python/api/azure.mgmt.containerinstance.models.containergroup#variables
[ResourceManagementClient]: /python/api/azure.mgmt.resource.resources.resourcemanagementclient