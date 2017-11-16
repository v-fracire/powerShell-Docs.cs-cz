---
description: 
manager: carmonm
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: "rutiny prostředí PowerShell"
ms.date: 2016-12-12
title: "Přidat pswaauthorizationrule"
ms.technology: powershell
schema: 2.0.0
ms.openlocfilehash: 18422f71b2a5f9af07af94e4324d3c7774f1d5ea
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/08/2017
---
# <a name="add-pswaauthorizationrule"></a><span data-ttu-id="0e76e-103">Add-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="0e76e-103">Add-PswaAuthorizationRule</span></span>

## <a name="synopsis"></a><span data-ttu-id="0e76e-104">STRUČNÝ OBSAH</span><span class="sxs-lookup"><span data-stu-id="0e76e-104">SYNOPSIS</span></span>

<span data-ttu-id="0e76e-105">Přidá nové autorizační pravidlo je sada pravidel autorizace pro Windows PowerShell® Web Access.</span><span class="sxs-lookup"><span data-stu-id="0e76e-105">Adds a new authorization rule to the Windows PowerShell® Web Access authorization rule set.</span></span>

## <a name="syntax"></a><span data-ttu-id="0e76e-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="0e76e-106">Syntax</span></span>

### <a name="usergroupnamecomputergroupname"></a><span data-ttu-id="0e76e-107">UserGroupNameComputerGroupName</span><span class="sxs-lookup"><span data-stu-id="0e76e-107">UserGroupNameComputerGroupName</span></span>
```
Add-PswaAuthorizationRule -ComputerGroupName <String> -ConfigurationName <String> -UserGroupName <String[]> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

### <a name="usergroupnamecomputername"></a><span data-ttu-id="0e76e-108">UserGroupNameComputerName</span><span class="sxs-lookup"><span data-stu-id="0e76e-108">UserGroupNameComputerName</span></span>
```
Add-PswaAuthorizationRule -ComputerName <String> -ConfigurationName <String> -UserGroupName <String[]> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

### <a name="usernamecomputergroupname"></a><span data-ttu-id="0e76e-109">UserNameComputerGroupName</span><span class="sxs-lookup"><span data-stu-id="0e76e-109">UserNameComputerGroupName</span></span>
```
Add-PswaAuthorizationRule [-UserName] <String[]> -ComputerGroupName <String> -ConfigurationName <String> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

### <a name="usernamecomputername"></a><span data-ttu-id="0e76e-110">UserNameComputerName</span><span class="sxs-lookup"><span data-stu-id="0e76e-110">UserNameComputerName</span></span>
```
Add-PswaAuthorizationRule [-UserName] <String[]> [-ComputerName] <String> [-ConfigurationName] <String> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

## <a name="description"></a><span data-ttu-id="0e76e-111">POPIS</span><span class="sxs-lookup"><span data-stu-id="0e76e-111">DESCRIPTION</span></span>

<span data-ttu-id="0e76e-112">**Add-PswaAuthorizationRule** rutiny přidá nové autorizační pravidlo je sada pravidel autorizace pro Windows PowerShell® Web Access.</span><span class="sxs-lookup"><span data-stu-id="0e76e-112">The **Add-PswaAuthorizationRule** cmdlet adds a new authorization rule to the Windows PowerShell® Web Access authorization rule set.</span></span>

<span data-ttu-id="0e76e-113">Zadejte uživatele, počítače a prostředí Windows PowerShell koncové body pro toto pravidlo.</span><span class="sxs-lookup"><span data-stu-id="0e76e-113">You must specify the users, computers, and Windows PowerShell endpoints for this rule.</span></span> <span data-ttu-id="0e76e-114">Můžete zadat uživatele a počítače podle jednotlivých uživatelských účtů a názvy počítačů, nebo zadáním skupiny.</span><span class="sxs-lookup"><span data-stu-id="0e76e-114">You can specify both users and computers either by individual user accounts and computer names, or by specifying groups.</span></span>

<span data-ttu-id="0e76e-115">Pro počítač, který je připojený k doméně služby Active Directory použije rutinu identifikátor zabezpečení (SID) počítače k vytvoření pravidla.</span><span class="sxs-lookup"><span data-stu-id="0e76e-115">For a computer that is joined to an Active Directory domain, the cmdlet uses the security identifier (SID) of the computer to create the rule.</span></span>
<span data-ttu-id="0e76e-116">To umožňuje použít krátký název, plně kvalifikovaný název domény (FQDN) nebo IP adresu pro **název počítače** pole na stránce přihlášení.</span><span class="sxs-lookup"><span data-stu-id="0e76e-116">This allows you to use a short name, a fully qualified domain name (FQDN), or an IP address for the **Computer Name** field on the sign-in page.</span></span>

<span data-ttu-id="0e76e-117">Pro počítač, který není připojený k doméně služby Active Directory rutina vytvoří pravidlo s použitím názvu počítače poskytnutý správcem.</span><span class="sxs-lookup"><span data-stu-id="0e76e-117">For a computer that is not joined to an Active Directory domain, the cmdlet creates the rule using the computer name provided by the administrator.</span></span> <span data-ttu-id="0e76e-118">K úspěšnému připojení k tomuto počítači, koncový uživatel musí poskytnout název počítače úplně stejně jako v pravidle.</span><span class="sxs-lookup"><span data-stu-id="0e76e-118">To successfully connect to this machine, the end user must provide the computer name exactly as it appears in the rule.</span></span>

