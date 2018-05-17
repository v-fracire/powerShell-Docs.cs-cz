---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: DSC pro Linux nxScript prostředků
ms.openlocfilehash: 339968512ab1c16c4c3785a3a19b00c3fbbf9ea1
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
---
# <a name="dsc-for-linux-nxscript-resource"></a>DSC pro Linux nxScript prostředků

**NxScript** prostředků v prostředí PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus ke spouštění skriptů Linux na uzlu Linux.

## <a name="syntax"></a>Syntaxe

```
nxScript <string> #ResourceName
{
    GetScript = <string>
    SetScript = <string>
    TestScript = <string>
    [ User = <string> ]
    [ Group = <string> ]
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a>Properties

|  Vlastnost |  Popis |
|---|---|
| GetScript| Poskytuje skript, který spouští při vyvolání [Get-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521625.aspx) rutiny. Skript musí začínat shebang, například #! / bin/bash.|
| SetScript| Poskytuje skript. Při vyvolání [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) rutiny **TestScript** spustí první. Pokud **TestScript** bloku vrátí ukončovací kód než 0, **SetScript** bloku se spustí. Pokud **TestScript** vrátí ukončovací kód 0, **SetScript** se nespustí. Skript musí začínat shebang, jako například `#!/bin/bash`.|
| TestScript| Poskytuje skript. Při vyvolání [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) tento skript spouští rutiny. Pokud vrátí ukončovací kód než 0, se spustí SetScript. Vrátí ukončovací kód 0,-li **SetScript** se nespustí. **TestScript** poběží i v případě vyvolání [Test DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) rutiny. V takovém případě však **SetScript** se nespustí, bez ohledu na to, jaké ukončovací kód je vrácen z **TestScript**. **TestScript** musí vracet ukončovací kód 0, pokud skutečné konfigurace odpovídá aktuální konfiguraci požadovaného stavu a ukončení kódu jiné než 0, pokud neodpovídá. (Aktuální konfigurace požadovaného stavu je poslední konfigurace použity na uzlu, který používá DSC). Skript musí začínat shebang, jako je například 1#!/bin/bash.1|
| Uživatel| Uživatele k spuštění skriptu jako.|
| Skupina| Skupina pro spuštění skriptu jako.|
| dependsOn | Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Například pokud **ID** prostředku blok skriptu konfigurace, který chcete spustit nejprve je **ResourceName** a její typ je **ResourceType**, pomocí této syntaxe Vlastnost je `DependsOn = "[ResourceType]ResourceName"`.|

## <a name="example"></a>Příklad

Následující příklad ukazuje použití **nxScript** prostředek se má provést další konfiguraci správy.

```
Import-DSCResource -Module nx

Node $node {
nxScript KeepDirEmpty{

    GetScript = @"
#!/bin/bash
ls /tmp/mydir/ | wc -l
"@

    SetScript = @"
#!/bin/bash
rm -rf /tmp/mydir/*
"@

    TestScript = @'
#!/bin/bash
filecount=`ls /tmp/mydir | wc -l`
if [ $filecount -gt 0 ]
then
    exit 1
else
    exit 0
fi
'@
}
}
```