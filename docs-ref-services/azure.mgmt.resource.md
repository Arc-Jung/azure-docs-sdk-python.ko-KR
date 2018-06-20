---
title: Python용 Azure 리소스 라이브러리
description: ''
keywords: Azure, Python, SDK, API, 리소스
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/19/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: resources
ms.openlocfilehash: 32e13bee27db091f0bca12c7d9ae4fc62165f4c0
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
ms.locfileid: "20909396"
---
# <a name="azure-resources-libraries-for-python"></a>Python용 Azure 리소스 라이브러리 

## <a name="overview"></a>개요 
리소스 그룹에서 Azure 리소스를 관리합니다.

| 패키지  |  설명 |
|---|---|
|[azure.mgmt.resource.features][1]|AFEC(Azure Feature Exposure Control)는 리소스 공급자가 사용자에 대한 기능 노출을 제어하는 메커니즘을 제공합니다.|
|[azure.mgmt.resource.links][2]|Azure 리소스는 서로 연결되어 논리적 관계를 형성할 수 있습니다. 서로 다른 리소스 그룹에 속한 리소스 간의 연결을 설정할 수 있습니다.|
|[azure.mgmt.resource.locks][3]|조직의 다른 사용자가 Azure 리소스를 삭제하거나 수정하지 못하도록 해당 리소스를 잠글 수 있습니다.|
|[azure.mgmt.resource.managedapplications][4]|ARM 관리되는 응용 프로그램(어플라이언스)입니다.|
|[azure.mgmt.resource.policy][5]|리소스에 대한 액세스를 관리하고 제어하려면 사용자 지정 정책을 정의하고 범위에 할당할 수 있습니다.|
|[azure.mgmt.resource.resources][6]| 리소스 및 리소스 그룹을 사용하기 위한 작업을 제공합니다.|
|[azure.mgmt.resource.subscriptions][7]|모든 리소스 그룹 및 리소스는 구독 내에 존재합니다. 이러한 작업을 통해 구독 및 테넌트에 대한 정보를 얻을 수 있습니다.|

[1]: /python/api/azure.mgmt.resource.features
[2]: /python/api/azure.mgmt.resource.links
[3]: /python/api/azure.mgmt.resource.locks
[4]: /python/api/azure.mgmt.resource.managedapplications
[5]: /python/api/azure.mgmt.resource.policy
[6]: /python/api/azure.mgmt.resource.resources
[7]: /python/api/azure.mgmt.resource.subscriptions

## <a name="install-the-libraries"></a>라이브러리 설치 
```bash
pip install azure-mgmt-resource
```

## <a name="example"></a>예제
다음 예제에서는 리소스 그룹을 만드는 방법을 보여 줍니다. 

```python
from azure.mgmt.resource import ResourceManagementClient
client = ResourceManagementClient(credentials, subscription_id)
client.resource_groups.create(RESOURCE_GROUP_NAME, {'location':'eastus'})
```

앱에서 사용할 수 있는 [Python 샘플 코드](https://azure.microsoft.com/resources/samples/?platform=python)를 추가로 탐색합니다. 