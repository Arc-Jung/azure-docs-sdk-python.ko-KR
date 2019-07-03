---
title: Python용 Azure Cognitive Services 모듈
description: Python용 Azure Cognitive Services 모듈에 대한 참조
keywords: Azure, Python, SDK, API, Cognitive Services
author: rloutlaw
ms.author: routlaw
manager: angerobe
ms.date: 04/04/2018
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 5a23a52414e70facd6feae3af3956a5131f6b5c4
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534348"
---
# <a name="azure-cognitive-services-modules-for-python"></a><span data-ttu-id="4ccbd-104">Python용 Azure Cognitive Services 모듈</span><span class="sxs-lookup"><span data-stu-id="4ccbd-104">Azure Cognitive Services modules for Python</span></span>

<span data-ttu-id="4ccbd-105">Python용 Azure Cognitive Services 모듈을 사용하여 Python 앱, 웹 사이트 및 도구에 이미지 및 얼굴 인식, 언어 분석 및 검색을 추가합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccbd-105">Add image and face recognition, language analysis, and search to your Python apps, websites, and tools using the Azure Cognitive Services modules for Python.</span></span>

## <a name="vision-modules"></a><span data-ttu-id="4ccbd-106">비전 모듈</span><span class="sxs-lookup"><span data-stu-id="4ccbd-106">Vision modules</span></span>

### <a name="computer-vision"></a><span data-ttu-id="4ccbd-107">Computer Vision</span><span class="sxs-lookup"><span data-stu-id="4ccbd-107">Computer Vision</span></span> 

<span data-ttu-id="4ccbd-108">이미지에서 찾은 시각적 콘텐츠에 대한 정보를 반환합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccbd-108">Returns information about visual content found in an image:</span></span>

- <span data-ttu-id="4ccbd-109">태그 지정, 설명 및 도메인 특정 모델을 사용하여 자신 있게 콘텐츠를 파악하고 레이블을 지정하세요.</span><span class="sxs-lookup"><span data-stu-id="4ccbd-109">Use tagging, descriptions, and domain-specific models to identify content and label it with confidence.</span></span>
- <span data-ttu-id="4ccbd-110">성인 콘텐츠를 자동으로 제한할 수 있도록 성인/외설 설정을 적용합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccbd-110">Apply adult/racy settings to enable automated restriction of adult content.</span></span>
- <span data-ttu-id="4ccbd-111">사진의 이미지 형식과 색 구성표를 파악합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccbd-111">Identify image types and color schemes in pictures.</span></span>

