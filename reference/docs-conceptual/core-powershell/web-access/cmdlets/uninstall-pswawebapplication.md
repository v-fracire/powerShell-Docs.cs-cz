---
description: 
manager: carmonm
ms.topic: article
author: jpjofre
ms.prod: powershell
keywords: "rutiny prostředí PowerShell"
ms.date: 2016-12-12
title: Odinstalace pswawebapplication
ms.technology: powershell
ms.openlocfilehash: 5fe608b3bfbb90f842f16c1f5a8c51879589cf6d
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/08/2017
---
# <a name="uninstall-pswawebapplication"></a><span data-ttu-id="ba765-103">Odinstalujte PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="ba765-103">Uninstall-PswaWebApplication</span></span>

## <a name="synopsis"></a><span data-ttu-id="ba765-104">STRUČNÝ OBSAH</span><span class="sxs-lookup"><span data-stu-id="ba765-104">SYNOPSIS</span></span>

<span data-ttu-id="ba765-105">Odinstaluje Windows PowerShell® webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="ba765-105">Uninstalls the Windows PowerShell® web application.</span></span>

## <a name="syntax"></a><span data-ttu-id="ba765-106">SYNTAXE</span><span class="sxs-lookup"><span data-stu-id="ba765-106">SYNTAX</span></span>

