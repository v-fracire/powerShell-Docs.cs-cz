---
ms.topic: reference
keywords: rutiny prostředí PowerShell
ms.date: 12/12/2016
title: Install-PswaWebApplication
ms.openlocfilehash: 29e074b75eeb387640831229c63142e6dd5e991a
ms.sourcegitcommit: c3f1a83b59484651119630f3089aa51b6e7d4c3c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/26/2018
ms.locfileid: "39268295"
---
# <a name="install-pswawebapplication"></a><span data-ttu-id="0c8fe-103">Install-PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="0c8fe-103">Install-PswaWebApplication</span></span>

## <a name="synopsis"></a><span data-ttu-id="0c8fe-104">SOUHRN</span><span class="sxs-lookup"><span data-stu-id="0c8fe-104">SYNOPSIS</span></span>

<span data-ttu-id="0c8fe-105">Nakonfiguruje Windows PowerShell Web Accessu webové aplikace ve službě IIS.</span><span class="sxs-lookup"><span data-stu-id="0c8fe-105">Configures the Windows PowerShell Web Access web application in IIS.</span></span>

## <a name="syntax"></a><span data-ttu-id="0c8fe-106">SYNTAXE</span><span class="sxs-lookup"><span data-stu-id="0c8fe-106">SYNTAX</span></span>

### <a name="default"></a><span data-ttu-id="0c8fe-107">Výchozí</span><span class="sxs-lookup"><span data-stu-id="0c8fe-107">Default</span></span>
```
Install-PswaWebApplication [[-WebApplicationName] <String> ] [-UseTestCertificate] [-WebSiteName <String> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```

## <a name="description"></a><span data-ttu-id="0c8fe-108">POPIS</span><span class="sxs-lookup"><span data-stu-id="0c8fe-108">DESCRIPTION</span></span>

<span data-ttu-id="0c8fe-109">**Rutiny Install-PswaWebApplication** rutina nakonfiguruje webové aplikace Windows PowerShell Web Accessu.</span><span class="sxs-lookup"><span data-stu-id="0c8fe-109">The **Install-PswaWebApplication** cmdlet configures Windows PowerShell Web Access web application.</span></span>
<span data-ttu-id="0c8fe-110">Tato rutina nainstaluje webovou aplikaci, přidruží ji k webu a volitelně vytváří certifikát SSL test pomocí **useTestCertificate** parametru.</span><span class="sxs-lookup"><span data-stu-id="0c8fe-110">This cmdlet installs the web application, associates it with a web site, and optionally creates a test SSL certificate using the **useTestCertificate** parameter.</span></span> <span data-ttu-id="0c8fe-111">Pro zabezpečení správcům webových důvodů nepoužívejte testovací certifikát pro produkční prostředí.</span><span class="sxs-lookup"><span data-stu-id="0c8fe-111">For security reasons web administrators should not use a test certificate for production environments.</span></span>

## <a name="parameters"></a><span data-ttu-id="0c8fe-112">PARAMETRY</span><span class="sxs-lookup"><span data-stu-id="0c8fe-112">PARAMETERS</span></span>

### <a name="-usetestcertificate"></a><span data-ttu-id="0c8fe-113">-UseTestCertificate</span><span class="sxs-lookup"><span data-stu-id="0c8fe-113">-UseTestCertificate</span></span>

<span data-ttu-id="0c8fe-114">Určuje, že se vytvoří testovací certifikát.</span><span class="sxs-lookup"><span data-stu-id="0c8fe-114">Specifies that a test certificate is created.</span></span> <span data-ttu-id="0c8fe-115">Pokud tento parametr je nastaven na hodnotu true, pak tato rutina vytvoří testovací certifikát a nakonfiguruje webovou aplikaci Windows PowerShell Web Access k použití certifikátu pro požadavky HTTPS.</span><span class="sxs-lookup"><span data-stu-id="0c8fe-115">If this parameter is set to true, then this cmdlet creates a test certificate and configures the Windows PowerShell Web Access web application to use the certificate for HTTPS requests.</span></span> <span data-ttu-id="0c8fe-116">Pokud tento parametr je nastaven na hodnotu false, pak je vytvořen žádný certifikát nebo vazby.</span><span class="sxs-lookup"><span data-stu-id="0c8fe-116">If this parameter is set to false, then no certificate or binding is created.</span></span> <span data-ttu-id="0c8fe-117">Tuto hodnotu nastavte na hodnotu false, pokud jiný certifikát se používá pro Windows PowerShell Web Accessu.</span><span class="sxs-lookup"><span data-stu-id="0c8fe-117">Set this value to false if another certificate is used for Windows PowerShell Web Access.</span></span>

