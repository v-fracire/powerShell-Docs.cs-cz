---
title: Životní cyklus podpory PowerShellu Core
description: Zásady, kterými se řídí podporu pro prostředí PowerShell Core
ms.date: 08/06/2018
ms.openlocfilehash: 2e0ca1b9c133e6f316a40aff13365d0489059165
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404108"
---
# <a name="powershell-core-support-lifecycle"></a><span data-ttu-id="4c1af-103">Životní cyklus podpory PowerShellu Core</span><span class="sxs-lookup"><span data-stu-id="4c1af-103">PowerShell Core Support Lifecycle</span></span>

<span data-ttu-id="4c1af-104">PowerShell Core je odlišnou sadu nástrojů a komponenty, které je dodán, nainstalovat a nakonfigurovat samostatně z prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4c1af-104">PowerShell Core is a distinct set of tools and components that is shipped, installed, and configured separately from Windows PowerShell.</span></span>
<span data-ttu-id="4c1af-105">PowerShell Core není proto součástí licenční smlouvy Windows 7/8.1/10 nebo Windows Server.</span><span class="sxs-lookup"><span data-stu-id="4c1af-105">Therefore, PowerShell Core is not included in the Windows 7/8.1/10 or Windows Server licensing agreements.</span></span>

<span data-ttu-id="4c1af-106">PowerShell Core je však podporováno v tradiční Microsoft smlouvy o podpoře, včetně [Premier][], [smlouvy Microsoft Enterprise][enterprise-agreement]a [Programu Microsoft Software Assurance][assurance].</span><span class="sxs-lookup"><span data-stu-id="4c1af-106">However, PowerShell Core is supported under traditional Microsoft support agreements, including [Premier][], [Microsoft Enterprise Agreements][enterprise-agreement], and [Microsoft Software Assurance][assurance].</span></span>
<span data-ttu-id="4c1af-107">Můžete také platit [podpora s asistencí][] pro PowerShell Core vyplněním žádosti o podporu pro váš problém.</span><span class="sxs-lookup"><span data-stu-id="4c1af-107">You can also pay for [assisted support][] for PowerShell Core by filing a support request for your problem.</span></span>

<span data-ttu-id="4c1af-108">Nabízíme také [Podpora komunity][] na Githubu, kde můžete soubor problému, chyby nebo žádost o funkci.</span><span class="sxs-lookup"><span data-stu-id="4c1af-108">We also offer [community support][] on GitHub where you can file an issue, bug, or feature request.</span></span>
<span data-ttu-id="4c1af-109">Alternativně můžete zjistit pomoc od ostatních členů komunity na Obecné [Microsoft Community][] nebo Microsoft [Prostředí PowerShell technické komunity][].</span><span class="sxs-lookup"><span data-stu-id="4c1af-109">Alternatively, you may find help from other members of the community on the general [Microsoft Community][] or the Microsoft [PowerShell Tech Community][].</span></span>
<span data-ttu-id="4c1af-110">Nabízíme-zaručeno existuje, že váš problém bude řešit nebo vyřešení v časovém limitu.</span><span class="sxs-lookup"><span data-stu-id="4c1af-110">We offer no guarantee there that your issue will be addressed or resolved in a timely manner.</span></span>
<span data-ttu-id="4c1af-111">Pokud máte problém vyžadující okamžitou pozornost, měli byste použít tradiční, placené možnosti podpory.</span><span class="sxs-lookup"><span data-stu-id="4c1af-111">If you have a problem that requires immediate attention, you should use the traditional, paid support options.</span></span>

## <a name="lifecycle-of-powershell-core"></a><span data-ttu-id="4c1af-112">Životní cyklus Powershellu Core</span><span class="sxs-lookup"><span data-stu-id="4c1af-112">Lifecycle of PowerShell Core</span></span>

<span data-ttu-id="4c1af-113">PowerShell Core se seznámíte s požadavky [moderní životní cyklus Microsoft][modern].</span><span class="sxs-lookup"><span data-stu-id="4c1af-113">PowerShell Core is adopting the [Microsoft Modern Lifecycle Policy][modern].</span></span>
<span data-ttu-id="4c1af-114">Tento životní cyklus podpory má Informujte zákazníky o nejnovější verze.</span><span class="sxs-lookup"><span data-stu-id="4c1af-114">This support lifecycle is intended to keep customers up-to-date with the latest versions.</span></span>

