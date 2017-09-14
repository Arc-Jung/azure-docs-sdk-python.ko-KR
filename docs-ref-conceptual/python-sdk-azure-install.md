---
title: "설치"
description: "Azure Python SDK를 설치하는 방법을 설명합니다."
keywords: Azure, Python, SDK, API
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/05/2017
ms.topic: install
ms.prod: azure
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.assetid: 
ms.openlocfilehash: d65f07a30b3aa8b0a1a502baa86986ad50848873
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="installation"></a>설치

## <a name="installation-with-pip"></a>pip를 사용하여 설치

Azure 서비스의 각 라이브러리를 개별적으로 설치할 수 있습니다.

```bash
pip install azure-batch          # Install the latest Batch runtime library
pip install azure-mgmt-scheduler # Install the latest Storage management library
```

미리 보기 패키지는 `--pre` 플래그를 사용하여 설치할 수 있습니다.

```bash
pip install --pre azure-mgmt-compute # will install only the latest Compute Management library
```

`azure` 메타패키지를 사용하여 한 줄로 Azure 라이브러리의 집합도 설치할 수 있습니다.

```bash
pip install azure
```

이 패키지의 미리 보기 버전을 게시하며, --pre 플래그를 사용하여 액세스할 수 있습니다.

```bash
pip install --pre azure
```

## <a name="install-from-github"></a>GitHub에서 설치

원본에서 `azure`를 설치하려면 다음과 같습니다.

    git clone git://github.com/Azure/azure-sdk-for-python.git
    cd azure-sdk-for-python
    python setup.py install

## <a name="stable-packages"></a>안정적인 패키지
| 패키지 이름 |
|--------------|
|[azure-batch](https://pypi.org/project/azure-batch/)  |   
|[azure-mgmt-batch](https://pypi.org/project/azure-mgmt-batch/)|
|[azure-mgmt-cognitiveservices](https://pypi.org/project/azure-mgmt-cognitiveservices/)|    
|[azure-mgmt-devtestlabs](https://pypi.org/project/azure-mgmt-devtestlabs/)|    
|[azure-mgmt-dns](https://pypi.org/project/azure-mgmt-dns/) |
|[azure-mgmt-logic](https://pypi.org/project/azure-mgmt-logic/)|
|[azure-mgmt-redis](https://pypi.org/project/azure-mgmt-redis/)|
|[azure-mgmt-scheduler](https://pypi.org/project/azure-mgmt-scheduler/)|    
|[azure-mgmt-servermanager](https://pypi.org/project/azure-mgmt-servermanager/)|    
|[azure-servicebus](https://pypi.org/project/azure-mgmt-servicebus/)|   
|[azure-servicefabric](https://pypi.org/project/azure-servicefabric/)|  
|[azure-servicemanagement-legacy](https://pypi.org/project/azure-servicemanagement-legacy/)|    
|[azure-storage](https://pypi.org/project/azure-storage/)|  

## <a name="preview-packages"></a>미리 보기 패키지
| 패키지 이름 | 
|--------------|
|[azure-keyvault](https://pypi.org/project/azure-keyvault/)|    
|[azure-monitor](https://pypi.org/project/azure-monitor)|   
|[azure-mgmt-resource](https://pypi.org/project/azure-mgmt-resource)|   
|[azure-mgmt-compute](https://pypi.org/project/azure-mgmt-compute)| 
|[azure-mgmt-network](https://pypi.org/project/azure-mgmt-network)| 
|[azure-mgmt-storage](https://pypi.org/project/azure-mgmt-storage)| 
|[azure-mgmt-keyvault](https://pypi.org/project/azure-mgmt-keyvault)|   
|[azure-graphrbac](https://pypi.org/project/azure-graphrbac)|   
|[azure-mgmt-authorization](https://pypi.org/project/azure-mgmt-authorization)| 
|[azure-mgmt-billing](https://pypi.org/project/azure-mgmt-billing)| 
|[azure-mgmt-cdn](https://pypi.org/project/azure-mgmt-cdn)| 
|[azure-mgmt-containerregistry](https://pypi.org/project/azure-mgmt-containerregistry)| 
|[azure-mgmt-commerce](https://pypi.org/project/azure-mgmt-commerce)|   
|[azure-mgmt-consumption](https://pypi.org/project/azure-mgmt-consumption)| 
|[azure-mgmt-datalake-analytics](https://pypi.org/project/azure-mgmt-datalake-analytics)|   
|[azure-mgmt-datalake-store](https://pypi.org/project/azure-mgmt-datalake-store)|   
|[azure-mgmt-documentdb](https://pypi.org/project/azure-mgmt-documentdb)|   
|[azure-mgmt-eventhub](https://pypi.org/project/azure-mgmt-eventhub)|   
|[azure-mgmt-iothub](https://pypi.org/project/azure-mgmt-iothub)|
|[azure-mgmt-media](https://pypi.org/project/azure-mgmt-media)| 
|[azure-mgmt-monitor](https://pypi.org/project/azure-mgmt-monitor)| 
|[azure-mgmt-notificationhubs](https://pypi.org/project/azure-mgmt-notificationhubs)|   
|[azure-mgmt-powerbiembedded](https://pypi.org/project/azure-mgmt-powerbiembedded)| 
|[azure-mgmt-search](https://pypi.org/project/azure-mgmt-search)|
|[azure-mgmt-servicebus](https://pypi.org/project/azure-mgmt-servicebus)|   
|[azure-mgmt-sql](https://pypi.org/project/azure-mgmt-sql)| 
|[azure-mgmt-trafficmanager](https://pypi.org/project/azure-mgmt-trafficmanager)|   
|[azure-mgmt-web](https://pypi.org/project/azure-mgmt-web)|