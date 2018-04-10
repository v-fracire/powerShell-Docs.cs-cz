---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Vytvoření powershellové karty v prostředí Windows PowerShell ISE
ms.assetid: c10c18c7-9ece-4fd0-83dc-a19c53d4fd83
ms.openlocfilehash: 4d4388d889f2178b2cd24cb0f3350aee37327625
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="how-to-create-a-powershell-tab-in-windows-powershell-ise"></a>Vytvoření powershellové karty v prostředí Windows PowerShell ISE

Karty v Windows PowerShell Integrované skriptovací prostředí (ISE) umožňují najednou vytvořit a použít více prostředích spuštění v rámci stejné aplikaci.
Každé kartě prostředí PowerShell odpovídá prostředí pro spuštění samostatné nebo relace.

> **POZNÁMKA:**:
>
> Proměnné, funkce a aliasy, které vytvoříte v jedné karty se nepřenesou do jiné. Jsou různé relace prostředí Windows PowerShell.

Pomocí následujících kroků spustit nebo zavřít karty v prostředí Windows PowerShell.
Chcete-li přejmenovat na kartě, nastavte [DisplayName](The-PowerShellTab-Object.md#displayname) vlastnost u objektu skriptování, karta Windows PowerShell.

## <a name="to-create-and-use-a-new-powershell-tab"></a>Vytváření a používání novou kartu prostředí PowerShell

Na **souboru** nabídky, klikněte na **novou kartu prostředí PowerShell**. Na nové kartě prostředí PowerShell se vždy otevře jako aktivní okno.
Prostředí PowerShell karty jsou číslované postupně v pořadí, že jsou otevřené.
Každé kartě souvisí s její vlastní konzole okno prostředí Windows PowerShell.
Může mít až 32 karet prostředí PowerShell s vlastní relaci otevřené v čase (to je omezené na 8 v prostředí Windows PowerShell ISE 2.0.)

Všimněte si, že kliknete **nový** nebo **otevřete** ikon na panelu nástrojů nevytvoří novou kartu s samostatných relací.
Místo toho těchto tlačítek otevřete soubor skriptu nový nebo existující na kartě aktuálně aktivní s relací.
Můžete mít více skript, který otevřít soubory s každou kartu a relace.
Skript karty pro relaci se zobrazí pouze pod karty relace při aktivním přidružená relace.

Aktivujte na kartě prostředí PowerShell, klikněte na kartu. A vyberte všechny karty prostředí PowerShell, které jsou otevřené a na **zobrazení** nabídky, klikněte na kartu prostředí PowerShell, kterou chcete použít.

## <a name="to-create-and-use-a-new-remote-powershell-tab"></a>Vytváření a používání novou kartu vzdáleného prostředí PowerShell

Na **soubor** nabídky, klikněte na tlačítko **novou kartu vzdáleného prostředí PowerShell** k vytvoření relace na vzdáleném počítači.
Dialogové okno se zobrazí a výzvu k zadání podrobností nutný k vytvoření vzdáleného připojení.
Karty vzdálený funguje stejně jako místní kartě prostředí PowerShell, ale příkazy a skripty se spouštějí ve vzdáleném počítači.

## <a name="to-close-a-powershell-tab"></a>Zavřete kartu prostředí PowerShell

Na kartě zavřete, můžete použít některý z následujících postupů:

- Klikněte na kartu, která chcete zavřít.

- Na **soubor** nabídky, klikněte na tlačítko **zavřete kartu prostředí PowerShell**, nebo klikněte na tlačítko Zavřít (**X**) active karty zavřete kartu.

Pokud máte neuložené otevřete soubory na kartě prostředí PowerShell, že chcete zavřít, zobrazí se výzva k uložte nebo zahoďte je.
Další informace o tom, jak uložit skript najdete v tématu [postup uložit skript](How-to-Write-and-Run-Scripts-in-the-Windows-PowerShell-ISE.md#how-to-save-a-script).

## <a name="see-also"></a>Viz také

- [Představení Windows PowerShell ISE](Introducing-the-Windows-PowerShell-ISE.md)
- [Jak používat podokně konzoly v systému Windows PowerShell ISE](How-to-Use-the-Console-Pane-in-the-Windows-PowerShell-ISE.md)