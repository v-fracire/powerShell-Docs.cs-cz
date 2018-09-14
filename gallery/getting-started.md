---
ms.date: 06/12/2017
contributor: JKeithB
keywords: Galerie prostředí powershell, rutina, psgallery
title: Začínáme s Galerie prostředí PowerShell
ms.openlocfilehash: 39998df1a2bf9363dd008dc96a802157c8d691d7
ms.sourcegitcommit: e46b868f56f359909ff7c8230b1d1770935cce0e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/13/2018
ms.locfileid: "45523025"
---
# <a name="get-started-with-the-powershell-gallery"></a>Začínáme s Galerie prostředí PowerShell

Správný způsob, jak nainstalovat položky z Galerie prostředí PowerShell je mohli používat rutiny v [PowerShellGet](/powershell/module/powershellget) modulu. Není nutné se přihlásit ke stažení položek z Galerie prostředí PowerShell.

> [!NOTE]
> Je možné stáhnout balíček přímo z Galerie prostředí PowerShell, ale toto není doporučený postup. Další podrobnosti najdete v tématu [ruční stažení balíčku](https://msdn.microsoft.com/en-us/powershell/gallery/psgallery/how-to/working-with-items/manual-download.md).  


## <a name="discovering-items-from-the-powershell-gallery"></a>Zjišťují se položky z Galerie prostředí PowerShell

Položky v galerii prostředí PowerShell můžete najít pomocí **hledání** ovládacího prvku na tomto webu, nebo tak, že přejdete na stránkách moduly a skripty. Můžete také najít položky z Galerie prostředí PowerShell spuštěním [Find-Module][] a [Find-Script][] rutin, v závislosti na typu položky s `-Repository PSGallery`.

Filtrování výsledků z galerie můžete provést pomocí následujících parametrů:

- Název
- AllVersions
- MinimumVersion
- RequiredVersion
- Značka
- Zahrnuje
- DscResource
- RoleCapability
- Příkaz
- Filtr

Pokud máte zájem zjišťování konkrétní prostředky DSC v galerii, můžete spustit [Find-DscResource] rutiny. Find-DscResource vrací data na prostředky DSC obsažené v galerii.
Protože prostředky DSC se vždy dodávají jako součást modulu, je stále potřeba spustit [Install-Module][] nainstalovat tyto prostředky DSC.

## <a name="learning-about-items-in-the-powershell-gallery"></a>Získání informací o položky v galerii prostředí PowerShell

Jakmile identifikujete položky, které vás zajímá, můžete další informace o něm. Můžete to provést tím, že kontroluje konkrétní stránka danou položku v galerii. Na této stránce budete moct Zobrazit vše se odeslaly s položku metadat. Tato metadata pro položku, kterou autorem položky, není ověřená společností Microsoft. Vlastník položky se silnou vazbu na galerii účet použitý k publikování položky a důvěryhodný více než pole Author.

Pokud zjistíte, že položka, která máte pocit, že není publikována v dobré víře, klikněte na tlačítko **ohlášení zneužití** na stránce danou položku.

Pokud používáte [Find-Module][] nebo [Find-Script][], zobrazí se tato data v vráceného objektu PSGetModuleInfo. Například systém `Find-Module -Name PSReadLine -Repository PSGallery |Get-Member`
Vrátí data o PSReadLine modulu v galerii.

## <a name="downloading-items-from-the-powershell-gallery"></a>Stažení položek z Galerie prostředí PowerShell

Při stažení položek z Galerie prostředí PowerShell doporučujeme následující postup:

### <a name="inspect"></a>Kontrola

Stahování položky z Galerie pro kontrolu, spusťte [Save-Module][] nebo [Save-Script][] rutiny, v závislosti na typu položky. To vám umožní uložit položku místně bez nutnosti jeho instalace a zkontrolovat obsah položky. Mějte na paměti uložené položky odstraňte ručně.

Některé z těchto položek jsou vytvořené microsoftem a jiné jsou vytvořené komunitou prostředí PowerShell.
Společnost Microsoft doporučuje, abyste si obsah a kód položek v této galerii před instalací.

Pokud zjistíte, že položka, která máte pocit, že není publikována v dobré víře, klikněte na tlačítko **ohlášení zneužití** na stránce danou položku.

### <a name="install"></a>Install

Pokud chcete nainstalovat položky z Galerie pro použití, spusťte [Install-Module][] nebo [Install-Script][] rutiny, v závislosti na typu položky.

[Install-Module][] nainstaluje modul `$env:ProgramFiles\WindowsPowerShell\Modules` ve výchozím nastavení.
To vyžaduje účet správce. Pokud chcete přidat `-Scope CurrentUser` parametr, je nainstalován modul `$env:USERPROFILE\Documents\WindowsPowerShell\Modules` .

[Install-Script][] skript, který nainstaluje `$env:ProgramFiles\WindowsPowerShell\Scripts` ve výchozím nastavení.
To vyžaduje účet správce. Pokud chcete přidat `-Scope CurrentUser` parametr, skript se nainstaluje do `$env:USERPROFILE\Documents\WindowsPowerShell\Scripts` .

Ve výchozím nastavení [Install-Module][] a [Install-Script][] nainstaluje nejnovější verzi položky.
Chcete-li nainstalovat starší verzi položky, přidejte `-RequiredVersion` parametru.

### <a name="deploy"></a>Nasazení

Pokud chcete nasadit položky z Galerie prostředí PowerShell pro Azure Automation, klikněte na tlačítko **nasadit do Azure Automation** na stránce s podrobnostmi položky. Budete přesměrováni na portál pro správu Azure, ve kterém se přihlásíte pomocí přihlašovacích údajů k účtu Azure. Všimněte si, že nasazení položky se závislostmi nasadí všechny závislosti na službě Azure Automation. Tlačítko 'Nasazení do služby Azure Automation' můžete zakázat přidáním **AzureAutomationNotSupported** značka, které vaše metadata položky.

Další informace o Azure Automation najdete v tématu [Azure Automation](/azure/automation) dokumentaci.

## <a name="updating-items-from-the-powershell-gallery"></a>Aktualizace položky z Galerie prostředí PowerShell

Pokud chcete aktualizovat položky v galerii prostředí PowerShell nainstalovali, spusťte rutiny [Update-skriptu] [] nebo [[Update-Module]]. Po spuštění bez žádné další parametry []. [Update-Module] pokusí aktualizovat každý modul nainstalovat spuštěním [Install-Module][]. Pokud chcete selektivně aktualizovat moduly, přidejte `-Name` parametru.

Podobně při spuštění bez žádné další parametry, [[Update-skriptu]] taky automatický pokus o aktualizaci každý skript instalaci spuštěním [Install-Script][]. Pokud chcete selektivně aktualizovat skripty, přidejte `-Name` parametru.

## <a name="list-items-that-you-have-installed-from-the-powershell-gallery"></a>Seznam položek, které jste nainstalovali z Galerie prostředí PowerShell

Chcete-li zjistit, které moduly, které jste nainstalovali z Galerie prostředí PowerShell, spusťte [Get-InstalledModule][] rutiny. Tento příkaz vypíše všechny moduly, které máte ve vašem systému, které byly nainstalovány přímo z Galerie prostředí PowerShell.

Podobně, chcete-li zjistit, které skripty, které jste nainstalovali z Galerie prostředí PowerShell, spusťte [Get-InstalledScript][] rutiny. Tento příkaz vypíše všechny skripty, které máte ve vašem systému, které byly nainstalovány přímo z Galerie prostředí PowerShell.

[Find-DscResource]: /powershell/module/powershellget/Find-DscResource
[Find-Module]: /powershell/module/powershellget/Find-Module
[Find-Script]: /powershell/module/powershellget/Find-Script
[Get-InstalledModule]: /powershell/module/powershellget/Get-InstalledModule
[Get-InstalledScript]: /powershell/module/powershellget/Get-InstalledScript
[Install-Module]: /powershell/module/powershellget/Install-Module
[Install-Script]: /powershell/module/powershellget/Install-Script
[Publish-Module]: /powershell/module/powershellget/Publish-Module
[Publish-Script]: /powershell/module/powershellget/Publish-Script
[Register-PSRepository]: /powershell/module/powershellget/Register-Repository
[Save-Module]: /powershell/module/powershellget/Save-Module
[Save-Script]: /powershell/module/powershellget/Save-Script