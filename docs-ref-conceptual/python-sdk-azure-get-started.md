---
title: "Python용 Azure 라이브러리 시작"
description: "Python용 Azure 라이브러리를 시작합니다."
keywords: Azure, Python, SDK, API
author: lisawong19
ms.author: liwong
manager: douge
ms.date: 06/05/2017
ms.topic: get-started
ms.technology: azure
ms.devlang: python
ms.service: multiple
ms.assetid: 
ms.openlocfilehash: 848ca9dc40000e68e5e3cea3af8b8a0d22747881
ms.sourcegitcommit: 3617d0db0111bbc00072ff8161de2d76606ce0ea
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/18/2017
---
# <a name="get-started-with-the-azure-libraries-for-python"></a>Python용 Azure 라이브러리 시작

이 가이드에서는 몇 가지 Python용 Azure 라이브러리를 사용하는 방법을 보여 줍니다.  인증을 설정하고, Azure Storage 계정을 만들어 사용하고, Azure SQL Database를 만들어 사용하고, 일부 가상 컴퓨터를 배포하고, GitHub에서 Azure App Service Web App을 배포합니다.

## <a name="prerequisites"></a>필수 조건

- Azure 계정. 계정이 없으면 [체험 계정을 얻습니다](https://azure.microsoft.com/free/).
- [Python](https://www.python.org/downloads/)
- [Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart) 또는 [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2)

[!INCLUDE [azure-cloud-shell](../docs-ref-conceptual/includes/cloud-shell-try-it.md)]

## <a name="set-up-authentication"></a>인증 설정
> [!IMPORTANT]
> 이는 빠른 시작 개발자 환경으로 사용되어야 합니다. 프로덕션 용도로는 [ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-python) 또는 사용자 고유의 자격 증명 시스템을 사용하세요.
> CLI 구성을 변경하면 SDK 실행에 영향을 줍니다.

SDK는 CLI 활성 구독을 사용하여 클라이언트를 만들 수 있습니다.

활성 자격 증명을 정의하려면 [az login](https://docs.microsoft.com/cli/azure/authenticate-azure-cli)을 사용합니다.
기본 구독 ID는 보유하고 있는 유일한 ID이거나 [az account](https://docs.microsoft.com/cli/azure/manage-azure-subscriptions-azure-cli)를 사용하여 정의할 수 있습니다.

```python
from azure.common.client_factory import get_client_from_cli_profile
from azure.mgmt.compute import ComputeManagementClient

client = get_client_from_cli_profile(ComputeManagementClient)
```
## <a name="create-a-virtual-environment"></a>가상 환경 만들기

> [!IMPORTANT]
> 이 작업은 선택적이지만 수행하는 것이 매우 좋습니다.

Bash에서 가상 환경 만들기(Linux 또는 [Windows용 Bash](https://msdn.microsoft.com/commandline/wsl/about)):
```bash
pip install virtualenv
virtualenv mytestenv
cd mytestenv
source ./bin/activate
```

Powershell에서 가상 환경 만들기:
```powershell
pip install virtualenv
virtualenv mytestenv
cd mytestenv
.\Scripts\activate
```

> [!IMPORTANT]
> [VSCode](https://code.visualstudio.com/) 및 [Python 확장](https://marketplace.visualstudio.com/items?itemName=donjayamanne.python)을 사용하는 경우 `code .`를 사용하여 시작하고 환경을 구성할 수 있습니다.

## <a name="create-a-linux-virtual-machine"></a>Linux 가상 컴퓨터 만들기
이 코드에서는 미국 동부 Azure 지역에서 실행되는 `sampleVmResourceGroup` 리소스 그룹에 `testLinuxVM`이라는 새 Linux VM을 만듭니다.

인증:
```azcli
az login
```
리소스 그룹 만들기:
```azurecli-interactive
az group create -l eastus --n sampleVmResourceGroup
```

가상 네트워크 및 서브넷 만들기:
```azurecli-interactive
az network vnet create -g sampleVmResourceGroup -n azure-sample-vnet --address-prefix 10.0.0.0/16 --subnet-name azure-sample-subnet --subnet-prefix 10.0.0.0/24
```

공용 IP 주소 만들기:
```azurecli-interactive
az network public-ip create -g sampleVmResourceGroup -n azure-sample-ip --allocation-method Dynamic --version IPv6
```
네트워크 인터페이스 클라이언트 만들기:
```azurecli-interactive
az network nic create -g sampleVmResourceGroup --vnet-name azure-sample-vnet --subnet azure-sample-subnet -n azure-sample-nic --public-ip-address azure-sample-ip
```

```python
from azure.mgmt.network import NetworkManagementClient
from azure.mgmt.compute import ComputeManagementClient
from azure.common.client_factory import get_client_from_cli_profile

# Azure Datacenter
LOCATION = 'eastus'

# Resource Group
GROUP_NAME = 'sampleVmResourceGroup'

# Network
VNET_NAME = 'azure-sample-vnet'
SUBNET_NAME = 'azure-sample-subnet'

# VM
NIC_NAME = 'azure-sample-nic'
VM_NAME = 'testLinuxVM'

USERNAME = 'userlogin'
PASSWORD = 'Pa$$w0rd91'

IP_ADDRESS_NAME='azure-sample-ip'

VM_REFERENCE = {
    'linux': {
        'publisher': 'Canonical',
        'offer': 'UbuntuServer',
        'sku': '16.04.0-LTS',
        'version': 'latest'
    },
    'windows': {
        'publisher': 'MicrosoftWindowsServerEssentials',
        'offer': 'WindowsServerEssentials',
        'sku': 'WindowsServerEssentials',
        'version': 'latest'
    }
}


def run_example():

    compute_client = get_client_from_cli_profile(ComputeManagementClient)
    network_client = get_client_from_cli_profile(NetworkManagementClient)

    # get nic id
    nic = network_client.network_interfaces.get(GROUP_NAME, NIC_NAME)

    # Create Linux VM
    print('\nCreating Linux Virtual Machine')
    vm_parameters = create_vm_parameters(nic.id, VM_REFERENCE['linux'])
    print(vm_parameters)
    async_vm_creation = compute_client.virtual_machines.create_or_update(
        GROUP_NAME, VM_NAME, vm_parameters)
    async_vm_creation.wait()


def create_vm_parameters(nic_id, vm_reference):
    """Create the VM parameters structure.
    """
    return {
        'location': LOCATION,
        'os_profile': {
            'computer_name': VM_NAME,
            'admin_username': USERNAME,
            'admin_password': PASSWORD
        },
        'hardware_profile': {
            'vm_size': 'Standard_DS1_v2'
        },
        'storage_profile': {
            'image_reference': {
                'publisher': vm_reference['publisher'],
                'offer': vm_reference['offer'],
                'sku': vm_reference['sku'],
                'version': vm_reference['version']
            },
        },
        'network_profile': {
            'network_interfaces': [{
                'id': nic_id,
            }]
        },
    }


if __name__ == "__main__":
    run_example()
```

프로그램이 완료되면 Azure CLI 2.0을 사용하여 구독의 가상 컴퓨터를 확인합니다.

```azurecli-interactive
az vm list --resource-group sampleVmResourceGroup
```

코드가 작동하는지 확인했으면 CLI를 사용하여 VM과 해당 리소스를 삭제합니다.

```azurecli-interactive
az group delete --name sampleVmResourceGroup
```

## <a name="deploy-a-web-app-from-a-github-repo"></a>GitHub 리포지토리에서 웹앱 배포
이 코드에서는 GitHub 리포지토리의 `master` 분기에 있는 Flask 웹 응용 프로그램을 체험 계층에서 실행되는 새 [Azure App Service 웹앱](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview)으로 배포합니다. 

시작 이전: https://github.com/Azure-Samples/python-docs-hello-world를 포크합니다.

인증:
```azcli
az login
```
리소스 그룹 만들기:
```azurecli-interactive
az group create -l eastus -n sampleWebResourceGroup
```

앱 서비스 체험 계획 만들기:
```azurecli-interactive
az appservice plan create -g sampleWebResourceGroup -n sampleFreePlan  --sku Free
```

```python
from azure.mgmt.web import WebSiteManagementClient
from azure.mgmt.web.models import Site, SiteSourceControl, SiteConfig
from azure.common.client_factory import get_client_from_cli_profile

RESOURCE_GROUP_NAME = 'sampleWebResourceGroup'
SERVICE_PLAN_NAME = 'sampleFreePlanName'
WEB_APP_NAME = 'sampleflaskapp123'
REPO_URL = 'GitHub_Repository_URL'

#log in
web_client = get_client_from_cli_profile(WebSiteManagementClient)

# get service plan id
service_plan = web_client.app_service_plans.get(RESOURCE_GROUP_NAME, SERVICE_PLAN_NAME)

# create a web app
siteConfiguration = SiteConfig(
    python_version='3.4',
)
site_async_operation = web_client.web_apps.create_or_update(
    RESOURCE_GROUP_NAME,
    WEB_APP_NAME,
    Site(
        location='eastus',
        server_farm_id=service_plan.id,
        site_config=siteConfiguration
    ),
)

site = site_async_operation.result()
print('created webapp: ' + site.default_host_name)

# continuous deployment with GitHub
source_control_async_operation = web_client.web_apps.create_or_update_source_control(
    RESOURCE_GROUP_NAME,
    WEB_APP_NAME,
    SiteSourceControl(
        location='GitHub',
        repo_url= REPO_URL,
        branch='master'
    )
)

source_control = source_control_async_operation.result()
print("added source control to: " + source_control.name + "azurewebsites.net")
```

CLI를 사용하여 응용 프로그램을 가리키는 브라우저를 엽니다.
```azurecli-interactive
az appservice web browse --resource-group sampleWebResourceGroup --name YOUR_APP_NAME
```

배포를 확인한 후 구독에서 웹앱을 제거하고 계획합니다. 
```azurecli-interactive
az group delete --name sampleWebResourceGroup
```


## <a name="connect-to-a-sql-database"></a>SQL 데이터베이스에 연결
이 코드에서는 원격 액세스를 허용하는 방화벽 규칙이 있는 새 SQL 데이터베이스를 만든 다음 Microsoft ODBC 드라이버를 사용하여 연결합니다. Pyodbc는 Linux의 Microsoft ODBC 드라이버를 사용하여 SQL Database에 연결합니다. 

인증:
```azcli
az login
```
리소스 그룹 만들기:
```azurecli-interactive
az group create -l eastus -n azure-sample-group
```

SQL 서버 만들기:
```azurecli-interactive
az sql server create --admin-password HusH_Sec4et --admin-user mysecretname -l eastus -n samplesqlserver123 -g azure-sample-group
```

방화벽 규칙 추가:
```azurecli-interactive
az sql server firewall-rule create --end-ip-address 167.220.0.235 --name firewall_rule_name_123.123.123.123 --resource-group azure-sample-group --server samplesqlserver123 --start-ip-address 123.123.123.123
```

SQL 데이터베이스 만들기:
```azurecli-interactive
az sql db create --name sample-db --resource-group azure-sample-group --server samplesqlserver123
```


```python
from azure.mgmt.sql import SqlManagementClient
from azure.common.client_factory import get_client_from_cli_profile
import pyodbc

LOCATION = 'eastus'
GROUP_NAME = 'azure-sample-group'
SERVER_NAME = 'samplesqlserver123'
DATABASE_NAME = 'sample-db'
USER_NAME ='mysecretname'
PASSWORD='HusH_Sec4et'

# authenticate
sql_client = get_client_from_cli_profile(SqlManagementClient)


def run_example():
    # Get SQL database
    print('Get SQL database')
    database = sql_client.databases.get(
        GROUP_NAME,
        SERVER_NAME,
        DATABASE_NAME
    )
    print(database)
    print("\n\n")


def create_and_insert():
    server = SERVER_NAME+'.database.windows.net'
    database = DATABASE_NAME
    username = USER_NAME
    password = PASSWORD
    driver = '{ODBC Driver 13 for SQL Server}'
    cnxn = pyodbc.connect(
        'DRIVER=' + driver + ';PORT=1433;SERVER=' + server + ';PORT=1443;DATABASE=' + database + ';UID=' + username + ';PWD=' + password)
    cursor = cnxn.cursor()
    tsql = "CREATE TABLE CLOUD (name varchar(255), code int);"
    tsqlInsert = "INSERT INTO CLOUD (name, code) VALUES ('Azure', 1); "
    selectValues = "SELECT * FROM CLOUD"
    with cursor.execute(tsql):
        print('Successfully created table!')
    with cursor.execute(tsqlInsert):
        print('Successfully inserted data into table')
    cursor.execute(selectValues)
    row = cursor.fetchone()
    while row:
        print(str(row[0]) + " " + str(row[1]))
        row = cursor.fetchone()
    cnxn.commit()

if __name__ == "__main__":
    run_example()
    create_and_insert()
```

코드가 작동하는지 확인한 후 CLI를 사용하여 SQL 데이터베이스 및 해당 리소스를 삭제합니다.

```azurecli-interactive
az group delete --name azure-sample-group
```

## <a name="write-a-blob-into-a-new-storage-account"></a>새 저장소 계정에 Blob 쓰기

인증:
```azcli
az login
```
리소스 그룹 만들기:
```azurecli-interactive
az group create -l eastus -n sampleStorageResourceGroup
```

저장소 계정 만들기:
```azurecli-interactive
az storage account create -n samplestorageaccountname -g sampleStorageResourceGroup -l eastus --sku Standard_RAGRS
```

이 코드에서는 [Azure 저장소 계정](https://docs.microsoft.com/azure/storage/storage-introduction)을 만든 다음 Python용 Azure Storage 라이브러리를 사용하여 클라우드에 새 html 파일을 만듭니다. 
```python
from azure.storage import CloudStorageAccount
from azure.storage.blob import PublicAccess
from azure.storage.blob.models import ContentSettings
from azure.common.client_factory import get_client_from_cli_profile
from azure.mgmt.storage import StorageManagementClient

RESOURCE_GROUP = 'sampleStorageResourceGroup'
STORAGE_ACCOUNT_NAME = 'samplestorageaccountname'
CONTAINER_NAME = 'samplecontainername'

# log in
storage_client = get_client_from_cli_profile(StorageManagementClient)

# create a public storage container to hold the file
storage_keys = storage_client.storage_accounts.list_keys(RESOURCE_GROUP, STORAGE_ACCOUNT_NAME)
storage_keys = {v.key_name: v.value for v in storage_keys.keys}

storage_client = CloudStorageAccount(STORAGE_ACCOUNT_NAME, storage_keys['key1'])
blob_service = storage_client.create_block_blob_service()

blob_service.create_container(CONTAINER_NAME, public_access=PublicAccess.Container)

blob_service.create_blob_from_bytes(
    CONTAINER_NAME,
    'helloworld.html',
    b'<center><h1>Hello World!</h1></center>',
    content_settings=ContentSettings('text/html')
)

print(blob_service.make_blob_url(CONTAINER_NAME, 'helloworld.html'))
```
성공적으로 업로드된 콘텐츠를 확인하려면 인쇄된 URL로 이동합니다. 

CLI를 사용하여 저장소 계정을 정리합니다.
```azurecli-interactive
az group delete --name sampleStorageResourceGroup
```

## <a name="explore-more-samples"></a>더 많은 샘플 탐색

Python용 Azure 관리 라이브러리를 사용하여 리소스를 관리하고 작업을 자동화하는 방법에 대한 자세한 내용은 [가상 컴퓨터](python-sdk-azure-web-apps-samples.md), [웹앱](python-sdk-azure-web-apps-samples.md) 및 [SQL 데이터베이스](python-sdk-azure-sql-database-samples.md)에 대한 샘플 코드를 참조하세요.


## <a name="reference"></a>참조

[참조](/python/api/overview/azure/?view=azure-python)는 모든 패키지에서 사용할 수 있습니다.
