---
title: "Python용 Service Bus 라이브러리"
description: "Python용 Service Bus 클라이언트 및 관리 라이브러리에 대한 참조 설명서"
keywords: "Azure, Python, SDK, API, 메시지, pubsub, pub-sub, 메시지 브로커"
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/26/2017
ms.topic: article
ms.devlang: python
ms.service: service-bus
ms.openlocfilehash: bf7be945f2c7a3daea93ff4e5b770459c00632c8
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="service-bus-libraries-for-python"></a>Python용 Service Bus 라이브러리

## <a name="overview"></a>개요

Microsoft Azure Service Bus는 신뢰할 수 있는 메시지 큐 및 지속형 게시/구독 메시징을 포함하여 클라우드 기반, 메시지 지향 미들웨어 기술 집합을 지원합니다. 

## <a name="install-the-libraries"></a>라이브러리 설치
```bash
pip install azure-mgmt-servicebus
```

## <a name="example"></a>예제
큐에 메시지를 보냅니다.

```python
from azure.servicebus import Message

msg1 = Message('Hello World!')
msg2 = Message('Hello World again!')
sbs.send_queue_message_batch('taskqueue', [msg1, msg2])
# dequeue the message
msg = sbs.receive_queue_message('taskqueue')
```
> [!div class="nextstepaction"]
> [관리 API 탐색](/python/api/overview/azure/servicebus/managementlibrary)

