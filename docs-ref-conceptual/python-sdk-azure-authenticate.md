---
title: Python용 Azure 관리 라이브러리를 사용하여 인증
description: Python용 Azure 관리 라이브러리에 서비스 사용자를 인증합니다.
keywords: Azure, Python, SDK, API, 인증, Active Directory, 서비스 사용자
author: sptramer
ms.author: sttramer
manager: carmonm
ms.date: 04/11/2019
ms.topic: article
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 51f26b120cefffd2d7f4af9c2b6b2cb532bc6006
ms.sourcegitcommit: 375a1f9180eb1323fe2af0a7e28fd4676973c68e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2019
ms.locfileid: "59586811"
---
# <a name="authenticate-with-the-azure-management-libraries-for-python"></a><span data-ttu-id="356b3-104">Python용 Azure 관리 라이브러리를 사용하여 인증</span><span class="sxs-lookup"><span data-stu-id="356b3-104">Authenticate with the Azure Management Libraries for Python</span></span>

<span data-ttu-id="356b3-105">Python 관리 라이브러리를 사용하여 리소스를 만들고 관리할 때 Azure를 통해 애플리케이션을 인증하는 데 사용할 수 있는 몇 가지 옵션이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="356b3-105">Several options are available to authenticate your application with Azure when using the Python management libraries to create and manage resources.</span></span>

## <a name="mgmt-auth-token"></a><span data-ttu-id="356b3-106">토큰 자격 증명을 사용하여 인증</span><span class="sxs-lookup"><span data-stu-id="356b3-106">Authenticate with token credentials</span></span>

<span data-ttu-id="356b3-107">구성 파일, 레지스트리 또는 Azure Key Vault에 자격 증명을 안전하게 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="356b3-107">Store the credentials securely in a configuration file, the registry, or Azure KeyVault.</span></span>

<span data-ttu-id="356b3-108">다음 예제에서는 [서비스 사용자](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json)를 사용하여 인증합니다.</span><span class="sxs-lookup"><span data-stu-id="356b3-108">The following example uses a [Service Principal](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli?toc=%2fazure%2fazure-resource-manager%2ftoc.json) for authentication.</span></span>

> [!NOTE]
> <span data-ttu-id="356b3-109">Azure CLI로 서비스 사용자를 만들려면 다음 명령을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="356b3-109">To create a service principal with the Azure CLI, use the following command:</span></span>
>
> ```bash
> az ad sp create-for-rbac --name "MY-PRINCIPAL-NAME" --password "STRONG-SECRET-PASSWORD"
> ```
>
> <span data-ttu-id="356b3-110">CLI로 서비스 사용자를 설정하는 방법을 자세히 알아보려면 [Azure CLI를 사용하여 Azure 서비스 사용자 만들기](/cli/azure/create-an-azure-service-principal-azure-cli)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="356b3-110">To learn more about setting up service princpals with the CLI, see [Create an Azure service principal with Azure CLI](/cli/azure/create-an-azure-service-principal-azure-cli)</span></span>

```python
from azure.common.credentials import ServicePrincipalCredentials

# Tenant ID for your Azure subscription
TENANT_ID = '<Your tenant ID>'

# Your service principal App ID
CLIENT = '<Your service principal ID>'

# Your service principal password
KEY = '<Your service principal password>'

credentials = ServicePrincipalCredentials(
    client_id = CLIENT,
    secret = KEY,
    tenant = TENANT_ID
)
```

