---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Konfigurace DSC
ms.openlocfilehash: 171068acb51f44e31c81e63f6640222ef71bee38
ms.sourcegitcommit: 77f62a55cac8c13d69d51eef5fade18f71d66955
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/17/2018
ms.locfileid: "39093690"
---
# <a name="dsc-configurations"></a>Konfigurace DSC

> Platí pro: Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

Konfigurace DSC se skripty Powershellu, které definují speciální typ funkce.
K definování konfigurace, použijte prostředí PowerShell – klíčové slovo **konfigurace**.

```powershell
Configuration MyDscConfiguration {
    Node "TEST-PC1" {
        WindowsFeature MyFeatureInstance {
            Ensure = 'Present'
            Name = 'RSAT'
        }
        WindowsFeature My2ndFeatureInstance {
            Ensure = 'Present'
            Name = 'Bitlocker'
        }
    }
}
MyDscConfiguration
```

Uložte skript jako soubor .ps1.

## <a name="configuration-syntax"></a>Konfigurace syntaxe

Skript konfigurace se skládá z následujících částí:

- **Konfigurace** bloku. Toto je skript vnějšího bloku. Definovat pomocí **konfigurace** – klíčové slovo a poskytnutí názvu. Název konfigurace je v tomto případě "MyDscConfiguration".
- Jeden nebo více **uzel** bloky. Tyto zásady určují uzly (virtuální počítače nebo počítače), které konfigurujete. V konfiguraci uvedené výš, existuje **uzel** blok, který cílí na počítač s názvem "TEST-PC1".
- Jeden nebo více prostředků bloky. To je, kde konfiguraci nastaví vlastnosti pro prostředky, které je konfigurace. V tomto případě existují dva prostředků bloky, z nichž každý prostředek "WindowsFeature" volání.

V rámci **konfigurace** blok, můžete provést cokoli, co můžete normálně ve funkci prostředí PowerShell. Například v předchozím příkladu, pokud nechcete pevně kódu název cílového počítače v konfiguraci, můžete přidat parametr pro název uzlu:

```powershell
Configuration MyDscConfiguration {
    param(
        [string[]]$ComputerName='localhost'
    )
    Node $ComputerName {
        WindowsFeature MyFeatureInstance {
            Ensure = 'Present'
            Name = 'RSAT'
        }
        WindowsFeature My2ndFeatureInstance {
            Ensure = 'Present'
            Name = 'Bitlocker'
        }
    }
}
MyDscConfiguration -ComputerName $ComputerName
```

V tomto příkladu zadáte předáním jako název uzlu **ComputerName** parametr při kompilaci konfigurace. Výchozí název "localhost".

## <a name="compiling-the-configuration"></a>Kompilace konfigurace

Předtím, než může přijmout konfiguraci, budete muset zkompilovat ji do dokument MOF.
To provedete voláním konfigurace, jako by volání funkce prostředí PowerShell.
Poslední řádek v příkladu obsahující název konfigurace, volá konfigurace.

> [!NOTE]
> Volání na konfiguraci, musí být funkce v globálním oboru (stejně jako u jakékoli jiné funkce Powershellu).
> Můžete provést toto možné buď pomocí "dot-sourcing" skript, nebo spuštěním skriptu konfigurace pomocí klávesy F5 nebo kliknutím na **spustit skript** tlačítko v prostředí ISE.
> Dot-source skriptu, spusťte příkaz `. .\myConfig.ps1` kde `myConfig.ps1` je název souboru skriptu, který obsahuje vaši konfiguraci.

Při volání v konfiguraci ji:

- Přeloží všechny proměnné
- Vytvoří složku v aktuálním adresáři se stejným názvem jako konfiguraci.
- Vytvoří soubor s názvem _NodeName_MOF v novém adresáři, ve kterém _NodeName_ je název uzlu cílové konfigurace.
  Pokud existuje více uzlů, vytvoří se soubor MOF pro každý uzel.

> [!NOTE]
> Soubor MOF obsahoval všechny informace o konfiguraci pro cílový uzel. Z toho důvodu je důležité, abyste zajistili jeho zabezpečení.
> Další informace najdete v tématu [zabezpečení souboru MOF](secureMOF.md).

Kompilování první konfigurace nad výsledky ve struktuře následující složky:

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

Pokud má parametr, viz druhý příklad konfigurace, který má být k dispozici v době kompilace. Tady je způsob, který by vypadalo:

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

Je užitečné DSC – klíčové slovo **DependsOn**. Obvykle (i když není vždy), platí prostředky v pořadí, ve kterém se zobrazují v rámci konfigurace DSC.
Ale **DependsOn** Určuje, které prostředky jsou závislé na jiných prostředcích a LCM se zajistí, že se použijí ve správném pořadí, bez ohledu na pořadí, ve které prostředky jsou definovány instancí.
Konfigurace například můžou určit, že instance **uživatele** prostředků závisí na existenci **skupiny** instance:

```powershell
Configuration DependsOnExample {
    Node Test-PC1 {
        Group GroupExample {
            Ensure = 'Present'
            GroupName = 'TestGroup'
        }

        User UserExample {
            Ensure = 'Present'
            UserName = 'TestUser'
            FullName = 'TestUser'
            DependsOn = '[Group]GroupExample'
        }
    }
}
```

## <a name="using-new-resources-in-your-configuration"></a>Pomocí nových prostředků v konfiguraci

Pokud jste spustili v předchozích příkladech, jste si možná všimli, že se upozornění, které jste používali prostředku bez explicitně importu.
V současné době DSC se dodává s 12 prostředků jako součást modulu PSDesiredStateConfiguration.
Ostatní prostředky v externích modulech musí být umístěn v `$env:PSModulePath` aby bylo možné je nerozpoznají LCM.
Nová rutina [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx), je možné určit, jaké prostředky jsou nainstalovaná v systému a k dispozici pro použití podle LCM.
Jakmile tyto moduly byly umístěny do `$env:PSModulePath` a jsou správně rozpoznány modulem [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx), stále potřebují být načteny v rámci vaší konfigurace.
**Import-DscResource** je dynamické klíčové slovo, který může být rozpoznán pouze v rámci **konfigurace** blok (tedy není rutina).
**Import-DscResource** podporuje dva parametry:

- **Název modulu** je doporučený způsob použití **Import-DscResource**. Přijímá název modulu, který obsahuje prostředky, které se mají naimportovat (stejně jako pole řetězců názvů modulů).
- **Název** je název prostředku, který chcete importovat. Nejedná se o popisný název vrácený jako "Name" [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx), ale název třídy používá při definování schématu prostředků (vrácena jako **elementu ResourceType** podle [Get-DscResource](https://technet.microsoft.com/library/dn521625.aspx)).

## <a name="see-also"></a>Viz také

- [Prostředí Windows PowerShell Desired State Configuration – přehled](overview.md)
- [Prostředky DSC](resources.md)
- [Konfigurace Local Configuration Manageru](metaConfig.md)