---
description: ''
ms.topic: article
ms.prod: powershell
keywords: rutiny prostředí PowerShell
ms.date: 12/12/2016
title: Odinstalace pswawebapplication
ms.technology: powershell
ms.openlocfilehash: 139c8358a24e54dec630f8c78737728330ba4aa2
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="uninstall-pswawebapplication"></a><span data-ttu-id="4d217-103">Odinstalujte PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="4d217-103">Uninstall-PswaWebApplication</span></span>

## <a name="synopsis"></a><span data-ttu-id="4d217-104">STRUČNÝ OBSAH</span><span class="sxs-lookup"><span data-stu-id="4d217-104">SYNOPSIS</span></span>

<span data-ttu-id="4d217-105">Odinstaluje Windows PowerShell® webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="4d217-105">Uninstalls the Windows PowerShell® web application.</span></span>

## <a name="syntax"></a><span data-ttu-id="4d217-106">SYNTAX</span><span class="sxs-lookup"><span data-stu-id="4d217-106">SYNTAX</span></span>

### <a name="default"></a><span data-ttu-id="4d217-107">Výchozí</span><span class="sxs-lookup"><span data-stu-id="4d217-107">Default</span></span>
```
Uninstall-PswaWebApplication [[-WebApplicationName] <String> ] [-DeleteTestCertificate] [-WebSiteName <String> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

## <a name="description"></a><span data-ttu-id="4d217-108">POPIS</span><span class="sxs-lookup"><span data-stu-id="4d217-108">DESCRIPTION</span></span>

<span data-ttu-id="4d217-109">**Uninstall-PswaWebApplication** rutiny odinstaluje prostředí Windows PowerShell webové aplikace a odebere ze služby IIS na webu.</span><span class="sxs-lookup"><span data-stu-id="4d217-109">The **Uninstall-PswaWebApplication** cmdlet uninstalls the Windows PowerShell web application and removes the website from IIS.</span></span> <span data-ttu-id="4d217-110">Rutina neodinstaluje službu IIS, ani žádné další funkce, nainstalovat, protože byly požadované pro prostředí Windows PowerShell ke spuštění.</span><span class="sxs-lookup"><span data-stu-id="4d217-110">The cmdlet does not uninstall IIS, or any other features installed because they were required for Windows PowerShell to run.</span></span>

## <a name="parameters"></a><span data-ttu-id="4d217-111">PARAMETRY</span><span class="sxs-lookup"><span data-stu-id="4d217-111">PARAMETERS</span></span>

### <a name="-deletetestcertificate"></a><span data-ttu-id="4d217-112">-DeleteTestCertificate</span><span class="sxs-lookup"><span data-stu-id="4d217-112">-DeleteTestCertificate</span></span>

<span data-ttu-id="4d217-113">Označuje, že testovací certifikáty vytvořená pomocí **nainstalovat\_PswaWebApplication** rutiny (s **UseTestCertificate** parametr) se odstraní.</span><span class="sxs-lookup"><span data-stu-id="4d217-113">Indicates that the test certificates created by the **Install\_PswaWebApplication** cmdlet (with the **UseTestCertificate** parameter) is deleted.</span></span>
<span data-ttu-id="4d217-114">Testovací certifikát se stejným názvem jako vytvořené **rutiny Install-PswaWebApplication** rutiny se odebere.</span><span class="sxs-lookup"><span data-stu-id="4d217-114">Only the test certificate with the same name as the one created by the **Install-PswaWebApplication** cmdlet is removed.</span></span>

|||
|-|-|
| <span data-ttu-id="4d217-115">Aliasy</span><span class="sxs-lookup"><span data-stu-id="4d217-115">Aliases</span></span>                              | <span data-ttu-id="4d217-116">žádný</span><span class="sxs-lookup"><span data-stu-id="4d217-116">none</span></span>                                 |
| <span data-ttu-id="4d217-117">Povinné?</span><span class="sxs-lookup"><span data-stu-id="4d217-117">Required?</span></span>                            | <span data-ttu-id="4d217-118">false</span><span class="sxs-lookup"><span data-stu-id="4d217-118">false</span></span>                                |
| <span data-ttu-id="4d217-119">Pozice?</span><span class="sxs-lookup"><span data-stu-id="4d217-119">Position?</span></span>                            | <span data-ttu-id="4d217-120">S názvem</span><span class="sxs-lookup"><span data-stu-id="4d217-120">named</span></span>                                |
| <span data-ttu-id="4d217-121">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="4d217-121">Default Value</span></span>                        | <span data-ttu-id="4d217-122">Hodnota TRUE</span><span class="sxs-lookup"><span data-stu-id="4d217-122">true</span></span>                                 |
| <span data-ttu-id="4d217-123">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="4d217-123">Accept Pipeline Input?</span></span>               | <span data-ttu-id="4d217-124">false</span><span class="sxs-lookup"><span data-stu-id="4d217-124">false</span></span>                                |
| <span data-ttu-id="4d217-125">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="4d217-125">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="4d217-126">false</span><span class="sxs-lookup"><span data-stu-id="4d217-126">false</span></span>                                |

### <a name="-webapplicationname-ltstringgt"></a><span data-ttu-id="4d217-127">-WebApplicationName &lt;řetězec&gt;</span><span class="sxs-lookup"><span data-stu-id="4d217-127">-WebApplicationName &lt;String&gt;</span></span>

<span data-ttu-id="4d217-128">Určuje název webové aplikace odinstalovat.</span><span class="sxs-lookup"><span data-stu-id="4d217-128">Specifies the name of the web application to uninstall.</span></span>

|||
|-|-|
| <span data-ttu-id="4d217-129">Aliasy</span><span class="sxs-lookup"><span data-stu-id="4d217-129">Aliases</span></span>                              | <span data-ttu-id="4d217-130">žádný</span><span class="sxs-lookup"><span data-stu-id="4d217-130">none</span></span>                                 |
| <span data-ttu-id="4d217-131">Povinné?</span><span class="sxs-lookup"><span data-stu-id="4d217-131">Required?</span></span>                            | <span data-ttu-id="4d217-132">false</span><span class="sxs-lookup"><span data-stu-id="4d217-132">false</span></span>                                |
| <span data-ttu-id="4d217-133">Pozice?</span><span class="sxs-lookup"><span data-stu-id="4d217-133">Position?</span></span>                            | <span data-ttu-id="4d217-134">1</span><span class="sxs-lookup"><span data-stu-id="4d217-134">1</span></span>                                    |
| <span data-ttu-id="4d217-135">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="4d217-135">Default Value</span></span>                        | <span data-ttu-id="4d217-136">pswa</span><span class="sxs-lookup"><span data-stu-id="4d217-136">pswa</span></span>                                 |
| <span data-ttu-id="4d217-137">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="4d217-137">Accept Pipeline Input?</span></span>               | <span data-ttu-id="4d217-138">false</span><span class="sxs-lookup"><span data-stu-id="4d217-138">false</span></span>                                |
| <span data-ttu-id="4d217-139">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="4d217-139">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="4d217-140">false</span><span class="sxs-lookup"><span data-stu-id="4d217-140">false</span></span>                                |

### <a name="-websitename-ltstringgt"></a><span data-ttu-id="4d217-141">-WebSiteName &lt;String&gt;</span><span class="sxs-lookup"><span data-stu-id="4d217-141">-WebSiteName &lt;String&gt;</span></span>

<span data-ttu-id="4d217-142">Určuje název webové stránky, kde je nainstalována webová aplikace.</span><span class="sxs-lookup"><span data-stu-id="4d217-142">Specifies the name of the web site where the web application is installed.</span></span>

|||
|-|-|
| <span data-ttu-id="4d217-143">Aliasy</span><span class="sxs-lookup"><span data-stu-id="4d217-143">Aliases</span></span>                              | <span data-ttu-id="4d217-144">žádný</span><span class="sxs-lookup"><span data-stu-id="4d217-144">none</span></span>                                 |
| <span data-ttu-id="4d217-145">Povinné?</span><span class="sxs-lookup"><span data-stu-id="4d217-145">Required?</span></span>                            | <span data-ttu-id="4d217-146">false</span><span class="sxs-lookup"><span data-stu-id="4d217-146">false</span></span>                                |
| <span data-ttu-id="4d217-147">Pozice?</span><span class="sxs-lookup"><span data-stu-id="4d217-147">Position?</span></span>                            | <span data-ttu-id="4d217-148">S názvem</span><span class="sxs-lookup"><span data-stu-id="4d217-148">named</span></span>                                |
| <span data-ttu-id="4d217-149">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="4d217-149">Default Value</span></span>                        | <span data-ttu-id="4d217-150">Výchozí web</span><span class="sxs-lookup"><span data-stu-id="4d217-150">Default Web Site</span></span>                     |
| <span data-ttu-id="4d217-151">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="4d217-151">Accept Pipeline Input?</span></span>               | <span data-ttu-id="4d217-152">false</span><span class="sxs-lookup"><span data-stu-id="4d217-152">false</span></span>                                |
| <span data-ttu-id="4d217-153">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="4d217-153">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="4d217-154">false</span><span class="sxs-lookup"><span data-stu-id="4d217-154">false</span></span>                                |

### <a name="-confirm"></a><span data-ttu-id="4d217-155">-Confirm</span><span class="sxs-lookup"><span data-stu-id="4d217-155">-Confirm</span></span>

<span data-ttu-id="4d217-156">Před spuštěním rutiny zobrazí výzvu k potvrzení.</span><span class="sxs-lookup"><span data-stu-id="4d217-156">Prompts you for confirmation before running the cmdlet.</span></span>

|||
|-|-|
| <span data-ttu-id="4d217-157">Povinné?</span><span class="sxs-lookup"><span data-stu-id="4d217-157">Required?</span></span>                            | <span data-ttu-id="4d217-158">false</span><span class="sxs-lookup"><span data-stu-id="4d217-158">false</span></span>                                |
| <span data-ttu-id="4d217-159">Pozice?</span><span class="sxs-lookup"><span data-stu-id="4d217-159">Position?</span></span>                            | <span data-ttu-id="4d217-160">S názvem</span><span class="sxs-lookup"><span data-stu-id="4d217-160">named</span></span>                                |
| <span data-ttu-id="4d217-161">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="4d217-161">Default Value</span></span>                        | <span data-ttu-id="4d217-162">false</span><span class="sxs-lookup"><span data-stu-id="4d217-162">false</span></span>                                |
| <span data-ttu-id="4d217-163">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="4d217-163">Accept Pipeline Input?</span></span>               | <span data-ttu-id="4d217-164">false</span><span class="sxs-lookup"><span data-stu-id="4d217-164">false</span></span>                                |
| <span data-ttu-id="4d217-165">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="4d217-165">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="4d217-166">false</span><span class="sxs-lookup"><span data-stu-id="4d217-166">false</span></span>                                |

### <a name="-whatif"></a><span data-ttu-id="4d217-167">-WhatIf</span><span class="sxs-lookup"><span data-stu-id="4d217-167">-WhatIf</span></span>

<span data-ttu-id="4d217-168">Zobrazuje, co by se stalo při spuštění rutiny.</span><span class="sxs-lookup"><span data-stu-id="4d217-168">Shows what would happen if the cmdlet runs.</span></span>
<span data-ttu-id="4d217-169">Rutina není spuštěna.</span><span class="sxs-lookup"><span data-stu-id="4d217-169">The cmdlet is not run.</span></span>

|||
|-|-|
| <span data-ttu-id="4d217-170">Povinné?</span><span class="sxs-lookup"><span data-stu-id="4d217-170">Required?</span></span>                            | <span data-ttu-id="4d217-171">false</span><span class="sxs-lookup"><span data-stu-id="4d217-171">false</span></span>                                |
| <span data-ttu-id="4d217-172">Pozice?</span><span class="sxs-lookup"><span data-stu-id="4d217-172">Position?</span></span>                            | <span data-ttu-id="4d217-173">S názvem</span><span class="sxs-lookup"><span data-stu-id="4d217-173">named</span></span>                                |
| <span data-ttu-id="4d217-174">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="4d217-174">Default Value</span></span>                        | <span data-ttu-id="4d217-175">false</span><span class="sxs-lookup"><span data-stu-id="4d217-175">false</span></span>                                |
| <span data-ttu-id="4d217-176">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="4d217-176">Accept Pipeline Input?</span></span>               | <span data-ttu-id="4d217-177">false</span><span class="sxs-lookup"><span data-stu-id="4d217-177">false</span></span>                                |
| <span data-ttu-id="4d217-178">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="4d217-178">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="4d217-179">false</span><span class="sxs-lookup"><span data-stu-id="4d217-179">false</span></span>                                |

### <a name="ltcommonparametersgt"></a><span data-ttu-id="4d217-180">&lt;CommonParameters&gt;</span><span class="sxs-lookup"><span data-stu-id="4d217-180">&lt;CommonParameters&gt;</span></span>

<span data-ttu-id="4d217-181">Tato rutina podporuje běžné parametry:-Verbose,-Debug, - ErrorAction, - ErrorVariable,-OutBuffer a - OutVariable.</span><span class="sxs-lookup"><span data-stu-id="4d217-181">This cmdlet supports the common parameters: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer, and -OutVariable.</span></span>
<span data-ttu-id="4d217-182">Další informace najdete v tématu [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span><span class="sxs-lookup"><span data-stu-id="4d217-182">For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span></span>

## <a name="inputs"></a><span data-ttu-id="4d217-183">VSTUPY</span><span class="sxs-lookup"><span data-stu-id="4d217-183">INPUTS</span></span>

<span data-ttu-id="4d217-184">Tato rutina nemá žádný vstup.</span><span class="sxs-lookup"><span data-stu-id="4d217-184">This cmdlet takes no input.</span></span>

## <a name="outputs"></a><span data-ttu-id="4d217-185">VÝSTUPY</span><span class="sxs-lookup"><span data-stu-id="4d217-185">OUTPUTS</span></span>

<span data-ttu-id="4d217-186">Tato rutina vrátí žádný výstup.</span><span class="sxs-lookup"><span data-stu-id="4d217-186">This cmdlet returns no output.</span></span>

## <a name="examples"></a><span data-ttu-id="4d217-187">PŘÍKLADY</span><span class="sxs-lookup"><span data-stu-id="4d217-187">EXAMPLES</span></span>

### <a name="example-1"></a><span data-ttu-id="4d217-188">PŘÍKLAD 1</span><span class="sxs-lookup"><span data-stu-id="4d217-188">EXAMPLE 1</span></span>

<span data-ttu-id="4d217-189">Tento příkaz odinstaluje webové aplikace Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="4d217-189">This command uninstalls the Windows PowerShell Web Application.</span></span>
<span data-ttu-id="4d217-190">Tuto rutinu můžete odinstalovat webovou aplikaci Windows PowerShell, pokud jste nainstalovali pomocí výchozí hodnoty.</span><span class="sxs-lookup"><span data-stu-id="4d217-190">You can use this cmdlet to uninstall the Windows PowerShell Web Application if you installed it using the default values.</span></span>

```PowerShell
Uninstall-PswaWebApplication
```

### <a name="example-2"></a><span data-ttu-id="4d217-191">PŘÍKLAD 2</span><span class="sxs-lookup"><span data-stu-id="4d217-191">EXAMPLE 2</span></span>

<span data-ttu-id="4d217-192">Tento příkaz odinstaluje webové aplikace Windows PowerShell a odstraní testovací certifikát přidružený k aplikaci.</span><span class="sxs-lookup"><span data-stu-id="4d217-192">This command uninstalls the Windows PowerShell Web Application, and deletes the test certificate associated with the application.</span></span>
<span data-ttu-id="4d217-193">Tuto rutinu můžete odinstalovat webovou aplikaci Windows PowerShell, pokud jste nainstalovali pomocí výchozí hodnoty a vytvořit testovací certifikát.</span><span class="sxs-lookup"><span data-stu-id="4d217-193">You can use this cmdlet to uninstall the Windows PowerShell Web Application if you installed it using the default values and created a test certificate.</span></span>

```PowerShell
Uninstall-PswaWebApplication -DeleteTestCertificate
```

### <a name="example-3-example-3-subheading"></a><span data-ttu-id="4d217-194">Příklad 3 {#example-3 .subHeading}</span><span class="sxs-lookup"><span data-stu-id="4d217-194">EXAMPLE 3 {#example-3 .subHeading}</span></span>

<span data-ttu-id="4d217-195">Tento příkaz odinstaluje webové aplikace Windows PowerShell, pokud vlastní web a aplikaci se zadaly během instalace.</span><span class="sxs-lookup"><span data-stu-id="4d217-195">This command uninstalls the Windows PowerShell Web Application when a custom website and application were specified during the install.</span></span>
<span data-ttu-id="4d217-196">Příkaz odebere web s názvem *server* a aplikaci s názvem *TestApplication* a určuje, že testovací certifikáty přidružené aplikace jsou také odstraněny.</span><span class="sxs-lookup"><span data-stu-id="4d217-196">The command removes the website named *MySite* and the application named *TestApplication* and specifies that the test certificates associated with the application are also deleted.</span></span>

```
Uninstall-PswaWebApplication -WebApplicationName TestApplication -WebsiteName MySite -DeleteTestCertificate
```

## <a name="related-topics"></a><span data-ttu-id="4d217-197">Příbuzná témata</span><span class="sxs-lookup"><span data-stu-id="4d217-197">Related topics</span></span>

- [<span data-ttu-id="4d217-198">Add-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="4d217-198">Add-PswaAuthorizationRule</span></span>](add-pswaauthorizationrule.md)
- [<span data-ttu-id="4d217-199">Get-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="4d217-199">Get-PswaAuthorizationRule</span></span>](get-pswaauthorizationrule.md)
- [<span data-ttu-id="4d217-200">Rutiny Install-PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="4d217-200">Install-PswaWebApplication</span></span>](install-pswawebapplication.md)
- [<span data-ttu-id="4d217-201">Remove-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="4d217-201">Remove-PswaAuthorizationRule</span></span>](remove-pswaauthorizationrule.md)
- [<span data-ttu-id="4d217-202">Test-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="4d217-202">Test-PswaAuthorizationRule</span></span>](test-pswaauthorizationrule.md)