---
title: Python용 Azure MySQL/PostgreSQL 라이브러리
description: ''
keywords: Azure, Python, SDK, API, SQL, 데이터베이스, MySQL, PostgreSQL
author: lisawong19
ms.author: routlaw
manager: douge
ms.date: 07/19/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.openlocfilehash: 81a29ea16dc9857257859181f0c2e5be8b4b7901
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534231"
---
# <a name="azure-mysqlpostgresql-libraries-for-python"></a><span data-ttu-id="f040b-103">Python용 Azure MySQL/PostgreSQL 라이브러리</span><span class="sxs-lookup"><span data-stu-id="f040b-103">Azure MySQL/PostgreSQL libraries for Python</span></span>

## <a name="mysql"></a><span data-ttu-id="f040b-104">MySQL</span><span class="sxs-lookup"><span data-stu-id="f040b-104">MySQL</span></span>

<span data-ttu-id="f040b-105">MySQL 관리자 및 pyodbc를 사용하여 Python에서 [Azure MySQL Database](/azure/mysql/overview)에 저장된 리소스 및 데이터로 작업합니다.</span><span class="sxs-lookup"><span data-stu-id="f040b-105">Work with resources and data stored in [Azure MySQL Database](/azure/mysql/overview) from python with the MySQL manager and pyodbc.</span></span>

### <a name="client-odbc-driver-and-pyodbc"></a><span data-ttu-id="f040b-106">Client ODBC 드라이버 및 pyodbc</span><span class="sxs-lookup"><span data-stu-id="f040b-106">Client ODBC driver and pyodbc</span></span>

