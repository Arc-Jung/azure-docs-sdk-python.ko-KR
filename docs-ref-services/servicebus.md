---
title: Python용 Service Bus 라이브러리
description: Python용 Service Bus 클라이언트 및 관리 라이브러리에 대한 참조 설명서
keywords: Azure, Python, SDK, API, 메시지, pubsub, pub-sub, 메시지 브로커
author: annatisch
ms.author: antisch
manager: mayurid
ms.date: 01/15/2019
ms.topic: article
ms.devlang: python
ms.service: service-bus
ms.openlocfilehash: 014f34b6ba3d3a2a8ce15afcd826195d6051f98a
ms.sourcegitcommit: 434186988284e0a8268a9de11645912a81226d6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/29/2019
ms.locfileid: "66376761"
---
# <a name="service-bus-libraries-for-python"></a><span data-ttu-id="30c07-104">Python용 Service Bus 라이브러리</span><span class="sxs-lookup"><span data-stu-id="30c07-104">Service Bus libraries for Python</span></span>

<span data-ttu-id="30c07-105">Microsoft Azure Service Bus는 신뢰할 수 있는 메시지 큐 및 지속형 게시/구독 메시징을 포함하여 클라우드 기반, 메시지 지향 미들웨어 기술 집합을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-105">Microsoft Azure Service Bus supports a set of cloud-based, message-oriented middleware technologies including reliable message queuing and durable publish/subscribe messaging.</span></span>

