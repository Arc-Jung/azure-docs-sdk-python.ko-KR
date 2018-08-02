---
title: Python용 Azure MySQL/PostgreSQL 라이브러리
description: ''
keywords: Azure, Python, SDK, API, SQL, 데이터베이스, MySQL, PostgreSQL
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 07/19/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.openlocfilehash: e3cd84288ad8d49cfcd673506e2db150c02e7918
ms.sourcegitcommit: 16eecfc4ed0e2a8344ce5887327cdf2619ba89e4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/21/2018
ms.locfileid: "39189593"
---
# <a name="azure-mysqlpostgresql-libraries-for-python"></a>Python용 Azure MySQL/PostgreSQL 라이브러리

## <a name="mysql"></a>MySQL

MySQL 관리자 및 pyodbc를 사용하여 Python에서 [Azure MySQL Database](/azure/mysql/overview)에 저장된 리소스 및 데이터로 작업합니다.

### <a name="client-odbc-driver-and-pyodbc"></a>Client ODBC 드라이버 및 pyodbc

Azure Database for MySQL에 액세스하는 데 권장되는 클라이언트 라이브러리는 Microsoft [ODBC 드라이버](/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries)입니다. ODBC 드라이버를 사용하여 데이터베이스에 연결하고 SQL 문을 직접 실행합니다.

#### <a name="example"></a>예

Azure Database for MySQL에 연결하고 sales 테이블의 모든 레코드를 선택합니다. Azure Portal에서 데이터베이스에 대한 ODBC 연결 문자열을 가져올 수 있습니다.

```python
SERVER = 'YOUR_SEVER_NAME' + '.mysql.database.azure.com'
DATABASE = 'YOUR_DATABASE_NAME'
USERNAME = 'YOUR_MYSQL_USERNAME'
PASSWORD = 'YOUR_MYSQL_PASSWORD'

DRIVER = '{MySQL ODBC 5.3 UNICODE Driver}'
cnxn = pyodbc.connect(
    'DRIVER=' + DRIVER + ';PORT=3306;SERVER=' + SERVER + ';PORT=3306;DATABASE=' + DATABASE + ';UID=' + USERNAME + ';PWD=' + PASSWORD)
cursor = cnxn.cursor()
selectsql = "SELECT * FROM SALES"  # SALES is an example table name
cursor.execute(selectsql)
```

### <a name="management-api"></a>관리 API

관리 API를 사용하여 구독의 MySQL 리소스를 만들고 관리합니다.

#### <a name="requirements"></a>요구 사항
Python용 MySQL 관리 라이브러리를 설치해야 합니다.
```bash
pip install azure-mgmt-rdbms
```

