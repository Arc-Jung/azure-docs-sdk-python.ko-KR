---
title: Python용 Graph RBAC 라이브러리
description: Python용 Graph RBAC 라이브러리에 대한 참조
keywords: Azure, Python, SDK, API, Graph RBAC
author: rloutlaw
ms.author: routlaw
manager: jfriend
ms.date: 05/10/2019
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: e9b0aba7998565284ae18e0036da96d033b2b05f
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534273"
---
# <a name="azure-active-directory-graph-libraries-for-python"></a><span data-ttu-id="f4067-104">Python용 Azure Active Directory Graph 라이브러리</span><span class="sxs-lookup"><span data-stu-id="f4067-104">Azure Active Directory Graph libraries for Python</span></span>

> [!IMPORTANT]
>
> <span data-ttu-id="f4067-105">2019년 2월부터 Microsoft Graph API를 위해 이전 버전의 Azure Active Directory Graph API를 사용하지 않도록 중단하는 프로세스를 시작했습니다.</span><span class="sxs-lookup"><span data-stu-id="f4067-105">As of February 2019, we started the process to deprecate some earlier versions of Azure Active Directory Graph API in favor of the Microsoft Graph API.</span></span> 
>
> <span data-ttu-id="f4067-106">자세한 내용, 업데이트 및 시간 프레임은 Office 개발자 센터의 [Microsoft Graph 또는 Azure AD Graph](https://dev.office.com/blogs/microsoft-graph-or-azure-ad-graph)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f4067-106">For details, updates, and time frames, see [Microsoft Graph or the Azure AD Graph](https://dev.office.com/blogs/microsoft-graph-or-azure-ad-graph) in the Office Dev Center.</span></span>
>
> <span data-ttu-id="f4067-107">앞으로 애플리케이션은 Microsoft Graph API를 사용해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4067-107">Moving forward, applications should use the Microsoft Graph API.</span></span> 

## <a name="overview"></a><span data-ttu-id="f4067-108">개요</span><span class="sxs-lookup"><span data-stu-id="f4067-108">Overview</span></span> 

<span data-ttu-id="f4067-109">[Active Directory Graph](/azure/active-directory/develop/active-directory-graph-api)를 사용하여 사용자로 로그온하고 애플리케이션 및 API에 대한 액세스를 제어합니다.</span><span class="sxs-lookup"><span data-stu-id="f4067-109">Sign-on users and control access to applications and APIs with [Active Directory Graph](/azure/active-directory/develop/active-directory-graph-api).</span></span>    

## <a name="client-library"></a><span data-ttu-id="f4067-110">클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="f4067-110">Client library</span></span>   

 ```bash    
pip install azure-graphrbac 
``` 

### <a name="example"></a><span data-ttu-id="f4067-111">예</span><span class="sxs-lookup"><span data-stu-id="f4067-111">Example</span></span> 
> [!NOTE]   
> <span data-ttu-id="f4067-112">자격 증명 인스턴스를 만드는 동안 리소스 매개 변수를 https://graph.windows.net 으로 변경해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f4067-112">You need to change the resource parameter to https://graph.windows.net while creating the credentials instance</span></span>    
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
<span data-ttu-id="f4067-113">다음 코드에서는 사용자를 만들고 목록 필터링을 통해 직접 가져와서 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="f4067-113">The following code creates a user, get it directly and by list filtering, and then delete it.</span></span>   
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