<span data-ttu-id="0e76e-119">Pokud existuje víc počítačů se stejným názvem v síti, může krátký název vyřešit více než jeden počítač.</span><span class="sxs-lookup"><span data-stu-id="0e76e-119">If there are multiple computers with the same name on the network, then short name can resolve to more than one computer.</span></span> <span data-ttu-id="0e76e-120">To může vést k nejednoznačnosti při navazování připojení.</span><span class="sxs-lookup"><span data-stu-id="0e76e-120">This can lead to ambiguity when establishing a connection.</span></span> <span data-ttu-id="0e76e-121">Například, pokud pravidlo existuje pro počítače pracovní skupiny s názvem "*Server1*" a nový počítač s názvem *server1.contoso.com* je připojený k síti, úspěšné ověření pomocí autorizačních pravidel a Windows PowerShell Web Access pokusí navázat připojení k počítači s názvem "*Server1*".</span><span class="sxs-lookup"><span data-stu-id="0e76e-121">For example, if a rule exists for the workgroup computer named "*Server1*” and a new computer named *server1.contoso.com* is joined to the network, validation using the authorization rules succeeds and Windows PowerShell Web Access attempts to establish a connection to the computer named “*Server1*”.</span></span> <span data-ttu-id="0e76e-122">Není zaručeno, že připojení k počítači konkrétní pracovní skupině; Pokus může být provedeny v pracovní skupině nebo doméně počítač s názvem "*Server1*".</span><span class="sxs-lookup"><span data-stu-id="0e76e-122">It is not guaranteed that the connection is established with the specified workgroup computer; the attempt could be made on either the workgroup or the domain computer named "*Server1*".</span></span> <span data-ttu-id="0e76e-123">Aby se snížilo nejednoznačnosti, se doporučuje použít plně kvalifikovaný název domény pro cílového počítače vždy, když je možné vytvořit autorizační pravidlo.</span><span class="sxs-lookup"><span data-stu-id="0e76e-123">To reduce ambiguity, it is recommended that you use the FQDN for the destination computer whenever possible to create an authorization rule.</span></span>

<span data-ttu-id="0e76e-124">Autorizační pravidla vyhodnotit primární přihlašovací pověření uživatelů Windows PowerShell Web Access, není alternativní přihlašovací údaje (druhou sadu pověření v nalezen **volitelná nastavení připojení** části přihlašovací stránka).</span><span class="sxs-lookup"><span data-stu-id="0e76e-124">The authorization rules evaluate the primary sign-in credential of the Windows PowerShell Web Access users, not the alternate credentials (the second set of credentials found in the **Optional connection settings** section of the sign-in page).</span></span> <span data-ttu-id="0e76e-125">Příklad tohoto najdete příklad 6.</span><span class="sxs-lookup"><span data-stu-id="0e76e-125">For an example of this, see Example 6.</span></span>

## <a name="parameters"></a><span data-ttu-id="0e76e-126">Parameters</span><span class="sxs-lookup"><span data-stu-id="0e76e-126">Parameters</span></span>

### <a name="-computergroupnameltstringgt"></a><span data-ttu-id="0e76e-127">-ComputerGroupName&lt;řetězec&gt;</span><span class="sxs-lookup"><span data-stu-id="0e76e-127">-ComputerGroupName&lt;String&gt;</span></span>

<span data-ttu-id="0e76e-128">Určuje název skupiny počítačů ve službě Active Directory Domain Services (AD DS) nebo místní skupiny, ke kterým toto pravidlo udělí přístup.</span><span class="sxs-lookup"><span data-stu-id="0e76e-128">Specifies the name of a computer group in Active Directory Domain Services (AD DS) or local groups to which this rule grants access.</span></span>

