---
title: Python용 Azure SDK 작업 구성
description: Python용 Azure SDK에서 발생된 C
keywords: Azure, Python, SDK, API, 예외
author: rloutlaw
ms.author: routlaw
manager: douge
ms.date: 03/07/2018
ms.topic: article
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: d7be7cd76d019c6741d93c04458376a9352e363b
ms.sourcegitcommit: 41e6e6b5469271f4ec497a322b460e2a2af2c73d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/28/2018
---
# <a name="operation-config"></a>작업 구성 

작업 방법에는 kwargs에서 제공할 수 있는 추가 매개 변수가 있습니다. 이를 operation_config라고 합니다.

작업 구성을 위한 옵션은 다음과 같습니다.

|매개 변수 이름|유형|역할|
|----------------------|------|---------------|
| verify |`bool`|SSL 인증서를 확인할지 지정합니다. 기본값은 True입니다.|
|  cert |`str`| 클라이언트 측 확인을 위한 로컬 인증서의 경로입니다.|
|  시간 제한 |`int`| 서버 연결을 설정하기 위한 시간 제한(초).|
|  allow_redirects |`bool` | 리디렉션을 허용할지 지정합니다.|
|  max_redirects  |`int`| 최대 허용 리디렉션 수입니다.|
|  proxies  |`dict` |프록시 서버 설정입니다.|
|  use_env_proxies |`bool` |로컬 환경 변수에서 프록시 설정을 읽을지 지정합니다.|
|  retries  |`int` | 총 재시도 횟수입니다.|
|  enable_http_logger | `bool`| 디버그 모드에서 HTTP 로그를 사용합니다(기본적으로 False).|
