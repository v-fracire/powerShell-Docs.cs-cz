---
description: 
ms.topic: article
ms.prod: powershell
keywords: "rutiny prostředí PowerShell"
ms.date: 2016-12-12
title: Odinstalace pswawebapplication
ms.technology: powershell
ms.openlocfilehash: cc54c94426d754ff2d3bf658e3e92083f02cd6c7
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="uninstall-pswawebapplication"></a><span data-ttu-id="30290-103">Odinstalujte PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="30290-103">Uninstall-PswaWebApplication</span></span>

## <a name="synopsis"></a><span data-ttu-id="30290-104">STRUČNÝ OBSAH</span><span class="sxs-lookup"><span data-stu-id="30290-104">SYNOPSIS</span></span>

<span data-ttu-id="30290-105">Odinstaluje Windows PowerShell® webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="30290-105">Uninstalls the Windows PowerShell® web application.</span></span>

## <a name="syntax"></a><span data-ttu-id="30290-106">SYNTAX</span><span class="sxs-lookup"><span data-stu-id="30290-106">SYNTAX</span></span>

### <a name="default"></a><span data-ttu-id="30290-107">Výchozí</span><span class="sxs-lookup"><span data-stu-id="30290-107">Default</span></span>
```
Uninstall-PswaWebApplication [[-WebApplicationName] <String> ] [-DeleteTestCertificate] [-WebSiteName <String> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

## <a name="description"></a><span data-ttu-id="30290-108">POPIS</span><span class="sxs-lookup"><span data-stu-id="30290-108">DESCRIPTION</span></span>

<span data-ttu-id="30290-109">**Uninstall-PswaWebApplication** rutiny odinstaluje prostředí Windows PowerShell webové aplikace a odebere ze služby IIS na webu.</span><span class="sxs-lookup"><span data-stu-id="30290-109">The **Uninstall-PswaWebApplication** cmdlet uninstalls the Windows PowerShell web application and removes the website from IIS.</span></span> <span data-ttu-id="30290-110">Rutina neodinstaluje službu IIS, ani žádné další funkce, nainstalovat, protože byly požadované pro prostředí Windows PowerShell ke spuštění.</span><span class="sxs-lookup"><span data-stu-id="30290-110">The cmdlet does not uninstall IIS, or any other features installed because they were required for Windows PowerShell to run.</span></span>

## <a name="parameters"></a><span data-ttu-id="30290-111">PARAMETRY</span><span class="sxs-lookup"><span data-stu-id="30290-111">PARAMETERS</span></span>

### <a name="-deletetestcertificate"></a><span data-ttu-id="30290-112">-DeleteTestCertificate</span><span class="sxs-lookup"><span data-stu-id="30290-112">-DeleteTestCertificate</span></span>

<span data-ttu-id="30290-113">Označuje, že testovací certifikáty vytvořená pomocí **nainstalovat\_PswaWebApplication** rutiny (s **UseTestCertificate** parametr) se odstraní.</span><span class="sxs-lookup"><span data-stu-id="30290-113">Indicates that the test certificates created by the **Install\_PswaWebApplication** cmdlet (with the **UseTestCertificate** parameter) is deleted.</span></span>
<span data-ttu-id="30290-114">Testovací certifikát se stejným názvem jako vytvořené **rutiny Install-PswaWebApplication** rutiny se odebere.</span><span class="sxs-lookup"><span data-stu-id="30290-114">Only the test certificate with the same name as the one created by the **Install-PswaWebApplication** cmdlet is removed.</span></span>

|||  
|-|-|
| <span data-ttu-id="30290-115">Aliasy</span><span class="sxs-lookup"><span data-stu-id="30290-115">Aliases</span></span>                              | <span data-ttu-id="30290-116">žádný</span><span class="sxs-lookup"><span data-stu-id="30290-116">none</span></span>                                 |
| <span data-ttu-id="30290-117">Povinné?</span><span class="sxs-lookup"><span data-stu-id="30290-117">Required?</span></span>                            | <span data-ttu-id="30290-118">false</span><span class="sxs-lookup"><span data-stu-id="30290-118">false</span></span>                                |
| <span data-ttu-id="30290-119">Pozice?</span><span class="sxs-lookup"><span data-stu-id="30290-119">Position?</span></span>                            | <span data-ttu-id="30290-120">S názvem</span><span class="sxs-lookup"><span data-stu-id="30290-120">named</span></span>                                |
| <span data-ttu-id="30290-121">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="30290-121">Default Value</span></span>                        | <span data-ttu-id="30290-122">Hodnota TRUE</span><span class="sxs-lookup"><span data-stu-id="30290-122">true</span></span>                                 |
| <span data-ttu-id="30290-123">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="30290-123">Accept Pipeline Input?</span></span>               | <span data-ttu-id="30290-124">false</span><span class="sxs-lookup"><span data-stu-id="30290-124">false</span></span>                                |
| <span data-ttu-id="30290-125">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="30290-125">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="30290-126">false</span><span class="sxs-lookup"><span data-stu-id="30290-126">false</span></span>                                |

### <a name="-webapplicationname-ltstringgt"></a><span data-ttu-id="30290-127">-WebApplicationName &lt;řetězec&gt;</span><span class="sxs-lookup"><span data-stu-id="30290-127">-WebApplicationName &lt;String&gt;</span></span>

<span data-ttu-id="30290-128">Určuje název webové aplikace odinstalovat.</span><span class="sxs-lookup"><span data-stu-id="30290-128">Specifies the name of the web application to uninstall.</span></span>

|||  
|-|-|
| <span data-ttu-id="30290-129">Aliasy</span><span class="sxs-lookup"><span data-stu-id="30290-129">Aliases</span></span>                              | <span data-ttu-id="30290-130">žádný</span><span class="sxs-lookup"><span data-stu-id="30290-130">none</span></span>                                 |
| <span data-ttu-id="30290-131">Povinné?</span><span class="sxs-lookup"><span data-stu-id="30290-131">Required?</span></span>                            | <span data-ttu-id="30290-132">false</span><span class="sxs-lookup"><span data-stu-id="30290-132">false</span></span>                                |
| <span data-ttu-id="30290-133">Pozice?</span><span class="sxs-lookup"><span data-stu-id="30290-133">Position?</span></span>                            | <span data-ttu-id="30290-134">1</span><span class="sxs-lookup"><span data-stu-id="30290-134">1</span></span>                                    |
| <span data-ttu-id="30290-135">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="30290-135">Default Value</span></span>                        | <span data-ttu-id="30290-136">pswa</span><span class="sxs-lookup"><span data-stu-id="30290-136">pswa</span></span>                                 |
| <span data-ttu-id="30290-137">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="30290-137">Accept Pipeline Input?</span></span>               | <span data-ttu-id="30290-138">false</span><span class="sxs-lookup"><span data-stu-id="30290-138">false</span></span>                                |
| <span data-ttu-id="30290-139">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="30290-139">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="30290-140">false</span><span class="sxs-lookup"><span data-stu-id="30290-140">false</span></span>                                |

### <a name="-websitename-ltstringgt"></a><span data-ttu-id="30290-141">-WebSiteName &lt;String&gt;</span><span class="sxs-lookup"><span data-stu-id="30290-141">-WebSiteName &lt;String&gt;</span></span>

<span data-ttu-id="30290-142">Určuje název webové stránky, kde je nainstalována webová aplikace.</span><span class="sxs-lookup"><span data-stu-id="30290-142">Specifies the name of the web site where the web application is installed.</span></span>

|||  
|-|-|
| <span data-ttu-id="30290-143">Aliasy</span><span class="sxs-lookup"><span data-stu-id="30290-143">Aliases</span></span>                              | <span data-ttu-id="30290-144">žádný</span><span class="sxs-lookup"><span data-stu-id="30290-144">none</span></span>                                 |
| <span data-ttu-id="30290-145">Povinné?</span><span class="sxs-lookup"><span data-stu-id="30290-145">Required?</span></span>                            | <span data-ttu-id="30290-146">false</span><span class="sxs-lookup"><span data-stu-id="30290-146">false</span></span>                                |
| <span data-ttu-id="30290-147">Pozice?</span><span class="sxs-lookup"><span data-stu-id="30290-147">Position?</span></span>                            | <span data-ttu-id="30290-148">S názvem</span><span class="sxs-lookup"><span data-stu-id="30290-148">named</span></span>                                |
| <span data-ttu-id="30290-149">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="30290-149">Default Value</span></span>                        | <span data-ttu-id="30290-150">Výchozí web</span><span class="sxs-lookup"><span data-stu-id="30290-150">Default Web Site</span></span>                     |
| <span data-ttu-id="30290-151">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="30290-151">Accept Pipeline Input?</span></span>               | <span data-ttu-id="30290-152">false</span><span class="sxs-lookup"><span data-stu-id="30290-152">false</span></span>                                |
| <span data-ttu-id="30290-153">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="30290-153">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="30290-154">false</span><span class="sxs-lookup"><span data-stu-id="30290-154">false</span></span>                                |

### <a name="-confirm"></a><span data-ttu-id="30290-155">-Confirm</span><span class="sxs-lookup"><span data-stu-id="30290-155">-Confirm</span></span>

<span data-ttu-id="30290-156">Před spuštěním rutiny zobrazí výzvu k potvrzení.</span><span class="sxs-lookup"><span data-stu-id="30290-156">Prompts you for confirmation before running the cmdlet.</span></span>

|||  
|-|-|
| <span data-ttu-id="30290-157">Povinné?</span><span class="sxs-lookup"><span data-stu-id="30290-157">Required?</span></span>                            | <span data-ttu-id="30290-158">false</span><span class="sxs-lookup"><span data-stu-id="30290-158">false</span></span>                                |
| <span data-ttu-id="30290-159">Pozice?</span><span class="sxs-lookup"><span data-stu-id="30290-159">Position?</span></span>                            | <span data-ttu-id="30290-160">S názvem</span><span class="sxs-lookup"><span data-stu-id="30290-160">named</span></span>                                |
| <span data-ttu-id="30290-161">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="30290-161">Default Value</span></span>                        | <span data-ttu-id="30290-162">false</span><span class="sxs-lookup"><span data-stu-id="30290-162">false</span></span>                                |
| <span data-ttu-id="30290-163">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="30290-163">Accept Pipeline Input?</span></span>               | <span data-ttu-id="30290-164">false</span><span class="sxs-lookup"><span data-stu-id="30290-164">false</span></span>                                |
| <span data-ttu-id="30290-165">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="30290-165">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="30290-166">false</span><span class="sxs-lookup"><span data-stu-id="30290-166">false</span></span>                                |

### <a name="-whatif"></a><span data-ttu-id="30290-167">-WhatIf</span><span class="sxs-lookup"><span data-stu-id="30290-167">-WhatIf</span></span>

<span data-ttu-id="30290-168">Zobrazuje, co by se stalo při spuštění rutiny.</span><span class="sxs-lookup"><span data-stu-id="30290-168">Shows what would happen if the cmdlet runs.</span></span>
<span data-ttu-id="30290-169">Rutina není spuštěna.</span><span class="sxs-lookup"><span data-stu-id="30290-169">The cmdlet is not run.</span></span>

|||  
|-|-|
| <span data-ttu-id="30290-170">Povinné?</span><span class="sxs-lookup"><span data-stu-id="30290-170">Required?</span></span>                            | <span data-ttu-id="30290-171">false</span><span class="sxs-lookup"><span data-stu-id="30290-171">false</span></span>                                |
| <span data-ttu-id="30290-172">Pozice?</span><span class="sxs-lookup"><span data-stu-id="30290-172">Position?</span></span>                            | <span data-ttu-id="30290-173">S názvem</span><span class="sxs-lookup"><span data-stu-id="30290-173">named</span></span>                                |
| <span data-ttu-id="30290-174">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="30290-174">Default Value</span></span>                        | <span data-ttu-id="30290-175">false</span><span class="sxs-lookup"><span data-stu-id="30290-175">false</span></span>                                |
| <span data-ttu-id="30290-176">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="30290-176">Accept Pipeline Input?</span></span>               | <span data-ttu-id="30290-177">false</span><span class="sxs-lookup"><span data-stu-id="30290-177">false</span></span>                                |
| <span data-ttu-id="30290-178">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="30290-178">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="30290-179">false</span><span class="sxs-lookup"><span data-stu-id="30290-179">false</span></span>                                |

### <a name="ltcommonparametersgt"></a><span data-ttu-id="30290-180">&lt;CommonParameters&gt;</span><span class="sxs-lookup"><span data-stu-id="30290-180">&lt;CommonParameters&gt;</span></span>

<span data-ttu-id="30290-181">Tato rutina podporuje běžné parametry:-Verbose,-Debug, - ErrorAction, - ErrorVariable,-OutBuffer a - OutVariable.</span><span class="sxs-lookup"><span data-stu-id="30290-181">This cmdlet supports the common parameters: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer, and -OutVariable.</span></span>
<span data-ttu-id="30290-182">Další informace najdete v tématu [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span><span class="sxs-lookup"><span data-stu-id="30290-182">For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span></span>

## <a name="inputs"></a><span data-ttu-id="30290-183">VSTUPY</span><span class="sxs-lookup"><span data-stu-id="30290-183">INPUTS</span></span>

<span data-ttu-id="30290-184">Tato rutina nemá žádný vstup.</span><span class="sxs-lookup"><span data-stu-id="30290-184">This cmdlet takes no input.</span></span>

## <a name="outputs"></a><span data-ttu-id="30290-185">VÝSTUPY</span><span class="sxs-lookup"><span data-stu-id="30290-185">OUTPUTS</span></span>

<span data-ttu-id="30290-186">Tato rutina vrátí žádný výstup.</span><span class="sxs-lookup"><span data-stu-id="30290-186">This cmdlet returns no output.</span></span>

## <a name="examples"></a><span data-ttu-id="30290-187">PŘÍKLADY</span><span class="sxs-lookup"><span data-stu-id="30290-187">EXAMPLES</span></span>

### <a name="example-1"></a><span data-ttu-id="30290-188">PŘÍKLAD 1</span><span class="sxs-lookup"><span data-stu-id="30290-188">EXAMPLE 1</span></span>

<span data-ttu-id="30290-189">Tento příkaz odinstaluje webové aplikace Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="30290-189">This command uninstalls the Windows PowerShell Web Application.</span></span>
<span data-ttu-id="30290-190">Tuto rutinu můžete odinstalovat webovou aplikaci Windows PowerShell, pokud jste nainstalovali pomocí výchozí hodnoty.</span><span class="sxs-lookup"><span data-stu-id="30290-190">You can use this cmdlet to uninstall the Windows PowerShell Web Application if you installed it using the default values.</span></span>

```PowerShell
Uninstall-PswaWebApplication
```

### <a name="example-2"></a><span data-ttu-id="30290-191">PŘÍKLAD 2</span><span class="sxs-lookup"><span data-stu-id="30290-191">EXAMPLE 2</span></span>

<span data-ttu-id="30290-192">Tento příkaz odinstaluje webové aplikace Windows PowerShell a odstraní testovací certifikát přidružený k aplikaci.</span><span class="sxs-lookup"><span data-stu-id="30290-192">This command uninstalls the Windows PowerShell Web Application, and deletes the test certificate associated with the application.</span></span>
<span data-ttu-id="30290-193">Tuto rutinu můžete odinstalovat webovou aplikaci Windows PowerShell, pokud jste nainstalovali pomocí výchozí hodnoty a vytvořit testovací certifikát.</span><span class="sxs-lookup"><span data-stu-id="30290-193">You can use this cmdlet to uninstall the Windows PowerShell Web Application if you installed it using the default values and created a test certificate.</span></span>

```PowerShell
Uninstall-PswaWebApplication -DeleteTestCertificate
```

### <a name="example-3-example-3-subheading"></a><span data-ttu-id="30290-194">Příklad 3 {#example-3 .subHeading}</span><span class="sxs-lookup"><span data-stu-id="30290-194">EXAMPLE 3 {#example-3 .subHeading}</span></span>

<span data-ttu-id="30290-195">Tento příkaz odinstaluje webové aplikace Windows PowerShell, pokud vlastní web a aplikaci se zadaly během instalace.</span><span class="sxs-lookup"><span data-stu-id="30290-195">This command uninstalls the Windows PowerShell Web Application when a custom website and application were specified during the install.</span></span>
<span data-ttu-id="30290-196">Příkaz odebere web s názvem *server* a aplikaci s názvem *TestApplication* a určuje, že testovací certifikáty přidružené aplikace jsou také odstraněny.</span><span class="sxs-lookup"><span data-stu-id="30290-196">The command removes the website named *MySite* and the application named *TestApplication* and specifies that the test certificates associated with the application are also deleted.</span></span>

```
Uninstall-PswaWebApplication -WebApplicationName TestApplication -WebsiteName MySite -DeleteTestCertificate
```

## <a name="related-topics"></a><span data-ttu-id="30290-197">Příbuzná témata</span><span class="sxs-lookup"><span data-stu-id="30290-197">Related topics</span></span>

- [<span data-ttu-id="30290-198">Add-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="30290-198">Add-PswaAuthorizationRule</span></span>](add-pswaauthorizationrule.md)
- [<span data-ttu-id="30290-199">Get-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="30290-199">Get-PswaAuthorizationRule</span></span>](get-pswaauthorizationrule.md)
- [<span data-ttu-id="30290-200">Rutiny Install-PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="30290-200">Install-PswaWebApplication</span></span>](install-pswawebapplication.md)
- [<span data-ttu-id="30290-201">Remove-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="30290-201">Remove-PswaAuthorizationRule</span></span>](remove-pswaauthorizationrule.md)
- [<span data-ttu-id="30290-202">Test-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="30290-202">Test-PswaAuthorizationRule</span></span>](test-pswaauthorizationrule.md)
