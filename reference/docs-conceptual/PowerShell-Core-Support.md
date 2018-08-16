---
title: Životní cyklus podpory PowerShellu Core
description: Zásady, kterými se řídí podporu pro prostředí PowerShell Core
ms.date: 08/06/2018
ms.openlocfilehash: 2e0ca1b9c133e6f316a40aff13365d0489059165
ms.sourcegitcommit: 01ac77cd0b00e4e5e964504563a9212e8002e5e0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/07/2018
ms.locfileid: "39587155"
---
# <a name="powershell-core-support-lifecycle"></a>Životní cyklus podpory PowerShellu Core

PowerShell Core je odlišnou sadu nástrojů a komponenty, které je dodán, nainstalovat a nakonfigurovat samostatně z prostředí Windows PowerShell.
PowerShell Core není proto součástí licenční smlouvy Windows 7/8.1/10 nebo Windows Server.

PowerShell Core je však podporováno v tradiční Microsoft smlouvy o podpoře, včetně [Premier][], [smlouvy Microsoft Enterprise][enterprise-agreement]a [Programu Microsoft Software Assurance][assurance].
Můžete také platit [odbornou pomoc][] pro PowerShell Core vyplněním žádosti o podporu pro váš problém.

Nabízíme také [komunitní podpory][] na Githubu, kde můžete soubor problému, chyby nebo žádost o funkci.
Alternativně můžete zjistit pomoc od ostatních členů komunity na Obecné [Microsoft Community][] nebo Microsoft [technické komunity Powershellu][].
Nabízíme-zaručeno existuje, že váš problém bude řešit nebo vyřešení v časovém limitu.
Pokud máte problém vyžadující okamžitou pozornost, měli byste použít tradiční, placené možnosti podpory.

## <a name="lifecycle-of-powershell-core"></a>Životní cyklus Powershellu Core

PowerShell Core se seznámíte s požadavky [moderní životní cyklus Microsoft][modern].
Tento životní cyklus podpory má Informujte zákazníky o nejnovější verze.

Větev verze 6.x PowerShell Core aktualizují přibližně jednou za šest měsíců (např. 6.0, 6.1, 6.2, atd.)

> [!IMPORTANT]
> Je nutné aktualizovat do šesti měsíců po vydání každý nový dílčí verze, chcete-li i nadále zajistit podporu.

Například pokud 1. července 2018, se uvolní prostředí PowerShell Core 6.1 by být očekáváte aktualizaci do prostředí PowerShell Core 6.1 1. ledna 2019 kvůli zachování podpory.

![Životní cyklus větev Powershellu Core][lifecycle-chart]

Moderní zásady životního cyklu také vyžaduje, aby Microsoft oznámit zákazníkům 12 měsíců před ukončením odborné pomoci pro produkt (tj. PowerShell Core).

Nakonec Očekáváme, že přijímají PowerShell Core "dlouhodobé údržby" zůstat podporována v konkrétní větvi nebo verze 6.x aktualizuje přístupu, kde by vyžadujeme pouze pro obsluhu a zabezpečení.

## <a name="supported-platforms"></a>Podporované platformy

Podrobnosti najdete v následující tabulce zobrazíte jaké platformy je oficiálně podporované verze prostředí PowerShell Core používáte.

Naše komunita také přidal balíčky pro některé platformy, ale nejsou oficiálně podporované.
Tyto balíčky jsou označeny jako `Community` v tabulce.

Uvedené jako platformy `Experimental` nejsou oficiálně podporované, ale jsou k dispozici pro experimentování ve službě a zpětnou vazbu.

