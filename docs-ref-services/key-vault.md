---
title: Python용 Azure Key Vault 라이브러리
description: Python용 Azure Key Vault 라이브러리에 대한 참조 설명서
author: lisawong19
keywords: Azure, Python, SDK, API, 키, Key Vault, 인증, 비밀, 키, 보안
manager: douge
ms.author: liwong
ms.date: 07/18/2017
ms.topic: article
ms.devlang: python
ms.service: keyvault
ms.openlocfilehash: 1ac9cc92a4c830a8c156117d3e0d188b8032f29a
ms.sourcegitcommit: 42d868d89eb28a6fdceffccfa03e3209a755b812
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/20/2018
---
# <a name="azure-key-vault-libraries-for-python"></a><span data-ttu-id="bfbfb-104">Python용 Azure Key Vault 라이브러리</span><span class="sxs-lookup"><span data-stu-id="bfbfb-104">Azure Key Vault libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="bfbfb-105">개요</span><span class="sxs-lookup"><span data-stu-id="bfbfb-105">Overview</span></span>

<span data-ttu-id="bfbfb-106">클라이언트 라이브러리를 사용하여 Azure Key Vault에서 키와 비밀을 생성, 업데이트 및 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbfb-106">Create, update, and delete keys and secrets in Azure Key Vault with the client libraries.</span></span>

<span data-ttu-id="bfbfb-107">Azure Key Vault 관리 라이브러리를 사용하여 키 자격 증명 모음을 만들고, 응용 프로그램에 권한을 부여하고, 권한을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbfb-107">Use the Azure Key Vault management libraries to create key vaults, authorize applications, and manage permissions.</span></span> 

<span data-ttu-id="bfbfb-108">[Azure Key Vault](/azure/key-vault/key-vault-whatis)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="bfbfb-108">Learn more about [Azure Key Vault](/azure/key-vault/key-vault-whatis).</span></span>

## <a name="install-the-libraries"></a><span data-ttu-id="bfbfb-109">라이브러리 설치</span><span class="sxs-lookup"><span data-stu-id="bfbfb-109">Install the libraries</span></span>

### <a name="client-library"></a><span data-ttu-id="bfbfb-110">클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="bfbfb-110">Client library</span></span>

```bash
pip install azure-keyvault
```

## <a name="examples"></a><span data-ttu-id="bfbfb-111">예</span><span class="sxs-lookup"><span data-stu-id="bfbfb-111">Examples</span></span>

<span data-ttu-id="bfbfb-112">Key Vault에서 [JSON 웹 키](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18)를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="bfbfb-112">Retrieve a [JSON web key](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) from a Key Vault.</span></span>

```python
from azure.keyvault import KeyVaultClient, KeyVaultAuthentication
from azure.common.credentials import ServicePrincipalCredentials

credentials = None

def auth_callback(server, resource, scope):
    credentials = ServicePrincipalCredentials(
        client_id = '', #client id
        secret = '',
        tenant = '',
        resource = "https://vault.azure.net"
    )
    token = credentials.token
    return token['token_type'], token['access_token']

client = KeyVaultClient(KeyVaultAuthentication(auth_callback))

key_bundle = client.get_key(vault_url, key_name, key_version)
json_key = key_bundle.key
```

<span data-ttu-id="bfbfb-113">마찬가지로, 다음 코드 조각을 사용하여 자격 증명 모음에서 비밀을 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="bfbfb-113">Similarly, you can use the following snippet to retrieve a secret from the vault:</span></span>

```
from azure.keyvault import KeyVaultClient, KeyVaultAuthentication
from azure.common.credentials import ServicePrincipalCredentials

credentials = None

def auth_callback(server, resource, scope):
    credentials = ServicePrincipalCredentials(
        client_id = '',
        secret = '',
        tenant = '',
        resource = "https://vault.azure.net"
    )
    token = credentials.token
    return token['token_type'], token['access_token']

client = KeyVaultClient(KeyVaultAuthentication(auth_callback))

secret_bundle = client.get_secret("https://VAULT_ID.vault.azure.net/", "SECRET_ID", "SECRET_VERSION")

print(secret_bundle.value)
```

[!div class="nextstepaction"]
[<span data-ttu-id="bfbfb-114">클라이언트 API 탐색</span><span class="sxs-lookup"><span data-stu-id="bfbfb-114">Explore the Client APIs</span></span>](/python/api/overview/azure/keyvault/client)

### <a name="management-api"></a><span data-ttu-id="bfbfb-115">관리 API</span><span class="sxs-lookup"><span data-stu-id="bfbfb-115">Management API</span></span>

```bash
pip install azure-mgmt-keyvault
```

### <a name="example"></a><span data-ttu-id="bfbfb-116">예</span><span class="sxs-lookup"><span data-stu-id="bfbfb-116">Example</span></span>
<span data-ttu-id="bfbfb-117">다음 예제에서는 Azure Key Vault를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="bfbfb-117">The following example shows how to create an Azure Key Vault.</span></span> 

```python
from azure.mgmt.keyvault import KeyVaultManagementClient

GROUP_NAME = 'your_resource_group_name'
KV_NAME = 'your_key_vault_name'
#The object ID of the User or Application for access policies. Find this number in the portal
OBJECT_ID = '00000000-0000-0000-0000-000000000000'

kv_client = KeyVaultManagementClient(credentials, subscription_id)

vault = kv_client.vaults.create_or_update(
    GROUP_NAME,
    KV_NAME,
    {
        'location': 'eastus',
        'properties': {
            'sku': {
                'name': 'standard'
            },
            'tenant_id': os.environ['AZURE_TENANT_ID'],
            'access_policies': [{
                'tenant_id': os.environ['AZURE_TENANT_ID'],
                'object_id': OBJECT_ID,
                'permissions': {
                    'keys': ['all'],
                    'secrets': ['all']
                }
            }]
        }
    }
)
```
> [!div class="nextstepaction"]
> [<span data-ttu-id="bfbfb-118">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="bfbfb-118">Explore the Management APIs</span></span>](/python/api/azure.mgmt.keyvault)

> [!div class="nextstepaction"]
> [<span data-ttu-id="bfbfb-119">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="bfbfb-119">Explore the Management APIs</span></span>](/python/api/overview/azure/keyvault/management)

## <a name="samples"></a><span data-ttu-id="bfbfb-120">샘플</span><span class="sxs-lookup"><span data-stu-id="bfbfb-120">Samples</span></span>
* <span data-ttu-id="bfbfb-121">[Key Vault 관리][1]</span><span class="sxs-lookup"><span data-stu-id="bfbfb-121">[Manage Key Vaults][1]</span></span> 
* <span data-ttu-id="bfbfb-122">[Key Vault 복구(영문)][2]</span><span class="sxs-lookup"><span data-stu-id="bfbfb-122">[Key Vault recovery][2]</span></span>

[1]: https://azure.microsoft.com/resources/samples/key-vault-python-manage/
[2]: https://azure.microsoft.com/resources/samples/key-vault-recovery-python/

<span data-ttu-id="bfbfb-123">Azure Key Vault 샘플의 [전체 목록](https://azure.microsoft.com/resources/samples/?platform=python&term=key+vault)을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="bfbfb-123">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=python&term=key+vault) of Azure Key Vault samples.</span></span> 
