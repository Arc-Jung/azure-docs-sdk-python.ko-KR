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
# <a name="azure-key-vault-libraries-for-python"></a>Python용 Azure Key Vault 라이브러리

[Azure Key Vault](/azure/key-vault/)는 암호화 키, 비밀 및 인증서 관리를 위한 Azure의 저장 및 관리 시스템입니다. Key Vault용 Python SDK API는 클라이언트 라이브러리와 관리 라이브러리로 분할됩니다.

클라이언트 라이브러리를 사용하여 다음을 수행할 수 있습니다.
- Azure Key Vault에 저장된 항목 액세스, 업데이트 또는 삭제
- 저장된 인증서에 대한 메타데이터 가져오기
- Key Vault에서 대칭 키에 대한 서명 확인

관리 라이브러리를 사용하여 다음을 수행할 수 있습니다.
- 새 Key Vault 저장소 만들기, 업데이트 또는 삭제
- Key Vault 액세스 정책 제어
- 구독 또는 리소스 그룹 별로 자격 증명 모음 나열
- 자격 증명 모음 이름 가용성 확인

## <a name="install-the-libraries"></a>라이브러리 설치

### <a name="client-library"></a>클라이언트 라이브러리

```bash
pip install azure-keyvault
```

## <a name="examples"></a>예

다음 예에서는 서비스 주체 인증을 사용합니다. 이 인증은 Azure에 연결하는 애플리케이션에 권장되는 로그인 방법입니다. 서비스 주체 인증에 대한 자세한 내용은 [Python용 Azure SDK로 인증](https://docs.microsoft.com/en-us/python/azure/python-sdk-azure-authenticate)을 참조하십시오.

자격 증명 모음에서 비대칭 키의 공용 부분 검색:

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

자격 증명 모음에서 비밀 검색:

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
> [클라이언트 API 탐색](/python/api/overview/azure/keyvault/client)

### <a name="management-library"></a>관리 라이브러리

```bash
pip install azure-mgmt-keyvault
```

### <a name="example"></a>예

다음 예제에서는 Azure Key Vault를 만드는 방법을 보여 줍니다. 

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
> [관리 API 탐색](/python/api/overview/azure/keyvault/management)

## <a name="samples"></a>샘플
* [Azure Key Vault 관리][1] 
* [Azure Key Vault 복구][2]

[1]: https://azure.microsoft.com/resources/samples/key-vault-python-manage/
[2]: https://azure.microsoft.com/resources/samples/key-vault-recovery-python/

Azure Key Vault 샘플의 [전체 목록](https://azure.microsoft.com/resources/samples/?platform=python&term=key+vault)을 봅니다. 
