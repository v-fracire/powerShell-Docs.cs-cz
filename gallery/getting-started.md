---
ms.date: 06/12/2017
contributor: JKeithB
ms.topic: conceptual
keywords: Galerie prostředí powershell, rutiny, psgallery
title: psgallery_gettingstarted
ms.openlocfilehash: c3aafe9e76eda9acdd4787f63dc0f8c71a20d02a
ms.sourcegitcommit: e9ad4d85fd7eb72fb5bc37f6ca3ae1282ae3c6d7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/10/2018
---
# <a name="get-started-with-the-powershell-gallery"></a>Začínáme s Galerie prostředí PowerShell

Stahování položky z Galerie prostředí PowerShell k vašemu systému vyžaduje [PowerShellGet](/powershell/module/powershellget) modulu. Modul PowerShellGet najdete v některém z následujících akcí. Není nutné se přihlásit ke stažení položky z Galerie prostředí PowerShell.

## <a name="discovering-items-from-the-powershell-gallery"></a>Zjišťování položky z Galerie Powershellu

Položky v galerii prostředí PowerShell můžete najít pomocí **vyhledávání** ovládacího prvku na tomto webu, nebo procházením prostřednictvím stránky moduly a skripty. Můžete také získat položky z Galerie Powershellu spuštěním [najít modul][] a [najít skriptu][] rutin, v závislosti na typu položky s `-Repository PSGallery`.

Filtrování výsledků z galerie lze provést pomocí následujících parametrů:

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

Pokud byste chtěli pouze konkrétní prostředky DSC v galerii zjišťování, můžete spustit [najít DscResource] rutiny. Najít DscResource vrací data na prostředky DSC obsažené v galerii.
Protože prostředky DSC jsou vždy dodávána jako součást modulu, potřebujete stále spustit [instalace modulu][] nainstalovat tyto prostředky DSC.

## <a name="learning-about-items-in-the-powershell-gallery"></a>Získávání informací o položky v galerii prostředí PowerShell

Jakmile jste zformulovali položky, které vás zajímají, můžete další informace o něm. To provedete tak, že prověří daná položka konkrétní stránky v galerii. Na této stránce budete moci zobrazit všechny metadat nahrán s položkou. Tato metadata položky od autora položky a není ověřen společností Microsoft. Vlastník položky je důrazně vázaný na Galerie účet použitý k publikování položku a více důvěryhodný než pole Author.

Pokud zjistíte, že položku, která si myslíte, že není publikována v dobré víře, klikněte na tlačítko **oznámení zneužití** na stránce této položky.

Pokud používáte [najít modul][] nebo [najít skriptu][], zobrazí se tato data v vráceného objektu PSGetModuleInfo. Například běžet `Find-Module -Name PSReadLine -Repository PSGallery |Get-Member` vrací data v modulu PSReadLine v galerii.

## <a name="downloading-items-from-the-powershell-gallery"></a>Při stahování položky z Galerie Powershellu

Při stahování položky z Galerie Powershellu doporučujeme následující proces:

### <a name="inspect"></a>Kontrola

Ke stažení položky z Galerie pro kontrolu, spusťte [uložit modulu][] nebo [uložit skript][] rutiny, v závislosti na typu položky. To vám umožní uložit položku místně bez nutnosti její instalace a zkontrolovat obsah položky. Mějte na paměti, odstraňte uložený položku ručně.

Některé z těchto položek vytvořené společností Microsoft a ostatní vytvořené komunitou prostředí PowerShell.
Společnost Microsoft doporučuje zkontrolovat obsah a kód položky v této galerii před instalací.

Pokud zjistíte, že položku, která si myslíte, že není publikována v dobré víře, klikněte na tlačítko **oznámení zneužití** na stránce této položky.

### <a name="install"></a>Install

Chcete-li nainstalovat položky z Galerie pro použití, spusťte [instalace modulu][] nebo [instalační skript][] rutiny, v závislosti na typu položky.

