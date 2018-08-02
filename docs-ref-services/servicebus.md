---
title: Python용 Service Bus 라이브러리
description: Python용 Service Bus 클라이언트 및 관리 라이브러리에 대한 참조 설명서
keywords: Azure, Python, SDK, API, 메시지, pubsub, pub-sub, 메시지 브로커
author: lisawong19
ms.author: liwong
manager: routlaw
ms.date: 02/21/2018
ms.topic: article
ms.devlang: python
ms.service: service-bus
ms.openlocfilehash: 02c172ff1a54d060c6af36a5a5daa5dcbff8795c
ms.sourcegitcommit: e35ec475d4b9d8061d0528a93aa8e1c4b7db6c0d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/02/2018
ms.locfileid: "39418958"
---
# <a name="service-bus-libraries-for-python"></a><span data-ttu-id="7720c-104">Python용 Service Bus 라이브러리</span><span class="sxs-lookup"><span data-stu-id="7720c-104">Service Bus libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="7720c-105">개요</span><span class="sxs-lookup"><span data-stu-id="7720c-105">Overview</span></span>

<span data-ttu-id="7720c-106">Microsoft Azure Service Bus는 신뢰할 수 있는 메시지 큐 및 지속형 게시/구독 메시징을 포함하여 클라우드 기반, 메시지 지향 미들웨어 기술 집합을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="7720c-106">Microsoft Azure Service Bus supports a set of cloud-based, message-oriented middleware technologies including reliable message queuing and durable publish/subscribe messaging.</span></span> 

## <a name="install-the-libraries"></a><span data-ttu-id="7720c-107">라이브러리 설치</span><span class="sxs-lookup"><span data-stu-id="7720c-107">Install the libraries</span></span>
```bash
pip install azure-servicebus
```

## <a name="servicebus-queues"></a><span data-ttu-id="7720c-108">ServiceBus 큐</span><span class="sxs-lookup"><span data-stu-id="7720c-108">ServiceBus Queues</span></span>
<span data-ttu-id="7720c-109">ServiceBus 큐는 푸시 스타일 배달(긴 폴링 사용)을 사용하는 고급 메시징 기능이 필요한 시나리오(대규모 메시지, 메시지 순서 지정, 단일 작업 파괴적 읽기, 예정된 배달)에 유용할 수 있는 Storage 큐의 대안입니다.</span><span class="sxs-lookup"><span data-stu-id="7720c-109">ServiceBus Queues are an alternative to Storage Queues that might be useful in scenarios where more advanced messaging features are needed (larger message sizes, message ordering, single-operation destructive reads, scheduled delivery) using push-style delivery (using long polling).</span></span>

<span data-ttu-id="7720c-110">서비스에서는 공유 액세스 서명 인증 또는 ACS 인증을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7720c-110">The service can use Shared Access Signature authentication, or ACS authentication.</span></span>

<span data-ttu-id="7720c-111">2014년 8월 이후 Azure Portal을 사용하여 만든 Service Bus 네임스페이스는 더 이상 ACS 인증을 지원하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7720c-111">Service bus namespaces created using the Azure portal after August 2014 no longer support ACS authentication.</span></span> <span data-ttu-id="7720c-112">Azure SDK를 사용하여 ACS 호환 가능 네임스페이스를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7720c-112">You can create ACS compatible namespaces with the Azure SDK.</span></span>

### <a name="shared-access-signature-authentication"></a><span data-ttu-id="7720c-113">공유 액세스 서명 인증</span><span class="sxs-lookup"><span data-stu-id="7720c-113">Shared Access Signature Authentication</span></span>

<span data-ttu-id="7720c-114">공유 액세스 서명 인증을 사용하려면 다음을 사용하여 Service Bus 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7720c-114">To use Shared Access Signature authentication, create the service bus service with:</span></span>

```python
from azure.servicebus import ServiceBusService

key_name = 'RootManageSharedAccessKey' # SharedAccessKeyName from Azure portal
key_value = '' # SharedAccessKey from Azure portal
sbs = ServiceBusService(service_namespace,
                        shared_access_key_name=key_name,
                        shared_access_key_value=key_value)
```

