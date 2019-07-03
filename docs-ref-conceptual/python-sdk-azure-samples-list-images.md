---
title: 이미지 나열
description: 가상 머신을 만드는 데 사용할 수 있는 모든 이미지를 인쇄합니다.
author: lisawong19
manager: douge
ms.assetid: ''
ms.devlang: python
ms.topic: article
ms.service: Azure
ms.technology: Azure
ms.date: 6/15/2017
ms.author: routlaw
ms.openlocfilehash: 5473c2f58af997695b8d1a6b1d2cfb6c504b50a5
ms.sourcegitcommit: 46bebbf5dd558750043ce5afadff2ec3714a54e6
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/03/2019
ms.locfileid: "67534431"
---
# <a name="list-images"></a><span data-ttu-id="46d18-103">이미지 나열</span><span class="sxs-lookup"><span data-stu-id="46d18-103">List images</span></span>

<span data-ttu-id="46d18-104">다음 코드를 사용하여 모든 SKU 및 버전을 포함하여 가상 머신을 만드는 데 사용할 수 있는 모든 이미지를 인쇄합니다.</span><span class="sxs-lookup"><span data-stu-id="46d18-104">Use the following code to print all of the available images to use for creating virtual machines, including all skus and versions.</span></span>

```python
region = 'eastus'

result_list_pub = compute_client.virtual_machine_images.list_publishers(
    region,
)

for publisher in result_list_pub:
    result_list_offers = compute_client.virtual_machine_images.list_offers(
        region,
        publisher.name,
    )

    for offer in result_list_offers:
        result_list_skus = compute_client.virtual_machine_images.list_skus(
            region,
            publisher.name,
            offer.name,
        )

        for sku in result_list_skus:
            result_list = compute_client.virtual_machine_images.list(
                region,
                publisher.name,
                offer.name,
                sku.name,
            )

            for version in result_list:
                result_get = compute_client.virtual_machine_images.get(
                    region,
                    publisher.name,
                    offer.name,
                    sku.name,
                    version.name,
                )

                print('PUBLISHER: {0}, OFFER: {1}, SKU: {2}, VERSION: {3}'.format(
                    publisher.name,
                    offer.name,
                    sku.name,
                    version.name,
                ))
```
