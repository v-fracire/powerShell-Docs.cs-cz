---
description: 
ms.topic: article
ms.prod: powershell
keywords: "rutiny prostředí PowerShell"
ms.date: 2016-12-12
title: Test pswaauthorizationrule
ms.technology: powershell
ms.openlocfilehash: fb2937397616160c70b056e412e42fb8ff4c2f27
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="test-pswaauthorizationrule"></a><span data-ttu-id="e3d52-103">Test-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="e3d52-103">Test-PswaAuthorizationRule</span></span>

## <a name="synopsis"></a><span data-ttu-id="e3d52-104">STRUČNÝ OBSAH</span><span class="sxs-lookup"><span data-stu-id="e3d52-104">SYNOPSIS</span></span>

<span data-ttu-id="e3d52-105">Ověřuje, zda pravidla pro zadaného uživatele, počítače nebo koncový bod neexistuje.</span><span class="sxs-lookup"><span data-stu-id="e3d52-105">Verifies whether a rule exists for a specified user, computer, or endpoint.</span></span>

## <a name="syntax"></a><span data-ttu-id="e3d52-106">SYNTAX</span><span class="sxs-lookup"><span data-stu-id="e3d52-106">SYNTAX</span></span>

### <a name="computername"></a><span data-ttu-id="e3d52-107">ComputerName</span><span class="sxs-lookup"><span data-stu-id="e3d52-107">ComputerName</span></span>
```
Test-PswaAuthorizationRule [-UserName] <String> [-ComputerName] <String> [[-ConfigurationName] <String> ] [-Credential <PSCredential> ] [-Rule <PswaAuthorizationRule[]> ] [ <CommonParameters>]
```

### <a name="connectionuri"></a><span data-ttu-id="e3d52-108">ConnectionUri</span><span class="sxs-lookup"><span data-stu-id="e3d52-108">ConnectionUri</span></span>
```
Test-PswaAuthorizationRule [-UserName] <String> [-ConnectionUri] <Uri> [[-ConfigurationName] <String> ] [-Credential <PSCredential> ] [-Rule <PswaAuthorizationRule[]> ] [ <CommonParameters>]
```

## <a name="description"></a><span data-ttu-id="e3d52-109">POPIS</span><span class="sxs-lookup"><span data-stu-id="e3d52-109">DESCRIPTION</span></span>

<span data-ttu-id="e3d52-110">**Test-PswaAuthorizationRule** rutiny ověřuje, zda pravidla pro zadaného uživatele, počítače nebo koncový bod neexistuje.</span><span class="sxs-lookup"><span data-stu-id="e3d52-110">The **Test-PswaAuthorizationRule** cmdlet verifies whether a rule exists for a specified user, computer, or endpoint.</span></span>
<span data-ttu-id="e3d52-111">Tuto rutinu můžete použít také otestovat autorizační pravidla, chcete-li ověřit, že je autorizovaný konkrétní uživatele, počítače nebo koncový bod žádost o přístup.</span><span class="sxs-lookup"><span data-stu-id="e3d52-111">This cmdlet can also be used to test authorization rules, to validate that a particular user, computer or endpoint access request is authorized.</span></span>
<span data-ttu-id="e3d52-112">Ve výchozím nastavení vyhodnotí tato rutina všechna pravidla v souboru autorizace.</span><span class="sxs-lookup"><span data-stu-id="e3d52-112">By default, this cmdlet evaluates all rules in the authorization file.</span></span>
<span data-ttu-id="e3d52-113">Můžete však zadat podmnožinu pravidla k testování.</span><span class="sxs-lookup"><span data-stu-id="e3d52-113">However, you can specify a subset of rules to test.</span></span>

<span data-ttu-id="e3d52-114">Tato rutina vám pomůže vyřešit potíže s počet selhání ověření.</span><span class="sxs-lookup"><span data-stu-id="e3d52-114">You can use this cmdlet to help troubleshoot authentication failures.</span></span>