> <span data-ttu-id="356b3-111">[참고!] 다른 지역의 Azure 클라우드에 연결하려면 `cloud_environment` 매개 변수를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="356b3-111">[NOTE!] To connect to one of the Azure sovereign clouds, use the `cloud_environment` parameter.</span></span>
>
> ```python
> from azure.common.credentials import ServicePrincipalCredentials
> from msrestazure.azure_cloud import AZURE_CHINA_CLOUD
> 
> # Tenant ID for your Azure Subscription
> TENANT_ID = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'
> 
> # Your Service Principal App ID
> CLIENT = 'a2ab11af-01aa-4759-8345-7803287dbd39'
> 
> # Your Service Principal Password
> KEY = 'password'
> 
> credentials = ServicePrincipalCredentials(
>     client_id = CLIENT,
>     secret = KEY,
>     tenant = TENANT_ID,
>     cloud_environment = AZURE_CHINA_CLOUD
> )
> ```

<span data-ttu-id="356b3-112">더 많은 제어가 필요하면 [ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-python) 및 SDK ADAL 래퍼를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="356b3-112">If you need more control, it is recommended to use [ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-python) and the SDK ADAL wrapper.</span></span> <span data-ttu-id="356b3-113">사용 가능한 모든 시나리오 목록과 샘플은 ADAL 웹 사이트를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="356b3-113">Please refer to the ADAL website for all the available scenarios list and samples.</span></span> <span data-ttu-id="356b3-114">예를 들어 서비스 사용자 인증의 경우 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="356b3-114">For instance for service principal authentication:</span></span>

```python
import adal
from msrestazure.azure_active_directory import AdalAuthentication
from msrestazure.azure_cloud import AZURE_PUBLIC_CLOUD

# Tenant ID for your Azure Subscription
TENANT_ID = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'

# Your Service Principal App ID
CLIENT = 'a2ab11af-01aa-4759-8345-7803287dbd39'

# Your Service Principal Password
KEY = 'password'

LOGIN_ENDPOINT = AZURE_PUBLIC_CLOUD.endpoints.active_directory
RESOURCE = AZURE_PUBLIC_CLOUD.endpoints.active_directory_resource_id

context = adal.AuthenticationContext(LOGIN_ENDPOINT + '/' + TENANT_ID)
credentials = AdalAuthentication(
    context.acquire_token_with_client_credentials,
    RESOURCE,
    CLIENT,
    KEY
)
```

<span data-ttu-id="356b3-115">유효한 모든 ADAL 호출은 `AdalAuthentication` 클래스에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="356b3-115">All ADAL valid calls can be used with the `AdalAuthentication` class.</span></span>

<span data-ttu-id="356b3-116">다음으로 클라이언트 개체를 만들어 API 작업을 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="356b3-116">Next, create a client object to start working with the API:</span></span>

```python
from azure.mgmt.compute import ComputeManagementClient

# Your Azure Subscription ID
subscription_id = '33333333-3333-3333-3333-333333333333'

client = ComputeManagementClient(credentials, subscription_id)
```

> <span data-ttu-id="356b3-117">[참고!] 다른 지역의 Azure 클라우드를 사용하는 경우 관리 클라이언트를 만들 때 지역에 맞는 기본 URL도 지정해야 합니다(`msrestazure.azure_cloud`의 상수를 통해).</span><span class="sxs-lookup"><span data-stu-id="356b3-117">[NOTE!] When using an Azure sovereign cloud you must also specify the appropriate base URL (via the constants in `msrestazure.azure_cloud`) when creating the management client.</span></span> <span data-ttu-id="356b3-118">예를 들어 Azure 중국 클라우드의 경우 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="356b3-118">For example for Azure China Cloud:</span></span>
> ```python
> client = ComputeManagementClient(credentials, subscription_id,
>     base_url=AZURE_CHINA_CLOUD.endpoints.resource_manager)
> ```


## <a name="mgmt-auth-file"></a><span data-ttu-id="356b3-119">파일 기반 인증</span><span class="sxs-lookup"><span data-stu-id="356b3-119">File based authentication</span></span>

<span data-ttu-id="356b3-120">가장 간단한 인증 방법은 Azure 서비스 사용자에 대한 자격 증명을 포함하는 JSON 파일을 만드는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="356b3-120">The simplest way to authenticate is to create a JSON file that contains credentials for an Azure Service Principal.</span></span> <span data-ttu-id="356b3-121">다음 CLI 명령을 사용하여 새 서비스 사용자와 JSON 파일을 동시에 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="356b3-121">You can use the following CLI command to create a new Service Principal and this file at the same time:</span></span>

