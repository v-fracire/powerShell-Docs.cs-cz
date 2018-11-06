---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: 46a278b83edb9d8e3d75b0874603710d416be3b5
ms.sourcegitcommit: f4247d3f91d06ec392c4cd66921ce7d0456a2bd9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/05/2018
ms.locfileid: "50998516"
---
# <a name="import-dscresource-keyword-supports--moduleversion-parameter"></a>Klíčové slovo import-DscResource podporuje parametr - ModuleVersion

Přidali jsme nový parametr pro `Import-DscResource` dynamické klíčové slovo dostupné při vytváření konfigurace DSC. Konfigurace autoři teď můžete zadat přesně verze modulu se načíst prostředky DSC od. Nová syntaxe klíčového slova je následující:

```powershell
Import-DscResource [-Name <ResourceName(s)>] [-ModuleName <ModuleName(s)>] [-ModuleVersion <ModuleVersion>]
```

* **Název**: názvy jeden nebo více prostředků k importu.
* **Název modulu**: názvy modulů nebo ModuleSpecification objekty jeden nebo více modulů k importu.
* **ModuleVersion**: verze modulu k importu. Pokud použijete, musí představovat název modulu pouze jeden modul podle názvu.

V prostředí Windows PowerShell ISE zobrazí se s technologií IntelliSense:

![](../images/Import-DscResource-Modversion.jpg)

**Poznámka:**: `–ModuleVersion` parametr lze použít pouze v kombinaci s `–ModuleName` parametru. Nelze zadat s použitím pouze názvy prostředků `–Name` parametru.

Před tím jediný způsob, jak určit verzi modulu při načítání prostředků DSC byla například pomocí specifikace objekt Module: `–ModuleName @{ModuleName="UserConfigProvider";ModuleVersion="3.0"}`