<span data-ttu-id="e3d52-115">Parametry pro tuto rutinu odpovídají pole na stránku pro přihlášení k Windows PowerShell® Web Access.</span><span class="sxs-lookup"><span data-stu-id="e3d52-115">The parameters for this cmdlet correspond to fields on the Windows PowerShell® Web Access sign-on page.</span></span>

## <a name="parameters"></a><span data-ttu-id="e3d52-116">PARAMETRY</span><span class="sxs-lookup"><span data-stu-id="e3d52-116">PARAMETERS</span></span>

### <a name="-computername-ltstringgt"></a><span data-ttu-id="e3d52-117">-ComputerName &lt;řetězec&gt;</span><span class="sxs-lookup"><span data-stu-id="e3d52-117">-ComputerName &lt;String&gt;</span></span>

<span data-ttu-id="e3d52-118">Určuje název počítače, které chcete otestovat.</span><span class="sxs-lookup"><span data-stu-id="e3d52-118">Specifies the name of the computer to test.</span></span>

|||  
|-|-|
| <span data-ttu-id="e3d52-119">Aliasy</span><span class="sxs-lookup"><span data-stu-id="e3d52-119">Aliases</span></span>                              | <span data-ttu-id="e3d52-120">žádný</span><span class="sxs-lookup"><span data-stu-id="e3d52-120">none</span></span>                                 |
| <span data-ttu-id="e3d52-121">Povinné?</span><span class="sxs-lookup"><span data-stu-id="e3d52-121">Required?</span></span>                            | <span data-ttu-id="e3d52-122">Hodnota TRUE</span><span class="sxs-lookup"><span data-stu-id="e3d52-122">true</span></span>                                 |
| <span data-ttu-id="e3d52-123">Pozice?</span><span class="sxs-lookup"><span data-stu-id="e3d52-123">Position?</span></span>                            | <span data-ttu-id="e3d52-124">2</span><span class="sxs-lookup"><span data-stu-id="e3d52-124">2</span></span>                                    |
| <span data-ttu-id="e3d52-125">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="e3d52-125">Default Value</span></span>                        | <span data-ttu-id="e3d52-126">žádný</span><span class="sxs-lookup"><span data-stu-id="e3d52-126">none</span></span>                                 |
| <span data-ttu-id="e3d52-127">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="e3d52-127">Accept Pipeline Input?</span></span>               | <span data-ttu-id="e3d52-128">false</span><span class="sxs-lookup"><span data-stu-id="e3d52-128">false</span></span>                                |
| <span data-ttu-id="e3d52-129">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="e3d52-129">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="e3d52-130">false</span><span class="sxs-lookup"><span data-stu-id="e3d52-130">false</span></span>                                |

### <a name="-configurationname-ltstringgt"></a><span data-ttu-id="e3d52-131">-ConfigurationName &lt;řetězec&gt;</span><span class="sxs-lookup"><span data-stu-id="e3d52-131">-ConfigurationName &lt;String&gt;</span></span>

<span data-ttu-id="e3d52-132">Určuje název konfigurace relace prostředí Windows PowerShell, také známé jako koncový bod nebo prostředí runspace k testování.</span><span class="sxs-lookup"><span data-stu-id="e3d52-132">Specifies the name of the Windows PowerShell session configuration, also known as endpoint or runspace, to test.</span></span>

