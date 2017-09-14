---
title: "Python용 Azure DNS 라이브러리"
description: "Python용 Azure DNS 라이브러리에 대한 참조"
keywords: Azure, Python, SDK, API, DNS
author: sptramer
ms.author: sttramer
manager: douge
ms.date: 07/10/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: 59ae3628b4a810db8fee21aacf46c13054dc8cd3
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-dns-libraries-for-python"></a>Python용 Azure DNS 라이브러리

## <a name="overview"></a>개요

[Azure DNS](/azure/dns/dns-overview)는 Azure 인프라를 통해 DNS 확인을 제공하는 DNS 도메인에 대한 호스팅 서비스입니다.

Azure DNS를 시작하려면 [Azure Portal을 사용하여 Azure DNS 시작](/azure/dns/dns-getstarted-portal)을 참조하세요.

## <a name="management-apis"></a>관리 API

관리 API를 사용하여 DNS 영역 및 레코드를 만들고 관리합니다.

pip를 사용하여 관리 패키지를 설치합니다.

```bash
pip install azure-mgmt-dns
```

### <a name="example"></a>예제

새 DNS 영역을 만듭니다.

```python
from azure.mgmt.dns import DnsManagementClient

dns_client = DnsManagementClient(credentials, 'your-subscription-id')
zone = dns_client.zones.create_or_update('resource-group',
                                         'zone_name_no_dot',
                                         {
                                            "location": "global"
                                         })

```

> [!div class="nextstepaction"]
> [관리 API 탐색](/python/api/overview/azure/dns/managementlibrary)
