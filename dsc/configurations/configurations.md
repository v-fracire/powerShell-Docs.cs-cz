---
ms.date: 12/12/2018
keywords: DSC, powershell, konfigurace, instalační program
title: Konfigurace DSC
ms.openlocfilehash: 6af27f442de3080facd65892c713c989d0e388c5
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403731"
---
# <a name="dsc-configurations"></a>Konfigurace DSC

> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

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

Uložte skript pod názvem `.ps1` souboru.

## <a name="configuration-syntax"></a>Konfigurace syntaxe

Skript konfigurace se skládá z následujících částí:

- **Konfigurace** bloku. Toto je skript vnějšího bloku. Definovat pomocí **konfigurace** – klíčové slovo a poskytnutí názvu. Název konfigurace je v tomto případě "MyDscConfiguration".
- Jeden nebo více **uzel** bloky. Tyto zásady určují uzly (virtuální počítače nebo počítače), které konfigurujete. V konfiguraci uvedené výš, existuje **uzel** blok, který cílí na počítač s názvem "TEST-PC1". Objekt uzlu může přijmout více názvů počítačů.
- Jeden nebo více prostředků bloky. To je, kde konfiguraci nastaví vlastnosti pro prostředky, které je konfigurace. V tomto případě existují dva prostředků bloky, z nichž každý prostředek "WindowsFeature" volání.

V rámci **konfigurace** blok, můžete provést cokoli, co můžete normálně ve funkci prostředí PowerShell. Například v předchozím příkladu, pokud nechcete pevně kódu název cílového počítače v konfiguraci, můžete přidat parametr pro název uzlu:

V tomto příkladu zadáte předáním jako název uzlu **ComputerName** parametr při kompilaci konfigurace. Výchozí název "localhost".

```powershell
Configuration MyDscConfiguration
{
    param
    (
        [string[]]$ComputerName='localhost'
    )

    Node $ComputerName
    {
        WindowsFeature MyFeatureInstance
        {
            Ensure = 'Present'
            Name = 'RSAT'
        }

        WindowsFeature My2ndFeatureInstance
        {
            Ensure = 'Present'
            Name = 'Bitlocker'
        }
    }
}

MyDscConfiguration
```

**Uzel** blok můžete také přijmout více názvů počítačů. V příkladu výše, můžete použít `-ComputerName` parametr nebo pass čárkou oddělený seznam počítačů přímo k **uzel** bloku.

```powershell
MyDscConfiguration -ComputerName "localhost", "Server01"
```

Při zadávání seznamu počítačů a **uzlu** bloku, z v rámci konfigurace, je třeba použít notaci pole.

```powershell
Configuration MyDscConfiguration
{
    Node @('localhost', 'Server01')
    {
        WindowsFeature MyFeatureInstance
        {
            Ensure = 'Present'
            Name = 'RSAT'
        }

        WindowsFeature My2ndFeatureInstance
        {
            Ensure = 'Present'
            Name = 'Bitlocker'
        }
    }
}

MyDscConfiguration
```

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
  Pokud existuje více než jeden uzel, vytvoří se soubor MOF pro každý uzel.

> [!NOTE]
> Soubor MOF obsahoval všechny informace o konfiguraci pro cílový uzel. Z toho důvodu je důležité, abyste zajistili jeho zabezpečení.
> Další informace najdete v tématu [zabezpečení souboru MOF](../pull-server/secureMOF.md).

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

## <a name="using-new-resources-in-your-configuration"></a>Pomocí nových prostředků v konfiguraci

Pokud jste spustili v předchozích příkladech, jste si možná všimli, že se upozornění, které jste používali prostředku bez explicitně importu.
V současné době DSC se dodává s 12 prostředků jako součást modulu PSDesiredStateConfiguration.

Rutiny [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource), je možné určit, jaké prostředky jsou nainstalovaná v systému a k dispozici pro použití podle LCM.
Jakmile tyto moduly byly umístěny do `$env:PSModulePath` a jsou správně rozpoznány modulem [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource), stále potřebují být načteny v rámci vaší konfigurace.

**Import-DscResource** je dynamické klíčové slovo, který může být rozpoznán pouze v rámci **konfigurace** bloku není rutina.
**Import-DscResource** podporuje dva parametry:

- **Název modulu** je doporučený způsob použití **Import-DscResource**. Přijímá název modulu, který obsahuje prostředky, které se mají naimportovat (stejně jako pole řetězců názvů modulů).
- **Název** je název prostředku, který chcete importovat. Nejedná se o popisný název vrácený jako "Name" [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource), ale název třídy používá při definování schématu prostředků (vrácena jako **elementu ResourceType** podle [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource)).

Další informace o používání `Import-DSCResource`, naleznete v tématu [pomocí Import-DSCResource](import-dscresource.md)

## <a name="powershell-v4-and-v5-differences"></a>Rozdíly v4, tak i v5 prostředí PowerShell

Existují rozdíly v kdy je potřeba prostředky DSC uložené v Powershellu 4.0. Další informace najdete v tématu [umístění prostředku](import-dscresource.md#resource-location).

## <a name="see-also"></a>Viz také

- [Prostředí Windows PowerShell Desired State Configuration – přehled](../overview/overview.md)
- [Prostředky DSC](../resources/resources.md)
- [Konfigurace Local Configuration Manageru](../managing-nodes/metaConfig.md)