|||  
|-|-|
| <span data-ttu-id="e3d52-133">Aliasy</span><span class="sxs-lookup"><span data-stu-id="e3d52-133">Aliases</span></span>                              | <span data-ttu-id="e3d52-134">žádný</span><span class="sxs-lookup"><span data-stu-id="e3d52-134">none</span></span>                                 |
| <span data-ttu-id="e3d52-135">Povinné?</span><span class="sxs-lookup"><span data-stu-id="e3d52-135">Required?</span></span>                            | <span data-ttu-id="e3d52-136">false</span><span class="sxs-lookup"><span data-stu-id="e3d52-136">false</span></span>                                |
| <span data-ttu-id="e3d52-137">Pozice?</span><span class="sxs-lookup"><span data-stu-id="e3d52-137">Position?</span></span>                            | <span data-ttu-id="e3d52-138">3</span><span class="sxs-lookup"><span data-stu-id="e3d52-138">3</span></span>                                    |
| <span data-ttu-id="e3d52-139">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="e3d52-139">Default Value</span></span>                        | <span data-ttu-id="e3d52-140">žádný</span><span class="sxs-lookup"><span data-stu-id="e3d52-140">none</span></span>                                 |
| <span data-ttu-id="e3d52-141">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="e3d52-141">Accept Pipeline Input?</span></span>               | <span data-ttu-id="e3d52-142">false</span><span class="sxs-lookup"><span data-stu-id="e3d52-142">false</span></span>                                |
| <span data-ttu-id="e3d52-143">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="e3d52-143">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="e3d52-144">false</span><span class="sxs-lookup"><span data-stu-id="e3d52-144">false</span></span>                                |

### <a name="-connectionuri-lturigt"></a><span data-ttu-id="e3d52-145">-ConnectionUri &lt;identifikátor Uri&gt;</span><span class="sxs-lookup"><span data-stu-id="e3d52-145">-ConnectionUri &lt;Uri&gt;</span></span>

<span data-ttu-id="e3d52-146">Určuje identifikátor URI k testování připojení.</span><span class="sxs-lookup"><span data-stu-id="e3d52-146">Specifies the connection URI to test.</span></span>

|||  
|-|-|
| <span data-ttu-id="e3d52-147">Aliasy</span><span class="sxs-lookup"><span data-stu-id="e3d52-147">Aliases</span></span>                              | <span data-ttu-id="e3d52-148">žádný</span><span class="sxs-lookup"><span data-stu-id="e3d52-148">none</span></span>                                 |
| <span data-ttu-id="e3d52-149">Povinné?</span><span class="sxs-lookup"><span data-stu-id="e3d52-149">Required?</span></span>                            | <span data-ttu-id="e3d52-150">Hodnota TRUE</span><span class="sxs-lookup"><span data-stu-id="e3d52-150">true</span></span>                                 |
| <span data-ttu-id="e3d52-151">Pozice?</span><span class="sxs-lookup"><span data-stu-id="e3d52-151">Position?</span></span>                            | <span data-ttu-id="e3d52-152">2</span><span class="sxs-lookup"><span data-stu-id="e3d52-152">2</span></span>                                    |
| <span data-ttu-id="e3d52-153">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="e3d52-153">Default Value</span></span>                        | <span data-ttu-id="e3d52-154">žádný</span><span class="sxs-lookup"><span data-stu-id="e3d52-154">none</span></span>                                 |
| <span data-ttu-id="e3d52-155">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="e3d52-155">Accept Pipeline Input?</span></span>               | <span data-ttu-id="e3d52-156">false</span><span class="sxs-lookup"><span data-stu-id="e3d52-156">false</span></span>                                |
| <span data-ttu-id="e3d52-157">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="e3d52-157">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="e3d52-158">false</span><span class="sxs-lookup"><span data-stu-id="e3d52-158">false</span></span>                                |

### <a name="-credential-ltpscredentialgt"></a><span data-ttu-id="e3d52-159">-Credential &lt;PSCredential&gt;</span><span class="sxs-lookup"><span data-stu-id="e3d52-159">-Credential &lt;PSCredential&gt;</span></span>