<span data-ttu-id="f040b-107">Azure Database for MySQL에 액세스하는 데 권장되는 클라이언트 라이브러리는 Microsoft [ODBC 드라이버](/azure/sql-database/sql-database-connect-query-python#prerequisites)입니다.</span><span class="sxs-lookup"><span data-stu-id="f040b-107">The recommended client library for accessing Azure Database for MySQL is the Microsoft [ODBC driver](/azure/sql-database/sql-database-connect-query-python#prerequisites).</span></span> <span data-ttu-id="f040b-108">ODBC 드라이버를 사용하여 데이터베이스에 연결하고 SQL 문을 직접 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f040b-108">Use the ODBC driver to connect to the database and execute SQL statements directly.</span></span>

#### <a name="example"></a><span data-ttu-id="f040b-109">예</span><span class="sxs-lookup"><span data-stu-id="f040b-109">Example</span></span>

<span data-ttu-id="f040b-110">Azure Database for MySQL에 연결하고 sales 테이블의 모든 레코드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f040b-110">Connect to a Azure Database for MySQL and select all records in the sales table.</span></span> <span data-ttu-id="f040b-111">Azure Portal에서 데이터베이스에 대한 ODBC 연결 문자열을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f040b-111">You can get the ODBC connection string for the database from the Azure Portal.</span></span>

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

### <a name="management-api"></a><span data-ttu-id="f040b-112">관리 API</span><span class="sxs-lookup"><span data-stu-id="f040b-112">Management API</span></span>

<span data-ttu-id="f040b-113">관리 API를 사용하여 구독의 MySQL 리소스를 만들고 관리합니다.</span><span class="sxs-lookup"><span data-stu-id="f040b-113">Create and manage MySQL resources in your subscription with the management API.</span></span>

#### <a name="requirements"></a><span data-ttu-id="f040b-114">요구 사항</span><span class="sxs-lookup"><span data-stu-id="f040b-114">Requirements</span></span>
<span data-ttu-id="f040b-115">Python용 MySQL 관리 라이브러리를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f040b-115">You must install the MySQL management libraries for Python.</span></span>
```bash
pip install azure-mgmt-rdbms
```

<span data-ttu-id="f040b-116">관리 클라이언트에서 인증할 자격 증명을 얻는 방법에 대한 자세한 내용은 [Python SDK 인증](https://docs.microsoft.com/python/azure/python-sdk-azure-authenticate) 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f040b-116">Please see the [Python SDK authentication](https://docs.microsoft.com/python/azure/python-sdk-azure-authenticate) page for details on obtaining credentials to authenticate with the management client.</span></span>

#### <a name="example"></a><span data-ttu-id="f040b-117">예</span><span class="sxs-lookup"><span data-stu-id="f040b-117">Example</span></span>

<span data-ttu-id="f040b-118">MySQL 5.7 Database 리소스를 만들고 방화벽 규칙을 사용하여 IP 주소 범위에 대한 액세스를 제한합니다.</span><span class="sxs-lookup"><span data-stu-id="f040b-118">Create a MySQL 5.7 Database resource and restrict access to a range of IP addresses using a firewall rule.</span></span>

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
> [<span data-ttu-id="f040b-119">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="f040b-119">Explore the Management APIs</span></span>](/python/api/overview/azure/postgresql/mysql/management)

## <a name="postgresql"></a><span data-ttu-id="f040b-120">PostgreSQL</span><span class="sxs-lookup"><span data-stu-id="f040b-120">PostgreSQL</span></span>
<span data-ttu-id="f040b-121">ODBC 드라이버 및 pyodbc를 사용하여 데이터베이스에 연결하고 SQL 문을 직접 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="f040b-121">Use the ODBC driver and pyodbc to connect to the database and execute SQL statements directly.</span></span>

<span data-ttu-id="f040b-122">[Azure Database for PostgreSQL](https://docs.microsoft.com/azure/postgresql/)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="f040b-122">Learn more about [Azure Database for PostgreSQL](https://docs.microsoft.com/azure/postgresql/).</span></span>

### <a name="client-odbc-driver-and-pyodbc"></a><span data-ttu-id="f040b-123">Client ODBC 드라이버 및 pyodbc</span><span class="sxs-lookup"><span data-stu-id="f040b-123">Client ODBC driver and pyodbc</span></span>
<span data-ttu-id="f040b-124">Azure Database for PostgreSQL에 액세스하는 데 권장되는 클라이언트 라이브러리는 Microsoft [ODBC 드라이버 및 pyodbc](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python#prerequisites)입니다.</span><span class="sxs-lookup"><span data-stu-id="f040b-124">The recommended client library for accessing Azure Database for PostgreSQL is the Microsoft [ODBC driver and pyodbc](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python#prerequisites).</span></span>

#### <a name="example"></a><span data-ttu-id="f040b-125">예</span><span class="sxs-lookup"><span data-stu-id="f040b-125">Example</span></span> 

<span data-ttu-id="f040b-126">Azure Database for PostgreSQL에 연결하고 `SALES` 테이블의 모든 레코드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="f040b-126">Connect to a Azure Database for PostgreSQL and select all records in the `SALES` table.</span></span> <span data-ttu-id="f040b-127">Azure Portal에서 데이터베이스에 대한 ODBC 연결 문자열을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="f040b-127">You can get the ODBC connection string for the database from the Azure Portal.</span></span>

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

### <a name="management-api"></a><span data-ttu-id="f040b-128">관리 API</span><span class="sxs-lookup"><span data-stu-id="f040b-128">Management API</span></span>
#### <a name="requirements"></a><span data-ttu-id="f040b-129">요구 사항</span><span class="sxs-lookup"><span data-stu-id="f040b-129">Requirements</span></span>
<span data-ttu-id="f040b-130">Python용 PostgreSQL 관리 라이브러리를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="f040b-130">You must install the PostgreSQL management libraries for Python.</span></span>
```bash
pip install azure-mgmt-rdbms
```

<span data-ttu-id="f040b-131">관리 클라이언트에서 인증할 자격 증명을 얻는 방법에 대한 자세한 내용은 [Python SDK 인증](https://docs.microsoft.com/python/azure/python-sdk-azure-authenticate) 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="f040b-131">Please see the [Python SDK authentication](https://docs.microsoft.com/python/azure/python-sdk-azure-authenticate) page for details on obtaining credentials to authenticate with the management client.</span></span>

#### <a name="example"></a><span data-ttu-id="f040b-132">예</span><span class="sxs-lookup"><span data-stu-id="f040b-132">Example</span></span>
<span data-ttu-id="f040b-133">이 예제에서는 기존 Postgres 서버에 새 Postgres 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="f040b-133">In this example we will create a new Postgres database on our existing Postgres server.</span></span>
```python
from azure.mgmt.rdbms.postgresql import PostgreSQLManagementClient

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
> [<span data-ttu-id="f040b-134">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="f040b-134">Explore the Management APIs</span></span>](/python/api/overview/azure/postgresql/mysql/management)
