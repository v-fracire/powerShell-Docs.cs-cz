# <a name="powershell-core-support-lifecycle"></a><span data-ttu-id="a47fa-101">Životní cyklus podpory PowerShellu Core</span><span class="sxs-lookup"><span data-stu-id="a47fa-101">PowerShell Core Support Lifecycle</span></span>

<span data-ttu-id="a47fa-102">Základní prostředí PowerShell je odlišnou sadu nástrojů a součásti, které je součástí, nainstalovat a nakonfigurovat samostatně z prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a47fa-102">PowerShell Core is a distinct set of tools and components that is shipped, installed, and configured separately from Windows PowerShell.</span></span>
<span data-ttu-id="a47fa-103">Proto základní prostředí PowerShell není součástí systému Windows 7/8.1/10 nebo Windows Server licenčních smluv.</span><span class="sxs-lookup"><span data-stu-id="a47fa-103">Therefore, PowerShell Core is not included in the Windows 7/8.1/10 or Windows Server licensing agreements.</span></span>

<span data-ttu-id="a47fa-104">Ale jádra prostředí PowerShell je podporován v rámci tradiční smlouvy podpory společnosti Microsoft, včetně [úrovně Premier][], [smlouvách Microsoft Enterprise][enterprise-agreement]a [Programu Microsoft Software Assurance][assurance].</span><span class="sxs-lookup"><span data-stu-id="a47fa-104">However, PowerShell Core is supported under traditional Microsoft support agreements, including [Premier][], [Microsoft Enterprise Agreements][enterprise-agreement], and [Microsoft Software Assurance][assurance].</span></span>
<span data-ttu-id="a47fa-105">Můžete také platíte [odbornou pomoc][] pro základní prostředí PowerShell pomocí vyplnění žádosti o podporu pro váš problém.</span><span class="sxs-lookup"><span data-stu-id="a47fa-105">You can also pay for [assisted support][] for PowerShell Core by filing a support request for your problem.</span></span>

<span data-ttu-id="a47fa-106">Také nabízí [podpora komunity][] na Githubu, kde můžete soubor problému, chyby nebo žádost o funkce.</span><span class="sxs-lookup"><span data-stu-id="a47fa-106">We also offer [community support][] on GitHub where you can file an issue, bug, or feature request.</span></span>
<span data-ttu-id="a47fa-107">Alternativně můžete zjistit pomoci ostatním členům komunity na Obecné [Microsoft Community][] nebo Microsoft [technické komunity Powershellu][].</span><span class="sxs-lookup"><span data-stu-id="a47fa-107">Alternatively, you may find help from other members of the community on the general [Microsoft Community][] or the Microsoft [PowerShell Tech Community][].</span></span>
<span data-ttu-id="a47fa-108">Nabízíme žádná záruka, existuje, bude problém řešit nebo přeložit včas.</span><span class="sxs-lookup"><span data-stu-id="a47fa-108">We offer no guarantee there that your issue will be addressed or resolved in a timely manner.</span></span>
<span data-ttu-id="a47fa-109">Pokud máte potíže, které vyžadují okamžitou pozornost, používejte tradiční, placené možnosti podpory.</span><span class="sxs-lookup"><span data-stu-id="a47fa-109">If you have a problem that requires immediate attention, you should use the traditional, paid support options.</span></span>

## <a name="lifecycle-of-powershell-core"></a><span data-ttu-id="a47fa-110">Životní cyklus jádra prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="a47fa-110">Lifecycle of PowerShell Core</span></span>

<span data-ttu-id="a47fa-111">Základní prostředí PowerShell přechází [moderní zásad životního cyklu Microsoft][modern].</span><span class="sxs-lookup"><span data-stu-id="a47fa-111">PowerShell Core is adopting the [Microsoft Modern Lifecycle Policy][modern].</span></span>
<span data-ttu-id="a47fa-112">Tohoto životního cyklu podpory je určený k zachování aktualizovaného stavu s nejnovější verzí zákazníků.</span><span class="sxs-lookup"><span data-stu-id="a47fa-112">This support lifecycle is intended to keep customers up-to-date with the latest versions.</span></span>

<span data-ttu-id="a47fa-113">Verze 6.x větev základní prostředí PowerShell bude aktualizovat přibližně jednou za šest měsíců (např. 6.0, 6.1, 6.2, atd.)</span><span class="sxs-lookup"><span data-stu-id="a47fa-113">The version 6.x branch of PowerShell Core will be updated approximately once every six months (e.g. 6.0, 6.1, 6.2, etc.)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a47fa-114">Je třeba aktualizovat šest měsíců po každé nové podverze verze dál dostávat podpory.</span><span class="sxs-lookup"><span data-stu-id="a47fa-114">You must update within six months after each new minor version release to continue receiving support.</span></span>

