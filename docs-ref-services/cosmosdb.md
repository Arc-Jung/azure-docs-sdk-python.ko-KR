---
title: Python용 Azure Cosmos DB 라이브러리
description: Azure Cosmos DB용 Python 클라이언트 라이브러리에 대한 참조 설명서
keywords: Azure, Python, SDK, API, SQL, 데이터베이스, PostGres, Cosmos DB, NoSQL
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 03/20/2018
ms.topic: article
ms.devlang: python
ms.service: cosmosdb
ms.openlocfilehash: c2f3ea017a8864d4d2fb74a439c420f1f0313082
ms.sourcegitcommit: f439ba940d5940359c982015db7ccfb82f9dffd9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/21/2018
ms.locfileid: "52276797"
---
# <a name="azure-cosmos-db-libraries-for-python"></a><span data-ttu-id="3c647-104">Python용 Azure Cosmos DB 라이브러리</span><span class="sxs-lookup"><span data-stu-id="3c647-104">Azure Cosmos DB libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="3c647-105">개요</span><span class="sxs-lookup"><span data-stu-id="3c647-105">Overview</span></span>

<span data-ttu-id="3c647-106">Python 응용 프로그램에서 Azure Cosmos DB를 사용하여 JSON 문서를 NoSQL 데이터 저장소에 저장하고 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="3c647-106">Use Azure Cosmos DB in your Python applications to store and query JSON documents in a NoSQL data store.</span></span>

<span data-ttu-id="3c647-107">[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="3c647-107">Learn more about [Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span></span>

## <a name="client-library"></a><span data-ttu-id="3c647-108">클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="3c647-108">Client library</span></span>
 ```bash
pip install pydocumentdb
 ```

## <a name="management-library"></a><span data-ttu-id="3c647-109">관리 라이브러리</span><span class="sxs-lookup"><span data-stu-id="3c647-109">Management library</span></span>
```bash
pip install azure-mgmt-cosmosdb
```

### <a name="example"></a><span data-ttu-id="3c647-110">예</span><span class="sxs-lookup"><span data-stu-id="3c647-110">Example</span></span>

<span data-ttu-id="3c647-111">SQL 방식 쿼리 인터페이스를 사용하여 Azure Cosmos DB에서 일치하는 문서를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="3c647-111">Find matching documents in Azure CosmosDB using a SQL-like query interface:</span></span>

```python
import pydocumentdb
import pydocumentdb.document_client as document_client

# Initialize the Python Azure Cosmos DB client
client = document_client.DocumentClient(config['ENDPOINT'], {'masterKey': config['MASTERKEY']})
# Create a database
db = client.CreateDatabase({ 'id': config['DOCUMENTDB_DATABASE'] })

# Create collection options
options = {
    'offerEnableRUPerMinuteThroughput': True,
    'offerVersion': "V2",
    'offerThroughput': 400
}

# Create a collection
collection = client.CreateCollection(db['_self'], { 'id': config['DOCUMENTDB_COLLECTION'] }, options)

# Create some documents
document1 = client.CreateDocument(collection['_self'],
    { 
        'id': 'server1',
        'Web Site': 0,
        'Cloud Service': 0,
        'Virtual Machine': 0,
        'name': 'some' 
    })

# Query them in SQL
query = { 'query': 'SELECT * FROM server s' }    

options = {} 
options['enableCrossPartitionQuery'] = True
options['maxItemCount'] = 2

result_iterable = client.QueryDocuments(collection['_self'], query, options)
results = list(result_iterable)

print(results)
```
> [!div class="nextstepaction"]
> [<span data-ttu-id="3c647-112">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="3c647-112">Explore the Management APIs</span></span>](/python/api/overview/azure/cosmosdb/management)

## <a name="samples"></a><span data-ttu-id="3c647-113">샘플</span><span class="sxs-lookup"><span data-stu-id="3c647-113">Samples</span></span>

* [<span data-ttu-id="3c647-114">Azure Cosmos DB SQL API 계정에 저장된 데이터를 액세스하고 관리하기 위한 Python 앱 개발</span><span class="sxs-lookup"><span data-stu-id="3c647-114">Develop a Python app to access and manage data stored in Azure Cosmos DB SQL API account</span></span>](https://github.com/Azure-Samples/azure-cosmos-db-python-getting-started.git)

* [<span data-ttu-id="3c647-115">Azure Cosmos DB MongoDB API 계정에 저장된 데이터를 액세스하고 관리하기 위한 Python 앱 개발</span><span class="sxs-lookup"><span data-stu-id="3c647-115">Develop a Python app to access and manage data stored in Azure Cosmos DB MongoDB API account</span></span>](https://github.com/Azure-Samples/CosmosDB-Flask-Mongo-Sample.git)

* [<span data-ttu-id="3c647-116">Azure Cosmos DB Gremlin API 계정에 저장된 데이터를 액세스하고 관리하기 위한 Python 앱 개발</span><span class="sxs-lookup"><span data-stu-id="3c647-116">Develop a Python app to access and manage data stored in Azure Cosmos DB Gremlin API account</span></span>](https://github.com/Azure-Samples/azure-cosmos-db-graph-python-getting-started.git)

* [<span data-ttu-id="3c647-117">Azure Cosmos DB Cassandra API 계정에 저장된 데이터를 액세스하고 관리하기 위한 Python 앱 개발</span><span class="sxs-lookup"><span data-stu-id="3c647-117">Develop a Python app to access and manage data stored in Azure Cosmos DB Cassandra API account</span></span>](https://github.com/Azure-Samples/azure-cosmos-db-cassandra-python-getting-started.git)

* [<span data-ttu-id="3c647-118">Azure Cosmos DB Table API 계정에 저장된 데이터를 액세스하고 관리하기 위한 Python 앱 개발</span><span class="sxs-lookup"><span data-stu-id="3c647-118">Develop a Python app to access and manage data stored in Azure Cosmos DB Table API account</span></span>](https://github.com/Azure-Samples/storage-python-getting-started.git)


