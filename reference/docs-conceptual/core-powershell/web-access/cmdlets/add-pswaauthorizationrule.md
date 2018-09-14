---
ms.topic: reference
keywords: rutiny prostředí PowerShell
ms.date: 12/12/2016
title: Add-PswaAuthorizationRule
schema: 2.0.0
ms.openlocfilehash: fe2b71dcfa870ba3f92484ae3fd3c45b3107a1bc
ms.sourcegitcommit: e46b868f56f359909ff7c8230b1d1770935cce0e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/13/2018
ms.locfileid: "45523073"
---
# <a name="add-pswaauthorizationrule"></a><span data-ttu-id="9b1ec-103">Add-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="9b1ec-103">Add-PswaAuthorizationRule</span></span>

## <a name="synopsis"></a><span data-ttu-id="9b1ec-104">SOUHRN</span><span class="sxs-lookup"><span data-stu-id="9b1ec-104">SYNOPSIS</span></span>

<span data-ttu-id="9b1ec-105">Přidá nové autorizační pravidlo sada pravidel autorizace pro Windows PowerShell Web Accessu.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-105">Adds a new authorization rule to the Windows PowerShell Web Access authorization rule set.</span></span>

## <a name="syntax"></a><span data-ttu-id="9b1ec-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="9b1ec-106">Syntax</span></span>

### <a name="usergroupnamecomputergroupname"></a><span data-ttu-id="9b1ec-107">UserGroupNameComputerGroupName</span><span class="sxs-lookup"><span data-stu-id="9b1ec-107">UserGroupNameComputerGroupName</span></span>

```
Add-PswaAuthorizationRule -ComputerGroupName <String> -ConfigurationName <String> -UserGroupName <String[]> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

### <a name="usergroupnamecomputername"></a><span data-ttu-id="9b1ec-108">UserGroupNameComputerName</span><span class="sxs-lookup"><span data-stu-id="9b1ec-108">UserGroupNameComputerName</span></span>

```
Add-PswaAuthorizationRule -ComputerName <String> -ConfigurationName <String> -UserGroupName <String[]> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

### <a name="usernamecomputergroupname"></a><span data-ttu-id="9b1ec-109">UserNameComputerGroupName</span><span class="sxs-lookup"><span data-stu-id="9b1ec-109">UserNameComputerGroupName</span></span>

```
Add-PswaAuthorizationRule [-UserName] <String[]> -ComputerGroupName <String> -ConfigurationName <String> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

### <a name="usernamecomputername"></a><span data-ttu-id="9b1ec-110">UserNameComputerName</span><span class="sxs-lookup"><span data-stu-id="9b1ec-110">UserNameComputerName</span></span>

```
Add-PswaAuthorizationRule [-UserName] <String[]> [-ComputerName] <String> [-ConfigurationName] <String> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

## <a name="description"></a><span data-ttu-id="9b1ec-111">POPIS</span><span class="sxs-lookup"><span data-stu-id="9b1ec-111">DESCRIPTION</span></span>

<span data-ttu-id="9b1ec-112">**Add-PswaAuthorizationRule** rutina přidá nové autorizační pravidlo do sada pravidel autorizace pro Windows PowerShell(r) Web Access.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-112">The **Add-PswaAuthorizationRule** cmdlet adds a new authorization rule to the Windows PowerShell(r) Web Access authorization rule set.</span></span>

<span data-ttu-id="9b1ec-113">Musíte zadat uživatelů, počítačů a prostředí Windows PowerShell koncové body pro toto pravidlo.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-113">You must specify the users, computers, and Windows PowerShell endpoints for this rule.</span></span> <span data-ttu-id="9b1ec-114">Můžete určit uživatele a počítače jednotlivých uživatelských účtů a názvy počítačů nebo zadáním skupiny.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-114">You can specify both users and computers either by individual user accounts and computer names, or by specifying groups.</span></span>

<span data-ttu-id="9b1ec-115">Pro počítač, který je připojený k doméně služby Active Directory rutina k vytvoření pravidla používá identifikátor zabezpečení (SID) počítače.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-115">For a computer that is joined to an Active Directory domain, the cmdlet uses the security identifier (SID) of the computer to create the rule.</span></span> <span data-ttu-id="9b1ec-116">Díky tomu můžete použít krátký název, plně kvalifikovaný název domény (FQDN) nebo IP adresu pro **název_počítače** na přihlašovací stránku.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-116">This allows you to use a short name, a fully qualified domain name (FQDN), or an IP address for the **Computer Name** field on the sign-in page.</span></span>

<span data-ttu-id="9b1ec-117">Pro počítač, který není připojený k doméně služby Active Directory rutina vytvoří pravidlo s použitím názvu počítače program od správce.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-117">For a computer that is not joined to an Active Directory domain, the cmdlet creates the rule using the computer name provided by the administrator.</span></span> <span data-ttu-id="9b1ec-118">K úspěšnému připojení k tomuto počítači, musí koncový uživatel poskytnutí názvu počítače, v naprosto stejném tvaru v pravidle.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-118">To successfully connect to this machine, the end user must provide the computer name exactly as it appears in the rule.</span></span>