관리 클라이언트에서 인증할 자격 증명을 얻는 방법에 대한 자세한 내용은 [Python SDK 인증](https://docs.microsoft.com/python/azure/python-sdk-azure-authenticate) 페이지를 참조하세요.

#### <a name="example"></a>예

MySQL 5.7 Database 리소스를 만들고 방화벽 규칙을 사용하여 IP 주소 범위에 대한 액세스를 제한합니다.

```python

from azure.mgmt.rdbms.mysql import MySQLManagementClient
from azure.mgmt.rdbms.mysql.models import ServerForCreate, ServerPropertiesForDefaultCreate, ServerVersion

SUBSCRIPTION_ID = "YOUR_AZURE_SUBSCRIPTION_ID"
RESOURCE_GROUP = "YOUR_AZURE_RESOURCE-GROUP_WITH_POSTGRES"
MYSQL_SERVER = "YOUR_DESIRED_MYSQL_SERVER_NAME"
MYSQL_ADMIN_USER = "YOUR_MYSQL_ADMIN_USERNAME"
MYSQL_ADMIN_PASSWORD = "YOUR_MYSQL_ADMIN_PASSOWRD"
LOCATION = "westus"  # example Azure availability zone, should match resource group


client = MySQLManagementClient(credentials=creds,
    subscription_id=SUBSCRIPTION_ID)

server_creation_poller = client.servers.create_or_update(
    resource_group_name=RESOURCE_GROUP,
    server_name=MYSQL_SERVER,
    ServerForCreate(
        ServerPropertiesForDefaultCreate(
            administrator_login=MYSQL_ADMIN_USER,
            administrator_login_password=MYSQL_ADMIN_PASSWORD,
            version=ServerVersion.five_full_stop_seven
        ),
        location=LOCATION
    )
)

server = server_creation_poller.result()

# Open access to this server for IPs
rule_creation_poller = client.firewall_rules.create_or_update(
    RESOURCE_GROUP
    MYSQL_SERVER,
    "some_custom_ip_range_whitelist_rule_name",  # Custom firewall rule name
    "123.123.123.123",  # Start ip range
    "167.220.0.235"  # End ip range
)

firewall_rule = rule_creation_poller.result()
```

> [!div class="nextstepaction"]
> [관리 API 탐색](/python/api/overview/azure/postgresql/mysql/management)

## <a name="postgresql"></a>PostgreSQL
ODBC 드라이버 및 pyodbc를 사용하여 데이터베이스에 연결하고 SQL 문을 직접 실행합니다.

[Azure Database for PostgreSQL](https://docs.microsoft.com/azure/postgresql/)에 대해 자세히 알아보세요.

### <a name="client-odbc-driver-and-pyodbc"></a>Client ODBC 드라이버 및 pyodbc
Azure Database for PostgreSQL에 액세스하는 데 권장되는 클라이언트 라이브러리는 Microsoft [ODBC 드라이버 및 pyodbc](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries)입니다.

#### <a name="example"></a>예 

Azure Database for PostgreSQL에 연결하고 `SALES` 테이블의 모든 레코드를 선택합니다. Azure Portal에서 데이터베이스에 대한 ODBC 연결 문자열을 가져올 수 있습니다.

```python
import pyodbc

SERVER = 'YOUR_SERVER_NAME.postgres.database.azure.com'
DATABASE = 'YOUR_DB_NAME'
USERNAME = 'YOUR_USERNAME'
PASSWORD = 'YOUR_PASSWORD'

DRIVER = '{PostgreSQL ODBC Driver}'
cnxn = pyodbc.connect(
    'DRIVER=' + DRIVER + ';PORT=5432;SERVER=' + SERVER +
    ';PORT=5432;DATABASE=' + DATABASE + ';UID=' + USERNAME +
    ';PWD=' + PASSWORD)
cursor = cnxn.cursor()
selectsql = "SELECT * FROM SALES" # SALES is an example table name
cursor.execute(selectsql)
```

### <a name="management-api"></a>관리 API
#### <a name="requirements"></a>요구 사항
Python용 PostgreSQL 관리 라이브러리를 설치해야 합니다.
```bash
pip install azure-mgmt-rdbms
```

관리 클라이언트에서 인증할 자격 증명을 얻는 방법에 대한 자세한 내용은 [Python SDK 인증](https://docs.microsoft.com/python/azure/python-sdk-azure-authenticate) 페이지를 참조하세요.

#### <a name="example"></a>예
이 예제에서는 기존 Postgres 서버에 새 Postgres 데이터베이스를 만듭니다.
```python
from azure.mgtm.rdbms.postgresql import PostgreSQLManagementClient

SUBSCRIPTION_ID = "YOUR_AZURE_SUBSCRIPTION_ID"
RESOURCE_GROUP = "YOUR_AZURE_RESOURCE_GROUP_WITH_POSTGRES"
POSTGRES_SERVER = "YOUR_POSTGRES_SERVER_NAME"
DB_NAME = "YOUR_DESIRED_DATABASE_NAME"

client = PostgreSQLManagementClient(credentials, SUBSCRIPTION_ID)

db_creation_poller = client.databases.create_or_update(
    resource_group_name=RESOURCE_GROUP,
    server_name=POSTGRES_SERVER, database_name=DB_NAME)
db = db_creation_poller.result()
```

> [!div class="nextstepaction"]
> [관리 API 탐색](/python/api/overview/azure/postgresql/mysql/management)