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
ms.openlocfilehash: 5b4d4cc2dfb32dceb66bdb5be3fe0f0075840d8f
ms.sourcegitcommit: 434186988284e0a8268a9de11645912a81226d6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/29/2019
ms.locfileid: "66376753"
---
# <a name="azure-storage-libraries-for-python"></a>Python용 Azure Storage 라이브러리

## <a name="overview"></a>개요
- [Azure Blob Storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-blob-storage)에서 개체와 파일 읽기 및 쓰기
- [Azure Queue Storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-queue-storage)를 사용하여 클라우드에 연결된 응용 프로그램 간에 메시지 보내기 및 받기
- [Azure Table Storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-table-storage)를 사용하여 대규모 구조적 데이터를 읽고 씁니다. 
- [Azure File Storage](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-file-storage)를 사용하여 앱 간에 스토리지를 공유합니다.

관리 라이브러리를 사용하여 Azure Storage 계정을 생성, 업데이트 및 관리하고, Python 코드에서 액세스 키를 쿼리하고 다시 생성합니다.

## <a name="install-the-libraries"></a>라이브러리 설치

### <a name="client"></a>클라이언트

Azure Storage 클라이언트 라이브러리는 Blob, File, Queue 및 Table의 4개 패키지로 구성되어 있습니다. Blob 패키지를 설치하려면 다음을 실행합니다.

```bash
pip install azure-storage-blob
```

### <a name="management"></a>관리

```bash
pip install azure-mgmt-storage
```

## <a name="example"></a>예
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

## <a name="samples"></a>샘플

| | |
|--|--|
| [Python에서 Azure Blob Storage 시작(영문)](https://docs.microsoft.com/azure/storage/blobs/storage-python-how-to-use-blob-storage) | Azure Storage에서 파일과 개체를 생성, 판독, 업데이트, 액세스 제한 및 삭제합니다. |
| [Python에서 Azure Queue Storage 시작(영문)](https://docs.microsoft.com/azure/storage/queues/storage-python-how-to-use-queue-storage) | Azure Storage 큐에서 메시지를 삽입, 피킹, 검색 및 삭제합니다. | 
| [Azure Storage 계정 관리(영문)](https://azure.microsoft.com/resources/samples/storage-python-manage) | 저장소 계정을 생성, 업데이트 및 삭제합니다. 저장소 계정 액세스 키를 검색하고 다시 생성합니다.

앱에서 사용할 수 있는 [Python 샘플 코드](https://azure.microsoft.com/resources/samples/?platform=python)를 추가로 탐색합니다.
