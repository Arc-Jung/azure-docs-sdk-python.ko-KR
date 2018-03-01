---
title: "Python용 Azure CosmosDB 라이브러리"
description: "Python용 CosmosDB 라이브러리에 대한 참조 설명서"
keywords: "Azure, Python, SDK, API, SQL, 데이터베이스, PostGres, CosmosDB, NoSQL"
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 08/11/2017
ms.topic: article
ms.devlang: python
ms.service: cosmosdb
ms.openlocfilehash: d56dd69f4fc4513034046f9f721608ad94ff5cfe
ms.sourcegitcommit: 41e90fe75de03d397079a276cdb388305290e27e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/23/2018
---
# <a name="azure-cosmosdb-libraries-for-python"></a><span data-ttu-id="99cb5-104">Python용 Azure CosmosDB 라이브러리</span><span class="sxs-lookup"><span data-stu-id="99cb5-104">Azure CosmosDB libraries for Python</span></span>

## <a name="overview"></a><span data-ttu-id="99cb5-105">개요</span><span class="sxs-lookup"><span data-stu-id="99cb5-105">Overview</span></span>

<span data-ttu-id="99cb5-106">Python 응용 프로그램에서 CosmosDB를 사용하여 JSON 문서를 NoSQL 데이터 저장소에 저장하고 쿼리할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="99cb5-106">Use CosmosDB in your Python applications to store and query JSON documents in a NoSQL data store.</span></span>

<span data-ttu-id="99cb5-107">[Azure CosmosDB](https://docs.microsoft.com/azure/cosmos-db/introduction)에 대해 자세히 알아보세요.</span><span class="sxs-lookup"><span data-stu-id="99cb5-107">Learn more about [Azure CosmosDB](https://docs.microsoft.com/azure/cosmos-db/introduction).</span></span>

## <a name="client-library"></a><span data-ttu-id="99cb5-108">클라이언트 라이브러리</span><span class="sxs-lookup"><span data-stu-id="99cb5-108">Client library</span></span>
 ```bash
pip install pydocumentdb
 ```

## <a name="management-library"></a><span data-ttu-id="99cb5-109">관리 라이브러리</span><span class="sxs-lookup"><span data-stu-id="99cb5-109">Management library</span></span>
```bash
pip install azure-mgmt-cosmosdb
```

### <a name="example"></a><span data-ttu-id="99cb5-110">예</span><span class="sxs-lookup"><span data-stu-id="99cb5-110">Example</span></span>

<span data-ttu-id="99cb5-111">SQL 방식 쿼리 인터페이스를 사용하여 CosmosDB에서 일치하는 문서를 찾습니다.</span><span class="sxs-lookup"><span data-stu-id="99cb5-111">Find matching documents in CosmosDB using a SQL-like query interface:</span></span>

```python
import pydocumentdb
import pydocumentdb.document_client as document_client

# Initialize the Python DocumentDB client
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
> [<span data-ttu-id="99cb5-112">관리 API 탐색</span><span class="sxs-lookup"><span data-stu-id="99cb5-112">Explore the Management APIs</span></span>](/python/api/overview/azure/cosmosdb/management)

## <a name="samples"></a><span data-ttu-id="99cb5-113">샘플</span><span class="sxs-lookup"><span data-stu-id="99cb5-113">Samples</span></span>

[<span data-ttu-id="99cb5-114">Azure Cosmos DB의 DocumentDB API를 사용하여 Python 앱 개발(영문)</span><span class="sxs-lookup"><span data-stu-id="99cb5-114">Develop a Python app using Azure Cosmos DB's DocumentDB API</span></span>](https://azure.microsoft.com/resources/samples/azure-cosmos-db-documentdb-python-getting-started/)


