---
title: Python용 Azure Cosmos DB 라이브러리
description: Azure Cosmos DB용 Python 클라이언트 라이브러리에 대한 참조 설명서
keywords: Azure, Python, SDK, API, SQL, 데이터베이스, PostGres, Cosmos DB, NoSQL
author: lisawong19
ms.author: routlaw
manager: douge
ms.date: 03/20/2018
ms.topic: article
ms.devlang: python
ms.service: cosmosdb
ms.openlocfilehash: bb5e2af6a28d9543cce0c1e80fab1575b78f8cfa
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534311"
---
# <a name="azure-cosmos-db-libraries-for-python"></a>Python용 Azure Cosmos DB 라이브러리

## <a name="overview"></a>개요

Python 애플리케이션에서 Azure Cosmos DB를 사용하여 JSON 문서를 NoSQL 데이터 저장소에 저장하고 쿼리할 수 있습니다.

[Azure Cosmos DB](https://docs.microsoft.com/azure/cosmos-db/introduction)에 대해 자세히 알아보세요.

## <a name="client-library"></a>클라이언트 라이브러리
 ```bash
pip install pydocumentdb
 ```

## <a name="management-library"></a>관리 라이브러리
```bash
pip install azure-mgmt-cosmosdb
```

### <a name="example"></a>예

SQL 방식 쿼리 인터페이스를 사용하여 Azure Cosmos DB에서 일치하는 문서를 찾습니다.

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
> [관리 API 탐색](/python/api/overview/azure/cosmosdb/management)

## <a name="samples"></a>샘플

* [Azure Cosmos DB SQL API 계정에 저장된 데이터를 액세스하고 관리하기 위한 Python 앱 개발](https://github.com/Azure-Samples/azure-cosmos-db-python-getting-started.git)

* [Azure Cosmos DB MongoDB API 계정에 저장된 데이터를 액세스하고 관리하기 위한 Python 앱 개발](https://github.com/Azure-Samples/CosmosDB-Flask-Mongo-Sample.git)

* [Azure Cosmos DB Gremlin API 계정에 저장된 데이터를 액세스하고 관리하기 위한 Python 앱 개발](https://github.com/Azure-Samples/azure-cosmos-db-graph-python-getting-started.git)

* [Azure Cosmos DB Cassandra API 계정에 저장된 데이터를 액세스하고 관리하기 위한 Python 앱 개발](https://github.com/Azure-Samples/azure-cosmos-db-cassandra-python-getting-started.git)

* [Azure Cosmos DB Table API 계정에 저장된 데이터를 액세스하고 관리하기 위한 Python 앱 개발](https://github.com/Azure-Samples/storage-python-getting-started.git)


