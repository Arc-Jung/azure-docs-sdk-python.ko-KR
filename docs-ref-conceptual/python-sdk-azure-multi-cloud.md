---
title: 다중 클라우드
description: 모든 지역에서 Azure 사용
author: lmazuel
ms.author: lmazuel
manager: routlaw
ms.date: 02/22/2018
ms.topic: article
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 6d2ba0580f8b6dda857b48ed5235a8c969a051f5
ms.sourcegitcommit: 7066ace94076483bae7d54172605f431e47bd5ee
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/05/2018
ms.locfileid: "30820127"
---
# <a name="multi-cloud---use-azure-on-all-regions"></a><span data-ttu-id="726b0-103">다중 클라우드 - 모든 지역에서 Azure 사용</span><span class="sxs-lookup"><span data-stu-id="726b0-103">Multi-cloud - use Azure on all regions</span></span>

<span data-ttu-id="726b0-104">Python용 Azure SDK를 사용하여 Azure를 [사용 가능한](https://azure.microsoft.com/regions/services) 모든 지역에 연결할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="726b0-104">You can use the Azure SDK for Python to connect to all regions where Azure is [available](https://azure.microsoft.com/regions/services).</span></span>

<span data-ttu-id="726b0-105">Python용 Azure SDK는 기본적으로 공용 Azure에 연결하도록 구성됩니다.</span><span class="sxs-lookup"><span data-stu-id="726b0-105">By default, the Azure SDK for Python is configured to connect to public Azure.</span></span>

## <a name="using-predeclared-cloud-definition"></a><span data-ttu-id="726b0-106">미리 선언된 클라우드 정의 사용</span><span class="sxs-lookup"><span data-stu-id="726b0-106">Using predeclared cloud definition</span></span>

> [!IMPORTANT]
> <span data-ttu-id="726b0-107">이 섹션에서 `msrestazure` 패키지는 0.4.11 이상이어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="726b0-107">The `msrestazure` package must be superior or equals to 0.4.11 for this section.</span></span>

<span data-ttu-id="726b0-108">`msrestazure`의 `azure_cloud` 모듈을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="726b0-108">You can use the `azure_cloud` module of `msrestazure`</span></span>

```python
from msrestazure.azure_cloud import AZURE_CHINA_CLOUD
from msrestazure.azure_active_directory import UserPassCredentials
from azure.mgmt.resource import ResourceManagementClient

credentials = UserPassCredentials(
    login,
    password,
    cloud_environment=AZURE_CHINA_CLOUD
)
client = ResourceManagementClient(
    credentials,
    subscription_id,
    base_url=AZURE_CHINA_CLOUD.endpoints.resource_manager
)
``` 
  
<span data-ttu-id="726b0-109">사용 가능한 클라우드 정의는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="726b0-109">Available cloud definition are</span></span>
  - <span data-ttu-id="726b0-110">AZURE_PUBLIC_CLOUD</span><span class="sxs-lookup"><span data-stu-id="726b0-110">AZURE_PUBLIC_CLOUD</span></span>
  - <span data-ttu-id="726b0-111">AZURE_CHINA_CLOUD</span><span class="sxs-lookup"><span data-stu-id="726b0-111">AZURE_CHINA_CLOUD</span></span>
  - <span data-ttu-id="726b0-112">AZURE_US_GOV_CLOUD</span><span class="sxs-lookup"><span data-stu-id="726b0-112">AZURE_US_GOV_CLOUD</span></span>
  - <span data-ttu-id="726b0-113">AZURE_GERMAN_CLOUD</span><span class="sxs-lookup"><span data-stu-id="726b0-113">AZURE_GERMAN_CLOUD</span></span>

## <a name="using-your-own-cloud-definition-eg-azure-stack"></a><span data-ttu-id="726b0-114">고유한 클라우드 정의 사용(예: Azure Stack)</span><span class="sxs-lookup"><span data-stu-id="726b0-114">Using your own cloud definition (e.g. Azure Stack)</span></span>
<span data-ttu-id="726b0-115">ARM에는 다음에 도움이 되는 메타데이터 끝점이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="726b0-115">ARM has a metadata endpoint to help you:</span></span>

```python
from msrestazure.azure_cloud import get_cloud_from_metadata_endpoint
from msrestazure.azure_active_directory import UserPassCredentials
from azure.mgmt.resource import ResourceManagementClient

mystack_cloud = get_cloud_from_metadata_endpoint("https://myazurestack-arm-endpoint.com")
credentials = UserPassCredentials(
    login,
    password,
    cloud_environment=mystack_cloud
)
client = ResourceManagementClient(
    credentials,
    subscription_id,
    base_url=mystack_cloud.endpoints.resource_manager
)
```
## <a name="using-adal"></a><span data-ttu-id="726b0-116">ADAL 사용</span><span class="sxs-lookup"><span data-stu-id="726b0-116">Using ADAL</span></span>

<span data-ttu-id="726b0-117">다른 지역에 연결하려면 몇 가지를 고려해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="726b0-117">To connect to another region, a few things have to be considered:</span></span>

- <span data-ttu-id="726b0-118">토큰에 요청할 끝점은 어디인가요(인증)?</span><span class="sxs-lookup"><span data-stu-id="726b0-118">What is the endpoint where to ask for a token (authentication)?</span></span>
- <span data-ttu-id="726b0-119">이 토큰을 사용할 끝점은 어디인가요(사용량)?</span><span class="sxs-lookup"><span data-stu-id="726b0-119">What is the endpoint where I will use this token (usage)?</span></span>

<span data-ttu-id="726b0-120">일반적인 예는 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="726b0-120">This is a generic example:</span></span>

```python
import adal
from msrestazure.azure_active_directory import AdalAuthentication
from azure.mgmt.resource import ResourceManagementClient

# Service Principal
tenant = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'
client_id = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'
password = 'password'

# Public Azure - default values
authentication_endpoint = 'https://login.microsoftonline.com/'
azure_endpoint = 'https://management.azure.com/'
    
context = adal.AuthenticationContext(authentication_endpoint+tenant)
credentials = AdalAuthentication(
    context.acquire_token_with_client_credentials,
    azure_endpoint,
    client_id,
    password
)
subscription_id = '33333333-3333-3333-3333-333333333333'

resource_client = ResourceManagementClient(
    credentials,
    subscription_id,
    base_url=azure_endpoint
)
```

### <a name="azure-government"></a><span data-ttu-id="726b0-121">Azure Government</span><span class="sxs-lookup"><span data-stu-id="726b0-121">Azure Government</span></span>
```python
import adal
from msrestazure.azure_active_directory import AdalAuthentication
from azure.mgmt.resource import ResourceManagementClient

# Service Principal
tenant = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'
client_id = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'
password = 'password'

# Government
authentication_endpoint = 'https://login-us.microsoftonline.com/'
azure_endpoint = 'https://management.usgovcloudapi.net/'
    
context = adal.AuthenticationContext(authentication_endpoint+tenant)
credentials = AdalAuthentication(
    context.acquire_token_with_client_credentials,
    azure_endpoint,
    client_id,
    password
)
subscription_id = '33333333-3333-3333-3333-333333333333'

resource_client = ResourceManagementClient(
    credentials,
    subscription_id,
    base_url=azure_endpoint
)
```

### <a name="azure-germany"></a><span data-ttu-id="726b0-122">Azure Germany</span><span class="sxs-lookup"><span data-stu-id="726b0-122">Azure Germany</span></span>
```python
import adal
from msrestazure.azure_active_directory import AdalAuthentication
from azure.mgmt.resource import ResourceManagementClient

# Service Principal
tenant = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'
client_id = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'
password = 'password'

# Azure Germany
authentication_endpoint = 'https://login.microsoftonline.de/'
azure_endpoint = 'https://management.microsoftazure.de/'
    
context = adal.AuthenticationContext(authentication_endpoint+tenant)
credentials = AdalAuthentication(
    context.acquire_token_with_client_credentials,
    azure_endpoint,
    client_id,
    password
)
subscription_id = '33333333-3333-3333-3333-333333333333'

resource_client = ResourceManagementClient(
    credentials,
    subscription_id,
    base_url=azure_endpoint
)
```

### <a name="azure-china"></a><span data-ttu-id="726b0-123">Azure China</span><span class="sxs-lookup"><span data-stu-id="726b0-123">Azure China</span></span>
```python
import adal
from msrestazure.azure_active_directory import AdalAuthentication
from azure.mgmt.resource import ResourceManagementClient

# Service Principal
tenant = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'
client_id = 'ABCDEFGH-1234-1234-1234-ABCDEFGHIJKL'
password = 'password'

# Azure China
authentication_endpoint = 'https://login.chinacloudapi.cn/'
azure_endpoint = 'https://management.chinacloudapi.cn/'
    
context = adal.AuthenticationContext(authentication_endpoint+tenant)
credentials = AdalAuthentication(
    context.acquire_token_with_client_credentials,
    azure_endpoint,
    client_id,
    password
)
subscription_id = '33333333-3333-3333-3333-333333333333'

resource_client = ResourceManagementClient(
    credentials,
    subscription_id,
    base_url=azure_endpoint
)
```
