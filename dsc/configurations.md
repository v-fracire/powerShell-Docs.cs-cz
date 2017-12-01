---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: Konfigurace DSC
ms.openlocfilehash: c0cf0e7aa1d18898c50a0662e4fc76ab02932f08
ms.sourcegitcommit: 7bb75bfb8d12aaa6b6071dcb2ca639d4ecceef26
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/01/2017
---
# <a name="dsc-configurations"></a>Konfigurace DSC

>Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

Konfigurace DSC jsou skripty prostředí PowerShell, které definují speciální typ funkce. K definování konfigurace, použijte klíčové slovo prostředí PowerShell **konfigurace**.

```powershell
Configuration MyDscConfiguration {

    Node "TEST-PC1" {
        WindowsFeature MyFeatureInstance {
            Ensure = "Present"
            Name =  "RSAT"
        }
        WindowsFeature My2ndFeatureInstance {
            Ensure = "Present"
            Name = "Bitlocker"
        }
    }
}
MyDscConfiguration

```

Uložte skript jako souboru s příponou .ps1.

## <a name="configuration-syntax"></a>Konfigurace syntaxe

Konfigurační skript se skládá z následujících částí:

- **Konfigurace** bloku. Toto je blok nejkrajnější skriptu. Můžete definovat pomocí **konfigurace** – klíčové slovo a poskytnutí názvu. Název konfigurace je v tomto případě "MyDscConfiguration".
- Jeden nebo více **uzlu** bloky. Tyto zásady určují uzly (počítačů nebo virtuální počítače), které konfigurujete. Ve výše uvedené konfiguraci je jeden **uzlu** bloku, která je cílena počítači s názvem "TEST-PC1".
- Jeden nebo více prostředků bloky. Toto je, kde konfigurace nastaví vlastnosti pro prostředky, které je konfigurace. V takovém případě existují dva bloky prostředků, z nichž každý volání prostředků "WindowsFeature".

V rámci **konfigurace** blok, můžete provést všechno, co se za normálních okolností může ve funkci prostředí PowerShell. Například v předchozím příkladu, pokud nebyla chcete pevného code název cílového počítače v konfiguraci, můžete přidat parametr pro název uzlu:

```powershell
Configuration MyDscConfiguration {

    param(
        [string[]]$ComputerName="localhost"
    )
    Node $ComputerName {
        WindowsFeature MyFeatureInstance {
            Ensure = "Present"
            Name =  "RSAT"
        }
        WindowsFeature My2ndFeatureInstance {
            Ensure = "Present"
            Name = "Bitlocker"
        }
    }
}
MyDscConfiguration

```

V tomto příkladu zadejte název uzlu předáním jej jako **ComputerName** parametr při kompilaci zobrazí. Výchozí název "localhost".

## <a name="compiling-the-configuration"></a>Kompilování konfigurace

Před konfigurací můžete uplatní, budete muset kompilována MOF dokumentu. To provedete pomocí volání konfigurace jako funkce prostředí PowerShell.  
Poslední řádek v příkladu obsahující pouze název konfigurace, zavolá konfigurace.

>**Poznámka:** volat konfigurace, musí být funkce v globálním oboru (stejně jako u jakékoli jiné funkce prostředí PowerShell). 
>Můžete použít tento dojít buď pomocí "dot-sourcing" skriptu, nebo spuštěním skriptu konfigurace pomocí F5 nebo kliknutím na **spustit skript** tlačítko (ISE) v. 
>Zdroj tečkou skriptu, spusťte příkaz `. .\myConfig.ps1` kde `myConfig.ps1` je název souboru skriptu, který obsahuje konfiguraci.

Při volání v konfiguraci ji:

- Přeloží všechny proměnné 
- Vytvoří složku v aktuálním adresáři se stejným názvem jako konfiguraci.
- Vytvoří soubor s názvem _NodeName_MOF do nového adresáře, kde _NodeName_ je název cílový uzel konfigurace. 
    Pokud je více než jeden uzlů, vytvoří se soubor MOF pro každý uzel.

