---
description: 
ms.topic: article
ms.prod: powershell
keywords: "rutiny prostředí PowerShell"
ms.date: 2016-12-12
title: "rutiny webový přístup"
ms.technology: powershell
ms.openlocfilehash: 54821c318b165461ec613678a39c4e3b500dfd0e
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="windows-powershell-web-access-cmdlets"></a><span data-ttu-id="f85fb-103">Rutiny Windows PowerShell Web Accessu</span><span class="sxs-lookup"><span data-stu-id="f85fb-103">Windows PowerShell Web Access Cmdlets</span></span>

<span data-ttu-id="f85fb-104">Tento odkaz obsahuje popisy rutinu a syntaxi pro všechny rutiny specifické pro Windows PowerShell® Web Access.</span><span class="sxs-lookup"><span data-stu-id="f85fb-104">This reference provides cmdlet descriptions and syntax for all Windows PowerShell® Web Access-specific cmdlets.</span></span> <span data-ttu-id="f85fb-105">Zobrazí se seznam rutin v abecedním pořadí založené na příkazu na začátku rutiny.</span><span class="sxs-lookup"><span data-stu-id="f85fb-105">It lists the cmdlets in alphabetical order based on the verb at the beginning of the cmdlet.</span></span>

## <a name="add-pswaauthorizationruleadd-pswaauthorizationrulemd"></a>[<span data-ttu-id="f85fb-106">Add-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="f85fb-106">Add-PswaAuthorizationRule</span></span>](add-pswaauthorizationrule.md)

<span data-ttu-id="f85fb-107">Přidá nové autorizační pravidlo je sada pravidel autorizace pro Windows PowerShell® Web Access.</span><span class="sxs-lookup"><span data-stu-id="f85fb-107">Adds a new authorization rule to the Windows PowerShell® Web Access authorization rule set.</span></span>

## <a name="get-pswaauthorizationruleget-pswaauthorizationrulemd"></a>[<span data-ttu-id="f85fb-108">Get-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="f85fb-108">Get-PswaAuthorizationRule</span></span>](get-pswaauthorizationrule.md)

<span data-ttu-id="f85fb-109">Vrací sadu autorizačních pravidel Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="f85fb-109">Returns a set of the Windows PowerShell Web Access authorization rules.</span></span>

## <a name="install-pswawebapplicationinstall-pswawebapplicationmd"></a>[<span data-ttu-id="f85fb-110">Rutiny Install-PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="f85fb-110">Install-PswaWebApplication</span></span>](install-pswawebapplication.md)

<span data-ttu-id="f85fb-111">Nakonfiguruje Windows PowerShell Web Access webové aplikace ve službě IIS.</span><span class="sxs-lookup"><span data-stu-id="f85fb-111">Configures the Windows PowerShell Web Access web application in IIS.</span></span>

## <a name="remove-pswaauthorizationruleremove-pswaauthorizationrulemd"></a>[<span data-ttu-id="f85fb-112">Remove-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="f85fb-112">Remove-PswaAuthorizationRule</span></span>](remove-pswaauthorizationrule.md)

<span data-ttu-id="f85fb-113">Odebere zadané autorizační pravidlo z Windows PowerShell Web Access.</span><span class="sxs-lookup"><span data-stu-id="f85fb-113">Removes a specified authorization rule from Windows PowerShell Web Access.</span></span>

## <a name="test-pswaauthorizationruletest-pswaauthorizationrulemd"></a>[<span data-ttu-id="f85fb-114">Test-PswaAuthorizationRule</span><span class="sxs-lookup"><span data-stu-id="f85fb-114">Test-PswaAuthorizationRule</span></span>](test-pswaauthorizationrule.md)

<span data-ttu-id="f85fb-115">Testy autorizační pravidla ověření, že určitého uživatele, počítače, žádost o přístup koncový bod má oprávnění.</span><span class="sxs-lookup"><span data-stu-id="f85fb-115">Tests authorization rules to validate that a particular user, computer, endpoint access request is authorized.</span></span>

