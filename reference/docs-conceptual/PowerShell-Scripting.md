---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Skriptování v prostředí PowerShell
ms.openlocfilehash: c6ba3abc2544834e2cbec16a524f79399a1d2599
ms.sourcegitcommit: 77f62a55cac8c13d69d51eef5fade18f71d66955
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/17/2018
ms.locfileid: "39094047"
---
# <a name="powershell"></a><span data-ttu-id="20c84-103">PowerShell</span><span class="sxs-lookup"><span data-stu-id="20c84-103">PowerShell</span></span>

<span data-ttu-id="20c84-104">Postaveno na rozhraní .NET Framework a prostředí PowerShell je prostředí příkazového řádku založeného na úlohách a skriptovací jazyk; je navržená speciálně pro správce systému a zkušení uživatelé rychle automatizovat správu více operačních systémů (Linux, macOS, Unix a Windows) a procesy, které souvisí s aplikacemi, které běží v těchto operačních systémech.</span><span class="sxs-lookup"><span data-stu-id="20c84-104">Built on the .NET Framework, PowerShell is a task-based command-line shell and scripting language; it is designed specifically for system administrators and power-users, to rapidly automate the administration of multiple operating systems (Linux, macOS, Unix, and Windows) and the processes related to the applications that run on those operating systems.</span></span>

## <a name="powershell-is-open-source"></a><span data-ttu-id="20c84-105">PowerShell je open source</span><span class="sxs-lookup"><span data-stu-id="20c84-105">PowerShell is open source</span></span>