<span data-ttu-id="4c1af-115">Větev verze 6.x PowerShell Core aktualizují přibližně jednou za šest měsíců (např. 6.0, 6.1, 6.2, atd.)</span><span class="sxs-lookup"><span data-stu-id="4c1af-115">The version 6.x branch of PowerShell Core will be updated approximately once every six months (e.g. 6.0, 6.1, 6.2, etc.)</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4c1af-116">Je nutné aktualizovat do šesti měsíců po vydání každý nový dílčí verze, chcete-li i nadále zajistit podporu.</span><span class="sxs-lookup"><span data-stu-id="4c1af-116">You must update within six months after each new minor version release to continue receiving support.</span></span>

<span data-ttu-id="4c1af-117">Například pokud 1. července 2018, se uvolní prostředí PowerShell Core 6.1 by být očekáváte aktualizaci do prostředí PowerShell Core 6.1 1. ledna 2019 kvůli zachování podpory.</span><span class="sxs-lookup"><span data-stu-id="4c1af-117">For example, if PowerShell Core 6.1 is released on July 1st, 2018, you would be expected to update to PowerShell Core 6.1 by January 1st, 2019 to maintain support.</span></span>

![Životní cyklus větev Powershellu Core][lifecycle-chart]

<span data-ttu-id="4c1af-119">Moderní zásady životního cyklu také vyžaduje, aby Microsoft oznámit zákazníkům 12 měsíců před ukončením odborné pomoci pro produkt (tj. PowerShell Core).</span><span class="sxs-lookup"><span data-stu-id="4c1af-119">The Modern Lifecycle Policy also requires that Microsoft give customers 12 months notice before discontinuing support for a product (i.e. PowerShell Core).</span></span>

<span data-ttu-id="4c1af-120">Nakonec Očekáváme, že přijímají PowerShell Core "dlouhodobé údržby" zůstat podporována v konkrétní větvi nebo verze 6.x aktualizuje přístupu, kde by vyžadujeme pouze pro obsluhu a zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="4c1af-120">Eventually, we expect PowerShell Core will adopt the "long-term servicing" approach where we would require only servicing and security updates to stay in support on a specific branch/version of 6.x.</span></span>

## <a name="supported-platforms"></a><span data-ttu-id="4c1af-121">Podporované platformy</span><span class="sxs-lookup"><span data-stu-id="4c1af-121">Supported platforms</span></span>

<span data-ttu-id="4c1af-122">Podrobnosti najdete v následující tabulce zobrazíte jaké platformy je oficiálně podporované verze prostředí PowerShell Core používáte.</span><span class="sxs-lookup"><span data-stu-id="4c1af-122">Please see the following table to see what platform the version of PowerShell Core you are using is officially supported.</span></span>

<span data-ttu-id="4c1af-123">Naše komunita také přidal balíčky pro některé platformy, ale nejsou oficiálně podporované.</span><span class="sxs-lookup"><span data-stu-id="4c1af-123">Our community has also contributed packages for some platforms, but they are not officially supported.</span></span>
<span data-ttu-id="4c1af-124">Tyto balíčky jsou označeny jako `Community` v tabulce.</span><span class="sxs-lookup"><span data-stu-id="4c1af-124">These packages are marked as `Community` in the table.</span></span>

<span data-ttu-id="4c1af-125">Uvedené jako platformy `Experimental` nejsou oficiálně podporované, ale jsou k dispozici pro experimentování ve službě a zpětnou vazbu.</span><span class="sxs-lookup"><span data-stu-id="4c1af-125">Platforms listed as `Experimental` are not officially supported, but are available for experimentation and feedback.</span></span>