|                                                   | 6.0         | 6.1         |
|---------------------------------------------------|:-----------:|:-----------:|
| Windows 7, 8.1 a 10                            | Podporované   | Podporované   |
| Windows Server 2008 R2, 2012 R2, 2016             | Podporované   | Podporované   |
| [Windows Server prostřednictvím půlročního kanálu][semi-annual] | Podporované   | Podporované   |
| Ubuntu 14.04 a 16.04                           | Podporované   | Podporované   |
| Ubuntu 18.04                                      |             | Podporované   |
| Ubuntu 18.10 (prostřednictvím přichycení balíček)                   |             | Komunita   |
| Debian 8.7 + a 9                                | Podporované   | Podporované   |
| CentOS 7                                          | Podporované   | Podporované   |
| Red Hat Enterprise Linux 7                        | Podporované   | Podporované   |
| OpenSUSE 42.3                                     | Podporované   | Podporované   |
| Fedora 27                                         | Podporované   | Podporované   |
| Fedora 28                                         |             | Podporované   |
| macOS 10.12 +                                      | Podporované   | Podporované   |
| Architektura                                              | Komunita   | Komunita   |
| Raspbian                                          | Experimentální| Komunita   |
| Kali                                              | Komunita   | Komunita   |
| AppImage (funguje na různých platformách Linux)     | Komunita   | Komunita   |
| [Přichytit balíčku](https://snapcraft.io/powershell)   | Další informace v poznámce    | Další informace v poznámce    |

> [!NOTE]
> Přichytit balíčky budou experimentální určitou dobu.  Po jsme si jisti, že Snap nezavádí nové problémy podpory, podpora bude následovat distribuci, kterou používáte balíček na.

## <a name="platform-which-are-out-of-support"></a>Platforma, která už skončila podpora

Ukončení životnosti technologie definovaným vlastníkem platformy dosáhne verze platformy PowerShell Core přestane také k poskytování podpory pro tuto verzi platformy. Dříve vydané balíčky zůstávají dostupné i pro zákazníky, kteří potřebují přístup, ale formální podpory a aktualizace jakéhokoli druhu už, poskytneme vám.

Proto podpora pro tyto verze vlastníky distribuce softwaru bylo ukončeno a nejsou podporovány.

| Operační systém       | Verze | Ukončení životnosti                                                                                 |
|----------|---------|---------------------------------------------------------------------------------------------|
| Fedora   | 24      | [Ze srpna 2017](https://fedoramagazine.org/fedora-24-eol/)                                    |
| Fedora   | 25      | [. Prosince 2017](https://fedoramagazine.org/fedora-25-end-life/)                             |
| Fedora   | 26      | [. Května 2018.](https://fedoramagazine.org/fedora-26-end-life/)                                  |
| OpenSUSE | 42.1    | [Květen 2017](https://lists.opensuse.org/opensuse-security-announce/2017-05/msg00053.html)     |
| OpenSUSE | 42.2    | [. Ledna 2018](https://lists.opensuse.org/opensuse-security-announce/2017-11/msg00066.html) |
| Ubuntu   | 16.10   | [. Července 2017](https://lists.ubuntu.com/archives/ubuntu-announce/2017-July/000223.html)        |
| Ubuntu   | č. 17.04   | [. Ledna 2018](https://lists.ubuntu.com/archives/ubuntu-announce/2018-January.txt)          |
| Ubuntu   | 17.10   | [. Července 2018](https://lists.ubuntu.com/archives/ubuntu-announce/2018-July/000232.html)        |

## <a name="notes-on-licensing"></a>Poznámky k licencování

PowerShell Core je vydávaný v rámci [Licence MIT][].
V rámci této licence a bez smlouvy placená odborná pomoc. Uživatelé jsou omezené na [komunitní podpory][].
Podpora komunity Microsoft neposkytuje žádnou záruku rychlosti odezvy nebo opravy.

## <a name="windows-powershell-module"></a>Modul Windows PowerShell

Podpora pro PowerShell Core nerozšiřuje ostatní moduly produktu, pokud tyto moduly explicitně podporují PowerShell Core.
Například použití `ActiveDirectory` modul, který se dodává jako součást systému Windows Server se o nepodporovaný scénář.

Moduly, které nepodporují explicitně PowerShell Core však může být v některých případech kompatibilní.
Po instalaci [`WindowsPSModulePath`][] modulu, prostředí Windows PowerShell můžete připojit `PSModulePath` k Powershellu Core `PSModulePath`.

Nejdřív nainstalujte `WindowsPSModulePath` modulu z Galerie prostředí PowerShell:

```powershell
# Add `-Scope CurrentUser` if you're installing as non-admin
Install-Module WindowsPSModulePath -Force
```

Po instalaci tohoto modulu, spusťte `Add-WindowsPSModulePath` rutiny prostředí Windows PowerShell přidat `PSModulePath` do prostředí PowerShell Core:

```powershell
# Add this line to your profile if you always want Windows PowerShell PSModulePath
Add-WindowsPSModulePath
```

[Premier]: https://www.microsoft.com/en-us/microsoftservices/support.aspx
[enterprise-agreement]: https://www.microsoft.com/en-us/licensing/licensing-programs/enterprise.aspx
[assurance]: https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx
[komunitní podpory]: https://github.com/powershell/powershell/issues
[Microsoft Community]: https://answers.microsoft.com/
[technické komunity Powershellu]: https://techcommunity.microsoft.com/t5/PowerShell/ct-p/WindowsPowerShell
[odbornou pomoc]: https://support.microsoft.com/assistedsupportproducts
[modern]: https://support.microsoft.com/help/30881/modern-lifecycle-policy
[lifecycle-chart]: ./images/modern-lifecycle.png
[semi-annual]: https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview
[Licence MIT]: https://github.com/PowerShell/PowerShell/blob/master/LICENSE.txt
["WindowsPSModulePath.]: https://www.powershellgallery.com/packages/WindowsPSModulePath/
