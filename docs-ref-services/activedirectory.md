---
title: Python용 Azure Active Directory 라이브러리
description: Python용 Azure Active Directory 라이브러리에 대한 참조 설명서
keywords: Azure, Python, SDK, API, SQL, 인증 AAD, Active Directory, Graph, OAuth 2.0
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 08/07/2017
ms.topic: reference
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: active-directory
ms.openlocfilehash: 78df70001dd0d55ac2c9c9da04fac6a51c5919e6
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/23/2018
ms.locfileid: "29478926"
---
# <a name="azure-active-directory-libraries-for-python"></a><span data-ttu-id="3df7b-104">Python용 Azure Active Directory 라이브러리</span><span class="sxs-lookup"><span data-stu-id="3df7b-104">Azure Active Directory libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="3df7b-105">개요</span><span class="sxs-lookup"><span data-stu-id="3df7b-105">Overview</span></span>

<span data-ttu-id="3df7b-106">[Azure Active Directory](/azure/active-directory/active-directory-whatis)를 사용하여 사용자를 로그온하고 응용 프로그램 및 API에 대한 액세스를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="3df7b-106">Sign-on users and control access to applications and APIs with [Azure Active Directory](/azure/active-directory/active-directory-whatis).</span></span>

## <a name="client-library"></a><span data-ttu-id="3df7b-107">클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="3df7b-107">Client library</span></span>

<span data-ttu-id="3df7b-108">[Python용 ADAL(Active Directory Authentication Library)](https://github.com/AzureAD/azure-activedirectory-library-for-python)을 사용하여 OAuth2, OpenID Connect 또는 Active Directory Graph 인증 및 [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) Single Sign-On을 구성합니다.</span><span class="sxs-lookup"><span data-stu-id="3df7b-108">Configure OAuth2, OpenID Connect, or Active Directory Graph authentication and [SAML 2.0](https://docs.microsoft.com/azure/active-directory/develop/active-directory-saml-protocol-reference) single-sign on with the [Azure Active Directory authentication library (ADAL) for Python](https://github.com/AzureAD/azure-activedirectory-library-for-python).</span></span>

```bash
pip install azure-graphrbac
```

### <a name="example"></a><span data-ttu-id="3df7b-109">예</span><span class="sxs-lookup"><span data-stu-id="3df7b-109">Example</span></span>
> [!NOTE]
> <span data-ttu-id="3df7b-110">자격 증명 인스턴스를 만드는 동안 리소스 매개 변수를 https://graph.windows.net으로 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="3df7b-110">You need to change the resource parameter to https://graph.windows.net while creating the credentials instance</span></span>

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
<span data-ttu-id="3df7b-111">다음 코드에서는 사용자를 만들고 목록 필터링을 통해 직접 가져와서 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="3df7b-111">The following code creates a user, get it directly and by list filtering, and then delete it.</span></span>
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
> [<span data-ttu-id="3df7b-112">클라이언트 API 탐색</span><span class="sxs-lookup"><span data-stu-id="3df7b-112">Explore the Client APIs</span></span>](/python/api/overview/azure/activedirectory/client)

<span data-ttu-id="3df7b-113">앱에서 사용할 수 있는 [Azure AD용 Python 샘플 코드](https://azure.microsoft.com/en-us/resources/samples/?term=active+directory&platform=python)를 추가로 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="3df7b-113">Explore more [sample Python code for Azure AD](https://azure.microsoft.com/en-us/resources/samples/?term=active+directory&platform=python) you can use in your apps.</span></span>