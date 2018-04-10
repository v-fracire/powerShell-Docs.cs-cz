---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: DSC pro Linux nxFileLine prostředků
ms.openlocfilehash: 798bfa4150996622c33c77d6a5aa3be4af342f1b
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-for-linux-nxfileline-resource"></a>DSC pro Linux nxFileLine prostředků

**NxFileLine** prostředků v prostředí PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus pro ke správě řádky v konfiguračním souboru na uzlu Linux.

## <a name="syntax"></a>Syntaxe

```
nxFileLine <string> #ResourceName
{
    FilePath = <string>
    ContainsLine = <string>
    [ DoesNotContainPattern = <string> ]
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a>Properties

|  Vlastnost |  Popis |
|---|---|
| FilePath| Úplná cesta k souboru ke správě řádků v na cílový uzel.|
| ContainsLine| Řádek zajistit existuje v souboru. Tento řádek bude připojen k souboru, pokud neexistuje v souboru. **ContainsLine** je povinná, ale můžete nastavit na prázdný řetězec ("ContainsLine =".) Pokud není nutné.|
| DoesNotContainPattern| Vzor regulárního výrazu řádky, které by neměly existovat v souboru. Pro všechny řádky, které existují v souboru odpovídající regulárnímu výrazu se odeberou ze souboru na řádku.|
| dependsOn | Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Například pokud **ID** prostředku blok skriptu konfigurace, který chcete spustit nejprve je **ResourceName** a její typ je **ResourceType**, pomocí této syntaxe Vlastnost je `DependsOn = "[ResourceType]ResourceName"`.|

## <a name="example"></a>Příklad

Tento příklad ukazuje, jak pomocí **nxFileLine** prostředků ke konfiguraci `/etc/sudoers` souboru zajistit, aby uživatel: monuser nakonfigurovaný tak, aby není requiretty.

```
Import-DSCResource -Module nx

nxFileLine DoNotRequireTTY
{
   FilePath = “/etc/sudoers”
   ContainsLine = 'Defaults:monuser !requiretty'
   DoesNotContainPattern = "Defaults:monuser[ ]+requiretty"
}
```