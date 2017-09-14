---
title: "Python용 Azure Active Directory 라이브러리"
description: "Python용 Azure Active Directory 라이브러리에 대한 참조 설명서"
keywords: "Azure, Python, SDK, API, SQL, 인증 AAD, Active Directory, Graph, OAuth 2.0"
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 08/07/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: active-directory
ms.openlocfilehash: 41234fd44fa98c1ff57287193b0437b7caca46c8
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-active-directory-libraries-for-python"></a>Python용 Azure Active Directory 라이브러리

## <a name="overview"></a>개요

[Azure Active Directory](/azure/active-directory/active-directory-whatis)를 사용하여 사용자를 로그온하고 응용 프로그램 및 API에 대한 액세스를 제어합니다.

## <a name="client-library"></a>클라이언트 라이브러리

[Python용 ADAL(Active Directory Authentication Library)](https://github.com/AzureAD/azure-activedirectory-library-for-python)을 사용하여 OAuth2, OpenID Connect 또는 Active Directory Graph 인증 및 [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) Single Sign-On을 구성합니다.

```bash
pip install azure-graphrbac
```

### <a name="example"></a>예제
> [!NOTE]
> 자격 증명 인스턴스를 만드는 동안 리소스 매개 변수를 https://graph.windows.net으로 변경해야 합니다.

```python
from azure.graphrbac import GraphRbacManagementClient
from azure.common.credentials import UserPassCredentials

credentials = UserPassCredentials(
            'user@domain.com',      # Your user
            'my_password',          # Your password
            resource="https://graph.windows.net"
    )

tenant_id = "myad.onmicrosoft.com"

graphrbac_client = GraphRbacManagementClient(
    credentials,
    tenant_id
)
```
다음 코드에서는 사용자를 만들고 목록 필터링을 통해 직접 가져와서 삭제합니다.
```python
from azure.graphrbac.models import UserCreateParameters, PasswordProfile

user = graphrbac_client.users.create(
    UserCreateParameters(
        user_principal_name="testbuddy@{}".format(MY_AD_DOMAIN),
        account_enabled=False,
        display_name='Test Buddy',
        mail_nickname='testbuddy',
        password_profile=PasswordProfile(
            password='MyStr0ngP4ssword',
            force_change_password_next_login=True
        )
    )
)
# user is a User instance
self.assertEqual(user.display_name, 'Test Buddy')

user = graphrbac_client.users.get(user.object_id)
self.assertEqual(user.display_name, 'Test Buddy')

for user in graphrbac_client.users.list(filter="displayName eq 'Test Buddy'"):
    self.assertEqual(user.display_name, 'Test Buddy')

graphrbac_client.users.delete(user.object_id)
```

> [!div class="nextstepaction"]
> [클라이언트 API 탐색](/python/api/overview/azure/activedirectory/clientlibrary?)

앱에서 사용할 수 있는 [Azure AD용 Python 샘플 코드](https://azure.microsoft.com/en-us/resources/samples/?term=active+directory&platform=python)를 추가로 탐색합니다.