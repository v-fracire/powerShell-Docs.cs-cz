---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Desired State Configuration rychlý Start"
ms.openlocfilehash: e21017f24db8c90229063895c1a7e4c6f0546d0c
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

# <a name="desired-state-configuration-quick-start"></a>Desired State Configuration rychlý Start

Tento postup vás provede vytvořením a použitím konfiguraci konfigurace požadovaného stavu (DSC) od začátku do konce.
V příkladu použijeme zajistí, že má server `Web-Server` povolena funkce (IIS) a která je k dispozici v obsahu pro jednoduchý web "Hello World" `intepub\wwwroot` adresáři z tohoto serveru.

Přehled DSC a jak to funguje, najdete v tématu [potřeby přehled stavu konfigurace pro rozhodují](decisionMaker.md).

## <a name="requirements"></a>Požadavky

Pokud chcete spustit tento příklad, budete potřebovat počítač se systémem Windows Server 2012 nebo novější a prostředí PowerShell 4.0 nebo novější.

## <a name="write-and-place-the-indexhtm-file"></a>Zápis a umístěte soubor index.htm

Nejdříve vytvoříme soubor HTML, který budeme používat jako obsah webu.

V kořenové složce, vytvořte složku s názvem `test`.

V textovém editoru zadejte následující text:

```html
<head></head>
<body>
<p>Hello World!</p>
</body>
```

Uložit jako `index.htm` v `test` složky, které jste vytvořili dříve. 

## <a name="write-the-configuration"></a>Zápis konfigurace

A [konfigurace DSC](configurations.md) je speciální funkce prostředí PowerShell, která definuje, jak chcete nakonfigurovat jeden nebo více cílových počítačů (uzlů).

V integrovaném Skriptovacím prostředí PowerShell zadejte následující příkaz:

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

Uvidíte, že to vypadá funkce prostředí PowerShell, a uveďte klíčové slovo **konfigurace** používali před název funkce.

**Uzlu** bloku Určuje cílový uzel potřeba nakonfigurovat v tomto případě `localhost`.

Konfigurace volá dva [prostředky](resources.md), [WindowsFeature](windowsFeatureResource.md) a [soubor](fileResource.md).
Prostředky udělají tuto práci zajistit, který cílový uzel je ve stavu definované v konfiguraci.

## <a name="compile-the-configuration"></a>Konfigurace kompilace

Pro konfiguraci DSC, kterou chcete použít k uzlu je nutné nejprve být zkompilován do souboru MOF.
K tomu spusťte konfigurace jako funkce.
V konzole Powershellu přejděte do stejné složky, kam jste uložili konfiguraci a spusťte následující příkazy ke kompilaci konfigurace do souboru MOF:

```powershell
. .\WebsiteTest.ps1
WebsiteTest
```

To vygeneruje následující výstup:

```
Directory: C:\ConfigurationTest\WebsiteTest


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/13/2017   5:20 PM           2746 localhost.mof
```

První řádek zpřístupní funkce konfigurace v konzole.
Druhý řádek se spustí v konfiguraci.
Výsledkem je, že novou složku s názvem `WebsiteTest` je vytvořen jako podsložkou aktuální složky.
`WebsiteTest` Složka obsahuje soubor s názvem `localhost.mof`.
Je tento soubor, který lze použít na cílový uzel.

## <a name="apply-the-configuration"></a>Použít konfiguraci

Teď, když máte kompilované MOF, můžete použít konfiguraci na cílovém uzlu (v tomto případě místní počítač) pomocí volání [Start-DscConfiguration](/reference/5.1/PSDesiredStateConfiguration/Start-DscConfiguration) rutiny.

`Start-DscConfiguration` Rutiny informuje [místní Configuration Manager (LCM)](metaConfig.md), což je modul DSC, můžete použít konfiguraci.
LCM funguje volání prostředky DSC můžete použít konfiguraci.

V konzole Powershellu přejděte do stejné složky, kam jste uložili konfiguraci a spusťte následující příkaz:

```powershell
Start-DscConfiguration .\WebsiteTest
```

## <a name="test-the-configuration"></a>Otestujte konfiguraci

Můžete volat [Get-DscConfigurationStatus](/reference/5.1/PSDesiredStateConfiguration/Get-DscConfigurationStatus) rutiny zobrazíte, jestli konfigurace byla úspěšná. 

Můžete také otestovat výsledky přímo, v takovém případě procházením `http://localhost/` ve webovém prohlížeči.
Měli byste vidět "Hello, World" HTML stránka, kterou jste vytvořili jako první krok v tomto příkladu.

## <a name="next-steps"></a>Další kroky

- Další informace o konfiguracích DSC v [konfigurace DSC](configurations.md).
- Jaké prostředky DSC jsou k dispozici a jak vytvořit vlastní prostředky DSC v [prostředky DSC](resources.md).
- Najít konfigurace DSC a prostředky v [Galerie prostředí PowerShell](https://www.powershellgallery.com/).