### <a name="acs-authentication"></a><span data-ttu-id="7720c-115">ACS 인증</span><span class="sxs-lookup"><span data-stu-id="7720c-115">ACS Authentication</span></span>

<span data-ttu-id="7720c-116">ACS 인증을 사용하려면 다음을 사용하여 Service Bus 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="7720c-116">To use ACS authentication, create the service bus service with:</span></span>

```python
from azure.servicebus import ServiceBusService

account_key = '' # DEFAULT KEY from Azure portal
issuer = 'owner' # DEFAULT ISSUER from Azure portal
sbs = ServiceBusService(service_namespace,
                        account_key=account_key,
                        issuer=issuer)
```
### <a name="sending-and-receiving-messages"></a><span data-ttu-id="7720c-117">메시지 송수신</span><span class="sxs-lookup"><span data-stu-id="7720c-117">Sending and Receiving Messages</span></span>

<span data-ttu-id="7720c-118">**create\_queue** 메서드를 사용하여 큐가 존재하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7720c-118">The **create\_queue** method can be used to ensure a queue exists:</span></span>

```python
sbs.create_queue('taskqueue')
```
<span data-ttu-id="7720c-119">**send\_queue\_message** 메서드를 호출하여 큐에 메시지를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7720c-119">The **send\_queue\_message** method can then be called to insert the message into the queue:</span></span>

```python
from azure.servicebus import Message

msg = Message('Hello World!')
sbs.send_queue_message('taskqueue', msg)
```
<span data-ttu-id="7720c-120">**send\_queue\_message_batch** 메서드를 호출하여 한 번에 여러 개의 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7720c-120">The **send\_queue\_message_batch** method can then be called to send several messages at once:</span></span>

```python
from azure.servicebus import Message

msg1 = Message('Hello World!')
msg2 = Message('Hello World again!')
sbs.send_queue_message_batch('taskqueue', [msg1, msg2])
```
<span data-ttu-id="7720c-121">**receive\_queue\_message** 메서드를 호출하여 메시지를 큐에서 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7720c-121">It is then possible to call the **receive\_queue\_message** method to dequeue the message.</span></span>

```python
msg = sbs.receive_queue_message('taskqueue')
```

## <a name="servicebus-topics"></a><span data-ttu-id="7720c-122">ServiceBus 항목</span><span class="sxs-lookup"><span data-stu-id="7720c-122">ServiceBus Topics</span></span>

<span data-ttu-id="7720c-123">ServiceBus 항목은 게시/구독 시나리오를 쉽게 구현하는 ServiceBus 큐를 기반으로 하는 추상화입니다.</span><span class="sxs-lookup"><span data-stu-id="7720c-123">ServiceBus topics are an abstraction on top of ServiceBus Queues that make pub/sub scenarios easy to implement.</span></span>

<span data-ttu-id="7720c-124">**create\_topic** 메서드를 사용하여 서버 쪽 항목을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7720c-124">The **create\_topic** method can be used to create a server-side topic:</span></span>

```python
sbs.create_topic('taskdiscussion')
```
<span data-ttu-id="7720c-125">**send\_topic\_message** 메서드를 사용하여 항목에 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7720c-125">The **send\_topic\_message** method can be used to send a message to a topic:</span></span>

```python
from azure.servicebus import Message

msg = Message(b'Hello World!')
sbs.send_topic_message('taskdiscussion', msg)
```

<span data-ttu-id="7720c-126">**send\_topic\_message_batch** 메서드를 사용하여 한 번에 여러 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7720c-126">The **send\_topic\_message_batch** method can be used to send several messages at once:</span></span>

```python
from azure.servicebus import Message

msg1 = Message(b'Hello World!')
msg2 = Message(b'Hello World again!')
sbs.send_topic_message_batch('taskdiscussion', [msg1, msg2])
```

<span data-ttu-id="7720c-127">Python 3에서 문자열 메시지는 utf-8로 인코딩되고 Python 2에서 인코딩을 직접 관리해야 한다는 점을 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="7720c-127">Please consider that in Python 3 a str message will be utf-8 encoded and you should have to manage your encoding yourself in Python 2.</span></span>

