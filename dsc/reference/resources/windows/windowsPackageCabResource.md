---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředek Windowspackagecab DSC
ms.openlocfilehash: 035944e7ca5c7469250c48a19b79f2f2d5d38e9a
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048126"
---
# <a name="dsc-windowspackagecab-resource"></a>Prostředek Windowspackagecab DSC

> Platí pro: Prostředí Windows PowerShell 5.1 a novější

**WindowsPackageCab** prostředků ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus pro instalaci nebo odinstalaci balíčků Windows soubor CAB (.cab) na cílový uzel.

Cílový uzel musí mít nainstalovaný modul PowerShell nástroje DISM. Informace najdete v tématu [pomocí nástroje DISM prostředí Windows PowerShell](https://msdn.microsoft.com/en-us/windows/hardware/commercialize/manufacture/desktop/use-dism-in-windows-powershell-s14).


## <a name="syntax"></a>Syntaxe

```
{
    Name = [string]
    Ensure = [string] { Absent | Present }
    SourcePath = [string]
    [ LogPath = [string] ]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a>Properties

|  Vlastnost  |  Popis   |
|---|---|
| Name| Určuje název balíčku pro budete muset zajistit, aby určitý stav.|
| Zkontrolujte| Určuje, zda je nainstalován balíček. Nastavte tuto vlastnost na "Chybí" Ujistěte se, že balíček není nainstalovaný, (nebo odinstalovat balíček, je-li nainstalován). Nastavte tak, aby "Předložit" (výchozí hodnota) ujistěte se, že je balíček nainstalován.|
| Cesta| Určuje cestu, kde se nachází balíček.|
| LogPath| Určuje úplnou cestu, kam chcete poskytovatele za účelem uložení souboru protokolu instalace nebo odinstalace balíčku.|
| DependsOn | Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba **ResourceName** a jejím typem je **ResourceType**, syntaxe pro použití této vlastnosti je "DependsOn ="[ ResourceName ResourceType]"".|

## <a name="example"></a>Příklad

Následující příklad konfigurace vstupní parametry a zajistí, že soubor .cab určené `$Name` parametr je nainstalována.

```powershell
Configuration Sample_WindowsPackageCab
{
    param
    (
        [Parameter (Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String]
        $Name,

        [Parameter (Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String]
        $SourcePath,

        [Parameter(Mandatory = $true)]
        [ValidateNotNullOrEmpty()]
        [String]
        $LogPath
    )

    Import-DscResource -ModuleName 'PSDscResources'

    WindowsPackageCab WindowsPackageCab1
    {
        Name = $Name
        Ensure = 'Present'
        SourcePath = $SourcePath
        LogPath = $LogPath
    }
}
```