<span data-ttu-id="9b1ec-119">Pokud existuje více počítačů se stejným názvem v síti, krátký název lze přeložit na více než jednom počítači.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-119">If there are multiple computers with the same name on the network, then short name can resolve to more than one computer.</span></span> <span data-ttu-id="9b1ec-120">To může vést k nejednoznačnosti při navazování připojení.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-120">This can lead to ambiguity when establishing a connection.</span></span> <span data-ttu-id="9b1ec-121">Například, pokud existuje pravidlo pro počítače pracovní skupiny s názvem "*Server1*" a nový počítač s názvem *"server1.contoso.com"* je připojen k síti a bude úspěšné ověření pomocí autorizačních pravidel a Windows PowerShell Web Accessu se pokusí navázat připojení k počítači s názvem "*Server1*".</span><span class="sxs-lookup"><span data-stu-id="9b1ec-121">For example, if a rule exists for the workgroup computer named "*Server1*" and a new computer named *server1.contoso.com* is joined to the network, validation using the authorization rules succeeds and Windows PowerShell Web Access attempts to establish a connection to the computer named "*Server1*".</span></span> <span data-ttu-id="9b1ec-122">Není zaručeno, že se připojení k počítači pracovní skupiny zadaný; Tento pokus se může provést v pracovní skupině nebo doméně počítač s názvem "*Server1*".</span><span class="sxs-lookup"><span data-stu-id="9b1ec-122">It is not guaranteed that the connection is established with the specified workgroup computer; the attempt could be made on either the workgroup or the domain computer named "*Server1*".</span></span> <span data-ttu-id="9b1ec-123">Ke snížení nejednoznačnost, doporučujeme použít plně kvalifikovaný název pro cílový počítač pokaždé, když je možné vytvořit autorizační pravidlo.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-123">To reduce ambiguity, it is recommended that you use the FQDN for the destination computer whenever possible to create an authorization rule.</span></span>

<span data-ttu-id="9b1ec-124">Autorizační pravidla vyhodnocení primární přihlašovací pověření uživatelů Windows PowerShell Web Accessu, ne alternativní přihlašovací údaje (součástí druhou sadu pověření **volitelná nastavení připojení** část přihlašovací stránka).</span><span class="sxs-lookup"><span data-stu-id="9b1ec-124">The authorization rules evaluate the primary sign-in credential of the Windows PowerShell Web Access users, not the alternate credentials (the second set of credentials found in the **Optional connection settings** section of the sign-in page).</span></span> <span data-ttu-id="9b1ec-125">Příkladem naleznete v příkladu 6.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-125">For an example of this, see Example 6.</span></span>

## <a name="parameters"></a><span data-ttu-id="9b1ec-126">Parameters</span><span class="sxs-lookup"><span data-stu-id="9b1ec-126">Parameters</span></span>

### <a name="-computergroupname-string"></a><span data-ttu-id="9b1ec-127">-ComputerGroupName \<řetězec\></span><span class="sxs-lookup"><span data-stu-id="9b1ec-127">-ComputerGroupName \<String\></span></span>

<span data-ttu-id="9b1ec-128">Určuje název skupiny počítačů v Active Directory Domain Services (AD DS) nebo místních skupin, na které toto pravidlo udělí přístup.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-128">Specifies the name of a computer group in Active Directory Domain Services (AD DS) or local groups to which this rule grants access.</span></span>

