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
ms.openlocfilehash: d65f07a30b3aa8b0a1a502baa86986ad50848873
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="installation"></a><span data-ttu-id="b0389-104">설치</span><span class="sxs-lookup"><span data-stu-id="b0389-104">Installation</span></span>

## <a name="installation-with-pip"></a><span data-ttu-id="b0389-105">pip를 사용하여 설치</span><span class="sxs-lookup"><span data-stu-id="b0389-105">Installation with pip</span></span>

<span data-ttu-id="b0389-106">Azure 서비스의 각 라이브러리를 개별적으로 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0389-106">You can install each Azure service's library individually:</span></span>

```bash
pip install azure-batch          # Install the latest Batch runtime library
pip install azure-mgmt-scheduler # Install the latest Storage management library
```

<span data-ttu-id="b0389-107">미리 보기 패키지는 `--pre` 플래그를 사용하여 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0389-107">Preview packages can be installed using the `--pre` flag:</span></span>

```bash
pip install --pre azure-mgmt-compute # will install only the latest Compute Management library
```

<span data-ttu-id="b0389-108">`azure` 메타패키지를 사용하여 한 줄로 Azure 라이브러리의 집합도 설치할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0389-108">You can also install a set of Azure libraries in a single line using the `azure` meta-package.</span></span>

```bash
pip install azure
```

<span data-ttu-id="b0389-109">이 패키지의 미리 보기 버전을 게시하며, --pre 플래그를 사용하여 액세스할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="b0389-109">We publish a preview version of this package, which you can access using the --pre flag:</span></span>

```bash
pip install --pre azure
```

## <a name="install-from-github"></a><span data-ttu-id="b0389-110">GitHub에서 설치</span><span class="sxs-lookup"><span data-stu-id="b0389-110">Install from GitHub</span></span>

<span data-ttu-id="b0389-111">원본에서 `azure`를 설치하려면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="b0389-111">If you want to install `azure` from source:</span></span>

    git clone git://github.com/Azure/azure-sdk-for-python.git
    cd azure-sdk-for-python
    python setup.py install

