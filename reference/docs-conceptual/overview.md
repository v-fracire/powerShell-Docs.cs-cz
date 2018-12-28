---
ms.date: 08/27/2018
keywords: rutiny prostředí PowerShell
title: Skriptování v prostředí PowerShell
ms.openlocfilehash: 07925ce8dcafd33970a703c9b241bf6f76f88d10
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403810"
---
# <a name="powershell"></a><span data-ttu-id="b266b-103">PowerShell</span><span class="sxs-lookup"><span data-stu-id="b266b-103">PowerShell</span></span>

<span data-ttu-id="b266b-104">PowerShell je prostředí příkazového řádku založeného na úlohách a skriptovací jazyk založená na rozhraní .NET.</span><span class="sxs-lookup"><span data-stu-id="b266b-104">PowerShell is a task-based command-line shell and scripting language built on .NET.</span></span>
<span data-ttu-id="b266b-105">PowerShell umožňuje správcům systému a zkušení uživatelé rychle automatizace úloh, které spravovat operační systémy (Linux, macOS a Windows) a procesy.</span><span class="sxs-lookup"><span data-stu-id="b266b-105">PowerShell helps system administrators and power-users rapidly automate tasks that manage operating systems (Linux, macOS, and Windows) and processes.</span></span>

<span data-ttu-id="b266b-106">Příkazy prostředí PowerShell umožňují spravovat počítače z příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="b266b-106">PowerShell commands let you manage computers from the command line.</span></span> <span data-ttu-id="b266b-107">Zprostředkovatelé prostředí PowerShell vám umožní přistupovat k úložištím dat, jako je například registr a úložiště certifikátů, stejně snadno, jako je přístup k systému souborů.</span><span class="sxs-lookup"><span data-stu-id="b266b-107">PowerShell providers let you access data stores, such as the registry and certificate store, as easily as you access the file system.</span></span> <span data-ttu-id="b266b-108">PowerShell zahrnuje analyzátor výrazů a propracovaný skriptovací jazyk.</span><span class="sxs-lookup"><span data-stu-id="b266b-108">PowerShell includes a rich expression parser and a fully developed scripting language.</span></span>

## <a name="powershell-is-open-source"></a><span data-ttu-id="b266b-109">PowerShell je open source</span><span class="sxs-lookup"><span data-stu-id="b266b-109">PowerShell is open-source</span></span>