## <a name="uninstall-pswawebapplicationuninstall-pswawebapplicationmd"></a>[<span data-ttu-id="f85fb-116">Uninstall-PswaWebApplication</span><span class="sxs-lookup"><span data-stu-id="f85fb-116">Uninstall-PswaWebApplication</span></span>](uninstall-pswawebapplication.md)

<span data-ttu-id="f85fb-117">Prostředí Windows PowerShell webové aplikace se odinstaluje ze služby IIS.</span><span class="sxs-lookup"><span data-stu-id="f85fb-117">Uninstalls the Windows PowerShell web application from IIS.</span></span>

><span data-ttu-id="f85fb-118">**Poznámka:**:</span><span class="sxs-lookup"><span data-stu-id="f85fb-118">**Note**:</span></span>
>
><span data-ttu-id="f85fb-119">Chcete-li zobrazit seznam všech rutin, které jsou k dispozici, použijte:</span><span class="sxs-lookup"><span data-stu-id="f85fb-119">To list all the cmdlets that are available, use the:</span></span>
>
> <span data-ttu-id="f85fb-120">`Get-Command –Module PowerShellWebAccess`rutiny.</span><span class="sxs-lookup"><span data-stu-id="f85fb-120">`Get-Command –Module PowerShellWebAccess` cmdlet.</span></span>

<span data-ttu-id="f85fb-121">Další informace o nebo jejich syntaxi rutiny, použijte:</span><span class="sxs-lookup"><span data-stu-id="f85fb-121">For more information about, or for the syntax of, any of the cmdlets, use:</span></span>  
<span data-ttu-id="f85fb-122">`Get-Help `*&lt;Název rutiny&gt;*</span><span class="sxs-lookup"><span data-stu-id="f85fb-122">`Get-Help `*&lt;cmdlet name&gt;*</span></span>  
<span data-ttu-id="f85fb-123">kde  *&lt;název rutiny&gt;*  představuje název rutiny, které chcete prozkoumat.</span><span class="sxs-lookup"><span data-stu-id="f85fb-123">where *&lt;cmdlet name&gt;* is the name of the cmdlet that you want to research.</span></span>

<span data-ttu-id="f85fb-124">Podrobnější informace můžete získat spuštěním těchto rutin:</span><span class="sxs-lookup"><span data-stu-id="f85fb-124">For more detailed information, you can run any of the following cmdlets:</span></span>

- <span data-ttu-id="f85fb-125">`Get-Help `*&lt;Název rutiny&gt;*` -Detailed`</span><span class="sxs-lookup"><span data-stu-id="f85fb-125">`Get-Help `*&lt;cmdlet name&gt;*` -Detailed`</span></span>
- <span data-ttu-id="f85fb-126">`Get-Help `*&lt;Název rutiny&gt;*` -Examples`</span><span class="sxs-lookup"><span data-stu-id="f85fb-126">`Get-Help `*&lt;cmdlet name&gt;*` -Examples`</span></span>
- <span data-ttu-id="f85fb-127">`Get-Help `*&lt;Název rutiny&gt;*` -Full`</span><span class="sxs-lookup"><span data-stu-id="f85fb-127">`Get-Help `*&lt;cmdlet name&gt;*` -Full`</span></span>

### <a name="more-information"></a><span data-ttu-id="f85fb-128">Další informace</span><span class="sxs-lookup"><span data-stu-id="f85fb-128">More Information</span></span>

<span data-ttu-id="f85fb-129">Další informace o prostředí PowerShell Web Access naleznete v následujících tématech:</span><span class="sxs-lookup"><span data-stu-id="f85fb-129">For more information about PowerShell Web Access, see the following:</span></span>

- [<span data-ttu-id="f85fb-130">Nainstalovat a používat Windows PowerShell Web Accessu</span><span class="sxs-lookup"><span data-stu-id="f85fb-130">Install and Use Windows PowerShell Web Access</span></span>](../install-and-use-windows-powershell-web-access.md)

