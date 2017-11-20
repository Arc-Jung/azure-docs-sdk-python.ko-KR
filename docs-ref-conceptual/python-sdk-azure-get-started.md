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
# <a name="get-started-with-the-azure-libraries-for-python"></a><span data-ttu-id="fbc55-104">Python용 Azure 라이브러리 시작</span><span class="sxs-lookup"><span data-stu-id="fbc55-104">Get started with the Azure libraries for Python</span></span>

<span data-ttu-id="fbc55-105">이 가이드에서는 몇 가지 Python용 Azure 라이브러리를 사용하는 방법을 보여 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fbc55-105">This guide demonstrates the usage of several Azure libraries for Python.</span></span>  <span data-ttu-id="fbc55-106">인증을 설정하고, Azure Storage 계정을 만들어 사용하고, Azure SQL Database를 만들어 사용하고, 일부 가상 컴퓨터를 배포하고, GitHub에서 Azure App Service Web App을 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc55-106">You will set up authentication, create and use an Azure Storage account, create and use an Azure SQL Database, deploy some virtual machines, and deploy an Azure App Service Web App from GitHub.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fbc55-107">필수 조건</span><span class="sxs-lookup"><span data-stu-id="fbc55-107">Prerequisites</span></span>

- <span data-ttu-id="fbc55-108">Azure 계정.</span><span class="sxs-lookup"><span data-stu-id="fbc55-108">An Azure account.</span></span> <span data-ttu-id="fbc55-109">계정이 없으면 [체험 계정을 얻습니다](https://azure.microsoft.com/free/).</span><span class="sxs-lookup"><span data-stu-id="fbc55-109">If you don't have one, [get a free trial](https://azure.microsoft.com/free/).</span></span>
- [<span data-ttu-id="fbc55-110">Python</span><span class="sxs-lookup"><span data-stu-id="fbc55-110">Python</span></span>](https://www.python.org/downloads/)
- <span data-ttu-id="fbc55-111">[Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart) 또는 [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2)</span><span class="sxs-lookup"><span data-stu-id="fbc55-111">[Azure Cloud Shell](https://docs.microsoft.com/azure/cloud-shell/quickstart) or [Azure CLI 2.0](https://docs.microsoft.com/cli/azure/install-az-cli2).</span></span>

[!INCLUDE [azure-cloud-shell](../docs-ref-conceptual/includes/cloud-shell-try-it.md)]

## <a name="set-up-authentication"></a><span data-ttu-id="fbc55-112">인증 설정</span><span class="sxs-lookup"><span data-stu-id="fbc55-112">Set up authentication</span></span>
> [!IMPORTANT]
> <span data-ttu-id="fbc55-113">이는 빠른 시작 개발자 환경으로 사용되어야 합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc55-113">This should be used as quick start developer experience.</span></span> <span data-ttu-id="fbc55-114">프로덕션 용도로는 [ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-python) 또는 사용자 고유의 자격 증명 시스템을 사용하세요.</span><span class="sxs-lookup"><span data-stu-id="fbc55-114">For production purposes, use [ADAL](https://github.com/AzureAD/azure-activedirectory-library-for-python) or your own credentials system.</span></span>
> <span data-ttu-id="fbc55-115">CLI 구성을 변경하면 SDK 실행에 영향을 줍니다.</span><span class="sxs-lookup"><span data-stu-id="fbc55-115">Any change to your CLI configuration will impact the SDK execution.</span></span>

<span data-ttu-id="fbc55-116">SDK는 CLI 활성 구독을 사용하여 클라이언트를 만들 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbc55-116">The SDK is able to create a client using your CLI active subscription.</span></span>

<span data-ttu-id="fbc55-117">활성 자격 증명을 정의하려면 [az login](https://docs.microsoft.com/cli/azure/authenticate-azure-cli)을 사용합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc55-117">To define active credentials, use [az login](https://docs.microsoft.com/cli/azure/authenticate-azure-cli).</span></span>
<span data-ttu-id="fbc55-118">기본 구독 ID는 보유하고 있는 유일한 ID이거나 [az account](https://docs.microsoft.com/cli/azure/manage-azure-subscriptions-azure-cli)를 사용하여 정의할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbc55-118">Default subscription ID is either the only one you have, or you can define it using [az account](https://docs.microsoft.com/cli/azure/manage-azure-subscriptions-azure-cli).</span></span>

```python
from azure.common.client_factory import get_client_from_cli_profile
from azure.mgmt.compute import ComputeManagementClient

client = get_client_from_cli_profile(ComputeManagementClient)
```
## <a name="create-a-virtual-environment"></a><span data-ttu-id="fbc55-119">가상 환경 만들기</span><span class="sxs-lookup"><span data-stu-id="fbc55-119">Create a virtual environment</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fbc55-120">이 작업은 선택적이지만 수행하는 것이 매우 좋습니다.</span><span class="sxs-lookup"><span data-stu-id="fbc55-120">Create a virtual environment is optional, but we strongly suggest you to do it.</span></span>

<span data-ttu-id="fbc55-121">Bash에서 가상 환경 만들기(Linux 또는 [Windows용 Bash](https://msdn.microsoft.com/commandline/wsl/about)):</span><span class="sxs-lookup"><span data-stu-id="fbc55-121">Create a virtual environment in Bash (Linux or [Bash for Windows](https://msdn.microsoft.com/commandline/wsl/about)):</span></span>
```bash
pip install virtualenv
virtualenv mytestenv
cd mytestenv
source ./bin/activate
```

<span data-ttu-id="fbc55-122">Powershell에서 가상 환경 만들기:</span><span class="sxs-lookup"><span data-stu-id="fbc55-122">Create a virtual environment in Powershell:</span></span>
```powershell
pip install virtualenv
virtualenv mytestenv
cd mytestenv
.\Scripts\activate
```

> [!IMPORTANT]
> <span data-ttu-id="fbc55-123">[VSCode](https://code.visualstudio.com/) 및 [Python 확장](https://marketplace.visualstudio.com/items?itemName=donjayamanne.python)을 사용하는 경우 `code .`를 사용하여 시작하고 환경을 구성할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbc55-123">Note that if you use [VSCode](https://code.visualstudio.com/) and the [Python extension](https://marketplace.visualstudio.com/items?itemName=donjayamanne.python),  you can start it using `code .` and get your environment configured.</span></span>

## <a name="create-a-linux-virtual-machine"></a><span data-ttu-id="fbc55-124">Linux 가상 컴퓨터 만들기</span><span class="sxs-lookup"><span data-stu-id="fbc55-124">Create a Linux virtual machine</span></span>
<span data-ttu-id="fbc55-125">이 코드에서는 미국 동부 Azure 지역에서 실행되는 `sampleVmResourceGroup` 리소스 그룹에 `testLinuxVM`이라는 새 Linux VM을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fbc55-125">This code creates a new Linux VM with name `testLinuxVM` in a resource group `sampleVmResourceGroup` running in the US East Azure region.</span></span>

<span data-ttu-id="fbc55-126">인증:</span><span class="sxs-lookup"><span data-stu-id="fbc55-126">Authenticate:</span></span>
```azcli
az login
```
<span data-ttu-id="fbc55-127">리소스 그룹 만들기:</span><span class="sxs-lookup"><span data-stu-id="fbc55-127">Create a resource group:</span></span>
```azurecli-interactive
az group create -l eastus --n sampleVmResourceGroup
```

<span data-ttu-id="fbc55-128">가상 네트워크 및 서브넷 만들기:</span><span class="sxs-lookup"><span data-stu-id="fbc55-128">Create a virtual network and subnet:</span></span>
```azurecli-interactive
az network vnet create -g sampleVmResourceGroup -n azure-sample-vnet --address-prefix 10.0.0.0/16 --subnet-name azure-sample-subnet --subnet-prefix 10.0.0.0/24
```

<span data-ttu-id="fbc55-129">공용 IP 주소 만들기:</span><span class="sxs-lookup"><span data-stu-id="fbc55-129">Create a public IP address:</span></span>
```azurecli-interactive
az network public-ip create -g sampleVmResourceGroup -n azure-sample-ip --allocation-method Dynamic --version IPv6
```
<span data-ttu-id="fbc55-130">네트워크 인터페이스 클라이언트 만들기:</span><span class="sxs-lookup"><span data-stu-id="fbc55-130">Create a network interface client:</span></span>
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

<span data-ttu-id="fbc55-131">프로그램이 완료되면 Azure CLI 2.0을 사용하여 구독의 가상 컴퓨터를 확인합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc55-131">When the program finishes, verify the virtual machine in your subscription with the Azure CLI 2.0:</span></span>

```azurecli-interactive
az vm list --resource-group sampleVmResourceGroup
```

<span data-ttu-id="fbc55-132">코드가 작동하는지 확인했으면 CLI를 사용하여 VM과 해당 리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc55-132">Once you've verified that the code worked, use the CLI to delete the VM and its resources.</span></span>

```azurecli-interactive
az group delete --name sampleVmResourceGroup
```

## <a name="deploy-a-web-app-from-a-github-repo"></a><span data-ttu-id="fbc55-133">GitHub 리포지토리에서 웹앱 배포</span><span class="sxs-lookup"><span data-stu-id="fbc55-133">Deploy a web app from a GitHub repo</span></span>
<span data-ttu-id="fbc55-134">이 코드에서는 GitHub 리포지토리의 `master` 분기에 있는 Flask 웹 응용 프로그램을 체험 계층에서 실행되는 새 [Azure App Service 웹앱](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview)으로 배포합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc55-134">This code deploys a Flask web application from the `master` branch in a GitHub repo in to a new [Azure App Service Web App](https://docs.microsoft.com/azure/app-service-web/app-service-web-overview) running in the free tier.</span></span> 

<span data-ttu-id="fbc55-135">시작 이전: https://github.com/Azure-Samples/python-docs-hello-world를 포크합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc55-135">Before you begin: Fork https://github.com/Azure-Samples/python-docs-hello-world</span></span>

<span data-ttu-id="fbc55-136">인증:</span><span class="sxs-lookup"><span data-stu-id="fbc55-136">Authenticate:</span></span>
```azcli
az login
```
<span data-ttu-id="fbc55-137">리소스 그룹 만들기:</span><span class="sxs-lookup"><span data-stu-id="fbc55-137">Create a resource group:</span></span>
```azurecli-interactive
az group create -l eastus -n sampleWebResourceGroup
```

<span data-ttu-id="fbc55-138">앱 서비스 체험 계획 만들기:</span><span class="sxs-lookup"><span data-stu-id="fbc55-138">Create a free app service plan:</span></span>
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

<span data-ttu-id="fbc55-139">CLI를 사용하여 응용 프로그램을 가리키는 브라우저를 엽니다.</span><span class="sxs-lookup"><span data-stu-id="fbc55-139">Open a browser pointed to the application using the CLI:</span></span>
```azurecli-interactive
az appservice web browse --resource-group sampleWebResourceGroup --name YOUR_APP_NAME
```

<span data-ttu-id="fbc55-140">배포를 확인한 후 구독에서 웹앱을 제거하고 계획합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc55-140">Remove the web app and plan from your subscription once you've verified the deployment.</span></span> 
```azurecli-interactive
az group delete --name sampleWebResourceGroup
```


## <a name="connect-to-a-sql-database"></a><span data-ttu-id="fbc55-141">SQL 데이터베이스에 연결</span><span class="sxs-lookup"><span data-stu-id="fbc55-141">Connect to a SQL database</span></span>
<span data-ttu-id="fbc55-142">이 코드에서는 원격 액세스를 허용하는 방화벽 규칙이 있는 새 SQL 데이터베이스를 만든 다음 Microsoft ODBC 드라이버를 사용하여 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc55-142">This code creates a new SQL database with a firewall rule allowing remote access, and then connected to it using the Microsoft ODBC driver.</span></span> <span data-ttu-id="fbc55-143">Pyodbc는 Linux의 Microsoft ODBC 드라이버를 사용하여 SQL Database에 연결합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc55-143">Pyodbc uses the Microsoft ODBC Driver on Linux to connect to SQL Databases.</span></span> 

<span data-ttu-id="fbc55-144">인증:</span><span class="sxs-lookup"><span data-stu-id="fbc55-144">Authenticate:</span></span>
```azcli
az login
```
<span data-ttu-id="fbc55-145">리소스 그룹 만들기:</span><span class="sxs-lookup"><span data-stu-id="fbc55-145">Create a resource group:</span></span>
```azurecli-interactive
az group create -l eastus -n azure-sample-group
```

<span data-ttu-id="fbc55-146">SQL 서버 만들기:</span><span class="sxs-lookup"><span data-stu-id="fbc55-146">Create a SQL server:</span></span>
```azurecli-interactive
az sql server create --admin-password HusH_Sec4et --admin-user mysecretname -l eastus -n samplesqlserver123 -g azure-sample-group
```

<span data-ttu-id="fbc55-147">방화벽 규칙 추가:</span><span class="sxs-lookup"><span data-stu-id="fbc55-147">Add firewall rule:</span></span>
```azurecli-interactive
az sql server firewall-rule create --end-ip-address 167.220.0.235 --name firewall_rule_name_123.123.123.123 --resource-group azure-sample-group --server samplesqlserver123 --start-ip-address 123.123.123.123
```

<span data-ttu-id="fbc55-148">SQL 데이터베이스 만들기:</span><span class="sxs-lookup"><span data-stu-id="fbc55-148">Create a SQL database:</span></span>
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

<span data-ttu-id="fbc55-149">코드가 작동하는지 확인한 후 CLI를 사용하여 SQL 데이터베이스 및 해당 리소스를 삭제합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc55-149">Once you've verified that the code worked, use the CLI to delete the SQL database and its resources.</span></span>

```azurecli-interactive
az group delete --name azure-sample-group
```

## <a name="write-a-blob-into-a-new-storage-account"></a><span data-ttu-id="fbc55-150">새 저장소 계정에 Blob 쓰기</span><span class="sxs-lookup"><span data-stu-id="fbc55-150">Write a blob into a new storage account</span></span>

<span data-ttu-id="fbc55-151">인증:</span><span class="sxs-lookup"><span data-stu-id="fbc55-151">Authenticate:</span></span>
```azcli
az login
```
<span data-ttu-id="fbc55-152">리소스 그룹 만들기:</span><span class="sxs-lookup"><span data-stu-id="fbc55-152">Create a resource group:</span></span>
```azurecli-interactive
az group create -l eastus -n sampleStorageResourceGroup
```

<span data-ttu-id="fbc55-153">저장소 계정 만들기:</span><span class="sxs-lookup"><span data-stu-id="fbc55-153">Create a storage account:</span></span>
```azurecli-interactive
az storage account create -n samplestorageaccountname -g sampleStorageResourceGroup -l eastus --sku Standard_RAGRS
```

<span data-ttu-id="fbc55-154">이 코드에서는 [Azure 저장소 계정](https://docs.microsoft.com/azure/storage/storage-introduction)을 만든 다음 Python용 Azure Storage 라이브러리를 사용하여 클라우드에 새 html 파일을 만듭니다.</span><span class="sxs-lookup"><span data-stu-id="fbc55-154">This code creates an [Azure storage account](https://docs.microsoft.com/azure/storage/storage-introduction) and then uses the Azure Storage libraries for Python to create a new html file in the cloud.</span></span> 
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
<span data-ttu-id="fbc55-155">성공적으로 업로드된 콘텐츠를 확인하려면 인쇄된 URL로 이동합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc55-155">To verify content successfully uploaded, navigate to the url printed.</span></span> 

<span data-ttu-id="fbc55-156">CLI를 사용하여 저장소 계정을 정리합니다.</span><span class="sxs-lookup"><span data-stu-id="fbc55-156">Clean up the storage account using the CLI:</span></span>
```azurecli-interactive
az group delete --name sampleStorageResourceGroup
```

## <a name="explore-more-samples"></a><span data-ttu-id="fbc55-157">더 많은 샘플 탐색</span><span class="sxs-lookup"><span data-stu-id="fbc55-157">Explore more samples</span></span>

<span data-ttu-id="fbc55-158">Python용 Azure 관리 라이브러리를 사용하여 리소스를 관리하고 작업을 자동화하는 방법에 대한 자세한 내용은 [가상 컴퓨터](python-sdk-azure-web-apps-samples.md), [웹앱](python-sdk-azure-web-apps-samples.md) 및 [SQL 데이터베이스](python-sdk-azure-sql-database-samples.md)에 대한 샘플 코드를 참조하세요.</span><span class="sxs-lookup"><span data-stu-id="fbc55-158">To learn more about how to use the Azure management libraries for Python to manage resources and automate tasks, see our sample code for [virtual machines](python-sdk-azure-web-apps-samples.md), [web apps](python-sdk-azure-web-apps-samples.md) and [SQL database](python-sdk-azure-sql-database-samples.md).</span></span>


## <a name="reference"></a><span data-ttu-id="fbc55-159">참조</span><span class="sxs-lookup"><span data-stu-id="fbc55-159">Reference</span></span>

<span data-ttu-id="fbc55-160">[참조](/python/api/overview/azure/?view=azure-python)는 모든 패키지에서 사용할 수 있습니다.</span><span class="sxs-lookup"><span data-stu-id="fbc55-160">A [reference](/python/api/overview/azure/?view=azure-python) is available for all packages.</span></span>
