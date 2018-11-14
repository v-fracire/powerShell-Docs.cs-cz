---
ms.date: 11/06/2018
contributor: JKeithB
keywords: Galerie prostředí powershell, rutina, psgallery, psget
title: Práce s místním PSRepositories
ms.openlocfilehash: 94824ea584c097838b24c6f2cd02407b6147a781
ms.sourcegitcommit: 91786b03704fbd2d185f674df0bc67faddfb6288
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/14/2018
ms.locfileid: "51619250"
---
# <a name="working-with-local-powershellget-repositories"></a>Práce s místním úložišti PowerShellGet

Modul PowerShellGet podporu úložišť než v galerii prostředí PowerShell.
Tyto rutiny se podporují následující scénáře:

- Podpora důvěryhodné, předběžně ověřená sadu moduly Powershellu pro použití ve vašem prostředí
- Testování kanálu CI/CD, který sestaví moduly Powershellu nebo skriptů
- Doručování Powershellové skripty a moduly pro systémy, které nemá přístup k Internetu

Tento článek popisuje, jak nastavit místní úložiště prostředí PowerShell. Tento článek také popisuje [OfflinePowerShellGetDeploy][] modulu k dispozici z Galerie prostředí PowerShell. Tento modul obsahuje rutiny pro instalaci na nejnovější verzi modulu PowerShellGet do svého místního úložiště.

## <a name="local-repository-types"></a>Typy místního úložiště

Existují dva způsoby, jak vytvořit místní PSRepository: NuGet server nebo sdílená složka. Každý typ má své výhody a nevýhody:

NuGet Server

| Výhody| Nevýhody |
| --- | --- |
| Úzce napodobuje funkce PowerShellGallery | Vícevrstvé aplikace vyžaduje plánování operací a podpora |
| NuGet se integruje se sadou Visual Studio a další nástroje | Model ověřování a správy účtů NuGet |
| Podporuje metadata v NuGet `.Nupkg` balíčky | Publikování vyžaduje klíč rozhraní API pro správu a údržbu |
| Poskytuje hledání, Správa balíčků, atd. | |

Sdílené složky

| Výhody| Nevýhody |
| --- | --- |
| Snadné nastavení, zálohování a údržbě | Metadata, používá modul PowerShellGet není k dispozici |
| Model zabezpečení Simple - uživatelských oprávnění pro sdílenou složku | Žádné uživatelské rozhraní nad rámec základní sdílenou složku |
| Bez omezení, jako je například nahrazení existujících položek | Omezené zabezpečení a žádný záznam, co aktualizace |

Správce balíčků PowerShellGet funguje s typem a podporuje vyhledávání verze a instalace závislostí.
Ale některé funkce, které fungují pro galerii prostředí PowerShell nejsou k dispozici pro základní servery NuGet nebo sdílené složky.

- Všechno, co je balíček – bez rozdílů mezi skripty, moduly, prostředky DSC nebo funkce role.
- Souborové servery se sdílená složka neuvidí metadata balíčků, včetně značek.

## <a name="creating-a-local-repository"></a>Vytvořit místní úložiště

V následujícím článku jsou uvedené kroky pro nastavení serveru NuGet.

- [NuGet.Server][]

