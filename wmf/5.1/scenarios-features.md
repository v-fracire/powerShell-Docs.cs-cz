---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: wmf,powershell,setup
title: Nové scénáře a funkce v WMF 5.1
ms.openlocfilehash: 77b439e61c5802f8ddbc4a0f39923cc8c0c36fe9
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
ms.locfileid: "34190311"
---
# <a name="new-scenarios-and-features-in-wmf-51"></a>Nové scénáře a funkce v WMF 5.1

> Poznámka: Tyto informace jsou předběžné a může se změnit.

## <a name="powershell-editions"></a>Edice PowerShellu

Od verze 5.1 je PowerShell k dispozici v různých edicích, které uvádějí různé sady funkcí a kompatibilitu platformy.

- **Desktop Edition:** Tato edice je založená na rozhraní .NET Framework a zajišťuje kompatibilitu se skripty a moduly cílenými na verze PowerShellu spouštěné na plných edicích Windows, jako je Jádro serveru a Windows Desktop.
- **Core Edition:** Tato edice je založená na rozhraní .NET Core a zajišťuje kompatibilitu se skripty a moduly cílenými na verze PowerShellu spouštěné na edicích Windows s nízkými nároky na prostředky, jako je Nano Server a Windows IoT.

**Další informace o používání prostředí PowerShell edice**

- [Určení spuštěné ve verzi prostředí PowerShell pomocí $PSVersionTable](/powershell/module/microsoft.powershell.core/about/about_automatic_variables)
- [Filtrování výsledků Get-Module podle CompatiblePSEditions pomocí parametru PSEdition](/powershell/module/microsoft.powershell.core/get-module)
- [Zabránit spuštění skriptu, není-li spustit na kompatibilní verzi prostředí PowerShell](/powershell/gallery/psget/script/scriptwithpseditionsupport)
- [Deklarace modul kompatibility na konkrétní verze prostředí PowerShell](/powershell/gallery/psget/module/modulewithpseditionsupport)

## <a name="catalog-cmdlets"></a>Rutiny katalogu

Byly přidány dva nové rutiny v [Microsoft.PowerShell.Security](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.security) modulu; tato generovat a ověření souborů katalogu systému Windows.

### <a name="new-filecatalog"></a>New-FileCatalog
--------------------------------

Nové FileCatalog vytvoří soubor katalogu systému Windows pro sadu složek a souborů.
Tento soubor katalogu obsahuje hodnoty hash pro všechny soubory v zadané cesty.
Uživatele můžete distribuovat sadu složek spolu s odpovídající soubor katalogu představující těchto složek.
Tyto informace jsou užitečné pro ověření, zda byly provedeny změny do složek od okamžiku vytvoření katalogu.