|||
|-|-|
| <span data-ttu-id="0c8fe-118">Aliasy</span><span class="sxs-lookup"><span data-stu-id="0c8fe-118">Aliases</span></span>                              | <span data-ttu-id="0c8fe-119">žádný</span><span class="sxs-lookup"><span data-stu-id="0c8fe-119">none</span></span>                                 |
| <span data-ttu-id="0c8fe-120">Povinné?</span><span class="sxs-lookup"><span data-stu-id="0c8fe-120">Required?</span></span>                            | <span data-ttu-id="0c8fe-121">false</span><span class="sxs-lookup"><span data-stu-id="0c8fe-121">false</span></span>                                |
| <span data-ttu-id="0c8fe-122">Pozice?</span><span class="sxs-lookup"><span data-stu-id="0c8fe-122">Position?</span></span>                            | <span data-ttu-id="0c8fe-123">s názvem</span><span class="sxs-lookup"><span data-stu-id="0c8fe-123">named</span></span>                                |
| <span data-ttu-id="0c8fe-124">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="0c8fe-124">Default Value</span></span>                        | <span data-ttu-id="0c8fe-125">Hodnota TRUE</span><span class="sxs-lookup"><span data-stu-id="0c8fe-125">true</span></span>                                 |
| <span data-ttu-id="0c8fe-126">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="0c8fe-126">Accept Pipeline Input?</span></span>               | <span data-ttu-id="0c8fe-127">false</span><span class="sxs-lookup"><span data-stu-id="0c8fe-127">false</span></span>                                |
| <span data-ttu-id="0c8fe-128">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="0c8fe-128">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="0c8fe-129">false</span><span class="sxs-lookup"><span data-stu-id="0c8fe-129">false</span></span>                                |

### <a name="-webapplicationname"></a><span data-ttu-id="0c8fe-130">-WebApplicationName</span><span class="sxs-lookup"><span data-stu-id="0c8fe-130">-WebApplicationName</span></span>

<span data-ttu-id="0c8fe-131">Určuje název pro vaši webovou aplikaci.</span><span class="sxs-lookup"><span data-stu-id="0c8fe-131">Specifies the name for your web application.</span></span> <span data-ttu-id="0c8fe-132">Zobrazí se jako poslední část Windows PowerShell Web Access URL.</span><span class="sxs-lookup"><span data-stu-id="0c8fe-132">This is displayed as the last part of the Windows PowerShell Web Access URL.</span></span>

|||
|-|-|
| <span data-ttu-id="0c8fe-133">Aliasy</span><span class="sxs-lookup"><span data-stu-id="0c8fe-133">Aliases</span></span>                              | <span data-ttu-id="0c8fe-134">žádný</span><span class="sxs-lookup"><span data-stu-id="0c8fe-134">none</span></span>                                 |
| <span data-ttu-id="0c8fe-135">Povinné?</span><span class="sxs-lookup"><span data-stu-id="0c8fe-135">Required?</span></span>                            | <span data-ttu-id="0c8fe-136">false</span><span class="sxs-lookup"><span data-stu-id="0c8fe-136">false</span></span>                                |
| <span data-ttu-id="0c8fe-137">Pozice?</span><span class="sxs-lookup"><span data-stu-id="0c8fe-137">Position?</span></span>                            | <span data-ttu-id="0c8fe-138">1</span><span class="sxs-lookup"><span data-stu-id="0c8fe-138">1</span></span>                                    |
| <span data-ttu-id="0c8fe-139">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="0c8fe-139">Default Value</span></span>                        | <span data-ttu-id="0c8fe-140">pswa</span><span class="sxs-lookup"><span data-stu-id="0c8fe-140">pswa</span></span>                                 |
| <span data-ttu-id="0c8fe-141">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="0c8fe-141">Accept Pipeline Input?</span></span>               | <span data-ttu-id="0c8fe-142">false</span><span class="sxs-lookup"><span data-stu-id="0c8fe-142">false</span></span>                                |
| <span data-ttu-id="0c8fe-143">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="0c8fe-143">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="0c8fe-144">false</span><span class="sxs-lookup"><span data-stu-id="0c8fe-144">false</span></span>                                |

### <a name="-websitename"></a><span data-ttu-id="0c8fe-145">-Zadaným hodnotám WebSiteName</span><span class="sxs-lookup"><span data-stu-id="0c8fe-145">-WebSiteName</span></span>

<span data-ttu-id="0c8fe-146">Určuje název webového serveru (IIS) webu, na které chcete nainstalovat tuto webovou aplikaci Windows PowerShell Web Accessu.</span><span class="sxs-lookup"><span data-stu-id="0c8fe-146">Specifies the name of the Web Server (IIS) website on which to install this Windows PowerShell Web Access web application.</span></span>

