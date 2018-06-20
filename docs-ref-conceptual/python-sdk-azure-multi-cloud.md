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
# <a name="multi-cloud---use-azure-on-all-regions"></a>다중 클라우드 - 모든 지역에서 Azure 사용

Python용 Azure SDK를 사용하여 Azure를 [사용 가능한](https://azure.microsoft.com/regions/services) 모든 지역에 연결할 수 있습니다.

Python용 Azure SDK는 기본적으로 공용 Azure에 연결하도록 구성됩니다.

## <a name="using-predeclared-cloud-definition"></a>미리 선언된 클라우드 정의 사용

> [!IMPORTANT]
> 이 섹션에서 `msrestazure` 패키지는 0.4.11 이상이어야 합니다.

`msrestazure`의 `azure_cloud` 모듈을 사용할 수 있습니다.

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
  
사용 가능한 클라우드 정의는 다음과 같습니다.
  - AZURE_PUBLIC_CLOUD
  - AZURE_CHINA_CLOUD
  - AZURE_US_GOV_CLOUD
  - AZURE_GERMAN_CLOUD

## <a name="using-your-own-cloud-definition-eg-azure-stack"></a>고유한 클라우드 정의 사용(예: Azure Stack)
ARM에는 다음에 도움이 되는 메타데이터 끝점이 있습니다.

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
## <a name="using-adal"></a>ADAL 사용

다른 지역에 연결하려면 몇 가지를 고려해야 합니다.

- 토큰에 요청할 끝점은 어디인가요(인증)?
- 이 토큰을 사용할 끝점은 어디인가요(사용량)?

일반적인 예는 다음과 같습니다.

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

### <a name="azure-government"></a>Azure Government
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

### <a name="azure-germany"></a>Azure Germany
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

### <a name="azure-china"></a>Azure China
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
