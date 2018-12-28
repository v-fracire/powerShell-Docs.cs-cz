---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Rychlý start – vytvoření webu s DSC
ms.openlocfilehash: c62e2d8af46bf74c4dd13069ddff6cc39763a209
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403634"
---
> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

# <a name="quickstart---create-a-website-with-dsc"></a>Rychlý start – vytvoření webu s DSC

V tomto cvičení vás provedou vytvořením a aplikování konfigurace Desired State Configuration (DSC) od začátku do konce.
Příklad použijeme zajistí, že je na serveru `Web-Server` povolena funkce (služby IIS), a je k dispozici v obsahu pro jednoduchý web "Hello World" `intepub\wwwroot` adresáře tohoto serveru.

Přehled o novinkách DSC a jak to funguje, najdete v části [Desired State Configuration přehled pro pracovníky s rozhodovací pravomocí](../overview/decisionMaker.md).

## <a name="requirements"></a>Požadavky

Chcete-li spustit tento příklad, musíte počítač se systémem Windows Server 2012 nebo novější a prostředí PowerShell 4.0 nebo novější.

## <a name="write-and-place-the-indexhtm-file"></a>Zápis a umístěte soubor index.htm

Nejprve vytvoříme soubor HTML, který budeme používat jako obsah webu.

V kořenové složce vytvořte složku s názvem `test`.

V textovém editoru zadejte následující text:

```html
<head></head>
<body>
<p>Hello World!</p>
</body>
```

Uložit jako `index.htm` v `test` složky, které jste vytvořili dříve.

## <a name="write-the-configuration"></a>Zapsat konfiguraci

A [konfigurace DSC](../configurations/configurations.md) je speciální funkce prostředí PowerShell, který definuje, jak chcete nakonfigurovat jeden nebo více cílových počítačů (uzlů).

V prostředí PowerShell ISE zadejte následující příkaz:

```powershell
Configuration WebsiteTest {

    # Import the module that contains the resources we're using.
    Import-DscResource -ModuleName PsDesiredStateConfiguration

    # The Node statement specifies which targets this configuration will be applied to.
    Node 'localhost' {

        # The first resource block ensures that the Web-Server (IIS) feature is enabled.
        WindowsFeature WebServer {
            Ensure = "Present"
            Name   = "Web-Server"
        }

        # The second resource block ensures that the website content copied to the website root folder.
        File WebsiteContent {
            Ensure = 'Present'
            SourcePath = 'c:\test\index.htm'
            DestinationPath = 'c:\inetpub\wwwroot'
        }
    }
}
```

Uložte soubor jako `WebsiteTest.ps1`.

Uvidíte, že to vypadá funkce prostředí PowerShell, a uveďte klíčového slova **konfigurace** nepoužili název funkce.

**Uzel** bloku Určuje cílový uzel nakonfigurovat, v tomto případě `localhost`.

Konfigurace vyžaduje dvě [prostředky](../resources/resources.md), **WindowsFeature** a **souboru**.
Prostředky vykonávají práci třeba zajistit, který cílový uzel je ve stavu, které jsou definované v konfiguraci.

## <a name="compile-the-configuration"></a>Kompilace konfigurace

Pro konfiguraci DSC, kterou chcete použít pro uzel je nutné nejprve být zkompilován do souboru MOF.
K tomuto účelu spustit konfiguraci jako funkce.
V konzole Powershellu přejděte do stejné složky, kam jste uložili konfiguraci a spusťte následující příkazy ke kompilaci konfigurace do souboru MOF:

```powershell
. .\WebsiteTest.ps1
WebsiteTest
```

Tím se vygeneruje následující výstup:

```
Directory: C:\ConfigurationTest\WebsiteTest


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/13/2017   5:20 PM           2746 localhost.mof
```

První řádek provede konfiguraci funkce dostupné v konzole.
Druhý řádek se spustí v konfiguraci.
Výsledkem je, že novou složku s názvem `WebsiteTest` je vytvořen jako podsložky do aktuální složky.
`WebsiteTest` Složka obsahuje soubor s názvem `localhost.mof`.
Je tento soubor, který lze následně použít na cílový uzel.

## <a name="apply-the-configuration"></a>Použít konfiguraci

Teď, když máte zkompilovaný soubor MOF, můžete provést konfiguraci na cílový uzel (v tomto případě místní počítač) pomocí volání [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) rutiny.

`Start-DscConfiguration` Říká rutiny [místní Configuration Manageru (LCM)](../managing-nodes/metaConfig.md), což je modul DSC, chcete-li použít konfiguraci.
LCM provádí volání prostředky DSC můžete použít konfiguraci.

V konzole Powershellu přejděte do stejné složky, kam jste uložili konfiguraci a spusťte následující příkaz:

```powershell
Start-DscConfiguration .\WebsiteTest
```

## <a name="test-the-configuration"></a>Otestujte konfiguraci

Můžete volat [Get-DscConfigurationStatus](/powershell/module/psdesiredstateconfiguration/get-dscconfigurationstatus) rutiny zobrazíte, jestli konfigurace proběhla úspěšně.

Můžete také otestovat výsledky přímo, v tomto případě tak, že přejdete do `http://localhost/` ve webovém prohlížeči.
Jako první krok v tomto příkladu byste měli vidět "Hello World" HTML stránka, kterou jste vytvořili.

## <a name="next-steps"></a>Další kroky

- Další informace o konfiguracích DSC na [konfigurací DSC](../configurations/configurations.md).
- Podívejte se, jaké prostředky DSC jsou k dispozici a jak vytvořit vlastní prostředky DSC na [prostředky DSC](../resources/resources.md).
- Najděte prostředky v a konfigurace DSC [Galerie prostředí PowerShell](https://www.powershellgallery.com/).