<span data-ttu-id="a47fa-115">Například pokud 6.1 základní prostředí PowerShell je vydána na 1. července 2018, můžete se očekává, aktualizujte na 6.1 základní prostředí PowerShell tak, že 1. ledna 2019 pro zachování podpory.</span><span class="sxs-lookup"><span data-stu-id="a47fa-115">For example, if PowerShell Core 6.1 is released on July 1st, 2018, you would be expected to update to PowerShell Core 6.1 by January 1st, 2019 to maintain support.</span></span>

![Životní cyklus větve základní prostředí PowerShell][lifecycle-chart]

<span data-ttu-id="a47fa-117">Moderní zásadách životního cyklu také vyžaduje, aby Microsoft oznámit zákazníkům dobu 12 měsíců před zrušený podporu pro produkt (tj. v prostředí PowerShell jader).</span><span class="sxs-lookup"><span data-stu-id="a47fa-117">The Modern Lifecycle Policy also requires that Microsoft give customers 12 months notice before discontinuing support for a product (i.e. PowerShell Core).</span></span>

<span data-ttu-id="a47fa-118">Nakonec Očekáváme, že základní prostředí PowerShell zavede "dlouhodobé údržby" přístup, pokud jsme vyžadují jenom údržby a bezpečnostní aktualizace zůstat v podporu na konkrétní firemní pobočky nebo verze 6.x.</span><span class="sxs-lookup"><span data-stu-id="a47fa-118">Eventually, we expect PowerShell Core will adopt the "long-term servicing" approach where we would require only servicing and security updates to stay in support on a specific branch/version of 6.x.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="a47fa-119">Podporované platformy</span><span class="sxs-lookup"><span data-stu-id="a47fa-119">Supported platforms</span></span>

<span data-ttu-id="a47fa-120">Základní prostředí PowerShell je oficiálně podporován na následujících platformách:</span><span class="sxs-lookup"><span data-stu-id="a47fa-120">PowerShell Core is officially supported on the following platforms:</span></span>

* <span data-ttu-id="a47fa-121">Windows 7, 8.1 a 10</span><span class="sxs-lookup"><span data-stu-id="a47fa-121">Windows 7, 8.1, and 10</span></span>
* <span data-ttu-id="a47fa-122">Windows Server 2008 R2, 2012 R2, 2016</span><span class="sxs-lookup"><span data-stu-id="a47fa-122">Windows Server 2008 R2, 2012 R2, 2016</span></span>
* <span data-ttu-id="a47fa-123">[Windows Server zadáte roční kanálu][semi-annual]</span><span class="sxs-lookup"><span data-stu-id="a47fa-123">[Windows Server Semi-Annual Channel][semi-annual]</span></span>
* <span data-ttu-id="a47fa-124">Ubuntu 14.04 a 16.04, č. 17.04</span><span class="sxs-lookup"><span data-stu-id="a47fa-124">Ubuntu 14.04, 16.04, and 17.04</span></span>
* <span data-ttu-id="a47fa-125">Debian 8.7 + a 9</span><span class="sxs-lookup"><span data-stu-id="a47fa-125">Debian 8.7+, and 9</span></span>
* <span data-ttu-id="a47fa-126">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="a47fa-126">CentOS 7</span></span>
* <span data-ttu-id="a47fa-127">Red Hat Enterprise Linux 7</span><span class="sxs-lookup"><span data-stu-id="a47fa-127">Red Hat Enterprise Linux 7</span></span>
* <span data-ttu-id="a47fa-128">OpenSUSE 42.2</span><span class="sxs-lookup"><span data-stu-id="a47fa-128">OpenSUSE 42.2</span></span>
* <span data-ttu-id="a47fa-129">Fedora 25, 26</span><span class="sxs-lookup"><span data-stu-id="a47fa-129">Fedora 25, 26</span></span>
* <span data-ttu-id="a47fa-130">macOS 10.12+</span><span class="sxs-lookup"><span data-stu-id="a47fa-130">macOS 10.12+</span></span>

<span data-ttu-id="a47fa-131">Naše komunita také přispívá balíčky pro tyto platformy, ale nejsou oficiálně suppported:</span><span class="sxs-lookup"><span data-stu-id="a47fa-131">Our community has also contributed packages for the following platforms, but they are not officially suppported:</span></span>

* <span data-ttu-id="a47fa-132">Arch Linux</span><span class="sxs-lookup"><span data-stu-id="a47fa-132">Arch Linux</span></span>
* <span data-ttu-id="a47fa-133">Kali Linux</span><span class="sxs-lookup"><span data-stu-id="a47fa-133">Kali Linux</span></span>
* <span data-ttu-id="a47fa-134">AppImage (funguje na více platforem Linux)</span><span class="sxs-lookup"><span data-stu-id="a47fa-134">AppImage (works on multiple Linux platforms)</span></span>

## <a name="notes-on-licensing"></a><span data-ttu-id="a47fa-135">Poznámky k licencování</span><span class="sxs-lookup"><span data-stu-id="a47fa-135">Notes on licensing</span></span>

