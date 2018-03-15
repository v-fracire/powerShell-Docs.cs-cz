---
ms.date: 2017-06-12
contributor: JKeithB
ms.topic: conceptual
keywords: "Galerie prostředí powershell, rutiny, psgallery"
title: psgallery_gettingstarted
ms.openlocfilehash: 2117712b0081db4a21f8480b458a499ed84dc512
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2018
---
# <a name="get-started-with-the-powershell-gallery"></a>Začínáme s Galerie prostředí PowerShell

## <a name="what-is-the-powershell-gallery"></a>Co je Galerie prostředí PowerShell?

Galerie prostředí PowerShell je centrálním úložištěm pro obsah prostředí PowerShell.
V něm můžete najít užitečné moduly Powershellu obsahující příkazy prostředí PowerShell a prostředky konfigurace požadovaného stavu (DSC). Můžete také získat skripty prostředí PowerShell, některé z nich může obsahovat pracovních postupů prostředí PowerShell a které popisují sadu úloh a zadejte sekvencování pro tyto úlohy.
Některé z těchto položek vytvořené společností Microsoft a ostatní vytvořené komunitou prostředí PowerShell.

## <a name="requirements"></a>Požadavky

Stahování položky z Galerie prostředí PowerShell k vašemu systému vyžaduje [PowerShellGet](http://go.microsoft.com/fwlink/?LinkID=760387&clcid=0x409) modulu. Modul PowerShellGet najdete v některém z následujících akcí. Není nutné se přihlásit ke stažení položky z Galerie prostředí PowerShell.

-   [Windows 10](http://go.microsoft.com/fwlink/?LinkID=624830&clcid=0x409)
-   [Windows Management Framework 5.0](http://go.microsoft.com/fwlink/?LinkId=398175)
-   [Instalační služba MSI (pro prostředí PowerShell, 3 a 4)](http://go.microsoft.com/fwlink/?LinkID=746217&clcid=0x409)

PowerShellGet taky vyžaduje [NuGet zprostředkovatele](http://go.microsoft.com/fwlink/?LinkId=722208) pro práci s Galerie prostředí PowerShell. Zobrazí se výzva k instalaci zprostředkovatele NuGet automaticky při prvním použití PowerShellGet, pokud poskytovatel NuGet není v jednom z následujících umístění:

- `$env:ProgramFiles\PackageManagement\ProviderAssemblies`
- `$env:LOCALAPPDATA\PackageManagement\ProviderAssemblies`

Nebo můžete spustit `Install-PackageProvider -Name NuGet -Force` k automatizaci stažení a instalaci zprostředkovatele NuGet.

  
Pokud máte na verzi, která je starší než 2.8.5.201 NuGet, musíte se k volání následující rutiny prostředí PowerShell k instalaci a přepněte na nejnovější verzi balíčku nuget.

1.  `Install-PackageProvider NuGet -MinimumVersion '2.8.5.201' -Force`
2.  `Import-PackageProvider NuGet -MinimumVersion '2.8.5.201' -Force`
3.  Odstraníte starší verze balíčku NuGet z výše uvedené umístění instalace.

Další informace najdete v tématu <http://oneget.org/> .

  
Poznámka: Z důvodu změn v balení formáty, doporučujeme, abyste že je aktualizovat na nejnovější verzi PowerShellGet a PackageManagement instalaci položek, které byly nedávno aktualizovány. PowerShellGet je součástí systému Windows 10, který se více o [zde](http://go.microsoft.com/fwlink/?LinkID=624830&clcid=0x409).
PowerShellGet je také součástí systému Windows Management Framework (WMF) 5.0, kterou si můžete stáhnout [zde](http://go.microsoft.com/fwlink/?LinkId=398175).

## <a name="discovering-items-from-the-powershell-gallery"></a>Zjišťování položky z Galerie Powershellu

Položky v galerii prostředí PowerShell můžete najít pomocí **vyhledávání** ovládacího prvku na tomto webu, nebo procházením prostřednictvím stránky moduly a skripty. Můžete také získat položky z Galerie Powershellu spuštěním [najít modul](https://go.microsoft.com/fwlink/?LinkId=821658) a [najít skriptu](https://go.microsoft.com/fwlink/?LinkId=822322) rutin, v závislosti na typu položky s `-Repository PSGallery`.

Filtrování výsledků z galerie lze provést pomocí následujících parametrů [najít modulu](https://go.microsoft.com/fwlink/?LinkId=821658) a [najít skriptu](https://go.microsoft.com/fwlink/?LinkId=822322)

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

Pokud byste chtěli pouze konkrétní prostředky DSC v galerii zjišťování, můžete spustit [najít DscResource](https://go.microsoft.com/fwlink/?LinkId=517196) rutiny.
[Najít DscResource](https://go.microsoft.com/fwlink/?LinkId=517196) vrací data na prostředky DSC obsažené v galerii. Protože prostředky DSC jsou vždy dodávána jako součást modulu, potřebujete stále spustit [instalace modulu](https://go.microsoft.com/fwlink/?LinkId=821663) nainstalovat tyto prostředky DSC.

## <a name="learning-about-items-in-the-powershell-gallery"></a>Získávání informací o položky v galerii prostředí PowerShell

Jakmile jste zformulovali položky, které vás zajímají, můžete další informace o něm. To provedete tak, že prověří daná položka konkrétní stránky v galerii. Na této stránce budete moci zobrazit všechny metadat nahrán s položkou. Tato metadata položky od autora položky a není ověřen společností Microsoft. Vlastník položky je důrazně vázaný na Galerie účet použitý k publikování položku a více důvěryhodný než pole Author.

Pokud zjistíte, že položku, která si myslíte, že není publikována v dobré víře, klikněte na tlačítko **oznámení zneužití** na stránce této položky.

Pokud používáte [najít modulu](https://go.microsoft.com/fwlink/?LinkId=821658) nebo [najít skriptu](https://go.microsoft.com/fwlink/?LinkId=822322), zobrazí se tato data v vráceného objektu PSGetModuleInfo.
Například běžet `Find-Module -Name PSReadLine -Repository PSGallery | Get-Member` vrací data v modulu PSReadLine v galerii.

## <a name="downloading-items-from-the-powershell-gallery"></a>Při stahování položky z Galerie Powershellu

Při stahování položky z Galerie Powershellu doporučujeme následující proces:

### <a name="inspect"></a>Kontrola

Ke stažení položky z Galerie pro kontrolu, spusťte [uložit modulu](https://go.microsoft.com/fwlink/?LinkId=821669) nebo [uložit skript](https://go.microsoft.com/fwlink/?LinkId=822334) rutiny, v závislosti na typu položky. To vám umožní uložit položku místně bez nutnosti její instalace a zkontrolovat obsah položky. Mějte na paměti, odstraňte uložený položku ručně.

Některé z těchto položek vytvořené společností Microsoft a ostatní vytvořené komunitou prostředí PowerShell. Společnost Microsoft doporučuje zkontrolovat obsah a kód položky v této galerii před instalací.

Pokud zjistíte, že položku, která si myslíte, že není publikována v dobré víře, klikněte na tlačítko **oznámení zneužití** na stránce této položky.

### <a name="install"></a>Install

Chcete-li nainstalovat položky z Galerie pro použití, spusťte [instalace modulu](https://go.microsoft.com/fwlink/?LinkId=821663) nebo [instalační skript](https://go.microsoft.com/fwlink/?LinkId=822327) rutiny, v závislosti na typu položky.

[Instalace modulu](https://go.microsoft.com/fwlink/?LinkId=821663) nainstaluje modul pro `$env:ProgramFiles\WindowsPowerShell\Modules` ve výchozím nastavení. To vyžaduje účet správce. Pokud přidáte `-Scope
CurrentUser` parametru, je nainstalován modul `$env:USERPROFILE\Documents\WindowsPowerShell\Modules` .

[Instalační skript](https://go.microsoft.com/fwlink/?LinkId=822327) nainstaluje skript, který chcete `$env:ProgramFiles\WindowsPowerShell\Scripts` ve výchozím nastavení. To vyžaduje účet správce. Pokud přidáte `-Scope
CurrentUser` parametr skript je nainstalován do `$env:USERPROFILE\Documents\WindowsPowerShell\Scripts` .

Ve výchozím nastavení [instalace modulu](https://go.microsoft.com/fwlink/?LinkId=821663) a [instalační skript](https://go.microsoft.com/fwlink/?LinkId=822327) nainstaluje nejnovější verzi položky. Chcete-li nainstalovat starší verzi položky, přidejte `-RequiredVersion` parametr.

### <a name="deploy"></a>Nasazení

Chcete-li nasadit položky z Galerie prostředí PowerShell pro Azure Automation, klikněte na tlačítko **nasadit do Azure Automation** na stránce podrobností položky. Budete přesměrováni na portálu Azure Management Portal, kde se přihlásíte pomocí svých přihlašovacích údajů účtu Azure. Všimněte si, že nasazení položky se závislostmi nasadí všechny závislosti pro Azure Automation. Tlačítko "nasadit do Azure Automation, lze zakázat tak, že přidáte **AzureAutomationNotSupported** značku metadata položky.

Další informace o Azure Automation najdete v tématu [web Azure Automation](http://azure.microsoft.com/services/automation/).

## <a name="updating-items-from-the-powershell-gallery"></a>Aktualizace položky z Galerie Powershellu

Aktualizovat položky nainstalovat z Galerie prostředí PowerShell, spusťte [aktualizace modulu](https://go.microsoft.com/fwlink/?LinkID=398576) nebo [skript aktualizace](http://go.microsoft.com/fwlink/?LinkId=619787) rutiny. Při spuštění bez žádné další parametry, [aktualizace modulu](https://go.microsoft.com/fwlink/?LinkID=398576) pokusí aktualizovat každý modul nainstalovaný spuštěním [instalace modulu](https://go.microsoft.com/fwlink/?LinkId=821663).
Chcete-li selektivně aktualizovat moduly, přidejte `-Name` parametr.

Podobně se při spuštění bez žádné další parametry, [skript aktualizace](http://go.microsoft.com/fwlink/?LinkId=619787) taky automatický pokus o aktualizaci každý skript nainstalovaná, spuštěním [instalační skript](https://go.microsoft.com/fwlink/?LinkId=822327).
Chcete-li selektivně aktualizovat skripty, přidejte `-Name` parametr.

## <a name="list-items-that-you-have-installed-from-the-powershell-gallery"></a>Seznam položek, které jste nainstalovali z Galerie Powershellu

Chcete-li zjistit, které moduly, které jste nainstalovali z Galerie prostředí PowerShell, spusťte [Get-InstalledModule](https://go.microsoft.com/fwlink/?LinkId=526863) rutiny. Tento příkaz vypíše všechny moduly, které máte ve vašem systému, které byly nainstalovány přímo z Galerie prostředí PowerShell.

Podobně, chcete-li zjistit, které skripty, které jste nainstalovali z Galerie prostředí PowerShell, spusťte [Get-InstalledScript](https://go.microsoft.com/fwlink/?LinkId=619790) rutiny. Tento příkaz vypíše všechny skripty, které máte ve vašem systému, které byly nainstalovány přímo z Galerie prostředí PowerShell.

