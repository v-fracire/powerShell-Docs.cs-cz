---
ms.topic: reference
keywords: rutiny prostředí PowerShell
ms.date: 12/12/2016
title: Add-PswaAuthorizationRule
schema: 2.0.0
ms.openlocfilehash: a8904ac36f7fd9fe3c649ad4ca709a98c31b63c3
ms.sourcegitcommit: 77f62a55cac8c13d69d51eef5fade18f71d66955
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/17/2018
ms.locfileid: "39094224"
---
# <a name="add-pswaauthorizationrule"></a><span data-ttu-id="103d2-103">Add-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="103d2-103">Add-PswaAuthorizationRule</span></span>

## <a name="synopsis"></a><span data-ttu-id="103d2-104">SOUHRN</span><span class="sxs-lookup"><span data-stu-id="103d2-104">SYNOPSIS</span></span>

<span data-ttu-id="103d2-105">Přidá nové autorizační pravidlo sada pravidel autorizace pro Windows PowerShell® Web Accessu.</span><span class="sxs-lookup"><span data-stu-id="103d2-105">Adds a new authorization rule to the Windows PowerShell® Web Access authorization rule set.</span></span>

## <a name="syntax"></a><span data-ttu-id="103d2-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="103d2-106">Syntax</span></span>

### <a name="usergroupnamecomputergroupname"></a><span data-ttu-id="103d2-107">UserGroupNameComputerGroupName</span><span class="sxs-lookup"><span data-stu-id="103d2-107">UserGroupNameComputerGroupName</span></span>

```
Add-PswaAuthorizationRule -ComputerGroupName <String> -ConfigurationName <String> -UserGroupName <String[]> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

### <a name="usergroupnamecomputername"></a><span data-ttu-id="103d2-108">UserGroupNameComputerName</span><span class="sxs-lookup"><span data-stu-id="103d2-108">UserGroupNameComputerName</span></span>

```
Add-PswaAuthorizationRule -ComputerName <String> -ConfigurationName <String> -UserGroupName <String[]> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

### <a name="usernamecomputergroupname"></a><span data-ttu-id="103d2-109">UserNameComputerGroupName</span><span class="sxs-lookup"><span data-stu-id="103d2-109">UserNameComputerGroupName</span></span>

```
Add-PswaAuthorizationRule [-UserName] <String[]> -ComputerGroupName <String> -ConfigurationName <String> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

### <a name="usernamecomputername"></a><span data-ttu-id="103d2-110">UserNameComputerName</span><span class="sxs-lookup"><span data-stu-id="103d2-110">UserNameComputerName</span></span>

```
Add-PswaAuthorizationRule [-UserName] <String[]> [-ComputerName] <String> [-ConfigurationName] <String> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

## <a name="description"></a><span data-ttu-id="103d2-111">POPIS</span><span class="sxs-lookup"><span data-stu-id="103d2-111">DESCRIPTION</span></span>

<span data-ttu-id="103d2-112">**Add-PswaAuthorizationRule** rutina přidá nové autorizační pravidlo do sada pravidel autorizace pro Windows PowerShell® Web Accessu.</span><span class="sxs-lookup"><span data-stu-id="103d2-112">The **Add-PswaAuthorizationRule** cmdlet adds a new authorization rule to the Windows PowerShell® Web Access authorization rule set.</span></span>

<span data-ttu-id="103d2-113">Musíte zadat uživatelů, počítačů a prostředí Windows PowerShell koncové body pro toto pravidlo.</span><span class="sxs-lookup"><span data-stu-id="103d2-113">You must specify the users, computers, and Windows PowerShell endpoints for this rule.</span></span> <span data-ttu-id="103d2-114">Můžete určit uživatele a počítače jednotlivých uživatelských účtů a názvy počítačů nebo zadáním skupiny.</span><span class="sxs-lookup"><span data-stu-id="103d2-114">You can specify both users and computers either by individual user accounts and computer names, or by specifying groups.</span></span>

<span data-ttu-id="103d2-115">Pro počítač, který je připojený k doméně služby Active Directory rutina k vytvoření pravidla používá identifikátor zabezpečení (SID) počítače.</span><span class="sxs-lookup"><span data-stu-id="103d2-115">For a computer that is joined to an Active Directory domain, the cmdlet uses the security identifier (SID) of the computer to create the rule.</span></span>
<span data-ttu-id="103d2-116">Díky tomu můžete použít krátký název, plně kvalifikovaný název domény (FQDN) nebo IP adresu pro **název_počítače** na přihlašovací stránku.</span><span class="sxs-lookup"><span data-stu-id="103d2-116">This allows you to use a short name, a fully qualified domain name (FQDN), or an IP address for the **Computer Name** field on the sign-in page.</span></span>

