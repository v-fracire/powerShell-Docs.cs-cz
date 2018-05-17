---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: wmf,powershell,setup
contributor: jianyunt, quoctruong
title: Vylepšení správy balíčků v WMF 5.1
ms.openlocfilehash: 1ebd574bd98a056de634ac688244813c1947618e
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
---
# <a name="improvements-to-package-management-in-wmf-51"></a>Vylepšení správy balíčků v WMF 5.1#

## <a name="improvements-in-packagemanagement"></a>Vylepšení v PackageManagement ##
Toto jsou opravy provedené v WMF 5.1:

### <a name="version-alias"></a>Alias verze

**Scénář**: Pokud máte verzi 1.0 nebo 2.0 balíčku P1, nainstaluje do systému a chcete provést odinstalaci verze 1.0, spustili byste `Uninstall-Package -Name P1 -Version 1.0` a očekávají, že verze 1.0, který se má odinstalovat po spuštění rutiny. Ale získá odinstalovat výsledkem je, že verze 2.0.

K tomu dochází, protože `-Version` parametr je zástupce `-MinimumVersion` parametr. Když PackageManagement hledá kvalifikovaný balíček s minimální verzi 1.0, vrátí na nejnovější verzi. Toto chování se očekává v případech, Normální, protože hledání, že nejnovější verze je obvykle požadovaný výsledek. Ale neměla vztahovat na `Uninstall-Package` případu.

**Řešení**: Odebrat `-Version` alias zcela v PackageManagement (také známa jako OneGet) a PowerShellGet.

### <a name="multiple-prompts-for-bootstrapping-the-nuget-provider"></a>Více výzev k zavedení spouštěcího programu NuGet zprostředkovatele

**Scénář**: při spuštění `Find-Module` nebo `Install-Module` nebo jinými rutinami PackageManagement ve vašem počítači poprvé, PackageManagement pokusí bootstrap zprostředkovatele NuGet. Dělá to, protože zprostředkovatel PowerShellGet také používá zprostředkovatele NuGet Stáhnout moduly Powershellu. PackageManagement potom zobrazí výzvu uživateli pro oprávnění k instalaci zprostředkovatele NuGet. Poté, co uživatel vybere "Ano" zavedení spouštěcího programu, se nainstalují nejnovější verzi zprostředkovatele NuGet.

Ale v některých případech, když máte starší verzi NuGet provider nainstalovaný na počítači, starší verze balíčku NuGet někdy získá načíst nejprve do relace prostředí PowerShell (který je časování ve PackageManagement). Ale PowerShellGet vyžaduje novější verzi zprostředkovatele NuGet, který má fungovat, proto PowerShellGet požádá PackageManagement k navázání připojení poskytovatele NuGet znovu. Výsledkem více výzev k zavedení spouštěcího programu NuGet zprostředkovatele.

**Řešení**: V WMF5.1, PackageManagement načte nejnovější verzi zprostředkovatele NuGet více výzev zavedení spouštěcího programu NuGet zprostředkovatele.

Může také pracovat řešení problému ručním odstraněním stará verze zprostředkovatele NuGet (NuGet-Anycpu.exe), pokud existuje z $env: ProgramFiles\PackageManagement\ProviderAssemblies $env: LOCALAPPDATA\PackageManagement\ProviderAssemblies


### <a name="support-for-packagemanagement-on-computers-with-intranet-access-only"></a>Podpora pro PackageManagement na počítačích s přístup v intranetu

**Scénář**: pro podnikový scénář, uživatelé pracují v rámci prostředí kde neexistuje žádný přístup k Internetu, ale intranetu jenom. PackageManagement nepodporoval tento případ v WMF 5.0.

**Scénář**: WMF 5.0, PackageManagement nepodporoval počítačů, které mají jenom. intranetu (ale ne Internet) přístup.

**Řešení**: V 5.1 WMF můžete následujícím postupem povolit použití PackageManagement počítače v síti Intranet:

1. Stáhnout poskytovatele NuGet použijete jiný počítač, který má připojení k Internetu pomocí `Install-PackageProvider -Name NuGet`.

2. Vyhledejte poskytovatele NuGet v rámci buď `$env:ProgramFiles\PackageManagement\ProviderAssemblies\nuget` nebo `$env:LOCALAPPDATA\PackageManagement\ProviderAssemblies\nuget`.

3. Zkopírujte binární soubory složku nebo síťovou umístění sdílené složky, které počítače v síti Intranet přístup a pak nainstalujte zprostředkovatele NuGet s `Install-PackageProvider -Name NuGet -Source <Path to folder>`.


### <a name="event-logging-improvements"></a>Vylepšení události protokolování

Při instalaci balíčků, se změní stav počítače. V WMF 5.1 PackageManagement nyní protokoluje události do protokolu událostí systému Windows pro `Install-Package`, `Uninstall-Package`, a `Save-Package` aktivity. Protokol událostí je stejná jako v prostředí PowerShell, který je `Microsoft-Windows-PowerShell, Operational`.

### <a name="support-for-basic-authentication"></a>Podpora pro základní ověřování

V WMF 5.1 PackageManagement podporuje hledání a instalaci balíčků z úložiště, který vyžaduje základní ověřování. Můžete zadat vaše přihlašovací údaje pro `Find-Package` a `Install-Package` rutiny. Příklad:

``` PowerShell
Find-Package -Source <SourceWithCredential> -Credential (Get-Credential)
```
### <a name="support-for-using-packagemanagement-behind-a-proxy"></a>Podpora pro použití PackageManagement za proxy server

V WMF 5.1 PackageManagement teď používá nové parametry proxy `-ProxyCredential` a `-Proxy`. Pomocí těchto parametrů, můžete zadat adresu URL proxy serveru a přihlašovací údaje pro PackageManagement rutiny. Ve výchozím nastavení proxy serveru systému používají. Příklad:

``` PowerShell
Find-Package -Source http://www.nuget.org/api/v2/ -Proxy http://www.myproxyserver.com -ProxyCredential (Get-Credential)
```
