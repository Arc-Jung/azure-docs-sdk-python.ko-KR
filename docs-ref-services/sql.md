---
title: "Python용 Azure SQL Database 라이브러리"
description: 
keywords: "Azure, Python, SDK, API, SQL, 데이터베이스, pyodbc"
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 07/11/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: sql-database
ms.openlocfilehash: b580c5011412bc77fd8fd55b709a305be07e2316
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-sql-database-libraries-for-python"></a>Python용 Azure SQL Database 라이브러리

## <a name="overview"></a>개요

Microsoft ODBC 드라이버와 pyodbc를 사용하여 Python에서 [Azure SQL Database](/azure/sql-database/sql-database-technical-overview)에 저장된 데이터로 작업합니다. 

## <a name="client-odbc-driver-and-pyodbc"></a>Client ODBC 드라이버 및 pyodbc

```bash
pip install pyodbc
```
Python 및 데이터베이스 통신 라이브러리 설치에 대한 자세한 내용은 [여기서](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries) 찾을 수 있습니다.

### <a name="example"></a>예제

SQL 데이터베이스에 연결하고 테이블의 모든 레코드를 선택합니다.

```python
import pyodbc 

SERVER = 'YOUR_SERVER_NAME.database.windows.net'
DATABASE = 'YOUR_DATABASE_NAME'
USERNAME = 'YOUR_DB_USERNAME'
PASSWORD = 'YOUR_DB_PASSWORD'

DRIVER= '{ODBC Driver 13 for SQL Server}'
cnxn = pyodbc.connect('DRIVER=' + DRIVER + ';PORT=1433;SERVER=' + SERVER +
    ';PORT=1443;DATABASE=' + DATABASE + ';UID=' + USERNAME + ';PWD=' + PASSWORD)
cursor = cnxn.cursor()
selectsql = "SELECT * FROM SALES"  # SALES is an example table name
cursor.execute(selectsql)
```

## <a name="management-api"></a>관리 API

관리 API를 사용하여 구독의 Azure SQL Database 리소스를 만들고 관리합니다. 

```bash
pip install azure-mgmt-sql
```

### <a name="example"></a>예제

SQL Database 리소스를 만들고 방화벽 규칙을 사용하여 IP 주소 범위에 대한 액세스를 제한합니다.

```python
RESOURCE_GROUP = 'YOUR_RESOURCE_GROUP_NAME'
LOCATION = 'eastus'  # example Azure availability zone, should match resource group
SQL_DB = 'YOUR_SQLDB_NAME'

# Create a SQL server
server = sql_client.servers.create_or_update(
    RESOURCE_GROUP,
    SQL_DB,
    {
        'location': LOCATION,
        'version': '12.0', # Required for create
        'administrator_login': USERNAME, # Required for create
        'administrator_login_password': PASSWORD # Required for create
    }
)

# Open access to this server for IPs
firewall_rule = sql_client.firewall_rules.create_or_update(
    RESOURCE_GROUP
    SQL_DB,
    "firewall_rule_name_123.123.123.123",
    "123.123.123.123", # Start ip range
    "167.220.0.235"  # End ip range
)
```
> [!div class="nextstepaction"]
> [관리 API 탐색](/python/api/overview/azure/sql/managementlibrary)

## <a name="samples"></a>샘플

* [SQL 데이터베이스 만들기 및 관리][1]    
* [Python을 사용하여 데이터 연결 및 쿼리][2]   

[1]: https://github.com/Azure-Samples/sql-database-python-manage
[2]: https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python

Azure SQL 데이터베이스 샘플의 [전체 목록](https://azure.microsoft.com/resources/samples/?platform=python&term=SQL)을 봅니다. 