>**Poznámka:**: soubor MOF obsahuje všechny informace o konfiguraci pro cílový uzel. Z toho důvodu je důležité k lepšímu zabezpečení. 
>Další informace najdete v tématu [zabezpečení souboru MOF](secureMOF.md).

Kompilování první konfiguraci výše má za následek následující strukturu složek:

```powershell
. .\MyDscConfiguration.ps1
MyDscConfiguration
```

```
    Directory: C:\users\default\Documents\DSC Configurations\MyDscConfiguration
Mode                LastWriteTime         Length Name                                                                                              
----                -------------         ------ ----                                                                                         
-a----       10/23/2015   4:32 PM           2842 localhost.mof
```  

Pokud konfigurace přebírá parametr, jako v druhém příkladu, který je třeba zadat v době kompilace. Zde je, který vzhledu:

```powershell
. .\MyDscConfiguration.ps1
MyDscConfiguration -ComputerName 'MyTestNode'
```

```
    Directory: C:\users\default\Documents\DSC Configurations\MyDscConfiguration
Mode                LastWriteTime         Length Name                                                                                              
----                -------------         ------ ----                                                                                         
-a----       10/23/2015   4:32 PM           2842 MyTestNode.mof
```      

## <a name="using-dependson"></a>Pomocí DependsOn

Je užitečné DSC – klíčové slovo **DependsOn**. Obvykle (i když není vždy), platí prostředky v pořadí, ve kterém se zobrazují v rámci konfigurace DSC. Ale **DependsOn** Určuje, které prostředky závisí na jiné prostředky, a LCM zajistí, že jejich použití ve správném pořadí, bez ohledu na pořadí, ve které prostředků jsou definovány instancí. Například, konfigurace může určit, že instance **uživatele** prostředků závisí na existenci **skupiny** instance:

```powershell
Configuration DependsOnExample {
    Node Test-PC1 {
        Group GroupExample {
            Ensure = "Present"
            GroupName = "TestGroup"
        }

        User UserExample {
            Ensure = "Present"
            UserName = "TestUser"
            FullName = "TestUser"
            DependsOn = "[Group]GroupExample"
        }
    }
}

```

## <a name="using-new-resources-in-your-configuration"></a>Pomocí nové prostředky ve vaší konfiguraci

Pokud jste spustili v předchozích příkladech, budete možná jste si všimli, že byly varování, že jste používali prostředku bez explicitně jeho import.
V současné době DSC se dodává s 12 prostředky jako součást modulu PSDesiredStateConfiguration. Další prostředky v externích moduly musí být umístěny v `$env:PSModulePath` aby rozpoznala LCM. Nové rutiny [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx), můžete použít k určení, jaké prostředky jsou nainstalovaná v systému a k dispozici pro použití LCM. Jakmile tyto moduly byly umístěny do `$env:PSModulePath` a jsou správně rozpoznáno [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx), ještě musí být načíst v konfiguraci. 
**Import DscResource** je dynamické klíčové slovo, které může být rozeznána pouze v rámci **konfigurace** bloku (tj. není rutina). 
**Import DscResource** podporuje dva parametry:
- **Název modulu** je doporučený způsob použití **Import DscResource**. Přijímá název modul, který obsahuje prostředky, které mají být importované (i pole řetězců názvů modulu). 
- **Název** je název prostředku pro import. Nejedná se o popisný název vrácené jako "Název" [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx), ale název třídy, které se používá při definování schématu zdroje (vrátí jako **ResourceType** podle [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx)). 

## <a name="see-also"></a>Viz také
* [Přehled stavu konfigurace požadovaného prostředí Windows PowerShell](overview.md)
* [Prostředky DSC](resources.md)
* [Konfigurace správce místní konfigurace](metaConfig.md)

