---
title: Python용 Azure Key Vault 라이브러리
description: Python용 Azure Key Vault 라이브러리에 대한 참조 설명서
author: sptramer
manager: carmonm
ms.author: sttramer
ms.date: 06/10/2019
ms.topic: conceptual
ms.devlang: python
ms.service: keyvault
ms.openlocfilehash: f4661ee389c13ce8546e7b5cc8866ab7b216d3b0
ms.sourcegitcommit: 92fa5dbcfd9a20f4a49da5f4bdc03045783d3495
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "67149331"
---
# <a name="azure-key-vault-libraries-for-python"></a><span data-ttu-id="927a0-103">Python용 Azure Key Vault 라이브러리</span><span class="sxs-lookup"><span data-stu-id="927a0-103">Azure Key Vault libraries for Python</span></span>

<span data-ttu-id="927a0-104">[Azure Key Vault](/azure/key-vault/)는 암호화 키, 비밀 및 인증서 관리를 위한 Azure의 저장 및 관리 시스템입니다.</span><span class="sxs-lookup"><span data-stu-id="927a0-104">[Azure Key Vault](/azure/key-vault/) is Azure's storage and management system for cryptographic keys, secrets, and certificate management.</span></span> <span data-ttu-id="927a0-105">Key Vault용 Python SDK API는 클라이언트 라이브러리와 관리 라이브러리로 분할됩니다.</span><span class="sxs-lookup"><span data-stu-id="927a0-105">The Python SDK API for Key Vault is split between client libraries and management libraries.</span></span>

<span data-ttu-id="927a0-106">클라이언트 라이브러리를 사용하여 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="927a0-106">Use the client library to:</span></span>
- <span data-ttu-id="927a0-107">Azure Key Vault에 저장된 항목 액세스, 업데이트 또는 삭제</span><span class="sxs-lookup"><span data-stu-id="927a0-107">Access, update, or delete items stored in an Azure Key Vault</span></span>
- <span data-ttu-id="927a0-108">저장된 인증서에 대한 메타데이터 가져오기</span><span class="sxs-lookup"><span data-stu-id="927a0-108">Get metadata for stored certificates</span></span>
- <span data-ttu-id="927a0-109">Key Vault에서 대칭 키에 대한 서명 확인</span><span class="sxs-lookup"><span data-stu-id="927a0-109">Verify signatures against symmetric keys in Key Vault</span></span>

<span data-ttu-id="927a0-110">관리 라이브러리를 사용하여 다음을 수행할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="927a0-110">Use the management library to:</span></span>
- <span data-ttu-id="927a0-111">새 Key Vault 저장소 만들기, 업데이트 또는 삭제</span><span class="sxs-lookup"><span data-stu-id="927a0-111">Create, update, or delete new Key Vault stores</span></span>
- <span data-ttu-id="927a0-112">Key Vault 액세스 정책 제어</span><span class="sxs-lookup"><span data-stu-id="927a0-112">Control vault access policies</span></span>
- <span data-ttu-id="927a0-113">구독 또는 리소스 그룹 별로 자격 증명 모음 나열</span><span class="sxs-lookup"><span data-stu-id="927a0-113">List vaults by subscription or resource group</span></span>
- <span data-ttu-id="927a0-114">자격 증명 모음 이름 가용성 확인</span><span class="sxs-lookup"><span data-stu-id="927a0-114">Check for vault name availability</span></span>

## <a name="install-the-libraries"></a><span data-ttu-id="927a0-115">라이브러리 설치</span><span class="sxs-lookup"><span data-stu-id="927a0-115">Install the libraries</span></span>

### <a name="client-library"></a><span data-ttu-id="927a0-116">클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="927a0-116">Client library</span></span>

```bash
pip install azure-keyvault
```

## <a name="examples"></a><span data-ttu-id="927a0-117">예</span><span class="sxs-lookup"><span data-stu-id="927a0-117">Examples</span></span>

