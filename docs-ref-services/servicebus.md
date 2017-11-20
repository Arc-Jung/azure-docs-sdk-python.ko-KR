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
# <a name="service-bus-libraries-for-python"></a><span data-ttu-id="6d2f5-104">Python용 Service Bus 라이브러리</span><span class="sxs-lookup"><span data-stu-id="6d2f5-104">Service Bus libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="6d2f5-105">개요</span><span class="sxs-lookup"><span data-stu-id="6d2f5-105">Overview</span></span>

<span data-ttu-id="6d2f5-106">Microsoft Azure Service Bus는 신뢰할 수 있는 메시지 큐 및 지속형 게시/구독 메시징을 포함하여 클라우드 기반, 메시지 지향 미들웨어 기술 집합을 지원합니다.</span><span class="sxs-lookup"><span data-stu-id="6d2f5-106">Microsoft Azure Service Bus supports a set of cloud-based, message-oriented middleware technologies including reliable message queuing and durable publish/subscribe messaging.</span></span> 

## <a name="install-the-libraries"></a><span data-ttu-id="6d2f5-107">라이브러리 설치</span><span class="sxs-lookup"><span data-stu-id="6d2f5-107">Install the libraries</span></span>
```bash
pip install azure-mgmt-servicebus
```

## <a name="example"></a><span data-ttu-id="6d2f5-108">예제</span><span class="sxs-lookup"><span data-stu-id="6d2f5-108">Example</span></span>
<span data-ttu-id="6d2f5-109">큐에 메시지를 보냅니다.</span><span class="sxs-lookup"><span data-stu-id="6d2f5-109">Send messages to a queue.</span></span>

```python
from azure.servicebus import Message

msg1 = Message('Hello World!')
msg2 = Message('Hello World again!')
sbs.send_queue_message_batch('taskqueue', [msg1, msg2])
# dequeue the message
msg = sbs.receive_queue_message('taskqueue')
```
> [!div class="nextstepaction"]
> [<span data-ttu-id="6d2f5-110">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="6d2f5-110">Explore the Management APIs</span></span>](/python/api/overview/azure/servicebus/managementlibrary)

