---
title: 설치
description: Azure Python SDK를 설치하는 방법을 설명합니다.
keywords: Azure, Python, SDK, API
author: lisawong19
ms.author: routlaw
manager: douge
ms.date: 06/05/2017
ms.topic: install
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 478118642122d7c0c80b1ddf37b13f71d8ca3adc
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534454"
---
# <a name="installation"></a><span data-ttu-id="4f161-104">설치</span><span class="sxs-lookup"><span data-stu-id="4f161-104">Installation</span></span>

## <a name="which-python-and-which-version-to-use"></a><span data-ttu-id="4f161-105">사용할 Python 및 버전</span><span class="sxs-lookup"><span data-stu-id="4f161-105">Which Python and which version to use</span></span>

<span data-ttu-id="4f161-106">몇 가지의 Python 인터프리터가 있으며 다음을 예로 들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f161-106">There are several Python interpreters available - examples include:</span></span>

* <span data-ttu-id="4f161-107">CPython - 가장 일반적으로 사용되는 표준 Python 인터프리터</span><span class="sxs-lookup"><span data-stu-id="4f161-107">CPython - the standard and most commonly used Python interpreter</span></span>
* <span data-ttu-id="4f161-108">PyPy - 빠르고 규정을 준수하는 CPython에 대한 대체 구현</span><span class="sxs-lookup"><span data-stu-id="4f161-108">PyPy - fast, compliant alternative implementation to CPython</span></span>
* <span data-ttu-id="4f161-109">IronPython - .Net/CLR에서 실행되는 Python 인터프리터</span><span class="sxs-lookup"><span data-stu-id="4f161-109">IronPython - Python interpreter that runs on .Net/CLR</span></span>
* <span data-ttu-id="4f161-110">Jython - Java Virtual Machine에서 실행되는 Python 인터프리터</span><span class="sxs-lookup"><span data-stu-id="4f161-110">Jython - Python interpreter that runs on the Java Virtual Machine</span></span>

<span data-ttu-id="4f161-111">**CPython** v2.7 또는 v3.4+ 이상 및 PyPy 5.4.0은 Python Azure SDK에 대해 테스트 및 지원됩니다.</span><span class="sxs-lookup"><span data-stu-id="4f161-111">**CPython** v2.7 or v3.4+ and PyPy 5.4.0 are tested and supported for the Python Azure SDK.</span></span>

## <a name="where-to-get-python"></a><span data-ttu-id="4f161-112">Python을 구하는 위치</span><span class="sxs-lookup"><span data-stu-id="4f161-112">Where to get Python?</span></span>

<span data-ttu-id="4f161-113">CPython을 구하는 몇 가지 방법이 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f161-113">There are several ways to get CPython:</span></span>

