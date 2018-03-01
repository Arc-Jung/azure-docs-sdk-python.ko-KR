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
ms.openlocfilehash: 299b50ce8366d0c49ade28dfece98d6696a4f9ef
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/23/2018
---
# <a name="event-grid-libraries-for-python"></a><span data-ttu-id="d72e9-103">Python용 Event Grid 라이브러리</span><span class="sxs-lookup"><span data-stu-id="d72e9-103">Event Grid libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="d72e9-104">개요</span><span class="sxs-lookup"><span data-stu-id="d72e9-104">Overview</span></span>
<span data-ttu-id="d72e9-105">Azure Event Grid는 게시-구독 모델을 사용하여 균일한 이벤트 소비를 허용하는 완전히 관리되는 지능형 이벤트 라우팅 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="d72e9-105">Azure Event Grid is a fully-managed intelligent event routing service that allows for uniform event consumption using a publish-subscribe model.</span></span>

## <a name="management-api"></a><span data-ttu-id="d72e9-106">관리 API</span><span class="sxs-lookup"><span data-stu-id="d72e9-106">Management API</span></span>
```bash
pip install azure-mgmt-eventgrid
```

### <a name="example"></a><span data-ttu-id="d72e9-107">예</span><span class="sxs-lookup"><span data-stu-id="d72e9-107">Example</span></span>
<span data-ttu-id="d72e9-108">다음 예제에서는 사용자 지정 토픽을 만들고, 토픽을 구독하고, 이벤트를 트리거하여 결과를 봅니다.</span><span class="sxs-lookup"><span data-stu-id="d72e9-108">The following creates a custom topic, subscribes to the topic, and triggers the event to view the result.</span></span> <span data-ttu-id="d72e9-109">RequestBin은 오픈 소스이면서 타사 도구로, 이 도구를 통해 끝점을 만들고 끝점에 전송된 요청을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="d72e9-109">RequestBin is an open source, third-party tool that enables you to create an endpoint, and view requests that are sent to it.</span></span> <span data-ttu-id="d72e9-110">[RequestBin](https://requestb.in/)으로 이동하고 **RequestBin 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="d72e9-110">Go to [RequestBin](https://requestb.in/), and click **Create a RequestBin**.</span></span> <span data-ttu-id="d72e9-111">토픽을 구독할 때 필요하기 때문에 bin URL을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="d72e9-111">Copy the bin URL, because you need it when subscribing to the topic.</span></span>

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
<span data-ttu-id="d72e9-112">앞에서 만든 RequestBin URL로 이동하여 방금 보낸 이벤트를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="d72e9-112">Browse to the RequestBin URL created earlier to see the event just sent.</span></span>

<span data-ttu-id="d72e9-113">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="d72e9-113">Clean up resources</span></span>
```azurecli-interactive
az group delete --name gridResourceGroup
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="d72e9-114">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="d72e9-114">Explore the Management APIs</span></span>](/python/api/overview/azure/eventgrid/management)

