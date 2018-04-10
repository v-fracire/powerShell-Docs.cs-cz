---
description: ''
ms.topic: article
ms.prod: powershell
keywords: rutiny prostředí PowerShell
ms.date: 12/12/2016
title: Nainstalujte pswawebapplication
ms.technology: powershell
ms.openlocfilehash: c7f7768a41b6784d8c29afa1fccf0b855160b777
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="install-pswawebapplication"></a><span data-ttu-id="66101-103">Install-PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="66101-103">Install-PswaWebApplication</span></span>

## <a name="synopsis"></a><span data-ttu-id="66101-104">STRUČNÝ OBSAH</span><span class="sxs-lookup"><span data-stu-id="66101-104">SYNOPSIS</span></span>

<span data-ttu-id="66101-105">Nakonfiguruje Windows PowerShell® Web Access webové aplikace ve službě IIS.</span><span class="sxs-lookup"><span data-stu-id="66101-105">Configures the Windows PowerShell® Web Access web application in IIS.</span></span>

## <a name="syntax"></a><span data-ttu-id="66101-106">SYNTAX</span><span class="sxs-lookup"><span data-stu-id="66101-106">SYNTAX</span></span>

### <a name="default"></a><span data-ttu-id="66101-107">Výchozí</span><span class="sxs-lookup"><span data-stu-id="66101-107">Default</span></span>
```
Install-PswaWebApplication [[-WebApplicationName] <String> ] [-UseTestCertificate] [-WebSiteName <String> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

## <a name="description"></a><span data-ttu-id="66101-108">POPIS</span><span class="sxs-lookup"><span data-stu-id="66101-108">DESCRIPTION</span></span>

<span data-ttu-id="66101-109">**Rutiny Install-PswaWebApplication** rutiny se konfiguruje Windows PowerShell Web Access webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="66101-109">The **Install-PswaWebApplication** cmdlet configures Windows PowerShell Web Access web application.</span></span> <span data-ttu-id="66101-110">Tato rutina nainstaluje webovou aplikaci, přidruží ji k webovému serveru a volitelně vytváří pomocí certifikátu testovací SSL **useTestCertificate** parametr.</span><span class="sxs-lookup"><span data-stu-id="66101-110">This cmdlet installs the web application, associates it with a web site, and optionally creates a test SSL certificate using the **useTestCertificate** parameter.</span></span> <span data-ttu-id="66101-111">Pro zabezpečení Správci webové důvodů neměli používat testovací certifikát pro produkční prostředí.</span><span class="sxs-lookup"><span data-stu-id="66101-111">For security reasons web administrators should not use a test certificate for production environments.</span></span>

## <a name="parameters"></a><span data-ttu-id="66101-112">PARAMETRY</span><span class="sxs-lookup"><span data-stu-id="66101-112">PARAMETERS</span></span>

### <a name="-usetestcertificate"></a><span data-ttu-id="66101-113">-UseTestCertificate</span><span class="sxs-lookup"><span data-stu-id="66101-113">-UseTestCertificate</span></span>

<span data-ttu-id="66101-114">Určuje, jestli je vytvořená testovací certifikát.</span><span class="sxs-lookup"><span data-stu-id="66101-114">Specifies that a test certificate is created.</span></span> <span data-ttu-id="66101-115">Pokud tento parametr je nastaven na hodnotu true, pak tato rutina vytvoří testovací certifikát a nakonfiguruje webové aplikace Windows PowerShell Web Access k použití certifikátu pro požadavky HTTPS.</span><span class="sxs-lookup"><span data-stu-id="66101-115">If this parameter is set to true, then this cmdlet creates a test certificate and configures the Windows PowerShell Web Access web application to use the certificate for HTTPS requests.</span></span> <span data-ttu-id="66101-116">Pokud tento parametr je nastaven na hodnotu false, pak je vytvořen žádný certifikát nebo vazby.</span><span class="sxs-lookup"><span data-stu-id="66101-116">If this parameter is set to false, then no certificate or binding is created.</span></span> <span data-ttu-id="66101-117">Tuto hodnotu nastavte na hodnotu false, pokud se používá jiný certifikát pro Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="66101-117">Set this value to false if another certificate is used for Windows PowerShell Web Access.</span></span>

|||
|-|-|
| <span data-ttu-id="66101-118">Aliasy</span><span class="sxs-lookup"><span data-stu-id="66101-118">Aliases</span></span>                              | <span data-ttu-id="66101-119">žádný</span><span class="sxs-lookup"><span data-stu-id="66101-119">none</span></span>                                 |
| <span data-ttu-id="66101-120">Povinné?</span><span class="sxs-lookup"><span data-stu-id="66101-120">Required?</span></span>                            | <span data-ttu-id="66101-121">false</span><span class="sxs-lookup"><span data-stu-id="66101-121">false</span></span>                                |
| <span data-ttu-id="66101-122">Pozice?</span><span class="sxs-lookup"><span data-stu-id="66101-122">Position?</span></span>                            | <span data-ttu-id="66101-123">S názvem</span><span class="sxs-lookup"><span data-stu-id="66101-123">named</span></span>                                |
| <span data-ttu-id="66101-124">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="66101-124">Default Value</span></span>                        | <span data-ttu-id="66101-125">Hodnota TRUE</span><span class="sxs-lookup"><span data-stu-id="66101-125">true</span></span>                                 |
| <span data-ttu-id="66101-126">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="66101-126">Accept Pipeline Input?</span></span>               | <span data-ttu-id="66101-127">false</span><span class="sxs-lookup"><span data-stu-id="66101-127">false</span></span>                                |
| <span data-ttu-id="66101-128">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="66101-128">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="66101-129">false</span><span class="sxs-lookup"><span data-stu-id="66101-129">false</span></span>                                |

### <a name="-webapplicationnameltstringgt"></a><span data-ttu-id="66101-130">-WebApplicationName&lt;String&gt;</span><span class="sxs-lookup"><span data-stu-id="66101-130">-WebApplicationName&lt;String&gt;</span></span>

<span data-ttu-id="66101-131">Určuje název webové aplikace.</span><span class="sxs-lookup"><span data-stu-id="66101-131">Specifies the name for your web application.</span></span> <span data-ttu-id="66101-132">Zobrazuje se jako poslední část Windows PowerShell Web Access URL.</span><span class="sxs-lookup"><span data-stu-id="66101-132">This is displayed as the last part of the Windows PowerShell Web Access URL.</span></span>

|||
|-|-|
| <span data-ttu-id="66101-133">Aliasy</span><span class="sxs-lookup"><span data-stu-id="66101-133">Aliases</span></span>                              | <span data-ttu-id="66101-134">žádný</span><span class="sxs-lookup"><span data-stu-id="66101-134">none</span></span>                                 |
| <span data-ttu-id="66101-135">Povinné?</span><span class="sxs-lookup"><span data-stu-id="66101-135">Required?</span></span>                            | <span data-ttu-id="66101-136">false</span><span class="sxs-lookup"><span data-stu-id="66101-136">false</span></span>                                |
| <span data-ttu-id="66101-137">Pozice?</span><span class="sxs-lookup"><span data-stu-id="66101-137">Position?</span></span>                            | <span data-ttu-id="66101-138">1</span><span class="sxs-lookup"><span data-stu-id="66101-138">1</span></span>                                    |
| <span data-ttu-id="66101-139">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="66101-139">Default Value</span></span>                        | <span data-ttu-id="66101-140">pswa</span><span class="sxs-lookup"><span data-stu-id="66101-140">pswa</span></span>                                 |
| <span data-ttu-id="66101-141">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="66101-141">Accept Pipeline Input?</span></span>               | <span data-ttu-id="66101-142">false</span><span class="sxs-lookup"><span data-stu-id="66101-142">false</span></span>                                |
| <span data-ttu-id="66101-143">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="66101-143">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="66101-144">false</span><span class="sxs-lookup"><span data-stu-id="66101-144">false</span></span>                                |

### <a name="-websitenameltstringgt"></a><span data-ttu-id="66101-145">-WebSiteName&lt;String&gt;</span><span class="sxs-lookup"><span data-stu-id="66101-145">-WebSiteName&lt;String&gt;</span></span>

<span data-ttu-id="66101-146">Určuje název webového serveru (IIS) webu, na který chcete nainstalovat tuto webovou aplikaci Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="66101-146">Specifies the name of the Web Server (IIS) website on which to install this Windows PowerShell Web Access web application.</span></span>

|||
|-|-|
| <span data-ttu-id="66101-147">Aliasy</span><span class="sxs-lookup"><span data-stu-id="66101-147">Aliases</span></span>                              | <span data-ttu-id="66101-148">žádný</span><span class="sxs-lookup"><span data-stu-id="66101-148">none</span></span>                                 |
| <span data-ttu-id="66101-149">Povinné?</span><span class="sxs-lookup"><span data-stu-id="66101-149">Required?</span></span>                            | <span data-ttu-id="66101-150">false</span><span class="sxs-lookup"><span data-stu-id="66101-150">false</span></span>                                |
| <span data-ttu-id="66101-151">Pozice?</span><span class="sxs-lookup"><span data-stu-id="66101-151">Position?</span></span>                            | <span data-ttu-id="66101-152">S názvem</span><span class="sxs-lookup"><span data-stu-id="66101-152">named</span></span>                                |
| <span data-ttu-id="66101-153">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="66101-153">Default Value</span></span>                        | <span data-ttu-id="66101-154">Výchozí web</span><span class="sxs-lookup"><span data-stu-id="66101-154">Default Web Site</span></span>                     |
| <span data-ttu-id="66101-155">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="66101-155">Accept Pipeline Input?</span></span>               | <span data-ttu-id="66101-156">false</span><span class="sxs-lookup"><span data-stu-id="66101-156">false</span></span>                                |
| <span data-ttu-id="66101-157">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="66101-157">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="66101-158">false</span><span class="sxs-lookup"><span data-stu-id="66101-158">false</span></span>                                |

### <a name="-confirm"></a><span data-ttu-id="66101-159">-Confirm</span><span class="sxs-lookup"><span data-stu-id="66101-159">-Confirm</span></span>

<span data-ttu-id="66101-160">Před spuštěním rutiny zobrazí výzvu k potvrzení.</span><span class="sxs-lookup"><span data-stu-id="66101-160">Prompts you for confirmation before running the cmdlet.</span></span>

|||
|-|-|
| <span data-ttu-id="66101-161">Povinné?</span><span class="sxs-lookup"><span data-stu-id="66101-161">Required?</span></span>                            | <span data-ttu-id="66101-162">false</span><span class="sxs-lookup"><span data-stu-id="66101-162">false</span></span>                                |
| <span data-ttu-id="66101-163">Pozice?</span><span class="sxs-lookup"><span data-stu-id="66101-163">Position?</span></span>                            | <span data-ttu-id="66101-164">S názvem</span><span class="sxs-lookup"><span data-stu-id="66101-164">named</span></span>                                |
| <span data-ttu-id="66101-165">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="66101-165">Default Value</span></span>                        | <span data-ttu-id="66101-166">false</span><span class="sxs-lookup"><span data-stu-id="66101-166">false</span></span>                                |
| <span data-ttu-id="66101-167">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="66101-167">Accept Pipeline Input?</span></span>               | <span data-ttu-id="66101-168">false</span><span class="sxs-lookup"><span data-stu-id="66101-168">false</span></span>                                |
| <span data-ttu-id="66101-169">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="66101-169">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="66101-170">false</span><span class="sxs-lookup"><span data-stu-id="66101-170">false</span></span>                                |

### <a name="-whatif"></a><span data-ttu-id="66101-171">-WhatIf</span><span class="sxs-lookup"><span data-stu-id="66101-171">-WhatIf</span></span>

<span data-ttu-id="66101-172">Zobrazuje, co by se stalo při spuštění rutiny.</span><span class="sxs-lookup"><span data-stu-id="66101-172">Shows what would happen if the cmdlet runs.</span></span>
<span data-ttu-id="66101-173">Rutina není spuštěna.</span><span class="sxs-lookup"><span data-stu-id="66101-173">The cmdlet is not run.</span></span>

|||
|-|-|
| <span data-ttu-id="66101-174">Povinné?</span><span class="sxs-lookup"><span data-stu-id="66101-174">Required?</span></span>                            | <span data-ttu-id="66101-175">false</span><span class="sxs-lookup"><span data-stu-id="66101-175">false</span></span>                                |
| <span data-ttu-id="66101-176">Pozice?</span><span class="sxs-lookup"><span data-stu-id="66101-176">Position?</span></span>                            | <span data-ttu-id="66101-177">S názvem</span><span class="sxs-lookup"><span data-stu-id="66101-177">named</span></span>                                |
| <span data-ttu-id="66101-178">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="66101-178">Default Value</span></span>                        | <span data-ttu-id="66101-179">false</span><span class="sxs-lookup"><span data-stu-id="66101-179">false</span></span>                                |
| <span data-ttu-id="66101-180">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="66101-180">Accept Pipeline Input?</span></span>               | <span data-ttu-id="66101-181">false</span><span class="sxs-lookup"><span data-stu-id="66101-181">false</span></span>                                |
| <span data-ttu-id="66101-182">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="66101-182">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="66101-183">false</span><span class="sxs-lookup"><span data-stu-id="66101-183">false</span></span>                                |

### <a name="ltcommonparametersgt"></a><span data-ttu-id="66101-184">&lt;CommonParameters&gt;</span><span class="sxs-lookup"><span data-stu-id="66101-184">&lt;CommonParameters&gt;</span></span>

<span data-ttu-id="66101-185">Tato rutina podporuje běžné parametry:-Verbose,-Debug, - ErrorAction, - ErrorVariable,-OutBuffer a - OutVariable.</span><span class="sxs-lookup"><span data-stu-id="66101-185">This cmdlet supports the common parameters: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer, and -OutVariable.</span></span>
<span data-ttu-id="66101-186">Další informace najdete v tématu [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span><span class="sxs-lookup"><span data-stu-id="66101-186">For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span></span>

## <a name="inputs"></a><span data-ttu-id="66101-187">VSTUPY</span><span class="sxs-lookup"><span data-stu-id="66101-187">INPUTS</span></span>

<span data-ttu-id="66101-188">Tato rutina nemá žádný vstup.</span><span class="sxs-lookup"><span data-stu-id="66101-188">This cmdlet takes no input.</span></span>

## <a name="outputs"></a><span data-ttu-id="66101-189">VÝSTUPY</span><span class="sxs-lookup"><span data-stu-id="66101-189">OUTPUTS</span></span>

<span data-ttu-id="66101-190">Tato rutina neprodukuje žádný výstup.</span><span class="sxs-lookup"><span data-stu-id="66101-190">This cmdlet produces no output.</span></span>

## <a name="examples"></a><span data-ttu-id="66101-191">PŘÍKLADY</span><span class="sxs-lookup"><span data-stu-id="66101-191">EXAMPLES</span></span>

### <a name="example-1"></a><span data-ttu-id="66101-192">PŘÍKLAD 1</span><span class="sxs-lookup"><span data-stu-id="66101-192">EXAMPLE 1</span></span>

<span data-ttu-id="66101-193">Tento příklad nainstaluje pomocí výchozí hodnoty pro webové aplikace PSWA **WebApplicationName** (*pswa*) a **zadaným hodnotám WebSiteName** (*výchozí web* ) parametry.</span><span class="sxs-lookup"><span data-stu-id="66101-193">This example installs the PSWA web application using the default values for the **WebApplicationName** (*pswa*) and **WebSiteName** (*Default Web Site*) parameters .</span></span>

```
Install-PswaWebApplication
```

### <a name="example-2"></a><span data-ttu-id="66101-194">PŘÍKLAD 2</span><span class="sxs-lookup"><span data-stu-id="66101-194">EXAMPLE 2</span></span>

<span data-ttu-id="66101-195">Tento příklad nainstaluje s testovací certifikát a pomocí výchozí hodnoty pro webové aplikace PSWA **WebApplicationName** a **zadaným hodnotám WebSiteName** parametry.</span><span class="sxs-lookup"><span data-stu-id="66101-195">This example installs the PSWA web application with a test certificate, and using the default values for the **WebApplicationName** and **WebSiteName** parameters.</span></span>

```
Install-PswaWebApplication -UseTestCertificate
```

## <a name="related-topics"></a><span data-ttu-id="66101-196">Příbuzná témata</span><span class="sxs-lookup"><span data-stu-id="66101-196">Related topics</span></span>

- [<span data-ttu-id="66101-197">Add-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="66101-197">Add-PswaAuthorizationRule</span></span>](add-pswaauthorizationrule.md)
- [<span data-ttu-id="66101-198">Get-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="66101-198">Get-PswaAuthorizationRule</span></span>](get-pswaauthorizationrule.md)
- [<span data-ttu-id="66101-199">Remove-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="66101-199">Remove-PswaAuthorizationRule</span></span>](remove-pswaauthorizationrule.md)
- [<span data-ttu-id="66101-200">Test-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="66101-200">Test-PswaAuthorizationRule</span></span>](test-pswaauthorizationrule.md)