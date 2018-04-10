---
description: ''
ms.topic: article
ms.prod: powershell
keywords: rutiny prostředí PowerShell
ms.date: 12/12/2016
title: získat pswaauthorizationrule
ms.technology: powershell
ms.openlocfilehash: 74c044c329d8b6a305b86c9056a7041fb5fd046b
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="get-pswaauthorizationrule"></a><span data-ttu-id="dd623-103">Get-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="dd623-103">Get-PswaAuthorizationRule</span></span>

## <a name="synopsis"></a><span data-ttu-id="dd623-104">STRUČNÝ OBSAH</span><span class="sxs-lookup"><span data-stu-id="dd623-104">SYNOPSIS</span></span>

<span data-ttu-id="dd623-105">Vrací sadu autorizačních pravidel Windows PowerShell® Web Access.</span><span class="sxs-lookup"><span data-stu-id="dd623-105">Returns a set of the Windows PowerShell® Web Access authorization rules.</span></span>

## <a name="syntax"></a><span data-ttu-id="dd623-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="dd623-106">Syntax</span></span>

### <a name="id"></a><span data-ttu-id="dd623-107">ID</span><span class="sxs-lookup"><span data-stu-id="dd623-107">ID</span></span>
```
Get-PswaAuthorizationRule [[-Id] <Int32[]> ] [ <CommonParameters>]
```

### <a name="name"></a><span data-ttu-id="dd623-108">Název</span><span class="sxs-lookup"><span data-stu-id="dd623-108">Name</span></span>
```
Get-PswaAuthorizationRule [-RuleName] <String[]> [ <CommonParameters>]
```

## <a name="description"></a><span data-ttu-id="dd623-109">POPIS</span><span class="sxs-lookup"><span data-stu-id="dd623-109">DESCRIPTION</span></span>

<span data-ttu-id="dd623-110">**Get-PswaAuthorizationRule** rutina vrací sadu autorizačních pravidel Windows PowerShell® Web Access.</span><span class="sxs-lookup"><span data-stu-id="dd623-110">The **Get-PswaAuthorizationRule** cmdlet returns a set of the Windows PowerShell® Web Access authorization rules.</span></span>
<span data-ttu-id="dd623-111">Pokud **Id** parametr ani **RuleName** parametr zadaný, bude tato rutina obsahuje seznam všech pravidel.</span><span class="sxs-lookup"><span data-stu-id="dd623-111">If neither the **Id** parameter nor the **RuleName** parameter is specified, then this cmdlet lists all rules.</span></span> <span data-ttu-id="dd623-112">**Id** parametr můžete použít k filtrování výsledků.</span><span class="sxs-lookup"><span data-stu-id="dd623-112">The **Id** parameter can be used to filter the results.</span></span>

## <a name="parameters"></a><span data-ttu-id="dd623-113">PARAMETRY</span><span class="sxs-lookup"><span data-stu-id="dd623-113">PARAMETERS</span></span>

### <a name="-idltint32gt"></a><span data-ttu-id="dd623-114">-Id&lt;Int32\[\]&gt;</span><span class="sxs-lookup"><span data-stu-id="dd623-114">-Id&lt;Int32\[\]&gt;</span></span>

<span data-ttu-id="dd623-115">Určuje identifikátory (ID) pravidla, která by měl získat tuto rutinu.</span><span class="sxs-lookup"><span data-stu-id="dd623-115">Specifies the identifiers (IDs) of the rules that this cmdlet should get.</span></span> <span data-ttu-id="dd623-116">Pokud nejsou zadány žádné ID, tato rutina vrátí všechna autorizační pravidla.</span><span class="sxs-lookup"><span data-stu-id="dd623-116">If no IDs are specified, then this cmdlet returns all authorization rules.</span></span>

