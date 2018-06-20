---
title: Python용 Azure PostgreSQL 라이브러리
description: ''
keywords: Azure, Python, SDK, API, SQL, 데이터베이스, Postgres, PostgreSQL
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 07/11/2017
ms.topic: article
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: postgresql
ms.openlocfilehash: cad5995072d5040764986765d9a900f46f5141ec
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/23/2018
ms.locfileid: "29478936"
---
#<a name="azure-postgresql-libraries-for-python"></a><span data-ttu-id="4d6e5-103">Python용 Azure PostgreSQL 라이브러리</span><span class="sxs-lookup"><span data-stu-id="4d6e5-103">Azure PostgreSQL libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="4d6e5-104">개요</span><span class="sxs-lookup"><span data-stu-id="4d6e5-104">Overview</span></span>
<span data-ttu-id="4d6e5-105">ODBC 드라이버 및 pyodbc를 사용하여 데이터베이스에 연결하고 SQL 문을 직접 실행합니다.</span><span class="sxs-lookup"><span data-stu-id="4d6e5-105">Use the ODBC driver and pyodbc to connect to the database and execute SQL statements directly.</span></span>

<span data-ttu-id="4d6e5-106">[Azure Database for PostgreSQL](https://docs.microsoft.com/azure/postgresql/)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="4d6e5-106">Learn more about [Azure Database for PostgreSQL](https://docs.microsoft.com/azure/postgresql/).</span></span>

## <a name="client-odbc-driver-and-pyodbc"></a><span data-ttu-id="4d6e5-107">Client ODBC 드라이버 및 pyodbc</span><span class="sxs-lookup"><span data-stu-id="4d6e5-107">Client ODBC driver and pyodbc</span></span>
<span data-ttu-id="4d6e5-108">Azure Database for PostgreSQL에 액세스하는 데 권장되는 클라이언트 라이브러리는 Microsoft [ODBC 드라이버 및 pyodbc](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries)입니다.</span><span class="sxs-lookup"><span data-stu-id="4d6e5-108">The recommended client library for accessing Azure Database for PostgreSQL is the Microsoft [ODBC driver and pyodbc](https://docs.microsoft.com/azure/sql-database/sql-database-connect-query-python#install-the-python-and-database-communication-libraries)</span></span>

### <a name="example"></a><span data-ttu-id="4d6e5-109">예</span><span class="sxs-lookup"><span data-stu-id="4d6e5-109">Example</span></span> 

<span data-ttu-id="4d6e5-110">Azure Database for PostgreSQL에 연결하고 `SALES` 테이블의 모든 레코드를 선택합니다.</span><span class="sxs-lookup"><span data-stu-id="4d6e5-110">Connect to a Azure Database for PostgreSQL and select all records in the `SALES` table.</span></span> <span data-ttu-id="4d6e5-111">Azure Portal에서 데이터베이스에 대한 ODBC 연결 문자열을 가져올 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="4d6e5-111">You can get the ODBC connection string for the database from the Azure Portal.</span></span>

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

## <a name="management-api"></a><span data-ttu-id="4d6e5-112">관리 API</span><span class="sxs-lookup"><span data-stu-id="4d6e5-112">Management API</span></span>
### <a name="requirements"></a><span data-ttu-id="4d6e5-113">요구 사항</span><span class="sxs-lookup"><span data-stu-id="4d6e5-113">Requirements</span></span>
<span data-ttu-id="4d6e5-114">Python용 PostgreSQL 관리 라이브러리를 설치해야 합니다.</span><span class="sxs-lookup"><span data-stu-id="4d6e5-114">You must install the PostgreSQL management libraries for Python.</span></span>
```bash
pip install azure-mgmt-rdbms
```

<span data-ttu-id="4d6e5-115">관리 클라이언트에서 인증할 자격 증명을 얻는 방법에 대한 자세한 내용은 [Python SDK 인증](https://docs.microsoft.com/python/azure/python-sdk-azure-authenticate) 페이지를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="4d6e5-115">Please see the [Python SDK authentication](https://docs.microsoft.com/python/azure/python-sdk-azure-authenticate) page for details on obtaining credentials to authenticate with the management client.</span></span>

### <a name="example"></a><span data-ttu-id="4d6e5-116">예</span><span class="sxs-lookup"><span data-stu-id="4d6e5-116">Example</span></span>
<span data-ttu-id="4d6e5-117">이 예제에서는 기존 Postgres 서버에 새 Postgres 데이터베이스를 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="4d6e5-117">In this example we will create a new Postgres database on our existing Postgres server.</span></span>
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
> [<span data-ttu-id="4d6e5-118">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="4d6e5-118">Explore the Management APIs</span></span>](/python/api/overview/azure/postgresql/management)

