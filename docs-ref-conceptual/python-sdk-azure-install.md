---
title: 설치
description: Azure Python SDK를 설치하는 방법을 설명합니다.
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
ms.openlocfilehash: 6014937fb41d6074e94578ccc47c30eb7b3f63d2
ms.sourcegitcommit: 434186988284e0a8268a9de11645912a81226d6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/29/2019
ms.locfileid: "66376873"
---
# <a name="installation"></a>설치

## <a name="which-python-and-which-version-to-use"></a>사용할 Python 및 버전

몇 가지의 Python 인터프리터가 있으며 다음을 예로 들 수 있습니다.

* CPython - 가장 일반적으로 사용되는 표준 Python 인터프리터
* PyPy - 빠르고 규정을 준수하는 CPython에 대한 대체 구현
* IronPython - .Net/CLR에서 실행되는 Python 인터프리터
* Jython - Java Virtual Machine에서 실행되는 Python 인터프리터

**CPython** v2.7 또는 v3.4+ 이상 및 PyPy 5.4.0은 Python Azure SDK에 대해 테스트 및 지원됩니다.

## <a name="where-to-get-python"></a>Python을 구하는 위치

CPython을 구하는 몇 가지 방법이 있습니다.

* [Python](https://www.python.org/)에서 직접
* [Anaconda](https://www.anaconda.com/), [Enthought](https://www.enthought.com/) 또는 [ActiveState](https://www.activestate.com/)와 같은 신뢰할 수 있는 배포판에서
* 원본에서 빌드

구체적인 요구 사항이 없다면 처음 두 가지 옵션을 사용하는 것이 좋습니다.

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

```bash
git clone git://github.com/Azure/azure-sdk-for-python.git
cd azure-sdk-for-python
python setup.py install
```
