---
ms.date: 06/12/2017
contributor: JKeithB
keywords: Galerie prostředí powershell, rutina, psgallery
title: Začínáme s Galerie prostředí PowerShell
ms.openlocfilehash: c8beba3009e462ce52cdecd34fc0313d9234f289
ms.sourcegitcommit: 1082b13115c5c5be4b76574ba55307b3e567983f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/28/2018
ms.locfileid: "52576885"
---
# <a name="getting-started-with-the-powershell-gallery"></a>Začínáme s Galerie prostředí PowerShell

Galerie prostředí PowerShell je úložiště balíčků, který obsahuje skripty, moduly a prostředky DSC můžete stáhnout a využít. Pomocí rutin v [PowerShellGet](/powershell/module/powershellget) modulu k instalaci balíčků z Galerie prostředí PowerShell. Není nutné se přihlásit ke stažení položek z Galerie prostředí PowerShell.

> [!NOTE]
> Je možné stáhnout balíček přímo z Galerie prostředí PowerShell, ale toto není doporučený postup.
> Další podrobnosti najdete v tématu [ruční stažení balíčku](/powershell/gallery/how-to/working-with-packages/manual-download).

## <a name="discovering-packages-from-the-powershell-gallery"></a>Vyhledávání balíčků z Galerie prostředí PowerShell

Balíčky můžete najít v galerii prostředí PowerShell pomocí **hledání** ovládací prvek v galerii prostředí PowerShell [domovskou stránku](https://www.powershellgallery.com), nebo že si projdete moduly a skripty z [balíčky stránky ](https://www.powershellgallery.com/packages). Můžete také vyhledat balíčky z Galerie prostředí PowerShell spuštěním [Find-Module][], [Find-DscResource], a [Find-Script][] rutin, v závislosti na typu balíčku s `-Repository PSGallery`.

Můžete filtrovat výsledky z galerie s použitím následujících parametrů:

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

## <a name="learning-about-packages-in-the-powershell-gallery"></a>Získání informací o balíčky v galerii prostředí PowerShell

Jakmile identifikujete balíček, který vás zajímá, můžete další informace o něm. Můžete to provést tím, že kontroluje konkrétní stránka tento balíček v galerii. Na této stránce budete moct zobrazit všechny metadat nahraje spolu s balíčkem. Tato metadata pochází od autora balíčku a není ověřená společností Microsoft. Vlastník balíčku se silnou vazbu na galerii účet použitý k publikování balíčku a důvěryhodný více než pole Author.

Pokud zjistíte, že balíček, který máte pocit, že není publikována v dobré víře, klikněte na tlačítko **ohlášení zneužití** na stránce tento balíček.

Pokud používáte [Find-Module][] nebo [Find-Script][], zobrazí se tato data v vráceného objektu PSGetModuleInfo. Například systém `Find-Module -Name PSReadLine -Repository PSGallery |Get-Member`
Vrátí data o PSReadLine modulu v galerii.

## <a name="downloading-packages-from-the-powershell-gallery"></a>Stahování balíčků z Galerie prostředí PowerShell

Při stahování balíčků z Galerie prostředí PowerShell doporučujeme následující postup:

### <a name="inspect"></a>Kontrola

Stáhnout balíček z Galerie pro kontrolu, spusťte [Save-Module][] nebo [Save-Script][] rutiny, v závislosti na typu balíčku. Díky tomu můžete balíček uložit místně bez nutnosti jeho instalace a zkontrolovat obsah balíčku. Nezapomeňte si uložený balíček odstranit ručně.

Některé tyto balíčky jsou vytvořené microsoftem a jiné jsou vytvořené komunitou prostředí PowerShell.
Společnost Microsoft doporučuje, abyste si obsah a kód balíčky v této galerii před instalací.

Pokud zjistíte, že balíček, který máte pocit, že není publikována v dobré víře, klikněte na tlačítko **ohlášení zneužití** na stránce tento balíček.

### <a name="install"></a>Install

Chcete-li nainstalovat balíček z Galerie pro použití, spusťte [Install-Module][] nebo [Install-Script][] rutiny, v závislosti na typu balíčku.

[Install-Module][] nainstaluje modul `$env:ProgramFiles\WindowsPowerShell\Modules` ve výchozím nastavení.
To vyžaduje účet správce. Pokud chcete přidat `-Scope CurrentUser` parametr, je nainstalován modul `$env:USERPROFILE\Documents\WindowsPowerShell\Modules` .

[Install-Script][] skript, který nainstaluje `$env:ProgramFiles\WindowsPowerShell\Scripts` ve výchozím nastavení.
To vyžaduje účet správce. Pokud chcete přidat `-Scope CurrentUser` parametr, skript se nainstaluje do `$env:USERPROFILE\Documents\WindowsPowerShell\Scripts` .

Ve výchozím nastavení [Install-Module][] a [Install-Script][] nainstaluje nejnovější verzi balíčku.
Chcete-li nainstalovat starší verzi balíčku, přidejte `-RequiredVersion` parametru.

### <a name="deploy"></a>Nasazení

Chcete-li nasadit balíček z Galerie prostředí PowerShell pro Azure Automation, klikněte na tlačítko **Azure Automation**, klikněte na **nasadit do Azure Automation** na stránce s podrobnostmi balíčku. Budete přesměrováni na portálu pro správu Azure, ve kterém se přihlásíte pomocí přihlašovacích údajů k účtu Azure. Všimněte si, že nasazení balíčků se závislostmi všechny závislosti nasadí do služby Azure Automation. Tlačítko 'Nasazení do služby Azure Automation' můžete zakázat přidáním **AzureAutomationNotSupported** značka, které vaše metadata balíčku.

Další informace o Azure Automation najdete v tématu [Azure Automation](/azure/automation) dokumentaci.

## <a name="updating-packages-from-the-powershell-gallery"></a>Aktualizace balíčků z Galerie prostředí PowerShell

Pokud chcete aktualizovat balíčky nainstalované z Galerie prostředí PowerShell, spusťte rutiny [Update-skriptu] [] nebo [[Update-Module]]. Při spuštění bez žádné další parametry, [[Update-Module]] pokusí aktualizovat všechny moduly nainstalované spuštěním [Install-Module][]. Pokud chcete selektivně aktualizovat moduly, přidejte `-Name` parametru. 

Podobně při spuštění bez žádné další parametry, [] [-skript pro aktualizaci] taky automatický pokus o aktualizaci nainstalovat spuštěním všechny skripty [Install-Script][]. Pokud chcete selektivně aktualizovat skripty, přidejte `-Name` parametru.

## <a name="list-packages-that-you-have-installed-from-the-powershell-gallery"></a>Seznam balíčků, které jste nainstalovali z Galerie prostředí PowerShell

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
