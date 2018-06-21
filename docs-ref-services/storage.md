---
title: Python용 Azure Storage 라이브러리
description: ''
keywords: Azure, Python, SDK, API, Storage
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/12/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: storage
ms.openlocfilehash: e45b12af9e026e0f6390556813385d86784feaa4
ms.sourcegitcommit: 86f7f40295271ef94272642efb89b471aae99a2c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2018
ms.locfileid: "35720064"
---
# <a name="azure-storage-libraries-for-python"></a><span data-ttu-id="71dce-103">Python용 Azure Storage 라이브러리</span><span class="sxs-lookup"><span data-stu-id="71dce-103">Azure Storage libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="71dce-104">개요</span><span class="sxs-lookup"><span data-stu-id="71dce-104">Overview</span></span>
- <span data-ttu-id="71dce-105">[Azure Blob 저장소](https://docs.microsoft.com/en-us/azure/storage/storage-python-how-to-use-blob-storage)에서 개체와 파일 읽기 및 쓰기</span><span class="sxs-lookup"><span data-stu-id="71dce-105">Read and write objects and files from [Azure Blob storage](https://docs.microsoft.com/en-us/azure/storage/storage-python-how-to-use-blob-storage)</span></span>
- <span data-ttu-id="71dce-106">[Azure 큐 저장소](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-queue-storage)를 사용하여 클라우드에 연결된 응용 프로그램 간에 메시지 보내기 및 받기</span><span class="sxs-lookup"><span data-stu-id="71dce-106">Send and receive messages between cloud-connected applications with [Azure Queue storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-queue-storage)</span></span>
- <span data-ttu-id="71dce-107">[Azure 테이블 저장소](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-table-storage)를 사용하여 대규모 구조적 데이터를 읽고 씁니다.</span><span class="sxs-lookup"><span data-stu-id="71dce-107">Read and write large structured data with [Azure Table storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-table-storage)</span></span> 
- <span data-ttu-id="71dce-108">[Azure 파일 저장소](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-file-storage)를 사용하여 앱 간에 저장소를 공유합니다.</span><span class="sxs-lookup"><span data-stu-id="71dce-108">Share storage between apps with [Azure File storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-file-storage)</span></span>

<span data-ttu-id="71dce-109">관리 라이브러리를 사용하여 Azure Storage 계정을 생성, 업데이트 및 관리하고, Python 코드에서 액세스 키를 쿼리하고 다시 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="71dce-109">Create, update, and manage Azure Storage accounts and query and regenerate access keys from your Python code with the management libraries.</span></span>

## <a name="install-the-libraries"></a><span data-ttu-id="71dce-110">라이브러리 설치</span><span class="sxs-lookup"><span data-stu-id="71dce-110">Install the libraries</span></span>

### <a name="client"></a><span data-ttu-id="71dce-111">클라이언트</span><span class="sxs-lookup"><span data-stu-id="71dce-111">Client</span></span>

<span data-ttu-id="71dce-112">Azure Storage 클라이언트 라이브러리는 Blob, 파일, 큐 및 테이블의 4개 패키지로 구성되어 있습니다.</span><span class="sxs-lookup"><span data-stu-id="71dce-112">Azure Storage Client Libraries consist of 4 packages: Blob, File, Queue and Table.</span></span> <span data-ttu-id="71dce-113">Blob 패키지를 설치하려면 다음을 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="71dce-113">To install the blob package, run:</span></span>

```bash
pip install azure-storage-blob
```

### <a name="management"></a><span data-ttu-id="71dce-114">관리</span><span class="sxs-lookup"><span data-stu-id="71dce-114">Management</span></span>

```bash
pip install azure-mgmt-storage
```

## <a name="example"></a><span data-ttu-id="71dce-115">예</span><span class="sxs-lookup"><span data-stu-id="71dce-115">Example</span></span>
```python
from azure.storage.blob import BlockBlobService

blob_service = BlockBlobService(account_name, account_key)

blob_service.create_container(
    'mycontainername',
    public_access=PublicAccess.Blob
)

blob_service.create_blob_from_bytes(
    'mycontainername',
    'myblobname',
    b'<center><h1>Hello World!</h1></center>',
    content_settings=ContentSettings('text/html')
)

print(blob_service.make_blob_url('mycontainername', 'myblobname'))
```

## <a name="samples"></a><span data-ttu-id="71dce-116">샘플</span><span class="sxs-lookup"><span data-stu-id="71dce-116">Samples</span></span>

| | |
|--|--|
| [<span data-ttu-id="71dce-117">Python에서 Azure Blob Storage 시작(영문)</span><span class="sxs-lookup"><span data-stu-id="71dce-117">Get started with Azure Blob Storage in Python</span></span>](https://docs.microsoft.com/en-us/azure/storage/blobs/storage-python-how-to-use-blob-storage) | <span data-ttu-id="71dce-118">Azure Storage에서 파일과 개체를 생성, 판독, 업데이트, 액세스 제한 및 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="71dce-118">Create, read, update, restrict access, and delete files and objects in Azure Storage.</span></span> |
| [<span data-ttu-id="71dce-119">Python에서 Azure Queue Storage 시작(영문)</span><span class="sxs-lookup"><span data-stu-id="71dce-119">Get started with Azure Queue Storage in Python</span></span>](https://docs.microsoft.com/en-us/azure/storage/queues/storage-python-how-to-use-queue-storage) | <span data-ttu-id="71dce-120">Azure Storage 큐에서 메시지를 삽입, 피킹, 검색 및 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="71dce-120">Insert, peek, retrieve and delete messages from Azure Storage queues.</span></span> | 
| [<span data-ttu-id="71dce-121">Azure Storage 계정 관리(영문)</span><span class="sxs-lookup"><span data-stu-id="71dce-121">Manage Azure Storage accounts</span></span>](https://azure.microsoft.com/resources/samples/storage-python-manage) | <span data-ttu-id="71dce-122">저장소 계정을 생성, 업데이트 및 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="71dce-122">Create, update , and delete storage accounts.</span></span> <span data-ttu-id="71dce-123">저장소 계정 액세스 키를 검색하고 다시 생성합니다.</span><span class="sxs-lookup"><span data-stu-id="71dce-123">Retrieve and regenerate storage account access keys.</span></span>

<span data-ttu-id="71dce-124">앱에서 사용할 수 있는 [Python 샘플 코드](https://azure.microsoft.com/resources/samples/?platform=python)를 추가로 탐색합니다.</span><span class="sxs-lookup"><span data-stu-id="71dce-124">Explore more [sample Python code](https://azure.microsoft.com/resources/samples/?platform=python) you can use in your apps.</span></span>