```powershell
New-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-CatalogVersion <int>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

Jsou podporovány katalogu verze 1 a 2.
Verze 1 používá algoritmus hash SHA1 k vytvoření hodnoty hash souboru; verze 2 používá algoritmus SHA256.
Katalog verze 2 není podporována na *Windows Server 2008 R2* nebo *Windows 7*.
Měli byste použít katalogu verze 2 v *Windows 8*, *systému Windows Server 2012*a novějších operačních systémech.

![](../images/NewFileCatalog.jpg)

Tím se vytvoří soubor katalogu.

![](../images/CatalogFile1.jpg)

![](../images/CatalogFile2.jpg)

Chcete-li ověřit integritu soubor katalogu (Pester.cat v výše příkladu), podepište ho pomocí [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) rutiny.

### <a name="test-filecatalog"></a>Test FileCatalog
--------------------------------

Test FileCatalog ověří katalogu představující sadu složek.

```powershell
Test-FileCatalog [-CatalogFilePath] <string> [[-Path] <string[]>] [-Detailed] [-FilesToSkip <string[]>] [-WhatIf] [-Confirm] [<CommonParameters>]
```

![](../images/TestFileCatalog.jpg)

Tato rutina porovná všechny hodnoty hash souborů a jejich relativní cesty v *katalogu* s těch, které jsou na *disku*.
Pokud zjistí jakékoli neshody mezi hodnoty hash souboru a cesty vrátí stav jako *ValidationFailed*.
Uživatele můžete načíst pomocí těchto informací *-podrobné* parametr.
Také se zobrazí stav podpisový katalogu v *podpis* vlastnost, která je ekvivalentní volání [Get-AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx) na soubor katalogu rutinu.
Uživatelé také přeskočit všechny soubory během ověřování pomocí *- FilesToSkip* parametr.

## <a name="module-analysis-cache"></a>Modul Analysis mezipaměti

Od verze WMF 5.1, prostředí PowerShell umožňuje řídit soubor, který se používá k o modulu, například příkazy exportuje data do mezipaměti.

Ve výchozím nastavení je tato mezipaměť uložené v souboru `${env:LOCALAPPDATA}\Microsoft\Windows\PowerShell\ModuleAnalysisCache`.
Mezipaměť je obvykle pro čtení na spuštění při vyhledávání pro příkaz a je zapsán v vlákna na pozadí zopakovat po importování modulu.

Chcete-li změnit výchozí umístění mezipaměti, nastavte `$env:PSModuleAnalysisCachePath` proměnnou prostředí před spuštěním prostředí PowerShell.
Změny této proměnné prostředí mají vliv jenom podřízené procesy.
Hodnota by měla název úplná cesta (včetně názvu souboru), který má oprávnění k vytvoření a zapisovat soubory prostředí PowerShell.
Mezipaměť souborů se zakázat, nastavte hodnotu neplatné umístění, například:

```powershell
$env:PSModuleAnalysisCachePath = 'nul'
```

Nastaví tato cesta neplatná zařízení.
Pokud PowerShell nemůže zapisovat do cesty, je vrácena žádná chyba, ale uvidíte pomocí trasovací zpráv o chybách:

```powershell
Trace-Command -PSHost -Name Modules -Expression { Import-Module Microsoft.PowerShell.Management -Force }
```

Při zápisu se do mezipaměti, zkontroluje, prostředí PowerShell pro moduly, které už existují předejdete zbytečně velké mezipaměti.
Někdy těmito kontrolami není vhodná, v takovém případě můžete vypnout jejich nastavením:

```powershell
$env:PSDisableModuleAnalysisCacheCleanup = 1
```

Nastavení této proměnné prostředí se projeví okamžitě v aktuálním procesu.

## <a name="specifying-module-version"></a>Určení verze modulu

V WMF 5.1 `using module` se chová stejně jako jiné související modulu konstrukce v prostředí PowerShell.
Dříve bylo žádný způsob, jak určit konkrétního modulu verze; kdyby existovalo víc verzí přítomen, výsledkem chyba.

V WMF 5.1:

- Můžete použít [ModuleSpecification – konstruktor (zatřiďovací tabulky)](https://msdn.microsoft.com/library/jj136290).
Tato tabulka hodnota hash má stejný formát jako `Get-Module -FullyQualifiedName`.

**Příklad:** `using module @{ModuleName = 'PSReadLine'; RequiredVersion = '1.1'}`

- Pokud existuje více verzí modulu, používá prostředí PowerShell **stejné logiky, která řešení** jako `Import-Module` a nevrací chybu – stejné chování jako `Import-Module` a `Import-DscResource`.

## <a name="improvements-to-pester"></a>Vylepšení Pester

V WMF 5.1 verzi Pester, který se dodává s prostředím PowerShell, má z 3.3.5 aktualizovaná tak, aby 3.4.0 doplněný o potvrzení https://github.com/pester/Pester/pull/484/commits/3854ae8a1f215b39697ac6c2607baf42257b102e, což umožňuje lepší chování pro Pester na Nano Server.

Můžete zkontrolovat změny ve verzích 3.3.5 k 3.4.0 zkontrolováním souboru ChangeLog.md v: https://github.com/pester/Pester/blob/master/CHANGELOG.md
