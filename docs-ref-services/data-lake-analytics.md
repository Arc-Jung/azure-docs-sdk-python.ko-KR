---
title: Python용 Azure Data Lake Analytics 라이브러리
description: Python용 Azure Data Lake Analytics 라이브러리에 대한 참조
keywords: Azure, Python, SDK, API, Data Lake Analytics
author: lisawong19
ms.author: routlaw
manager: douge
ms.date: 08/04/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.openlocfilehash: e98b2f314080146429c89061ab5e154526a87a48
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534309"
---
# <a name="azure-data-lake-analytics-libraries-for-python"></a>Python용 Azure Data Lake Analytics 라이브러리

## <a name="overview"></a>개요
[Azure Data Lake Analytics](/azure/data-lake-analytics/data-lake-analytics-overview)를 사용하여 대규모 데이터 집합으로 조정되는 빅 데이터 분석 작업을 실행합니다.

## <a name="install-the-libraries"></a>라이브러리 설치

## <a name="management-api"></a>관리 API
관리 API를 사용하여 Data Lake Analytics 계정, 작업, 정책 및 카탈로그를 관리합니다.

```bash
pip install azure-mgmt-datalake-analytics
```

### <a name="example"></a>예
이 예제에서는 Data Lake Analytics 계정을 만들고 작업을 제출하는 방법을 보여 줍니다. 

```python
## Required for Azure Resource Manager
from azure.mgmt.resource.resources import ResourceManagementClient
from azure.mgmt.resource.resources.models import ResourceGroup

## Required for Azure Data Lake Store account management
from azure.mgmt.datalake.store import DataLakeStoreAccountManagementClient
from azure.mgmt.datalake.store.models import DataLakeStoreAccount

## Required for Azure Data Lake Store filesystem management
from azure.datalake.store import core, lib, multithread

## Required for Azure Data Lake Analytics account management
from azure.mgmt.datalake.analytics.account import DataLakeAnalyticsAccountManagementClient
from azure.mgmt.datalake.analytics.account.models import DataLakeAnalyticsAccount, DataLakeStoreAccountInfo

## Required for Azure Data Lake Analytics job management
from azure.mgmt.datalake.analytics.job import DataLakeAnalyticsJobManagementClient
from azure.mgmt.datalake.analytics.job.models import JobInformation, JobState, USqlJobProperties

subid= '<Azure Subscription ID>'
rg = '<Azure Resource Group Name>'
location = '<Location>' # i.e. 'eastus2'
adls = '<Azure Data Lake Store Account Name>'
adls = '<Azure Data Lake Analytics Account Name>'

# Create the clients
resourceClient = ResourceManagementClient(credentials, subid)
adlaAcctClient = DataLakeAnalyticsAccountManagementClient(credentials, subid)
adlaJobClient = DataLakeAnalyticsJobManagementClient( credentials, 'azuredatalakeanalytics.net')

# Create resource group
armGroupResult = resourceClient.resource_groups.create_or_update(rg, ResourceGroup(location=location))

# Create a store account
adlaAcctResult = adlaAcctClient.account.create(
    rg,
    adla,
    DataLakeAnalyticsAccount(
        location=location,
        default_data_lake_store_account=adls,
        data_lake_store_accounts=[DataLakeStoreAccountInfo(name=adls)]
    )
).wait()

# Create an ADLA account
adlaAcctResult = adlaAcctClient.account.create(
    rg,
    adla,
    DataLakeAnalyticsAccount(
        location=location,
        default_data_lake_store_account=adls,
        data_lake_store_accounts=[DataLakeStoreAccountInfo(name=adls)]
    )
).wait()

# Submit a job
script = """
@a  = 
    SELECT * FROM 
        (VALUES
            ("Contoso", 1500.0),
            ("Woodgrove", 2700.0)
        ) AS 
              D( customer, amount );
OUTPUT @a
    TO "/data.csv"
    USING Outputters.Csv();
"""

jobId = str(uuid.uuid4())
jobResult = adlaJobClient.job.create(
    adla,
    jobId,
    JobInformation(
        name='Sample Job',
        type='USql',
        properties=USqlJobProperties(script=script)
    )
)
```

> [!div class="nextstepaction"]
> [관리 API 탐색](/python/api/overview/azure/datalakeanalytics/management)

## <a name="samples"></a>샘플
[Azure Data Lake Analytics 관리](https://docs.microsoft.com/azure/data-lake-analytics/data-lake-analytics-manage-use-python-sdk)