|||
|-|-|
| <span data-ttu-id="9b1ec-129">Aliasy</span><span class="sxs-lookup"><span data-stu-id="9b1ec-129">Aliases</span></span>                     | <span data-ttu-id="9b1ec-130">žádný</span><span class="sxs-lookup"><span data-stu-id="9b1ec-130">none</span></span>                  |
| <span data-ttu-id="9b1ec-131">Povinné?</span><span class="sxs-lookup"><span data-stu-id="9b1ec-131">Required?</span></span>                   | <span data-ttu-id="9b1ec-132">Hodnota TRUE</span><span class="sxs-lookup"><span data-stu-id="9b1ec-132">true</span></span>                  |
| <span data-ttu-id="9b1ec-133">Pozice?</span><span class="sxs-lookup"><span data-stu-id="9b1ec-133">Position?</span></span>                   | <span data-ttu-id="9b1ec-134">s názvem</span><span class="sxs-lookup"><span data-stu-id="9b1ec-134">named</span></span>                 |
| <span data-ttu-id="9b1ec-135">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="9b1ec-135">Default Value</span></span>               | <span data-ttu-id="9b1ec-136">žádný</span><span class="sxs-lookup"><span data-stu-id="9b1ec-136">none</span></span>                  |
| <span data-ttu-id="9b1ec-137">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="9b1ec-137">Accept Pipeline Input?</span></span>      | <span data-ttu-id="9b1ec-138">True (ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="9b1ec-138">True (ByPropertyName)</span></span> |
| <span data-ttu-id="9b1ec-139">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="9b1ec-139">Accept Wildcard Characters?</span></span> | <span data-ttu-id="9b1ec-140">false</span><span class="sxs-lookup"><span data-stu-id="9b1ec-140">false</span></span>                 |

### <a name="-computername-string"></a><span data-ttu-id="9b1ec-141">-ComputerName \<řetězec\></span><span class="sxs-lookup"><span data-stu-id="9b1ec-141">-ComputerName \<String\></span></span>

<span data-ttu-id="9b1ec-142">Určuje název počítače, na které toto pravidlo udělí přístup.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-142">Specifies the computer name to which this rule grants access.</span></span>

|||
|-|-|
| <span data-ttu-id="9b1ec-143">Aliasy</span><span class="sxs-lookup"><span data-stu-id="9b1ec-143">Aliases</span></span>                     | <span data-ttu-id="9b1ec-144">žádný</span><span class="sxs-lookup"><span data-stu-id="9b1ec-144">none</span></span>                  |
| <span data-ttu-id="9b1ec-145">Povinné?</span><span class="sxs-lookup"><span data-stu-id="9b1ec-145">Required?</span></span>                   | <span data-ttu-id="9b1ec-146">Hodnota TRUE</span><span class="sxs-lookup"><span data-stu-id="9b1ec-146">true</span></span>                  |
| <span data-ttu-id="9b1ec-147">Pozice?</span><span class="sxs-lookup"><span data-stu-id="9b1ec-147">Position?</span></span>                   | <span data-ttu-id="9b1ec-148">s názvem</span><span class="sxs-lookup"><span data-stu-id="9b1ec-148">named</span></span>                 |
| <span data-ttu-id="9b1ec-149">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="9b1ec-149">Default Value</span></span>               | <span data-ttu-id="9b1ec-150">žádný</span><span class="sxs-lookup"><span data-stu-id="9b1ec-150">none</span></span>                  |
| <span data-ttu-id="9b1ec-151">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="9b1ec-151">Accept Pipeline Input?</span></span>      | <span data-ttu-id="9b1ec-152">True (ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="9b1ec-152">True (ByPropertyName)</span></span> |
| <span data-ttu-id="9b1ec-153">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="9b1ec-153">Accept Wildcard Characters?</span></span> | <span data-ttu-id="9b1ec-154">false</span><span class="sxs-lookup"><span data-stu-id="9b1ec-154">false</span></span>                 |

### <a name="-configurationname-string"></a><span data-ttu-id="9b1ec-155">– Při ConfigurationName \<řetězec\></span><span class="sxs-lookup"><span data-stu-id="9b1ec-155">-ConfigurationName \<String\></span></span>

<span data-ttu-id="9b1ec-156">Určuje název konfigurace relace prostředí Windows PowerShell, označované také jako prostředí runspace, do které toto pravidlo udělí přístup.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-156">Specifies the name of the Windows PowerShell session configuration, also known as runspace, to which this rule grants access.</span></span>

|||
|-|-|
| <span data-ttu-id="9b1ec-157">Aliasy</span><span class="sxs-lookup"><span data-stu-id="9b1ec-157">Aliases</span></span>                     | <span data-ttu-id="9b1ec-158">žádný</span><span class="sxs-lookup"><span data-stu-id="9b1ec-158">none</span></span>                  |
| <span data-ttu-id="9b1ec-159">Povinné?</span><span class="sxs-lookup"><span data-stu-id="9b1ec-159">Required?</span></span>                   | <span data-ttu-id="9b1ec-160">Hodnota TRUE</span><span class="sxs-lookup"><span data-stu-id="9b1ec-160">true</span></span>                  |
| <span data-ttu-id="9b1ec-161">Pozice?</span><span class="sxs-lookup"><span data-stu-id="9b1ec-161">Position?</span></span>                   | <span data-ttu-id="9b1ec-162">s názvem</span><span class="sxs-lookup"><span data-stu-id="9b1ec-162">named</span></span>                 |
| <span data-ttu-id="9b1ec-163">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="9b1ec-163">Default Value</span></span>               | <span data-ttu-id="9b1ec-164">žádný</span><span class="sxs-lookup"><span data-stu-id="9b1ec-164">none</span></span>                  |
| <span data-ttu-id="9b1ec-165">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="9b1ec-165">Accept Pipeline Input?</span></span>      | <span data-ttu-id="9b1ec-166">True (ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="9b1ec-166">True (ByPropertyName)</span></span> |
| <span data-ttu-id="9b1ec-167">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="9b1ec-167">Accept Wildcard Characters?</span></span> | <span data-ttu-id="9b1ec-168">false</span><span class="sxs-lookup"><span data-stu-id="9b1ec-168">false</span></span>                 |

### <a name="-credential--pscredential"></a><span data-ttu-id="9b1ec-169">-Credential \<PSCredential\></span><span class="sxs-lookup"><span data-stu-id="9b1ec-169">-Credential  \<PSCredential\></span></span>

<span data-ttu-id="9b1ec-170">Určuje **PSCredential** objektu pro uživatelský účet, který chcete použít ke změně Windows PowerShell Web Accessu autorizačních pravidel.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-170">Specifies a **PSCredential** object for a user account that you want to use to change Windows PowerShell Web Access authorization rules.</span></span> <span data-ttu-id="9b1ec-171">Pokud nemůžete přidat tento parametr, rutina používá účet aktuálně přihlášeného uživatele.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-171">If you do not add this parameter, the cmdlet uses the currently logged-on user account.</span></span> <span data-ttu-id="9b1ec-172">Chcete-li získat **PSCredential** objektu, který je potřeba přidat autorizační pravidla vzdáleně, spusťte [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential) rutiny.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-172">To get a **PSCredential** object, which is required to add authorization rules remotely, run the [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential) cmdlet.</span></span>

|||
|-|-|
| <span data-ttu-id="9b1ec-173">Aliasy</span><span class="sxs-lookup"><span data-stu-id="9b1ec-173">Aliases</span></span>                     | <span data-ttu-id="9b1ec-174">žádný</span><span class="sxs-lookup"><span data-stu-id="9b1ec-174">none</span></span>  |
| <span data-ttu-id="9b1ec-175">Povinné?</span><span class="sxs-lookup"><span data-stu-id="9b1ec-175">Required?</span></span>                   | <span data-ttu-id="9b1ec-176">false</span><span class="sxs-lookup"><span data-stu-id="9b1ec-176">false</span></span> |
| <span data-ttu-id="9b1ec-177">Pozice?</span><span class="sxs-lookup"><span data-stu-id="9b1ec-177">Position?</span></span>                   | <span data-ttu-id="9b1ec-178">s názvem</span><span class="sxs-lookup"><span data-stu-id="9b1ec-178">named</span></span> |
| <span data-ttu-id="9b1ec-179">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="9b1ec-179">Default Value</span></span>               | <span data-ttu-id="9b1ec-180">žádný</span><span class="sxs-lookup"><span data-stu-id="9b1ec-180">none</span></span>  |
| <span data-ttu-id="9b1ec-181">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="9b1ec-181">Accept Pipeline Input?</span></span>      | <span data-ttu-id="9b1ec-182">false</span><span class="sxs-lookup"><span data-stu-id="9b1ec-182">false</span></span> |
| <span data-ttu-id="9b1ec-183">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="9b1ec-183">Accept Wildcard Characters?</span></span> | <span data-ttu-id="9b1ec-184">false</span><span class="sxs-lookup"><span data-stu-id="9b1ec-184">false</span></span> |

### <a name="-force"></a><span data-ttu-id="9b1ec-185">-Force</span><span class="sxs-lookup"><span data-stu-id="9b1ec-185">-Force</span></span>

<span data-ttu-id="9b1ec-186">Vynutí spuštění příkazu, aniž by požádal uživatele o potvrzení.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-186">Forces the command to run without asking for user confirmation.</span></span> <span data-ttu-id="9b1ec-187">Kromě toho se také zobrazí výzvu k potvrzení při zadání názvu počítače jednoduché nebo krátké (jako je například název, který není název domény nebo není plně kvalifikovaný).</span><span class="sxs-lookup"><span data-stu-id="9b1ec-187">In addition, it also prompts for confirmation when you enter a simple or short computer name (such as a name that is not a domain name or is not fully qualified).</span></span> <span data-ttu-id="9b1ec-188">Potvrzení je požadována z důvodu zabezpečení tak, aby jednoduchý název slouží k přidání počítače pouze v případě, že je počítač v pracovní skupině.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-188">Confirmation is requested for security reasons, so that you can use the simple name to add a computer only if the computer is in a workgroup.</span></span>

|||
|-|-|
| <span data-ttu-id="9b1ec-189">Aliasy</span><span class="sxs-lookup"><span data-stu-id="9b1ec-189">Aliases</span></span>                              | <span data-ttu-id="9b1ec-190">žádný</span><span class="sxs-lookup"><span data-stu-id="9b1ec-190">none</span></span>                                 |
| <span data-ttu-id="9b1ec-191">Povinné?</span><span class="sxs-lookup"><span data-stu-id="9b1ec-191">Required?</span></span>                            | <span data-ttu-id="9b1ec-192">false</span><span class="sxs-lookup"><span data-stu-id="9b1ec-192">false</span></span>                                |
| <span data-ttu-id="9b1ec-193">Pozice?</span><span class="sxs-lookup"><span data-stu-id="9b1ec-193">Position?</span></span>                            | <span data-ttu-id="9b1ec-194">s názvem</span><span class="sxs-lookup"><span data-stu-id="9b1ec-194">named</span></span>                                |
| <span data-ttu-id="9b1ec-195">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="9b1ec-195">Default Value</span></span>                        | <span data-ttu-id="9b1ec-196">žádný</span><span class="sxs-lookup"><span data-stu-id="9b1ec-196">none</span></span>                                 |
| <span data-ttu-id="9b1ec-197">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="9b1ec-197">Accept Pipeline Input?</span></span>               | <span data-ttu-id="9b1ec-198">false</span><span class="sxs-lookup"><span data-stu-id="9b1ec-198">false</span></span>                                |
| <span data-ttu-id="9b1ec-199">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="9b1ec-199">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="9b1ec-200">false</span><span class="sxs-lookup"><span data-stu-id="9b1ec-200">false</span></span>                                |

### <a name="-rulename-string"></a><span data-ttu-id="9b1ec-201">-RuleName \<řetězec\></span><span class="sxs-lookup"><span data-stu-id="9b1ec-201">-RuleName \<String\></span></span>

<span data-ttu-id="9b1ec-202">Určuje popisný název pro toto pravidlo.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-202">Specifies the friendly name for this rule.</span></span>

|||
|-|-|
| <span data-ttu-id="9b1ec-203">Aliasy</span><span class="sxs-lookup"><span data-stu-id="9b1ec-203">Aliases</span></span>                              | <span data-ttu-id="9b1ec-204">žádný</span><span class="sxs-lookup"><span data-stu-id="9b1ec-204">none</span></span>                                 |
| <span data-ttu-id="9b1ec-205">Povinné?</span><span class="sxs-lookup"><span data-stu-id="9b1ec-205">Required?</span></span>                            | <span data-ttu-id="9b1ec-206">false</span><span class="sxs-lookup"><span data-stu-id="9b1ec-206">false</span></span>                                |
| <span data-ttu-id="9b1ec-207">Pozice?</span><span class="sxs-lookup"><span data-stu-id="9b1ec-207">Position?</span></span>                            | <span data-ttu-id="9b1ec-208">s názvem</span><span class="sxs-lookup"><span data-stu-id="9b1ec-208">named</span></span>                                |
| <span data-ttu-id="9b1ec-209">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="9b1ec-209">Default Value</span></span>                        | <span data-ttu-id="9b1ec-210">žádný</span><span class="sxs-lookup"><span data-stu-id="9b1ec-210">none</span></span>                                 |
| <span data-ttu-id="9b1ec-211">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="9b1ec-211">Accept Pipeline Input?</span></span>               | <span data-ttu-id="9b1ec-212">True (ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="9b1ec-212">True (ByPropertyName)</span></span>                |
| <span data-ttu-id="9b1ec-213">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="9b1ec-213">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="9b1ec-214">false</span><span class="sxs-lookup"><span data-stu-id="9b1ec-214">false</span></span>                                |

### <a name="-usergroupname-string"></a><span data-ttu-id="9b1ec-215">-UserGroupName \<řetězec\[\]\></span><span class="sxs-lookup"><span data-stu-id="9b1ec-215">-UserGroupName \<String\[\]\></span></span>

<span data-ttu-id="9b1ec-216">Určuje název jedné nebo víc skupin uživatelů ve službě AD DS nebo místních skupin, na které toto pravidlo udělí přístup.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-216">Specifies the name of one or more user groups in AD DS or local groups to which this rule grants access.</span></span>

|||
|-|-|
| <span data-ttu-id="9b1ec-217">Aliasy</span><span class="sxs-lookup"><span data-stu-id="9b1ec-217">Aliases</span></span>                              | <span data-ttu-id="9b1ec-218">žádný</span><span class="sxs-lookup"><span data-stu-id="9b1ec-218">none</span></span>                                 |
| <span data-ttu-id="9b1ec-219">Povinné?</span><span class="sxs-lookup"><span data-stu-id="9b1ec-219">Required?</span></span>                            | <span data-ttu-id="9b1ec-220">Hodnota TRUE</span><span class="sxs-lookup"><span data-stu-id="9b1ec-220">true</span></span>                                 |
| <span data-ttu-id="9b1ec-221">Pozice?</span><span class="sxs-lookup"><span data-stu-id="9b1ec-221">Position?</span></span>                            | <span data-ttu-id="9b1ec-222">s názvem</span><span class="sxs-lookup"><span data-stu-id="9b1ec-222">named</span></span>                                |
| <span data-ttu-id="9b1ec-223">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="9b1ec-223">Default Value</span></span>                        | <span data-ttu-id="9b1ec-224">žádný</span><span class="sxs-lookup"><span data-stu-id="9b1ec-224">none</span></span>                                 |
| <span data-ttu-id="9b1ec-225">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="9b1ec-225">Accept Pipeline Input?</span></span>               | <span data-ttu-id="9b1ec-226">True (ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="9b1ec-226">True (ByPropertyName)</span></span>                |
| <span data-ttu-id="9b1ec-227">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="9b1ec-227">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="9b1ec-228">false</span><span class="sxs-lookup"><span data-stu-id="9b1ec-228">false</span></span>                                |

### <a name="-username-string"></a><span data-ttu-id="9b1ec-229">-UserName \<řetězec\[\]\></span><span class="sxs-lookup"><span data-stu-id="9b1ec-229">-UserName \<String\[\]\></span></span>

<span data-ttu-id="9b1ec-230">Určuje jeden nebo více uživatelů, na které toto pravidlo udělí přístup.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-230">Specifies one or more users to which this rule grants access.</span></span> <span data-ttu-id="9b1ec-231">Uživatelské jméno může být místní uživatelský účet na počítači brány nebo uživatel ve službě AD DS.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-231">The user name can be a local user account on the gateway computer or a user in AD DS.</span></span> <span data-ttu-id="9b1ec-232">Formát je `domain\user` nebo `computer\user`.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-232">The format is `domain\user` or `computer\user`.</span></span>

|||
|-|-|
| <span data-ttu-id="9b1ec-233">Aliasy</span><span class="sxs-lookup"><span data-stu-id="9b1ec-233">Aliases</span></span>                              | <span data-ttu-id="9b1ec-234">žádný</span><span class="sxs-lookup"><span data-stu-id="9b1ec-234">none</span></span>                                 |
| <span data-ttu-id="9b1ec-235">Povinné?</span><span class="sxs-lookup"><span data-stu-id="9b1ec-235">Required?</span></span>                            | <span data-ttu-id="9b1ec-236">Hodnota TRUE</span><span class="sxs-lookup"><span data-stu-id="9b1ec-236">true</span></span>                                 |
| <span data-ttu-id="9b1ec-237">Pozice?</span><span class="sxs-lookup"><span data-stu-id="9b1ec-237">Position?</span></span>                            | <span data-ttu-id="9b1ec-238">1</span><span class="sxs-lookup"><span data-stu-id="9b1ec-238">1</span></span>                                    |
| <span data-ttu-id="9b1ec-239">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="9b1ec-239">Default Value</span></span>                        | <span data-ttu-id="9b1ec-240">žádný</span><span class="sxs-lookup"><span data-stu-id="9b1ec-240">none</span></span>                                 |
| <span data-ttu-id="9b1ec-241">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="9b1ec-241">Accept Pipeline Input?</span></span>               | <span data-ttu-id="9b1ec-242">True (ByValue, ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="9b1ec-242">True (ByValue, ByPropertyName)</span></span>       |
| <span data-ttu-id="9b1ec-243">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="9b1ec-243">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="9b1ec-244">false</span><span class="sxs-lookup"><span data-stu-id="9b1ec-244">false</span></span>                                |

###  <a name="commonparameters"></a><span data-ttu-id="9b1ec-245">\<CommonParameters\></span><span class="sxs-lookup"><span data-stu-id="9b1ec-245">\<CommonParameters\></span></span>

<span data-ttu-id="9b1ec-246">Tato rutina podporuje běžné parametry:</span><span class="sxs-lookup"><span data-stu-id="9b1ec-246">This cmdlet supports the common parameters:</span></span>

<span data-ttu-id="9b1ec-247">-Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer a -OutVariable.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-247">-Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer, and -OutVariable.</span></span>
<span data-ttu-id="9b1ec-248">Další informace najdete v tématu [about_CommonParameters](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/about/about_commonparameters).</span><span class="sxs-lookup"><span data-stu-id="9b1ec-248">For more information, see [about_CommonParameters](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/about/about_commonparameters).</span></span>

## <a name="inputs"></a><span data-ttu-id="9b1ec-249">VSTUPY</span><span class="sxs-lookup"><span data-stu-id="9b1ec-249">INPUTS</span></span>

### <a name="string"></a><span data-ttu-id="9b1ec-250">Řetězec</span><span class="sxs-lookup"><span data-stu-id="9b1ec-250">String</span></span>

<span data-ttu-id="9b1ec-251">Tato rutina akceptuje jako vstupní řetězec nebo pole řetězců.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-251">This cmdlet accepts a string or an array of strings as input.</span></span>

### <a name="string"></a><span data-ttu-id="9b1ec-252">Řetězec\[\]</span><span class="sxs-lookup"><span data-stu-id="9b1ec-252">String\[\]</span></span>

<span data-ttu-id="9b1ec-253">Tato rutina akceptuje jako vstupní řetězec nebo pole řetězců.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-253">This cmdlet accepts a string or an array of strings as input.</span></span>

## <a name="outputs"></a><span data-ttu-id="9b1ec-254">Výstupy</span><span class="sxs-lookup"><span data-stu-id="9b1ec-254">Outputs</span></span>

### <a name="microsoftmanagementpowershellwebaccesspswaauthorizationrule"></a><span data-ttu-id="9b1ec-255">Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="9b1ec-255">Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule</span></span>

<span data-ttu-id="9b1ec-256">Tato rutina vrátí objektu pravidla autorizace.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-256">This cmdlet returns the an authorization rule object.</span></span>

## <a name="examples"></a><span data-ttu-id="9b1ec-257">PŘÍKLADY</span><span class="sxs-lookup"><span data-stu-id="9b1ec-257">EXAMPLES</span></span>

### <a name="example-1"></a><span data-ttu-id="9b1ec-258">PŘÍKLAD 1</span><span class="sxs-lookup"><span data-stu-id="9b1ec-258">EXAMPLE 1</span></span>

<span data-ttu-id="9b1ec-259">Tento příklad uděluje přístup ke konfiguraci relace _Pswakoncovybod_, omezuje prostředí runspace _srv2_ pro uživatele v _SMAdmins_ skupiny.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-259">This example grants access to the session configuration _PSWAEndpoint_, a restricted runspace, on _srv2_ for users in the _SMAdmins_ group.</span></span>

> [!NOTE]
> <span data-ttu-id="9b1ec-260">Název počítače musí být plně kvalifikovaný název domény (FQDN).</span><span class="sxs-lookup"><span data-stu-id="9b1ec-260">The computer name must be a fully qualified domain name (FQDN).</span></span> <span data-ttu-id="9b1ec-261">Správci definují konfiguraci relace s omezeným přístupem nebo prostředí runspace, což je omezeným rozsahem rutin a úloh, které koncoví uživatelé můžou spouštět.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-261">Administrators define a restricted session configuration or runspace, which is a limited range of cmdlets and tasks that end users can run.</span></span> <span data-ttu-id="9b1ec-262">Definování omezeném prostředí runspace můžete zabránit uživatelům v přístupu k jiným počítačům, které nejsou v povolených prostředí runspace Windows PowerShell(r), což zajišťuje bezpečnější připojení.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-262">Defining a restricted runspace can prevent users from accessing other computers that are not in the allowed Windows PowerShell(r) runspace, thus offering a more secure connection.</span></span> <span data-ttu-id="9b1ec-263">Další informace o konfiguracích relace najdete v tématu [about_Session_Configurations](/powershell/module/microsoft.powershell.core/about/about_session_configurations) nebo [instalace a používání Windows PowerShell Web Accessu](../install-and-use-windows-powershell-web-access.md).</span><span class="sxs-lookup"><span data-stu-id="9b1ec-263">For more information on session configurations, see [about_Session_Configurations](/powershell/module/microsoft.powershell.core/about/about_session_configurations) or [Install and Use Windows PowerShell Web Access](../install-and-use-windows-powershell-web-access.md).</span></span>

```powershell
Add-PswaAuthorizationRule -ComputerName srv2.contoso.com -UserGroupName contoso\SMAdmins -ConfigurationName PSWAEndpoint
```

### <a name="example-2"></a><span data-ttu-id="9b1ec-264">PŘÍKLAD 2</span><span class="sxs-lookup"><span data-stu-id="9b1ec-264">EXAMPLE 2</span></span>

<span data-ttu-id="9b1ec-265">Tento příklad uděluje přístup k výchozí konfiguraci relace prostředí Windows PowerShell `Microsoft.PowerShell`na *srv2* pro uživatele v uživatelů s názvem `contoso\user1`, `contoso\user2`, a `contoso\user3`.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-265">This example grants access to the default Windows PowerShell session configuration, `Microsoft.PowerShell`, on *srv2* for users in the users named `contoso\user1`, `contoso\user2`, and `contoso\user3`.</span></span> <span data-ttu-id="9b1ec-266">Tato rutina vytvoří tři pravidla (1 na osobu).</span><span class="sxs-lookup"><span data-stu-id="9b1ec-266">This cmdlet creates three rules (1 per person).</span></span>

```powershell
Add-PswaAuthorizationRule -UserName contoso\user1, contoso\user2, contoso\user3 -ComputerName srv2.contoso.com -ConfigurationName Microsoft.PowerShell
```

### <a name="example-3"></a><span data-ttu-id="9b1ec-267">PŘÍKLAD 3</span><span class="sxs-lookup"><span data-stu-id="9b1ec-267">EXAMPLE 3</span></span>

<span data-ttu-id="9b1ec-268">Tento příklad ukazuje, jak vstupní hodnoty název uživatele prostřednictvím kanálu.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-268">This example illustrates how to input user name values via the pipeline.</span></span>

```powershell
"contoso\user1","contoso\user2" | Add-pswaAuthorizationRule -ComputerName srv2.contoso.com -ConfigurationName Microsoft.PowerShell
```

### <a name="example-4"></a><span data-ttu-id="9b1ec-269">PŘÍKLAD 4:</span><span class="sxs-lookup"><span data-stu-id="9b1ec-269">EXAMPLE 4</span></span>

<span data-ttu-id="9b1ec-270">Tento příklad ukazuje, jak všechny parametry v této hodnoty z kanálu název vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-270">This example illustrates how all parameters take values from pipeline by property name.</span></span>

````powershell
$o = New-Object -TypeName PSObject |
    Add-Member -Type NoteProperty -Name "UserName" -Value "contoso\user1" -PassThru |
    Add-Member -Type NoteProperty -Name "ComputerName" -Value "srv2.contoso.com" -PassThru |
    Add-Member -Type NoteProperty -Name "ConfigurationName" -Value "Microsoft.PowerShell" -PassThru

$o | Add-PswaAuthorizationRule -UserName contoso\user1 -ConfigurationName Microsoft.PowerShell
````

### <a name="example-5"></a><span data-ttu-id="9b1ec-271">PŘÍKLAD 5</span><span class="sxs-lookup"><span data-stu-id="9b1ec-271">EXAMPLE 5</span></span>

<span data-ttu-id="9b1ec-272">V tomto příkladu přidá pravidla povolení místního uživatele s názvem `PswaServer\ChrisLocal` přístup k serveru s názvem **srv1.contoso.com**.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-272">This example adds a rule to allow the local user named `PswaServer\ChrisLocal` access to the server named **srv1.contoso.com**.</span></span>

<span data-ttu-id="9b1ec-273">Tento příklad ukazuje scénář, ve kterém je brána v pracovní skupině a cílový počítač nachází v doméně.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-273">This example illustrates a scenario where the gateway is in a workgroup and the destination computer is in a domain.</span></span> <span data-ttu-id="9b1ec-274">Autorizační pravidlo platí pro místní uživatele v bráně.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-274">The authorization rule applies to the local users on the gateway.</span></span> <span data-ttu-id="9b1ec-275">Na Windows PowerShell Web Accessu přihlašovací stránku k ověření úspěšně, uživatel musí zadat druhou sadu pověření v **volitelná nastavení připojení** oblasti.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-275">On the Windows PowerShell Web Access sign-in page, to successfully authenticate, the user must provide a second set of credentials in the **Optional connection settings** area.</span></span> <span data-ttu-id="9b1ec-276">Server brány použije další sadu pověření pro ověření uživatele v cílovém počítači, serveru s názvem *srv1.contoso.com*.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-276">The gateway server uses the additional set of credentials to authenticate the user on the destination computer, a server named *srv1.contoso.com*.</span></span>

````powershell
Add-PswaAuthorizationRule -UserName PswaServer\ChrisLocal -ComputerName srv1.contoso.com -ConfigurationName Microsoft.PowerShell
````

### <a name="example-6"></a><span data-ttu-id="9b1ec-277">PŘÍKLAD 6</span><span class="sxs-lookup"><span data-stu-id="9b1ec-277">EXAMPLE 6</span></span>

<span data-ttu-id="9b1ec-278">Tento příklad umožňuje všem uživatelům přístup k všechny koncové body na všech počítačích.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-278">This example allows all users access to all endpoints on all computers.</span></span> <span data-ttu-id="9b1ec-279">To v podstatě vypne autorizačních pravidel.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-279">This essentially turns off authorization rules.</span></span>

> [!NOTE]
> <span data-ttu-id="9b1ec-280">Použití `*` zástupný znak se doporučují pro nasazení zabezpečené a by měl pouze se považuje za pro testovací prostředí nebo použít v nasazeních, kde můžete zmírnit zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="9b1ec-280">Use of the `*` wildcard character is not recommended for security-sensitive deployments and should only be considered for test environments or used in deployments where security can be relaxed.</span></span>

````powershell
Add-PswaAuthorizationRule -UserName * -ComputerName * -ConfigurationName *
````

## <a name="see-also"></a><span data-ttu-id="9b1ec-281">Viz také</span><span class="sxs-lookup"><span data-stu-id="9b1ec-281">See Also</span></span>

<span data-ttu-id="9b1ec-282">[Get-PswaAuthorizationRule](https://technet.microsoft.com/library/jj592891(v=wps.630).aspx)</span><span class="sxs-lookup"><span data-stu-id="9b1ec-282">[Get-PswaAuthorizationRule](https://technet.microsoft.com/library/jj592891(v=wps.630).aspx)</span></span>

<span data-ttu-id="9b1ec-283">[Remove-PswaAuthorizationRule](https://technet.microsoft.com/library/jj592893(v=wps.630).aspx)</span><span class="sxs-lookup"><span data-stu-id="9b1ec-283">[Remove-PswaAuthorizationRule](https://technet.microsoft.com/library/jj592893(v=wps.630).aspx)</span></span>

<span data-ttu-id="9b1ec-284">[Test-PswaAuthorizationRule](https://technet.microsoft.com/library/jj592892(v=wps.630).aspx)</span><span class="sxs-lookup"><span data-stu-id="9b1ec-284">[Test-PswaAuthorizationRule](https://technet.microsoft.com/library/jj592892(v=wps.630).aspx)</span></span>

<span data-ttu-id="9b1ec-285">[Rutiny Install-PswaWebApplication](https://technet.microsoft.com/library/jj592894(v=wps.630).aspx)</span><span class="sxs-lookup"><span data-stu-id="9b1ec-285">[Install-PswaWebApplication](https://technet.microsoft.com/library/jj592894(v=wps.630).aspx)</span></span>

[<span data-ttu-id="9b1ec-286">Přidat člena</span><span class="sxs-lookup"><span data-stu-id="9b1ec-286">Add-Member</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=113280)

[<span data-ttu-id="9b1ec-287">New-Object</span><span class="sxs-lookup"><span data-stu-id="9b1ec-287">New-Object</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=113355)

[<span data-ttu-id="9b1ec-288">Get-Credential</span><span class="sxs-lookup"><span data-stu-id="9b1ec-288">Get-Credential</span></span>](http://go.microsoft.com/fwlink/?LinkID=293936)
