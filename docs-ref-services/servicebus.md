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
# <a name="service-bus-libraries-for-python"></a>Python용 Service Bus 라이브러리

## <a name="overview"></a>개요

Microsoft Azure Service Bus는 신뢰할 수 있는 메시지 큐 및 지속형 게시/구독 메시징을 포함하여 클라우드 기반, 메시지 지향 미들웨어 기술 집합을 지원합니다. 

## <a name="install-the-libraries"></a>라이브러리 설치
```bash
pip install azure-servicebus
```

## <a name="servicebus-queues"></a>ServiceBus 큐
ServiceBus 큐는 푸시 스타일 배달(긴 폴링 사용)을 사용하는 고급 메시징 기능이 필요한 시나리오(대규모 메시지, 메시지 순서 지정, 단일 작업 파괴적 읽기, 예정된 배달)에 유용할 수 있는 Storage 큐의 대안입니다.

서비스에서는 공유 액세스 서명 인증 또는 ACS 인증을 사용할 수 있습니다.

2014년 8월 이후 Azure Portal을 사용하여 만든 Service Bus 네임스페이스는 더 이상 ACS 인증을 지원하지 않습니다. Azure SDK를 사용하여 ACS 호환 가능 네임스페이스를 만들 수 있습니다.

### <a name="shared-access-signature-authentication"></a>공유 액세스 서명 인증

공유 액세스 서명 인증을 사용하려면 다음을 사용하여 Service Bus 서비스를 만듭니다.

```python
from azure.servicebus import ServiceBusService

key_name = 'RootManageSharedAccessKey' # SharedAccessKeyName from Azure portal
key_value = '' # SharedAccessKey from Azure portal
sbs = ServiceBusService(service_namespace,
                        shared_access_key_name=key_name,
                        shared_access_key_value=key_value)
```

### <a name="acs-authentication"></a>ACS 인증

ACS 인증을 사용하려면 다음을 사용하여 Service Bus 서비스를 만듭니다.

```python
from azure.servicebus import ServiceBusService

account_key = '' # DEFAULT KEY from Azure portal
issuer = 'owner' # DEFAULT ISSUER from Azure portal
sbs = ServiceBusService(service_namespace,
                        account_key=account_key,
                        issuer=issuer)
```
### <a name="sending-and-receiving-messages"></a>메시지 송수신

**create\_queue** 메서드를 사용하여 큐가 존재하는지 확인할 수 있습니다.

```python
sbs.create_queue('taskqueue')
```
**send\_queue\_message** 메서드를 호출하여 큐에 메시지를 삽입할 수 있습니다.

```python
from azure.servicebus import Message

msg = Message('Hello World!')
sbs.send_queue_message('taskqueue', msg)
```
**send\_queue\_message_batch** 메서드를 호출하여 한 번에 여러 개의 메시지를 보낼 수 있습니다.

```python
from azure.servicebus import Message

msg1 = Message('Hello World!')
msg2 = Message('Hello World again!')
sbs.send_queue_message_batch('taskqueue', [msg1, msg2])
```
**receive\_queue\_message** 메서드를 호출하여 메시지를 큐에서 제거할 수 있습니다.

```python
msg = sbs.receive_queue_message('taskqueue')
```

## <a name="servicebus-topics"></a>ServiceBus 항목

ServiceBus 항목은 게시/구독 시나리오를 쉽게 구현하는 ServiceBus 큐를 기반으로 하는 추상화입니다.

**create\_topic** 메서드를 사용하여 서버 쪽 항목을 만들 수 있습니다.

```python
sbs.create_topic('taskdiscussion')
```
**send\_topic\_message** 메서드를 사용하여 항목에 메시지를 보낼 수 있습니다.

```python
from azure.servicebus import Message

msg = Message(b'Hello World!')
sbs.send_topic_message('taskdiscussion', msg)
```

**send\_topic\_message_batch** 메서드를 사용하여 한 번에 여러 메시지를 보낼 수 있습니다.

```python
from azure.servicebus import Message

msg1 = Message(b'Hello World!')
msg2 = Message(b'Hello World again!')
sbs.send_topic_message_batch('taskdiscussion', [msg1, msg2])
```

Python 3에서 문자열 메시지는 utf-8로 인코딩되고 Python 2에서 인코딩을 직접 관리해야 한다는 점을 고려하세요.

클라이언트가 구독을 만들고 **create\_subscription** 메서드 및 **receive\_subscription\_message** 메서드를 호출하여 메시지를 사용하기 시작할 수 있습니다. 구독을 만들기 전에 전송된 모든 메시지는 수신되지 않습니다.

```python
from azure.servicebus import Message

sbs.create_subscription('taskdiscussion', 'client1')
msg = Message('Hello World!')
sbs.send_topic_message('taskdiscussion', msg)
msg = sbs.receive_subscription_message('taskdiscussion', 'client1')
```

## <a name="event-hub"></a>이벤트 허브

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

## <a name="advanced-features"></a>고급 기능

### <a name="broker-properties-and-user-properties"></a>Broker 속성 및 사용자 속성

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

> [!div class="nextstepaction"]
> [관리 API 탐색](/python/api/overview/azure/servicebus/management)
