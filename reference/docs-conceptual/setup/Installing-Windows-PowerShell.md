---
ms.date: 08/09/2017
keywords: prostředí PowerShell, rutina, stažení, instalace, instalační program, windows 10, windows 8.1, windows 8.0, windows 7
title: Instalace Windows PowerShellu
ms.openlocfilehash: e703d3444b1d661c482b314781cf9a1cb16ef7ed
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893517"
---
# <a name="installing-windows-powershell"></a>Instalace Windows PowerShellu

Prostředí Windows PowerShell je nainstalovaný ve výchozím nastavení v každé Windows od verze Windows 7 SP1 a Windows Server 2008 R2 SP1.

Pokud vás zajímá, v Powershellu 6 nebo novější, musíte nainstalovat PowerShell Core místo prostředí Windows PowerShell. K tomu najdete v článku [instalace Powershellu Core ve Windows](Installing-PowerShell-Core-on-Windows.md).

## <a name="finding-powershell-in-windows-10-81-80-and-7"></a>Hledání prostředí PowerShell v systému Windows 10, 8.1, 8.0 a 7

Někdy vyhledání prostředí PowerShell konzoly nebo ISE (Integrované skriptovací prostředí) ve Windows může být obtížné, protože poloha nalezeného přesune z jedné verze Windows na další.

Následující tabulky by vám pomoct najít prostředí PowerShell ve vaší verzi Windows.
Všechny verze, tady jsou původní verze vydané s žádné aktualizace.

### <a name="for-console"></a>Pro konzolu

Verze | Umístění
-- | --
Windows 10 | Klikněte na levý nižší rohová ikona Windows, začněte psát prostředí PowerShell
Windows 8.1, 8.0 | Na úvodní obrazovce začněte psát, prostředí PowerShell.<br/>Pokud na pracovní ploše, klikněte na levý nižší rohová ikona Windows, začněte psát prostředí PowerShell
Windows 7 SP1 | Klikněte na levý nižší rohu Windows ikonu, v nabídce start pole hledání zadáte prostředí PowerShell

### <a name="for-ise"></a>ISE

Verze | Umístění
-- | --
Windows 10 | Klikněte na levý nižší rohová ikona Windows, začněte psát ISE
Windows 8.1, 8.0 | Na úvodní obrazovce zadejte **prostředí PowerShell ISE**.<br/>Pokud je na ploše, klikněte na levý nižší rohová ikona Windows, zadejte **prostředí PowerShell ISE**
Windows 7 SP1 | Klikněte na levý nižší rohu Windows ikonu, v nabídce start pole hledání zadáte prostředí PowerShell

## <a name="finding-powershell-in-windows-server-versions"></a>Hledání prostředí PowerShell v systému Windows Server

Od verze Windows Server 2008 R2, je nainstalovat operační systém Windows bez grafického uživatelského rozhraní (GUI).
Edice Windows serveru bez grafického uživatelského rozhraní jsou pojmenovány **Core** edice a edice pomocí grafického uživatelského rozhraní jsou pojmenovány **Desktop**.

### <a name="windows-server-core-editions"></a>Edice systému Windows Server Core

Ve všech edicích Core když se připojujete k serveru získat okno příkazového řádku Windows.

Typ `powershell` a stiskněte klávesu **ENTER** spuštění prostředí PowerShell v relaci příkazového řádku.
Typ `exit` ukončit relaci Powershellu a návrat na příkazovém řádku.

### <a name="windows-server-desktop-editions"></a>Edice Windows serveru Desktop

Ve všech edicích klasické pracovní plochy klikněte na ikonu Windows levém dolním rohu, začněte psát prostředí PowerShell.
Získáte konzoly a možnosti ISE.

Jedinou výjimkou z výše uvedeného pravidla je ISE v systému Windows Server 2008 R2 SP1; v tomto případě klikněte na ikonu Windows levém dolním rohu, zadejte ISE Powershellu.

## <a name="how-to-check-the-version-of-powershell"></a>Návod k ověření verze prostředí PowerShell

Pokud chcete zjistit, kterou verzi Powershellu jste nainstalovali, spusťte konzolu Powershellu (nebo ISE) a typ `$PSVersionTable` a stiskněte klávesu **ENTER**. Hledat `PSVersion` hodnotu.

## <a name="upgrading-existing-windows-powershell"></a>Upgrade stávající prostředí Windows PowerShell

Instalační balíček pro prostředí PowerShell se dodává v instalační program, který WMF.
Verze instalačního programu WMF odpovídá verzi prostředí PowerShell; neexistuje žádný samostatný instalační program pro prostředí Windows PowerShell.

Pokud je potřeba aktualizovat stávající verzi prostředí PowerShell, ve Windows, použijte v následující tabulce vyhledejte instalační program pro verzi prostředí PowerShell, které chcete aktualizovat.

Windows | PS 3.0 | PS 4.0 | PS 5.0 | PS 5.1 |
--|--|--|--|--|
Windows 10 (viz Note1)<br/>Windows Server 2016 | - | - | - | nainstalovat
Windows 8.1<br/>Windows Server 2012 R2 | - | nainstalovat | [WMF 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) | [WMF 5.1](https://www.microsoft.com/en-us/download/details.aspx?id=54616)
Windows 8<br/>Windows Server 2012 | nainstalovat | [WMF 4.0](https://www.microsoft.com/en-us/download/details.aspx?id=40855) | [WMF 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) | [WMF 5.1](https://www.microsoft.com/en-us/download/details.aspx?id=54616)
Windows 7 SP1<br/>Windows Server 2008 R2 SP1 | [WMF 3.0](https://www.microsoft.com/en-us/download/details.aspx?id=34595) | [WMF 4.0](https://www.microsoft.com/en-us/download/details.aspx?id=40855) | [WMF 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) | [WMF 5.1](https://www.microsoft.com/en-us/download/details.aspx?id=54616)

> [!NOTE]
>
> V počáteční verzi systému Windows 10 pomocí funkce Automatické aktualizace povolena prostředí PowerShell se aktualizuje z verze 5.0 k 5.1.
>
> Pokud původní verzi Windows 10 není aktualizován prostřednictvím aktualizací Windows, je verze Powershellu 5.0.

## <a name="need-azure-powershell"></a>Potřebujete prostředí Azure PowerShell

Pokud hledáte **prostředí Azure PowerShell**, můžete začít s [Přehled prostředí Azure PowerShell](/powershell/azure/overview).

V opačném případě je třeba co [instalace a konfigurace Azure Powershellu](/powershell/azure/install-azurerm-ps)

## <a name="see-also"></a>Viz také

[Požadavky na prostředí PowerShell systému Windows](Windows-PowerShell-System-Requirements.md)

[Spuštění Windows Powershellu](Starting-Windows-PowerShell.md)