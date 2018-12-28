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
# <a name="azure-libraries-for-python"></a><span data-ttu-id="e0c8e-104">Python용 Azure 라이브러리</span><span class="sxs-lookup"><span data-stu-id="e0c8e-104">Azure libraries for Python</span></span>

<span data-ttu-id="e0c8e-105">Python용 Azure 라이브러리를 사용하면 Azure 서비스를 사용하고 애플리케이션 코드에서 Azure 리소스를 관리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0c8e-105">The Azure libraries for Python let you use Azure services and manage Azure resources from your application code.</span></span> 

## <a name="manage-azure-resources"></a><span data-ttu-id="e0c8e-106">Azure 리소스 관리</span><span class="sxs-lookup"><span data-stu-id="e0c8e-106">Manage Azure resources</span></span>

<span data-ttu-id="e0c8e-107">Python용 Azure 라이브러리를 사용하여 Python 애플리케이션에서 Azure 리소스를 만들고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="e0c8e-107">Create and manage Azure resources from Python applications using the Azure libraries for Python.</span></span>

<span data-ttu-id="e0c8e-108">예를 들어 SQL Server 인스턴스를 만들려면 다음 코드를 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0c8e-108">For example, to create a SQL Server instance, you can use the following code:</span></span>

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

<span data-ttu-id="e0c8e-109">라이브러리의 전체 목록 및 프로젝트로 가져오는 방법에 대한 [설치 지침](python-sdk-azure-install.md)을 검토한 다음 [시작 문서](python-sdk-azure-get-started.yml)를 참조하여 인증을 설정하고 자신의 Azure 구독에 대한 샘플 코드를 실행합니다 .</span><span class="sxs-lookup"><span data-stu-id="e0c8e-109">Review the [install instructions](python-sdk-azure-install.md) for a full list of the libraries and how to import them into your projects and then read the [get started article](python-sdk-azure-get-started.yml) to set up your authentication and run sample code against your own Azure subscription.</span></span>

## <a name="connect-to-azure-services"></a><span data-ttu-id="e0c8e-110">Azure 서비스에 연결</span><span class="sxs-lookup"><span data-stu-id="e0c8e-110">Connect to Azure services</span></span>

<span data-ttu-id="e0c8e-111">Python 라이브러리를 사용하여 Azure 내에서 리소스를 만들고 관리하는 것 외에도, Python 라이브러리를 사용하여 앱에서 해당 리소스를 연결하여 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0c8e-111">In addition to using Python libraries to create and manage resources within Azure, you can also use Python libraries to connect and use those resources in your apps.</span></span> <span data-ttu-id="e0c8e-112">예를 들어 SQL Database 테이블을 업데이트하거나 Azure Storage에 파일을 저장할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0c8e-112">For example, you might update a table SQL Database or store files in Azure Storage.</span></span> <span data-ttu-id="e0c8e-113">라이브러리 전체 목록에서 특정 서비스에 필요한 라이브러리를 선택하고, Python 개발자 센터를 방문하여 앱에서 사용하는 데 도움이 되는 자습서와 샘플 코드를 참조합니다.</span><span class="sxs-lookup"><span data-stu-id="e0c8e-113">Select the library you need for a particular service from the complete list of libraries and visit the Python developer center for tutorials and sample code for help using them in your apps.</span></span>

<span data-ttu-id="e0c8e-114">예를 들어 Blob에 간단한 HTML 페이지를 업로드하고 URL을 얻으려면 다음과 같습니다.</span><span class="sxs-lookup"><span data-stu-id="e0c8e-114">For example, to upload a simple HTML page on a blob and get the Url:</span></span>

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

## <a name="sample-code-and-reference"></a><span data-ttu-id="e0c8e-115">샘플 코드 및 참조</span><span class="sxs-lookup"><span data-stu-id="e0c8e-115">Sample code and reference</span></span>
<span data-ttu-id="e0c8e-116">다음 샘플은 Python용 Azure 관리 라이브러리를 사용한 일반적인 자동화 작업을 다루며 앱에 바로 사용할 수 있는 코드도 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0c8e-116">The following samples cover common automation tasks with the Azure management libraries for Python and have code ready to use in your own apps:</span></span>
- [<span data-ttu-id="e0c8e-117">Virtual Machines</span><span class="sxs-lookup"><span data-stu-id="e0c8e-117">Virtual Machines</span></span>](python-sdk-azure-virtual-machine-samples.md)
- [<span data-ttu-id="e0c8e-118">웹앱</span><span class="sxs-lookup"><span data-stu-id="e0c8e-118">Web apps</span></span>](python-sdk-azure-web-apps-samples.md)
- [<span data-ttu-id="e0c8e-119">SQL Database</span><span class="sxs-lookup"><span data-stu-id="e0c8e-119">SQL Database</span></span>](python-sdk-azure-sql-database-samples.md)

<span data-ttu-id="e0c8e-120">[참조](/python/api/overview/azure)는 서비스 라이브러리와 관리 라이브러리의 모든 패키지에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0c8e-120">A [reference](/python/api/overview/azure) is available for all packages in both the service an management libraries.</span></span> <span data-ttu-id="e0c8e-121">새 기능, 주요 변경 내용 및 이전 버전에서의 마이그레이션 지침은 [릴리스 정보](python-sdk-azure-release-notes.md)에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="e0c8e-121">New features, breaking changes, and migration instructions from previous versions are available in the [release notes](python-sdk-azure-release-notes.md).</span></span> 

## <a name="get-help-and-give-feedback"></a><span data-ttu-id="e0c8e-122">도움말 가져오기 및 피드백 제공</span><span class="sxs-lookup"><span data-stu-id="e0c8e-122">Get help and give feedback</span></span>

<span data-ttu-id="e0c8e-123">[Stack Overflow](http://stackoverflow.com/questions/tagged/azure-sdk-python)에서 커뮤니티에 질문을 게시하고 [프로젝트 GitHub](https://github.com/Azure/azure-sdk-for-python)에서 SDK에 대한 문제를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="e0c8e-123">Post questions to the community on [Stack Overflow](http://stackoverflow.com/questions/tagged/azure-sdk-python) and open issues against the SDK on the [project GitHub](https://github.com/Azure/azure-sdk-for-python).</span></span>