### <a name="default"></a><span data-ttu-id="ba765-107">Výchozí</span><span class="sxs-lookup"><span data-stu-id="ba765-107">Default</span></span>
```
Uninstall-PswaWebApplication [[-WebApplicationName] <String> ] [-DeleteTestCertificate] [-WebSiteName <String> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

## <a name="description"></a><span data-ttu-id="ba765-108">POPIS</span><span class="sxs-lookup"><span data-stu-id="ba765-108">DESCRIPTION</span></span>

<span data-ttu-id="ba765-109">**Uninstall-PswaWebApplication** rutiny odinstaluje prostředí Windows PowerShell webové aplikace a odebere ze služby IIS na webu.</span><span class="sxs-lookup"><span data-stu-id="ba765-109">The **Uninstall-PswaWebApplication** cmdlet uninstalls the Windows PowerShell web application and removes the website from IIS.</span></span> <span data-ttu-id="ba765-110">Rutina neodinstaluje službu IIS, ani žádné další funkce, nainstalovat, protože byly požadované pro prostředí Windows PowerShell ke spuštění.</span><span class="sxs-lookup"><span data-stu-id="ba765-110">The cmdlet does not uninstall IIS, or any other features installed because they were required for Windows PowerShell to run.</span></span>

## <a name="parameters"></a><span data-ttu-id="ba765-111">PARAMETRY</span><span class="sxs-lookup"><span data-stu-id="ba765-111">PARAMETERS</span></span>

### <a name="-deletetestcertificate"></a><span data-ttu-id="ba765-112">-DeleteTestCertificate</span><span class="sxs-lookup"><span data-stu-id="ba765-112">-DeleteTestCertificate</span></span>

<span data-ttu-id="ba765-113">Označuje, že testovací certifikáty vytvořená pomocí **nainstalovat\_PswaWebApplication** rutiny (s **UseTestCertificate** parametr) se odstraní.</span><span class="sxs-lookup"><span data-stu-id="ba765-113">Indicates that the test certificates created by the **Install\_PswaWebApplication** cmdlet (with the **UseTestCertificate** parameter) is deleted.</span></span>
<span data-ttu-id="ba765-114">Testovací certifikát se stejným názvem jako vytvořené **rutiny Install-PswaWebApplication** rutiny se odebere.</span><span class="sxs-lookup"><span data-stu-id="ba765-114">Only the test certificate with the same name as the one created by the **Install-PswaWebApplication** cmdlet is removed.</span></span>

|||  
|-|-|
| <span data-ttu-id="ba765-115">Aliasy</span><span class="sxs-lookup"><span data-stu-id="ba765-115">Aliases</span></span>                              | <span data-ttu-id="ba765-116">žádný</span><span class="sxs-lookup"><span data-stu-id="ba765-116">none</span></span>                                 |
| <span data-ttu-id="ba765-117">Povinné?</span><span class="sxs-lookup"><span data-stu-id="ba765-117">Required?</span></span>                            | <span data-ttu-id="ba765-118">false</span><span class="sxs-lookup"><span data-stu-id="ba765-118">false</span></span>                                |
| <span data-ttu-id="ba765-119">Pozice?</span><span class="sxs-lookup"><span data-stu-id="ba765-119">Position?</span></span>                            | <span data-ttu-id="ba765-120">S názvem</span><span class="sxs-lookup"><span data-stu-id="ba765-120">named</span></span>                                |
| <span data-ttu-id="ba765-121">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="ba765-121">Default Value</span></span>                        | <span data-ttu-id="ba765-122">Hodnota TRUE</span><span class="sxs-lookup"><span data-stu-id="ba765-122">true</span></span>                                 |
| <span data-ttu-id="ba765-123">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="ba765-123">Accept Pipeline Input?</span></span>               | <span data-ttu-id="ba765-124">false</span><span class="sxs-lookup"><span data-stu-id="ba765-124">false</span></span>                                |
| <span data-ttu-id="ba765-125">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="ba765-125">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="ba765-126">false</span><span class="sxs-lookup"><span data-stu-id="ba765-126">false</span></span>                                |

### <a name="-webapplicationname-ltstringgt"></a><span data-ttu-id="ba765-127">-WebApplicationName &lt;řetězec&gt;</span><span class="sxs-lookup"><span data-stu-id="ba765-127">-WebApplicationName &lt;String&gt;</span></span>

<span data-ttu-id="ba765-128">Určuje název webové aplikace odinstalovat.</span><span class="sxs-lookup"><span data-stu-id="ba765-128">Specifies the name of the web application to uninstall.</span></span>

|||  
|-|-|
| <span data-ttu-id="ba765-129">Aliasy</span><span class="sxs-lookup"><span data-stu-id="ba765-129">Aliases</span></span>                              | <span data-ttu-id="ba765-130">žádný</span><span class="sxs-lookup"><span data-stu-id="ba765-130">none</span></span>                                 |
| <span data-ttu-id="ba765-131">Povinné?</span><span class="sxs-lookup"><span data-stu-id="ba765-131">Required?</span></span>                            | <span data-ttu-id="ba765-132">false</span><span class="sxs-lookup"><span data-stu-id="ba765-132">false</span></span>                                |
| <span data-ttu-id="ba765-133">Pozice?</span><span class="sxs-lookup"><span data-stu-id="ba765-133">Position?</span></span>                            | <span data-ttu-id="ba765-134">1</span><span class="sxs-lookup"><span data-stu-id="ba765-134">1</span></span>                                    |
| <span data-ttu-id="ba765-135">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="ba765-135">Default Value</span></span>                        | <span data-ttu-id="ba765-136">pswa</span><span class="sxs-lookup"><span data-stu-id="ba765-136">pswa</span></span>                                 |
| <span data-ttu-id="ba765-137">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="ba765-137">Accept Pipeline Input?</span></span>               | <span data-ttu-id="ba765-138">false</span><span class="sxs-lookup"><span data-stu-id="ba765-138">false</span></span>                                |
| <span data-ttu-id="ba765-139">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="ba765-139">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="ba765-140">false</span><span class="sxs-lookup"><span data-stu-id="ba765-140">false</span></span>                                |

### <a name="-websitename-ltstringgt"></a><span data-ttu-id="ba765-141">-Zadaným hodnotám WebSiteName &lt;řetězec&gt;</span><span class="sxs-lookup"><span data-stu-id="ba765-141">-WebSiteName &lt;String&gt;</span></span>

<span data-ttu-id="ba765-142">Určuje název webové stránky, kde je nainstalována webová aplikace.</span><span class="sxs-lookup"><span data-stu-id="ba765-142">Specifies the name of the web site where the web application is installed.</span></span>

|||  
|-|-|
| <span data-ttu-id="ba765-143">Aliasy</span><span class="sxs-lookup"><span data-stu-id="ba765-143">Aliases</span></span>                              | <span data-ttu-id="ba765-144">žádný</span><span class="sxs-lookup"><span data-stu-id="ba765-144">none</span></span>                                 |
| <span data-ttu-id="ba765-145">Povinné?</span><span class="sxs-lookup"><span data-stu-id="ba765-145">Required?</span></span>                            | <span data-ttu-id="ba765-146">false</span><span class="sxs-lookup"><span data-stu-id="ba765-146">false</span></span>                                |
| <span data-ttu-id="ba765-147">Pozice?</span><span class="sxs-lookup"><span data-stu-id="ba765-147">Position?</span></span>                            | <span data-ttu-id="ba765-148">S názvem</span><span class="sxs-lookup"><span data-stu-id="ba765-148">named</span></span>                                |
| <span data-ttu-id="ba765-149">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="ba765-149">Default Value</span></span>                        | <span data-ttu-id="ba765-150">Výchozí web</span><span class="sxs-lookup"><span data-stu-id="ba765-150">Default Web Site</span></span>                     |
| <span data-ttu-id="ba765-151">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="ba765-151">Accept Pipeline Input?</span></span>               | <span data-ttu-id="ba765-152">false</span><span class="sxs-lookup"><span data-stu-id="ba765-152">false</span></span>                                |
| <span data-ttu-id="ba765-153">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="ba765-153">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="ba765-154">false</span><span class="sxs-lookup"><span data-stu-id="ba765-154">false</span></span>                                |

### <a name="-confirm"></a><span data-ttu-id="ba765-155">-Confirm</span><span class="sxs-lookup"><span data-stu-id="ba765-155">-Confirm</span></span>

<span data-ttu-id="ba765-156">Před spuštěním rutiny zobrazí výzvu k potvrzení.</span><span class="sxs-lookup"><span data-stu-id="ba765-156">Prompts you for confirmation before running the cmdlet.</span></span>

|||  
|-|-|
| <span data-ttu-id="ba765-157">Povinné?</span><span class="sxs-lookup"><span data-stu-id="ba765-157">Required?</span></span>                            | <span data-ttu-id="ba765-158">false</span><span class="sxs-lookup"><span data-stu-id="ba765-158">false</span></span>                                |
| <span data-ttu-id="ba765-159">Pozice?</span><span class="sxs-lookup"><span data-stu-id="ba765-159">Position?</span></span>                            | <span data-ttu-id="ba765-160">S názvem</span><span class="sxs-lookup"><span data-stu-id="ba765-160">named</span></span>                                |
| <span data-ttu-id="ba765-161">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="ba765-161">Default Value</span></span>                        | <span data-ttu-id="ba765-162">false</span><span class="sxs-lookup"><span data-stu-id="ba765-162">false</span></span>                                |
| <span data-ttu-id="ba765-163">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="ba765-163">Accept Pipeline Input?</span></span>               | <span data-ttu-id="ba765-164">false</span><span class="sxs-lookup"><span data-stu-id="ba765-164">false</span></span>                                |
| <span data-ttu-id="ba765-165">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="ba765-165">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="ba765-166">false</span><span class="sxs-lookup"><span data-stu-id="ba765-166">false</span></span>                                |

### <a name="-whatif"></a><span data-ttu-id="ba765-167">-WhatIf</span><span class="sxs-lookup"><span data-stu-id="ba765-167">-WhatIf</span></span>

<span data-ttu-id="ba765-168">Zobrazuje, co by se stalo při spuštění rutiny.</span><span class="sxs-lookup"><span data-stu-id="ba765-168">Shows what would happen if the cmdlet runs.</span></span>
<span data-ttu-id="ba765-169">Rutina není spuštěna.</span><span class="sxs-lookup"><span data-stu-id="ba765-169">The cmdlet is not run.</span></span>

|||  
|-|-|
| <span data-ttu-id="ba765-170">Povinné?</span><span class="sxs-lookup"><span data-stu-id="ba765-170">Required?</span></span>                            | <span data-ttu-id="ba765-171">false</span><span class="sxs-lookup"><span data-stu-id="ba765-171">false</span></span>                                |
| <span data-ttu-id="ba765-172">Pozice?</span><span class="sxs-lookup"><span data-stu-id="ba765-172">Position?</span></span>                            | <span data-ttu-id="ba765-173">S názvem</span><span class="sxs-lookup"><span data-stu-id="ba765-173">named</span></span>                                |
| <span data-ttu-id="ba765-174">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="ba765-174">Default Value</span></span>                        | <span data-ttu-id="ba765-175">false</span><span class="sxs-lookup"><span data-stu-id="ba765-175">false</span></span>                                |
| <span data-ttu-id="ba765-176">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="ba765-176">Accept Pipeline Input?</span></span>               | <span data-ttu-id="ba765-177">false</span><span class="sxs-lookup"><span data-stu-id="ba765-177">false</span></span>                                |
| <span data-ttu-id="ba765-178">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="ba765-178">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="ba765-179">false</span><span class="sxs-lookup"><span data-stu-id="ba765-179">false</span></span>                                |

### <a name="ltcommonparametersgt"></a><span data-ttu-id="ba765-180">&lt;CommonParameters&gt;</span><span class="sxs-lookup"><span data-stu-id="ba765-180">&lt;CommonParameters&gt;</span></span>

<span data-ttu-id="ba765-181">Tato rutina podporuje běžné parametry:-Verbose,-Debug, - ErrorAction, - ErrorVariable,-OutBuffer a - OutVariable.</span><span class="sxs-lookup"><span data-stu-id="ba765-181">This cmdlet supports the common parameters: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer, and -OutVariable.</span></span>
<span data-ttu-id="ba765-182">Další informace najdete v tématu [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span><span class="sxs-lookup"><span data-stu-id="ba765-182">For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span></span>

## <a name="inputs"></a><span data-ttu-id="ba765-183">VSTUPY</span><span class="sxs-lookup"><span data-stu-id="ba765-183">INPUTS</span></span>

<span data-ttu-id="ba765-184">Tato rutina nemá žádný vstup.</span><span class="sxs-lookup"><span data-stu-id="ba765-184">This cmdlet takes no input.</span></span>

## <a name="outputs"></a><span data-ttu-id="ba765-185">VÝSTUPY</span><span class="sxs-lookup"><span data-stu-id="ba765-185">OUTPUTS</span></span>

<span data-ttu-id="ba765-186">Tato rutina vrátí žádný výstup.</span><span class="sxs-lookup"><span data-stu-id="ba765-186">This cmdlet returns no output.</span></span>

## <a name="examples"></a><span data-ttu-id="ba765-187">PŘÍKLADY</span><span class="sxs-lookup"><span data-stu-id="ba765-187">EXAMPLES</span></span>

### <a name="example-1"></a><span data-ttu-id="ba765-188">PŘÍKLAD 1</span><span class="sxs-lookup"><span data-stu-id="ba765-188">EXAMPLE 1</span></span>

<span data-ttu-id="ba765-189">Tento příkaz odinstaluje webové aplikace Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ba765-189">This command uninstalls the Windows PowerShell Web Application.</span></span>
<span data-ttu-id="ba765-190">Tuto rutinu můžete odinstalovat webovou aplikaci Windows PowerShell, pokud jste nainstalovali pomocí výchozí hodnoty.</span><span class="sxs-lookup"><span data-stu-id="ba765-190">You can use this cmdlet to uninstall the Windows PowerShell Web Application if you installed it using the default values.</span></span>

```PowerShell
Uninstall-PswaWebApplication
```

### <a name="example-2"></a><span data-ttu-id="ba765-191">PŘÍKLAD 2</span><span class="sxs-lookup"><span data-stu-id="ba765-191">EXAMPLE 2</span></span>

<span data-ttu-id="ba765-192">Tento příkaz odinstaluje webové aplikace Windows PowerShell a odstraní testovací certifikát přidružený k aplikaci.</span><span class="sxs-lookup"><span data-stu-id="ba765-192">This command uninstalls the Windows PowerShell Web Application, and deletes the test certificate associated with the application.</span></span>
<span data-ttu-id="ba765-193">Tuto rutinu můžete odinstalovat webovou aplikaci Windows PowerShell, pokud jste nainstalovali pomocí výchozí hodnoty a vytvořit testovací certifikát.</span><span class="sxs-lookup"><span data-stu-id="ba765-193">You can use this cmdlet to uninstall the Windows PowerShell Web Application if you installed it using the default values and created a test certificate.</span></span>

```PowerShell
Uninstall-PswaWebApplication -DeleteTestCertificate
```

### <a name="example-3-example-3-subheading"></a><span data-ttu-id="ba765-194">Příklad 3 {#example-3 .subHeading}</span><span class="sxs-lookup"><span data-stu-id="ba765-194">EXAMPLE 3 {#example-3 .subHeading}</span></span>

<span data-ttu-id="ba765-195">Tento příkaz odinstaluje webové aplikace Windows PowerShell, pokud vlastní web a aplikaci se zadaly během instalace.</span><span class="sxs-lookup"><span data-stu-id="ba765-195">This command uninstalls the Windows PowerShell Web Application when a custom website and application were specified during the install.</span></span>
<span data-ttu-id="ba765-196">Příkaz odebere web s názvem *server* a aplikaci s názvem *TestApplication* a určuje, že testovací certifikáty přidružené aplikace jsou také odstraněny.</span><span class="sxs-lookup"><span data-stu-id="ba765-196">The command removes the website named *MySite* and the application named *TestApplication* and specifies that the test certificates associated with the application are also deleted.</span></span>

```
Uninstall-PswaWebApplication -WebApplicationName TestApplication -WebsiteName MySite -DeleteTestCertificate
```

## <a name="related-topics"></a><span data-ttu-id="ba765-197">Příbuzná témata</span><span class="sxs-lookup"><span data-stu-id="ba765-197">Related topics</span></span>

- [<span data-ttu-id="ba765-198">Add-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="ba765-198">Add-PswaAuthorizationRule</span></span>](add-pswaauthorizationrule.md)
- [<span data-ttu-id="ba765-199">Get-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="ba765-199">Get-PswaAuthorizationRule</span></span>](get-pswaauthorizationrule.md)
- [<span data-ttu-id="ba765-200">Rutiny Install-PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="ba765-200">Install-PswaWebApplication</span></span>](install-pswawebapplication.md)
- [<span data-ttu-id="ba765-201">Remove-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="ba765-201">Remove-PswaAuthorizationRule</span></span>](remove-pswaauthorizationrule.md)
- [<span data-ttu-id="ba765-202">Test-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="ba765-202">Test-PswaAuthorizationRule</span></span>](test-pswaauthorizationrule.md)
