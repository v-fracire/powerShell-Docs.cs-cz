---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Vytvoření powershellové karty v prostředí Windows PowerShell ISE
ms.assetid: c10c18c7-9ece-4fd0-83dc-a19c53d4fd83
ms.openlocfilehash: 080fe89bf1443f51460589b445431913fa20b4b8
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403662"
---
# <a name="how-to-create-a-powershell-tab-in-windows-powershell-ise"></a>Vytvoření powershellové karty v prostředí Windows PowerShell ISE

Karty v Windows Powershellu integrovaném skriptovacím prostředí (ISE) umožňují najednou vytvořit a použít několik prostředí provádění v rámci stejné aplikace.
Každá karta Powershellu odpovídá samostatné spouštěcí prostředí nebo relace.

> [!NOTE]
> Proměnné, funkce a aliasy, které vytvoříte v jedné karty se nepřenesou do jiné. Jsou různé relace Windows Powershellu.

Otevřít nebo zavřít karty v prostředí Windows PowerShell použijte následující postup.
Chcete-li přejmenovat kartu, nastavte [DisplayName](object-model/The-PowerShellTab-Object.md#displayname) vlastnost v objektu skriptu Windows PowerShell Tab.

## <a name="to-create-and-use-a-new-powershell-tab"></a>Jak vytvořit a používat na nové kartě prostředí PowerShell

Na **souboru** nabídky, klikněte na tlačítko **nový PowerShell Tab**. Vždy otevře se nová karta prostředí PowerShell jako aktivní okno.
Karty Powershellu jsou číslovány postupně v pořadí, že jsou otevřené.
Každá karta souvisí s vlastní okna konzoly Windows Powershellu.
Můžete mít až 32 karty Powershellu s vlastní relace, otevřete v čase (to je omezené na 8 na Windows PowerShell ISE 2.0.)

Všimněte si, že kliknete na **nový** nebo **otevřít** ikon na panelu nástrojů nevytvoří novou kartu samostatné relaci.
Místo toho těchto tlačítek otevření souboru nového nebo existujícího skriptu na kartě aktuálně aktivní relaci.
Můžete mít více skriptu, který otevření souborů s každou kartu a relace.
Karty skript pro relaci se zobrazí pouze pod karty relace při aktivním přidružená relace.

Abyste aktivovali Powershellové karty, klikněte na kartu. Můžete vybírat z všechny karty Powershellu, které jsou otevřeny v **zobrazení** nabídky, klikněte na kartu prostředí PowerShell, kterou chcete použít.

## <a name="to-create-and-use-a-new-remote-powershell-tab"></a>Jak vytvořit a používat na nové kartě vzdáleného prostředí PowerShell

Na **souboru** nabídky, klikněte na tlačítko **nové karty vzdálený PowerShell** k vytvoření relace na vzdáleném počítači.
Dialogové okno se zobrazí a zobrazí výzvu k zadání podrobností, které jsou potřebné k navázání vzdáleného připojení.
Kartě Vzdálená funguje stejně jako místní Powershellové karty, ale příkazy a skripty se spouštějí na vzdáleném počítači.

## <a name="to-close-a-powershell-tab"></a>Zavřete kartu prostředí PowerShell

Zavřete kartu, můžete použít některý z následujících postupů:

- Klikněte na kartu, kterou chcete zavřít.

- Na **souboru** nabídky, klikněte na tlačítko **zavřete PowerShell Tab**, nebo kliknutím na tlačítko Zavřít (**X**) na aktivní kartě kartu zavřete.

Pokud máte neuložené soubory otevřít v PowerShell tab, že chcete zavřít, zobrazí se výzva k ukládání nebo zahazování je.
Další informace o tom, jak uložit skript najdete v tématu [jak uložit skript](How-to-Write-and-Run-Scripts-in-the-Windows-PowerShell-ISE.md#how-to-save-a-script).

## <a name="see-also"></a>Viz také

- [Představení Windows PowerShell ISE](Introducing-the-Windows-PowerShell-ISE.md)
- [Použití Pokokna konzoly v prostředí Windows PowerShell ISE](How-to-Use-the-Console-Pane-in-the-Windows-PowerShell-ISE.md)