```bash
az ad sp create-for-rbac --sdk-auth > mycredentials.json
```

<span data-ttu-id="356b3-122">코드에서 읽을 수 있는 시스템의 안전한 위치에 JSON 파일을 저장합니다.</span><span class="sxs-lookup"><span data-stu-id="356b3-122">Save this file in a secure location on your system where your code can read it.</span></span> <span data-ttu-id="356b3-123">셸에서 이 파일의 전체 경로가 포함된 환경 변수를 설정합니다.</span><span class="sxs-lookup"><span data-stu-id="356b3-123">Set an environment variable with the full path to the file in your shell:</span></span>

```bash
export AZURE_AUTH_LOCATION=~/.azure/azure_credentials.json
```

<span data-ttu-id="356b3-124">JSON 파일을 직접 만들려면 다음 형식을 따르십시오.</span><span class="sxs-lookup"><span data-stu-id="356b3-124">If you want to create the file yourself, please follow this format:</span></span>

```json
{
    "clientId": "<Service principal ID>",
    "clientSecret": "<Service principal secret/password>",
    "subscriptionId": "<Subscription associated with the service principal>",
    "tenantId": "<The service principal's tenant>",
    "activeDirectoryEndpointUrl": "https://login.microsoftonline.com",
    "resourceManagerEndpointUrl": "https://management.azure.com/",
    "activeDirectoryGraphResourceId": "https://graph.windows.net/",
    "sqlManagementEndpointUrl": "https://management.core.windows.net:8443/",
    "galleryEndpointUrl": "https://gallery.azure.com/",
    "managementEndpointUrl": "https://management.core.windows.net/"
}
```

<span data-ttu-id="356b3-125">그런 다음 클라이언트 팩터리를 사용하여 클라이언트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="356b3-125">You can then create any client using the client factory:</span></span>

```python
from azure.common.client_factory import get_client_from_auth_file
from azure.mgmt.compute import ComputeManagementClient

client = get_client_from_auth_file(ComputeManagementClient)
```

## <a name="mgmt-auth-msi"></a><span data-ttu-id="356b3-126">Azure 관리 ID로 인증</span><span class="sxs-lookup"><span data-stu-id="356b3-126">Authenticate with Azure Managed Identities</span></span>
<span data-ttu-id="356b3-127">Azure 관리 ID는 특정 자격 증명을 만들 필요 없이 Azure의 리소스로 SDK/CLI를 사용하는 간단한 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="356b3-127">Azure Managed Identity is a simple way for a resource in Azure to use SDK/CLI without the need to create specific credentials.</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="356b3-128">관리 ID를 사용하려면 Azure에서 실행 중인 VM 또는 Azure 함수와 같은 Azure 리소스에서 Azure에 연결해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="356b3-128">To use managed identities, you must be connecting to Azure from an Azure resource, such as an Azure Function or a VM running in Azure.</span></span> <span data-ttu-id="356b3-129">리소스의 관리 ID를 구성하는 방법을 알아보려면 [Azure 리소스의 관리 ID 구성](/azure/active-directory/managed-identities-azure-resources/qs-configure-cli-windows-vm) 및 [Azure 리소스의 관리 ID를 사용하는 방법](/azure/active-directory/managed-identities-azure-resources/how-to-use-vm-sign-in)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="356b3-129">To learn how to configure a managed identity for a resource, see [Configure managed identities for Azure resources](/azure/active-directory/managed-identities-azure-resources/qs-configure-cli-windows-vm) and [How to use managed identities for Azure resources](/azure/active-directory/managed-identities-azure-resources/how-to-use-vm-sign-in).</span></span>