<span data-ttu-id="20c84-106">Prostředí PowerShell základní zdrojový kód je nyní k dispozici na webu GitHub a otevřít příspěvky vytvořené komunitou.</span><span class="sxs-lookup"><span data-stu-id="20c84-106">PowerShell base source code is now available in GitHub and open to community contributions.</span></span>
<span data-ttu-id="20c84-107">Zobrazit [Powershellu source na Githubu](https://github.com/powershell/powershell).</span><span class="sxs-lookup"><span data-stu-id="20c84-107">See [PowerShell source on GitHub](https://github.com/powershell/powershell).</span></span>

<span data-ttu-id="20c84-108">Můžete začít s bity, je potřeba mít [získat PowerShell](https://github.com/PowerShell/PowerShell#get-powershell).</span><span class="sxs-lookup"><span data-stu-id="20c84-108">You can start with the bits you need at [Get PowerShell](https://github.com/PowerShell/PowerShell#get-powershell).</span></span>
<span data-ttu-id="20c84-109">Nebo možná s rychlou prohlídku u [Začínáme](https://github.com/PowerShell/PowerShell/blob/master/docs/learning-powershell)</span><span class="sxs-lookup"><span data-stu-id="20c84-109">Or, perhaps, with a quick tour at [Getting Started](https://github.com/PowerShell/PowerShell/blob/master/docs/learning-powershell)</span></span>

## <a name="powershell-design-goals"></a><span data-ttu-id="20c84-110">Cíle návrhu prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="20c84-110">PowerShell design goals</span></span>
<span data-ttu-id="20c84-111">PowerShell slouží ke zlepšení prostředí příkazového řádku a skriptovací odstraňuje dlouhotrvající problémy a přidáním nových funkcí.</span><span class="sxs-lookup"><span data-stu-id="20c84-111">PowerShell is designed to improve the command-line and scripting environment by eliminating long-standing problems and adding new features.</span></span>

### <a name="discoverability"></a><span data-ttu-id="20c84-112">Zjistitelnost</span><span class="sxs-lookup"><span data-stu-id="20c84-112">Discoverability</span></span>
<span data-ttu-id="20c84-113">PowerShell umožňuje snadno zjistit jeho funkcí.</span><span class="sxs-lookup"><span data-stu-id="20c84-113">PowerShell makes it easy to discover its features.</span></span> <span data-ttu-id="20c84-114">Například najdete seznam rutin, které zobrazení a změna služby Windows, zadejte:</span><span class="sxs-lookup"><span data-stu-id="20c84-114">For example, to find a list of cmdlets that view and change Windows services, type:</span></span>

```powershell
Get-Command *-Service
```

<span data-ttu-id="20c84-115">Po zjištění, které rutina provede úlohu, můžete další informace o rutině pomocí `Get-Help` rutiny.</span><span class="sxs-lookup"><span data-stu-id="20c84-115">After discovering which cmdlet accomplishes a task, you can learn more about the cmdlet by using the `Get-Help` cmdlet.</span></span>
<span data-ttu-id="20c84-116">Například pro zobrazení nápovědy o `Get-Service` rutiny, typ:</span><span class="sxs-lookup"><span data-stu-id="20c84-116">For example, to display help about the `Get-Service` cmdlet, type:</span></span>

```powershell
Get-Help Get-Service
```
<span data-ttu-id="20c84-117">Většina rutin generování objektů, které je možné ovládat a pak vykreslí do textu k zobrazení.</span><span class="sxs-lookup"><span data-stu-id="20c84-117">Most cmdlets emit objects which can be manipulated and then rendered into text for display.</span></span>
<span data-ttu-id="20c84-118">Abyste úplně pochopili výstup této rutiny, kanálem jeho výstup `Get-Member` rutiny.</span><span class="sxs-lookup"><span data-stu-id="20c84-118">To fully understand the output of that cmdlet, pipe its output to the `Get-Member` cmdlet.</span></span>
<span data-ttu-id="20c84-119">Například následující příkaz zobrazí informace o členech výstup objektu podle `Get-Service` rutiny.</span><span class="sxs-lookup"><span data-stu-id="20c84-119">For example, the following command displays information about the members of the object output by the `Get-Service` cmdlet.</span></span>

```powershell
Get-Service | Get-Member
```

### <a name="consistency"></a><span data-ttu-id="20c84-120">Konzistence</span><span class="sxs-lookup"><span data-stu-id="20c84-120">Consistency</span></span>
<span data-ttu-id="20c84-121">Správa systémů může být složité zařízeními a nástrojů, které mají konzistentní rozhraní pomáhají řídit zákonitou složitost.</span><span class="sxs-lookup"><span data-stu-id="20c84-121">Managing systems can be a complex endeavor and tools that have a consistent interface help to control the inherent complexity.</span></span>
<span data-ttu-id="20c84-122">Bohužel byl vědět nástroje příkazového řádku ani skriptovatelný objekty modelu COM pro jejich konzistence.</span><span class="sxs-lookup"><span data-stu-id="20c84-122">Unfortunately, neither command-line tools nor scriptable COM objects have been known for their consistency.</span></span>

<span data-ttu-id="20c84-123">Konzistence Powershellu je jedním z jeho primární prostředky.</span><span class="sxs-lookup"><span data-stu-id="20c84-123">The consistency of PowerShell is one of its primary assets.</span></span>
<span data-ttu-id="20c84-124">Například, pokud se dozvíte, jak používat `Sort-Object` rutiny, vám pomůže dané znalosti seřadit výstup všechny rutiny.</span><span class="sxs-lookup"><span data-stu-id="20c84-124">For example, if you learn how to use the `Sort-Object` cmdlet, you can use that knowledge to sort the output of any cmdlet.</span></span>
<span data-ttu-id="20c84-125">Není nutné další různé rutiny řazení jednotlivých rutin.</span><span class="sxs-lookup"><span data-stu-id="20c84-125">You do not have to learn the different sorting routines of each cmdlet.</span></span>

<span data-ttu-id="20c84-126">Vývojáři rutiny navíc není potřeba navrhovat funkce řazení pro jejich rutiny.</span><span class="sxs-lookup"><span data-stu-id="20c84-126">In addition, cmdlet developers do not have to design sorting features for their cmdlets.</span></span>
<span data-ttu-id="20c84-127">PowerShell je poskytuje rozhraní, které poskytuje základní funkce a vynutí, aby byla konzistentní o mnoho aspektů rozhraní.</span><span class="sxs-lookup"><span data-stu-id="20c84-127">PowerShell gives them a framework that provides the basic features and forces them to be consistent about many aspects of the interface.</span></span>
<span data-ttu-id="20c84-128">Rozhraní framework eliminuje některé z možností, které jsou obvykle ponechána pro vývojáře, ale na oplátku umožňuje vývoj rutin robustní a snadno použitelné mnohem jednodušší.</span><span class="sxs-lookup"><span data-stu-id="20c84-128">The framework eliminates some of the choices that are typically left to the developer, but, in return, it makes the development of robust and easy-to-use cmdlets much simpler.</span></span>

### <a name="interactive-and-scripting-environments"></a><span data-ttu-id="20c84-129">Interaktivní a skriptovací prostředí</span><span class="sxs-lookup"><span data-stu-id="20c84-129">Interactive and Scripting Environments</span></span>
<span data-ttu-id="20c84-130">PowerShell je kombinované skriptování a interaktivní prostředí, které poskytuje přístup k nástroji příkazového řádku a objekty modelu COM a také umožňuje používat napájení z rozhraní .NET Framework třída Library (FCL).</span><span class="sxs-lookup"><span data-stu-id="20c84-130">PowerShell is a combined interactive and scripting environment that gives you access to command-line tools and COM objects, and also enables you to use the power of the .NET Framework Class Library (FCL).</span></span>

<span data-ttu-id="20c84-131">Toto prostředí zlepšuje po Windows příkazového řádku, která poskytuje interaktivní prostředí s více nástrojů příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="20c84-131">This environment improves upon the Windows Command Prompt, which provides an interactive environment with multiple command-line tools.</span></span>
<span data-ttu-id="20c84-132">Je také dále to vylepšuje skriptů Windows Script Host (WSH), které vám umožní používat více nástrojů pro příkazový řádek a objekty automatizace COM, ale neposkytuje interaktivního prostředí.</span><span class="sxs-lookup"><span data-stu-id="20c84-132">It also improves upon Windows Script Host (WSH) scripts, which let you use multiple command-line tools and COM automation objects, but do not provide an interactive environment.</span></span>

<span data-ttu-id="20c84-133">Kombinací přístup ke všem z těchto funkcí Powershellu rozšiřuje možnosti interaktivního uživatele a skripty a díky lépe zvládnutelné Správa systému.</span><span class="sxs-lookup"><span data-stu-id="20c84-133">By combining access to all of these features, PowerShell extends the ability of the interactive user and the script writer, and makes system administration more manageable.</span></span>

### <a name="object-orientation"></a><span data-ttu-id="20c84-134">Objekt orientace</span><span class="sxs-lookup"><span data-stu-id="20c84-134">Object Orientation</span></span>
<span data-ttu-id="20c84-135">I když pracujete s prostředím PowerShell zadáním příkazů v textu, prostředí PowerShell je založená na objektech, ne text.</span><span class="sxs-lookup"><span data-stu-id="20c84-135">Although you interact with PowerShell by typing commands in text, PowerShell is based on objects, not text.</span></span>
<span data-ttu-id="20c84-136">Výstup příkazu je objekt.</span><span class="sxs-lookup"><span data-stu-id="20c84-136">The output of a command is an object.</span></span>
<span data-ttu-id="20c84-137">Můžete odeslat výstupní objekt k jinému příkazu jako vstup.</span><span class="sxs-lookup"><span data-stu-id="20c84-137">You can send the output object to another command as its input.</span></span>
<span data-ttu-id="20c84-138">V důsledku toho prostředí PowerShell poskytuje známému rozhraní lidem se zkušenostmi s jiné prostředí, při Představujeme novou a výkonnou paradigma příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="20c84-138">As a result, PowerShell provides a familiar interface to people experienced with other shells, while introducing a new and powerful command-line paradigm.</span></span>
<span data-ttu-id="20c84-139">Rozšiřuje koncept odesílání dat mezi příkazy tím, že povolíte odesílání objektů, spíše než textovém.</span><span class="sxs-lookup"><span data-stu-id="20c84-139">It extends the concept of sending data between commands by enabling you to send objects, rather than text.</span></span>

### <a name="easy-transition-to-scripting"></a><span data-ttu-id="20c84-140">Snadný přechod do skriptů</span><span class="sxs-lookup"><span data-stu-id="20c84-140">Easy Transition to Scripting</span></span>
<span data-ttu-id="20c84-141">Díky Powershellu usnadňuje přechod od psaní příkazů interaktivně k vytváření a spouštění skriptů.</span><span class="sxs-lookup"><span data-stu-id="20c84-141">PowerShell makes it easy to transition from typing commands interactively to creating and running scripts.</span></span>
<span data-ttu-id="20c84-142">Můžete zadávat příkazy příkazového řádku Powershellu se zjistit příkazy, které provádějí úlohy.</span><span class="sxs-lookup"><span data-stu-id="20c84-142">You can type commands at the PowerShell command prompt to discover the commands that perform a task.</span></span>
<span data-ttu-id="20c84-143">Potom můžete uložit tyto příkazy v řádné záznamy o studiu nebo historii před zkopírováním do souboru pro použití jako skript.</span><span class="sxs-lookup"><span data-stu-id="20c84-143">Then, you can save those commands in a transcript or a history before copying them to a file for use as a script.</span></span>
