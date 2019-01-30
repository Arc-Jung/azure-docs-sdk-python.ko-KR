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
ms.openlocfilehash: 540a2a248f7a2abcc83517bc4a4ef96ef03e8a9f
ms.sourcegitcommit: fba77bdf8eb9f49621be94544d9fef88aff98c14
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/23/2019
ms.locfileid: "54747743"
---
# <a name="service-bus-libraries-for-python"></a>Python용 Service Bus 라이브러리

Microsoft Azure Service Bus는 신뢰할 수 있는 메시지 큐 및 지속형 게시/구독 메시징을 포함하여 클라우드 기반, 메시지 지향 미들웨어 기술 집합을 지원합니다.

* [SDK 소스 코드](https://github.com/Azure/azure-sdk-for-python/tree/master/azure-servicebus)
* [SDK 참조 설명서](https://docs.microsoft.com/python/api/overview/azure/servicebus/client?view=azure-python)

## <a name="whats-new-in-v0500"></a>v0.50.0의 새로운 기능
0.50.0 버전부터 새 AMQP 기반 API는 메시지 보내기 및 받기를 할 수 있습니다. 이 업데이트는 **호환성이 손상되는 변경**을 포함합니다.
현 시점에서 업그레이드가 적합한지 판단하려면 [v0.21.1에서 v0.50.0로 마이그레이션](#migration-from-v0211-to-v0500)을 읽어보세요.

새로운 AMQP 기반 API는 향상된 메시지 전달 신뢰성, 성능 및 향후 확장된 기능 지원을 제공합니다.
새로운 API는 또한 메시지를 보내고 받고 처리하는 비동기 작업(asyncio 기반)을 지원합니다.

레거시 HTTP 기반 작업에 대한 문서는 [레거시 API의 HTTP 기반 작업 사용](#using-http-based-operations-of-the-legacy-api)을 참조하세요.


## <a name="prerequisites"></a>필수 조건

* Azure 구독 -[체험 계정 만들기](https://azure.microsoft.com/free/)
* Azure [Service Bus 네임스페이스 및 관리 자격 증명](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-create-namespace-portal)
* [Python 2.7-3.7](https://www.python.org/downloads/)


## <a name="installation"></a>설치
```bash
pip install azure-servicebus
```

## <a name="connect-to-azure-service-bus"></a>Azure Service Bus에 연결

### <a name="get-credentials"></a>자격 증명 가져오기
아래 Azure CLI 조각을 사용하여 Service Bus 연결 문자열로 환경 변수를 채웁니다(Azure Portal에서도 이 값을 찾을 수 있습니다). 조각은 Bash 셸에 대해 서식이 지정됩니다.

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

### <a name="create-client"></a>클라이언트 만들기
`SB_CONN_STR` 환경 변수를 채우면 ServiceBusClient를 만들 수 있습니다.
```python
import os
from azure.servicebus import ServiceBusClient

connection_str = os.environ['SB_CONN_STR']

sb_client = ServiceBusClient.from_connection_string(connection_str)
```
비동기 작업을 사용하려는 경우 `azure.servicebus.aio` 네임스페이스를 사용합니다.
```python
import os
from azure.servicebus.aio import ServiceBusClient

connection_str = os.environ['SB_CONN_STR']

sb_client = ServiceBusClient.from_connection_string(connection_str)
```


## <a name="service-bus-queues"></a>Service Bus 큐
Service Bus 큐는 푸시 스타일 배달(긴 폴링 사용)을 사용하는 고급 메시징 기능이 필요한 시나리오(대규모 메시지, 메시지 순서 지정, 단일 작업 파괴적 읽기, 예정된 배달)에 유용할 수 있는 Storage 큐의 대안입니다.

### <a name="create-queue"></a>큐 만들기
이는 Service Bus 네임스페이스 내에서 새 큐를 만듭니다. 네임스페이스 내에 같은 이름의 큐가 이미 있으면 오류가 발생합니다. 
```python
sb_client.create_queue("MyQueue")
```
큐 동작을 구성하는 선택적 매개 변수를 지정할 수도 있습니다.
```python
sb_client.create_queue(
    "MySessionQueue",
    requires_session=True  # Create a sessionful queue
    max_delivery_count=5  # Max delivery attempts per message
)
```

### <a name="get-a-queue-client"></a>큐 클라이언트 가져오기
QueueClient는 다른 작업과 함께 큐와 메시지를 주고 받고 데 사용할 수 있습니다.
```python
queue_client = sb_client.get_queue("MyQueue")
```

### <a name="sending-messages"></a>메시지 보내기
큐 클라이언트는 한 번에 하나 이상의 메시지를 보낼 수 있습니다.
```python
from azure.servicebus import Message

message = Message("Hello World")
queue_client.send(message)

message_one = Message("First")
message_two = Message("Second")
queue_client.send([message_one, message_two])
```
QueueClient.send를 호출할 때마다 새 서비스 연결을 만듭니다. 여러 호출에 전송에 동일한 연결을 다시 사용하려면 발신자를 열 수 있습니다.
```python
message_one = Message("First")
message_two = Message("Second")

with queue_client.get_sender() as sender:
    sender.send(message_one)
    sender.send(message_two)
```
비동기 클라이언트를 사용하는 경우 위의 작업은 비동기 구문을 사용합니다.
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


### <a name="receiving-messages"></a>메시지 수신
연속 반복기로 큐에서 메시지를 받을 수 있습니다. 메시지 수신을 위한 기본 모드는 [PeekLock](https://docs.microsoft.com/rest/api/servicebus/peek-lock-message-non-destructive-read)이며 각 메시지는 큐에서 제거되도록 명시적으로 완료해야 합니다.
```python
messages = queue_client.get_receiver()
for message in messages:
    print(message)
    message.complete()
```
서비스 연결은 전체 반복기에 대해 계속 열려 있습니다.
메시지 스트림을 부분적으로만 반복하는 경우 `with` 문에서 수신자를 실행하여 연결이 닫혔는지 확인해야 합니다.
```python
with queue_client.get_receiver() as messages:
    for message in messages:
        print(message)
        message.complete()
        break
```
비동기 클라이언트를 사용하는 경우 위의 작업은 비동기 구문을 사용합니다.
```python
async with queue_client.get_receiver() as messages:
    async for message in messages:
        print(message)
        await message.complete()
        break
```

## <a name="service-bus-topics-and-subscriptions"></a>Service Bus 토픽 및 구독

Service Bus 토픽 및 구독은 Service Bus 큐 위의 추상화로서 게시/구독 패턴으로 일 대 다 형태의 통신을 제공합니다. 메시지는 토픽으로 전송되어 하나 이상의 연관된 구독으로 전달되므로 많은 수의 수신자로 확장하는 데 유용합니다.

### <a name="create-topic"></a>토픽 만들기
이는 Service Bus 네임스페이스 내에서 새 토픽을 만듭니다. 동일한 이름의 토픽이 이미 있으면 오류가 발생합니다. 
```python
sb_client.create_topic("MyTopic")
```

### <a name="get-a-topic-client"></a>토픽 클라이언트 가져오기
다른 작업과 함께 토픽에 메시지를 보내려면 TopicClient를 사용할 수 있습니다.
```python
topic_client = sb_client.get_topic("MyTopic")
```

### <a name="create-subscription"></a>구독 만들기
이는 Service Bus 네임스페이스 내에서 지정된 토픽에 대한 새 구독을 만듭니다.
```python
sb_client.create_subscription("MyTopic", "MySubscription")
```

### <a name="get-a-subscription-client"></a>구독 클라이언트 가져오기
SubscriptionClient는 다른 작업과 함께 토픽에서 메시지를 받는 데 사용할 수 있습니다.
```python
topic_client = sb_client.get_subscription("MyTopic", "MySubscription")
```

## <a name="migration-from-v0211-to-v0500"></a>v0.21.1에서 v0.50.0으로 마이그레이션
호환성이 손상되는 변경이 0.50.0 버전에 도입되었습니다.
원래 HTTP 기반 API는 v0.50.0에서 계속 사용할 수 있지만 이제는 새로운 네임스페이스 `azure.servicebus.control_client` 아래에 존재합니다.

### <a name="should-i-upgrade"></a>업그레이드해야 합니까?
새로운 패키지(v0.50.0)는 v0.21.1 이상의 HTTP 기반 작업을 개선하지 않습니다. HTTP 기반 API는 이제 새 네임스페이스 아래에 있다는 점을 제외하고는 동일합니다. 따라서 HTTP 기반 작업(`create_queue`, `delete_queue` 등)만 사용하려는 경우에는 현재 업그레이드할 때 추가 이점이 없습니다.


### <a name="how-do-i-migrate-my-code-to-the-new-version"></a>내 코드를 새 버전으로 마이그레이션하려면 어떻게 하나요?
v0.21.0에 대해 작성된 코드는 네임스페이스 가져오기를 변경하여 버전 0.50.0으로 가져올 수 있습니다.

```python
# from azure.servicebus import ServiceBusService  <- This will now raise an ImportError
from azure.servicebus.control_client import ServiceBusService

key_name = 'RootManageSharedAccessKey' # SharedAccessKeyName from Azure portal
key_value = '' # SharedAccessKey from Azure portal
sbs = ServiceBusService(service_namespace,
                        shared_access_key_name=key_name,
                        shared_access_key_value=key_value)
```

## <a name="using-http-based-operations-of-the-legacy-api"></a>기존 API의 HTTP 기반 작업 사용하기
다음 문서에서는 기존 API에 대해 설명하고 있으며 추가 변경 없이 기존 코드를 v0.50.0으로 가져오려는 사용자를 위한 것입니다. v0.21.1 사용자도 이 참조 지침을 사용할 수 있습니다.
새 코드 작성자들은 위에서 설명한 새로운 API를 사용하는 것이 좋습니다.

### <a name="service-bus-queues"></a>Service Bus 큐

#### <a name="shared-access-signature-sas-authentication"></a>공유 액세스 서명(SAS) 인증

공유 액세스 서명 인증을 사용하려면 다음을 사용하여 Service Bus 서비스를 만듭니다.

```python
from azure.servicebus.control_client import ServiceBusService

key_name = 'RootManageSharedAccessKey' # SharedAccessKeyName from Azure portal
key_value = '' # SharedAccessKey from Azure portal
sbs = ServiceBusService(service_namespace,
                        shared_access_key_name=key_name,
                        shared_access_key_value=key_value)
```

#### <a name="access-control-service-acs-authentication"></a>ACS(Access Control Service) 인증
ACS는 더 이상 새 Service Bus 네임스페이스에서 지원되지 않습니다. [SAS 인증으로 애플리케이션을 마이그레이션](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-migrate-acs-sas) 하는 것이 좋습니다.
이전 Service Bus 네임스페이스 내에서 ACS 인증을 사용하려면 다음을 사용하여 ServiceBusService를 만듭니다.

```python
from azure.servicebus.control_client import ServiceBusService

account_key = '' # DEFAULT KEY from Azure portal
issuer = 'owner' # DEFAULT ISSUER from Azure portal
sbs = ServiceBusService(service_namespace,
                        account_key=account_key,
                        issuer=issuer)
```
#### <a name="sending-and-receiving-messages"></a>메시지 송수신

**create\_queue** 메서드를 사용하여 큐가 존재하는지 확인할 수 있습니다.

```python
sbs.create_queue('taskqueue')
```
**send\_queue\_message** 메서드를 호출하여 큐에 메시지를 삽입할 수 있습니다.

```python
from azure.servicebus.control_client import Message

msg = Message('Hello World!')
sbs.send_queue_message('taskqueue', msg)
```
**send\_queue\_message_batch** 메서드를 호출하여 한 번에 여러 개의 메시지를 보낼 수 있습니다.

```python
from azure.servicebus.control_client import Message

msg1 = Message('Hello World!')
msg2 = Message('Hello World again!')
sbs.send_queue_message_batch('taskqueue', [msg1, msg2])
```
**receive\_queue\_message** 메서드를 호출하여 메시지를 큐에서 제거할 수 있습니다.

```python
msg = sbs.receive_queue_message('taskqueue')
```

### <a name="service-bus-topics"></a>Service Bus 토픽

**create\_topic** 메서드를 사용하여 서버 쪽 항목을 만들 수 있습니다.

```python
sbs.create_topic('taskdiscussion')
```
**send\_topic\_message** 메서드를 사용하여 항목에 메시지를 보낼 수 있습니다.

```python
from azure.servicebus.control_client import Message

msg = Message(b'Hello World!')
sbs.send_topic_message('taskdiscussion', msg)
```

**send\_topic\_message_batch** 메서드를 사용하여 한 번에 여러 메시지를 보낼 수 있습니다.

```python
from azure.servicebus.control_client import Message

msg1 = Message(b'Hello World!')
msg2 = Message(b'Hello World again!')
sbs.send_topic_message_batch('taskdiscussion', [msg1, msg2])
```

Python 3에서 문자열 메시지는 utf-8로 인코딩되고 Python 2에서 인코딩을 직접 관리해야 한다는 점을 고려하세요.

클라이언트가 구독을 만들고 **create\_subscription** 메서드 및 **receive\_subscription\_message** 메서드를 호출하여 메시지를 사용하기 시작할 수 있습니다. 구독을 만들기 전에 전송된 모든 메시지는 수신되지 않습니다.

```python
from azure.servicebus.control_client import Message

sbs.create_subscription('taskdiscussion', 'client1')
msg = Message('Hello World!')
sbs.send_topic_message('taskdiscussion', msg)
msg = sbs.receive_subscription_message('taskdiscussion', 'client1')
```

### <a name="event-hub"></a>이벤트 허브

Event Hubs를 통해 다양한 디바이스 및 서비스 집합에서 높은 처리량으로 이벤트 스트림을 수집할 수 있습니다.

**create\_event\_hub** 메서드를 사용하여 Event Hub를 만들 수 있습니다.

```python
sbs.create_event_hub('myhub')
```
이벤트를 보내려면:

```python
sbs.send_event('myhub', '{ "DeviceId":"dev-01", "Temperature":"37.0" }')
```
이벤트 내용은 여러 메시지를 포함하는 이벤트 메시지 또는 JSON 인코딩 문자열입니다.

### <a name="advanced-features"></a>고급 기능

#### <a name="broker-properties-and-user-properties"></a>Broker 속성 및 사용자 속성

이 섹션에서는 [여기](https://docs.microsoft.com/rest/api/servicebus/message-headers-and-properties)에 정의된 Broker 및 사용자 속성을 사용하는 방법을 설명합니다.

```python
sent_msg = Message(b'This is the third message',
                   broker_properties={'Label': 'M3'},
                   custom_properties={'Priority': 'Medium',
                                      'Customer': 'ABC'}
            )
```
날짜/시간, int, 부동 또는 부울 값을 사용할 수 있습니다.

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
이 라이브러리의 이전 버전과 호환성 이유로 `broker_properties`를 JSON 문자열로 정의할 수 있습니다.
이 경우에 유효한 JSON 문자열을 작성해야 합니다. RestAPI에 보내기 전에 Python에서 검사하지 않습니다.

```python
broker_properties = '{"ForcePersistence": false, "Label": "My label"}'
sent_msg = Message(b'receive message',
                   broker_properties = broker_properties
)
```

## <a name="next-steps"></a>다음 단계
* [Service Bus 설명서](https://docs.microsoft.com/azure/service-bus-messaging)
* [SDK 소스 코드](https://github.com/Azure/azure-sdk-for-python/tree/master/azure-servicebus)
* [SDK 참조 설명서](https://docs.microsoft.com/python/api/overview/azure/servicebus/client?view=azure-python)
* [추가 샘플](https://github.com/Azure/azure-sdk-for-python/tree/master/azure-servicebus/examples)