<span data-ttu-id="a47fa-136">Základní prostředí PowerShell je vydávaný v rámci [licencí MIT][].</span><span class="sxs-lookup"><span data-stu-id="a47fa-136">PowerShell Core is released under the [MIT license][].</span></span>
<span data-ttu-id="a47fa-137">V části tuto licenci a bez placené podporu smlouvy, uživatelé jsou omezeny na [podpora komunity][].</span><span class="sxs-lookup"><span data-stu-id="a47fa-137">Under this license, and in the absence of a paid support agreement, users are limited to [community support][].</span></span>
<span data-ttu-id="a47fa-138">S podporou komunity společnost Microsoft neposkytuje žádné záruky odezvy nebo opravy.</span><span class="sxs-lookup"><span data-stu-id="a47fa-138">With community support, Microsoft makes no guarantees of responsiveness or fixes.</span></span>

## <a name="windows-powershell-module"></a><span data-ttu-id="a47fa-139">Windows PowerShell Module</span><span class="sxs-lookup"><span data-stu-id="a47fa-139">Windows PowerShell Module</span></span>

<span data-ttu-id="a47fa-140">Podpora pro PowerShell základní neprodlužuje z ostatních modulů produktu, pokud tyto moduly explicitně nepodporují základní prostředí PowerShell.</span><span class="sxs-lookup"><span data-stu-id="a47fa-140">Support for PowerShell Core does not extend to other product modules unless those modules explicitly support PowerShell Core.</span></span>
<span data-ttu-id="a47fa-141">Například pomocí `ActiveDirectory` modul, který se dodává jako součást systému Windows Server se o nepodporovaný scénář.</span><span class="sxs-lookup"><span data-stu-id="a47fa-141">For example, using the `ActiveDirectory` module that ships as part of Windows Server is an unsupported scenario.</span></span>

<span data-ttu-id="a47fa-142">Moduly, které nepodporují explicitně základní prostředí PowerShell však může být v některých případech kompatibilní.</span><span class="sxs-lookup"><span data-stu-id="a47fa-142">However, modules that do not explicitly support PowerShell Core may be compatible in some cases.</span></span>
<span data-ttu-id="a47fa-143">Nainstalováním [ `WindowsPSModulePath` ][] modulu prostředí Windows PowerShell můžete připojit `PSModulePath` pro vaše prostředí PowerShell základní `PSModulePath`.</span><span class="sxs-lookup"><span data-stu-id="a47fa-143">By installing the [`WindowsPSModulePath`][] module, you can append the Windows PowerShell `PSModulePath` to your PowerShell Core `PSModulePath`.</span></span>

<span data-ttu-id="a47fa-144">Nejdřív nainstalujte `WindowsPSModulePath` modulu z Galerie prostředí PowerShell:</span><span class="sxs-lookup"><span data-stu-id="a47fa-144">First, install the `WindowsPSModulePath` module from the PowerShell Gallery:</span></span>

```powershell
# Add `-Scope CurrentUser` if you're installing as non-admin
Install-Module WindowsPSModulePath -Force
```

<span data-ttu-id="a47fa-145">Po instalaci tohoto modulu, spusťte `Add-WindowsPSModulePath` rutiny prostředí Windows PowerShell přidat `PSModulePath` na jádro prostředí PowerShell:</span><span class="sxs-lookup"><span data-stu-id="a47fa-145">After installing this module, run the `Add-WindowsPSModulePath` cmdlet to add the Windows PowerShell `PSModulePath` to PowerShell Core:</span></span>

```powershell
# Add this line to your profile if you always want Windows PowerShell PSModulePath
Add-WindowsPSModulePath
```

[úrovně Premier]: https://www.microsoft.com/en-us/microsoftservices/support.aspx
[Premier]: https://www.microsoft.com/en-us/microsoftservices/support.aspx
[enterprise-agreement]: https://www.microsoft.com/en-us/licensing/licensing-programs/enterprise.aspx
[assurance]: https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx
[podpora komunity]: https://github.com/powershell/powershell/issues
[community support]: https://github.com/powershell/powershell/issues
[Microsoft Community]: https://answers.microsoft.com/
[technické komunity Powershellu]: https://techcommunity.microsoft.com/t5/PowerShell/ct-p/WindowsPowerShell
[PowerShell Tech Community]: https://techcommunity.microsoft.com/t5/PowerShell/ct-p/WindowsPowerShell
[odbornou pomoc]: https://support.microsoft.com/assistedsupportproducts
[assisted support]: https://support.microsoft.com/assistedsupportproducts
[modern]: https://support.microsoft.com/help/30881/modern-lifecycle-policy
[lifecycle-chart]: ./images/modern-lifecycle.png
[semi-annual]: https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview
[licencí MIT]: https://github.com/PowerShell/PowerShell/blob/master/LICENSE.txt
[MIT license]: https://github.com/PowerShell/PowerShell/blob/master/LICENSE.txt
[`WindowsPSModulePath`]: https://www.powershellgallery.com/packages/WindowsPSModulePath/