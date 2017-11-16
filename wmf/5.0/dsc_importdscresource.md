---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
ms.openlocfilehash: b839b476bb4ef7f8d73b158d61f0e8cbc1265e60
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
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

Před tím jediný způsob, jak při načítání prostředků DSC určit verze modulu byl pomocí specifikace objektu modulu. například:`–ModuleName @{ModuleName="UserConfigProvider";ModuleVersion="3.0"}`