<span data-ttu-id="4ccbd-112">브라우저에서 무료로 [Computer Vision을 사용](https://azure.microsoft.com/en-us/services/cognitive-services/computer-vision/)해 보세요.</span><span class="sxs-lookup"><span data-stu-id="4ccbd-112">[Try Computer Vision](https://azure.microsoft.com/en-us/services/cognitive-services/computer-vision/) for free in your browser.</span></span>

<span data-ttu-id="4ccbd-113">[pip](https://pip.pypa.io/en/stable/quickstart/)를 사용하여 Python 모듈 가져오기:</span><span class="sxs-lookup"><span data-stu-id="4ccbd-113">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```python
pip install azure-cognitiveservices-vision-computervision
```

<span data-ttu-id="4ccbd-114">Computer Vision API에 대해 [자세히 알아보고](/azure/cognitive-services/computer-vision/home) [Computer Vision API Python 빠른 시작](/azure/cognitive-services/computer-vision/quickstarts/python)을 시작하세요.</span><span class="sxs-lookup"><span data-stu-id="4ccbd-114">[Learn more](/azure/cognitive-services/computer-vision/home) about the Computer Vision API and get started with the [Computer Vision API Python quickstart](/azure/cognitive-services/computer-vision/quickstarts/python).</span></span>

### <a name="content-moderator"></a><span data-ttu-id="4ccbd-115">Content Moderator</span><span class="sxs-lookup"><span data-stu-id="4ccbd-115">Content Moderator</span></span>

<span data-ttu-id="4ccbd-116">사용자 검토 도구로 확대된, 텍스트, 비디오 및 이미지의 기계 지원 조정.</span><span class="sxs-lookup"><span data-stu-id="4ccbd-116">Machine-assisted moderation of text, video and images, augmented with human review tools.</span></span>

<span data-ttu-id="4ccbd-117">[pip](https://pip.pypa.io/en/stable/quickstart/)를 사용하여 Python 모듈 가져오기:</span><span class="sxs-lookup"><span data-stu-id="4ccbd-117">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```python
pip install azure-cognitiveservices-vision-contentmoderator
```

<span data-ttu-id="4ccbd-118">Content Moderator 서비스에 대해 [자세히 알아보세요](/azure/cognitive-services/content-moderator/overview).</span><span class="sxs-lookup"><span data-stu-id="4ccbd-118">[Learn more](/azure/cognitive-services/content-moderator/overview) about the Content Moderator service.</span></span>

### <a name="custom-vision-service"></a><span data-ttu-id="4ccbd-119">사용자 지정 시각 서비스</span><span class="sxs-lookup"><span data-stu-id="4ccbd-119">Custom Vision Service</span></span>

<span data-ttu-id="4ccbd-120">이미지를 업로드하여 특정 사용 사례에 맞게 Computer Vision 모델을 학습시키고 사용자 지정하세요.</span><span class="sxs-lookup"><span data-stu-id="4ccbd-120">Upload images to train and customize a computer vision model for your specific use case.</span></span> <span data-ttu-id="4ccbd-121">모델이 학습되면 API를 사용하여 모델로 이미지에 태그를 지정하고 결과를 평가하여 분류자를 개선할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ccbd-121">Once the model is trained, you can use the API to tag images using the model and evaluate the results to improve your classifier.</span></span>

<span data-ttu-id="4ccbd-122">[pip](https://pip.pypa.io/en/stable/quickstart/)를 사용하여 Python 모듈 가져오기:</span><span class="sxs-lookup"><span data-stu-id="4ccbd-122">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```python
pip install azure-cognitiveservices-vision-customvision
```

<span data-ttu-id="4ccbd-123">Custom Vision 서비스에 대해 [자세히 알아보고](/azure/cognitive-services/Custom-Vision-Service/home) [Custom Vision Python 자습서](/azure/cognitive-services/Custom-Vision-Service/python-tutorial)를 시작하세요.</span><span class="sxs-lookup"><span data-stu-id="4ccbd-123">[Learn more](/azure/cognitive-services/Custom-Vision-Service/home) about the Custom Vision service and get started with the [Custom Vision Python tutorial](/azure/cognitive-services/Custom-Vision-Service/python-tutorial)</span></span>

### <a name="face-api"></a><span data-ttu-id="4ccbd-124">Face API</span><span class="sxs-lookup"><span data-stu-id="4ccbd-124">Face API</span></span>

<span data-ttu-id="4ccbd-125">사진에서 얼굴을 감지, 식별, 분석, 구성하고 태그를 지정합니다.</span><span class="sxs-lookup"><span data-stu-id="4ccbd-125">Detect, identify, analyze, organize, and tag faces in photos.</span></span> 

<span data-ttu-id="4ccbd-126">브라우저에서 [Face API를 사용](https://azure.microsoft.com/en-us/services/cognitive-services/face/)해 보세요.</span><span class="sxs-lookup"><span data-stu-id="4ccbd-126">[Try the Face API](https://azure.microsoft.com/en-us/services/cognitive-services/face/) in your browser.</span></span>

<span data-ttu-id="4ccbd-127">[pip](https://pip.pypa.io/en/stable/quickstart/)를 사용하여 Python 모듈 가져오기:</span><span class="sxs-lookup"><span data-stu-id="4ccbd-127">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```python
pip install cognitive-face
```

<span data-ttu-id="4ccbd-128">Face API에 대해 [자세히 알아보고](/azure/cognitive-services/face/overview) [Face API Python 빠른 시작](/azure/cognitive-services/Face/Tutorials/FaceAPIinPythonTutorial)을 시작하세요.</span><span class="sxs-lookup"><span data-stu-id="4ccbd-128">[Learn more](/azure/cognitive-services/face/overview) about the Face API and get started with the [Face API Python quickstart](/azure/cognitive-services/Face/Tutorials/FaceAPIinPythonTutorial).</span></span>

## <a name="search-modules"></a><span data-ttu-id="4ccbd-129">검색 모듈</span><span class="sxs-lookup"><span data-stu-id="4ccbd-129">Search modules</span></span>

### <a name="web-search"></a><span data-ttu-id="4ccbd-130">Web Search</span><span class="sxs-lookup"><span data-stu-id="4ccbd-130">Web search</span></span>

<span data-ttu-id="4ccbd-131">Bing Web Search API로 인덱싱된 웹 문서를 검색하고 결과 형식, 최신성 등을 기준으로 결과의 범위를 축소해 보세요.</span><span class="sxs-lookup"><span data-stu-id="4ccbd-131">Retrieve web documents indexed by the Bing Web Search API and narrow down the results by result type, freshness and more.</span></span> 

<span data-ttu-id="4ccbd-132">브라우저에서 [Web Search API를 사용](https://azure.microsoft.com/en-us/services/cognitive-services/bing-web-search-api/)해 보세요.</span><span class="sxs-lookup"><span data-stu-id="4ccbd-132">[Try the Web Search API](https://azure.microsoft.com/en-us/services/cognitive-services/bing-web-search-api/) in your browser.</span></span>

<span data-ttu-id="4ccbd-133">[pip](https://pip.pypa.io/en/stable/quickstart/)를 사용하여 Python 모듈 가져오기:</span><span class="sxs-lookup"><span data-stu-id="4ccbd-133">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```python
pip install azure-cognitiveservices-search-websearch
```

<span data-ttu-id="4ccbd-134">Bing Web Search API에 대해 [자세히 알아보고](/azure/cognitive-services/bing-web-search/overview) [Web Search API Python 빠른 시작](/azure/cognitive-services/bing-web-search/quickstarts/python)을 시작하세요.</span><span class="sxs-lookup"><span data-stu-id="4ccbd-134">[Learn more](/azure/cognitive-services/bing-web-search/overview) about the Bing Web Search API and get started with the [Web Search API Python quickstart](/azure/cognitive-services/bing-web-search/quickstarts/python).</span></span>

### <a name="image-search"></a><span data-ttu-id="4ccbd-135">이미지 검색</span><span class="sxs-lookup"><span data-stu-id="4ccbd-135">Image search</span></span>

<span data-ttu-id="4ccbd-136">이미지를 검색하고 결과에 썸네일, 전체 이미지 URL, 이미지 메타데이터 등을 가져오세요.</span><span class="sxs-lookup"><span data-stu-id="4ccbd-136">Search for images and get thumbnails, full image URLs, image metadata and more in your results.</span></span>

<span data-ttu-id="4ccbd-137">브라우저에서 [Image Search API를 사용](https://azure.microsoft.com/en-us/services/cognitive-services/bing-image-search-api/)해 보세요.</span><span class="sxs-lookup"><span data-stu-id="4ccbd-137">[Try the Image Search API](https://azure.microsoft.com/en-us/services/cognitive-services/bing-image-search-api/) in your browser.</span></span>

<span data-ttu-id="4ccbd-138">[pip](https://pip.pypa.io/en/stable/quickstart/)를 사용하여 Python 모듈 가져오기:</span><span class="sxs-lookup"><span data-stu-id="4ccbd-138">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```python
pip install azure-cognitiveservices-search-imagesearch
```

<span data-ttu-id="4ccbd-139">Bing Image Search API에 대해 [자세히 알아보고](/azure/cognitive-services/bing-image-search/overview) [Image Search API Python 빠른 시작](/azure/cognitive-services/bing-image-search/quickstarts/python)을 시작하세요.</span><span class="sxs-lookup"><span data-stu-id="4ccbd-139">[Learn more](/azure/cognitive-services/bing-image-search/overview) about the Bing Image Search API and get started with the [Image Search API Python quickstart](/azure/cognitive-services/bing-image-search/quickstarts/python).</span></span>


### <a name="entity-search"></a><span data-ttu-id="4ccbd-140">Entity Search</span><span class="sxs-lookup"><span data-stu-id="4ccbd-140">Entity search</span></span>

<span data-ttu-id="4ccbd-141">특정 검색어 또는 위치와 가장 관련 있는 엔터티(장소, 사람 또는 물건)를 검색하세요.</span><span class="sxs-lookup"><span data-stu-id="4ccbd-141">Search for the most relevant entity (place, person, or thing) for a given search term or location.</span></span>

<span data-ttu-id="4ccbd-142">브라우저에서 [Entity Search API를 사용](https://azure.microsoft.com/services/cognitive-services/bing-entity-search-api/)해 보세요.</span><span class="sxs-lookup"><span data-stu-id="4ccbd-142">[Try the Entity Search API](https://azure.microsoft.com/services/cognitive-services/bing-entity-search-api/) in your browser.</span></span>

<span data-ttu-id="4ccbd-143">[pip](https://pip.pypa.io/en/stable/quickstart/)를 사용하여 Python 모듈 가져오기:</span><span class="sxs-lookup"><span data-stu-id="4ccbd-143">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```python
pip install azure-cognitiveservices-search-entitysearch
```

<span data-ttu-id="4ccbd-144">Bing Entity Search API에 대해 [자세히 알아보고](/azure/cognitive-services/bing-entities-search/search-the-web) [Entity Search API Python 빠른 시작](/azure/cognitive-services/bing-entities-search/quickstarts/python)을 시작하세요.</span><span class="sxs-lookup"><span data-stu-id="4ccbd-144">[Learn more](/azure/cognitive-services/bing-entities-search/search-the-web) about the Bing Entity Search API and get started with the [Entity Search API Python quickstart](/azure/cognitive-services/bing-entities-search/quickstarts/python).</span></span>

### <a name="custom-search"></a><span data-ttu-id="4ccbd-145">Custom Search</span><span class="sxs-lookup"><span data-stu-id="4ccbd-145">Custom search</span></span>

<span data-ttu-id="4ccbd-146">특정 검색 도메인에 맞는 사용자 지정 웹 검색을 빌드해 보세요.</span><span class="sxs-lookup"><span data-stu-id="4ccbd-146">Build and a custom web search that meets your specific search domain.</span></span>

<span data-ttu-id="4ccbd-147">[pip](https://pip.pypa.io/en/stable/quickstart/)를 사용하여 Python 모듈 가져오기:</span><span class="sxs-lookup"><span data-stu-id="4ccbd-147">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```python
pip install azure-cognitiveservices-search-customsearch
```

<span data-ttu-id="4ccbd-148">Bing Custom Search 서비스에 대해 [자세히 알아보고](/azure/cognitive-services/bing-custom-search/) [Custom Search API Python 빠른 시작](/azure/cognitive-services/bing-custom-search/call-endpoint-python)을 사용하여 Python에서 사용자 지정 검색 쿼리를 시작하세요.</span><span class="sxs-lookup"><span data-stu-id="4ccbd-148">[Learn more](/azure/cognitive-services/bing-custom-search/) about the Bing Custom Search service and get started with querying your custom search from Python with the [Custom Search API Python quickstart](/azure/cognitive-services/bing-custom-search/call-endpoint-python).</span></span>

### <a name="video-search"></a><span data-ttu-id="4ccbd-149">Video Search</span><span class="sxs-lookup"><span data-stu-id="4ccbd-149">Video search</span></span>

<span data-ttu-id="4ccbd-150">웹에서 비디오를 검색하고 작성자, 인코딩, 길이 및 조회수 메타데이터가 포함된 결과를 가져오세요.</span><span class="sxs-lookup"><span data-stu-id="4ccbd-150">Find videos across the web and get results with creator, encoding, length, and view count metadata.</span></span>

<span data-ttu-id="4ccbd-151">브라우저에서 [Video Search API를 사용](https://azure.microsoft.com/services/cognitive-services/bing-video-search-api/)해 보세요.</span><span class="sxs-lookup"><span data-stu-id="4ccbd-151">[Try the Video Search API](https://azure.microsoft.com/services/cognitive-services/bing-video-search-api/) in your browser.</span></span>

<span data-ttu-id="4ccbd-152">[pip](https://pip.pypa.io/en/stable/quickstart/)를 사용하여 Python 모듈 가져오기:</span><span class="sxs-lookup"><span data-stu-id="4ccbd-152">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```python
pip install azure-cognitiveservices-search-videosearch
```

<span data-ttu-id="4ccbd-153">Bing Video Search 서비스에 대해 [자세히 알아보고](/azure/cognitive-services/bing-video-search/search-the-web) [Video Search API Python 빠른 시작](/azure/cognitive-services/bing-video-search/python)을 시작하세요.</span><span class="sxs-lookup"><span data-stu-id="4ccbd-153">[Learn more](/azure/cognitive-services/bing-video-search/search-the-web) about the Bing Video Search service and get started with the [Video Search API Python quickstart](/azure/cognitive-services/bing-video-search/python).</span></span>


### <a name="news-search"></a><span data-ttu-id="4ccbd-154">News Search</span><span class="sxs-lookup"><span data-stu-id="4ccbd-154">News search</span></span>

<span data-ttu-id="4ccbd-155">웹에서 뉴스 기사를 검색하고, 기사, 관련 뉴스, 이미지 및 공급자 정보 메타데이터로 작업하세요.</span><span class="sxs-lookup"><span data-stu-id="4ccbd-155">Search the web for news articles and work with article, related news, images, and provider info metadata.</span></span>

<span data-ttu-id="4ccbd-156">브라우저에서 [News Search API를 사용](https://azure.microsoft.com/services/cognitive-services/bing-news-search-api/)해 보세요.</span><span class="sxs-lookup"><span data-stu-id="4ccbd-156">[Try the News Search API](https://azure.microsoft.com/services/cognitive-services/bing-news-search-api/) in your browser.</span></span>

<span data-ttu-id="4ccbd-157">[pip](https://pip.pypa.io/en/stable/quickstart/)를 사용하여 Python 모듈 가져오기:</span><span class="sxs-lookup"><span data-stu-id="4ccbd-157">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```python
pip install azure-cognitiveservices-search-newssearch
```

<span data-ttu-id="4ccbd-158">Bing News Search 서비스에 대해 [자세히 알아보고](/azure/cognitive-services/bing-news-search/search-the-web) [News Search API Python 빠른 시작](/azure/cognitive-services/bing-news-search/python)을 시작하세요.</span><span class="sxs-lookup"><span data-stu-id="4ccbd-158">[Learn more](/azure/cognitive-services/bing-news-search/search-the-web) about the Bing News Search service and get started with the [News Search API Python quickstart](/azure/cognitive-services/bing-news-search/python).</span></span>


## <a name="language-modules"></a><span data-ttu-id="4ccbd-159">언어 모듈</span><span class="sxs-lookup"><span data-stu-id="4ccbd-159">Language modules</span></span>

### <a name="text-analytics"></a><span data-ttu-id="4ccbd-160">텍스트 분석</span><span class="sxs-lookup"><span data-stu-id="4ccbd-160">Text Analytics</span></span> 

<span data-ttu-id="4ccbd-161">텍스트 분석 API는 원시 텍스트에 대한 자연어 처리를 제공하는 클라우드 기반 서비스입니다.</span><span class="sxs-lookup"><span data-stu-id="4ccbd-161">The Text Analytics API is a cloud-based service that provides  natural language processing over raw text.</span></span> <span data-ttu-id="4ccbd-162">이 API에는 세 가지 주요 기능이 포함되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4ccbd-162">The API includes three main functions:</span></span>

- <span data-ttu-id="4ccbd-163">정서 분석</span><span class="sxs-lookup"><span data-stu-id="4ccbd-163">Sentiment analysis</span></span>
- <span data-ttu-id="4ccbd-164">핵심 문구 추출</span><span class="sxs-lookup"><span data-stu-id="4ccbd-164">Key phrase extraction</span></span>
- <span data-ttu-id="4ccbd-165">언어 검색</span><span class="sxs-lookup"><span data-stu-id="4ccbd-165">Language detection</span></span>

<span data-ttu-id="4ccbd-166">브라우저에서 [텍스트 분석 API를 사용](https://azure.microsoft.com/en-us/services/cognitive-services/text-analytics/)해 보세요.</span><span class="sxs-lookup"><span data-stu-id="4ccbd-166">[Try the Text Analytics API](https://azure.microsoft.com/en-us/services/cognitive-services/text-analytics/) in your browser.</span></span>

<span data-ttu-id="4ccbd-167">[pip](https://pip.pypa.io/en/stable/quickstart/)를 사용하여 Python 모듈 가져오기:</span><span class="sxs-lookup"><span data-stu-id="4ccbd-167">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```python
pip install azure-cognitiveservices-language-textanalytics
```

<span data-ttu-id="4ccbd-168">텍스트 분석 API에 대해 [자세히 알아보고](/azure/cognitive-services/text-analytics/overview) [텍스트 분석 API Python 빠른 시작](/azure/cognitive-services/text-analytics/quickstarts/python)을 시작하세요.</span><span class="sxs-lookup"><span data-stu-id="4ccbd-168">[Learn more](/azure/cognitive-services/text-analytics/overview) about the Text Analytics API and get started with the [Text Analytics API Python quickstart](/azure/cognitive-services/text-analytics/quickstarts/python).</span></span>


### <a name="spell-check"></a><span data-ttu-id="4ccbd-169">Spell Check</span><span class="sxs-lookup"><span data-stu-id="4ccbd-169">Spell Check</span></span>

<span data-ttu-id="4ccbd-170">Bing Spell Check API를 사용하여 상황별 문법 및 맞춤법 검사를 수행하세요.</span><span class="sxs-lookup"><span data-stu-id="4ccbd-170">Perform contextual grammar and spell checking with the Bing Spell Check API.</span></span>

<span data-ttu-id="4ccbd-171">브라우저에서 [Spell Check API를 사용](https://azure.microsoft.com/en-us/services/cognitive-services/spell-check/)해 보세요.</span><span class="sxs-lookup"><span data-stu-id="4ccbd-171">[Try the Spell Check API](https://azure.microsoft.com/en-us/services/cognitive-services/spell-check/) in your browser.</span></span>

<span data-ttu-id="4ccbd-172">[pip](https://pip.pypa.io/en/stable/quickstart/)를 사용하여 Python 모듈 가져오기:</span><span class="sxs-lookup"><span data-stu-id="4ccbd-172">Get the Python module with [pip](https://pip.pypa.io/en/stable/quickstart/):</span></span>

```python
pip install azure-cognitiveservices-language-spellcheck
```

<span data-ttu-id="4ccbd-173">Spell Check API에 대해 [자세히 알아보고](/azure/cognitive-services/bing-spell-check/proof-text) [Spell Check API Python 빠른 시작](/azure/cognitive-services/bing-spell-check/quickstarts/python)을 시작하세요.</span><span class="sxs-lookup"><span data-stu-id="4ccbd-173">[Learn more](/azure/cognitive-services/bing-spell-check/proof-text) about the Spell Check API and get started with the [Spell Check API Python quickstart](/azure/cognitive-services/bing-spell-check/quickstarts/python).</span></span>