|||
|-|-|
| <span data-ttu-id="dd623-117">Aliasy</span><span class="sxs-lookup"><span data-stu-id="dd623-117">Aliases</span></span>                              | <span data-ttu-id="dd623-118">žádný</span><span class="sxs-lookup"><span data-stu-id="dd623-118">none</span></span>                                 |
| <span data-ttu-id="dd623-119">Povinné?</span><span class="sxs-lookup"><span data-stu-id="dd623-119">Required?</span></span>                            | <span data-ttu-id="dd623-120">false</span><span class="sxs-lookup"><span data-stu-id="dd623-120">false</span></span>                                |
| <span data-ttu-id="dd623-121">Pozice?</span><span class="sxs-lookup"><span data-stu-id="dd623-121">Position?</span></span>                            | <span data-ttu-id="dd623-122">2</span><span class="sxs-lookup"><span data-stu-id="dd623-122">2</span></span>                                    |
| <span data-ttu-id="dd623-123">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="dd623-123">Default Value</span></span>                        | <span data-ttu-id="dd623-124">žádný</span><span class="sxs-lookup"><span data-stu-id="dd623-124">none</span></span>                                 |
| <span data-ttu-id="dd623-125">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="dd623-125">Accept Pipeline Input?</span></span>               | <span data-ttu-id="dd623-126">Hodnotu true (ByValue, ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="dd623-126">True (ByValue, ByPropertyName)</span></span>       |
| <span data-ttu-id="dd623-127">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="dd623-127">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="dd623-128">false</span><span class="sxs-lookup"><span data-stu-id="dd623-128">false</span></span>                                |

### <a name="-rulenameltstringgt"></a><span data-ttu-id="dd623-129">-RuleName&lt;String\[\]&gt;</span><span class="sxs-lookup"><span data-stu-id="dd623-129">-RuleName&lt;String\[\]&gt;</span></span>

<span data-ttu-id="dd623-130">Určuje názvy autorizačních pravidel pro načtení.</span><span class="sxs-lookup"><span data-stu-id="dd623-130">Specifies the names of authorization rules to retrieve.</span></span> <span data-ttu-id="dd623-131">Tento parametr vrátí všechna pravidla, která přesně shodovat s názvy pravidel řetězců v toto pole.</span><span class="sxs-lookup"><span data-stu-id="dd623-131">This parameter returns any rules that exactly match the rule names of the strings in this array.</span></span>

|||
|-|-|
| <span data-ttu-id="dd623-132">Aliasy</span><span class="sxs-lookup"><span data-stu-id="dd623-132">Aliases</span></span>                              | <span data-ttu-id="dd623-133">žádný</span><span class="sxs-lookup"><span data-stu-id="dd623-133">none</span></span>                                 |
| <span data-ttu-id="dd623-134">Povinné?</span><span class="sxs-lookup"><span data-stu-id="dd623-134">Required?</span></span>                            | <span data-ttu-id="dd623-135">Hodnota TRUE</span><span class="sxs-lookup"><span data-stu-id="dd623-135">true</span></span>                                 |
| <span data-ttu-id="dd623-136">Pozice?</span><span class="sxs-lookup"><span data-stu-id="dd623-136">Position?</span></span>                            | <span data-ttu-id="dd623-137">2</span><span class="sxs-lookup"><span data-stu-id="dd623-137">2</span></span>                                    |
| <span data-ttu-id="dd623-138">Výchozí hodnota</span><span class="sxs-lookup"><span data-stu-id="dd623-138">Default Value</span></span>                        | <span data-ttu-id="dd623-139">žádný</span><span class="sxs-lookup"><span data-stu-id="dd623-139">none</span></span>                                 |
| <span data-ttu-id="dd623-140">Přijmout kanálový vstup?</span><span class="sxs-lookup"><span data-stu-id="dd623-140">Accept Pipeline Input?</span></span>               | <span data-ttu-id="dd623-141">Hodnotu true (ByValue, ByPropertyName)</span><span class="sxs-lookup"><span data-stu-id="dd623-141">True (ByValue, ByPropertyName)</span></span>       |
| <span data-ttu-id="dd623-142">Přijímat zástupné znaky?</span><span class="sxs-lookup"><span data-stu-id="dd623-142">Accept Wildcard Characters?</span></span>          | <span data-ttu-id="dd623-143">false</span><span class="sxs-lookup"><span data-stu-id="dd623-143">false</span></span>                                |

### <a name="ltcommonparametersgt"></a><span data-ttu-id="dd623-144">&lt;CommonParameters&gt;</span><span class="sxs-lookup"><span data-stu-id="dd623-144">&lt;CommonParameters&gt;</span></span>

<span data-ttu-id="dd623-145">Tato rutina podporuje běžné parametry:-Verbose,-Debug, - ErrorAction, - ErrorVariable,-OutBuffer a - OutVariable.</span><span class="sxs-lookup"><span data-stu-id="dd623-145">This cmdlet supports the common parameters: -Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer, and -OutVariable.</span></span>
<span data-ttu-id="dd623-146">Další informace najdete v tématu [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span><span class="sxs-lookup"><span data-stu-id="dd623-146">For more information, see [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).</span></span>

## <a name="inputs"></a><span data-ttu-id="dd623-147">VSTUPY</span><span class="sxs-lookup"><span data-stu-id="dd623-147">INPUTS</span></span>

### <a name="int"></a><span data-ttu-id="dd623-148">celá čísla\[\]</span><span class="sxs-lookup"><span data-stu-id="dd623-148">int\[\]</span></span>

<span data-ttu-id="dd623-149">Tato rutina akceptuje jako vstupní pole celá čísla nebo pole řetězcové hodnoty.</span><span class="sxs-lookup"><span data-stu-id="dd623-149">This cmdlet accepts an array of integers or an array of string values as input.</span></span>

### <a name="string"></a><span data-ttu-id="dd623-150">Řetězec\[\]</span><span class="sxs-lookup"><span data-stu-id="dd623-150">String\[\]</span></span>

<span data-ttu-id="dd623-151">Tato rutina akceptuje jako vstupní pole celá čísla nebo pole řetězcové hodnoty.</span><span class="sxs-lookup"><span data-stu-id="dd623-151">This cmdlet accepts an array of integers or an array of string values as input.</span></span>

## <a name="outputs"></a><span data-ttu-id="dd623-152">VÝSTUPY</span><span class="sxs-lookup"><span data-stu-id="dd623-152">OUTPUTS</span></span>

### <a name="microsoftmanagementpowershellwebaccesspswaauthorizationrule"></a><span data-ttu-id="dd623-153">Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule\[\]</span><span class="sxs-lookup"><span data-stu-id="dd623-153">Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule\[\]</span></span>

<span data-ttu-id="dd623-154">Tato rutina vytvoří objekt PswaAuthorizationRule jako výstup.</span><span class="sxs-lookup"><span data-stu-id="dd623-154">This cmdlet produces a PswaAuthorizationRule object as output.</span></span>


## <a name="examples"></a><span data-ttu-id="dd623-155">PŘÍKLADY</span><span class="sxs-lookup"><span data-stu-id="dd623-155">EXAMPLES</span></span>

### <a name="example-1"></a><span data-ttu-id="dd623-156">PŘÍKLAD 1</span><span class="sxs-lookup"><span data-stu-id="dd623-156">EXAMPLE 1</span></span>

<span data-ttu-id="dd623-157">Tento příklad načte všechna pravidla.</span><span class="sxs-lookup"><span data-stu-id="dd623-157">This example gets all of the rules.</span></span>

```PowerShell
    PS C:\> Get-PswaAuthorizationRule
```

### <a name="example-2"></a><span data-ttu-id="dd623-158">PŘÍKLAD 2</span><span class="sxs-lookup"><span data-stu-id="dd623-158">EXAMPLE 2</span></span>

<span data-ttu-id="dd623-159">Tento příklad načte pravidlo s ID *2*.</span><span class="sxs-lookup"><span data-stu-id="dd623-159">This example gets a rule with an ID of *2*.</span></span>

```PowerShell
    PS C:\> Get-PswaAuthorizationRule –Id 2
```

### <a name="example-3-example-3-subheading"></a><span data-ttu-id="dd623-160">Příklad 3 {#example-3 .subHeading}</span><span class="sxs-lookup"><span data-stu-id="dd623-160">EXAMPLE 3 {#example-3 .subHeading}</span></span>

<span data-ttu-id="dd623-161">Tento příklad ukazuje, jak rutina umožňuje hodnotu z kanálu.</span><span class="sxs-lookup"><span data-stu-id="dd623-161">This example illustrates how the cmdlet accepts a value from pipeline.</span></span>
<span data-ttu-id="dd623-162">Id pravidla a název pravidla se předávají v této rutině.</span><span class="sxs-lookup"><span data-stu-id="dd623-162">A rule id and a rule name are passed in this cmdlet.</span></span>

```PowerShell
    PS C:\> "rule1",0 | Get-PswaAuthorizationRule
```

## <a name="related-topics"></a><span data-ttu-id="dd623-163">Příbuzná témata</span><span class="sxs-lookup"><span data-stu-id="dd623-163">Related topics</span></span>

- [<span data-ttu-id="dd623-164">Add-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="dd623-164">Add-PswaAuthorizationRule</span></span>](add-pswaauthorizationrule.md)
- [<span data-ttu-id="dd623-165">Remove-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="dd623-165">Remove-PswaAuthorizationRule</span></span>](remove-pswaauthorizationrule.md)
- [<span data-ttu-id="dd623-166">Test-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="dd623-166">Test-PswaAuthorizationRule</span></span>](test-pswaauthorizationrule.md)
- [<span data-ttu-id="dd623-167">Rutiny Install-PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="dd623-167">Install-PswaWebApplication</span></span>](install-pswawebapplication.md)