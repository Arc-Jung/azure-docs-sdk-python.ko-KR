---
title: Python용 Azure Event Grid 라이브러리
description: ''
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
ms.openlocfilehash: e68504b3ba5834a145af1231eacc076e424a2256
ms.sourcegitcommit: 560362db0f65307c8b02b7b7ad8642b5c4aa6294
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/08/2018
---
# <a name="event-grid-libraries-for-python"></a>Python용 Event Grid 라이브러리


Azure Event Grid는 게시-구독 모델을 사용하여 균일한 이벤트 소비를 허용하는 완전히 관리되는 지능형 이벤트 라우팅 서비스입니다.

Azure Event Grid에 대해 [자세히 알아보고](/azure/event-grid/overview), [Azure Blob 저장소 이벤트 자습서](/azure/storage/blobs/storage-blob-event-quickstart)를 시작합니다. 

## <a name="publish-sdk"></a>SDK 게시

Azure Event Grid Publish SDK를 사용하여 토픽에 이벤트를 인증하고 만들고 처리하고 게시합니다.

### <a name="installation"></a>설치 

[pip](https://pip.pypa.io/en/stable/quickstart/)를 사용하여 패키지 설치합니다.

```bash
pip install azure-eventgrid
```

### <a name="example"></a>예 

다음 코드는 토픽에 이벤트를 게시합니다. Azure Portal 또는 Azure CLI를 통해 토픽 키 및 엔트포인트를 검색할 수 있습니다.

```azurecli-interactive
endpoint=$(az eventgrid topic show --name <topic_name> -g gridResourceGroup --query "endpoint" --output tsv)
key=$(az eventgrid topic key list --name <topic_name> -g gridResourceGroup --query "key1" --output tsv)
```

```python
from datetime import datetime
from azure.eventgrid import EventGridClient
from msrest.authentication import TopicCredentials

def publish_event(self):

        credentials = TopicCredentials(
            self.settings.EVENT_GRID_KEY
        )
        event_grid_client = EventGridClient(credentials)
        event_grid_client.publish_events(
            "your-endpoint-here",
            events=[{
                'id' : "dbf93d79-3859-4cac-8055-51e3b6b54bea",
                'subject' : "Sample subject",
                'data': {
                    'key': 'Sample Data'
                },
                'event_type': 'SampleEventType',
                'event_time': datetime(2018, 5, 2),
                'data_version': 1
            }]
        )
```

> [!div class="nextstepaction"]
> [클라이언트 API 탐색](/python/api/overview/azure/eventgrid/client)

## <a name="management-sdk"></a>관리 SDK

관리 SDK를 사용하여 Event Grid 인스턴스, 토픽 및 구독을 만들고 업데이트하거나 삭제합니다.

### <a name="installation"></a>설치 

[pip](https://pip.pypa.io/en/stable/quickstart/)를 사용하여 패키지 설치합니다.

```bash
pip install azure-mgmt-eventgrid
```

### <a name="example"></a>예

다음에서는 사용자 지정 토픽을 만들고 해당 토픽에 엔트포인트를 등록합니다. 그런 다음, 코드는 HTTPS를 통해 토픽에 이벤트를 보냅니다.
RequestBin은 오픈 소스이면서 타사 도구로, 이 도구를 통해 끝점을 만들고 끝점에 전송된 요청을 볼 수 있습니다. [RequestBin](https://requestb.in/)으로 이동하고 **RequestBin 만들기**를 클릭합니다. 토픽을 구독할 때 필요하기 때문에 bin URL을 복사합니다.

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
> [관리 API 탐색](/python/api/overview/azure/eventgrid/management)

## <a name="learn-more"></a>자세한 정보

[Event Grid SDK를 사용하여 이벤트 수신](/azure/event-grid/receive-events)