<span data-ttu-id="e3d52-160">Určuje **PSCredential** objekt pro uživatelský účet, který chcete použít pro testování Windows PowerShell Web Access autorizačních pravidel.</span><span class="sxs-lookup"><span data-stu-id="e3d52-160">Specifies a **PSCredential** object for a user account that you want to use to test Windows PowerShell Web Access authorization rules.</span></span> <span data-ttu-id="e3d52-161">Pokud tento parametr nepřidáte, rutina používá účet aktuálně přihlášeného uživatele.</span><span class="sxs-lookup"><span data-stu-id="e3d52-161">If you do not add this parameter, the cmdlet uses the currently logged-on user account.</span></span> <span data-ttu-id="e3d52-162">Chcete-li získat **PSCredential** objekt, který je potřeba otestovat autorizační pravidla vzdáleně, spusťte [Get-Credential](http://go.microsoft.com/fwlink/?LinkID=293936) rutiny.</span><span class="sxs-lookup"><span data-stu-id="e3d52-162">To get a **PSCredential** object, which is required to test authorization rules remotely, run the [Get-Credential](http://go.microsoft.com/fwlink/?LinkID=293936) cmdlet.</span></span>

|||  
|-|-|
| <span data-ttu-id="e3d52-163">Aliasy</span><span class="sxs-lookup"><span data-stu-id="e3d52-163">Aliases</span></span>                              | <span data-ttu-id="e3d52-164">žádný</span><span class="sxs-lookup"><span data-stu-id="e3d52-164">none</span></span>                                 |
| <span data-ttu-id="e3d52-165">Povinné?</span><span class="sxs-lookup"><span data-stu-id="e3d52-165">Required?</span></span>                            | <span data-ttu-id="e3d52-166">false</span><span class="sxs-lookup"><span data-stu-id="e3d52-166">false</span></span>                                |
| <span data-ttu-id="e3d52-167">Pozice?</span><span class="sxs-lookup"><span data-stu-id="e3d52-167">Position?</span></span>                            | <span data-ttu-id="e3d52-168">S názvem</span><span class="sxs-lookup"><span data-stu-id="e3d52-168">named</span></span>                                |
| <span data-ttu-id="e3d52-169">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="e3d52-169">Default Value</span></span>                        | <span data-ttu-id="e3d52-170">žádný</span><span class="sxs-lookup"><span data-stu-id="e3d52-170">none</span></span>                                 |
| <span data-ttu-id="e3d52-171">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="e3d52-171">Accept Pipeline Input?</span></span>               | <span data-ttu-id="e3d52-172">false</span><span class="sxs-lookup"><span data-stu-id="e3d52-172">false</span></span>                                |
| <span data-ttu-id="e3d52-173">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="e3d52-173">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="e3d52-174">false</span><span class="sxs-lookup"><span data-stu-id="e3d52-174">false</span></span>                                |

### <a name="-rule-ltpswaauthorizationrulegt"></a><span data-ttu-id="e3d52-175">-Pravidla &lt;PswaAuthorizationRule\[\]&gt;</span><span class="sxs-lookup"><span data-stu-id="e3d52-175">-Rule &lt;PswaAuthorizationRule\[\]&gt;</span></span>

<span data-ttu-id="e3d52-176">Určuje podmnožinu pravidla k testování.</span><span class="sxs-lookup"><span data-stu-id="e3d52-176">Specifies a subset of rules to test.</span></span> <span data-ttu-id="e3d52-177">Pokud není tento parametr zadán, tato rutina testuje proti všechna autorizační pravidla.</span><span class="sxs-lookup"><span data-stu-id="e3d52-177">If this parameter is not specified, then this cmdlet tests against all authorization rules.</span></span>

|||  
|-|-|
| <span data-ttu-id="e3d52-178">Aliasy</span><span class="sxs-lookup"><span data-stu-id="e3d52-178">Aliases</span></span>                              | <span data-ttu-id="e3d52-179">žádný</span><span class="sxs-lookup"><span data-stu-id="e3d52-179">none</span></span>                                 |
| <span data-ttu-id="e3d52-180">Povinné?</span><span class="sxs-lookup"><span data-stu-id="e3d52-180">Required?</span></span>                            | <span data-ttu-id="e3d52-181">false</span><span class="sxs-lookup"><span data-stu-id="e3d52-181">false</span></span>                                |
| <span data-ttu-id="e3d52-182">Pozice?</span><span class="sxs-lookup"><span data-stu-id="e3d52-182">Position?</span></span>                            | <span data-ttu-id="e3d52-183">S názvem</span><span class="sxs-lookup"><span data-stu-id="e3d52-183">named</span></span>                                |
| <span data-ttu-id="e3d52-184">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="e3d52-184">Default Value</span></span>                        | <span data-ttu-id="e3d52-185">žádný</span><span class="sxs-lookup"><span data-stu-id="e3d52-185">none</span></span>                                 |
| <span data-ttu-id="e3d52-186">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="e3d52-186">Accept Pipeline Input?</span></span>               | <span data-ttu-id="e3d52-187">Hodnotu true (ByValue)</span><span class="sxs-lookup"><span data-stu-id="e3d52-187">True (ByValue)</span></span>                       |
| <span data-ttu-id="e3d52-188">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="e3d52-188">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="e3d52-189">false</span><span class="sxs-lookup"><span data-stu-id="e3d52-189">false</span></span>                                |

### <a name="-username-ltstringgt"></a><span data-ttu-id="e3d52-190">-UserName &lt;řetězec&gt;</span><span class="sxs-lookup"><span data-stu-id="e3d52-190">-UserName &lt;String&gt;</span></span>

<span data-ttu-id="e3d52-191">Určuje jméno uživatele, který chcete otestovat.</span><span class="sxs-lookup"><span data-stu-id="e3d52-191">Specifies the name of the user to test.</span></span>

|||  
|-|-|
| <span data-ttu-id="e3d52-192">Aliasy</span><span class="sxs-lookup"><span data-stu-id="e3d52-192">Aliases</span></span>                              | <span data-ttu-id="e3d52-193">žádný</span><span class="sxs-lookup"><span data-stu-id="e3d52-193">none</span></span>                                 |
| <span data-ttu-id="e3d52-194">Povinné?</span><span class="sxs-lookup"><span data-stu-id="e3d52-194">Required?</span></span>                            | <span data-ttu-id="e3d52-195">Hodnota TRUE</span><span class="sxs-lookup"><span data-stu-id="e3d52-195">true</span></span>                                 |
| <span data-ttu-id="e3d52-196">Pozice?</span><span class="sxs-lookup"><span data-stu-id="e3d52-196">Position?</span></span>                            | <span data-ttu-id="e3d52-197">1</span><span class="sxs-lookup"><span data-stu-id="e3d52-197">1</span></span>                                    |
| <span data-ttu-id="e3d52-198">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="e3d52-198">Default Value</span></span>                        | <span data-ttu-id="e3d52-199">žádný</span><span class="sxs-lookup"><span data-stu-id="e3d52-199">none</span></span>                                 |
| <span data-ttu-id="e3d52-200">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="e3d52-200">Accept Pipeline Input?</span></span>               | <span data-ttu-id="e3d52-201">false</span><span class="sxs-lookup"><span data-stu-id="e3d52-201">false</span></span>                                |
| <span data-ttu-id="e3d52-202">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="e3d52-202">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="e3d52-203">false</span><span class="sxs-lookup"><span data-stu-id="e3d52-203">false</span></span>                                |

### <a name="ltcommonparametersgt"></a><span data-ttu-id="e3d52-204">&lt;CommonParameters&gt;</span><span class="sxs-lookup"><span data-stu-id="e3d52-204">&lt;CommonParameters&gt;</span></span>

<span data-ttu-id="e3d52-205">Tato rutina podporuje běžné parametry:-Verbose,-Debug, - ErrorAction, - ErrorVariable,-OutBuffer a - OutVariable.</span><span class="sxs-lookup"><span data-stu-id="e3d52-205">This cmdlet supports the common parameters: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer, and -OutVariable.</span></span>
<span data-ttu-id="e3d52-206">Další informace najdete v tématu [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span><span class="sxs-lookup"><span data-stu-id="e3d52-206">For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span></span>

## <a name="inputs"></a><span data-ttu-id="e3d52-207">VSTUPY</span><span class="sxs-lookup"><span data-stu-id="e3d52-207">INPUTS</span></span>

### <a name="microsoftmanagementpowershellwebaccesspswaauthorizationrule"></a><span data-ttu-id="e3d52-208">Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule\[\]</span><span class="sxs-lookup"><span data-stu-id="e3d52-208">Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule\[\]</span></span>

<span data-ttu-id="e3d52-209">Tato rutina akceptuje jako vstupní pole objektů PswaAuthorizationRule.</span><span class="sxs-lookup"><span data-stu-id="e3d52-209">This cmdlet accepts an array of PswaAuthorizationRule objects as input.</span></span>

## <a name="outputs"></a><span data-ttu-id="e3d52-210">VÝSTUPY</span><span class="sxs-lookup"><span data-stu-id="e3d52-210">OUTPUTS</span></span>

### <a name="microsoftmanagementpowershellwebaccesspswaauthorizationrule"></a><span data-ttu-id="e3d52-211">Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule\[\]</span><span class="sxs-lookup"><span data-stu-id="e3d52-211">Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule\[\]</span></span>

<span data-ttu-id="e3d52-212">Tato rutina vytvoří pole objektů PswaAuthorizationRule jako výstup.</span><span class="sxs-lookup"><span data-stu-id="e3d52-212">This cmdlet produces an array of PswaAuthorizationRule objects as output.</span></span>

## <a name="examples"></a><span data-ttu-id="e3d52-213">PŘÍKLADY</span><span class="sxs-lookup"><span data-stu-id="e3d52-213">EXAMPLES</span></span>

### <a name="example-1"></a><span data-ttu-id="e3d52-214">PŘÍKLAD 1</span><span class="sxs-lookup"><span data-stu-id="e3d52-214">EXAMPLE 1</span></span>

<span data-ttu-id="e3d52-215">Tento příklad testuje všechna autorizační pravidla, aby bylo možné zobrazit všechna pravidla, které uživateli *contoso\\mhanson* pro připojení k počítači *srv2* a použijte k tomu relaci prostředí Windows PowerShell Konfigurace s názvem *testování*.</span><span class="sxs-lookup"><span data-stu-id="e3d52-215">This example tests all authorization rules in order to display all the rules that allow the user *contoso\\mhanson* to connect to the computer *srv2* and use a Windows PowerShell session configuration named *test*.</span></span>

```
Test-PswaAuthorizationRule -ComputerName srv2.contoso.com -UserName contoso\mhanson -ConfigurationName test
```

### <a name="example-2"></a><span data-ttu-id="e3d52-216">PŘÍKLAD 2</span><span class="sxs-lookup"><span data-stu-id="e3d52-216">EXAMPLE 2</span></span>

<span data-ttu-id="e3d52-217">Tento příklad testy všechna autorizační pravidla ke kontrole které autorizační pravidla platí pro uživatele *contoso\\mhanson*.</span><span class="sxs-lookup"><span data-stu-id="e3d52-217">This example tests all authorization rules to check which authorization rules apply to the user *contoso\\mhanson*.</span></span>

```
Test-PswaAuthorizationRule -UserName contoso\mhanson -ComputerName *
```

## <a name="related-topics"></a><span data-ttu-id="e3d52-218">Příbuzná témata</span><span class="sxs-lookup"><span data-stu-id="e3d52-218">Related topics</span></span>

- [<span data-ttu-id="e3d52-219">Add-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="e3d52-219">Add-PswaAuthorizationRule</span></span>](add-pswaauthorizationrule.md)
- [<span data-ttu-id="e3d52-220">Get-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="e3d52-220">Get-PswaAuthorizationRule</span></span>](get-pswaauthorizationrule.md)
- [<span data-ttu-id="e3d52-221">Rutiny Install-PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="e3d52-221">Install-PswaWebApplication</span></span>](install-pswawebapplication.md)
- [<span data-ttu-id="e3d52-222">Remove-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="e3d52-222">Remove-PswaAuthorizationRule</span></span>](remove-pswaauthorizationrule.md)