<span data-ttu-id="103d2-117">Pro počítač, který není připojený k doméně služby Active Directory rutina vytvoří pravidlo s použitím názvu počítače program od správce.</span><span class="sxs-lookup"><span data-stu-id="103d2-117">For a computer that is not joined to an Active Directory domain, the cmdlet creates the rule using the computer name provided by the administrator.</span></span> <span data-ttu-id="103d2-118">K úspěšnému připojení k tomuto počítači, musí koncový uživatel poskytnutí názvu počítače, v naprosto stejném tvaru v pravidle.</span><span class="sxs-lookup"><span data-stu-id="103d2-118">To successfully connect to this machine, the end user must provide the computer name exactly as it appears in the rule.</span></span>

<span data-ttu-id="103d2-119">Pokud existuje více počítačů se stejným názvem v síti, krátký název lze přeložit na více než jednom počítači.</span><span class="sxs-lookup"><span data-stu-id="103d2-119">If there are multiple computers with the same name on the network, then short name can resolve to more than one computer.</span></span> <span data-ttu-id="103d2-120">To může vést k nejednoznačnosti při navazování připojení.</span><span class="sxs-lookup"><span data-stu-id="103d2-120">This can lead to ambiguity when establishing a connection.</span></span> <span data-ttu-id="103d2-121">Například, pokud existuje pravidlo pro počítače pracovní skupiny s názvem "*Server1*" a nový počítač s názvem *"server1.contoso.com"* je připojen k síti a bude úspěšné ověření pomocí autorizačních pravidel a Windows PowerShell Web Accessu se pokusí navázat připojení k počítači s názvem "*Server1*".</span><span class="sxs-lookup"><span data-stu-id="103d2-121">For example, if a rule exists for the workgroup computer named "*Server1*” and a new computer named *server1.contoso.com* is joined to the network, validation using the authorization rules succeeds and Windows PowerShell Web Access attempts to establish a connection to the computer named “*Server1*”.</span></span> <span data-ttu-id="103d2-122">Není zaručeno, že se připojení k počítači pracovní skupiny zadaný; Tento pokus se může provést v pracovní skupině nebo doméně počítač s názvem "*Server1*".</span><span class="sxs-lookup"><span data-stu-id="103d2-122">It is not guaranteed that the connection is established with the specified workgroup computer; the attempt could be made on either the workgroup or the domain computer named "*Server1*".</span></span> <span data-ttu-id="103d2-123">Ke snížení nejednoznačnost, doporučujeme použít plně kvalifikovaný název pro cílový počítač pokaždé, když je možné vytvořit autorizační pravidlo.</span><span class="sxs-lookup"><span data-stu-id="103d2-123">To reduce ambiguity, it is recommended that you use the FQDN for the destination computer whenever possible to create an authorization rule.</span></span>

<span data-ttu-id="103d2-124">Autorizační pravidla vyhodnocení primární přihlašovací pověření uživatelů Windows PowerShell Web Accessu, ne alternativní přihlašovací údaje (součástí druhou sadu pověření **volitelná nastavení připojení** část přihlašovací stránka).</span><span class="sxs-lookup"><span data-stu-id="103d2-124">The authorization rules evaluate the primary sign-in credential of the Windows PowerShell Web Access users, not the alternate credentials (the second set of credentials found in the **Optional connection settings** section of the sign-in page).</span></span> <span data-ttu-id="103d2-125">Příkladem naleznete v příkladu 6.</span><span class="sxs-lookup"><span data-stu-id="103d2-125">For an example of this, see Example 6.</span></span>

## <a name="parameters"></a><span data-ttu-id="103d2-126">Parameters</span><span class="sxs-lookup"><span data-stu-id="103d2-126">Parameters</span></span>

### <a name="-computergroupname-string"></a><span data-ttu-id="103d2-127">-ComputerGroupName \<řetězec\></span><span class="sxs-lookup"><span data-stu-id="103d2-127">-ComputerGroupName \<String\></span></span>

<span data-ttu-id="103d2-128">Určuje název skupiny počítačů v Active Directory Domain Services (AD DS) nebo místních skupin, na které toto pravidlo udělí přístup.</span><span class="sxs-lookup"><span data-stu-id="103d2-128">Specifies the name of a computer group in Active Directory Domain Services (AD DS) or local groups to which this rule grants access.</span></span>

