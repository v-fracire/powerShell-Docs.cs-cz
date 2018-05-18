---
ms.topic: reference
keywords: rutiny prostředí PowerShell
ms.date: 12/12/2016
title: Install-PswaWebApplication
ms.openlocfilehash: 68455d9490f7d5c33c1a928ac262a76a78ad7128
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
---
# <a name="install-pswawebapplication"></a><span data-ttu-id="3091e-103">Install-PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="3091e-103">Install-PswaWebApplication</span></span>

## <a name="synopsis"></a><span data-ttu-id="3091e-104">STRUČNÝ OBSAH</span><span class="sxs-lookup"><span data-stu-id="3091e-104">SYNOPSIS</span></span>

<span data-ttu-id="3091e-105">Nakonfiguruje Windows PowerShell® Web Access webové aplikace ve službě IIS.</span><span class="sxs-lookup"><span data-stu-id="3091e-105">Configures the Windows PowerShell® Web Access web application in IIS.</span></span>

## <a name="syntax"></a><span data-ttu-id="3091e-106">SYNTAXE</span><span class="sxs-lookup"><span data-stu-id="3091e-106">SYNTAX</span></span>

### <a name="default"></a><span data-ttu-id="3091e-107">Výchozí</span><span class="sxs-lookup"><span data-stu-id="3091e-107">Default</span></span>
```
Install-PswaWebApplication [[-WebApplicationName] <String> ] [-UseTestCertificate] [-WebSiteName <String> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

## <a name="description"></a><span data-ttu-id="3091e-108">POPIS</span><span class="sxs-lookup"><span data-stu-id="3091e-108">DESCRIPTION</span></span>

<span data-ttu-id="3091e-109">**Rutiny Install-PswaWebApplication** rutiny se konfiguruje Windows PowerShell Web Access webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="3091e-109">The **Install-PswaWebApplication** cmdlet configures Windows PowerShell Web Access web application.</span></span> <span data-ttu-id="3091e-110">Tato rutina nainstaluje webovou aplikaci, přidruží ji k webovému serveru a volitelně vytváří pomocí certifikátu testovací SSL **useTestCertificate** parametr.</span><span class="sxs-lookup"><span data-stu-id="3091e-110">This cmdlet installs the web application, associates it with a web site, and optionally creates a test SSL certificate using the **useTestCertificate** parameter.</span></span> <span data-ttu-id="3091e-111">Pro zabezpečení Správci webové důvodů neměli používat testovací certifikát pro produkční prostředí.</span><span class="sxs-lookup"><span data-stu-id="3091e-111">For security reasons web administrators should not use a test certificate for production environments.</span></span>

## <a name="parameters"></a><span data-ttu-id="3091e-112">PARAMETRY</span><span class="sxs-lookup"><span data-stu-id="3091e-112">PARAMETERS</span></span>

### <a name="-usetestcertificate"></a><span data-ttu-id="3091e-113">-UseTestCertificate</span><span class="sxs-lookup"><span data-stu-id="3091e-113">-UseTestCertificate</span></span>

<span data-ttu-id="3091e-114">Určuje, jestli je vytvořená testovací certifikát.</span><span class="sxs-lookup"><span data-stu-id="3091e-114">Specifies that a test certificate is created.</span></span> <span data-ttu-id="3091e-115">Pokud tento parametr je nastaven na hodnotu true, pak tato rutina vytvoří testovací certifikát a nakonfiguruje webové aplikace Windows PowerShell Web Access k použití certifikátu pro požadavky HTTPS.</span><span class="sxs-lookup"><span data-stu-id="3091e-115">If this parameter is set to true, then this cmdlet creates a test certificate and configures the Windows PowerShell Web Access web application to use the certificate for HTTPS requests.</span></span> <span data-ttu-id="3091e-116">Pokud tento parametr je nastaven na hodnotu false, pak je vytvořen žádný certifikát nebo vazby.</span><span class="sxs-lookup"><span data-stu-id="3091e-116">If this parameter is set to false, then no certificate or binding is created.</span></span> <span data-ttu-id="3091e-117">Tuto hodnotu nastavte na hodnotu false, pokud se používá jiný certifikát pro Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="3091e-117">Set this value to false if another certificate is used for Windows PowerShell Web Access.</span></span>

|||
|-|-|
| <span data-ttu-id="3091e-118">Aliasy</span><span class="sxs-lookup"><span data-stu-id="3091e-118">Aliases</span></span>                              | <span data-ttu-id="3091e-119">žádný</span><span class="sxs-lookup"><span data-stu-id="3091e-119">none</span></span>                                 |
| <span data-ttu-id="3091e-120">Povinné?</span><span class="sxs-lookup"><span data-stu-id="3091e-120">Required?</span></span>                            | <span data-ttu-id="3091e-121">false</span><span class="sxs-lookup"><span data-stu-id="3091e-121">false</span></span>                                |
| <span data-ttu-id="3091e-122">Pozice?</span><span class="sxs-lookup"><span data-stu-id="3091e-122">Position?</span></span>                            | <span data-ttu-id="3091e-123">S názvem</span><span class="sxs-lookup"><span data-stu-id="3091e-123">named</span></span>                                |
| <span data-ttu-id="3091e-124">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="3091e-124">Default Value</span></span>                        | <span data-ttu-id="3091e-125">Hodnota TRUE</span><span class="sxs-lookup"><span data-stu-id="3091e-125">true</span></span>                                 |
| <span data-ttu-id="3091e-126">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="3091e-126">Accept Pipeline Input?</span></span>               | <span data-ttu-id="3091e-127">false</span><span class="sxs-lookup"><span data-stu-id="3091e-127">false</span></span>                                |
| <span data-ttu-id="3091e-128">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="3091e-128">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="3091e-129">false</span><span class="sxs-lookup"><span data-stu-id="3091e-129">false</span></span>                                |

### <a name="-webapplicationnameltstringgt"></a><span data-ttu-id="3091e-130">-WebApplicationName&lt;řetězec&gt;</span><span class="sxs-lookup"><span data-stu-id="3091e-130">-WebApplicationName&lt;String&gt;</span></span>

<span data-ttu-id="3091e-131">Určuje název webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="3091e-131">Specifies the name for your web application.</span></span> <span data-ttu-id="3091e-132">Zobrazuje se jako poslední část Windows PowerShell Web Access URL.</span><span class="sxs-lookup"><span data-stu-id="3091e-132">This is displayed as the last part of the Windows PowerShell Web Access URL.</span></span>

|||
|-|-|
| <span data-ttu-id="3091e-133">Aliasy</span><span class="sxs-lookup"><span data-stu-id="3091e-133">Aliases</span></span>                              | <span data-ttu-id="3091e-134">žádný</span><span class="sxs-lookup"><span data-stu-id="3091e-134">none</span></span>                                 |
| <span data-ttu-id="3091e-135">Povinné?</span><span class="sxs-lookup"><span data-stu-id="3091e-135">Required?</span></span>                            | <span data-ttu-id="3091e-136">false</span><span class="sxs-lookup"><span data-stu-id="3091e-136">false</span></span>                                |
| <span data-ttu-id="3091e-137">Pozice?</span><span class="sxs-lookup"><span data-stu-id="3091e-137">Position?</span></span>                            | <span data-ttu-id="3091e-138">1</span><span class="sxs-lookup"><span data-stu-id="3091e-138">1</span></span>                                    |
| <span data-ttu-id="3091e-139">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="3091e-139">Default Value</span></span>                        | <span data-ttu-id="3091e-140">pswa</span><span class="sxs-lookup"><span data-stu-id="3091e-140">pswa</span></span>                                 |
| <span data-ttu-id="3091e-141">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="3091e-141">Accept Pipeline Input?</span></span>               | <span data-ttu-id="3091e-142">false</span><span class="sxs-lookup"><span data-stu-id="3091e-142">false</span></span>                                |
| <span data-ttu-id="3091e-143">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="3091e-143">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="3091e-144">false</span><span class="sxs-lookup"><span data-stu-id="3091e-144">false</span></span>                                |

### <a name="-websitenameltstringgt"></a><span data-ttu-id="3091e-145">-Zadaným hodnotám WebSiteName&lt;řetězec&gt;</span><span class="sxs-lookup"><span data-stu-id="3091e-145">-WebSiteName&lt;String&gt;</span></span>

<span data-ttu-id="3091e-146">Určuje název webového serveru (IIS) webu, na který chcete nainstalovat tuto webovou aplikaci Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="3091e-146">Specifies the name of the Web Server (IIS) website on which to install this Windows PowerShell Web Access web application.</span></span>

|||
|-|-|
| <span data-ttu-id="3091e-147">Aliasy</span><span class="sxs-lookup"><span data-stu-id="3091e-147">Aliases</span></span>                              | <span data-ttu-id="3091e-148">žádný</span><span class="sxs-lookup"><span data-stu-id="3091e-148">none</span></span>                                 |
| <span data-ttu-id="3091e-149">Povinné?</span><span class="sxs-lookup"><span data-stu-id="3091e-149">Required?</span></span>                            | <span data-ttu-id="3091e-150">false</span><span class="sxs-lookup"><span data-stu-id="3091e-150">false</span></span>                                |
| <span data-ttu-id="3091e-151">Pozice?</span><span class="sxs-lookup"><span data-stu-id="3091e-151">Position?</span></span>                            | <span data-ttu-id="3091e-152">S názvem</span><span class="sxs-lookup"><span data-stu-id="3091e-152">named</span></span>                                |
| <span data-ttu-id="3091e-153">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="3091e-153">Default Value</span></span>                        | <span data-ttu-id="3091e-154">Výchozí web</span><span class="sxs-lookup"><span data-stu-id="3091e-154">Default Web Site</span></span>                     |
| <span data-ttu-id="3091e-155">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="3091e-155">Accept Pipeline Input?</span></span>               | <span data-ttu-id="3091e-156">false</span><span class="sxs-lookup"><span data-stu-id="3091e-156">false</span></span>                                |
| <span data-ttu-id="3091e-157">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="3091e-157">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="3091e-158">false</span><span class="sxs-lookup"><span data-stu-id="3091e-158">false</span></span>                                |

### <a name="-confirm"></a><span data-ttu-id="3091e-159">-Confirm</span><span class="sxs-lookup"><span data-stu-id="3091e-159">-Confirm</span></span>

<span data-ttu-id="3091e-160">Před spuštěním rutiny zobrazí výzvu k potvrzení.</span><span class="sxs-lookup"><span data-stu-id="3091e-160">Prompts you for confirmation before running the cmdlet.</span></span>

|||
|-|-|
| <span data-ttu-id="3091e-161">Povinné?</span><span class="sxs-lookup"><span data-stu-id="3091e-161">Required?</span></span>                            | <span data-ttu-id="3091e-162">false</span><span class="sxs-lookup"><span data-stu-id="3091e-162">false</span></span>                                |
| <span data-ttu-id="3091e-163">Pozice?</span><span class="sxs-lookup"><span data-stu-id="3091e-163">Position?</span></span>                            | <span data-ttu-id="3091e-164">S názvem</span><span class="sxs-lookup"><span data-stu-id="3091e-164">named</span></span>                                |
| <span data-ttu-id="3091e-165">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="3091e-165">Default Value</span></span>                        | <span data-ttu-id="3091e-166">false</span><span class="sxs-lookup"><span data-stu-id="3091e-166">false</span></span>                                |
| <span data-ttu-id="3091e-167">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="3091e-167">Accept Pipeline Input?</span></span>               | <span data-ttu-id="3091e-168">false</span><span class="sxs-lookup"><span data-stu-id="3091e-168">false</span></span>                                |
| <span data-ttu-id="3091e-169">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="3091e-169">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="3091e-170">false</span><span class="sxs-lookup"><span data-stu-id="3091e-170">false</span></span>                                |

### <a name="-whatif"></a><span data-ttu-id="3091e-171">-WhatIf</span><span class="sxs-lookup"><span data-stu-id="3091e-171">-WhatIf</span></span>

<span data-ttu-id="3091e-172">Zobrazuje, co by se stalo při spuštění rutiny.</span><span class="sxs-lookup"><span data-stu-id="3091e-172">Shows what would happen if the cmdlet runs.</span></span>
<span data-ttu-id="3091e-173">Rutina není spuštěna.</span><span class="sxs-lookup"><span data-stu-id="3091e-173">The cmdlet is not run.</span></span>

|||
|-|-|
| <span data-ttu-id="3091e-174">Povinné?</span><span class="sxs-lookup"><span data-stu-id="3091e-174">Required?</span></span>                            | <span data-ttu-id="3091e-175">false</span><span class="sxs-lookup"><span data-stu-id="3091e-175">false</span></span>                                |
| <span data-ttu-id="3091e-176">Pozice?</span><span class="sxs-lookup"><span data-stu-id="3091e-176">Position?</span></span>                            | <span data-ttu-id="3091e-177">S názvem</span><span class="sxs-lookup"><span data-stu-id="3091e-177">named</span></span>                                |
| <span data-ttu-id="3091e-178">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="3091e-178">Default Value</span></span>                        | <span data-ttu-id="3091e-179">false</span><span class="sxs-lookup"><span data-stu-id="3091e-179">false</span></span>                                |
| <span data-ttu-id="3091e-180">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="3091e-180">Accept Pipeline Input?</span></span>               | <span data-ttu-id="3091e-181">false</span><span class="sxs-lookup"><span data-stu-id="3091e-181">false</span></span>                                |
| <span data-ttu-id="3091e-182">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="3091e-182">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="3091e-183">false</span><span class="sxs-lookup"><span data-stu-id="3091e-183">false</span></span>                                |

### <a name="ltcommonparametersgt"></a><span data-ttu-id="3091e-184">&lt;CommonParameters&gt;</span><span class="sxs-lookup"><span data-stu-id="3091e-184">&lt;CommonParameters&gt;</span></span>

<span data-ttu-id="3091e-185">Tato rutina podporuje běžné parametry:-Verbose,-Debug, - ErrorAction, - ErrorVariable,-OutBuffer a - OutVariable.</span><span class="sxs-lookup"><span data-stu-id="3091e-185">This cmdlet supports the common parameters: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer, and -OutVariable.</span></span>
<span data-ttu-id="3091e-186">Další informace najdete v tématu [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span><span class="sxs-lookup"><span data-stu-id="3091e-186">For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span></span>

## <a name="inputs"></a><span data-ttu-id="3091e-187">VSTUPY</span><span class="sxs-lookup"><span data-stu-id="3091e-187">INPUTS</span></span>

<span data-ttu-id="3091e-188">Tato rutina nemá žádný vstup.</span><span class="sxs-lookup"><span data-stu-id="3091e-188">This cmdlet takes no input.</span></span>

## <a name="outputs"></a><span data-ttu-id="3091e-189">VÝSTUPY</span><span class="sxs-lookup"><span data-stu-id="3091e-189">OUTPUTS</span></span>

<span data-ttu-id="3091e-190">Tato rutina neprodukuje žádný výstup.</span><span class="sxs-lookup"><span data-stu-id="3091e-190">This cmdlet produces no output.</span></span>

## <a name="examples"></a><span data-ttu-id="3091e-191">PŘÍKLADY</span><span class="sxs-lookup"><span data-stu-id="3091e-191">EXAMPLES</span></span>

### <a name="example-1"></a><span data-ttu-id="3091e-192">PŘÍKLAD 1</span><span class="sxs-lookup"><span data-stu-id="3091e-192">EXAMPLE 1</span></span>

<span data-ttu-id="3091e-193">Tento příklad nainstaluje pomocí výchozí hodnoty pro webové aplikace PSWA **WebApplicationName** (*pswa*) a **zadaným hodnotám WebSiteName** (*výchozí web* ) parametry.</span><span class="sxs-lookup"><span data-stu-id="3091e-193">This example installs the PSWA web application using the default values for the **WebApplicationName** (*pswa*) and **WebSiteName** (*Default Web Site*) parameters .</span></span>

```
Install-PswaWebApplication
```

### <a name="example-2"></a><span data-ttu-id="3091e-194">PŘÍKLAD 2</span><span class="sxs-lookup"><span data-stu-id="3091e-194">EXAMPLE 2</span></span>

<span data-ttu-id="3091e-195">Tento příklad nainstaluje s testovací certifikát a pomocí výchozí hodnoty pro webové aplikace PSWA **WebApplicationName** a **zadaným hodnotám WebSiteName** parametry.</span><span class="sxs-lookup"><span data-stu-id="3091e-195">This example installs the PSWA web application with a test certificate, and using the default values for the **WebApplicationName** and **WebSiteName** parameters.</span></span>

```
Install-PswaWebApplication -UseTestCertificate
```

## <a name="related-topics"></a><span data-ttu-id="3091e-196">Příbuzná témata</span><span class="sxs-lookup"><span data-stu-id="3091e-196">Related topics</span></span>

- [<span data-ttu-id="3091e-197">Add-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="3091e-197">Add-PswaAuthorizationRule</span></span>](add-pswaauthorizationrule.md)
- [<span data-ttu-id="3091e-198">Get-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="3091e-198">Get-PswaAuthorizationRule</span></span>](get-pswaauthorizationrule.md)
- [<span data-ttu-id="3091e-199">Remove-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="3091e-199">Remove-PswaAuthorizationRule</span></span>](remove-pswaauthorizationrule.md)
- [<span data-ttu-id="3091e-200">Test-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="3091e-200">Test-PswaAuthorizationRule</span></span>](test-pswaauthorizationrule.md)