<span data-ttu-id="927a0-118">다음 예에서는 서비스 주체 인증을 사용합니다. 이 인증은 Azure에 연결하는 애플리케이션에 권장되는 로그인 방법입니다.</span><span class="sxs-lookup"><span data-stu-id="927a0-118">The following examples use service principal authentication, which is the recommended sign in method for applications that connect to Azure.</span></span> <span data-ttu-id="927a0-119">서비스 주체 인증에 대한 자세한 내용은 [Python용 Azure SDK로 인증](https://docs.microsoft.com/en-us/python/azure/python-sdk-azure-authenticate)을 참조하십시오.</span><span class="sxs-lookup"><span data-stu-id="927a0-119">To learn about service principal authentication, see [Authenticate with the Azure SDK for Python](https://docs.microsoft.com/en-us/python/azure/python-sdk-azure-authenticate)</span></span>

<span data-ttu-id="927a0-120">자격 증명 모음에서 비대칭 키의 공용 부분 검색:</span><span class="sxs-lookup"><span data-stu-id="927a0-120">Retrieve the public portion of an asymmetric key from a vault:</span></span>

```python
from azure.keyvault import KeyVaultClient
from azure.common.credentials import ServicePrincipalCredentials

credentials = ServicePrincipalCredentials(
    client_id = '...',
    secret = '...',
    tenant = '...'
)

client = KeyVaultClient(credentials)

# VAULT_URL must be in the format 'https://<vaultname>.vault.azure.net'
# KEY_VERSION is required, and can be obtained with the KeyVaultClient.get_key_versions(self, vault_url, key_name) API
key_bundle = client.get_key(VAULT_URL, KEY_NAME, KEY_VERSION)
key = key_bundle.key
```

<span data-ttu-id="927a0-121">자격 증명 모음에서 비밀 검색:</span><span class="sxs-lookup"><span data-stu-id="927a0-121">Retrieve a secret from a vault:</span></span>

```python
from azure.keyvault import KeyVaultClient
from azure.common.credentials import ServicePrincipalCredentials

credentials = ServicePrincipalCredentials(
    client_id = '...',
    secret = '...',
    tenant = '...'
)

client = KeyVaultClient(credentials)

# VAULT_URL must be in the format 'https://<vaultname>.vault.azure.net'
# SECRET_VERSION is required, and can be obtained with the KeyVaultClient.get_secret_versions(self, vault_url, secret_id) API
secret_bundle = client.get_secret(VAULT_URL, SECRET_ID, SECRET_VERSION)
secret = secret_bundle.value
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="927a0-122">클라이언트 API 탐색</span><span class="sxs-lookup"><span data-stu-id="927a0-122">Explore the Client APIs</span></span>](/python/api/overview/azure/keyvault/client)

### <a name="management-library"></a><span data-ttu-id="927a0-123">관리 라이브러리</span><span class="sxs-lookup"><span data-stu-id="927a0-123">Management library</span></span>

```bash
pip install azure-mgmt-keyvault
```

### <a name="example"></a><span data-ttu-id="927a0-124">예</span><span class="sxs-lookup"><span data-stu-id="927a0-124">Example</span></span>

<span data-ttu-id="927a0-125">다음 예제에서는 Azure Key Vault를 만드는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="927a0-125">The following example shows how to create an Azure Key Vault.</span></span> 

```python
from azure.mgmt.keyvault import KeyVaultManagementClient
from azure.common.credentials import ServicePrincipalCredentials


credentials = ServicePrincipalCredentials(
    client_id = '...',
    secret = '...',
    tenant = '...'
)

# Even when using service principal credentials, a subscription ID is required. For service principals,
# this should be the subscription used to create the service principal. Storing a token like a valid
# subscription ID in code is not recommended and only shown here for example purposes.
SUBSCRIPTION_ID = '...'
client = KeyVaultManagementClient(credentials, SUBSCRIPTION_ID)

# The object ID and organization ID (tenant) of the user, application, or service principal for access policies.
# These values can be found through the Azure CLI or the Portal.
ALLOW_OBJECT_ID = '...'
ALLOW_TENANT_ID = '...'

RESOURCE_GROUP = '...'
VAULT_NAME = '...'

# Vault properties may also be created by using the azure.mgmt.keyvault.models.VaultCreateOrUpdateParameters
# class, rather than a map. 
operation = client.vaults.create_or_update(
    RESOURCE_GROUP,
    VAULT_NAME,
    {
        'location': 'eastus',
        'properties': {
            'sku': {
                'name': 'standard'
            },
            'tenant_id': TENANT_ID,
            'access_policies': [{
                'object_id': OBJECT_ID,
                'tenant_id': ALLOW_TENANT_ID,
                'permissions': {
                    'keys': ['all'],
                    'secrets': ['all']
                }
            }]
        }
    }
)

vault = operation.result()
print(f'New vault URI: {vault.properties.vault_uri}')
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="927a0-126">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="927a0-126">Explore the Management APIs</span></span>](/python/api/overview/azure/keyvault/management)

## <a name="samples"></a><span data-ttu-id="927a0-127">샘플</span><span class="sxs-lookup"><span data-stu-id="927a0-127">Samples</span></span>
* <span data-ttu-id="927a0-128">[Azure Key Vault 관리][1]</span><span class="sxs-lookup"><span data-stu-id="927a0-128">[Manage Azure Key Vaults][1]</span></span> 
* <span data-ttu-id="927a0-129">[Azure Key Vault 복구][2]</span><span class="sxs-lookup"><span data-stu-id="927a0-129">[Azure Key Vault recovery][2]</span></span>

[1]: https://azure.microsoft.com/resources/samples/key-vault-python-manage/
[2]: https://azure.microsoft.com/resources/samples/key-vault-recovery-python/

<span data-ttu-id="927a0-130">Azure Key Vault 샘플의 [전체 목록](https://azure.microsoft.com/resources/samples/?platform=python&term=key+vault)을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="927a0-130">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=python&term=key+vault) of Azure Key Vault samples.</span></span> 