* <span data-ttu-id="4f161-114">[Python](https://www.python.org/)에서 직접</span><span class="sxs-lookup"><span data-stu-id="4f161-114">Directly from [Python](https://www.python.org/)</span></span>
* <span data-ttu-id="4f161-115">[Anaconda](https://www.anaconda.com/), [Enthought](https://www.enthought.com/) 또는 [ActiveState](https://www.activestate.com/)와 같은 신뢰할 수 있는 배포판에서</span><span class="sxs-lookup"><span data-stu-id="4f161-115">From a reputable distro such as [Anaconda](https://www.anaconda.com/), [Enthought](https://www.enthought.com/) or [ActiveState](https://www.activestate.com/)</span></span>
* <span data-ttu-id="4f161-116">원본에서 빌드</span><span class="sxs-lookup"><span data-stu-id="4f161-116">Build from source!</span></span>

<span data-ttu-id="4f161-117">구체적인 요구 사항이 없다면 처음 두 가지 옵션을 사용하는 것이 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="4f161-117">Unless you have a specific need, we recommend the first two options.</span></span>

## <a name="installation-with-pip"></a><span data-ttu-id="4f161-118">pip를 사용하여 설치</span><span class="sxs-lookup"><span data-stu-id="4f161-118">Installation with pip</span></span>

<span data-ttu-id="4f161-119">Azure 서비스의 각 라이브러리를 개별적으로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f161-119">You can install each Azure service's library individually:</span></span>

```bash
pip install azure-batch          # Install the latest Batch runtime library
pip install azure-mgmt-scheduler # Install the latest Storage management library
```

<span data-ttu-id="4f161-120">미리 보기 패키지는 `--pre` 플래그를 사용하여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f161-120">Preview packages can be installed using the `--pre` flag:</span></span>

```bash
pip install --pre azure-mgmt-compute # will install only the latest Compute Management library
```

<span data-ttu-id="4f161-121">`azure` 메타패키지를 사용하여 한 줄로 Azure 라이브러리의 집합도 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f161-121">You can also install a set of Azure libraries in a single line using the `azure` meta-package.</span></span>

```bash
pip install azure
```

<span data-ttu-id="4f161-122">이 패키지의 미리 보기 버전을 게시하며, --pre 플래그를 사용하여 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f161-122">We publish a preview version of this package, which you can access using the --pre flag:</span></span>

```bash
pip install --pre azure
```

## <a name="install-from-github"></a><span data-ttu-id="4f161-123">GitHub에서 설치</span><span class="sxs-lookup"><span data-stu-id="4f161-123">Install from GitHub</span></span>

<span data-ttu-id="4f161-124">원본에서 `azure`를 설치하려면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="4f161-124">If you want to install `azure` from source:</span></span>

```bash
git clone git://github.com/Azure/azure-sdk-for-python.git
cd azure-sdk-for-python
python setup.py install
```

## <a name="install-an-older-version-with-pip"></a><span data-ttu-id="4f161-125">Pip를 사용하여 이전 버전을 설치</span><span class="sxs-lookup"><span data-stu-id="4f161-125">Install an older version with pip</span></span>
<span data-ttu-id="4f161-126">`azure`'azure==3.0.0' 버전 세부 정보를 지정하여 이전 버전을 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f161-126">You can install an older version of `azure` by specifying 'azure==3.0.0' version details.</span></span>
```bash
pip install azure==3.0.0 
```
## <a name="check-sdk-installation-details-with-pip"></a><span data-ttu-id="4f161-127">Pip를 사용하여 SDK 설치 세부 정보를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="4f161-127">Check SDK installation details with pip</span></span>
<span data-ttu-id="4f161-128">`azure` SDK 설치 위치, 버전 정보 등을 확인할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f161-128">You can check `azure` SDK installation location, version details etc.</span></span>
```bash
pip show azure # Show installed version, location details etc.
pip freeze     # Output installed packages in requirements format.
pip list       # List installed packages, including editables.
```
## <a name="to-uninstall-with-pip"></a><span data-ttu-id="4f161-129">pip를 사용하여 제거하려면 다음을 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4f161-129">To uninstall with pip</span></span>
<span data-ttu-id="4f161-130">`azure` 메타패키지를 사용하여 한 줄로 Azure 라이브러리의 집합을 제거할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4f161-130">You can uninstall all Azure libraries in a single line using the `azure` meta-package.</span></span>
```bash
pip uninstall azure 
```
> [!NOTE]
> <span data-ttu-id="4f161-131">`pip uninstall azure`는 `azure` 메타패키지를 제거하지만 개별 `azure-*` 패키지(그리고 `adal` 및 `msrest` 등의 기타)를 뒤에 남겨 둡니다.</span><span class="sxs-lookup"><span data-stu-id="4f161-131">`pip uninstall azure`removes the `azure` meta-package but leaves the individual `azure-*` packages behind (and others, like `adal` and `msrest` ).</span></span> <span data-ttu-id="4f161-132">Python과 pip의 한 측면은 종속성이 있는 모든 패키지에 대해 초기 패키지를 제거해도 종속성을 제거하지 않는다는 것입니다.</span><span class="sxs-lookup"><span data-stu-id="4f161-132">An aspect of Python and pip is that for all packages that have dependencies, uninstalling the initial package does not uninstall the dependencies.</span></span> <span data-ttu-id="4f161-133">`azure-` 및 지원 패키지를 제거하려면 `pip freeze | grep 'azure-' | xargs pip uninstall -y` 명령을 실행한 다음 adal, msrest 및 msrestazure에 대한 개별 제거를 수행합니다.</span><span class="sxs-lookup"><span data-stu-id="4f161-133">To remove `azure-` and its supporting packages, run the command `pip freeze | grep 'azure-' | xargs pip uninstall -y` (and then perform individual uninstalls for adal, msrest, and msrestazure).</span></span>

