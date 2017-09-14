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
ms.openlocfilehash: 5382779d659f7c85e5ecbd304920e00b78a08a49
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="azure-cosmosdb-libraries-for-python"></a>Python용 Azure CosmosDB 라이브러리

## <a name="overview"></a>개요

Python 응용 프로그램에서 CosmosDB를 사용하여 JSON 문서를 NoSQL 데이터 저장소에 저장하고 쿼리할 수 있습니다.

[Azure CosmosDB](https://docs.microsoft.com/azure/cosmos-db/introduction)에 대해 자세히 알아보세요.

## <a name="client-library"></a>클라이언트 라이브러리
 ```bash
pip install pydocumentdb
 ```

## <a name="management-library"></a>관리 라이브러리
```bash
pip install azure-mgmt-cosmosdb
```

### <a name="example"></a>예제

SQL 방식 쿼리 인터페이스를 사용하여 CosmosDB에서 일치하는 문서를 찾습니다.

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
> [관리 API 탐색](/python/api/overview/azure/cosmosdb/managementlibrary)

## <a name="samples"></a>샘플

[Azure Cosmos DB의 DocumentDB API를 사용하여 Python 앱 개발(영문)](https://azure.microsoft.com/resources/samples/azure-cosmos-db-documentdb-python-getting-started/)


