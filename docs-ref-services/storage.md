---
title: "Python용 Azure Storage 라이브러리"
description: 
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
ms.openlocfilehash: 64465964d32934a6a45dec44cb92a0a8a84b9c37
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-storage-libraries-for-python"></a>Python용 Azure Storage 라이브러리

## <a name="overview"></a>개요
- [Azure Blob 저장소](https://docs.microsoft.com/en-us/azure/storage/storage-python-how-to-use-blob-storage)에서 개체와 파일을 읽고 씁니다.
- [Azure 큐 저장소](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-queue-storage)를 사용하여 클라우드에 연결된 응용 프로그램 간에 메시지를 보내고 받습니다.
- [Azure 테이블 저장소](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-table-storage)를 사용하여 대규모 구조적 데이터를 읽고 씁니다. 
- [Azure 파일 저장소](https://docs.microsoft.com/azure/storage/storage-python-how-to-use-file-storage)를 사용하여 앱 간에 저장소를 공유합니다.

관리 라이브러리를 사용하여 Azure Storage 계정을 생성, 업데이트 및 관리하고, Python 코드에서 액세스 키를 쿼리하고 다시 생성합니다.

## <a name="install-the-libraries"></a>라이브러리 설치

### <a name="client"></a>클라이언트

```bash
pip install azure-storage
```

### <a name="management"></a>관리

```bash
pip install azure-mgmt-storage
```

## <a name="example"></a>예제
```python
storage_client = CloudStorageAccount(storage_account_name, storage_key)
blob_service = storage_client.create_block_blob_service()

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
| [Python에서 Azure Blob Storage 시작(영문)](https://azure.microsoft.com/resources/samples/storage-blob-python-getting-started/) | Azure Storage에서 파일과 개체를 생성, 판독, 업데이트, 액세스 제한 및 삭제합니다. |
| [Python에서 Azure Queue Storage 시작(영문)](https://azure.microsoft.com/resources/samples/storage-queue-python-getting-started/) | Azure Storage 큐에서 메시지를 삽입, 피킹, 검색 및 삭제합니다. | 
| [Azure Storage 계정 관리(영문)](https://azure.microsoft.com/resources/samples/storage-python-manage) | 저장소 계정을 생성, 업데이트 및 삭제합니다. 저장소 계정 액세스 키를 검색하고 다시 생성합니다.

앱에서 사용할 수 있는 [Python 샘플 코드](https://azure.microsoft.com/resources/samples/?platform=python)를 추가로 탐색합니다.