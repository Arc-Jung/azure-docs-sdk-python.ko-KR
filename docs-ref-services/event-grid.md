---
title: "Python용 Azure Event Grid 라이브러리"
description: 
keywords: Azure, Python, SDK, API, Event Grid
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 08/21/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: event-grid
ms.openlocfilehash: a50a203a0733f25f2a88d6f4a43c6bddc388d3e7
ms.sourcegitcommit: 79afc8a1b427e26ecea7bdc0b7b3c898f143360f
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 09/14/2017
---
# <a name="event-grid-libraries-for-python"></a>Python용 Event Grid 라이브러리

## <a name="overview"></a>개요
Azure Event Grid는 게시-구독 모델을 사용하여 균일한 이벤트 소비를 허용하는 완전히 관리되는 지능형 이벤트 라우팅 서비스입니다.

## <a name="management-api"></a>관리 API
```bash
pip install azure-mgmt-eventgrid
```

### <a name="example"></a>예제
다음 예제에서는 사용자 지정 토픽을 만들고, 토픽을 구독하고, 이벤트를 트리거하여 결과를 봅니다. RequestBin은 오픈 소스이면서 타사 도구로, 이 도구를 통해 끝점을 만들고 끝점에 전송된 요청을 볼 수 있습니다. [RequestBin](https://requestb.in/)으로 이동하고 **RequestBin 만들기**를 클릭합니다. 토픽을 구독할 때 필요하기 때문에 bin URL을 복사합니다.

```python
from azure.mgmt.resource import ResourceManagementClient
from azure.mgmt.eventgrid import EventGridManagementClient
import requests

RESOURCE_GROUP_NAME = 'gridResourceGroup'
TOPIC_NAME = 'gridTopic1234'
LOCATION = 'westus2'
SUBSCRIPTION_ID = 'YOUR_SUBSCRIPTION_ID'
SUBSCRIPTION_NAME = 'gridSubscription'
REQUEST_BIN_URL = 'YOUR_REQUEST_BIN_URL'

# create resource group
resource_client = ResourceManagementClient(credentials, SUBSCRIPTION_ID)
resource_client.resource_groups.create_or_update(
    RESOURCE_GROUP_NAME,
    {
        'location': LOCATION
    }
)

event_client = EventGridManagementClient(credentials, SUBSCRIPTION_ID)

# create a custom topic
event_client.topics.create_or_update(RESOURCE_GROUP_NAME, TOPIC_NAME, LOCATION)

# subscribe to a topic
scope = '/subscriptions/'+SUBSCRIPTION_ID+'/resourceGroups/'+RESOURCE_GROUP_NAME+'/providers/Microsoft.EventGrid/topics/'+TOPIC_NAME
event_client.event_subscriptions.create(scope, SUBSCRIPTION_NAME,
    {
        'destination': {
            'endpoint_url': REQUEST_BIN_URL
        }
    }
)

# send an event to topic
# get endpoint url
url = event_client.event_subscriptions.get_full_url(scope, SUBSCRIPTION_NAME).endpoint_url
# get key
key = event_client.topics.list_shared_access_keys(RESOURCE_GROUP_NAME,TOPIC_NAME).key1
headers = {'aeg-sas-key': key}
s = requests.get('https://raw.githubusercontent.com/Azure/azure-docs-json-samples/master/event-grid/customevent.json')
r = requests.post(url, data=s, headers=headers)
print(r.status_code)
print(r.content)
```
앞에서 만든 RequestBin URL로 이동하여 방금 보낸 이벤트를 확인합니다.

리소스 정리
```azurecli-interactive
az group delete --name gridResourceGroup
```

> [!div class="nextstepaction"]
> [관리 API 탐색](/python/api/overview/azure/eventgrid/managementlibrary)