[instalace modulu][] nainstaluje modul pro `$env:ProgramFiles\WindowsPowerShell\Modules` ve výchozím nastavení.
To vyžaduje účet správce. Pokud přidáte `-Scope CurrentUser` parametru, je nainstalován modul `$env:USERPROFILE\Documents\WindowsPowerShell\Modules` .

[instalační skript][] nainstaluje skript, který chcete `$env:ProgramFiles\WindowsPowerShell\Scripts` ve výchozím nastavení.
To vyžaduje účet správce. Pokud přidáte `-Scope CurrentUser` parametr skript je nainstalován do `$env:USERPROFILE\Documents\WindowsPowerShell\Scripts` .

Ve výchozím nastavení [instalace modulu][] a [instalační skript][] nainstaluje nejnovější verzi položky.
Chcete-li nainstalovat starší verzi položky, přidejte `-RequiredVersion` parametr.

### <a name="deploy"></a>Nasazení

Chcete-li nasadit položky z Galerie prostředí PowerShell pro Azure Automation, klikněte na tlačítko **nasadit do Azure Automation** na stránce podrobností položky. Budete přesměrováni na portálu Azure Management Portal, kde se přihlásíte pomocí svých přihlašovacích údajů účtu Azure. Všimněte si, že nasazení položky se závislostmi nasadí všechny závislosti pro Azure Automation. Tlačítko "nasadit do Azure Automation, lze zakázat tak, že přidáte **AzureAutomationNotSupported** značku metadata položky.

Další informace o Azure Automation najdete v tématu [Azure Automation](/azure/automation) dokumentaci.

## <a name="updating-items-from-the-powershell-gallery"></a>Aktualizace položky z Galerie Powershellu

Pokud chcete aktualizovat položky nainstalovat z Galerie prostředí PowerShell, spusťte buď [] – [aktualizace-Module] nebo [skript aktualizace] [] rutiny. Když se spustí bez dalších parametrů, [] – [aktualizace-Module] pokusí aktualizovat každý modul nainstalovaný spuštěním [instalace modulu][]. Chcete-li selektivně aktualizovat moduly, přidejte `-Name` parametr.

Podobně když se spustí bez dalších parametrů, [] – [skript aktualizace] také pokusí aktualizovat každý skript nainstalovaná, spuštěním [instalační skript][]. Chcete-li selektivně aktualizovat skripty, přidejte `-Name` parametr.

## <a name="list-items-that-you-have-installed-from-the-powershell-gallery"></a>Seznam položek, které jste nainstalovali z Galerie Powershellu

Chcete-li zjistit, které moduly, které jste nainstalovali z Galerie prostředí PowerShell, spusťte [Get-InstalledModule][] rutiny. Tento příkaz vypíše všechny moduly, které máte ve vašem systému, které byly nainstalovány přímo z Galerie prostředí PowerShell.

Podobně, chcete-li zjistit, které skripty, které jste nainstalovali z Galerie prostředí PowerShell, spusťte [Get-InstalledScript][] rutiny. Tento příkaz vypíše všechny skripty, které máte ve vašem systému, které byly nainstalovány přímo z Galerie prostředí PowerShell.

[najít DscResource]: /powershell/module/powershellget/Find-DscResource
[najít modul]: /powershell/module/powershellget/Find-Module
[najít skriptu]: /powershell/module/powershellget/Find-Script
[Get-InstalledModule]: /powershell/module/powershellget/Get-InstalledModule
[Get-InstalledScript]: /powershell/module/powershellget/Get-InstalledScript
[instalace modulu]: /powershell/module/powershellget/Install-Module
[instalační skript]: /powershell/module/powershellget/Install-Script
[Publish-Module]: /powershell/module/powershellget/Publish-Module
[Publish-Script]: /powershell/module/powershellget/Publish-Script
[Register-PSRepository]: /powershell/module/powershellget/Register-Repository
[uložit modulu]: /powershell/module/powershellget/Save-Module
[uložit skript]: /powershell/module/powershellget/Save-Script