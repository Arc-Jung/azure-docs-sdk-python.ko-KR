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
# <a name="operation-config"></a><span data-ttu-id="c5f0a-104">작업 구성</span><span class="sxs-lookup"><span data-stu-id="c5f0a-104">Operation config</span></span> 

<span data-ttu-id="c5f0a-105">작업에 대한 메서드에는 `kwargs`에서 제공할 수 있는 추가 매개 변수가 있습니다.</span><span class="sxs-lookup"><span data-stu-id="c5f0a-105">Methods on operations have extra parameters which can be provided in the `kwargs`.</span></span> <span data-ttu-id="c5f0a-106">이를 operation_config라고 합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f0a-106">This is called operation_config.</span></span>

<span data-ttu-id="c5f0a-107">작업 구성을 위한 옵션은 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="c5f0a-107">The options for operation configuration are:</span></span>

|<span data-ttu-id="c5f0a-108">매개 변수 이름</span><span class="sxs-lookup"><span data-stu-id="c5f0a-108">Parameter name</span></span>|<span data-ttu-id="c5f0a-109">Type</span><span class="sxs-lookup"><span data-stu-id="c5f0a-109">Type</span></span>|<span data-ttu-id="c5f0a-110">역할</span><span class="sxs-lookup"><span data-stu-id="c5f0a-110">Role</span></span>|
|----------------------|------|---------------|
| <span data-ttu-id="c5f0a-111">verify</span><span class="sxs-lookup"><span data-stu-id="c5f0a-111">verify</span></span> |`bool`|<span data-ttu-id="c5f0a-112">SSL 인증서를 확인할지 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f0a-112">Whether to verify the SSL certificate.</span></span> <span data-ttu-id="c5f0a-113">기본값은 True입니다.</span><span class="sxs-lookup"><span data-stu-id="c5f0a-113">Default is True.</span></span>|
|  <span data-ttu-id="c5f0a-114">cert</span><span class="sxs-lookup"><span data-stu-id="c5f0a-114">cert</span></span> |`str`| <span data-ttu-id="c5f0a-115">클라이언트 측 확인을 위한 로컬 인증서의 경로입니다.</span><span class="sxs-lookup"><span data-stu-id="c5f0a-115">Path to local certificate for client side verification.</span></span>|
|  <span data-ttu-id="c5f0a-116">시간 제한</span><span class="sxs-lookup"><span data-stu-id="c5f0a-116">timeout</span></span> |`int`| <span data-ttu-id="c5f0a-117">서버 연결을 설정하기 위한 시간 제한(초).</span><span class="sxs-lookup"><span data-stu-id="c5f0a-117">Timeout for establishing a server connection in seconds.</span></span>|
|  <span data-ttu-id="c5f0a-118">allow_redirects</span><span class="sxs-lookup"><span data-stu-id="c5f0a-118">allow_redirects</span></span> |`bool` | <span data-ttu-id="c5f0a-119">리디렉션을 허용할지 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f0a-119">Whether to allow redirects.</span></span>|
|  <span data-ttu-id="c5f0a-120">max_redirects</span><span class="sxs-lookup"><span data-stu-id="c5f0a-120">max_redirects</span></span>  |`int`| <span data-ttu-id="c5f0a-121">최대 허용 리디렉션 수입니다.</span><span class="sxs-lookup"><span data-stu-id="c5f0a-121">Maimum number of allowed redirects.</span></span>|
|  <span data-ttu-id="c5f0a-122">proxies</span><span class="sxs-lookup"><span data-stu-id="c5f0a-122">proxies</span></span>  |`dict` |<span data-ttu-id="c5f0a-123">프록시 서버 설정입니다.</span><span class="sxs-lookup"><span data-stu-id="c5f0a-123">Proxy server settings.</span></span>|
|  <span data-ttu-id="c5f0a-124">use_env_proxies</span><span class="sxs-lookup"><span data-stu-id="c5f0a-124">use_env_proxies</span></span> |`bool` |<span data-ttu-id="c5f0a-125">로컬 환경 변수에서 프록시 설정을 읽을지 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="c5f0a-125">Whether to read proxy settings from local environment variables.</span></span>|
|  <span data-ttu-id="c5f0a-126">retries</span><span class="sxs-lookup"><span data-stu-id="c5f0a-126">retries</span></span>  |`int` | <span data-ttu-id="c5f0a-127">총 재시도 횟수입니다.</span><span class="sxs-lookup"><span data-stu-id="c5f0a-127">Total number of retry attempts.</span></span>|
|  <span data-ttu-id="c5f0a-128">enable_http_logger</span><span class="sxs-lookup"><span data-stu-id="c5f0a-128">enable_http_logger</span></span> | `bool`| <span data-ttu-id="c5f0a-129">디버그 모드에서 HTTP 로그를 사용합니다(기본적으로 False).</span><span class="sxs-lookup"><span data-stu-id="c5f0a-129">Enable logs of HTTP in debug mode (False by default).</span></span>|
