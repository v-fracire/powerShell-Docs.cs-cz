---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: DSC pro Linux nxScript prostředků
ms.openlocfilehash: 339968512ab1c16c4c3785a3a19b00c3fbbf9ea1
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048127"
---
# <a name="dsc-for-linux-nxscript-resource"></a>DSC pro Linux nxScript prostředků

**NxScript** prostředků v prostředí PowerShell Desired State Configuration (DSC) poskytuje mechanismus pro spouštění skriptů Linux v systému Linux uzlu.

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
| GetScript| Poskytuje skript, který se spustí při vyvolání [Get-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521625.aspx) rutiny. Skript musí začínat shebang, jako je například #! / bin/bash.|
| SetScript| Obsahuje skript. Při vyvolání [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) rutiny **TestScript** spustí první. Pokud **TestScript** bloku vrátí výstupní kód než 0, **SetScript** blok se spustí. Pokud **TestScript** vrátí ukončovací kód 0, **SetScript** se nespustí. Skript musí začínat shebang, jako například `#!/bin/bash`.|
| TestScript| Obsahuje skript. Při vyvolání [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) , tento skript spustí. Pokud se vrátí výstupní kód než 0, se spustí SetScript. Vrátí ukončovací kód 0,-li **SetScript** se nespustí. **TestScript** poběží i v případě vyvolání [Test-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) rutiny. V takovém případě však **SetScript** se nespustí, bez ohledu na to, jaké ukončovací kód je vrácen z **TestScript**. **TestScript** musí vrátit ukončovací kód 0, pokud skutečnou konfiguraci odpovídá aktuální konfigurace požadovaného stavu a východ kódu jiné než 0, pokud neodpovídá. (Aktuální konfigurace požadovaného stavu je poslední konfigurace plnění na uzlu, který používá DSC). Skript musí začínat shebang, jako je například 1#!/bin/bash.1|
| Uživatel| Uživatel ke spuštění skriptu jako.|
| Skupina| Skupina pro spuštění skriptu jako.|
| DependsOn | Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Například pokud **ID** prostředku bloku skriptu konfigurace, který chcete spustit nejdřív ale **ResourceName** a jejím typem je **ResourceType**, syntaxe pro použití této funkce Vlastnost je `DependsOn = "[ResourceType]ResourceName"`.|

## <a name="example"></a>Příklad

Následující příklad ukazuje použití **nxScript** prostředků k provedení další správa konfigurace.

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