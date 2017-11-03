---
title: "설치"
description: "Azure Python SDK를 설치하는 방법을 설명합니다."
keywords: Azure, Python, SDK, API
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/05/2017
ms.topic: install
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.assetid: 
ms.openlocfilehash: 1ee0c110673f908832c1c9e8fd6dac4c90c16e8e
ms.sourcegitcommit: ce2921d9a6f21d58fdf77cbc843c9b4af0ea796d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/31/2017
---
# <a name="installation"></a>설치

## <a name="installation-with-pip"></a>pip를 사용하여 설치

Azure 서비스의 각 라이브러리를 개별적으로 설치할 수 있습니다.

```bash
pip install azure-batch          # Install the latest Batch runtime library
pip install azure-mgmt-scheduler # Install the latest Storage management library
```

미리 보기 패키지는 `--pre` 플래그를 사용하여 설치할 수 있습니다.

```bash
pip install --pre azure-mgmt-compute # will install only the latest Compute Management library
```

`azure` 메타패키지를 사용하여 한 줄로 Azure 라이브러리의 집합도 설치할 수 있습니다.

```bash
pip install azure
```

이 패키지의 미리 보기 버전을 게시하며, --pre 플래그를 사용하여 액세스할 수 있습니다.

```bash
pip install --pre azure
```

## <a name="install-from-github"></a>GitHub에서 설치

원본에서 `azure`를 설치하려면 다음과 같습니다.

    git clone git://github.com/Azure/azure-sdk-for-python.git
    cd azure-sdk-for-python
    python setup.py install
