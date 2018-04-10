# <a name="powershell-core-support-lifecycle"></a>Životní cyklus podpory PowerShellu Core

Základní prostředí PowerShell je odlišnou sadu nástrojů a součásti, které je součástí, nainstalovat a nakonfigurovat samostatně z prostředí Windows PowerShell.
Proto základní prostředí PowerShell není součástí systému Windows 7/8.1/10 nebo Windows Server licenčních smluv.

Ale jádra prostředí PowerShell je podporován v rámci tradiční smlouvy podpory společnosti Microsoft, včetně [úrovně Premier][], [smlouvách Microsoft Enterprise][enterprise-agreement]a [Programu Microsoft Software Assurance][assurance].
Můžete také platíte [odbornou pomoc][] pro základní prostředí PowerShell pomocí vyplnění žádosti o podporu pro váš problém.

Také nabízí [podpora komunity][] na Githubu, kde můžete soubor problému, chyby nebo žádost o funkce.
Alternativně můžete zjistit pomoci ostatním členům komunity na Obecné [Microsoft Community][] nebo Microsoft [technické komunity Powershellu][].
Nabízíme žádná záruka, existuje, bude problém řešit nebo přeložit včas.
Pokud máte potíže, které vyžadují okamžitou pozornost, používejte tradiční, placené možnosti podpory.

## <a name="lifecycle-of-powershell-core"></a>Životní cyklus jádra prostředí PowerShell

Základní prostředí PowerShell přechází [moderní zásad životního cyklu Microsoft][modern].
Tohoto životního cyklu podpory je určený k zachování aktualizovaného stavu s nejnovější verzí zákazníků.

Verze 6.x větev základní prostředí PowerShell bude aktualizovat přibližně jednou za šest měsíců (např. 6.0, 6.1, 6.2, atd.)

> [!IMPORTANT]
> Je třeba aktualizovat šest měsíců po každé nové podverze verze dál dostávat podpory.

Například pokud 6.1 základní prostředí PowerShell je vydána na 1. července 2018, můžete se očekává, aktualizujte na 6.1 základní prostředí PowerShell tak, že 1. ledna 2019 pro zachování podpory.

![Životní cyklus větve základní prostředí PowerShell][lifecycle-chart]

Moderní zásadách životního cyklu také vyžaduje, aby Microsoft oznámit zákazníkům dobu 12 měsíců před zrušený podporu pro produkt (tj. v prostředí PowerShell jader).

Nakonec Očekáváme, že základní prostředí PowerShell zavede "dlouhodobé údržby" přístup, pokud jsme vyžadují jenom údržby a bezpečnostní aktualizace zůstat v podporu na konkrétní firemní pobočky nebo verze 6.x.

## <a name="supported-platforms"></a>Podporované platformy

Základní prostředí PowerShell je oficiálně podporován na následujících platformách:

* Windows 7, 8.1 a 10
* Windows Server 2008 R2, 2012 R2, 2016
* [Windows Server zadáte roční kanálu][semi-annual]
* Ubuntu 14.04 a 16.04, č. 17.04
* Debian 8.7 + a 9
* CentOS 7
* Red Hat Enterprise Linux 7
* OpenSUSE 42.2
* Fedora 25, 26
* macOS 10.12+

Naše komunita také přispívá balíčky pro tyto platformy, ale nejsou oficiálně suppported:

* Arch Linux
* Kali Linux
* AppImage (funguje na více platforem Linux)

## <a name="notes-on-licensing"></a>Poznámky k licencování

Základní prostředí PowerShell je vydávaný v rámci [licencí MIT][].
V části tuto licenci a bez placené podporu smlouvy, uživatelé jsou omezeny na [podpora komunity][].
S podporou komunity společnost Microsoft neposkytuje žádné záruky odezvy nebo opravy.

## <a name="windows-powershell-module"></a>Windows PowerShell Module

Podpora pro PowerShell základní neprodlužuje z ostatních modulů produktu, pokud tyto moduly explicitně nepodporují základní prostředí PowerShell.
Například pomocí `ActiveDirectory` modul, který se dodává jako součást systému Windows Server se o nepodporovaný scénář.

Moduly, které nepodporují explicitně základní prostředí PowerShell však může být v některých případech kompatibilní.
Nainstalováním [ `WindowsPSModulePath` ][] modulu prostředí Windows PowerShell můžete připojit `PSModulePath` pro vaše prostředí PowerShell základní `PSModulePath`.

Nejdřív nainstalujte `WindowsPSModulePath` modulu z Galerie prostředí PowerShell:

```powershell
# Add `-Scope CurrentUser` if you're installing as non-admin
Install-Module WindowsPSModulePath -Force
```

Po instalaci tohoto modulu, spusťte `Add-WindowsPSModulePath` rutiny prostředí Windows PowerShell přidat `PSModulePath` na jádro prostředí PowerShell:

```powershell
# Add this line to your profile if you always want Windows PowerShell PSModulePath
Add-WindowsPSModulePath
```

[úrovně Premier]: https://www.microsoft.com/en-us/microsoftservices/support.aspx
[enterprise-agreement]: https://www.microsoft.com/en-us/licensing/licensing-programs/enterprise.aspx
[assurance]: https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx
[podpora komunity]: https://github.com/powershell/powershell/issues
[Microsoft Community]: https://answers.microsoft.com/
[technické komunity Powershellu]: https://techcommunity.microsoft.com/t5/PowerShell/ct-p/WindowsPowerShell
[odbornou pomoc]: https://support.microsoft.com/assistedsupportproducts
[modern]: https://support.microsoft.com/help/30881/modern-lifecycle-policy
[lifecycle-chart]: ./images/modern-lifecycle.png
[semi-annual]: https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview
[licencí MIT]: https://github.com/PowerShell/PowerShell/blob/master/LICENSE.txt
[`WindowsPSModulePath`]: https://www.powershellgallery.com/packages/WindowsPSModulePath/