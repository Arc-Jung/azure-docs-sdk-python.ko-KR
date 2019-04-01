---
title: Python용 Azure Container Instances 라이브러리
description: Python용 Azure Container Instances 라이브러리에 대한 참조
keywords: Azure, python, SDK, API, ACI, 컨테이너, 인스턴스
author: mmacy
manager: jeconnoc
ms.date: 06/04/2018
ms.author: marsma
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: container-instances
ms.openlocfilehash: 95571e0da6ef82ef045d8c9ba0a5beb0abe9b63a
ms.sourcegitcommit: f439ba940d5940359c982015db7ccfb82f9dffd9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2018
ms.locfileid: "52273019"
---
# <a name="azure-container-instances-libraries-for-python"></a><span data-ttu-id="82dd7-104">Python용 Azure Container Instances 라이브러리</span><span class="sxs-lookup"><span data-stu-id="82dd7-104">Azure Container Instances libraries for Python</span></span>

<span data-ttu-id="82dd7-105">Python용 Microsoft Azure Container Instances 라이브러리를 사용하여 Azure Container Instances를 만들고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="82dd7-105">Use the Microsoft Azure Container Instances libraries for Python to create and manage Azure container instances.</span></span> <span data-ttu-id="82dd7-106">자세한 내용은 [Azure Container Instances 개요](/azure/container-instances/container-instances-overview)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="82dd7-106">Learn more by reading the [Azure Container Instances overview](/azure/container-instances/container-instances-overview).</span></span>

## <a name="management-apis"></a><span data-ttu-id="82dd7-107">관리 API</span><span class="sxs-lookup"><span data-stu-id="82dd7-107">Management APIs</span></span>

<span data-ttu-id="82dd7-108">Azure에서 관리 라이브러리를 사용하여 Azure Container Instances를 만들고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="82dd7-108">Use the management library to create and manage Azure container instances in Azure.</span></span>

<span data-ttu-id="82dd7-109">pip를 통해 관리 패키지를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="82dd7-109">Install the management package via pip:</span></span>

```bash
pip install azure-mgmt-containerinstance
```

## <a name="example-source"></a><span data-ttu-id="82dd7-110">예제 소스</span><span class="sxs-lookup"><span data-stu-id="82dd7-110">Example source</span></span>

<span data-ttu-id="82dd7-111">컨텍스트에서 다음 코드 예제를 보려는 경우, 다음 GitHub 리포지토리에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82dd7-111">If you'd like to see the following code examples in context, you can find them in the following GitHub repository:</span></span>