<span data-ttu-id="7720c-128">클라이언트가 구독을 만들고 **create\_subscription** 메서드 및 **receive\_subscription\_message** 메서드를 호출하여 메시지를 사용하기 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7720c-128">A client can then create a subscription and start consuming messages by calling the **create\_subscription** method followed by the **receive\_subscription\_message** method.</span></span> <span data-ttu-id="7720c-129">구독을 만들기 전에 전송된 모든 메시지는 수신되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7720c-129">Please note that any messages sent before the subscription is created will not be received.</span></span>

```python
from azure.servicebus import Message

sbs.create_subscription('taskdiscussion', 'client1')
msg = Message('Hello World!')
sbs.send_topic_message('taskdiscussion', msg)
msg = sbs.receive_subscription_message('taskdiscussion', 'client1')
```

## <a name="event-hub"></a><span data-ttu-id="7720c-130">이벤트 허브</span><span class="sxs-lookup"><span data-stu-id="7720c-130">Event Hub</span></span>

<span data-ttu-id="7720c-131">Event Hubs를 통해 다양한 장치 및 서비스 집합에서 높은 처리량으로 이벤트 스트림을 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7720c-131">Event Hubs enable the collection of event streams at high throughput, from a diverse set of devices and services.</span></span>

<span data-ttu-id="7720c-132">**create\_event\_hub** 메서드를 사용하여 Event Hub를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7720c-132">The **create\_event\_hub** method can be used to create an event hub:</span></span>

```python
sbs.create_event_hub('myhub')
```
<span data-ttu-id="7720c-133">이벤트를 보내려면:</span><span class="sxs-lookup"><span data-stu-id="7720c-133">To send an event:</span></span>

```python
sbs.send_event('myhub', '{ "DeviceId":"dev-01", "Temperature":"37.0" }')
```
<span data-ttu-id="7720c-134">이벤트 내용은 여러 메시지를 포함하는 이벤트 메시지 또는 JSON 인코딩 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="7720c-134">The event content is the event message or JSON-encoded string that contains multiple messages.</span></span>

## <a name="advanced-features"></a><span data-ttu-id="7720c-135">고급 기능</span><span class="sxs-lookup"><span data-stu-id="7720c-135">Advanced features</span></span>

### <a name="broker-properties-and-user-properties"></a><span data-ttu-id="7720c-136">Broker 속성 및 사용자 속성</span><span class="sxs-lookup"><span data-stu-id="7720c-136">Broker Properties and User Properties</span></span>

<span data-ttu-id="7720c-137">이 섹션에서는 [여기](https://docs.microsoft.com/rest/api/servicebus/message-headers-and-properties)에 정의된 Broker 및 사용자 속성을 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="7720c-137">This section describes how to use Broker and User properties defined [here](https://docs.microsoft.com/rest/api/servicebus/message-headers-and-properties):</span></span>

```python
sent_msg = Message(b'This is the third message',
                    broker_properties={'Label': 'M3'},
                    custom_properties={'Priority': 'Medium',
                                        'Customer': 'ABC'}
            )
```
<span data-ttu-id="7720c-138">날짜/시간, int, 부동 또는 부울 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7720c-138">You can use datetime, int, float or boolean</span></span>

```python
props = {'hello': 'world',
            'number': 42,
            'active': True,
            'deceased': False,
            'large': 8555111000,
            'floating': 3.14,
            'dob': datetime(2011, 12, 14),
            'double_quote_message': 'This "should" work fine',
            'quote_message': "This 'should' work fine"}
sent_msg = Message(b'message with properties', custom_properties=props)
```
<span data-ttu-id="7720c-139">이 라이브러리의 이전 버전과 호환성 이유로 `broker_properties`를 JSON 문자열로 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="7720c-139">For compatibility reason with old version of this library, `broker_properties` could also be defined as a JSON string.</span></span>
<span data-ttu-id="7720c-140">이 경우에 유효한 JSON 문자열을 작성해야 합니다. RestAPI에 보내기 전에 Python에서 검사하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="7720c-140">If this situation, you're responsible to write a valid JSON string, no check will be made by Python before sending to the RestAPI.</span></span>

```python
broker_properties = '{"ForcePersistence": false, "Label": "My label"}'
sent_msg = Message(b'receive message',
                    broker_properties = broker_properties
)
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="7720c-141">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="7720c-141">Explore the Management APIs</span></span>](/python/api/overview/azure/servicebus/management)