<span data-ttu-id="b266b-110">Prostředí PowerShell základní zdrojový kód je nyní k dispozici na webu GitHub a otevřít příspěvky vytvořené komunitou.</span><span class="sxs-lookup"><span data-stu-id="b266b-110">PowerShell base source code is now available in GitHub and open to community contributions.</span></span>
<span data-ttu-id="b266b-111">Zobrazit [Powershellu source na Githubu](https://github.com/powershell/powershell).</span><span class="sxs-lookup"><span data-stu-id="b266b-111">See [PowerShell source on GitHub](https://github.com/powershell/powershell).</span></span>

<span data-ttu-id="b266b-112">Můžete začít s bity, je potřeba mít [získat PowerShell](https://github.com/PowerShell/PowerShell#get-powershell).</span><span class="sxs-lookup"><span data-stu-id="b266b-112">You can start with the bits you need at [Get PowerShell](https://github.com/PowerShell/PowerShell#get-powershell).</span></span>
<span data-ttu-id="b266b-113">Nebo možná s rychlou prohlídku u [Začínáme](https://github.com/PowerShell/PowerShell/blob/master/docs/learning-powershell).</span><span class="sxs-lookup"><span data-stu-id="b266b-113">Or, perhaps, with a quick tour at [Getting Started](https://github.com/PowerShell/PowerShell/blob/master/docs/learning-powershell).</span></span>

## <a name="powershell-design-goals"></a><span data-ttu-id="b266b-114">Cíle návrhu prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="b266b-114">PowerShell design goals</span></span>

<span data-ttu-id="b266b-115">PowerShell slouží ke zlepšení prostředí příkazového řádku a skriptovací odstraňuje dlouhotrvající problémy a přidáním nových funkcí.</span><span class="sxs-lookup"><span data-stu-id="b266b-115">PowerShell is designed to improve the command-line and scripting environment by eliminating long-standing problems and adding new features.</span></span>

### <a name="discoverability"></a><span data-ttu-id="b266b-116">Zjistitelnost</span><span class="sxs-lookup"><span data-stu-id="b266b-116">Discoverability</span></span>

<span data-ttu-id="b266b-117">PowerShell umožňuje snadno zjistit jeho funkcí.</span><span class="sxs-lookup"><span data-stu-id="b266b-117">PowerShell makes it easy to discover its features.</span></span> <span data-ttu-id="b266b-118">Například najdete seznam rutin, které zobrazení a změna služby Windows, zadejte:</span><span class="sxs-lookup"><span data-stu-id="b266b-118">For example, to find a list of cmdlets that view and change Windows services, type:</span></span>

```powershell
Get-Command *-Service
```

<span data-ttu-id="b266b-119">Po zjištění, které rutina provede úlohu, můžete další informace o rutině pomocí `Get-Help` rutiny.</span><span class="sxs-lookup"><span data-stu-id="b266b-119">After discovering which cmdlet accomplishes a task, you can learn more about the cmdlet by using the `Get-Help` cmdlet.</span></span> <span data-ttu-id="b266b-120">Například pro zobrazení nápovědy o `Get-Service` rutiny, typ:</span><span class="sxs-lookup"><span data-stu-id="b266b-120">For example, to display help about the `Get-Service` cmdlet, type:</span></span>

```powershell
Get-Help Get-Service
```

<span data-ttu-id="b266b-121">Většina rutin návratových objektů, které mohou manipulovat a pak se vykresluje jako text k zobrazení.</span><span class="sxs-lookup"><span data-stu-id="b266b-121">Most cmdlets return objects that can be manipulated and then rendered as text for display.</span></span> <span data-ttu-id="b266b-122">Abyste úplně pochopili výstupu rutiny, přesměrujte výstup do `Get-Member` rutiny.</span><span class="sxs-lookup"><span data-stu-id="b266b-122">To fully understand the output of a cmdlet, pipe the output to the `Get-Member` cmdlet.</span></span> <span data-ttu-id="b266b-123">Například následující příkaz zobrazí informace o členech výstup objektu podle `Get-Service` rutiny.</span><span class="sxs-lookup"><span data-stu-id="b266b-123">For example, the following command displays information about the members of the object output by the `Get-Service` cmdlet.</span></span>

```powershell
Get-Service | Get-Member
```

### <a name="consistency"></a><span data-ttu-id="b266b-124">Konzistence</span><span class="sxs-lookup"><span data-stu-id="b266b-124">Consistency</span></span>

<span data-ttu-id="b266b-125">Správa systémů může být složitý úkol.</span><span class="sxs-lookup"><span data-stu-id="b266b-125">Managing systems can be a complex task.</span></span> <span data-ttu-id="b266b-126">Nástroje, které mají nápovědu jednotné rozhraní pro řízení zákonitou složitost.</span><span class="sxs-lookup"><span data-stu-id="b266b-126">Tools that have a consistent interface help to control the inherent complexity.</span></span> <span data-ttu-id="b266b-127">Bohužel nástrojů příkazového řádku a skriptovatelný objektů COM nejsou známy jejich konzistence.</span><span class="sxs-lookup"><span data-stu-id="b266b-127">Unfortunately, command-line tools and scriptable COM objects aren't known for their consistency.</span></span>

<span data-ttu-id="b266b-128">Konzistence Powershellu je jedním z jeho primární prostředky.</span><span class="sxs-lookup"><span data-stu-id="b266b-128">The consistency of PowerShell is one of its primary assets.</span></span> <span data-ttu-id="b266b-129">Například, pokud se dozvíte, jak používat `Sort-Object` rutiny, vám pomůže dané znalosti seřadit výstup všechny rutiny.</span><span class="sxs-lookup"><span data-stu-id="b266b-129">For example, if you learn how to use the `Sort-Object` cmdlet, you can use that knowledge to sort the output of any cmdlet.</span></span> <span data-ttu-id="b266b-130">Není nutné další různé rutiny řazení jednotlivých rutin.</span><span class="sxs-lookup"><span data-stu-id="b266b-130">You don't have to learn the different sorting routines of each cmdlet.</span></span>

<span data-ttu-id="b266b-131">Kromě toho rutina vývojáři nemuseli navrhnout řazení funkce pro jejich rutiny.</span><span class="sxs-lookup"><span data-stu-id="b266b-131">Additionally, cmdlet developers don't have to design sorting features for their cmdlets.</span></span> <span data-ttu-id="b266b-132">PowerShell nabízí rozhraní se základními funkcemi, které vynutí konzistence.</span><span class="sxs-lookup"><span data-stu-id="b266b-132">PowerShell provides a framework with the basic features that forces consistency.</span></span> <span data-ttu-id="b266b-133">Rozhraní framework eliminuje některé možnosti, které jsou ponechána pro vývojáře.</span><span class="sxs-lookup"><span data-stu-id="b266b-133">The framework eliminates some choices that are left to the developer.</span></span> <span data-ttu-id="b266b-134">Ale naopak to vývoj rutin značně zjednodušuje.</span><span class="sxs-lookup"><span data-stu-id="b266b-134">But, in return, it makes the development of cmdlets much simpler.</span></span>

### <a name="interactive-and-scripting-environments"></a><span data-ttu-id="b266b-135">Interaktivní a skriptovací prostředí</span><span class="sxs-lookup"><span data-stu-id="b266b-135">Interactive and scripting environments</span></span>

<span data-ttu-id="b266b-136">Příkazový řádek Windows poskytuje interaktivní prostředí s přístupem k nástroji příkazového řádku a skriptování základní.</span><span class="sxs-lookup"><span data-stu-id="b266b-136">The Windows Command Prompt provides an interactive shell with access to command-line tools and basic scripting.</span></span> <span data-ttu-id="b266b-137">Windows Script Host (WSH) je možné používat skripty příkazového řádku nástroje a objekty automatizace COM, ale neposkytuje interaktivní prostředí.</span><span class="sxs-lookup"><span data-stu-id="b266b-137">Windows Script Host (WSH) has scriptable command-line tools and COM automation objects, but doesn't provide an interactive shell.</span></span>

<span data-ttu-id="b266b-138">Prostředí PowerShell spojuje interaktivní prostředí a skriptovací prostředí.</span><span class="sxs-lookup"><span data-stu-id="b266b-138">PowerShell combines an interactive shell and a scripting environment.</span></span> <span data-ttu-id="b266b-139">Prostředí PowerShell můžete přistupovat k nástroje příkazového řádku, objekty COM a knihovny tříd .NET.</span><span class="sxs-lookup"><span data-stu-id="b266b-139">PowerShell can access command-line tools, COM objects, and .NET class libraries.</span></span> <span data-ttu-id="b266b-140">Tato kombinace funkcí rozšiřuje možnosti interaktivního uživatele, skripty a správce systému.</span><span class="sxs-lookup"><span data-stu-id="b266b-140">This combination of features extends the capabilities of the interactive user, the script writer, and the system administrator.</span></span>

### <a name="object-orientation"></a><span data-ttu-id="b266b-141">Objekt orientace</span><span class="sxs-lookup"><span data-stu-id="b266b-141">Object orientation</span></span>

<span data-ttu-id="b266b-142">PowerShell je založená na objekt není text.</span><span class="sxs-lookup"><span data-stu-id="b266b-142">PowerShell is based on object not text.</span></span> <span data-ttu-id="b266b-143">Výstup příkazu je objekt.</span><span class="sxs-lookup"><span data-stu-id="b266b-143">The output of a command is an object.</span></span> <span data-ttu-id="b266b-144">Výstupní objekt, prostřednictvím kanálu, můžete odeslat k jinému příkazu jako vstup.</span><span class="sxs-lookup"><span data-stu-id="b266b-144">You can send the output object, through the pipeline, to another command as its input.</span></span>

<span data-ttu-id="b266b-145">Tento kanál obsahuje známému rozhraní pro osoby zkušenosti s další prostředí.</span><span class="sxs-lookup"><span data-stu-id="b266b-145">This pipeline provides a familiar interface for people experienced with other shells.</span></span> <span data-ttu-id="b266b-146">Prostředí PowerShell rozšiřuje tento koncept odesláním objekty namísto textu.</span><span class="sxs-lookup"><span data-stu-id="b266b-146">PowerShell extends this concept by sending objects rather than text.</span></span>

### <a name="easy-transition-to-scripting"></a><span data-ttu-id="b266b-147">Snadný přechod do skriptů</span><span class="sxs-lookup"><span data-stu-id="b266b-147">Easy transition to scripting</span></span>

<span data-ttu-id="b266b-148">Díky možnosti rozpoznání příkazu Powershellu usnadňuje přechod od psaní příkazů interaktivně k vytváření a spouštění skriptů.</span><span class="sxs-lookup"><span data-stu-id="b266b-148">PowerShell's command discoverability makes it easy to transition from typing commands interactively to creating and running scripts.</span></span> <span data-ttu-id="b266b-149">Záznamy o studiu prostředí PowerShell a historie usnadňují kopírování příkazů do souboru pro použití jako skript.</span><span class="sxs-lookup"><span data-stu-id="b266b-149">PowerShell transcripts and history make it easy to copy commands to a file for use as a script.</span></span>
