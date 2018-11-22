---
title: Python용 Azure Event Grid 라이브러리
description: ''
keywords: Azure, Python, SDK, API, Event Grid
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 08/21/2017
ms.topic: article
ms.devlang: python
ms.service: event-grid
ms.openlocfilehash: bfaa1908295eb77531e399f1337acdeee512005f
ms.sourcegitcommit: f439ba940d5940359c982015db7ccfb82f9dffd9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2018
ms.locfileid: "52276837"
---
# <a name="event-grid-libraries-for-python"></a><span data-ttu-id="20616-103">Python용 Event Grid 라이브러리</span><span class="sxs-lookup"><span data-stu-id="20616-103">Event Grid libraries for Python</span></span>


<span data-ttu-id="20616-104">Azure Event Grid는 게시-구독 모델을 사용하여 균일한 이벤트 소비를 허용하는 완전히 관리되는 지능형 이벤트 라우팅 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="20616-104">Azure Event Grid is a fully-managed intelligent event routing service that allows for uniform event consumption using a publish-subscribe model.</span></span>

<span data-ttu-id="20616-105">Azure Event Grid에 대해 [자세히 알아보고](/azure/event-grid/overview), [Azure Blob 저장소 이벤트 자습서](/azure/storage/blobs/storage-blob-event-quickstart)를 시작합니다.</span><span class="sxs-lookup"><span data-stu-id="20616-105">[Learn more](/azure/event-grid/overview) about Azure Event Grid and get started with the [Azure Blob storage event tutorial](/azure/storage/blobs/storage-blob-event-quickstart).</span></span> 

## <a name="publish-sdk"></a><span data-ttu-id="20616-106">SDK 게시</span><span class="sxs-lookup"><span data-stu-id="20616-106">Publish SDK</span></span>

<span data-ttu-id="20616-107">Azure Event Grid Publish SDK를 사용하여 토픽에 이벤트를 인증하고 만들고 처리하고 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="20616-107">Authenticate, create, handle, and publish events to topics using the Azure Event Grid publish SDK.</span></span>

### <a name="installation"></a><span data-ttu-id="20616-108">설치</span><span class="sxs-lookup"><span data-stu-id="20616-108">Installation</span></span> 

<span data-ttu-id="20616-109">[pip](https://pip.pypa.io/en/stable/quickstart/)를 사용하여 패키지 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="20616-109">Install the package with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```bash
pip install azure-eventgrid
```

### <a name="example"></a><span data-ttu-id="20616-110">예</span><span class="sxs-lookup"><span data-stu-id="20616-110">Example</span></span> 

<span data-ttu-id="20616-111">다음 코드는 토픽에 이벤트를 게시합니다.</span><span class="sxs-lookup"><span data-stu-id="20616-111">The following code publishes an event to a topic.</span></span> <span data-ttu-id="20616-112">Azure Portal 또는 Azure CLI를 통해 토픽 키 및 엔트포인트를 검색할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20616-112">You can retrieve the topic key and endpoint through the Azure Portal or through the Azure CLI:</span></span>

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
> [<span data-ttu-id="20616-113">클라이언트 API 탐색</span><span class="sxs-lookup"><span data-stu-id="20616-113">Explore the Client APIs</span></span>](/python/api/overview/azure/eventgrid/client)

## <a name="management-sdk"></a><span data-ttu-id="20616-114">관리 SDK</span><span class="sxs-lookup"><span data-stu-id="20616-114">Management SDK</span></span>

<span data-ttu-id="20616-115">관리 SDK를 사용하여 Event Grid 인스턴스, 토픽 및 구독을 만들거나 업데이트하거나 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="20616-115">Create, update, or delete Event Grid instances, topics, and subscriptions with the management SDK.</span></span>

### <a name="installation"></a><span data-ttu-id="20616-116">설치</span><span class="sxs-lookup"><span data-stu-id="20616-116">Installation</span></span> 

<span data-ttu-id="20616-117">[pip](https://pip.pypa.io/en/stable/quickstart/)를 사용하여 패키지 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="20616-117">Install the package with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```bash
pip install azure-mgmt-eventgrid
```

### <a name="example"></a><span data-ttu-id="20616-118">예</span><span class="sxs-lookup"><span data-stu-id="20616-118">Example</span></span>

<span data-ttu-id="20616-119">다음에서는 사용자 지정 토픽을 만들고 해당 토픽에 엔트포인트를 등록합니다.</span><span class="sxs-lookup"><span data-stu-id="20616-119">The following creates a custom topic and subscribes an endpoint to the topic.</span></span> <span data-ttu-id="20616-120">그런 다음, 코드는 HTTPS를 통해 토픽에 이벤트를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="20616-120">The code then sends an event to the topic through HTTPS.</span></span>
<span data-ttu-id="20616-121">RequestBin은 오픈 소스이면서 타사 도구로, 이 도구를 통해 엔드포인트를 만들고 엔드포인트에 전송된 요청을 볼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="20616-121">RequestBin is an open source, third-party tool that enables you to create an endpoint, and view requests that are sent to it.</span></span> <span data-ttu-id="20616-122">[RequestBin](https://requestb.in/)으로 이동하고 **RequestBin 만들기**를 클릭합니다.</span><span class="sxs-lookup"><span data-stu-id="20616-122">Go to [RequestBin](https://requestb.in/), and click **Create a RequestBin**.</span></span> <span data-ttu-id="20616-123">토픽을 구독할 때 필요하기 때문에 bin URL을 복사합니다.</span><span class="sxs-lookup"><span data-stu-id="20616-123">Copy the bin URL, because you need it when subscribing to the topic.</span></span>

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
<span data-ttu-id="20616-124">앞에서 만든 RequestBin URL로 이동하여 방금 보낸 이벤트를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="20616-124">Browse to the RequestBin URL created earlier to see the event just sent.</span></span>

<span data-ttu-id="20616-125">리소스 정리</span><span class="sxs-lookup"><span data-stu-id="20616-125">Clean up resources</span></span>
```azurecli-interactive
az group delete --name gridResourceGroup
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="20616-126">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="20616-126">Explore the Management APIs</span></span>](/python/api/overview/azure/eventgrid/management)

## <a name="learn-more"></a><span data-ttu-id="20616-127">자세한 정보</span><span class="sxs-lookup"><span data-stu-id="20616-127">Learn more</span></span>

[<span data-ttu-id="20616-128">Event Grid SDK를 사용하여 이벤트 수신</span><span class="sxs-lookup"><span data-stu-id="20616-128">Receive events using the Event Grid SDK</span></span>](/azure/event-grid/receive-events)