|                                                   | <span data-ttu-id="4c1af-126">6.0</span><span class="sxs-lookup"><span data-stu-id="4c1af-126">6.0</span></span>         | <span data-ttu-id="4c1af-127">6.1</span><span class="sxs-lookup"><span data-stu-id="4c1af-127">6.1</span></span>         |
|---------------------------------------------------|:-----------:|:-----------:|
| <span data-ttu-id="4c1af-128">Windows 7, 8.1 a 10</span><span class="sxs-lookup"><span data-stu-id="4c1af-128">Windows 7, 8.1, and 10</span></span>                            | <span data-ttu-id="4c1af-129">Podporované</span><span class="sxs-lookup"><span data-stu-id="4c1af-129">Supported</span></span>   | <span data-ttu-id="4c1af-130">Podporované</span><span class="sxs-lookup"><span data-stu-id="4c1af-130">Supported</span></span>   |
| <span data-ttu-id="4c1af-131">Windows Server 2008 R2, 2012 R2, 2016</span><span class="sxs-lookup"><span data-stu-id="4c1af-131">Windows Server 2008 R2, 2012 R2, 2016</span></span>             | <span data-ttu-id="4c1af-132">Podporované</span><span class="sxs-lookup"><span data-stu-id="4c1af-132">Supported</span></span>   | <span data-ttu-id="4c1af-133">Podporované</span><span class="sxs-lookup"><span data-stu-id="4c1af-133">Supported</span></span>   |
| <span data-ttu-id="4c1af-134">[Windows Server prostřednictvím půlročního kanálu][semi-annual]</span><span class="sxs-lookup"><span data-stu-id="4c1af-134">[Windows Server Semi-Annual Channel][semi-annual]</span></span> | <span data-ttu-id="4c1af-135">Podporované</span><span class="sxs-lookup"><span data-stu-id="4c1af-135">Supported</span></span>   | <span data-ttu-id="4c1af-136">Podporované</span><span class="sxs-lookup"><span data-stu-id="4c1af-136">Supported</span></span>   |
| <span data-ttu-id="4c1af-137">Ubuntu 14.04 a 16.04</span><span class="sxs-lookup"><span data-stu-id="4c1af-137">Ubuntu 14.04 and, 16.04</span></span>                           | <span data-ttu-id="4c1af-138">Podporované</span><span class="sxs-lookup"><span data-stu-id="4c1af-138">Supported</span></span>   | <span data-ttu-id="4c1af-139">Podporované</span><span class="sxs-lookup"><span data-stu-id="4c1af-139">Supported</span></span>   |
| <span data-ttu-id="4c1af-140">Ubuntu 18.04</span><span class="sxs-lookup"><span data-stu-id="4c1af-140">Ubuntu 18.04</span></span>                                      |             | <span data-ttu-id="4c1af-141">Podporované</span><span class="sxs-lookup"><span data-stu-id="4c1af-141">Supported</span></span>   |
| <span data-ttu-id="4c1af-142">Ubuntu 18.10 (prostřednictvím přichycení balíček)</span><span class="sxs-lookup"><span data-stu-id="4c1af-142">Ubuntu 18.10 (via Snap Package)</span></span>                   |             | <span data-ttu-id="4c1af-143">Komunita</span><span class="sxs-lookup"><span data-stu-id="4c1af-143">Community</span></span>   |
| <span data-ttu-id="4c1af-144">Debian 8.7 + a 9</span><span class="sxs-lookup"><span data-stu-id="4c1af-144">Debian 8.7+, and 9</span></span>                                | <span data-ttu-id="4c1af-145">Podporované</span><span class="sxs-lookup"><span data-stu-id="4c1af-145">Supported</span></span>   | <span data-ttu-id="4c1af-146">Podporované</span><span class="sxs-lookup"><span data-stu-id="4c1af-146">Supported</span></span>   |
| <span data-ttu-id="4c1af-147">CentOS 7</span><span class="sxs-lookup"><span data-stu-id="4c1af-147">CentOS 7</span></span>                                          | <span data-ttu-id="4c1af-148">Podporované</span><span class="sxs-lookup"><span data-stu-id="4c1af-148">Supported</span></span>   | <span data-ttu-id="4c1af-149">Podporované</span><span class="sxs-lookup"><span data-stu-id="4c1af-149">Supported</span></span>   |
| <span data-ttu-id="4c1af-150">Red Hat Enterprise Linux 7</span><span class="sxs-lookup"><span data-stu-id="4c1af-150">Red Hat Enterprise Linux 7</span></span>                        | <span data-ttu-id="4c1af-151">Podporované</span><span class="sxs-lookup"><span data-stu-id="4c1af-151">Supported</span></span>   | <span data-ttu-id="4c1af-152">Podporované</span><span class="sxs-lookup"><span data-stu-id="4c1af-152">Supported</span></span>   |
| <span data-ttu-id="4c1af-153">OpenSUSE 42.3</span><span class="sxs-lookup"><span data-stu-id="4c1af-153">OpenSUSE 42.3</span></span>                                     | <span data-ttu-id="4c1af-154">Podporované</span><span class="sxs-lookup"><span data-stu-id="4c1af-154">Supported</span></span>   | <span data-ttu-id="4c1af-155">Podporované</span><span class="sxs-lookup"><span data-stu-id="4c1af-155">Supported</span></span>   |
| <span data-ttu-id="4c1af-156">Fedora 27</span><span class="sxs-lookup"><span data-stu-id="4c1af-156">Fedora 27</span></span>                                         | <span data-ttu-id="4c1af-157">Podporované</span><span class="sxs-lookup"><span data-stu-id="4c1af-157">Supported</span></span>   | <span data-ttu-id="4c1af-158">Podporované</span><span class="sxs-lookup"><span data-stu-id="4c1af-158">Supported</span></span>   |
| <span data-ttu-id="4c1af-159">Fedora 28</span><span class="sxs-lookup"><span data-stu-id="4c1af-159">Fedora 28</span></span>                                         |             | <span data-ttu-id="4c1af-160">Podporované</span><span class="sxs-lookup"><span data-stu-id="4c1af-160">Supported</span></span>   |
| <span data-ttu-id="4c1af-161">macOS 10.12 +</span><span class="sxs-lookup"><span data-stu-id="4c1af-161">macOS 10.12+</span></span>                                      | <span data-ttu-id="4c1af-162">Podporované</span><span class="sxs-lookup"><span data-stu-id="4c1af-162">Supported</span></span>   | <span data-ttu-id="4c1af-163">Podporované</span><span class="sxs-lookup"><span data-stu-id="4c1af-163">Supported</span></span>   |
| <span data-ttu-id="4c1af-164">Architektura</span><span class="sxs-lookup"><span data-stu-id="4c1af-164">Arch</span></span>                                              | <span data-ttu-id="4c1af-165">Komunita</span><span class="sxs-lookup"><span data-stu-id="4c1af-165">Community</span></span>   | <span data-ttu-id="4c1af-166">Komunita</span><span class="sxs-lookup"><span data-stu-id="4c1af-166">Community</span></span>   |
| <span data-ttu-id="4c1af-167">Raspbian</span><span class="sxs-lookup"><span data-stu-id="4c1af-167">Raspbian</span></span>                                          | <span data-ttu-id="4c1af-168">Experimentální</span><span class="sxs-lookup"><span data-stu-id="4c1af-168">Experimental</span></span>| <span data-ttu-id="4c1af-169">Komunita</span><span class="sxs-lookup"><span data-stu-id="4c1af-169">Community</span></span>   |
| <span data-ttu-id="4c1af-170">Kali</span><span class="sxs-lookup"><span data-stu-id="4c1af-170">Kali</span></span>                                              | <span data-ttu-id="4c1af-171">Komunita</span><span class="sxs-lookup"><span data-stu-id="4c1af-171">Community</span></span>   | <span data-ttu-id="4c1af-172">Komunita</span><span class="sxs-lookup"><span data-stu-id="4c1af-172">Community</span></span>   |
| <span data-ttu-id="4c1af-173">AppImage (funguje na různých platformách Linux)</span><span class="sxs-lookup"><span data-stu-id="4c1af-173">AppImage  (works on multiple Linux platforms)</span></span>     | <span data-ttu-id="4c1af-174">Komunita</span><span class="sxs-lookup"><span data-stu-id="4c1af-174">Community</span></span>   | <span data-ttu-id="4c1af-175">Komunita</span><span class="sxs-lookup"><span data-stu-id="4c1af-175">Community</span></span>   |
| [<span data-ttu-id="4c1af-176">Přichytit balíčku</span><span class="sxs-lookup"><span data-stu-id="4c1af-176">Snap Package</span></span>](https://snapcraft.io/powershell)   | <span data-ttu-id="4c1af-177">Další informace v poznámce</span><span class="sxs-lookup"><span data-stu-id="4c1af-177">See note</span></span>    | <span data-ttu-id="4c1af-178">Další informace v poznámce</span><span class="sxs-lookup"><span data-stu-id="4c1af-178">See note</span></span>    |

> [!NOTE]
> <span data-ttu-id="4c1af-179">Přichytit balíčky budou experimentální určitou dobu.</span><span class="sxs-lookup"><span data-stu-id="4c1af-179">Snap packages will be experimental for a period.</span></span>  <span data-ttu-id="4c1af-180">Po jsme si jisti, že Snap nezavádí nové problémy podpory, podpora bude následovat distribuci, kterou používáte balíček na.</span><span class="sxs-lookup"><span data-stu-id="4c1af-180">After, we are confident that Snap does not introduce new support issues, the support will follow the distribution you are running the package on.</span></span>

## <a name="platform-which-are-out-of-support"></a><span data-ttu-id="4c1af-181">Platforma, která už skončila podpora</span><span class="sxs-lookup"><span data-stu-id="4c1af-181">Platform which are out of support</span></span>

<span data-ttu-id="4c1af-182">Ukončení životnosti technologie definovaným vlastníkem platformy dosáhne verze platformy PowerShell Core přestane také k poskytování podpory pro tuto verzi platformy.</span><span class="sxs-lookup"><span data-stu-id="4c1af-182">When a platform version reaches end-of-life as defined by the platform owner, PowerShell Core will also cease to provide support for that platform version.</span></span> <span data-ttu-id="4c1af-183">Dříve vydané balíčky zůstávají dostupné i pro zákazníky, kteří potřebují přístup, ale formální podpory a aktualizace jakéhokoli druhu už, poskytneme vám.</span><span class="sxs-lookup"><span data-stu-id="4c1af-183">Previously released packages will remain available for customers needing access but formal support and updates of any kind will no longer be provided.</span></span>

<span data-ttu-id="4c1af-184">Proto podpora pro tyto verze vlastníky distribuce softwaru bylo ukončeno a nejsou podporovány.</span><span class="sxs-lookup"><span data-stu-id="4c1af-184">Therefore, support for the following versions was ended by the distribution owners and are not supported.</span></span>

| <span data-ttu-id="4c1af-185">Operační systém</span><span class="sxs-lookup"><span data-stu-id="4c1af-185">OS</span></span>       | <span data-ttu-id="4c1af-186">Verze</span><span class="sxs-lookup"><span data-stu-id="4c1af-186">Version</span></span> | <span data-ttu-id="4c1af-187">Ukončení životnosti</span><span class="sxs-lookup"><span data-stu-id="4c1af-187">End of Life</span></span>                                                                                 |
|----------|---------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="4c1af-188">Fedora</span><span class="sxs-lookup"><span data-stu-id="4c1af-188">Fedora</span></span>   | <span data-ttu-id="4c1af-189">24</span><span class="sxs-lookup"><span data-stu-id="4c1af-189">24</span></span>      | [<span data-ttu-id="4c1af-190">Ze srpna 2017</span><span class="sxs-lookup"><span data-stu-id="4c1af-190">August 2017</span></span>](https://fedoramagazine.org/fedora-24-eol/)                                    |
| <span data-ttu-id="4c1af-191">Fedora</span><span class="sxs-lookup"><span data-stu-id="4c1af-191">Fedora</span></span>   | <span data-ttu-id="4c1af-192">25</span><span class="sxs-lookup"><span data-stu-id="4c1af-192">25</span></span>      | [<span data-ttu-id="4c1af-193">. Prosince 2017</span><span class="sxs-lookup"><span data-stu-id="4c1af-193">December 2017</span></span>](https://fedoramagazine.org/fedora-25-end-life/)                             |
| <span data-ttu-id="4c1af-194">Fedora</span><span class="sxs-lookup"><span data-stu-id="4c1af-194">Fedora</span></span>   | <span data-ttu-id="4c1af-195">26</span><span class="sxs-lookup"><span data-stu-id="4c1af-195">26</span></span>      | [<span data-ttu-id="4c1af-196">. Května 2018.</span><span class="sxs-lookup"><span data-stu-id="4c1af-196">May 2018</span></span>](https://fedoramagazine.org/fedora-26-end-life/)                                  |
| <span data-ttu-id="4c1af-197">OpenSUSE</span><span class="sxs-lookup"><span data-stu-id="4c1af-197">openSUSE</span></span> | <span data-ttu-id="4c1af-198">42.1</span><span class="sxs-lookup"><span data-stu-id="4c1af-198">42.1</span></span>    | [<span data-ttu-id="4c1af-199">Květen 2017</span><span class="sxs-lookup"><span data-stu-id="4c1af-199">May 2017</span></span>](https://lists.opensuse.org/opensuse-security-announce/2017-05/msg00053.html)     |
| <span data-ttu-id="4c1af-200">OpenSUSE</span><span class="sxs-lookup"><span data-stu-id="4c1af-200">openSUSE</span></span> | <span data-ttu-id="4c1af-201">42.2</span><span class="sxs-lookup"><span data-stu-id="4c1af-201">42.2</span></span>    | [<span data-ttu-id="4c1af-202">. Ledna 2018</span><span class="sxs-lookup"><span data-stu-id="4c1af-202">January 2018</span></span>](https://lists.opensuse.org/opensuse-security-announce/2017-11/msg00066.html) |
| <span data-ttu-id="4c1af-203">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="4c1af-203">Ubuntu</span></span>   | <span data-ttu-id="4c1af-204">16.10</span><span class="sxs-lookup"><span data-stu-id="4c1af-204">16.10</span></span>   | [<span data-ttu-id="4c1af-205">. Července 2017</span><span class="sxs-lookup"><span data-stu-id="4c1af-205">July 2017</span></span>](https://lists.ubuntu.com/archives/ubuntu-announce/2017-July/000223.html)        |
| <span data-ttu-id="4c1af-206">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="4c1af-206">Ubuntu</span></span>   | <span data-ttu-id="4c1af-207">č. 17.04</span><span class="sxs-lookup"><span data-stu-id="4c1af-207">17.04</span></span>   | [<span data-ttu-id="4c1af-208">. Ledna 2018</span><span class="sxs-lookup"><span data-stu-id="4c1af-208">January 2018</span></span>](https://lists.ubuntu.com/archives/ubuntu-announce/2018-January.txt)          |
| <span data-ttu-id="4c1af-209">Ubuntu</span><span class="sxs-lookup"><span data-stu-id="4c1af-209">Ubuntu</span></span>   | <span data-ttu-id="4c1af-210">17.10</span><span class="sxs-lookup"><span data-stu-id="4c1af-210">17.10</span></span>   | [<span data-ttu-id="4c1af-211">. Července 2018</span><span class="sxs-lookup"><span data-stu-id="4c1af-211">July 2018</span></span>](https://lists.ubuntu.com/archives/ubuntu-announce/2018-July/000232.html)        |

## <a name="notes-on-licensing"></a><span data-ttu-id="4c1af-212">Poznámky k licencování</span><span class="sxs-lookup"><span data-stu-id="4c1af-212">Notes on licensing</span></span>

<span data-ttu-id="4c1af-213">PowerShell Core je vydávaný v rámci [licencí MIT][].</span><span class="sxs-lookup"><span data-stu-id="4c1af-213">PowerShell Core is released under the [MIT license][].</span></span>
<span data-ttu-id="4c1af-214">V rámci této licence a bez smlouvy placená odborná pomoc. Uživatelé jsou omezené na [Podpora komunity][].</span><span class="sxs-lookup"><span data-stu-id="4c1af-214">Under this license, and in the absence of a paid support agreement, users are limited to [community support][].</span></span>
<span data-ttu-id="4c1af-215">Podpora komunity Microsoft neposkytuje žádnou záruku rychlosti odezvy nebo opravy.</span><span class="sxs-lookup"><span data-stu-id="4c1af-215">With community support, Microsoft makes no guarantees of responsiveness or fixes.</span></span>

## <a name="windows-powershell-module"></a><span data-ttu-id="4c1af-216">Modul Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="4c1af-216">Windows PowerShell Module</span></span>

<span data-ttu-id="4c1af-217">Podpora pro PowerShell Core nerozšiřuje ostatní moduly produktu, pokud tyto moduly explicitně podporují PowerShell Core.</span><span class="sxs-lookup"><span data-stu-id="4c1af-217">Support for PowerShell Core does not extend to other product modules unless those modules explicitly support PowerShell Core.</span></span>
<span data-ttu-id="4c1af-218">Například použití `ActiveDirectory` modul, který se dodává jako součást systému Windows Server se o nepodporovaný scénář.</span><span class="sxs-lookup"><span data-stu-id="4c1af-218">For example, using the `ActiveDirectory` module that ships as part of Windows Server is an unsupported scenario.</span></span>

<span data-ttu-id="4c1af-219">Moduly, které nepodporují explicitně PowerShell Core však může být v některých případech kompatibilní.</span><span class="sxs-lookup"><span data-stu-id="4c1af-219">However, modules that do not explicitly support PowerShell Core may be compatible in some cases.</span></span>
<span data-ttu-id="4c1af-220">Po instalaci [ `WindowsPSModulePath` ][] modulu, prostředí Windows PowerShell můžete připojit `PSModulePath` k Powershellu Core `PSModulePath`.</span><span class="sxs-lookup"><span data-stu-id="4c1af-220">By installing the [`WindowsPSModulePath`][] module, you can append the Windows PowerShell `PSModulePath` to your PowerShell Core `PSModulePath`.</span></span>

<span data-ttu-id="4c1af-221">Nejdřív nainstalujte `WindowsPSModulePath` modulu z Galerie prostředí PowerShell:</span><span class="sxs-lookup"><span data-stu-id="4c1af-221">First, install the `WindowsPSModulePath` module from the PowerShell Gallery:</span></span>

```powershell
# Add `-Scope CurrentUser` if you're installing as non-admin
Install-Module WindowsPSModulePath -Force
```

<span data-ttu-id="4c1af-222">Po instalaci tohoto modulu, spusťte `Add-WindowsPSModulePath` rutiny prostředí Windows PowerShell přidat `PSModulePath` do prostředí PowerShell Core:</span><span class="sxs-lookup"><span data-stu-id="4c1af-222">After installing this module, run the `Add-WindowsPSModulePath` cmdlet to add the Windows PowerShell `PSModulePath` to PowerShell Core:</span></span>

```powershell
# Add this line to your profile if you always want Windows PowerShell PSModulePath
Add-WindowsPSModulePath
```

[Premier]: https://www.microsoft.com/en-us/microsoftservices/support.aspx
[enterprise-agreement]: https://www.microsoft.com/en-us/licensing/licensing-programs/enterprise.aspx
[assurance]: https://www.microsoft.com/en-us/licensing/licensing-programs/software-assurance-default.aspx
[Podpora komunity]: https://github.com/powershell/powershell/issues
[community support]: https://github.com/powershell/powershell/issues
[Microsoft Community]: https://answers.microsoft.com/
[Prostředí PowerShell technické komunity]: https://techcommunity.microsoft.com/t5/PowerShell/ct-p/WindowsPowerShell
[PowerShell Tech Community]: https://techcommunity.microsoft.com/t5/PowerShell/ct-p/WindowsPowerShell
[podpora s asistencí]: https://support.microsoft.com/assistedsupportproducts
[assisted support]: https://support.microsoft.com/assistedsupportproducts
[modern]: https://support.microsoft.com/help/30881/modern-lifecycle-policy
[lifecycle-chart]: ./images/modern-lifecycle.png
[semi-annual]: https://docs.microsoft.com/windows-server/get-started/semi-annual-channel-overview
[licencí MIT]: https://github.com/PowerShell/PowerShell/blob/master/LICENSE.txt
[MIT license]: https://github.com/PowerShell/PowerShell/blob/master/LICENSE.txt
["WindowsPSModulePath.]: https://www.powershellgallery.com/packages/WindowsPSModulePath/
[`WindowsPSModulePath`]: https://www.powershellgallery.com/packages/WindowsPSModulePath/
