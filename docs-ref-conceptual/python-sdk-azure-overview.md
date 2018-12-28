---
title: Python용 Azure 라이브러리
description: Python용 Azure 관리 및 서비스 라이브러리에 대한 개요입니다.
keywords: Azure, Python, SDK, API
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/01/2017
ms.topic: article
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.assetid: ''
ms.openlocfilehash: 2b3e6d31edd7b946664853b3478e22205ab8c92e
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/23/2018
ms.locfileid: "29478806"
---
# <a name="azure-libraries-for-python"></a>Python용 Azure 라이브러리

Python용 Azure 라이브러리를 사용하면 Azure 서비스를 사용하고 애플리케이션 코드에서 Azure 리소스를 관리할 수 있습니다. 

## <a name="manage-azure-resources"></a>Azure 리소스 관리

Python용 Azure 라이브러리를 사용하여 Python 애플리케이션에서 Azure 리소스를 만들고 관리합니다.

예를 들어 SQL Server 인스턴스를 만들려면 다음 코드를 사용할 수 있습니다.

```python
sql_client = SqlManagementClient(
    credentials,
    subscription_id
)

server = sql_client.servers.create_or_update(
    'myresourcegroup',
    'myservername',
    {
        'location': 'eastus',
        'version': '12.0', # Required for create
        'administrator_login': 'mysecretname', # Required for create
        'administrator_login_password': 'HusH_Sec4et' # Required for create
    }
)
```

라이브러리의 전체 목록 및 프로젝트로 가져오는 방법에 대한 [설치 지침](python-sdk-azure-install.md)을 검토한 다음 [시작 문서](python-sdk-azure-get-started.yml)를 참조하여 인증을 설정하고 자신의 Azure 구독에 대한 샘플 코드를 실행합니다 .

## <a name="connect-to-azure-services"></a>Azure 서비스에 연결

Python 라이브러리를 사용하여 Azure 내에서 리소스를 만들고 관리하는 것 외에도, Python 라이브러리를 사용하여 앱에서 해당 리소스를 연결하여 사용할 수 있습니다. 예를 들어 SQL Database 테이블을 업데이트하거나 Azure Storage에 파일을 저장할 수 있습니다. 라이브러리 전체 목록에서 특정 서비스에 필요한 라이브러리를 선택하고, Python 개발자 센터를 방문하여 앱에서 사용하는 데 도움이 되는 자습서와 샘플 코드를 참조합니다.

예를 들어 Blob에 간단한 HTML 페이지를 업로드하고 URL을 얻으려면 다음과 같습니다.

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

## <a name="sample-code-and-reference"></a>샘플 코드 및 참조
다음 샘플은 Python용 Azure 관리 라이브러리를 사용한 일반적인 자동화 작업을 다루며 앱에 바로 사용할 수 있는 코드도 있습니다.
- [Virtual Machines](python-sdk-azure-virtual-machine-samples.md)
- [웹앱](python-sdk-azure-web-apps-samples.md)
- [SQL Database](python-sdk-azure-sql-database-samples.md)

[참조](/python/api/overview/azure)는 서비스 라이브러리와 관리 라이브러리의 모든 패키지에서 사용할 수 있습니다. 새 기능, 주요 변경 내용 및 이전 버전에서의 마이그레이션 지침은 [릴리스 정보](python-sdk-azure-release-notes.md)에서 사용할 수 있습니다. 

## <a name="get-help-and-give-feedback"></a>도움말 가져오기 및 피드백 제공

[Stack Overflow](http://stackoverflow.com/questions/tagged/azure-sdk-python)에서 커뮤니티에 질문을 게시하고 [프로젝트 GitHub](https://github.com/Azure/azure-sdk-for-python)에서 SDK에 대한 문제를 엽니다.