[<span data-ttu-id="82dd7-112">Azure-Samples/aci-docs-sample-python</span><span class="sxs-lookup"><span data-stu-id="82dd7-112">Azure-Samples/aci-docs-sample-python</span></span>](https://github.com/Azure-Samples/aci-docs-sample-python)

## <a name="authentication"></a><span data-ttu-id="82dd7-113">인증</span><span class="sxs-lookup"><span data-stu-id="82dd7-113">Authentication</span></span>

<span data-ttu-id="82dd7-114">SDK 클라이언트(예: 다음 예제의 Azure Container Instance 및 Resource Manager 클라이언트를 인증하는 가장 쉬운 방법)은 [파일 기반 인증](/python/azure/python-sdk-azure-authenticate#mgmt-auth-file)입니다.</span><span class="sxs-lookup"><span data-stu-id="82dd7-114">One of the easiest ways to authenticate SDK clients (like the Azure Container Instances and Resource Manager clients in the following example) is with [file-based authentication](/python/azure/python-sdk-azure-authenticate#mgmt-auth-file).</span></span> <span data-ttu-id="82dd7-115">파일 기반 인증은 `AZURE_AUTH_LOCATION`자격 증명 파일의 경로 환경 변수를 쿼리합니다.</span><span class="sxs-lookup"><span data-stu-id="82dd7-115">File-based authentication queries the `AZURE_AUTH_LOCATION` environment variable for the path to a credentials file.</span></span> <span data-ttu-id="82dd7-116">파일 기반 인증 사용:</span><span class="sxs-lookup"><span data-stu-id="82dd7-116">To use file-based authentication:</span></span>

1. <span data-ttu-id="82dd7-117">[Azure CLI](/cli/azure) 또는 [Cloud Shell](https://shell.azure.com/)로 자격 증명 파일 만들기:</span><span class="sxs-lookup"><span data-stu-id="82dd7-117">Create a credentials file with the [Azure CLI](/cli/azure) or [Cloud Shell](https://shell.azure.com/):</span></span>

   `az ad sp create-for-rbac --sdk-auth > my.azureauth`

   <span data-ttu-id="82dd7-118">[Cloud Shell](https://shell.azure.com/)을 사용하여 자격 증명 파일을 생성하려면 해당 내용을 Python 응용 프로그램이 액세스할 수 있는 로컬 파일에 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="82dd7-118">If you use the [Cloud Shell](https://shell.azure.com/) to generate the credentials file, copy its contents into a local file that your Python application can access.</span></span>

2. <span data-ttu-id="82dd7-119">`AZURE_AUTH_LOCATION` 환경 변수를 생성된 자격 증명 파일의 전체 경로로 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="82dd7-119">Set the `AZURE_AUTH_LOCATION` environment variable to the full path of the generated credentials file.</span></span> <span data-ttu-id="82dd7-120">예(Bash에서):</span><span class="sxs-lookup"><span data-stu-id="82dd7-120">For example (in Bash):</span></span>

   ```bash
   export AZURE_AUTH_LOCATION=/home/yourusername/my.azureauth
   ```

<span data-ttu-id="82dd7-121">자격 증명 파일을 만들고 `AZURE_AUTH_LOCATION` 환경 변수를 채웠다면, [client_factory] [ client_factory] 모듈의 `get_client_from_auth_file` 메서드를 사용하여 [ResourceManagementClient] [ ResourceManagementClient] 및 [ContainerInstanceManagementClient] [ ContainerInstanceManagementClient] 개체를 초기화합니다.</span><span class="sxs-lookup"><span data-stu-id="82dd7-121">Once you've created the credentials file and populated the `AZURE_AUTH_LOCATION` environment variable, use the `get_client_from_auth_file` method of the [client_factory][client_factory] module to initialize the [ResourceManagementClient][ResourceManagementClient] and [ContainerInstanceManagementClient][ContainerInstanceManagementClient] objects.</span></span>

<span data-ttu-id="82dd7-122"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python --> [!code-python[authenticate](~/aci-docs-sample-python/src/aci_docs_sample.py#L45-L58 "Authenticate ACI and Resource Manager clients")]</span><span class="sxs-lookup"><span data-stu-id="82dd7-122"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python --> [!code-python[authenticate](~/aci-docs-sample-python/src/aci_docs_sample.py#L45-L58 "Authenticate ACI and Resource Manager clients")]</span></span>

<span data-ttu-id="82dd7-123">Python용 Azure 관리 라이브러리에 사용가능한 인증 방법에 대한 자세한 내용은 [Python용 Azure 관리 라이브러리로 인증하기](/python/azure/python-sdk-azure-authenticate)를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="82dd7-123">For more details about the available authentication methods in the Python management libraries for Azure, see [Authenticate with the Azure Management Libraries for Python](/python/azure/python-sdk-azure-authenticate).</span></span>

## <a name="create-container-group---single-container"></a><span data-ttu-id="82dd7-124">컨테이너 그룹 만들기 - 단일 컨테이너</span><span class="sxs-lookup"><span data-stu-id="82dd7-124">Create container group - single container</span></span>

<span data-ttu-id="82dd7-125">이 예에서는 단일 컨테이너로 컨테이너 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="82dd7-125">This example creates a container group with a single container</span></span>

<span data-ttu-id="82dd7-126"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python --> [!code-python[create_container_group](~/aci-docs-sample-python/src/aci_docs_sample.py#L94-L140 "Create single-container group")]</span><span class="sxs-lookup"><span data-stu-id="82dd7-126"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python --> [!code-python[create_container_group](~/aci-docs-sample-python/src/aci_docs_sample.py#L94-L140 "Create single-container group")]</span></span>

## <a name="create-container-group---multiple-containers"></a><span data-ttu-id="82dd7-127">컨테이너 그룹 만들기 - 여러 컨테이너</span><span class="sxs-lookup"><span data-stu-id="82dd7-127">Create container group - multiple containers</span></span>

<span data-ttu-id="82dd7-128">이 예에서는 애플리케이션 컨테이너와 사이드카 컨테이너라는 두 개의 컨테이너로 컨테이너 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="82dd7-128">This example creates a container group with two containers: an application container and a sidecar container.</span></span>

<span data-ttu-id="82dd7-129"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python --> [!code-python[create_container_group_multi](~/aci-docs-sample-python/src/aci_docs_sample.py#L143-L196 "Create multi-container group")]</span><span class="sxs-lookup"><span data-stu-id="82dd7-129"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python --> [!code-python[create_container_group_multi](~/aci-docs-sample-python/src/aci_docs_sample.py#L143-L196 "Create multi-container group")]</span></span>

## <a name="create-task-based-container-group"></a><span data-ttu-id="82dd7-130">작업 기반 컨테이너 그룹 만들기</span><span class="sxs-lookup"><span data-stu-id="82dd7-130">Create task-based container group</span></span>

<span data-ttu-id="82dd7-131">이 예에서는 단일 작업 기반 컨테이너로 컨테이너 그룹을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="82dd7-131">This example creates a container group with a single task-based container.</span></span> <span data-ttu-id="82dd7-132">이 예제에서는 몇 가지 기능을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="82dd7-132">This example demonstrates several features:</span></span>

* <span data-ttu-id="82dd7-133">[명령줄 재정의](/azure/container-instances/container-instances-restart-policy#command-line-override) - 컨테이너의 Dockerfile `CMD` 줄에 지정된 것과 다른 사용자 지정 명령줄이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="82dd7-133">[Command line override](/azure/container-instances/container-instances-restart-policy#command-line-override) - A custom command line, different from that which is specified in the container's Dockerfile `CMD` line, is specified.</span></span> <span data-ttu-id="82dd7-134">명령줄 재정의를 사용하면 컨테이너 시작 시 실행 하는 사용자 지정 명령줄을 지정할 수 있으며, 이는 컨테이너에 내장된 기본 명령줄을 재정의합니다.</span><span class="sxs-lookup"><span data-stu-id="82dd7-134">Command line override allows you to specify a custom command line to execute at container startup, overriding the default command line baked-in to the container.</span></span> <span data-ttu-id="82dd7-135">컨테이너 시작 시 여러 명령을 실행하는 것과 관련하여 다음이 적용됩니다.</span><span class="sxs-lookup"><span data-stu-id="82dd7-135">Regarding executing multiple commands at container startup, the following applies:</span></span>

   <span data-ttu-id="82dd7-136">`echo FOO BAR`에서와 같이 여러 명령줄 인수를 사용하여 **단일 명령**을 실행하려면 이들 인수를 문자열 배열로서 [ 컨테이너][Container]의 `command`속성에 제공해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="82dd7-136">If you want to run a **single command** with several command-line arguments, for example `echo FOO BAR`, you must supply them as a string list to the `command` property of the [Container][Container].</span></span> <span data-ttu-id="82dd7-137">예를 들면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="82dd7-137">For example:</span></span>

   `command = ['echo', 'FOO', 'BAR']`

   <span data-ttu-id="82dd7-138">그러나 (잠재적으로) 여러 인수를 사용하여 **여러 명령**을 실행하려는 경우, 셸을 실행하고 연결된 명령을 인수로서 전달해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="82dd7-138">If, however, you want to run **multiple commands** with (potentially) multiple arguments, you must execute a shell and pass the chained commands as an argument.</span></span> <span data-ttu-id="82dd7-139">예를 들어,이는 `echo` 및 `tail` 명령을 모두 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="82dd7-139">For example, this executes both an `echo` and a `tail` command:</span></span>

   `command = ['/bin/sh', '-c', 'echo FOO BAR && tail -f /dev/null']`
* <span data-ttu-id="82dd7-140">[환경 변수](/azure/container-instances/container-instances-environment-variables) - 두 환경 변수가 컨테이너 그룹의 컨테이너에 대해 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="82dd7-140">[Environment variables](/azure/container-instances/container-instances-environment-variables) - Two environment variables are specified for the container in the container group.</span></span> <span data-ttu-id="82dd7-141">환경 변수를 사용 하여 런타임 시 스크립트 또는 애플리케이션 동작을 수정하거나, 컨테이너에서 실행 중인 애플리케이션에 동적 정보를 전달 합니다.</span><span class="sxs-lookup"><span data-stu-id="82dd7-141">Use environment variables to modify script or application behavior at runtime, or otherwise pass dynamic information to an application running in the container.</span></span>
* <span data-ttu-id="82dd7-142">[정책 다시 시작](/azure/container-instances/container-instances-restart-policy) - 해당 컨테이너는 "Never" 재시작 정책을 사용하여 구성되었으며, 이는 일괄 처리 작업의 일부로 실행되는 작업 기반 컨테이너에 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="82dd7-142">[Restart policy](/azure/container-instances/container-instances-restart-policy) - The container is configured with a restart policy of "Never," useful for task-based containers that are executed as part of a batch job.</span></span>
* <span data-ttu-id="82dd7-143">[AzureOperationPoller] [ AzureOperationPoller]로 폴링하여 작업 - create 메서드가 호출된 후, 작업이 완료되고 컨테이너 그룹 로그를 얻을 수 있는 시기를 결정하기 위해 작업이 폴링됩니다.</span><span class="sxs-lookup"><span data-stu-id="82dd7-143">Operation polling with [AzureOperationPoller][AzureOperationPoller] - After the create method is invoked, the operation is polled to determine when it has completed and the container group's logs can be obtained.</span></span>

<span data-ttu-id="82dd7-144"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python --> [!code-python[create_container_group_task](~/aci-docs-sample-python/src/aci_docs_sample.py#L199-L275 "Run a task-based container")]</span><span class="sxs-lookup"><span data-stu-id="82dd7-144"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python --> [!code-python[create_container_group_task](~/aci-docs-sample-python/src/aci_docs_sample.py#L199-L275 "Run a task-based container")]</span></span>

## <a name="list-container-groups"></a><span data-ttu-id="82dd7-145">컨테이너 그룹 나열</span><span class="sxs-lookup"><span data-stu-id="82dd7-145">List container groups</span></span>

<span data-ttu-id="82dd7-146">이 예에서는 리소스 그룹의 컨테이너 그룹을 나열 한 다음 해당 속성 중 일부를 출력합니다.</span><span class="sxs-lookup"><span data-stu-id="82dd7-146">This example lists the container groups in a resource group and then prints a few of their properties.</span></span>

<span data-ttu-id="82dd7-147">컨테이너 그룹을 나열하는 경우 반환된 각 그룹의 [instance_view] [ instance_view]는 `None`입니다.</span><span class="sxs-lookup"><span data-stu-id="82dd7-147">When you list container groups,the [instance_view][instance_view] of each returned group is `None`.</span></span> <span data-ttu-id="82dd7-148">컨테이너 그룹에 있는 컨테이너의 세부 정보를 얻으려면, [get] [ containergroupoperations_get] 컨테이너 그룹을 실행해야 하며 이때 `instance_view`속성이 채워진 그룹이 반환됩니다.</span><span class="sxs-lookup"><span data-stu-id="82dd7-148">To get the details of the containers within a container group, you must then [get][containergroupoperations_get] the container group, which returns the group with its `instance_view` property populated.</span></span> <span data-ttu-id="82dd7-149">다음 섹션을 참조 [기존 컨테이너 그룹 가져오기](#get-an-existing-container-group), 컨테이너 그룹의 컨테이너 `instance_view`에서 반복하기의 예제를 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82dd7-149">See the next section, [Get an existing container group](#get-an-existing-container-group), for an example of iterating over a container group's containers in its `instance_view`.</span></span>

<span data-ttu-id="82dd7-150"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python --> [!code-python[list_container_groups](~/aci-docs-sample-python/src/aci_docs_sample.py#L278-L292 "List container groups")]</span><span class="sxs-lookup"><span data-stu-id="82dd7-150"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python --> [!code-python[list_container_groups](~/aci-docs-sample-python/src/aci_docs_sample.py#L278-L292 "List container groups")]</span></span>

## <a name="get-an-existing-container-group"></a><span data-ttu-id="82dd7-151">기존 컨테이너 그룹 가져오기</span><span class="sxs-lookup"><span data-stu-id="82dd7-151">Get an existing container group</span></span>

<span data-ttu-id="82dd7-152">이 예에서는 리소스 그룹에 있는 특정 컨테이너 그룹을 가져와서 몇 가지 속성(해당 컨테이너 포함)과 그 값을 인쇄합니다.</span><span class="sxs-lookup"><span data-stu-id="82dd7-152">This example gets a specific container group from a resource group, and then prints a few of its properties (including its containers) and their values.</span></span>

<span data-ttu-id="82dd7-153">[가져오기 작업] [ containergroupoperations_get]은 해당 [instance_view] [ instance_view]가 채워진 컨테이너 그룹을 반환합니다. 이때 각 그룹의 컨테이너에서 반복을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82dd7-153">The [get operation][containergroupoperations_get] returns a container group with its [instance_view][instance_view] populated, which allows you to iterate over each container in the group.</span></span> <span data-ttu-id="82dd7-154"> `get` 작업만이 컨테이너 그룹의 `instance_vew` 속성을 채웁니다 --구독 또는 리소스 그룹에 컨테이너 그룹을 나열하면 작업의 잠재적으로 비용이 많이 드는 특성으로 인해 인스턴스 보기가 채워지지 않습니다(예: 각각 잠재적으로 여러 컨테이너를 포함하는 수백 개의 컨테이너 그룹을 나열할 때).</span><span class="sxs-lookup"><span data-stu-id="82dd7-154">Only the `get` operation populates the `instance_vew` property of the container group--listing the container groups in a subscription or resource group doesn't populate the instance view due to the potentially expensive nature of the operation (for example, when listing hundreds of container groups, each potentially containing multiple containers).</span></span> <span data-ttu-id="82dd7-155">[컨테이너 그룹 목록](#list-container-groups)섹션에 설명한 것처럼, `list` 이후, `get`컨테이너 인스턴스 세부 정보를 얻기 위해 특정 컨테이너 그룹을 지정해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="82dd7-155">As mentioned previously in the [List container groups](#list-container-groups) section, after a `list`, you must subsequently `get` a specific container group to obtain its container instance details.</span></span>

<span data-ttu-id="82dd7-156"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python --> [!code-python[get_container_group](~/aci-docs-sample-python/src/aci_docs_sample.py#L295-L324 "Get container group")]</span><span class="sxs-lookup"><span data-stu-id="82dd7-156"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python --> [!code-python[get_container_group](~/aci-docs-sample-python/src/aci_docs_sample.py#L295-L324 "Get container group")]</span></span>

## <a name="delete-a-container-group"></a><span data-ttu-id="82dd7-157">컨테이너 그룹 삭제</span><span class="sxs-lookup"><span data-stu-id="82dd7-157">Delete a container group</span></span>

<span data-ttu-id="82dd7-158">이 예에서는 리소스 그룹 및 리소스 그룹의 몇몇 컨테이너 그룹을 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="82dd7-158">This example deletes several container groups from a resource group, as well as the resource group.</span></span>

<span data-ttu-id="82dd7-159"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python --> [!code-python[delete_container_group](~/aci-docs-sample-python/src/aci_docs_sample.py#L83-L91 "Delete container groups and resource group")]</span><span class="sxs-lookup"><span data-stu-id="82dd7-159"><!-- SOURCE REPO: https://github.com/Azure-Samples/aci-docs-sample-python --> [!code-python[delete_container_group](~/aci-docs-sample-python/src/aci_docs_sample.py#L83-L91 "Delete container groups and resource group")]</span></span>

## <a name="next-steps"></a><span data-ttu-id="82dd7-160">다음 단계</span><span class="sxs-lookup"><span data-stu-id="82dd7-160">Next steps</span></span>

* <span data-ttu-id="82dd7-161">앞의 예에 대한 소스 코드는 GitHub에서 찾을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="82dd7-161">The source code for the preceding examples can be found on GitHub:</span></span>

  <span data-ttu-id="82dd7-162">[Azure-Samples/aci-docs-sample-python][aci-docs-sample-python]</span><span class="sxs-lookup"><span data-stu-id="82dd7-162">[Azure-Samples/aci-docs-sample-python][aci-docs-sample-python]</span></span>

* <span data-ttu-id="82dd7-163">더 많은 Azure Container Instances 코드 샘플:</span><span class="sxs-lookup"><span data-stu-id="82dd7-163">More Azure Container Instances code samples:</span></span>

  <span data-ttu-id="82dd7-164">[Azure 코드 샘플][samples-aci]</span><span class="sxs-lookup"><span data-stu-id="82dd7-164">[Azure Code Samples][samples-aci]</span></span>

* <span data-ttu-id="82dd7-165">앱에서 사용할 수 있는 [Python 샘플 코드][samples-python]를 추가로 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="82dd7-165">Explore more [sample Python code][samples-python] you can use in your apps.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="82dd7-166">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="82dd7-166">Explore the management APIs</span></span>](/python/api/overview/azure/containerinstance/management)

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