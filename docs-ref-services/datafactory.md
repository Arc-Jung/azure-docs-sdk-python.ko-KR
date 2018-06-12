---
title: Python용 Azure Data Factory 라이브러리
description: Python용 Azure Data Factory 라이브러리에 대한 참조
author: rloutlaw
ms.author: routlaw
manager: angerobe
ms.date: 05/10/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 05d93f7d1838c110c3ba77f7abd3967f7870774b
ms.sourcegitcommit: d65549030a0edb50d75482f79aac0962d1dacb57
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/05/2018
ms.locfileid: "34759054"
---
# <a name="azure-data-factory-libraries-for-python"></a>Python용 Azure Data Factory 라이브러리

[Azure Data Factory](/azure/data-factory/)로 데이터 저장, 이동 및 처리 서비스를 자동화된 데이터 파이프라인으로 만들어 보세요.

Data Factory에 대해 [자세히 알아보고](/azure/data-factory/introduction) [ Python 퀵스타트를 사용하여 데이터 팩터리 및 파이프라인 만들기](/azure/data-factory/quickstart-create-data-factory-python)를 시작합니다. 

## <a name="management-module"></a>관리 모듈

관리 모듈을 사용하여 구독의 Data Factory 인스턴스를 만들고 관리합니다.

### <a name="installation"></a>설치

[pip](https://pip.pypa.io/en/stable/quickstart/)를 사용하여 패키지 설치합니다.

```bash
pip install azure-mgmt-datafactory 
```

### <a name="example"></a>예 

미국 동부 지역의 귀하의 구독 내에 Data Factory를 만듭니다.

```python
from azure.common.credentials import ServicePrincipalCredentials
from azure.mgmt.resource import ResourceManagementClient
from azure.mgmt.datafactory import DataFactoryManagementClient
from azure.mgmt.datafactory.models import *
import time

#Create a data factory
subscription_id = '<Specify your Azure Subscription ID>'
credentials = ServicePrincipalCredentials(client_id='<Active Directory application/client ID>', secret='<client secret>', tenant='<Active Directory tenant ID>')
adf_client = DataFactoryManagementClient(credentials, subscription_id)

rg_params = {'location':'eastus'}
df_params = {'location':'eastus'}  

df_resource = Factory(location='eastus')
df = adf_client.factories.create_or_update(rg_name, df_name, df_resource)
print_item(df)
while df.provisioning_state != 'Succeeded':
    df = adf_client.factories.get(rg_name, df_name)
    time.sleep(1)
```

> [!div class="nextstepaction"]
> [관리 API 탐색](/python/api/overview/azure/datafactory/management)