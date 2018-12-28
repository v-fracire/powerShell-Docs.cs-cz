---
ms.date: 12/12/2018
keywords: DSC, powershell, konfigurace, služby, instalační program
title: Psaní, kompilace a použití konfigurace
ms.openlocfilehash: fa4d98fd12202439ba7025fd8af3fa398653ca05
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403673"
---
> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

# <a name="write-compile-and-apply-a-configuration"></a>Psaní, kompilace a použití konfigurace

V tomto cvičení vás provedou vytvořením a aplikování konfigurace Desired State Configuration (DSC) od začátku do konce.
V následujícím příkladu se dozvíte, jak napsat a použít velmi jednoduchou konfiguraci. Konfigurace se ujistěte se, že "HelloWorld.txt" soubor existuje na místním počítači. Při odstranění souboru, DSC se jej znovu vytvořit při příštím aktualizuje.

Přehled o novinkách DSC a jak to funguje, najdete v části [Desired State Configuration přehled pro vývojáře](../overview/overview.md).

## <a name="requirements"></a>Požadavky

Chcete-li spustit tento příklad, musíte počítač se systémem Powershellu 4.0 nebo novější.

## <a name="write-the-configuration"></a>Zapsat konfiguraci

DSC [konfigurace](configurations.md) je speciální funkce prostředí PowerShell, který definuje, jak chcete nakonfigurovat jeden nebo více cílových počítačů (uzlů).

V prostředí PowerShell ISE, nebo jiném editoru prostředí PowerShell zadejte následující příkaz:

```powershell
Configuration HelloWorld {

    # Import the module that contains the File resource.
    Import-DscResource -ModuleName PsDesiredStateConfiguration

    # The Node statement specifies which targets to compile MOF files for, when this configuration is executed.
    Node 'localhost' {

        # The File resource can ensure the state of files, or copy them from a source to a destination with persistent updates.
        File HelloWorld {
            DestinationPath = "C:\Temp\HelloWorld.txt"
            Ensure = "Present"
            Contents   = "Hello World from DSC!"
        }
    }
}
```

Uložte soubor jako "HelloWorld.ps1".

Definování konfigurace je stejná jako definice funkce. **Uzel** bloku Určuje cílový uzel nakonfigurovat, v tomto případě `localhost`.

Konfigurace volá jedno [prostředky](../resources/resources.md), `File` prostředků. Prostředky vykonávají práci třeba zajistit, který cílový uzel je ve stavu, které jsou definované v konfiguraci.

## <a name="compile-the-configuration"></a>Kompilace konfigurace

Pro konfiguraci DSC, kterou chcete použít pro uzel je nutné nejprve být zkompilován do souboru MOF.
Spouštění konfigurace, jako je funkce, zkompiluje jeden soubor "MOF" pro každý uzel určené `Node` bloku.
Pokud chcete spustit konfiguraci, je potřeba *tečkou zdroj* "HelloWorld.ps1" skript do aktuálního oboru.
Další informace najdete v tématu [about_Scripts](/powershell/module/microsoft.powershell.core/about/about_scripts?view=powershell-6#script-scope-and-dot-sourcing).

*Zdroj tečkou* skriptu "HelloWorld.ps1" tak, že zadáte cestu, kam jste uložili, ho po `. ` (tečka, místo). Potom můžete spustit konfiguraci voláním jako funkce.

```powershell
. C:\Scripts\WebsiteTest.ps1
HelloWolrd
```

Tím se vygeneruje následující výstup:

```output
Directory: C:\Scripts\HelloWorld


Mode                LastWriteTime         Length Name
----                -------------         ------ ----
-a----        3/13/2017   5:20 PM           2746 localhost.mof
```

## <a name="apply-the-configuration"></a>Použít konfiguraci

Teď, když máte zkompilovaný soubor MOF, můžete provést konfiguraci na cílový uzel (v tomto případě místní počítač) pomocí volání [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) rutiny.

`Start-DscConfiguration` Říká rutiny [místní Configuration Manageru (LCM)](../managing-nodes/metaConfig.md), modulu DSC, chcete-li použít konfiguraci.
LCM provádí volání prostředky DSC můžete použít konfiguraci.

Použít níže uvedený kód ke spuštění `Start-DSCConfiguration` rutiny. Zadejte vaše "localhost.mof" se mají ukládat do cesta k adresáři `-Path` parametru. `Start-DSCConfiguration` Rutiny prohlédne do adresáře určeného pro všechny "\<computername\>.mof" soubory. `Start-DSCConfiguration` Rutina se pokusí použít každý soubor "MOF", které nalezne na název určený název souboru ("localhost", "server01", "dc-02" atd.).

> [!NOTE]
> Pokud `-Wait` parametr není zadán, `Start-DSCConfiguration` vytvoří úlohu na pozadí k provedení této operace. Zadání `-Verbose` parametr umožňuje sledovat **Verbose** výstupní operace. `-Wait`, a `-Verbose` jsou obě volitelné parametry.

```powershell
Start-DscConfiguration -Path C:\Scripts\HelloWorld -Verbose -Wait
```

## <a name="test-the-configuration"></a>Otestujte konfiguraci

Jakmile `Start-DSCConfiguration` dokončení rutiny, měli byste vidět soubor "HelloWorld.txt" v zadaném umístění. Můžete ověřit obsah s [Get-Content](/powershell/module/microsoft.powershell.management/get-content) rutiny.

Můžete také *testování* aktuální stav pomocí [Test-DSCConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration).

Výstup by měl "True", pokud uzel je nyní kompatibilní s použité konfigurace.

```powershell
Test-DSCConfiguration
```

```output
True
```

```powershell
Get-Content -Path C:\Temp\HelloWorld.txt
```

```output
Hello World from DSC!
```

## <a name="re-applying-the-configuration"></a>Opětovné použití konfigurace

Zobrazit konfiguraci znovu použije, můžete odebrat textový soubor vytvořil konfiguraci. Použití `Start-DSCConfiguration` rutinu s `-UseExisting` parametru. `-UseExisting` Nastaví parametr `Start-DSCConfiguration` znovu použít soubor "current.mof", která představuje naposledy úspěšně použili konfiguraci.

```powershell
Remove-Item -Path C:\Temp\HelloWorld.txt
```

## <a name="next-steps"></a>Další kroky

- Další informace o konfiguracích DSC na [konfigurací DSC](configurations.md).
- Podívejte se, jaké prostředky DSC jsou k dispozici a jak vytvořit vlastní prostředky DSC na [prostředky DSC](../resources/resources.md).
- Najděte prostředky v a konfigurace DSC [Galerie prostředí PowerShell](https://www.powershellgallery.com/).
