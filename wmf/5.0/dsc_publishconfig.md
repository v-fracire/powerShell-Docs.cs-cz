---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: f929ce4684bb53c3039238ecd465f1c0e432f741
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
ms.locfileid: "34225670"
---
# <a name="deliver-a-configuration-document-without-applying"></a>Poskytování dokumentu konfigurace bez použití

[Publikovat DscConfiguration](https://technet.microsoft.com/library/mt517875.aspx) rutiny zkopíruje na cílový uzel konfigurační soubor MOF, ale nevztahuje konfigurace.
Tato konfigurace se použije během průchodu další konzistence, nebo při spuštění [aktualizace DscConfiguration](https://technet.microsoft.com/library/mt143541.aspx) rutiny.