|||  
|-|-|
| <span data-ttu-id="0e76e-129">Aliasy</span><span class="sxs-lookup"><span data-stu-id="0e76e-129">Aliases</span></span>                              | <span data-ttu-id="0e76e-130">žádný</span><span class="sxs-lookup"><span data-stu-id="0e76e-130">none</span></span>                                 |
| <span data-ttu-id="0e76e-131">Povinné?</span><span class="sxs-lookup"><span data-stu-id="0e76e-131">Required?</span></span>                            | <span data-ttu-id="0e76e-132">Hodnota TRUE</span><span class="sxs-lookup"><span data-stu-id="0e76e-132">true</span></span>                                 |
| <span data-ttu-id="0e76e-133">Pozice?</span><span class="sxs-lookup"><span data-stu-id="0e76e-133">Position?</span></span>                            | <span data-ttu-id="0e76e-134">S názvem</span><span class="sxs-lookup"><span data-stu-id="0e76e-134">named</span></span>                                |
| <span data-ttu-id="0e76e-135">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="0e76e-135">Default Value</span></span>                        | <span data-ttu-id="0e76e-136">žádný</span><span class="sxs-lookup"><span data-stu-id="0e76e-136">none</span></span>                                 |
| <span data-ttu-id="0e76e-137">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="0e76e-137">Accept Pipeline Input?</span></span>               | <span data-ttu-id="0e76e-138">Hodnotu true (ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="0e76e-138">True (ByPropertyName)</span></span>                |
| <span data-ttu-id="0e76e-139">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="0e76e-139">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="0e76e-140">false</span><span class="sxs-lookup"><span data-stu-id="0e76e-140">false</span></span>                                |

### <a name="-computernameltstringgt"></a><span data-ttu-id="0e76e-141">-ComputerName&lt;řetězec&gt;</span><span class="sxs-lookup"><span data-stu-id="0e76e-141">-ComputerName&lt;String&gt;</span></span>

<span data-ttu-id="0e76e-142">Určuje název počítače, na kterou toto pravidlo udělí přístup.</span><span class="sxs-lookup"><span data-stu-id="0e76e-142">Specifies the computer name to which this rule grants access.</span></span>

|||  
|-|-|
| <span data-ttu-id="0e76e-143">Aliasy</span><span class="sxs-lookup"><span data-stu-id="0e76e-143">Aliases</span></span>                              | <span data-ttu-id="0e76e-144">žádný</span><span class="sxs-lookup"><span data-stu-id="0e76e-144">none</span></span>                                 |
| <span data-ttu-id="0e76e-145">Povinné?</span><span class="sxs-lookup"><span data-stu-id="0e76e-145">Required?</span></span>                            | <span data-ttu-id="0e76e-146">Hodnota TRUE</span><span class="sxs-lookup"><span data-stu-id="0e76e-146">true</span></span>                                 |
| <span data-ttu-id="0e76e-147">Pozice?</span><span class="sxs-lookup"><span data-stu-id="0e76e-147">Position?</span></span>                            | <span data-ttu-id="0e76e-148">S názvem</span><span class="sxs-lookup"><span data-stu-id="0e76e-148">named</span></span>                                |
| <span data-ttu-id="0e76e-149">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="0e76e-149">Default Value</span></span>                        | <span data-ttu-id="0e76e-150">žádný</span><span class="sxs-lookup"><span data-stu-id="0e76e-150">none</span></span>                                 |
| <span data-ttu-id="0e76e-151">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="0e76e-151">Accept Pipeline Input?</span></span>               | <span data-ttu-id="0e76e-152">Hodnotu true (ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="0e76e-152">True (ByPropertyName)</span></span>                |
| <span data-ttu-id="0e76e-153">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="0e76e-153">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="0e76e-154">false</span><span class="sxs-lookup"><span data-stu-id="0e76e-154">false</span></span>                                |

### <a name="-configurationnameltstringgt"></a><span data-ttu-id="0e76e-155">-ConfigurationName&lt;řetězec&gt;</span><span class="sxs-lookup"><span data-stu-id="0e76e-155">-ConfigurationName&lt;String&gt;</span></span>

<span data-ttu-id="0e76e-156">Určuje název konfigurace relace prostředí Windows PowerShell, také známé jako prostředí runspace, do které toto pravidlo udělí přístup.</span><span class="sxs-lookup"><span data-stu-id="0e76e-156">Specifies the name of the Windows PowerShell session configuration, also known as runspace, to which this rule grants access.</span></span>

|||  
|-|-|
| <span data-ttu-id="0e76e-157">Aliasy</span><span class="sxs-lookup"><span data-stu-id="0e76e-157">Aliases</span></span>                              | <span data-ttu-id="0e76e-158">žádný</span><span class="sxs-lookup"><span data-stu-id="0e76e-158">none</span></span>                                 |
| <span data-ttu-id="0e76e-159">Povinné?</span><span class="sxs-lookup"><span data-stu-id="0e76e-159">Required?</span></span>                            | <span data-ttu-id="0e76e-160">Hodnota TRUE</span><span class="sxs-lookup"><span data-stu-id="0e76e-160">true</span></span>                                 |
| <span data-ttu-id="0e76e-161">Pozice?</span><span class="sxs-lookup"><span data-stu-id="0e76e-161">Position?</span></span>                            | <span data-ttu-id="0e76e-162">S názvem</span><span class="sxs-lookup"><span data-stu-id="0e76e-162">named</span></span>                                |
| <span data-ttu-id="0e76e-163">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="0e76e-163">Default Value</span></span>                        | <span data-ttu-id="0e76e-164">žádný</span><span class="sxs-lookup"><span data-stu-id="0e76e-164">none</span></span>                                 |
| <span data-ttu-id="0e76e-165">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="0e76e-165">Accept Pipeline Input?</span></span>               | <span data-ttu-id="0e76e-166">Hodnotu true (ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="0e76e-166">True (ByPropertyName)</span></span>                |
| <span data-ttu-id="0e76e-167">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="0e76e-167">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="0e76e-168">false</span><span class="sxs-lookup"><span data-stu-id="0e76e-168">false</span></span>                                |

### <a name="-credentialltpscredentialgt"></a><span data-ttu-id="0e76e-169">-Credential&lt;PSCredential&gt;</span><span class="sxs-lookup"><span data-stu-id="0e76e-169">-Credential&lt;PSCredential&gt;</span></span>

<span data-ttu-id="0e76e-170">Určuje **PSCredential** objekt pro uživatelský účet, který chcete použít ke změně Windows PowerShell Web Access autorizačních pravidel.</span><span class="sxs-lookup"><span data-stu-id="0e76e-170">Specifies a **PSCredential** object for a user account that you want to use to change Windows PowerShell Web Access authorization rules.</span></span> <span data-ttu-id="0e76e-171">Pokud tento parametr nepřidáte, rutina používá účet aktuálně přihlášeného uživatele.</span><span class="sxs-lookup"><span data-stu-id="0e76e-171">If you do not add this parameter, the cmdlet uses the currently logged-on user account.</span></span> <span data-ttu-id="0e76e-172">Chcete-li získat **PSCredential** objekt, který je potřeba přidat autorizační pravidla vzdáleně, spusťte [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential) rutiny.</span><span class="sxs-lookup"><span data-stu-id="0e76e-172">To get a **PSCredential** object, which is required to add authorization rules remotely, run the [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential) cmdlet.</span></span>

|||  
|-|-|
| <span data-ttu-id="0e76e-173">Aliasy</span><span class="sxs-lookup"><span data-stu-id="0e76e-173">Aliases</span></span>                              | <span data-ttu-id="0e76e-174">žádný</span><span class="sxs-lookup"><span data-stu-id="0e76e-174">none</span></span>                                 |
| <span data-ttu-id="0e76e-175">Povinné?</span><span class="sxs-lookup"><span data-stu-id="0e76e-175">Required?</span></span>                            | <span data-ttu-id="0e76e-176">false</span><span class="sxs-lookup"><span data-stu-id="0e76e-176">false</span></span>                                |
| <span data-ttu-id="0e76e-177">Pozice?</span><span class="sxs-lookup"><span data-stu-id="0e76e-177">Position?</span></span>                            | <span data-ttu-id="0e76e-178">S názvem</span><span class="sxs-lookup"><span data-stu-id="0e76e-178">named</span></span>                                |
| <span data-ttu-id="0e76e-179">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="0e76e-179">Default Value</span></span>                        | <span data-ttu-id="0e76e-180">žádný</span><span class="sxs-lookup"><span data-stu-id="0e76e-180">none</span></span>                                 |
| <span data-ttu-id="0e76e-181">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="0e76e-181">Accept Pipeline Input?</span></span>               | <span data-ttu-id="0e76e-182">false</span><span class="sxs-lookup"><span data-stu-id="0e76e-182">false</span></span>                                |
| <span data-ttu-id="0e76e-183">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="0e76e-183">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="0e76e-184">false</span><span class="sxs-lookup"><span data-stu-id="0e76e-184">false</span></span>                                |

### <a name="-force"></a><span data-ttu-id="0e76e-185">-Force</span><span class="sxs-lookup"><span data-stu-id="0e76e-185">-Force</span></span>

<span data-ttu-id="0e76e-186">Vynutí spuštění příkazu, aniž by požádal uživatele o potvrzení. \\</span><span class="sxs-lookup"><span data-stu-id="0e76e-186">Forces the command to run without asking for user confirmation.\\</span></span>
<span data-ttu-id="0e76e-187">Kromě toho je také vyzve k potvrzení při zadání názvu počítače jednoduchý nebo krátké (například název, který není platný název domény nebo není plně kvalifikovaná).</span><span class="sxs-lookup"><span data-stu-id="0e76e-187">In addition, it also prompts for confirmation when you enter a simple or short computer name (such as a name that is not a domain name or is not fully qualified).</span></span> <span data-ttu-id="0e76e-188">Potvrzení je požadována z bezpečnostních důvodů, takže pokud chcete přidat počítač, pouze pokud je počítač v pracovní skupině můžete použít jednoduchý název.</span><span class="sxs-lookup"><span data-stu-id="0e76e-188">Confirmation is requested for security reasons, so that you can use the simple name to add a computer only if the computer is in a workgroup.</span></span>

|||  
|-|-|
| <span data-ttu-id="0e76e-189">Aliasy</span><span class="sxs-lookup"><span data-stu-id="0e76e-189">Aliases</span></span>                              | <span data-ttu-id="0e76e-190">žádný</span><span class="sxs-lookup"><span data-stu-id="0e76e-190">none</span></span>                                 |
| <span data-ttu-id="0e76e-191">Povinné?</span><span class="sxs-lookup"><span data-stu-id="0e76e-191">Required?</span></span>                            | <span data-ttu-id="0e76e-192">false</span><span class="sxs-lookup"><span data-stu-id="0e76e-192">false</span></span>                                |
| <span data-ttu-id="0e76e-193">Pozice?</span><span class="sxs-lookup"><span data-stu-id="0e76e-193">Position?</span></span>                            | <span data-ttu-id="0e76e-194">S názvem</span><span class="sxs-lookup"><span data-stu-id="0e76e-194">named</span></span>                                |
| <span data-ttu-id="0e76e-195">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="0e76e-195">Default Value</span></span>                        | <span data-ttu-id="0e76e-196">žádný</span><span class="sxs-lookup"><span data-stu-id="0e76e-196">none</span></span>                                 |
| <span data-ttu-id="0e76e-197">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="0e76e-197">Accept Pipeline Input?</span></span>               | <span data-ttu-id="0e76e-198">false</span><span class="sxs-lookup"><span data-stu-id="0e76e-198">false</span></span>                                |
| <span data-ttu-id="0e76e-199">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="0e76e-199">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="0e76e-200">false</span><span class="sxs-lookup"><span data-stu-id="0e76e-200">false</span></span>                                |

### <a name="-rulenameltstringgt"></a><span data-ttu-id="0e76e-201">-RuleName&lt;řetězec&gt;</span><span class="sxs-lookup"><span data-stu-id="0e76e-201">-RuleName&lt;String&gt;</span></span>

<span data-ttu-id="0e76e-202">Určuje popisný název pro toto pravidlo.</span><span class="sxs-lookup"><span data-stu-id="0e76e-202">Specifies the friendly name for this rule.</span></span>

|||  
|-|-|
| <span data-ttu-id="0e76e-203">Aliasy</span><span class="sxs-lookup"><span data-stu-id="0e76e-203">Aliases</span></span>                              | <span data-ttu-id="0e76e-204">žádný</span><span class="sxs-lookup"><span data-stu-id="0e76e-204">none</span></span>                                 |
| <span data-ttu-id="0e76e-205">Povinné?</span><span class="sxs-lookup"><span data-stu-id="0e76e-205">Required?</span></span>                            | <span data-ttu-id="0e76e-206">false</span><span class="sxs-lookup"><span data-stu-id="0e76e-206">false</span></span>                                |
| <span data-ttu-id="0e76e-207">Pozice?</span><span class="sxs-lookup"><span data-stu-id="0e76e-207">Position?</span></span>                            | <span data-ttu-id="0e76e-208">S názvem</span><span class="sxs-lookup"><span data-stu-id="0e76e-208">named</span></span>                                |
| <span data-ttu-id="0e76e-209">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="0e76e-209">Default Value</span></span>                        | <span data-ttu-id="0e76e-210">žádný</span><span class="sxs-lookup"><span data-stu-id="0e76e-210">none</span></span>                                 |
| <span data-ttu-id="0e76e-211">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="0e76e-211">Accept Pipeline Input?</span></span>               | <span data-ttu-id="0e76e-212">Hodnotu true (ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="0e76e-212">True (ByPropertyName)</span></span>                |
| <span data-ttu-id="0e76e-213">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="0e76e-213">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="0e76e-214">false</span><span class="sxs-lookup"><span data-stu-id="0e76e-214">false</span></span>                                |

### <a name="-usergroupnameltstringgt"></a><span data-ttu-id="0e76e-215">-UserGroupName&lt;řetězec\[\]&gt;</span><span class="sxs-lookup"><span data-stu-id="0e76e-215">-UserGroupName&lt;String\[\]&gt;</span></span>

<span data-ttu-id="0e76e-216">Určuje název jednoho nebo víc skupin uživatelů ve službě AD DS nebo místních skupin, ke kterým toto pravidlo udělí přístup.</span><span class="sxs-lookup"><span data-stu-id="0e76e-216">Specifies the name of one or more user groups in AD DS or local groups to which this rule grants access.</span></span>

|||  
|-|-|
| <span data-ttu-id="0e76e-217">Aliasy</span><span class="sxs-lookup"><span data-stu-id="0e76e-217">Aliases</span></span>                              | <span data-ttu-id="0e76e-218">žádný</span><span class="sxs-lookup"><span data-stu-id="0e76e-218">none</span></span>                                 |
| <span data-ttu-id="0e76e-219">Povinné?</span><span class="sxs-lookup"><span data-stu-id="0e76e-219">Required?</span></span>                            | <span data-ttu-id="0e76e-220">Hodnota TRUE</span><span class="sxs-lookup"><span data-stu-id="0e76e-220">true</span></span>                                 |
| <span data-ttu-id="0e76e-221">Pozice?</span><span class="sxs-lookup"><span data-stu-id="0e76e-221">Position?</span></span>                            | <span data-ttu-id="0e76e-222">S názvem</span><span class="sxs-lookup"><span data-stu-id="0e76e-222">named</span></span>                                |
| <span data-ttu-id="0e76e-223">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="0e76e-223">Default Value</span></span>                        | <span data-ttu-id="0e76e-224">žádný</span><span class="sxs-lookup"><span data-stu-id="0e76e-224">none</span></span>                                 |
| <span data-ttu-id="0e76e-225">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="0e76e-225">Accept Pipeline Input?</span></span>               | <span data-ttu-id="0e76e-226">Hodnotu true (ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="0e76e-226">True (ByPropertyName)</span></span>                |
| <span data-ttu-id="0e76e-227">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="0e76e-227">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="0e76e-228">false</span><span class="sxs-lookup"><span data-stu-id="0e76e-228">false</span></span>                                |

### <a name="-usernameltstringgt"></a><span data-ttu-id="0e76e-229">-UserName&lt;řetězec\[\]&gt;</span><span class="sxs-lookup"><span data-stu-id="0e76e-229">-UserName&lt;String\[\]&gt;</span></span>

<span data-ttu-id="0e76e-230">Určuje jeden nebo více uživatelů, na které toto pravidlo udělí přístup.</span><span class="sxs-lookup"><span data-stu-id="0e76e-230">Specifies one or more users to which this rule grants access.</span></span> <span data-ttu-id="0e76e-231">Uživatelské jméno může být místní uživatelský účet v počítači brány nebo uživatele ve službě AD DS.</span><span class="sxs-lookup"><span data-stu-id="0e76e-231">The user name can be a local user account on the gateway computer or a user in AD DS.</span></span>
<span data-ttu-id="0e76e-232">Formát je `domain\user` nebo `computer\user`.</span><span class="sxs-lookup"><span data-stu-id="0e76e-232">The format is `domain\user` or `computer\user`.</span></span>

|||  
|-|-|
| <span data-ttu-id="0e76e-233">Aliasy</span><span class="sxs-lookup"><span data-stu-id="0e76e-233">Aliases</span></span>                              | <span data-ttu-id="0e76e-234">žádný</span><span class="sxs-lookup"><span data-stu-id="0e76e-234">none</span></span>                                 |
| <span data-ttu-id="0e76e-235">Povinné?</span><span class="sxs-lookup"><span data-stu-id="0e76e-235">Required?</span></span>                            | <span data-ttu-id="0e76e-236">Hodnota TRUE</span><span class="sxs-lookup"><span data-stu-id="0e76e-236">true</span></span>                                 |
| <span data-ttu-id="0e76e-237">Pozice?</span><span class="sxs-lookup"><span data-stu-id="0e76e-237">Position?</span></span>                            | <span data-ttu-id="0e76e-238">1</span><span class="sxs-lookup"><span data-stu-id="0e76e-238">1</span></span>                                    |
| <span data-ttu-id="0e76e-239">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="0e76e-239">Default Value</span></span>                        | <span data-ttu-id="0e76e-240">žádný</span><span class="sxs-lookup"><span data-stu-id="0e76e-240">none</span></span>                                 |
| <span data-ttu-id="0e76e-241">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="0e76e-241">Accept Pipeline Input?</span></span>               | <span data-ttu-id="0e76e-242">Hodnotu true (ByValue, ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="0e76e-242">True (ByValue, ByPropertyName)</span></span>       |
| <span data-ttu-id="0e76e-243">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="0e76e-243">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="0e76e-244">false</span><span class="sxs-lookup"><span data-stu-id="0e76e-244">false</span></span>                                |

### <a name="ltcommonparametersgt"></a><span data-ttu-id="0e76e-245">&lt;CommonParameters&gt;</span><span class="sxs-lookup"><span data-stu-id="0e76e-245">&lt;CommonParameters&gt;</span></span>

<span data-ttu-id="0e76e-246">Tato rutina podporuje běžné parametry:-Verbose,-Debug, - ErrorAction, - ErrorVariable,-OutBuffer a - OutVariable.</span><span class="sxs-lookup"><span data-stu-id="0e76e-246">This cmdlet supports the common parameters: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer, and -OutVariable.</span></span>
<span data-ttu-id="0e76e-247">Další informace najdete v tématu [about_CommonParameters](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/about/about_commonparameters).</span><span class="sxs-lookup"><span data-stu-id="0e76e-247">For more information, see [about_CommonParameters](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/about/about_commonparameters).</span></span>

## <a name="inputs"></a><span data-ttu-id="0e76e-248">VSTUPY</span><span class="sxs-lookup"><span data-stu-id="0e76e-248">INPUTS</span></span>

### <a name="string"></a><span data-ttu-id="0e76e-249">Řetězec</span><span class="sxs-lookup"><span data-stu-id="0e76e-249">String</span></span>

<span data-ttu-id="0e76e-250">Tato rutina akceptuje jako vstupní řetězec nebo pole řetězců.</span><span class="sxs-lookup"><span data-stu-id="0e76e-250">This cmdlet accepts a string or an array of strings as input.</span></span>

### <a name="string"></a><span data-ttu-id="0e76e-251">Řetězec\[\]</span><span class="sxs-lookup"><span data-stu-id="0e76e-251">String\[\]</span></span>

<span data-ttu-id="0e76e-252">Tato rutina akceptuje jako vstupní řetězec nebo pole řetězců.</span><span class="sxs-lookup"><span data-stu-id="0e76e-252">This cmdlet accepts a string or an array of strings as input.</span></span>

## <a name="outputs"></a><span data-ttu-id="0e76e-253">Výstupy</span><span class="sxs-lookup"><span data-stu-id="0e76e-253">Outputs</span></span>

### <a name="microsoftmanagementpowershellwebaccesspswaauthorizationrule"></a><span data-ttu-id="0e76e-254">Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="0e76e-254">Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule</span></span>

<span data-ttu-id="0e76e-255">Tato rutina vrací objektu pravidla autorizace.</span><span class="sxs-lookup"><span data-stu-id="0e76e-255">This cmdlet returns the an authorization rule object.</span></span>

## <a name="examples"></a><span data-ttu-id="0e76e-256">PŘÍKLADY</span><span class="sxs-lookup"><span data-stu-id="0e76e-256">EXAMPLES</span></span>

### <a name="example-1"></a><span data-ttu-id="0e76e-257">PŘÍKLAD 1</span><span class="sxs-lookup"><span data-stu-id="0e76e-257">EXAMPLE 1</span></span>

<span data-ttu-id="0e76e-258">Tento příklad uděluje přístup k této konfiguraci relace *Pswakoncovybod*, omezuje prostředí runspace *srv2* pro uživatele v *SMAdmins* skupiny. \\</span><span class="sxs-lookup"><span data-stu-id="0e76e-258">This example grants access to the session configuration *PSWAEndpoint*, a restricted runspace, on *srv2* for users in the *SMAdmins* group.\\</span></span>
<span data-ttu-id="0e76e-259">**Poznámka:**: název počítače musí být platný plně kvalifikovaný název domény (FQDN).</span><span class="sxs-lookup"><span data-stu-id="0e76e-259">**Note**: The computer name must be a fully qualified domain name (FQDN).</span></span> <span data-ttu-id="0e76e-260">Správci definují konfiguraci relace s omezeným přístupem nebo prostředí runspace, což je omezeným rozsahem rutin a úloh, které koncoví uživatelé můžou běžet.</span><span class="sxs-lookup"><span data-stu-id="0e76e-260">Administrators define a restricted session configuration or runspace, which is a limited range of cmdlets and tasks that end users can run.</span></span> <span data-ttu-id="0e76e-261">Definování omezeném prostředí runspace může zabránit uživatelům v přístupu k jiným počítačům, které nejsou v povolené prostředí runspace Windows PowerShell®, což zajišťuje bezpečnější připojení.</span><span class="sxs-lookup"><span data-stu-id="0e76e-261">Defining a restricted runspace can prevent users from accessing other computers that are not in the allowed Windows PowerShell® runspace, thus offering a more secure connection.</span></span> <span data-ttu-id="0e76e-262">Další informace o konfiguracích relace najdete v tématu [about_Session_Configurations](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/about/about_session_configurations) nebo [instalace a použití Windows PowerShell Web Access](../install-and-use-windows-powershell-web-access.md).</span><span class="sxs-lookup"><span data-stu-id="0e76e-262">For more information on session configurations, see [about_Session_Configurations](https://msdn.microsoft.com/en-us/powershell/reference/5.1/microsoft.powershell.core/about/about_session_configurations) or the [Install and Use Windows PowerShell Web Access](../install-and-use-windows-powershell-web-access.md).</span></span>

```PowerShell
Add-PswaAuthorizationRule -ComputerName srv2.contoso.com -UserGroupName contoso\SMAdmins -ConfigurationName PSWAEndpoint
```

### <a name="example-2"></a><span data-ttu-id="0e76e-263">PŘÍKLAD 2</span><span class="sxs-lookup"><span data-stu-id="0e76e-263">EXAMPLE 2</span></span>

<span data-ttu-id="0e76e-264">Tento příklad uděluje přístup k výchozí konfiguraci relace prostředí Windows PowerShell, `Microsoft.PowerShell`na *srv2* pro uživatele v seznamu Uživatelé s názvem contoso\\uživatel1, contoso\\uživatel2 a contoso\\UŽIVATEL3.</span><span class="sxs-lookup"><span data-stu-id="0e76e-264">This example grants access to the default Windows PowerShell session configuration, `Microsoft.PowerShell`, on *srv2* for users in the users named contoso\\user1, contoso\\user2, and contoso\\user3.</span></span> <span data-ttu-id="0e76e-265">Tato rutina vytvoří tři pravidla (1 na osobu).</span><span class="sxs-lookup"><span data-stu-id="0e76e-265">This cmdlet creates three rules (1 per person).</span></span>

```PowerShell
Add-PswaAuthorizationRule –UserName contoso\user1, contoso\user2, contoso\user3 –ComputerName srv2.contoso.com -ConfigurationName Microsoft.PowerShell
```

### <a name="example-3"></a><span data-ttu-id="0e76e-266">PŘÍKLAD 3</span><span class="sxs-lookup"><span data-stu-id="0e76e-266">EXAMPLE 3</span></span>

<span data-ttu-id="0e76e-267">Tento příklad ukazuje, jak vstupní hodnoty názvu uživatele prostřednictvím kanálu.</span><span class="sxs-lookup"><span data-stu-id="0e76e-267">This example illustrates how to input user name values via the pipeline.</span></span>

```
"contoso\user1","contoso\user2" | Add-pswaAuthorizationRule –ComputerName srv2.contoso.com –ConfigurationName Microsoft.PowerShell
```

### <a name="example-4"></a><span data-ttu-id="0e76e-268">PŘÍKLAD 4</span><span class="sxs-lookup"><span data-stu-id="0e76e-268">EXAMPLE 4</span></span>

<span data-ttu-id="0e76e-269">Tento příklad ukazuje, jak všechny parametry trvat hodnoty z kanálu podle názvu vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="0e76e-269">This example illustrates how all parameters take values from pipeline by property name.</span></span>

````PowerShell
$o = New-Object -TypeName PSObject | 
    Add-Member -Type NoteProperty -Name "UserName" -Value "contoso\user1" -PassThru | 
    Add-Member -Type NoteProperty -Name "ComputerName" -Value "srv2.contoso.com" -PassThru | 
    Add-Member -Type NoteProperty -Name "ConfigurationName" -Value "Microsoft.PowerShell" –PassThru

$o | Add-PswaAuthorizationRule -UserName contoso\user1 -ConfigurationName Microsoft.PowerShell
````

### <a name="example-5"></a><span data-ttu-id="0e76e-270">PŘÍKLAD 5</span><span class="sxs-lookup"><span data-stu-id="0e76e-270">EXAMPLE 5</span></span>

<span data-ttu-id="0e76e-271">Tento příklad přidá pravidlo povolující místního uživatele s názvem *PswaServer\\Janlocal* přístup k serveru s názvem *srv1.contoso.com*.</span><span class="sxs-lookup"><span data-stu-id="0e76e-271">This example adds a rule to allow the local user named *PswaServer\\ChrisLocal* access to the server named *srv1.contoso.com*.</span></span>

<span data-ttu-id="0e76e-272">Tento příklad ukazuje scénář, kde brána je v pracovní skupině a cílový počítač je v doméně.</span><span class="sxs-lookup"><span data-stu-id="0e76e-272">This example illustrates a scenario where the gateway is in a workgroup and the destination computer is in a domain.</span></span> <span data-ttu-id="0e76e-273">Autorizační pravidlo platí pro místní uživatele na bráně.</span><span class="sxs-lookup"><span data-stu-id="0e76e-273">The authorization rule applies to the local users on the gateway.</span></span> <span data-ttu-id="0e76e-274">Na Windows PowerShell Web Access přihlašovací stránku k ověření úspěšně, musí uživatel zadat druhou sadu pověření v **volitelná nastavení připojení** oblasti.</span><span class="sxs-lookup"><span data-stu-id="0e76e-274">On the Windows PowerShell Web Access sign-in page, to successfully authenticate, the user must provide a second set of credentials in the **Optional connection settings** area.</span></span> <span data-ttu-id="0e76e-275">Server brány použije další sadu pověření k ověření uživatele v cílovém počítači, serveru s názvem *srv1.contoso.com*.</span><span class="sxs-lookup"><span data-stu-id="0e76e-275">The gateway server uses the additional set of credentials to authenticate the user on the destination computer, a server named *srv1.contoso.com*.</span></span>

````
Add-PswaAuthorizationRule –UserName PswaServer\ChrisLocal –ComputerName srv1.contoso.com –ConfigurationName Microsoft.PowerShell
````

### <a name="example-6"></a><span data-ttu-id="0e76e-276">PŘÍKLAD 6</span><span class="sxs-lookup"><span data-stu-id="0e76e-276">EXAMPLE 6</span></span>

<span data-ttu-id="0e76e-277">Tento příklad umožňuje všem uživatelům přístup k všechny koncové body na všech počítačích.</span><span class="sxs-lookup"><span data-stu-id="0e76e-277">This example allows all users access to all endpoints on all computers.</span></span>
<span data-ttu-id="0e76e-278">To v podstatě vypne autorizačních pravidel. \\</span><span class="sxs-lookup"><span data-stu-id="0e76e-278">This essentially turns off authorization rules.\\</span></span>
<span data-ttu-id="0e76e-279">**Poznámka:**: použití `*` zástupný znak se nedoporučuje pro nasazení citlivé na zabezpečení a by měla pouze být považovány za pro testovací prostředí nebo použitým v nasazeních, kde můžete zmírnit zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="0e76e-279">**Note**: Use of the `*` wildcard character is not recommended for security-sensitive deployments and should only be considered for test environments or used in deployments where security can be relaxed.</span></span>

````PowerShell
Add-PswaAuthorizationRule –UserName * -ComputerName * -ConfigurationName *
````

## <a name="see-also"></a><span data-ttu-id="0e76e-280">Viz také</span><span class="sxs-lookup"><span data-stu-id="0e76e-280">See Also</span></span>

- <span data-ttu-id="0e76e-281">[Get-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592891(v=wps.630).aspx)</span><span class="sxs-lookup"><span data-stu-id="0e76e-281">[Get-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592891(v=wps.630).aspx)</span></span>
- <span data-ttu-id="0e76e-282">[Remove-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592893(v=wps.630).aspx)</span><span class="sxs-lookup"><span data-stu-id="0e76e-282">[Remove-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592893(v=wps.630).aspx)</span></span>
- <span data-ttu-id="0e76e-283">[Test-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592892(v=wps.630).aspx)</span><span class="sxs-lookup"><span data-stu-id="0e76e-283">[Test-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592892(v=wps.630).aspx)</span></span>
- <span data-ttu-id="0e76e-284">[Rutiny Install-PswaWebApplication](https://technet.microsoft.com/en-us/library/jj592894(v=wps.630).aspx)</span><span class="sxs-lookup"><span data-stu-id="0e76e-284">[Install-PswaWebApplication](https://technet.microsoft.com/en-us/library/jj592894(v=wps.630).aspx)</span></span>
- [<span data-ttu-id="0e76e-285">Přidat člena</span><span class="sxs-lookup"><span data-stu-id="0e76e-285">Add-Member</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=113280)
- [<span data-ttu-id="0e76e-286">Nový objekt</span><span class="sxs-lookup"><span data-stu-id="0e76e-286">New-Object</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=113355)
- [<span data-ttu-id="0e76e-287">Get-Credential</span><span class="sxs-lookup"><span data-stu-id="0e76e-287">Get-Credential</span></span>](http://go.microsoft.com/fwlink/?LinkID=293936)