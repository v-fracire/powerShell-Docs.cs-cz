---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: 136e16ae74e54f3bc9d0623178257df1e9104aac
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="deliver-a-configuration-document-without-applying"></a><span data-ttu-id="5c643-102">Poskytování dokumentu konfigurace bez použití</span><span class="sxs-lookup"><span data-stu-id="5c643-102">Deliver a configuration document without applying</span></span>

<span data-ttu-id="5c643-103">[Publikovat DscConfiguration](https://technet.microsoft.com/library/mt517875.aspx) rutiny zkopíruje na cílový uzel konfigurační soubor MOF, ale nevztahuje konfigurace.</span><span class="sxs-lookup"><span data-stu-id="5c643-103">The [Publish-DscConfiguration](https://technet.microsoft.com/library/mt517875.aspx) cmdlet copies a configuration MOF file to a target node, but does not apply the configuration.</span></span>
<span data-ttu-id="5c643-104">Tato konfigurace se použije během průchodu další konzistence, nebo při spuštění [aktualizace DscConfiguration](https://technet.microsoft.com/library/mt143541.aspx) rutiny.</span><span class="sxs-lookup"><span data-stu-id="5c643-104">This configuration is applied during the next consistency pass, or when you run the [Update-DscConfiguration](https://technet.microsoft.com/library/mt143541.aspx) cmdlet.</span></span>