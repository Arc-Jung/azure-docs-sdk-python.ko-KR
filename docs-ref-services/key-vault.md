---
title: "Python용 Azure Key Vault 라이브러리"
description: "Python용 Azure Key Vault 라이브러리에 대한 참조 설명서"
author: lisawong19
keywords: "Azure, Python, SDK, API, 키, Key Vault, 인증, 비밀, 키, 보안"
manager: douge
ms.author: liwong
ms.date: 07/18/2017
ms.topic: article
ms.devlang: python
ms.service: keyvault
ms.openlocfilehash: 3eac46eb4d5d19273ead9f19b739f6fb6d72e5cc
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-key-vault-libraries-for-python"></a><span data-ttu-id="227c5-104">Python용 Azure Key Vault 라이브러리</span><span class="sxs-lookup"><span data-stu-id="227c5-104">Azure Key Vault libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="227c5-105">개요</span><span class="sxs-lookup"><span data-stu-id="227c5-105">Overview</span></span>

<span data-ttu-id="227c5-106">클라이언트 라이브러리를 사용하여 Azure Key Vault에서 키와 비밀을 생성, 업데이트 및 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="227c5-106">Create, update, and delete keys and secrets in Azure Key Vault with the client libraries.</span></span>

<span data-ttu-id="227c5-107">Azure Key Vault 관리 라이브러리를 사용하여 키 자격 증명 모음을 만들고, 응용 프로그램에 권한을 부여하고, 권한을 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="227c5-107">Use the Azure Key Vault management libraries to create key vaults, authorize applications, and manage permissions.</span></span> 

<span data-ttu-id="227c5-108">[Azure Key Vault](/azure/key-vault/key-vault-whatis)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="227c5-108">Learn more about [Azure Key Vault](/azure/key-vault/key-vault-whatis).</span></span>

## <a name="install-the-libraries"></a><span data-ttu-id="227c5-109">라이브러리 설치</span><span class="sxs-lookup"><span data-stu-id="227c5-109">Install the libraries</span></span>

### <a name="client-library"></a><span data-ttu-id="227c5-110">클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="227c5-110">Client library</span></span>
```bash
pip install azure-keyvault
```

## <a name="example"></a><span data-ttu-id="227c5-111">예제</span><span class="sxs-lookup"><span data-stu-id="227c5-111">Example</span></span>
<span data-ttu-id="227c5-112">Key Vault에서 [JSON 웹 키](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18)를 검색합니다.</span><span class="sxs-lookup"><span data-stu-id="227c5-112">Retrieve a [JSON web key](https://tools.ietf.org/html/draft-ietf-jose-json-web-key-18) from a Key Vault.</span></span>

```python
from azure.keyvault import KeyVaultClient, KeyVaultAuthentication
from azure.common.credentials import ServicePrincipalCredentials

credentials = None

def auth_callack(server, resource, scope):
    credentials = credentials or ServicePrincipalCredentials(
        client_id = '', #client id
        secret = '',
        tenant = '',
        resource = resource
    )
    token = credentials.token
    return token['token_type'], token['access_token']

client = KeyVaultClient(KeyVaultAuthentication(auth_callack))

key_bundle = client.get_key(vault_url, key_name, key_version)
json_key = key_bundle.key
```
[!div class="nextstepaction"]
[<span data-ttu-id="227c5-113">클라이언트 API 탐색</span><span class="sxs-lookup"><span data-stu-id="227c5-113">Explore the Client APIs</span></span>](/python/api/overview/azure/keyvault/clientlibrary)

### <a name="management-api"></a><span data-ttu-id="227c5-114">관리 API</span><span class="sxs-lookup"><span data-stu-id="227c5-114">Management API</span></span>
```bash
pip install azure-mgmt-keyvault
```

### <a name="example"></a><span data-ttu-id="227c5-115">예제</span><span class="sxs-lookup"><span data-stu-id="227c5-115">Example</span></span>
<span data-ttu-id="227c5-116">다음 예제에서는 Azure Key Vault를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="227c5-116">The following example shows how to create an Azure Key Vault.</span></span> 

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
> [<span data-ttu-id="227c5-117">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="227c5-117">Explore the Management APIs</span></span>](/python/api/azure.mgmt.keyvault)

> [!div class="nextstepaction"]
> [<span data-ttu-id="227c5-118">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="227c5-118">Explore the Management APIs</span></span>](/python/api/overview/azure/keyvault/managementlibrary)

## <a name="samples"></a><span data-ttu-id="227c5-119">샘플</span><span class="sxs-lookup"><span data-stu-id="227c5-119">Samples</span></span>
* <span data-ttu-id="227c5-120">[Key Vault 관리][1]</span><span class="sxs-lookup"><span data-stu-id="227c5-120">[Manage Key Vaults][1]</span></span> 
* <span data-ttu-id="227c5-121">[Key Vault 복구(영문)][2]</span><span class="sxs-lookup"><span data-stu-id="227c5-121">[Key Vault recovery][2]</span></span>

[1]: https://azure.microsoft.com/resources/samples/key-vault-python-manage/
[2]: https://azure.microsoft.com/resources/samples/key-vault-recovery-python/

<span data-ttu-id="227c5-122">Azure Key Vault 샘플의 [전체 목록](https://azure.microsoft.com/resources/samples/?platform=python&term=key+vault)을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="227c5-122">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=python&term=key+vault) of Azure Key Vault samples.</span></span> 