|||
|-|-|
| <span data-ttu-id="0c8fe-147">Aliasy</span><span class="sxs-lookup"><span data-stu-id="0c8fe-147">Aliases</span></span>                              | <span data-ttu-id="0c8fe-148">žádný</span><span class="sxs-lookup"><span data-stu-id="0c8fe-148">none</span></span>                                 |
| <span data-ttu-id="0c8fe-149">Povinné?</span><span class="sxs-lookup"><span data-stu-id="0c8fe-149">Required?</span></span>                            | <span data-ttu-id="0c8fe-150">false</span><span class="sxs-lookup"><span data-stu-id="0c8fe-150">false</span></span>                                |
| <span data-ttu-id="0c8fe-151">Pozice?</span><span class="sxs-lookup"><span data-stu-id="0c8fe-151">Position?</span></span>                            | <span data-ttu-id="0c8fe-152">s názvem</span><span class="sxs-lookup"><span data-stu-id="0c8fe-152">named</span></span>                                |
| <span data-ttu-id="0c8fe-153">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="0c8fe-153">Default Value</span></span>                        | <span data-ttu-id="0c8fe-154">Výchozí web</span><span class="sxs-lookup"><span data-stu-id="0c8fe-154">Default Web Site</span></span>                     |
| <span data-ttu-id="0c8fe-155">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="0c8fe-155">Accept Pipeline Input?</span></span>               | <span data-ttu-id="0c8fe-156">false</span><span class="sxs-lookup"><span data-stu-id="0c8fe-156">false</span></span>                                |
| <span data-ttu-id="0c8fe-157">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="0c8fe-157">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="0c8fe-158">false</span><span class="sxs-lookup"><span data-stu-id="0c8fe-158">false</span></span>                                |

### <a name="-confirm"></a><span data-ttu-id="0c8fe-159">-Confirm</span><span class="sxs-lookup"><span data-stu-id="0c8fe-159">-Confirm</span></span>

<span data-ttu-id="0c8fe-160">Před spuštěním rutiny zobrazí výzvu k potvrzení.</span><span class="sxs-lookup"><span data-stu-id="0c8fe-160">Prompts you for confirmation before running the cmdlet.</span></span>

|||
|-|-|
| <span data-ttu-id="0c8fe-161">Povinné?</span><span class="sxs-lookup"><span data-stu-id="0c8fe-161">Required?</span></span>                            | <span data-ttu-id="0c8fe-162">false</span><span class="sxs-lookup"><span data-stu-id="0c8fe-162">false</span></span>                                |
| <span data-ttu-id="0c8fe-163">Pozice?</span><span class="sxs-lookup"><span data-stu-id="0c8fe-163">Position?</span></span>                            | <span data-ttu-id="0c8fe-164">s názvem</span><span class="sxs-lookup"><span data-stu-id="0c8fe-164">named</span></span>                                |
| <span data-ttu-id="0c8fe-165">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="0c8fe-165">Default Value</span></span>                        | <span data-ttu-id="0c8fe-166">false</span><span class="sxs-lookup"><span data-stu-id="0c8fe-166">false</span></span>                                |
| <span data-ttu-id="0c8fe-167">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="0c8fe-167">Accept Pipeline Input?</span></span>               | <span data-ttu-id="0c8fe-168">false</span><span class="sxs-lookup"><span data-stu-id="0c8fe-168">false</span></span>                                |
| <span data-ttu-id="0c8fe-169">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="0c8fe-169">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="0c8fe-170">false</span><span class="sxs-lookup"><span data-stu-id="0c8fe-170">false</span></span>                                |

### <a name="-whatif"></a><span data-ttu-id="0c8fe-171">-WhatIf</span><span class="sxs-lookup"><span data-stu-id="0c8fe-171">-WhatIf</span></span>

<span data-ttu-id="0c8fe-172">Zobrazuje, co by se stalo při spuštění rutiny.</span><span class="sxs-lookup"><span data-stu-id="0c8fe-172">Shows what would happen if the cmdlet runs.</span></span>
<span data-ttu-id="0c8fe-173">Rutina není spuštěna.</span><span class="sxs-lookup"><span data-stu-id="0c8fe-173">The cmdlet is not run.</span></span>

|||
|-|-|
| <span data-ttu-id="0c8fe-174">Povinné?</span><span class="sxs-lookup"><span data-stu-id="0c8fe-174">Required?</span></span>                            | <span data-ttu-id="0c8fe-175">false</span><span class="sxs-lookup"><span data-stu-id="0c8fe-175">false</span></span>                                |
| <span data-ttu-id="0c8fe-176">Pozice?</span><span class="sxs-lookup"><span data-stu-id="0c8fe-176">Position?</span></span>                            | <span data-ttu-id="0c8fe-177">s názvem</span><span class="sxs-lookup"><span data-stu-id="0c8fe-177">named</span></span>                                |
| <span data-ttu-id="0c8fe-178">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="0c8fe-178">Default Value</span></span>                        | <span data-ttu-id="0c8fe-179">false</span><span class="sxs-lookup"><span data-stu-id="0c8fe-179">false</span></span>                                |
| <span data-ttu-id="0c8fe-180">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="0c8fe-180">Accept Pipeline Input?</span></span>               | <span data-ttu-id="0c8fe-181">false</span><span class="sxs-lookup"><span data-stu-id="0c8fe-181">false</span></span>                                |
| <span data-ttu-id="0c8fe-182">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="0c8fe-182">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="0c8fe-183">false</span><span class="sxs-lookup"><span data-stu-id="0c8fe-183">false</span></span>                                |

