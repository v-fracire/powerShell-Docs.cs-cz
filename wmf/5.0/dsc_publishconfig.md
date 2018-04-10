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
# <a name="deliver-a-configuration-document-without-applying"></a>Poskytování dokumentu konfigurace bez použití

[Publikovat DscConfiguration](https://technet.microsoft.com/library/mt517875.aspx) rutiny zkopíruje na cílový uzel konfigurační soubor MOF, ale nevztahuje konfigurace.
Tato konfigurace se použije během průchodu další konzistence, nebo při spuštění [aktualizace DscConfiguration](https://technet.microsoft.com/library/mt143541.aspx) rutiny.