|||
|-|-|
| <span data-ttu-id="103d2-129">Aliasy</span><span class="sxs-lookup"><span data-stu-id="103d2-129">Aliases</span></span>                              | <span data-ttu-id="103d2-130">žádný</span><span class="sxs-lookup"><span data-stu-id="103d2-130">none</span></span>                                 |
| <span data-ttu-id="103d2-131">Povinné?</span><span class="sxs-lookup"><span data-stu-id="103d2-131">Required?</span></span>                            | <span data-ttu-id="103d2-132">Hodnota TRUE</span><span class="sxs-lookup"><span data-stu-id="103d2-132">true</span></span>                                 |
| <span data-ttu-id="103d2-133">Pozice?</span><span class="sxs-lookup"><span data-stu-id="103d2-133">Position?</span></span>                            | <span data-ttu-id="103d2-134">s názvem</span><span class="sxs-lookup"><span data-stu-id="103d2-134">named</span></span>                                |
| <span data-ttu-id="103d2-135">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="103d2-135">Default Value</span></span>                        | <span data-ttu-id="103d2-136">žádný</span><span class="sxs-lookup"><span data-stu-id="103d2-136">none</span></span>                                 |
| <span data-ttu-id="103d2-137">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="103d2-137">Accept Pipeline Input?</span></span>               | <span data-ttu-id="103d2-138">True (ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="103d2-138">True (ByPropertyName)</span></span>                |
| <span data-ttu-id="103d2-139">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="103d2-139">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="103d2-140">false</span><span class="sxs-lookup"><span data-stu-id="103d2-140">false</span></span>                                |

### <a name="-computername-string"></a><span data-ttu-id="103d2-141">-ComputerName \<řetězec\></span><span class="sxs-lookup"><span data-stu-id="103d2-141">-ComputerName \<String\></span></span>

<span data-ttu-id="103d2-142">Určuje název počítače, na které toto pravidlo udělí přístup.</span><span class="sxs-lookup"><span data-stu-id="103d2-142">Specifies the computer name to which this rule grants access.</span></span>

|||
|-|-|
| <span data-ttu-id="103d2-143">Aliasy</span><span class="sxs-lookup"><span data-stu-id="103d2-143">Aliases</span></span>                              | <span data-ttu-id="103d2-144">žádný</span><span class="sxs-lookup"><span data-stu-id="103d2-144">none</span></span>                                 |
| <span data-ttu-id="103d2-145">Povinné?</span><span class="sxs-lookup"><span data-stu-id="103d2-145">Required?</span></span>                            | <span data-ttu-id="103d2-146">Hodnota TRUE</span><span class="sxs-lookup"><span data-stu-id="103d2-146">true</span></span>                                 |
| <span data-ttu-id="103d2-147">Pozice?</span><span class="sxs-lookup"><span data-stu-id="103d2-147">Position?</span></span>                            | <span data-ttu-id="103d2-148">s názvem</span><span class="sxs-lookup"><span data-stu-id="103d2-148">named</span></span>                                |
| <span data-ttu-id="103d2-149">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="103d2-149">Default Value</span></span>                        | <span data-ttu-id="103d2-150">žádný</span><span class="sxs-lookup"><span data-stu-id="103d2-150">none</span></span>                                 |
| <span data-ttu-id="103d2-151">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="103d2-151">Accept Pipeline Input?</span></span>               | <span data-ttu-id="103d2-152">True (ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="103d2-152">True (ByPropertyName)</span></span>                |
| <span data-ttu-id="103d2-153">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="103d2-153">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="103d2-154">false</span><span class="sxs-lookup"><span data-stu-id="103d2-154">false</span></span>                                |

### <a name="-configurationname-string"></a><span data-ttu-id="103d2-155">– Při ConfigurationName \<řetězec\></span><span class="sxs-lookup"><span data-stu-id="103d2-155">-ConfigurationName \<String\></span></span>

<span data-ttu-id="103d2-156">Určuje název konfigurace relace prostředí Windows PowerShell, označované také jako prostředí runspace, do které toto pravidlo udělí přístup.</span><span class="sxs-lookup"><span data-stu-id="103d2-156">Specifies the name of the Windows PowerShell session configuration, also known as runspace, to which this rule grants access.</span></span>

|||
|-|-|
| <span data-ttu-id="103d2-157">Aliasy</span><span class="sxs-lookup"><span data-stu-id="103d2-157">Aliases</span></span>                              | <span data-ttu-id="103d2-158">žádný</span><span class="sxs-lookup"><span data-stu-id="103d2-158">none</span></span>                                 |
| <span data-ttu-id="103d2-159">Povinné?</span><span class="sxs-lookup"><span data-stu-id="103d2-159">Required?</span></span>                            | <span data-ttu-id="103d2-160">Hodnota TRUE</span><span class="sxs-lookup"><span data-stu-id="103d2-160">true</span></span>                                 |
| <span data-ttu-id="103d2-161">Pozice?</span><span class="sxs-lookup"><span data-stu-id="103d2-161">Position?</span></span>                            | <span data-ttu-id="103d2-162">s názvem</span><span class="sxs-lookup"><span data-stu-id="103d2-162">named</span></span>                                |
| <span data-ttu-id="103d2-163">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="103d2-163">Default Value</span></span>                        | <span data-ttu-id="103d2-164">žádný</span><span class="sxs-lookup"><span data-stu-id="103d2-164">none</span></span>                                 |
| <span data-ttu-id="103d2-165">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="103d2-165">Accept Pipeline Input?</span></span>               | <span data-ttu-id="103d2-166">True (ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="103d2-166">True (ByPropertyName)</span></span>                |
| <span data-ttu-id="103d2-167">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="103d2-167">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="103d2-168">false</span><span class="sxs-lookup"><span data-stu-id="103d2-168">false</span></span>                                |

### <a name="-credential--pscredential"></a><span data-ttu-id="103d2-169">-Credential \<PSCredential\></span><span class="sxs-lookup"><span data-stu-id="103d2-169">-Credential  \<PSCredential\></span></span>

<span data-ttu-id="103d2-170">Určuje **PSCredential** objektu pro uživatelský účet, který chcete použít ke změně Windows PowerShell Web Accessu autorizačních pravidel.</span><span class="sxs-lookup"><span data-stu-id="103d2-170">Specifies a **PSCredential** object for a user account that you want to use to change Windows PowerShell Web Access authorization rules.</span></span> <span data-ttu-id="103d2-171">Pokud nemůžete přidat tento parametr, rutina používá účet aktuálně přihlášeného uživatele.</span><span class="sxs-lookup"><span data-stu-id="103d2-171">If you do not add this parameter, the cmdlet uses the currently logged-on user account.</span></span> <span data-ttu-id="103d2-172">Chcete-li získat **PSCredential** objektu, který je potřeba přidat autorizační pravidla vzdáleně, spusťte [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential) rutiny.</span><span class="sxs-lookup"><span data-stu-id="103d2-172">To get a **PSCredential** object, which is required to add authorization rules remotely, run the [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential) cmdlet.</span></span>

|||
|-|-|
| <span data-ttu-id="103d2-173">Aliasy</span><span class="sxs-lookup"><span data-stu-id="103d2-173">Aliases</span></span>                              | <span data-ttu-id="103d2-174">žádný</span><span class="sxs-lookup"><span data-stu-id="103d2-174">none</span></span>                                 |
| <span data-ttu-id="103d2-175">Povinné?</span><span class="sxs-lookup"><span data-stu-id="103d2-175">Required?</span></span>                            | <span data-ttu-id="103d2-176">false</span><span class="sxs-lookup"><span data-stu-id="103d2-176">false</span></span>                                |
| <span data-ttu-id="103d2-177">Pozice?</span><span class="sxs-lookup"><span data-stu-id="103d2-177">Position?</span></span>                            | <span data-ttu-id="103d2-178">s názvem</span><span class="sxs-lookup"><span data-stu-id="103d2-178">named</span></span>                                |
| <span data-ttu-id="103d2-179">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="103d2-179">Default Value</span></span>                        | <span data-ttu-id="103d2-180">žádný</span><span class="sxs-lookup"><span data-stu-id="103d2-180">none</span></span>                                 |
| <span data-ttu-id="103d2-181">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="103d2-181">Accept Pipeline Input?</span></span>               | <span data-ttu-id="103d2-182">false</span><span class="sxs-lookup"><span data-stu-id="103d2-182">false</span></span>                                |
| <span data-ttu-id="103d2-183">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="103d2-183">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="103d2-184">false</span><span class="sxs-lookup"><span data-stu-id="103d2-184">false</span></span>                                |

### <a name="-force"></a><span data-ttu-id="103d2-185">-Force</span><span class="sxs-lookup"><span data-stu-id="103d2-185">-Force</span></span>

<span data-ttu-id="103d2-186">Vynutí příkazu ke spuštění bez nutnosti potvrzení uživatelem. \\</span><span class="sxs-lookup"><span data-stu-id="103d2-186">Forces the command to run without asking for user confirmation.\\</span></span>
<span data-ttu-id="103d2-187">Kromě toho se také zobrazí výzvu k potvrzení při zadání názvu počítače jednoduché nebo krátké (jako je například název, který není název domény nebo není plně kvalifikovaný).</span><span class="sxs-lookup"><span data-stu-id="103d2-187">In addition, it also prompts for confirmation when you enter a simple or short computer name (such as a name that is not a domain name or is not fully qualified).</span></span> <span data-ttu-id="103d2-188">Potvrzení je požadována z důvodu zabezpečení tak, aby jednoduchý název slouží k přidání počítače pouze v případě, že je počítač v pracovní skupině.</span><span class="sxs-lookup"><span data-stu-id="103d2-188">Confirmation is requested for security reasons, so that you can use the simple name to add a computer only if the computer is in a workgroup.</span></span>

|||
|-|-|
| <span data-ttu-id="103d2-189">Aliasy</span><span class="sxs-lookup"><span data-stu-id="103d2-189">Aliases</span></span>                              | <span data-ttu-id="103d2-190">žádný</span><span class="sxs-lookup"><span data-stu-id="103d2-190">none</span></span>                                 |
| <span data-ttu-id="103d2-191">Povinné?</span><span class="sxs-lookup"><span data-stu-id="103d2-191">Required?</span></span>                            | <span data-ttu-id="103d2-192">false</span><span class="sxs-lookup"><span data-stu-id="103d2-192">false</span></span>                                |
| <span data-ttu-id="103d2-193">Pozice?</span><span class="sxs-lookup"><span data-stu-id="103d2-193">Position?</span></span>                            | <span data-ttu-id="103d2-194">s názvem</span><span class="sxs-lookup"><span data-stu-id="103d2-194">named</span></span>                                |
| <span data-ttu-id="103d2-195">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="103d2-195">Default Value</span></span>                        | <span data-ttu-id="103d2-196">žádný</span><span class="sxs-lookup"><span data-stu-id="103d2-196">none</span></span>                                 |
| <span data-ttu-id="103d2-197">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="103d2-197">Accept Pipeline Input?</span></span>               | <span data-ttu-id="103d2-198">false</span><span class="sxs-lookup"><span data-stu-id="103d2-198">false</span></span>                                |
| <span data-ttu-id="103d2-199">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="103d2-199">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="103d2-200">false</span><span class="sxs-lookup"><span data-stu-id="103d2-200">false</span></span>                                |

### <a name="-rulename-string"></a><span data-ttu-id="103d2-201">-RuleName \<řetězec\></span><span class="sxs-lookup"><span data-stu-id="103d2-201">-RuleName \<String\></span></span>

<span data-ttu-id="103d2-202">Určuje popisný název pro toto pravidlo.</span><span class="sxs-lookup"><span data-stu-id="103d2-202">Specifies the friendly name for this rule.</span></span>

|||
|-|-|
| <span data-ttu-id="103d2-203">Aliasy</span><span class="sxs-lookup"><span data-stu-id="103d2-203">Aliases</span></span>                              | <span data-ttu-id="103d2-204">žádný</span><span class="sxs-lookup"><span data-stu-id="103d2-204">none</span></span>                                 |
| <span data-ttu-id="103d2-205">Povinné?</span><span class="sxs-lookup"><span data-stu-id="103d2-205">Required?</span></span>                            | <span data-ttu-id="103d2-206">false</span><span class="sxs-lookup"><span data-stu-id="103d2-206">false</span></span>                                |
| <span data-ttu-id="103d2-207">Pozice?</span><span class="sxs-lookup"><span data-stu-id="103d2-207">Position?</span></span>                            | <span data-ttu-id="103d2-208">s názvem</span><span class="sxs-lookup"><span data-stu-id="103d2-208">named</span></span>                                |
| <span data-ttu-id="103d2-209">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="103d2-209">Default Value</span></span>                        | <span data-ttu-id="103d2-210">žádný</span><span class="sxs-lookup"><span data-stu-id="103d2-210">none</span></span>                                 |
| <span data-ttu-id="103d2-211">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="103d2-211">Accept Pipeline Input?</span></span>               | <span data-ttu-id="103d2-212">True (ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="103d2-212">True (ByPropertyName)</span></span>                |
| <span data-ttu-id="103d2-213">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="103d2-213">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="103d2-214">false</span><span class="sxs-lookup"><span data-stu-id="103d2-214">false</span></span>                                |

### <a name="-usergroupname-string"></a><span data-ttu-id="103d2-215">-UserGroupName \<řetězec\[\]\></span><span class="sxs-lookup"><span data-stu-id="103d2-215">-UserGroupName \<String\[\]\></span></span>

<span data-ttu-id="103d2-216">Určuje název jedné nebo víc skupin uživatelů ve službě AD DS nebo místních skupin, na které toto pravidlo udělí přístup.</span><span class="sxs-lookup"><span data-stu-id="103d2-216">Specifies the name of one or more user groups in AD DS or local groups to which this rule grants access.</span></span>

|||
|-|-|
| <span data-ttu-id="103d2-217">Aliasy</span><span class="sxs-lookup"><span data-stu-id="103d2-217">Aliases</span></span>                              | <span data-ttu-id="103d2-218">žádný</span><span class="sxs-lookup"><span data-stu-id="103d2-218">none</span></span>                                 |
| <span data-ttu-id="103d2-219">Povinné?</span><span class="sxs-lookup"><span data-stu-id="103d2-219">Required?</span></span>                            | <span data-ttu-id="103d2-220">Hodnota TRUE</span><span class="sxs-lookup"><span data-stu-id="103d2-220">true</span></span>                                 |
| <span data-ttu-id="103d2-221">Pozice?</span><span class="sxs-lookup"><span data-stu-id="103d2-221">Position?</span></span>                            | <span data-ttu-id="103d2-222">s názvem</span><span class="sxs-lookup"><span data-stu-id="103d2-222">named</span></span>                                |
| <span data-ttu-id="103d2-223">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="103d2-223">Default Value</span></span>                        | <span data-ttu-id="103d2-224">žádný</span><span class="sxs-lookup"><span data-stu-id="103d2-224">none</span></span>                                 |
| <span data-ttu-id="103d2-225">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="103d2-225">Accept Pipeline Input?</span></span>               | <span data-ttu-id="103d2-226">True (ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="103d2-226">True (ByPropertyName)</span></span>                |
| <span data-ttu-id="103d2-227">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="103d2-227">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="103d2-228">false</span><span class="sxs-lookup"><span data-stu-id="103d2-228">false</span></span>                                |

### <a name="-username-string"></a><span data-ttu-id="103d2-229">-UserName \<řetězec\[\]\></span><span class="sxs-lookup"><span data-stu-id="103d2-229">-UserName \<String\[\]\></span></span>

<span data-ttu-id="103d2-230">Určuje jeden nebo více uživatelů, na které toto pravidlo udělí přístup.</span><span class="sxs-lookup"><span data-stu-id="103d2-230">Specifies one or more users to which this rule grants access.</span></span> <span data-ttu-id="103d2-231">Uživatelské jméno může být místní uživatelský účet na počítači brány nebo uživatel ve službě AD DS.</span><span class="sxs-lookup"><span data-stu-id="103d2-231">The user name can be a local user account on the gateway computer or a user in AD DS.</span></span>
<span data-ttu-id="103d2-232">Formát je `domain\user` nebo `computer\user`.</span><span class="sxs-lookup"><span data-stu-id="103d2-232">The format is `domain\user` or `computer\user`.</span></span>

|||
|-|-|
| <span data-ttu-id="103d2-233">Aliasy</span><span class="sxs-lookup"><span data-stu-id="103d2-233">Aliases</span></span>                              | <span data-ttu-id="103d2-234">žádný</span><span class="sxs-lookup"><span data-stu-id="103d2-234">none</span></span>                                 |
| <span data-ttu-id="103d2-235">Povinné?</span><span class="sxs-lookup"><span data-stu-id="103d2-235">Required?</span></span>                            | <span data-ttu-id="103d2-236">Hodnota TRUE</span><span class="sxs-lookup"><span data-stu-id="103d2-236">true</span></span>                                 |
| <span data-ttu-id="103d2-237">Pozice?</span><span class="sxs-lookup"><span data-stu-id="103d2-237">Position?</span></span>                            | <span data-ttu-id="103d2-238">1</span><span class="sxs-lookup"><span data-stu-id="103d2-238">1</span></span>                                    |
| <span data-ttu-id="103d2-239">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="103d2-239">Default Value</span></span>                        | <span data-ttu-id="103d2-240">žádný</span><span class="sxs-lookup"><span data-stu-id="103d2-240">none</span></span>                                 |
| <span data-ttu-id="103d2-241">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="103d2-241">Accept Pipeline Input?</span></span>               | <span data-ttu-id="103d2-242">True (ByValue, ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="103d2-242">True (ByValue, ByPropertyName)</span></span>       |
| <span data-ttu-id="103d2-243">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="103d2-243">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="103d2-244">false</span><span class="sxs-lookup"><span data-stu-id="103d2-244">false</span></span>                                |

###  <a name="commonparameters"></a><span data-ttu-id="103d2-245">\<CommonParameters\></span><span class="sxs-lookup"><span data-stu-id="103d2-245">\<CommonParameters\></span></span>

<span data-ttu-id="103d2-246">Tato rutina podporuje běžné parametry:-Verbose,-Debug, - ErrorAction, - ErrorVariable,-OutBuffer a - OutVariable.</span><span class="sxs-lookup"><span data-stu-id="103d2-246">This cmdlet supports the common parameters: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer, and -OutVariable.</span></span>
<span data-ttu-id="103d2-247">Další informace najdete v tématu [about_CommonParameters](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/about/about_commonparameters).</span><span class="sxs-lookup"><span data-stu-id="103d2-247">For more information, see [about_CommonParameters](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/about/about_commonparameters).</span></span>

## <a name="inputs"></a><span data-ttu-id="103d2-248">VSTUPY</span><span class="sxs-lookup"><span data-stu-id="103d2-248">INPUTS</span></span>

### <a name="string"></a><span data-ttu-id="103d2-249">Řetězec</span><span class="sxs-lookup"><span data-stu-id="103d2-249">String</span></span>

<span data-ttu-id="103d2-250">Tato rutina akceptuje jako vstupní řetězec nebo pole řetězců.</span><span class="sxs-lookup"><span data-stu-id="103d2-250">This cmdlet accepts a string or an array of strings as input.</span></span>

### <a name="string"></a><span data-ttu-id="103d2-251">Řetězec\[\]</span><span class="sxs-lookup"><span data-stu-id="103d2-251">String\[\]</span></span>

<span data-ttu-id="103d2-252">Tato rutina akceptuje jako vstupní řetězec nebo pole řetězců.</span><span class="sxs-lookup"><span data-stu-id="103d2-252">This cmdlet accepts a string or an array of strings as input.</span></span>

## <a name="outputs"></a><span data-ttu-id="103d2-253">Výstupy</span><span class="sxs-lookup"><span data-stu-id="103d2-253">Outputs</span></span>

### <a name="microsoftmanagementpowershellwebaccesspswaauthorizationrule"></a><span data-ttu-id="103d2-254">Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="103d2-254">Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule</span></span>

<span data-ttu-id="103d2-255">Tato rutina vrátí objektu pravidla autorizace.</span><span class="sxs-lookup"><span data-stu-id="103d2-255">This cmdlet returns the an authorization rule object.</span></span>

## <a name="examples"></a><span data-ttu-id="103d2-256">PŘÍKLADY</span><span class="sxs-lookup"><span data-stu-id="103d2-256">EXAMPLES</span></span>

### <a name="example-1"></a><span data-ttu-id="103d2-257">PŘÍKLAD 1</span><span class="sxs-lookup"><span data-stu-id="103d2-257">EXAMPLE 1</span></span>

<span data-ttu-id="103d2-258">Tento příklad uděluje přístup ke konfiguraci relace _Pswakoncovybod_, omezuje prostředí runspace _srv2_ pro uživatele v _SMAdmins_ skupiny.</span><span class="sxs-lookup"><span data-stu-id="103d2-258">This example grants access to the session configuration _PSWAEndpoint_, a restricted runspace, on _srv2_ for users in the _SMAdmins_ group.</span></span>

> [!NOTE]
> <span data-ttu-id="103d2-259">Název počítače musí být plně kvalifikovaný název domény (FQDN).</span><span class="sxs-lookup"><span data-stu-id="103d2-259">The computer name must be a fully qualified domain name (FQDN).</span></span> <span data-ttu-id="103d2-260">Správci definují konfiguraci relace s omezeným přístupem nebo prostředí runspace, což je omezeným rozsahem rutin a úloh, které koncoví uživatelé můžou spouštět.</span><span class="sxs-lookup"><span data-stu-id="103d2-260">Administrators define a restricted session configuration or runspace, which is a limited range of cmdlets and tasks that end users can run.</span></span> <span data-ttu-id="103d2-261">Definování omezeném prostředí runspace můžete zabránit uživatelům v přístupu k jiným počítačům, které nejsou v povolených Windows PowerShell® prostředí runspace, což zajišťuje bezpečnější připojení.</span><span class="sxs-lookup"><span data-stu-id="103d2-261">Defining a restricted runspace can prevent users from accessing other computers that are not in the allowed Windows PowerShell® runspace, thus offering a more secure connection.</span></span> <span data-ttu-id="103d2-262">Další informace o konfiguracích relace najdete v tématu [about_Session_Configurations](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/about/about_session_configurations) nebo [instalace a používání Windows PowerShell Web Accessu](../install-and-use-windows-powershell-web-access.md).</span><span class="sxs-lookup"><span data-stu-id="103d2-262">For more information on session configurations, see [about_Session_Configurations](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/about/about_session_configurations) or the [Install and Use Windows PowerShell Web Access](../install-and-use-windows-powershell-web-access.md).</span></span>

```PowerShell
Add-PswaAuthorizationRule -ComputerName srv2.contoso.com -UserGroupName contoso\SMAdmins -ConfigurationName PSWAEndpoint
```

### <a name="example-2"></a><span data-ttu-id="103d2-263">PŘÍKLAD 2</span><span class="sxs-lookup"><span data-stu-id="103d2-263">EXAMPLE 2</span></span>

<span data-ttu-id="103d2-264">Tento příklad uděluje přístup k výchozí konfiguraci relace prostředí Windows PowerShell `Microsoft.PowerShell`na *srv2* pro uživatele v uživatelů s názvem `contoso\user1`, `contoso\user2`, a `contoso\user3`.</span><span class="sxs-lookup"><span data-stu-id="103d2-264">This example grants access to the default Windows PowerShell session configuration, `Microsoft.PowerShell`, on *srv2* for users in the users named `contoso\user1`, `contoso\user2`, and `contoso\user3`.</span></span> <span data-ttu-id="103d2-265">Tato rutina vytvoří tři pravidla (1 na osobu).</span><span class="sxs-lookup"><span data-stu-id="103d2-265">This cmdlet creates three rules (1 per person).</span></span>

```PowerShell
Add-PswaAuthorizationRule –UserName contoso\user1, contoso\user2, contoso\user3 –ComputerName srv2.contoso.com -ConfigurationName Microsoft.PowerShell
```

### <a name="example-3"></a><span data-ttu-id="103d2-266">PŘÍKLAD 3</span><span class="sxs-lookup"><span data-stu-id="103d2-266">EXAMPLE 3</span></span>

<span data-ttu-id="103d2-267">Tento příklad ukazuje, jak vstupní hodnoty název uživatele prostřednictvím kanálu.</span><span class="sxs-lookup"><span data-stu-id="103d2-267">This example illustrates how to input user name values via the pipeline.</span></span>

```powershell
"contoso\user1","contoso\user2" | Add-pswaAuthorizationRule –ComputerName srv2.contoso.com –ConfigurationName Microsoft.PowerShell
```

### <a name="example-4"></a><span data-ttu-id="103d2-268">PŘÍKLAD 4:</span><span class="sxs-lookup"><span data-stu-id="103d2-268">EXAMPLE 4</span></span>

<span data-ttu-id="103d2-269">Tento příklad ukazuje, jak všechny parametry v této hodnoty z kanálu název vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="103d2-269">This example illustrates how all parameters take values from pipeline by property name.</span></span>

````PowerShell
$o = New-Object -TypeName PSObject |
    Add-Member -Type NoteProperty -Name "UserName" -Value "contoso\user1" -PassThru |
    Add-Member -Type NoteProperty -Name "ComputerName" -Value "srv2.contoso.com" -PassThru |
    Add-Member -Type NoteProperty -Name "ConfigurationName" -Value "Microsoft.PowerShell" –PassThru

$o | Add-PswaAuthorizationRule -UserName contoso\user1 -ConfigurationName Microsoft.PowerShell
````

### <a name="example-5"></a><span data-ttu-id="103d2-270">PŘÍKLAD 5</span><span class="sxs-lookup"><span data-stu-id="103d2-270">EXAMPLE 5</span></span>

<span data-ttu-id="103d2-271">V tomto příkladu přidá pravidla povolení místního uživatele s názvem `PswaServer\ChrisLocal` přístup k serveru s názvem **srv1.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="103d2-271">This example adds a rule to allow the local user named `PswaServer\ChrisLocal` access to the server named **srv1.contoso.com**.</span></span>

<span data-ttu-id="103d2-272">Tento příklad ukazuje scénář, ve kterém je brána v pracovní skupině a cílový počítač nachází v doméně.</span><span class="sxs-lookup"><span data-stu-id="103d2-272">This example illustrates a scenario where the gateway is in a workgroup and the destination computer is in a domain.</span></span> <span data-ttu-id="103d2-273">Autorizační pravidlo platí pro místní uživatele v bráně.</span><span class="sxs-lookup"><span data-stu-id="103d2-273">The authorization rule applies to the local users on the gateway.</span></span> <span data-ttu-id="103d2-274">Na Windows PowerShell Web Accessu přihlašovací stránku k ověření úspěšně, uživatel musí zadat druhou sadu pověření v **volitelná nastavení připojení** oblasti.</span><span class="sxs-lookup"><span data-stu-id="103d2-274">On the Windows PowerShell Web Access sign-in page, to successfully authenticate, the user must provide a second set of credentials in the **Optional connection settings** area.</span></span> <span data-ttu-id="103d2-275">Server brány použije další sadu pověření pro ověření uživatele v cílovém počítači, serveru s názvem *srv1.contoso.com*.</span><span class="sxs-lookup"><span data-stu-id="103d2-275">The gateway server uses the additional set of credentials to authenticate the user on the destination computer, a server named *srv1.contoso.com*.</span></span>

````powershell
Add-PswaAuthorizationRule –UserName PswaServer\ChrisLocal –ComputerName srv1.contoso.com –ConfigurationName Microsoft.PowerShell
````

### <a name="example-6"></a><span data-ttu-id="103d2-276">PŘÍKLAD 6</span><span class="sxs-lookup"><span data-stu-id="103d2-276">EXAMPLE 6</span></span>

<span data-ttu-id="103d2-277">Tento příklad umožňuje všem uživatelům přístup k všechny koncové body na všech počítačích.</span><span class="sxs-lookup"><span data-stu-id="103d2-277">This example allows all users access to all endpoints on all computers.</span></span>
<span data-ttu-id="103d2-278">To v podstatě vypne autorizačních pravidel.</span><span class="sxs-lookup"><span data-stu-id="103d2-278">This essentially turns off authorization rules.</span></span>

> [!NOTE]
> <span data-ttu-id="103d2-279">Použití `*` zástupný znak se doporučují pro nasazení zabezpečené a by měl pouze se považuje za pro testovací prostředí nebo použít v nasazeních, kde můžete zmírnit zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="103d2-279">Use of the `*` wildcard character is not recommended for security-sensitive deployments and should only be considered for test environments or used in deployments where security can be relaxed.</span></span>

````PowerShell
Add-PswaAuthorizationRule –UserName * -ComputerName * -ConfigurationName *
````

## <a name="see-also"></a><span data-ttu-id="103d2-280">Viz také</span><span class="sxs-lookup"><span data-stu-id="103d2-280">See Also</span></span>

<span data-ttu-id="103d2-281">[Get-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592891(v=wps.630).aspx)</span><span class="sxs-lookup"><span data-stu-id="103d2-281">[Get-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592891(v=wps.630).aspx)</span></span>

<span data-ttu-id="103d2-282">[Remove-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592893(v=wps.630).aspx)</span><span class="sxs-lookup"><span data-stu-id="103d2-282">[Remove-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592893(v=wps.630).aspx)</span></span>

<span data-ttu-id="103d2-283">[Test-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592892(v=wps.630).aspx)</span><span class="sxs-lookup"><span data-stu-id="103d2-283">[Test-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592892(v=wps.630).aspx)</span></span>

<span data-ttu-id="103d2-284">[Rutiny Install-PswaWebApplication](https://technet.microsoft.com/en-us/library/jj592894(v=wps.630).aspx)</span><span class="sxs-lookup"><span data-stu-id="103d2-284">[Install-PswaWebApplication](https://technet.microsoft.com/en-us/library/jj592894(v=wps.630).aspx)</span></span>

[<span data-ttu-id="103d2-285">Přidat člena</span><span class="sxs-lookup"><span data-stu-id="103d2-285">Add-Member</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=113280)

[<span data-ttu-id="103d2-286">New-Object</span><span class="sxs-lookup"><span data-stu-id="103d2-286">New-Object</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=113355)

[<span data-ttu-id="103d2-287">Get-Credential</span><span class="sxs-lookup"><span data-stu-id="103d2-287">Get-Credential</span></span>](http://go.microsoft.com/fwlink/?LinkID=293936)