* [<span data-ttu-id="30c07-106">SDK 소스 코드</span><span class="sxs-lookup"><span data-stu-id="30c07-106">SDK source code</span></span>](https://github.com/Azure/azure-sdk-for-python/tree/master/azure-servicebus)
* [<span data-ttu-id="30c07-107">SDK 참조 설명서</span><span class="sxs-lookup"><span data-stu-id="30c07-107">SDK reference documentation</span></span>](https://docs.microsoft.com/python/api/overview/azure/servicebus/client?view=azure-python)

## <a name="whats-new-in-v0500"></a><span data-ttu-id="30c07-108">v0.50.0의 새로운 기능</span><span class="sxs-lookup"><span data-stu-id="30c07-108">What's new in v0.50.0?</span></span>

<span data-ttu-id="30c07-109">0.50.0 버전부터 새 AMQP 기반 API는 메시지 보내기 및 받기를 할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-109">As of version 0.50.0 a new AMQP-based API is available for sending and receiving messages.</span></span> <span data-ttu-id="30c07-110">이 업데이트는 **호환성이 손상되는 변경**을 포함합니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-110">This update involves **breaking changes**.</span></span>

<span data-ttu-id="30c07-111">현 시점에서 업그레이드가 적합한지 판단하려면 [v0.21.1에서 v0.50.0로 마이그레이션](#migration-from-v0211-to-v0500)을 읽어보세요.</span><span class="sxs-lookup"><span data-stu-id="30c07-111">Please read [Migration from v0.21.1 to v0.50.0](#migration-from-v0211-to-v0500) to determine if upgrading is right for you at this time.</span></span>

<span data-ttu-id="30c07-112">새로운 AMQP 기반 API는 향상된 메시지 전달 신뢰성, 성능 및 향후 확장된 기능 지원을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-112">The new AMQP-based API offers improved message passing reliability, performance and expanded feature support going forward.</span></span>
<span data-ttu-id="30c07-113">새로운 API는 또한 메시지를 보내고 받고 처리하는 비동기 작업(asyncio 기반)을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-113">The new API also offers support for asynchronous operations (based on asyncio) for sending, receiving and handling messages.</span></span>

<span data-ttu-id="30c07-114">레거시 HTTP 기반 작업에 대한 문서는 [레거시 API의 HTTP 기반 작업 사용](#using-http-based-operations-of-the-legacy-api)을 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="30c07-114">For documentation on the legacy HTTP-based operations please see [Using HTTP-based operations of the legacy API](#using-http-based-operations-of-the-legacy-api).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="30c07-115">필수 조건</span><span class="sxs-lookup"><span data-stu-id="30c07-115">Prerequisites</span></span>

* <span data-ttu-id="30c07-116">Azure 구독 -[체험 계정 만들기](https://azure.microsoft.com/free/)</span><span class="sxs-lookup"><span data-stu-id="30c07-116">Azure subscription - [Create a free account](https://azure.microsoft.com/free/)</span></span>
* <span data-ttu-id="30c07-117">Azure [Service Bus 네임스페이스 및 관리 자격 증명](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-create-namespace-portal)</span><span class="sxs-lookup"><span data-stu-id="30c07-117">Azure [Service Bus namespace and management credentials](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-create-namespace-portal)</span></span>
* [<span data-ttu-id="30c07-118">Python 2.7-3.7</span><span class="sxs-lookup"><span data-stu-id="30c07-118">Python 2.7-3.7</span></span>](https://www.python.org/downloads/)

## <a name="installation"></a><span data-ttu-id="30c07-119">설치</span><span class="sxs-lookup"><span data-stu-id="30c07-119">Installation</span></span>

```bash
pip install azure-servicebus
```

## <a name="connect-to-azure-service-bus"></a><span data-ttu-id="30c07-120">Azure Service Bus에 연결</span><span class="sxs-lookup"><span data-stu-id="30c07-120">Connect to Azure Service Bus</span></span>

### <a name="get-credentials"></a><span data-ttu-id="30c07-121">자격 증명 가져오기</span><span class="sxs-lookup"><span data-stu-id="30c07-121">Get credentials</span></span>

<span data-ttu-id="30c07-122">아래 Azure CLI 조각을 사용하여 Service Bus 연결 문자열로 환경 변수를 채웁니다(Azure Portal에서도 이 값을 찾을 수 있습니다).</span><span class="sxs-lookup"><span data-stu-id="30c07-122">Use the Azure CLI snippet below to populate an environment variable with the Service Bus connection string (you can also find this value in the Azure portal).</span></span> <span data-ttu-id="30c07-123">조각은 Bash 셸에 대해 서식이 지정됩니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-123">The snippet is formatted for the Bash shell.</span></span>

```Bash
RES_GROUP=<resource-group-name>
NAMESPACE=<servicebus-namespace>

export SB_CONN_STR=$(az servicebus namespace authorization-rule keys list \
 --resource-group $RES_GROUP \
 --namespace-name $NAMESPACE \
 --name RootManageSharedAccessKey \
 --query primaryConnectionString \
 --output tsv)
```

### <a name="create-client"></a><span data-ttu-id="30c07-124">클라이언트 만들기</span><span class="sxs-lookup"><span data-stu-id="30c07-124">Create client</span></span>

<span data-ttu-id="30c07-125">`SB_CONN_STR` 환경 변수를 채우면 ServiceBusClient를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-125">Once you've populated the `SB_CONN_STR` environment variable, you can create the ServiceBusClient.</span></span>

```python
import os
from azure.servicebus import ServiceBusClient

connection_str = os.environ['SB_CONN_STR']

sb_client = ServiceBusClient.from_connection_string(connection_str)
```

<span data-ttu-id="30c07-126">비동기 작업을 사용하려는 경우 `azure.servicebus.aio` 네임스페이스를 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-126">If you wish to use asynchronous operations, please use the `azure.servicebus.aio` namespace.</span></span>

```python
import os
from azure.servicebus.aio import ServiceBusClient

connection_str = os.environ['SB_CONN_STR']

sb_client = ServiceBusClient.from_connection_string(connection_str)
```

## <a name="service-bus-queues"></a><span data-ttu-id="30c07-127">Service Bus 큐</span><span class="sxs-lookup"><span data-stu-id="30c07-127">Service Bus queues</span></span>

<span data-ttu-id="30c07-128">Service Bus 큐는 푸시 스타일 배달(긴 폴링 사용)을 사용하는 고급 메시징 기능이 필요한 시나리오(대규모 메시지, 메시지 순서 지정, 단일 작업 파괴적 읽기, 예정된 배달)에 유용할 수 있는 Storage 큐의 대안입니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-128">Service Bus queues are an alternative to Storage queues that might be useful in scenarios where more advanced messaging features are needed (larger message sizes, message ordering, single-operation destructive reads, scheduled delivery) using push-style delivery (using long polling).</span></span>

### <a name="create-queue"></a><span data-ttu-id="30c07-129">큐 만들기</span><span class="sxs-lookup"><span data-stu-id="30c07-129">Create queue</span></span>

<span data-ttu-id="30c07-130">이는 Service Bus 네임스페이스 내에서 새 큐를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-130">This creates a new queue within the Service Bus namespace.</span></span> <span data-ttu-id="30c07-131">네임스페이스 내에 같은 이름의 큐가 이미 있으면 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-131">If a queue of the same name already exists within the namespace an error will be raised.</span></span>

```python
sb_client.create_queue("MyQueue")
```

<span data-ttu-id="30c07-132">큐 동작을 구성하는 선택적 매개 변수를 지정할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-132">Optional parameters to configure the queue behavior can also be specified.</span></span>

```python
sb_client.create_queue(
    "MySessionQueue",
    requires_session=True  # Create a sessionful queue
    max_delivery_count=5  # Max delivery attempts per message
)
```

### <a name="get-a-queue-client"></a><span data-ttu-id="30c07-133">큐 클라이언트 가져오기</span><span class="sxs-lookup"><span data-stu-id="30c07-133">Get a queue client</span></span>

<span data-ttu-id="30c07-134">QueueClient는 다른 작업과 함께 큐와 메시지를 주고 받고 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-134">A QueueClient can be used to send and receive messages from the queue, along with other operations.</span></span>

```python
queue_client = sb_client.get_queue("MyQueue")
```

### <a name="sending-messages"></a><span data-ttu-id="30c07-135">메시지 보내기</span><span class="sxs-lookup"><span data-stu-id="30c07-135">Sending messages</span></span>

<span data-ttu-id="30c07-136">큐 클라이언트는 한 번에 하나 이상의 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-136">The queue client can send one or more messages at a time:</span></span>

```python
from azure.servicebus import Message

message = Message("Hello World")
queue_client.send(message)

message_one = Message("First")
message_two = Message("Second")
queue_client.send([message_one, message_two])
```

<span data-ttu-id="30c07-137">QueueClient.send를 호출할 때마다 새 서비스 연결을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-137">Each call to QueueClient.send will create a new service connection.</span></span> <span data-ttu-id="30c07-138">여러 호출에 전송에 동일한 연결을 다시 사용하려면 발신자를 열 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-138">To reuse the same connection for multiple send calls, you can open a sender:</span></span>

```python
message_one = Message("First")
message_two = Message("Second")

with queue_client.get_sender() as sender:
    sender.send(message_one)
    sender.send(message_two)
```

<span data-ttu-id="30c07-139">비동기 클라이언트를 사용하는 경우 위의 작업은 비동기 구문을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-139">If you are using an asynchronous client, the above operations will use async syntax:</span></span>

```python
from azure.servicebus.aio import Message

message = Message("Hello World")
await queue_client.send(message)

message_one = Message("First")
message_two = Message("Second")
async with queue_client.get_sender() as sender:
    await sender.send(message_one)
    await sender.send(message_two)
```

### <a name="receiving-messages"></a><span data-ttu-id="30c07-140">메시지 수신</span><span class="sxs-lookup"><span data-stu-id="30c07-140">Receiving messages</span></span>

<span data-ttu-id="30c07-141">연속 반복기로 큐에서 메시지를 받을 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-141">Messages can be received from a queue as a continuous iterator.</span></span> <span data-ttu-id="30c07-142">메시지 수신을 위한 기본 모드는 [PeekLock](https://docs.microsoft.com/rest/api/servicebus/peek-lock-message-non-destructive-read)이며 각 메시지는 큐에서 제거되도록 명시적으로 완료해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-142">The default mode for message receiving is [PeekLock](https://docs.microsoft.com/rest/api/servicebus/peek-lock-message-non-destructive-read), which requires each message to be explicitly completed in order that it be removed from the queue.</span></span>

```python
messages = queue_client.get_receiver()
for message in messages:
    print(message)
    message.complete()
```

<span data-ttu-id="30c07-143">서비스 연결은 전체 반복기에 대해 계속 열려 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-143">The service connection will remain open for the entirety of the iterator.</span></span> <span data-ttu-id="30c07-144">메시지 스트림을 부분적으로만 반복하는 경우 `with` 문에서 수신자를 실행하여 연결이 닫혔는지 확인해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-144">If you find yourself only partially iterating the message stream, you should run the receiver in a `with` statement to ensure the connection is closed:</span></span>

```python
with queue_client.get_receiver() as messages:
    for message in messages:
        print(message)
        message.complete()
        break
```
<span data-ttu-id="30c07-145">비동기 클라이언트를 사용하는 경우 위의 작업은 비동기 구문을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-145">If you are using an asynchronous client, the above operations will use async syntax:</span></span>

```python
async with queue_client.get_receiver() as messages:
    async for message in messages:
        print(message)
        await message.complete()
        break
```

## <a name="service-bus-topics-and-subscriptions"></a><span data-ttu-id="30c07-146">Service Bus 토픽 및 구독</span><span class="sxs-lookup"><span data-stu-id="30c07-146">Service Bus topics and subscriptions</span></span>

<span data-ttu-id="30c07-147">Service Bus 토픽 및 구독은 Service Bus 큐 위의 추상화로서 게시/구독 패턴으로 일 대 다 형태의 통신을 제공합니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-147">Service Bus topics and subscriptions are an abstraction on top of Service Bus queues that provide a one-to-many form of communication, in a publish/subscribe pattern.</span></span> <span data-ttu-id="30c07-148">메시지는 토픽으로 전송되어 하나 이상의 연관된 구독으로 전달되므로 많은 수의 수신자로 확장하는 데 유용합니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-148">Messages are sent to a topic and delivered to one or more associated subscriptions, which is useful for scaling to large numbers of recipients.</span></span>

### <a name="create-topic"></a><span data-ttu-id="30c07-149">토픽 만들기</span><span class="sxs-lookup"><span data-stu-id="30c07-149">Create topic</span></span>

<span data-ttu-id="30c07-150">이는 Service Bus 네임스페이스 내에서 새 토픽을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-150">This creates a new topic within the Service Bus namespace.</span></span> <span data-ttu-id="30c07-151">동일한 이름의 토픽이 이미 있으면 오류가 발생합니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-151">If a topic of the same name already exists an error will be raised.</span></span>

```python
sb_client.create_topic("MyTopic")
```

### <a name="get-a-topic-client"></a><span data-ttu-id="30c07-152">토픽 클라이언트 가져오기</span><span class="sxs-lookup"><span data-stu-id="30c07-152">Get a topic client</span></span>

<span data-ttu-id="30c07-153">다른 작업과 함께 토픽에 메시지를 보내려면 TopicClient를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-153">A TopicClient can be used to send messages to the topic, along with other operations.</span></span>

```python
topic_client = sb_client.get_topic("MyTopic")
```

### <a name="create-subscription"></a><span data-ttu-id="30c07-154">구독 만들기</span><span class="sxs-lookup"><span data-stu-id="30c07-154">Create subscription</span></span>

<span data-ttu-id="30c07-155">이는 Service Bus 네임스페이스 내에서 지정된 토픽에 대한 새 구독을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-155">This creates a new subscription for the specified topic within the Service Bus namespace.</span></span>

```python
sb_client.create_subscription("MyTopic", "MySubscription")
```

### <a name="get-a-subscription-client"></a><span data-ttu-id="30c07-156">구독 클라이언트 가져오기</span><span class="sxs-lookup"><span data-stu-id="30c07-156">Get a subscription client</span></span>

<span data-ttu-id="30c07-157">SubscriptionClient는 다른 작업과 함께 토픽에서 메시지를 받는 데 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-157">A SubscriptionClient can be used to receive messages from the topic, along with other operations.</span></span>

```python
topic_client = sb_client.get_subscription("MyTopic", "MySubscription")
```

## <a name="migration-from-v0211-to-v0500"></a><span data-ttu-id="30c07-158">v0.21.1에서 v0.50.0으로 마이그레이션</span><span class="sxs-lookup"><span data-stu-id="30c07-158">Migration from v0.21.1 to v0.50.0</span></span>

<span data-ttu-id="30c07-159">호환성이 손상되는 변경이 0.50.0 버전에 도입되었습니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-159">Major breaking changes were introduced in version 0.50.0.</span></span> <span data-ttu-id="30c07-160">원래 HTTP 기반 API는 v0.50.0에서 계속 사용할 수 있지만 이제는 새로운 네임스페이스 `azure.servicebus.control_client` 아래에 존재합니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-160">The original HTTP-based API is still available in v0.50.0 - however it now exists under a new namesapce: `azure.servicebus.control_client`.</span></span>

### <a name="should-i-upgrade"></a><span data-ttu-id="30c07-161">업그레이드해야 합니까?</span><span class="sxs-lookup"><span data-stu-id="30c07-161">Should I upgrade?</span></span>

<span data-ttu-id="30c07-162">새로운 패키지(v0.50.0)는 v0.21.1 이상의 HTTP 기반 작업을 개선하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-162">The new package (v0.50.0) offers no improvements in HTTP-based operations over v0.21.1.</span></span> <span data-ttu-id="30c07-163">HTTP 기반 API는 이제 새 네임스페이스 아래에 있다는 점을 제외하고는 동일합니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-163">The HTTP-based API is identical except that it now exists under a new namespace.</span></span> <span data-ttu-id="30c07-164">따라서 HTTP 기반 작업(`create_queue`, `delete_queue` 등)만 사용하려는 경우에는 현재 업그레이드할 때 추가 이점이 없습니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-164">For this reason if you only wish to use HTTP-based operations (`create_queue`, `delete_queue` etc) - there will be no additional benefit in upgrading at this time.</span></span>

### <a name="how-do-i-migrate-my-code-to-the-new-version"></a><span data-ttu-id="30c07-165">내 코드를 새 버전으로 마이그레이션하려면 어떻게 하나요?</span><span class="sxs-lookup"><span data-stu-id="30c07-165">How do I migrate my code to the new version?</span></span>

<span data-ttu-id="30c07-166">v0.21.0에 대해 작성된 코드는 네임스페이스 가져오기를 변경하여 버전 0.50.0으로 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-166">Code written against v0.21.0 can be ported to version 0.50.0 by simply changing the import namespace:</span></span>

```python
# from azure.servicebus import ServiceBusService  <- This will now raise an ImportError
from azure.servicebus.control_client import ServiceBusService

key_name = 'RootManageSharedAccessKey' # SharedAccessKeyName from Azure portal
key_value = '' # SharedAccessKey from Azure portal
sbs = ServiceBusService(service_namespace,
                        shared_access_key_name=key_name,
                        shared_access_key_value=key_value)
```

## <a name="using-http-based-operations-of-the-legacy-api"></a><span data-ttu-id="30c07-167">기존 API의 HTTP 기반 작업 사용하기</span><span class="sxs-lookup"><span data-stu-id="30c07-167">Using HTTP-based operations of the legacy API</span></span>

<span data-ttu-id="30c07-168">다음 문서에서는 기존 API에 대해 설명하고 있으며 추가 변경 없이 기존 코드를 v0.50.0으로 가져오려는 사용자를 위한 것입니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-168">The following documentation describes the legacy API and should be used for those wishing to port existing code to v0.50.0 without making any additional changes.</span></span> <span data-ttu-id="30c07-169">v0.21.1 사용자도 이 참조 지침을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-169">This reference can also be used as guidance by those using v0.21.1.</span></span>
<span data-ttu-id="30c07-170">새 코드 작성자들은 위에서 설명한 새로운 API를 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-170">For those writing new code, we recommend using the new API described above.</span></span>

### <a name="service-bus-queues"></a><span data-ttu-id="30c07-171">Service Bus 큐</span><span class="sxs-lookup"><span data-stu-id="30c07-171">Service Bus queues</span></span>

#### <a name="shared-access-signature-sas-authentication"></a><span data-ttu-id="30c07-172">공유 액세스 서명(SAS) 인증</span><span class="sxs-lookup"><span data-stu-id="30c07-172">Shared Access Signature (SAS) authentication</span></span>

<span data-ttu-id="30c07-173">공유 액세스 서명 인증을 사용하려면 다음을 사용하여 Service Bus 서비스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-173">To use Shared Access Signature authentication, create the service bus service with:</span></span>

```python
from azure.servicebus.control_client import ServiceBusService

key_name = 'RootManageSharedAccessKey' # SharedAccessKeyName from Azure portal
key_value = '' # SharedAccessKey from Azure portal
sbs = ServiceBusService(service_namespace,
                        shared_access_key_name=key_name,
                        shared_access_key_value=key_value)
```

#### <a name="access-control-service-acs-authentication"></a><span data-ttu-id="30c07-174">ACS(Access Control Service) 인증</span><span class="sxs-lookup"><span data-stu-id="30c07-174">Access Control Service (ACS) authentication</span></span>

<span data-ttu-id="30c07-175">ACS는 새 Service Bus 네임스페이스에서 지원되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-175">ACS is not supported on new Service Bus namespaces.</span></span> <span data-ttu-id="30c07-176">[SAS 인증으로 애플리케이션을 마이그레이션](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-migrate-acs-sas) 하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-176">We recommend [migrating applications to SAS authentication](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-migrate-acs-sas).</span></span> <span data-ttu-id="30c07-177">이전 Service Bus 네임스페이스 내에서 ACS 인증을 사용하려면 다음을 사용하여 ServiceBusService를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-177">To use ACS authentication within an older Service Bus namesapce, create the ServiceBusService with:</span></span>

```python
from azure.servicebus.control_client import ServiceBusService

account_key = '' # DEFAULT KEY from Azure portal
issuer = 'owner' # DEFAULT ISSUER from Azure portal
sbs = ServiceBusService(service_namespace,
                        account_key=account_key,
                        issuer=issuer)
```

#### <a name="sending-and-receiving-messages"></a><span data-ttu-id="30c07-178">메시지 송수신</span><span class="sxs-lookup"><span data-stu-id="30c07-178">Sending and receiving messages</span></span>

<span data-ttu-id="30c07-179">**create\_queue** 메서드를 사용하여 큐가 존재하는지 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-179">The **create\_queue** method can be used to ensure a queue exists:</span></span>

```python
sbs.create_queue('taskqueue')
```

<span data-ttu-id="30c07-180">**send\_queue\_message** 메서드를 호출하여 큐에 메시지를 삽입할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-180">The **send\_queue\_message** method can then be called to insert the message into the queue:</span></span>

```python
from azure.servicebus.control_client import Message

msg = Message('Hello World!')
sbs.send_queue_message('taskqueue', msg)
```

<span data-ttu-id="30c07-181">**send\_queue\_message_batch** 메서드를 호출하여 여러 개의 메시지를 한 번에 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-181">The **send\_queue\_message_batch** method can then be called to  send several messages at once:</span></span>

```python
from azure.servicebus.control_client import Message

msg1 = Message('Hello World!')
msg2 = Message('Hello World again!')
sbs.send_queue_message_batch('taskqueue', [msg1, msg2])
```

<span data-ttu-id="30c07-182">**receive\_queue\_message** 메서드를 호출하여 메시지를 큐에서 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-182">It is then possible to call the **receive\_queue\_message** method to dequeue the message.</span></span>

```python
msg = sbs.receive_queue_message('taskqueue')
```

### <a name="service-bus-topics"></a><span data-ttu-id="30c07-183">Service Bus 토픽</span><span class="sxs-lookup"><span data-stu-id="30c07-183">Service Bus topics</span></span>

<span data-ttu-id="30c07-184">**create\_topic** 메서드를 사용하여 서버 쪽 항목을 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-184">The **create\_topic** method can be used to create a server-side topic:</span></span>

```python
sbs.create_topic('taskdiscussion')
```

<span data-ttu-id="30c07-185">**send\_topic\_message** 메서드를 사용하여 항목에 메시지를 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-185">The **send\_topic\_message** method can be used to send a message to a topic:</span></span>

```python
from azure.servicebus.control_client import Message

msg = Message(b'Hello World!')
sbs.send_topic_message('taskdiscussion', msg)
```

<span data-ttu-id="30c07-186">**send\_topic\_message_batch** 메서드를 사용하여 여러 개의 메시지를 한 번에 보낼 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-186">The **send\_topic\_message_batch** method can be used to send  several messages at once:</span></span>

```python
from azure.servicebus.control_client import Message

msg1 = Message(b'Hello World!')
msg2 = Message(b'Hello World again!')
sbs.send_topic_message_batch('taskdiscussion', [msg1, msg2])
```

<span data-ttu-id="30c07-187">Python 3에서 문자열 메시지는 utf-8로 인코딩되고 Python 2에서 인코딩을 직접 관리해야 한다는 점을 고려하세요.</span><span class="sxs-lookup"><span data-stu-id="30c07-187">Please consider that in Python 3 a str message will be utf-8 encoded and you should have to manage your encoding yourself in Python 2.</span></span>

<span data-ttu-id="30c07-188">클라이언트가 구독을 만들고 **create\_subscription** 메서드 및 **receive\_subscription\_message** 메서드를 호출하여 메시지를 사용하기 시작할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-188">A client can then create a subscription and start consuming messages by calling the **create\_subscription** method followed by the **receive\_subscription\_message** method.</span></span> <span data-ttu-id="30c07-189">구독을 만들기 전에 전송된 모든 메시지는 수신되지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-189">Please note that any messages sent before the subscription is created will not be received.</span></span>

```python
from azure.servicebus.control_client import Message

sbs.create_subscription('taskdiscussion', 'client1')
msg = Message('Hello World!')
sbs.send_topic_message('taskdiscussion', msg)
msg = sbs.receive_subscription_message('taskdiscussion', 'client1')
```

### <a name="event-hub"></a><span data-ttu-id="30c07-190">이벤트 허브</span><span class="sxs-lookup"><span data-stu-id="30c07-190">Event Hub</span></span>

<span data-ttu-id="30c07-191">Event Hubs를 통해 다양한 디바이스 및 서비스 집합에서 높은 처리량으로 이벤트 스트림을 수집할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-191">Event Hubs enable the collection of event streams at high throughput, from a diverse set of devices and services.</span></span>

<span data-ttu-id="30c07-192">**create\_event\_hub** 메서드를 사용하여 Event Hub를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-192">The **create\_event\_hub** method can be used to create an event hub:</span></span>

```python
sbs.create_event_hub('myhub')
```

<span data-ttu-id="30c07-193">이벤트를 보내려면:</span><span class="sxs-lookup"><span data-stu-id="30c07-193">To send an event:</span></span>

```python
sbs.send_event('myhub', '{ "DeviceId":"dev-01", "Temperature":"37.0" }')
```

<span data-ttu-id="30c07-194">이벤트 내용은 여러 메시지를 포함하는 이벤트 메시지 또는 JSON 인코딩 문자열입니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-194">The event content is the event message or JSON-encoded string that contains multiple messages.</span></span>

### <a name="advanced-features"></a><span data-ttu-id="30c07-195">고급 기능</span><span class="sxs-lookup"><span data-stu-id="30c07-195">Advanced features</span></span>

#### <a name="broker-properties-and-user-properties"></a><span data-ttu-id="30c07-196">Broker 속성 및 사용자 속성</span><span class="sxs-lookup"><span data-stu-id="30c07-196">Broker properties and user properties</span></span>

<span data-ttu-id="30c07-197">이 섹션에서는 [여기](https://docs.microsoft.com/rest/api/servicebus/message-headers-and-properties)에 정의된 Broker 및 사용자 속성을 사용하는 방법을 설명합니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-197">This section describes how to use Broker and User properties defined [here](https://docs.microsoft.com/rest/api/servicebus/message-headers-and-properties):</span></span>

```python
sent_msg = Message(b'This is the third message',
                   broker_properties={'Label': 'M3'},
                   custom_properties={'Priority': 'Medium',
                                      'Customer': 'ABC'}
            )
```

<span data-ttu-id="30c07-198">날짜/시간, int, 부동 또는 부울 값을 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-198">You can use datetime, int, float or boolean</span></span>

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

<span data-ttu-id="30c07-199">이 라이브러리의 이전 버전과의 호환성을 위해 `broker_properties`를 JSON 문자열로 정의할 수도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-199">For compatibility reason with old version of this library,  `broker_properties` could also be defined as a JSON string.</span></span>
<span data-ttu-id="30c07-200">이 경우에 유효한 JSON 문자열을 작성해야 합니다. RestAPI에 보내기 전에 Python에서 검사하지 않습니다.</span><span class="sxs-lookup"><span data-stu-id="30c07-200">If this situation, you're responsible to write a valid JSON string, no check will be made by Python before sending to the RestAPI.</span></span>

```python
broker_properties = '{"ForcePersistence": false, "Label": "My label"}'
sent_msg = Message(b'receive message',
                   broker_properties = broker_properties
)
```

## <a name="next-steps"></a><span data-ttu-id="30c07-201">다음 단계</span><span class="sxs-lookup"><span data-stu-id="30c07-201">Next Steps</span></span>

* [<span data-ttu-id="30c07-202">Service Bus 설명서</span><span class="sxs-lookup"><span data-stu-id="30c07-202">Service Bus documentation</span></span>](https://docs.microsoft.com/azure/service-bus-messaging)
* [<span data-ttu-id="30c07-203">SDK 소스 코드</span><span class="sxs-lookup"><span data-stu-id="30c07-203">SDK source code</span></span>](https://github.com/Azure/azure-sdk-for-python/tree/master/azure-servicebus)
* [<span data-ttu-id="30c07-204">SDK 참조 설명서</span><span class="sxs-lookup"><span data-stu-id="30c07-204">SDK reference documentation</span></span>](https://docs.microsoft.com/python/api/overview/azure/servicebus/client?view=azure-python)
* [<span data-ttu-id="30c07-205">추가 샘플</span><span class="sxs-lookup"><span data-stu-id="30c07-205">Additional samples</span></span>](https://github.com/Azure/azure-sdk-for-python/tree/master/azure-servicebus/examples)
