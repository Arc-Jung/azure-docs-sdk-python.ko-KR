---
title: Python용 Azure Web Apps 라이브러리
description: ''
keywords: Azure, Python, SDK, API, Web Apps, App Service
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/12/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: appservice
ms.openlocfilehash: 8e8dd78cbc2d5887308361a47a9571ce242aee6e
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/23/2018
ms.locfileid: "29479226"
---
# <a name="azure-web-apps-libraries-for-python"></a>Python용 Azure Web Apps 라이브러리

## <a name="overview"></a>개요

[Azure App Service](/azure/app-service)를 사용하여 웹 사이트, 웹 응용 프로그램, 서비스 및 REST API를 배포하고 크기 조정합니다.

Azure App Service를 시작하려면 [Azure에서 Python 웹앱 만들기](/azure/app-service-web/app-service-web-get-started-python)를 참조하세요.

## <a name="management-api"></a>관리 API

관리 API를 사용하여 Azure App Service에서 호스팅되는 요소를 배포, 관리 및 크기 조정합니다.

pip를 통해 라이브러리를 설치합니다.

```bash
pip install azure-mgmt-web
```

### <a name="example"></a>예

GitHub 리포지토리에서 Azure Web App으로 웹앱을 배포합니다.

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
> [관리 API 탐색](/python/api/overview/azure/webapps/management)

## <a name="samples"></a>샘플 

* [Python을 사용하여 Azure 웹 사이트 관리(영문)][1]
* [논리 앱 워크플로 만들기][2]
 
웹 응용 프로그램 샘플의 [전체 목록](https://azure.microsoft.com/en-us/resources/samples/?platform=python&term=web-app)을 봅니다.

[1]: https://azure.microsoft.com/resources/samples/app-service-web-python-manage
[2]: ../docs-ref-conceptual/python-sdk-azure-samples-logic-app-workflow.md