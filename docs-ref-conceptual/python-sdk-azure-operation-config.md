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
ms.openlocfilehash: adeb6aa8a2c363c3119e97503df9536fb0633b4c
ms.sourcegitcommit: 434186988284e0a8268a9de11645912a81226d6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/29/2019
ms.locfileid: "66376870"
---
# <a name="operation-config"></a>작업 구성 

작업에 대한 메서드에는 `kwargs`에서 제공할 수 있는 추가 매개 변수가 있습니다. 이를 operation_config라고 합니다.

작업 구성을 위한 옵션은 다음과 같습니다.

|매개 변수 이름|Type|역할|
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
