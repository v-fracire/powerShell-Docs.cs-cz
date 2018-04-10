---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: a3b176101bebf7081febd8629bddcfa0ae1e7540
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="import-dscresource-keyword-supports--moduleversion-parameter"></a>Parametr - ModuleVersion podporuje import DscResource – klíčové slovo

Jsme přidali nový parametr, který se `Import-DscResource` dynamické – klíčové slovo dostupné při vytváření konfigurace DSC. Autoři konfigurace nyní můžete určit přesně verze načíst prostředky DSC z které modulu. Nové syntaxe klíčového slova je:

```powershell
Import-DscResource [-Name <ResourceName(s)>] [-ModuleName <ModuleName(s)>] [-ModuleVersion <ModuleVersion>]
```

* **Název**: názvy jeden nebo více prostředků pro import.
* **Název modulu**: názvy modulů nebo ModuleSpecification objekty jeden nebo více modulů pro import.
* **Verze modulu**: verzi importu typ objektu modulu. Pokud se používá, název modulu musí představovat pouze jeden modul podle názvu.

V systému Windows PowerShell ISE se zobrazí s IntelliSense:

![](../images/Import-DscResource-Modversion.jpg)

**Poznámka:**: `–ModuleVersion` parametr lze použít pouze v kombinaci s `–ModuleName` parametr. Nedá se použít s názvy prostředků pomocí pouze `–Name` parametr.

Před tím jediný způsob, jak při načítání prostředků DSC určit verze modulu byl pomocí specifikace objektu modulu. například: `–ModuleName @{ModuleName="UserConfigProvider";ModuleVersion="3.0"}`