## <a name="stable-packages"></a><span data-ttu-id="b0389-112">안정적인 패키지</span><span class="sxs-lookup"><span data-stu-id="b0389-112">Stable packages</span></span>
| <span data-ttu-id="b0389-113">패키지 이름</span><span class="sxs-lookup"><span data-stu-id="b0389-113">Package name</span></span> |
|--------------|
|[<span data-ttu-id="b0389-114">azure-batch</span><span class="sxs-lookup"><span data-stu-id="b0389-114">azure-batch</span></span>](https://pypi.org/project/azure-batch/)  |   
|[<span data-ttu-id="b0389-115">azure-mgmt-batch</span><span class="sxs-lookup"><span data-stu-id="b0389-115">azure-mgmt-batch</span></span>](https://pypi.org/project/azure-mgmt-batch/)|
|[<span data-ttu-id="b0389-116">azure-mgmt-cognitiveservices</span><span class="sxs-lookup"><span data-stu-id="b0389-116">azure-mgmt-cognitiveservices</span></span>](https://pypi.org/project/azure-mgmt-cognitiveservices/)|    
|[<span data-ttu-id="b0389-117">azure-mgmt-devtestlabs</span><span class="sxs-lookup"><span data-stu-id="b0389-117">azure-mgmt-devtestlabs</span></span>](https://pypi.org/project/azure-mgmt-devtestlabs/)|    
|[<span data-ttu-id="b0389-118">azure-mgmt-dns</span><span class="sxs-lookup"><span data-stu-id="b0389-118">azure-mgmt-dns</span></span>](https://pypi.org/project/azure-mgmt-dns/) |
|[<span data-ttu-id="b0389-119">azure-mgmt-logic</span><span class="sxs-lookup"><span data-stu-id="b0389-119">azure-mgmt-logic</span></span>](https://pypi.org/project/azure-mgmt-logic/)|
|[<span data-ttu-id="b0389-120">azure-mgmt-redis</span><span class="sxs-lookup"><span data-stu-id="b0389-120">azure-mgmt-redis</span></span>](https://pypi.org/project/azure-mgmt-redis/)|
|[<span data-ttu-id="b0389-121">azure-mgmt-scheduler</span><span class="sxs-lookup"><span data-stu-id="b0389-121">azure-mgmt-scheduler</span></span>](https://pypi.org/project/azure-mgmt-scheduler/)|    
|[<span data-ttu-id="b0389-122">azure-mgmt-servermanager</span><span class="sxs-lookup"><span data-stu-id="b0389-122">azure-mgmt-servermanager</span></span>](https://pypi.org/project/azure-mgmt-servermanager/)|    
|[<span data-ttu-id="b0389-123">azure-servicebus</span><span class="sxs-lookup"><span data-stu-id="b0389-123">azure-servicebus</span></span>](https://pypi.org/project/azure-mgmt-servicebus/)|   
|[<span data-ttu-id="b0389-124">azure-servicefabric</span><span class="sxs-lookup"><span data-stu-id="b0389-124">azure-servicefabric</span></span>](https://pypi.org/project/azure-servicefabric/)|  
|[<span data-ttu-id="b0389-125">azure-servicemanagement-legacy</span><span class="sxs-lookup"><span data-stu-id="b0389-125">azure-servicemanagement-legacy</span></span>](https://pypi.org/project/azure-servicemanagement-legacy/)|    
|[<span data-ttu-id="b0389-126">azure-storage</span><span class="sxs-lookup"><span data-stu-id="b0389-126">azure-storage</span></span>](https://pypi.org/project/azure-storage/)|  

## <a name="preview-packages"></a><span data-ttu-id="b0389-127">미리 보기 패키지</span><span class="sxs-lookup"><span data-stu-id="b0389-127">Preview packages</span></span>
| <span data-ttu-id="b0389-128">패키지 이름</span><span class="sxs-lookup"><span data-stu-id="b0389-128">Package name</span></span> | 
|--------------|
|[<span data-ttu-id="b0389-129">azure-keyvault</span><span class="sxs-lookup"><span data-stu-id="b0389-129">azure-keyvault</span></span>](https://pypi.org/project/azure-keyvault/)|    
|[<span data-ttu-id="b0389-130">azure-monitor</span><span class="sxs-lookup"><span data-stu-id="b0389-130">azure-monitor</span></span>](https://pypi.org/project/azure-monitor)|   
|[<span data-ttu-id="b0389-131">azure-mgmt-resource</span><span class="sxs-lookup"><span data-stu-id="b0389-131">azure-mgmt-resource</span></span>](https://pypi.org/project/azure-mgmt-resource)|   
|[<span data-ttu-id="b0389-132">azure-mgmt-compute</span><span class="sxs-lookup"><span data-stu-id="b0389-132">azure-mgmt-compute</span></span>](https://pypi.org/project/azure-mgmt-compute)| 
|[<span data-ttu-id="b0389-133">azure-mgmt-network</span><span class="sxs-lookup"><span data-stu-id="b0389-133">azure-mgmt-network</span></span>](https://pypi.org/project/azure-mgmt-network)| 
|[<span data-ttu-id="b0389-134">azure-mgmt-storage</span><span class="sxs-lookup"><span data-stu-id="b0389-134">azure-mgmt-storage</span></span>](https://pypi.org/project/azure-mgmt-storage)| 
|[<span data-ttu-id="b0389-135">azure-mgmt-keyvault</span><span class="sxs-lookup"><span data-stu-id="b0389-135">azure-mgmt-keyvault</span></span>](https://pypi.org/project/azure-mgmt-keyvault)|   
|[<span data-ttu-id="b0389-136">azure-graphrbac</span><span class="sxs-lookup"><span data-stu-id="b0389-136">azure-graphrbac</span></span>](https://pypi.org/project/azure-graphrbac)|   
|[<span data-ttu-id="b0389-137">azure-mgmt-authorization</span><span class="sxs-lookup"><span data-stu-id="b0389-137">azure-mgmt-authorization</span></span>](https://pypi.org/project/azure-mgmt-authorization)| 
|[<span data-ttu-id="b0389-138">azure-mgmt-billing</span><span class="sxs-lookup"><span data-stu-id="b0389-138">azure-mgmt-billing</span></span>](https://pypi.org/project/azure-mgmt-billing)| 
|[<span data-ttu-id="b0389-139">azure-mgmt-cdn</span><span class="sxs-lookup"><span data-stu-id="b0389-139">azure-mgmt-cdn</span></span>](https://pypi.org/project/azure-mgmt-cdn)| 
|[<span data-ttu-id="b0389-140">azure-mgmt-containerregistry</span><span class="sxs-lookup"><span data-stu-id="b0389-140">azure-mgmt-containerregistry</span></span>](https://pypi.org/project/azure-mgmt-containerregistry)| 
|[<span data-ttu-id="b0389-141">azure-mgmt-commerce</span><span class="sxs-lookup"><span data-stu-id="b0389-141">azure-mgmt-commerce</span></span>](https://pypi.org/project/azure-mgmt-commerce)|   
|[<span data-ttu-id="b0389-142">azure-mgmt-consumption</span><span class="sxs-lookup"><span data-stu-id="b0389-142">azure-mgmt-consumption</span></span>](https://pypi.org/project/azure-mgmt-consumption)| 
|[<span data-ttu-id="b0389-143">azure-mgmt-datalake-analytics</span><span class="sxs-lookup"><span data-stu-id="b0389-143">azure-mgmt-datalake-analytics</span></span>](https://pypi.org/project/azure-mgmt-datalake-analytics)|   
|[<span data-ttu-id="b0389-144">azure-mgmt-datalake-store</span><span class="sxs-lookup"><span data-stu-id="b0389-144">azure-mgmt-datalake-store</span></span>](https://pypi.org/project/azure-mgmt-datalake-store)|   
|[<span data-ttu-id="b0389-145">azure-mgmt-documentdb</span><span class="sxs-lookup"><span data-stu-id="b0389-145">azure-mgmt-documentdb</span></span>](https://pypi.org/project/azure-mgmt-documentdb)|   
|[<span data-ttu-id="b0389-146">azure-mgmt-eventhub</span><span class="sxs-lookup"><span data-stu-id="b0389-146">azure-mgmt-eventhub</span></span>](https://pypi.org/project/azure-mgmt-eventhub)|   
|[<span data-ttu-id="b0389-147">azure-mgmt-iothub</span><span class="sxs-lookup"><span data-stu-id="b0389-147">azure-mgmt-iothub</span></span>](https://pypi.org/project/azure-mgmt-iothub)|
|[<span data-ttu-id="b0389-148">azure-mgmt-media</span><span class="sxs-lookup"><span data-stu-id="b0389-148">azure-mgmt-media</span></span>](https://pypi.org/project/azure-mgmt-media)| 
|[<span data-ttu-id="b0389-149">azure-mgmt-monitor</span><span class="sxs-lookup"><span data-stu-id="b0389-149">azure-mgmt-monitor</span></span>](https://pypi.org/project/azure-mgmt-monitor)| 
|[<span data-ttu-id="b0389-150">azure-mgmt-notificationhubs</span><span class="sxs-lookup"><span data-stu-id="b0389-150">azure-mgmt-notificationhubs</span></span>](https://pypi.org/project/azure-mgmt-notificationhubs)|   
|[<span data-ttu-id="b0389-151">azure-mgmt-powerbiembedded</span><span class="sxs-lookup"><span data-stu-id="b0389-151">azure-mgmt-powerbiembedded</span></span>](https://pypi.org/project/azure-mgmt-powerbiembedded)| 
|[<span data-ttu-id="b0389-152">azure-mgmt-search</span><span class="sxs-lookup"><span data-stu-id="b0389-152">azure-mgmt-search</span></span>](https://pypi.org/project/azure-mgmt-search)|
|[<span data-ttu-id="b0389-153">azure-mgmt-servicebus</span><span class="sxs-lookup"><span data-stu-id="b0389-153">azure-mgmt-servicebus</span></span>](https://pypi.org/project/azure-mgmt-servicebus)|   
|[<span data-ttu-id="b0389-154">azure-mgmt-sql</span><span class="sxs-lookup"><span data-stu-id="b0389-154">azure-mgmt-sql</span></span>](https://pypi.org/project/azure-mgmt-sql)| 
|[<span data-ttu-id="b0389-155">azure-mgmt-trafficmanager</span><span class="sxs-lookup"><span data-stu-id="b0389-155">azure-mgmt-trafficmanager</span></span>](https://pypi.org/project/azure-mgmt-trafficmanager)|   
|[<span data-ttu-id="b0389-156">azure-mgmt-web</span><span class="sxs-lookup"><span data-stu-id="b0389-156">azure-mgmt-web</span></span>](https://pypi.org/project/azure-mgmt-web)|