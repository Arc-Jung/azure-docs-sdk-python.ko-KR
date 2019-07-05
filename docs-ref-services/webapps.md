---
title: Python용 Azure Web Apps 라이브러리
description: ''
keywords: Azure, Python, SDK, API, Web Apps, App Service
author: lisawong19
ms.author: routlaw
manager: douge
ms.date: 06/12/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: appservice
ms.openlocfilehash: 26b578d9edc7023c06d4c9bfc8c8fb44a169c40d
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534172"
---
# <a name="azure-web-apps-libraries-for-python"></a><span data-ttu-id="195cf-103">Python용 Azure Web Apps 라이브러리</span><span class="sxs-lookup"><span data-stu-id="195cf-103">Azure Web Apps libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="195cf-104">개요</span><span class="sxs-lookup"><span data-stu-id="195cf-104">Overview</span></span>

<span data-ttu-id="195cf-105">[Azure App Service](/azure/app-service)를 사용하여 웹 사이트, 웹 애플리케이션, 서비스 및 REST API를 배포하고 크기 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="195cf-105">Deploy and scale websites, web applications, services, and REST APIs with [Azure App Service](/azure/app-service).</span></span>

<span data-ttu-id="195cf-106">Azure App Service를 시작하려면 [Azure에서 Python 웹앱 만들기](/azure/app-service-web/app-service-web-get-started-python)를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="195cf-106">To get started with Azure App Service, see [Create a Python web app in Azure](/azure/app-service-web/app-service-web-get-started-python).</span></span>

## <a name="management-api"></a><span data-ttu-id="195cf-107">관리 API</span><span class="sxs-lookup"><span data-stu-id="195cf-107">Management API</span></span>

<span data-ttu-id="195cf-108">관리 API를 사용하여 Azure App Service에서 호스팅되는 요소를 배포, 관리 및 크기 조정합니다.</span><span class="sxs-lookup"><span data-stu-id="195cf-108">Deploy, manage, and scale elements hosted in the Azure App Service with the management API.</span></span>

<span data-ttu-id="195cf-109">pip를 통해 라이브러리를 설치합니다.</span><span class="sxs-lookup"><span data-stu-id="195cf-109">Install the library via pip.</span></span>

```bash
pip install azure-mgmt-web
```

### <a name="example"></a><span data-ttu-id="195cf-110">예</span><span class="sxs-lookup"><span data-stu-id="195cf-110">Example</span></span>

<span data-ttu-id="195cf-111">GitHub 리포지토리에서 Azure Web App으로 웹앱을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="195cf-111">Deploy a webapp from a GitHub repository into Azure Web App.</span></span>

```python
siteConfiguration = SiteConfig(
    python_version='3.4'
)

# create a web app
web_client.web_apps.create_or_update(
    RESOURCE_GROUP_NAME,
    WEB_APP_NAME,
    Site(
        location='eastus',
        server_farm_id=SERVICE_PLAN_ID,
        site_config=siteConfiguration
    )
)

# continuous deployment with GitHub
source_control_async_operation = web_client.web_apps.create_or_update_source_control(
    RESOURCE_GROUP_NAME,
    WEB_APP_NAME,
    SiteSourceControl(
        location='GitHub',
        repo_url='https://github.com/lisawong19/python-docs-hello-world',
        branch='master'
    )
)
```

> [!div class="nextstepaction"]
> [<span data-ttu-id="195cf-112">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="195cf-112">Explore the Management APIs</span></span>](/python/api/overview/azure/webapps/management)

## <a name="samples"></a><span data-ttu-id="195cf-113">샘플</span><span class="sxs-lookup"><span data-stu-id="195cf-113">Samples</span></span>

* <span data-ttu-id="195cf-114">[Python을 사용하여 Azure 웹 사이트 관리(영문)][1]</span><span class="sxs-lookup"><span data-stu-id="195cf-114">[Manage Azure websites with python][1]</span></span>
* <span data-ttu-id="195cf-115">[논리 앱 워크플로 만들기][2]</span><span class="sxs-lookup"><span data-stu-id="195cf-115">[Create a Logic App workflow][2]</span></span>

<span data-ttu-id="195cf-116">웹 애플리케이션 샘플의 [전체 목록](https://azure.microsoft.com/resources/samples/?platform=python&term=web-app)을 봅니다.</span><span class="sxs-lookup"><span data-stu-id="195cf-116">View the [complete list](https://azure.microsoft.com/resources/samples/?platform=python&term=web-app) of web application samples.</span></span>

[1]: https://azure.microsoft.com/resources/samples/app-service-web-python-manage
[2]: ../docs-ref-conceptual/python-sdk-azure-samples-logic-app-workflow.md