### <a name="ltcommonparametersgt"></a><span data-ttu-id="0c8fe-184">&lt;CommonParameters&gt;</span><span class="sxs-lookup"><span data-stu-id="0c8fe-184">&lt;CommonParameters&gt;</span></span>

<span data-ttu-id="0c8fe-185">Tato rutina podporuje běžné parametry:-Verbose,-Debug, - ErrorAction, - ErrorVariable,-OutBuffer a - OutVariable.</span><span class="sxs-lookup"><span data-stu-id="0c8fe-185">This cmdlet supports the common parameters: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer, and -OutVariable.</span></span> <span data-ttu-id="0c8fe-186">Další informace najdete v tématu [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span><span class="sxs-lookup"><span data-stu-id="0c8fe-186">For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span></span>

## <a name="inputs"></a><span data-ttu-id="0c8fe-187">VSTUPY</span><span class="sxs-lookup"><span data-stu-id="0c8fe-187">INPUTS</span></span>

<span data-ttu-id="0c8fe-188">Tato rutina nemá žádný vstup.</span><span class="sxs-lookup"><span data-stu-id="0c8fe-188">This cmdlet takes no input.</span></span>

## <a name="outputs"></a><span data-ttu-id="0c8fe-189">VÝSTUPY</span><span class="sxs-lookup"><span data-stu-id="0c8fe-189">OUTPUTS</span></span>

<span data-ttu-id="0c8fe-190">Tato rutina negeneruje žádný výstup.</span><span class="sxs-lookup"><span data-stu-id="0c8fe-190">This cmdlet produces no output.</span></span>

## <a name="examples"></a><span data-ttu-id="0c8fe-191">PŘÍKLADY</span><span class="sxs-lookup"><span data-stu-id="0c8fe-191">EXAMPLES</span></span>

### <a name="example-1"></a><span data-ttu-id="0c8fe-192">PŘÍKLAD 1</span><span class="sxs-lookup"><span data-stu-id="0c8fe-192">EXAMPLE 1</span></span>

<span data-ttu-id="0c8fe-193">Tento příklad nainstaluje PSWA webovou aplikaci pomocí výchozích hodnot pro **WebApplicationName** (*pswa*) a **zadaným hodnotám WebSiteName** (*výchozí webový server* ) parametry.</span><span class="sxs-lookup"><span data-stu-id="0c8fe-193">This example installs the PSWA web application using the default values for the **WebApplicationName** (*pswa*) and **WebSiteName** (*Default Web Site*) parameters .</span></span>

```
Install-PswaWebApplication
```

### <a name="example-2"></a><span data-ttu-id="0c8fe-194">PŘÍKLAD 2</span><span class="sxs-lookup"><span data-stu-id="0c8fe-194">EXAMPLE 2</span></span>

<span data-ttu-id="0c8fe-195">Tento příklad nainstaluje webovou aplikaci PSWA testovací certifikát a pomocí výchozích hodnot pro **WebApplicationName** a **zadaným hodnotám WebSiteName** parametry.</span><span class="sxs-lookup"><span data-stu-id="0c8fe-195">This example installs the PSWA web application with a test certificate, and using the default values for the **WebApplicationName** and **WebSiteName** parameters.</span></span>

```
Install-PswaWebApplication -UseTestCertificate
```

## <a name="related-topics"></a><span data-ttu-id="0c8fe-196">Příbuzná témata</span><span class="sxs-lookup"><span data-stu-id="0c8fe-196">Related topics</span></span>

- [<span data-ttu-id="0c8fe-197">Add-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="0c8fe-197">Add-PswaAuthorizationRule</span></span>](add-pswaauthorizationrule.md)
- [<span data-ttu-id="0c8fe-198">Get-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="0c8fe-198">Get-PswaAuthorizationRule</span></span>](get-pswaauthorizationrule.md)
- [<span data-ttu-id="0c8fe-199">Remove-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="0c8fe-199">Remove-PswaAuthorizationRule</span></span>](remove-pswaauthorizationrule.md)
- [<span data-ttu-id="0c8fe-200">Test-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="0c8fe-200">Test-PswaAuthorizationRule</span></span>](test-pswaauthorizationrule.md)