Postupujte podle pokynů až do okamžiku přidávání balíčků. Kroky pro [publikovat balíček](#publishing-to-a-local-repository) jsou popsané dále v tomto článku.

Na základě sdílené složky úložiště souborů Ujistěte se, aby uživatelé měli oprávnění pro přístup ke sdílené složce.

## <a name="registering-a-local-repository"></a>Registrace místní úložiště

Před použitím úložiště, je nutné jej zaregistrovat pomocí `Register-PSRepository` příkazu.
V příkladech níže **InstallationPolicy** je nastavena na *důvěryhodné*, za předpokladu, že důvěřujete vlastního úložiště.

```powershell
# Register a NuGet-based server
Register-PSRepository -Name LocalPSRepo -SourceLocation http://MyLocalNuget/Api/V2/ -ScriptSourceLocation http://MyLocalNuget/Api/V2 -InstallationPolicy Trusted

# Register a file share on my local machine
Register-PSRepository -Name LocalPSRepo -SourceLocation '\\localhost\PSRepoLocal\' -ScriptSourceLocation '\\localhost\PSRepoLocal\' -InstallationPolicy Trusted
```

Poznamenejte si hodnotu rozdílu mezi způsob, jakým dva příkazy pracovat **ScriptSourceLocation**. Pro soubor úložiště založené na sdílenou složku **SourceLocation** a **ScriptSourceLocation** se musí shodovat. Pro úložiště založeného na webu, musí být jiný, takže v tomto příkladu koncový znak "/" se přidá do **SourceLocation**.

Pokud chcete nově vytvořenou PSRepository výchozí úložiště, musíte zrušit registraci jiných PSRepositories. Příklad:

```powershell
Unregister-PSRepository -Name PSGallery
```

> [!NOTE]
> Název úložiště 'PSGallery' je vyhrazený pro použití ve galerii prostředí PowerShell. Můžete zrušit registraci PSGallery, ale nemůže znovu použít název PSGallery jakéhokoli jiného úložiště.

Pokud je potřeba obnovit PSGallery, spusťte následující příkaz:

```powershell
Register-PSRepository -Default
```

## <a name="publishing-to-a-local-repository"></a>Publikování do místního úložiště

Po zaregistrování místního PSRepository, můžete publikovat místní PSRepository. Existují dva základní scénáře publikování: publikování vlastní modul a publikování modulu z PSGallery.

### <a name="publishing-a-module-you-authored"></a>Publikování modul, který jste vytvořili

Použití `Publish-Module` a `Publish-Script` publikovat modul Místní PSRepository stejným způsobem jako v galerii prostředí PowerShell.

- Zadejte umístění pro váš kód
- Zadejte klíč rozhraní API
- Zadejte název úložiště. Například `-PSRepository LocalPSRepo`.

> [!NOTE]
> Musíte vytvořit účet na serveru NuGet a přihlaste se k vygenerování a uložit klíč rozhraní API.
> Pro sdílenou složku použijte pro hodnotu NuGetApiKey jakýkoli neprázdný řetězec.

Příklady:

```powershell
# Publish to a NuGet Server repository using my NuGetAPI key
Publish-Module -Path 'c:\projects\MyModule' -Repository LocalPsRepo -NuGetApiKey 'oy2bi4avlkjolp6bme6azdyssn6ps3iu7ib2qpiudrtbji'

# Publish to a file share repo - the NuGet API key must be a non-blank string
Publish-Module -Path 'c:\projects\MyModule' -Repository LocalPsRepo -NuGetApiKey 'AnyStringWillDo'
```

> [!IMPORTANT]
> Abyste zajistili bezpečnost, klíče rozhraní API by neměl být pevně zakódovaný ve skriptech. Používejte systém zabezpečená správa klíčů.

### <a name="publishing-a-module-from-the-psgallery"></a>Publikování z PSGallery modulu

K publikování modul z PSGallery a místní PSRepository, můžete použít rutinu balíček uložit-Package.

- Zadejte název balíčku
- Jako poskytovatel zadat "NuGet.
- Zadejte umístění PSGallery jako zdroj (https://www.powershellgallery.com/api/v2)
- Zadejte cestu do místního úložiště

Příklad:

```powershell
# Publish from the PSGallery to your local Repository
Save-Package -Name 'PackageName' -Provider Nuget -Source https://www.powershellgallery.com/api/v2 -Path '\\localhost\PSRepoLocal\'
```

Pokud vaše místní PSRepository založeného na webu, vyžaduje další krok, který používá nuget.exe k publikování.

Viz dokumentace pro používání [nuget.exe][].

## <a name="installing-powershellget-on-a-disconnected-system"></a>Instalace Správce balíčků PowerShellGet na odpojeném režimu

Nasazení modulu PowerShellGet je obtížné v prostředích, která vyžadují systém odpojit od Internetu. Správce balíčků PowerShellGet má spuštění procesu, který nainstaluje nejnovější verzi okamžiku, kdy se používá. Modul OfflinePowerShellGetDeploy v galerii prostředí PowerShell obsahuje rutiny, které podporují tento proces spuštění.

Ke spuštění v režimu offline nasazení, budete muset:

- Stáhněte a nainstalujte systém OfflinePowerShellGetDeploy vašich připojených k Internetu a odpojených systémů
- Stáhnout modul PowerShellGet a jeho závislosti na systému připojeného k Internetu pomocí `Save-PowerShellGetForOffline` rutiny
- Kopírovat PowerShellGet a jeho závislé součásti ze systému připojeného k Internetu do odpojeného systému
- Použití `Install-PowerShellGetOffline` v odpojeném systému umístí modul PowerShellGet a jeho závislosti do správné složky

Následující příkazy použijte `Save-PowerShellGetForOffline` převést všechny součásti do složky `f:\OfflinePowerShellGet`

```powershell
# Requires -RunAsAdministrator
#Download the OfflinePowerShellGetDeploy to a location that can be accessed
# by both the connected and disconnected systems.
Save-Module -Name OfflinePowerShellGetDeploy -Path 'F:\' -Repository PSGallery
Import-Module F:\OfflinePowerShellGetDeploy

# Put PowerShellGet somewhere locally
Save-PowerShellGetForOffline -LocalFolder 'F:\OfflinePowerShellGet'
```

V tomto okamžiku je třeba obsah `F:\OfflinePowerShellGet` odpojených systémů k dispozici. Spustit `Install-PowerShellGetOffline` rutinu instalace Správce balíčků PowerShellGet v odpojeném systému.

> [!NOTE]
> Je důležité, nespouštějte PowerShellGet v relaci prostředí PowerShell před spuštěním těchto příkazů. Jakmile správce balíčků PowerShellGet je načten do relace, komponenty se nedá aktualizovat. Pokud spustíte Správce balíčků PowerShellGet omylem, ukončete a restartujte prostředí PowerShell.

```powershell
Import-Module F:\OfflinePowerShellGetDeploy

Install-PowerShellGetOffline -LocalFolder 'F:\OfflinePowerShellGet'
```

Po spuštění těchto příkazů, jste připraveni publikovat PowerShellGet do místního úložiště.

```powershell
# Publish to a NuGet Server repository using my NuGetAPI key
Publish-Module -Path 'F:\OfflinePowershellGet' -Repository LocalPsRepo -NuGetApiKey 'oy2bi4avlkjolp6bme6azdyssn6ps3iu7ib2qpiudrtbji'

# Publish to a file share repo - the NuGet API key must be a non-blank string
Publish-Module -Path 'F:\OfflinePowerShellGet' -Repository LocalPsRepo -NuGetApiKey 'AnyStringWillDo'
```

> [!IMPORTANT]
> Abyste zajistili bezpečnost, klíče rozhraní API by neměl být pevně zakódovaný ve skriptech. Používejte systém zabezpečená správa klíčů.

<!-- external links -->
[OfflinePowerShellGetDeploy]: https://www.powershellgallery.com/packages/OfflinePowerShellGetDeploy/0.1.1
[Nuget.Server]: /nuget/hosting-packages/nuget-server
[nuget.exe]: /nuget/tools/nuget-exe-cli-reference
