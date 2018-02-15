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
ms.openlocfilehash: 5ce4ef27667d45697200eef67be92c62812b3809
ms.sourcegitcommit: 66e112df9be660354e23955b0adf3efd784ba739
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/14/2018
---
# <a name="installation"></a><span data-ttu-id="702d4-104">설치</span><span class="sxs-lookup"><span data-stu-id="702d4-104">Installation</span></span>

## <a name="installation-with-pip"></a><span data-ttu-id="702d4-105">pip를 사용하여 설치</span><span class="sxs-lookup"><span data-stu-id="702d4-105">Installation with pip</span></span>

<span data-ttu-id="702d4-106">Azure 서비스의 각 라이브러리를 개별적으로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="702d4-106">You can install each Azure service's library individually:</span></span>

```bash
pip install azure-batch          # Install the latest Batch runtime library
pip install azure-mgmt-scheduler # Install the latest Storage management library
```

<span data-ttu-id="702d4-107">미리 보기 패키지는 `--pre` 플래그를 사용하여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="702d4-107">Preview packages can be installed using the `--pre` flag:</span></span>

```bash
pip install --pre azure-mgmt-compute # will install only the latest Compute Management library
```

<span data-ttu-id="702d4-108">`azure` 메타패키지를 사용하여 한 줄로 Azure 라이브러리의 집합도 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="702d4-108">You can also install a set of Azure libraries in a single line using the `azure` meta-package.</span></span>

```bash
pip install azure
```

<span data-ttu-id="702d4-109">이 패키지의 미리 보기 버전을 게시하며, --pre 플래그를 사용하여 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="702d4-109">We publish a preview version of this package, which you can access using the --pre flag:</span></span>

```bash
pip install --pre azure
```

## <a name="install-from-github"></a><span data-ttu-id="702d4-110">GitHub에서 설치</span><span class="sxs-lookup"><span data-stu-id="702d4-110">Install from GitHub</span></span>

<span data-ttu-id="702d4-111">원본에서 `azure`를 설치하려면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="702d4-111">If you want to install `azure` from source:</span></span>

    git clone git://github.com/Azure/azure-sdk-for-python.git
    cd azure-sdk-for-python
    python setup.py install
