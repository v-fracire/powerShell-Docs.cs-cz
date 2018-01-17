---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Začínáme s prostředím PowerShell konfigurace požadovaného stavu"
ms.openlocfilehash: 856528f1e52eafa8b2c93b825a60376a0d64cab2
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="getting-started-with-powershell-desired-state-configuration"></a>Začínáme s prostředím PowerShell konfigurace požadovaného stavu #

Tato příručka popisuje, jak začít vytvářet dokumenty konfigurace požadovaného stavu prostředí PowerShell a použít je k počítačům. Předpokládá základní znalost rutiny prostředí PowerShell, moduly a funkce. 


## <a name="create-a-configuration"></a>Vytvoření konfigurace ##

[**Konfigurace** ](https://msdn.microsoft.com/en-us/powershell/dsc/configurations) jsou dokumenty, které popisují prostředí. Prostředí obsahovat "**uzly**", které jsou běžně virtuálních nebo fyzických počítačích. 

Konfigurace můžou mít v různých formách. Nejjednodušší způsob, jak vytvořit novou konfiguraci je vytvoření souboru s příponou .ps1 (skript prostředí PowerShell). K tomuto účelu otevřete váš editor výběru. Prostředí PowerShell ISE je dobrá volba, vzhledem k tomu, že nativně rozumí DSC. Uložte jako PS1 následující:

```powershell
configuration MyFirstConfiguration
{
    Import-DscResource -Name WindowsFeature

    Node localhost
    {
        WindowsFeature IIS
        {
            Name = "IIS"

        }
        
    }

}
```
## <a name="parts-of-a-configuration"></a>Součástí konfigurace ##
**Konfigurace** je klíčové slovo, který byl přidán do prostředí PowerShell 4.0. Označuje je zvláštní druh funkce prostředí PowerShell používané konfigurace požadovaného stavu. V tomto příkladu je funkce s názvem myFirstConfiguration. 

Na další řádek je příkaz import, podobně jako Import modulu. Bude probírat později.

"Uzel" definuje název počítače, které tato konfigurace bude fungovat na. I když tato konfigurace je upravovat místně, můžete konfigurace přístup ke vzdálené uzly a nakonfigurovat. 

Uzly mohou být názvy počítačů nebo IP adresy. Může mít více uzlů v jedné konfiguraci dokumentu. Pomocí [konfigurační data](https://msdn.microsoft.com/en-us/powershell/dsc/configdata), můžete mít také stejnou konfiguraci použít na víc uzlů. V takovém případě uzlu je "localhost" – to znamená místního počítače. 

Další položka [ **prostředků**](https://msdn.microsoft.com/en-us/powershell/dsc/resources). Prostředky jsou stavební bloky konfigurací. Každý prostředek, je modul, který definuje logiku implementace jeden aspekt počítače. Každý prostředek na počítači můžete zobrazit spuštěním **Get-DscResource** v prostředí PowerShell. Prostředky musí být na místním počítači a importovat před použitím v konfiguraci s **Import DscResource** tedy na druhém řádku této konfigurace. 

**Přijetí konfigurace**

Skript výše je uložena a spustíte, bude možné vytvořit žádný výstup. Toto je vzhledem k tomu, že konfigurace je právě funkce a skript výše má definované funkce, ale ještě není ji spustit. Jakmile je definována funkce, musí být volána:
```powershell
myFirstConfiguration
```

Po provedení konfigurace funkcí je ověření konfigurace je neplatná. Měl by mít žádné chyby syntaxe, prostředky by měly mít všechny povinné parametry definované a všechny prostředky by měly být naimportovány před spuštěním.

Po konfiguraci se spustí, vytvoří složku s názvem konfigurace obsahující **. Soubor MOF** pro každý uzel v konfiguraci. Na. Soubor MOF je formátu založených na standardech správy, který je používán DSC prostředí PowerShell pro komunikaci přes síť.

Chcete-li uplatní konfigurace:
```powershell
Start-DscConfiguration -Path ./myFirstConfiguration
```
Tím se vytvoří úlohu prostředí PowerShell, která dosáhne pro uzly v konfiguraci a nakonfiguruje je. Pokud chcete zobrazit výstup úlohy, použijte - čekání. 
```powershell
Start-DscConfiguration -Path ./myFirstConfiguration -Wait
```