```python
from msrestazure.azure_active_directory import MSIAuthentication
from azure.mgmt.resource import ResourceManagementClient, SubscriptionClient

# Create MSI Authentication
credentials = MSIAuthentication()


# Create a Subscription Client
subscription_client = SubscriptionClient(credentials)
subscription = next(subscription_client.subscriptions.list())
subscription_id = subscription.subscription_id

# Create a Resource Management client
resource_client = ResourceManagementClient(credentials, subscription_id)


# List resource groups as an example. The only limit is what role and policy are assigned to this MSI token.
for resource_group in resource_client.resource_groups.list():
    print(resource_group.name)
```

## <a name="mgmt-auth-cli"></a><span data-ttu-id="356b3-130">CLI 기반 인증</span><span class="sxs-lookup"><span data-stu-id="356b3-130">CLI-based authentication</span></span>

<span data-ttu-id="356b3-131">SDK는 Azure CLI 활성 구독을 사용하여 클라이언트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="356b3-131">The SDK is able to create a client using the Azure CLI's active subscription.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="356b3-132">이 인증 방법은 개발자가 빠르게 시작해볼 때 사용되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="356b3-132">This should be used as quick start developer experience.</span></span> <span data-ttu-id="356b3-133">프로덕션 용도로는 [ADAL](#mgmt-auth-legacy) 또는 사용자 고유의 자격 증명 시스템을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="356b3-133">For production purposes, use [ADAL](#mgmt-auth-legacy) or your own credentials system.</span></span>
> <span data-ttu-id="356b3-134">CLI 구성을 변경하면 SDK 실행에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="356b3-134">Any change to your CLI configuration will impact the SDK execution.</span></span>

<span data-ttu-id="356b3-135">활성 자격 증명을 정의하려면 [az login](https://docs.microsoft.com/cli/azure/authenticate-azure-cli)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="356b3-135">To define active credentials, use [az login](https://docs.microsoft.com/cli/azure/authenticate-azure-cli).</span></span>
<span data-ttu-id="356b3-136">기본 구독 ID는 보유하고 있는 유일한 ID이거나 [az account](https://docs.microsoft.com/cli/azure/manage-azure-subscriptions-azure-cli)를 사용하여 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="356b3-136">Default subscription ID is either the only one you have, or you can define it using [az account](https://docs.microsoft.com/cli/azure/manage-azure-subscriptions-azure-cli)</span></span>

```python
from azure.common.client_factory import get_client_from_cli_profile
from azure.mgmt.compute import ComputeManagementClient

client = get_client_from_cli_profile(ComputeManagementClient)
```

## <a name="mgmt-auth-legacy"></a><span data-ttu-id="356b3-137">토큰 자격 증명(레거시)을 사용하여 인증</span><span class="sxs-lookup"><span data-stu-id="356b3-137">Authenticate with token credentials (legacy)</span></span>

<span data-ttu-id="356b3-138">이전 버전의 SDK에서는 ADAL을 사용할 수 없었으며 `UserPassCredentials` 클래스를 제공했습니다.</span><span class="sxs-lookup"><span data-stu-id="356b3-138">In previous version of the SDK, ADAL was not yet available and we provided a `UserPassCredentials` class.</span></span> <span data-ttu-id="356b3-139">이는 사용되지 않는 것으로 간주되며, 더 이상 사용되지 않아야 합니다.</span><span class="sxs-lookup"><span data-stu-id="356b3-139">This is considered deprecated and should not be used anymore.</span></span>

<span data-ttu-id="356b3-140">이 샘플에서는 사용자/암호 시나리오를 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="356b3-140">This sample shows user/password scenario.</span></span> <span data-ttu-id="356b3-141">이 시나리오는 2FA를 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="356b3-141">This does not support 2FA.</span></span>

```python
from azure.common.credentials import UserPassCredentials

credentials = UserPassCredentials(
    'user@domain.com',
    'my_smart_password'
)
```
