---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Seznámení s koncepty důležité Windows PowerShell"
ms.assetid: 3e601e38-4520-4578-a48d-b6779f1d35ee
ms.openlocfilehash: 1ffcfefcc7ffc7c98ba4d1e3ccc9a59cd9b0baac
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/03/2017
---
# <a name="understanding-important-windows-powershell-concepts"></a><span data-ttu-id="afd70-103">Seznámení s koncepty důležité Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="afd70-103">Understanding Important Windows PowerShell Concepts</span></span>
<span data-ttu-id="afd70-104">Prostředí Windows PowerShell návrhu integruje koncepty z mnoha různých prostředích.</span><span class="sxs-lookup"><span data-stu-id="afd70-104">The Windows PowerShell design integrates concepts from many different environments.</span></span> <span data-ttu-id="afd70-105">Několik z nich jsou známé uživatelům s prostředím v součásti pro konkrétní nebo programovací prostředí, ale jen několik lidí věděli o všech z nich.</span><span class="sxs-lookup"><span data-stu-id="afd70-105">Several of them are familiar to people with experience in specific shells or programming environments, but very few people will know about all of them.</span></span> <span data-ttu-id="afd70-106">Vyhledávání na některé z těchto pojmech obsahuje užitečné Přehled prostředí.</span><span class="sxs-lookup"><span data-stu-id="afd70-106">Looking at some of these concepts provides a useful overview of the shell.</span></span>

### <a name="commands-are-not-text-based"></a><span data-ttu-id="afd70-107">Příkazy nejsou založený na textu</span><span class="sxs-lookup"><span data-stu-id="afd70-107">Commands Are Not Text-Based</span></span>
<span data-ttu-id="afd70-108">Na rozdíl od tradičních rozhraní příkazového řádku příkazy prostředí Windows PowerShell rutiny jsou navrženy tak, jak nakládat s objekty - strukturovaná informace, které je více než jen řetězec znaků, které jsou uvedeny na obrazovce.</span><span class="sxs-lookup"><span data-stu-id="afd70-108">Unlike traditional command-line interface commands, Windows PowerShell cmdlets are designed to deal with objects - structured information that is more than just a string of characters appearing on the screen.</span></span> <span data-ttu-id="afd70-109">Vždy výstup příkazu představuje podél doplňující informace, které můžete použít, pokud to potřebujete.</span><span class="sxs-lookup"><span data-stu-id="afd70-109">Command output always carries along extra information that you can use if you need it.</span></span> <span data-ttu-id="afd70-110">Toto téma podrobněji, v tomto dokumentu se budeme zabývat.</span><span class="sxs-lookup"><span data-stu-id="afd70-110">We will discuss this topic in depth in this document.</span></span>

<span data-ttu-id="afd70-111">Pokud jste použili text zpracování nástroje ke zpracování příkazového řádku data v minulosti, zjistíte, že budou chovat jinak Pokud se pokusíte použít je v prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="afd70-111">If you have used text-processing tools to process command-line data in the past, you will find that they behave differently if you try to use them in Windows PowerShell.</span></span> <span data-ttu-id="afd70-112">Ve většině případů není nutné nástrojů pro zpracování textu k extrakci konkrétní informace.</span><span class="sxs-lookup"><span data-stu-id="afd70-112">In most cases, you do not need text-processing tools to extract specific information.</span></span> <span data-ttu-id="afd70-113">Dostanete částem dat přímo pomocí standardní příkazy zpracování objektu prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="afd70-113">You can access portions of the data directly by using standard Windows PowerShell object manipulation commands.</span></span>

### <a name="the-command-family-is-extensible"></a><span data-ttu-id="afd70-114">Příkaz řada je rozšiřitelný</span><span class="sxs-lookup"><span data-stu-id="afd70-114">The Command Family Is Extensible</span></span>
<span data-ttu-id="afd70-115">Rozhraní, jako je například Cmd.exe neposkytují způsob, jak můžete přímo rozšířit sadu předdefinovaných příkazů.</span><span class="sxs-lookup"><span data-stu-id="afd70-115">Interfaces such as Cmd.exe do not provide a way for you to directly extend the built-in command set.</span></span> <span data-ttu-id="afd70-116">Můžete vytvořit externí nástroje příkazového řádku, které běží v Cmd.exe, ale tyto externí nástroje nemají služby, jako je Nápověda integrace a Cmd.exe nezná automaticky, že jsou platné příkazy.</span><span class="sxs-lookup"><span data-stu-id="afd70-116">You can create external command-line tools that run in Cmd.exe, but these external tools do not have services, such as Help integration, and Cmd.exe does not automatically know that they are valid commands.</span></span>

<span data-ttu-id="afd70-117">Nativní binární příkazy v prostředí Windows PowerShell, označuje jako *rutiny* (výrazný příkaz – umožňuje), může být rozšířen o rutiny, které vytvoříte a která přidáte do prostředí Windows PowerShell pomocí modulu snap in.</span><span class="sxs-lookup"><span data-stu-id="afd70-117">The native binary commands in Windows PowerShell, known as *cmdlets* (pronounced command-lets), can be augmented by cmdlets that you create and that you add to Windows PowerShell by using snap-ins.</span></span> <span data-ttu-id="afd70-118">Prostředí Windows PowerShell *moduly snap in* kompilovány, stejně jako binární nástroje v jiných rozhraní.</span><span class="sxs-lookup"><span data-stu-id="afd70-118">Windows PowerShell *snap-ins* are compiled, just like binary tools in any other interface.</span></span> <span data-ttu-id="afd70-119">Můžete je přidat do prostředí, jakož i nové rutiny prostředí Windows PowerShell poskytovatelů.</span><span class="sxs-lookup"><span data-stu-id="afd70-119">You can use them to add Windows PowerShell providers to the shell, as well as new cmdlets.</span></span>

<span data-ttu-id="afd70-120">Speciální charakter interní příkazy prostředí Windows PowerShell, bude označujeme je jako *rutiny*.</span><span class="sxs-lookup"><span data-stu-id="afd70-120">Because of the special nature of the Windows PowerShell internal commands, we will refer to them as *cmdlets*.</span></span>

> [!NOTE]
> <span data-ttu-id="afd70-121">Prostředí Windows PowerShell můžete spouštět příkazy než rutiny.</span><span class="sxs-lookup"><span data-stu-id="afd70-121">Windows PowerShell can run commands other than cmdlets.</span></span> <span data-ttu-id="afd70-122">Jsme nebude možné hovoříte o je podrobně v Průvodci uživatele Windows PowerShell, ale jsou užitečné vědět o jako kategorie typů příkaz.</span><span class="sxs-lookup"><span data-stu-id="afd70-122">We will not be discussing them in detail in the Windows PowerShell User's Guide, but they are useful to know about as categories of command types.</span></span> <span data-ttu-id="afd70-123">Prostředí Windows PowerShell podporuje skripty, které se podobá skripty prostředí UNIX a Cmd.exe dávkové soubory, ale jsou příponu názvu souboru .ps1.</span><span class="sxs-lookup"><span data-stu-id="afd70-123">Windows PowerShell supports scripts that are analogous to UNIX shell scripts and Cmd.exe batch files, but have a .ps1 file name extension.</span></span> <span data-ttu-id="afd70-124">Prostředí Windows PowerShell můžete taky vytvořit interní funkce, které lze použít přímo v rozhraní nebo ve skriptech.</span><span class="sxs-lookup"><span data-stu-id="afd70-124">Windows PowerShell also allows you to create internal functions that can be used directly in the interface or in scripts.</span></span>

### <a name="windows-powershell-handles-console-input-and-display"></a><span data-ttu-id="afd70-125">Vstup konzoly obslužných rutin prostředí PowerShell systému Windows a zobrazení</span><span class="sxs-lookup"><span data-stu-id="afd70-125">Windows PowerShell Handles Console Input and Display</span></span>
<span data-ttu-id="afd70-126">Když zadáte příkaz, prostředí Windows PowerShell vždy zpracovává příkazového řádku vstup přímo.</span><span class="sxs-lookup"><span data-stu-id="afd70-126">When you type a command, Windows PowerShell always processes the command-line input directly.</span></span> <span data-ttu-id="afd70-127">Prostředí Windows PowerShell taky formáty výstupu, který se zobrazí na obrazovce.</span><span class="sxs-lookup"><span data-stu-id="afd70-127">Windows PowerShell also formats the output that you see on the screen.</span></span> <span data-ttu-id="afd70-128">To je důležité, protože snižuje práce potřebné jednotlivých rutin a zajišťuje, že můžete vždy způsobem stejným způsobem, bez ohledu na to, které rutina, kterou používáte.</span><span class="sxs-lookup"><span data-stu-id="afd70-128">This is significant because it reduces the work required of each cmdlet and ensures that you can always do things the same way regardless of which cmdlet you are using.</span></span> <span data-ttu-id="afd70-129">Jedním z příkladů jak tato funkce zjednodušuje životnosti pro nástroj vývojáři a uživatelé je Nápověda příkazového řádku.</span><span class="sxs-lookup"><span data-stu-id="afd70-129">One example of how this simplifies life for both tool developers and users is command-line Help.</span></span>

<span data-ttu-id="afd70-130">Tradiční nástroje příkazového řádku mají své vlastní schémata požaduje a zobrazení nápovědy.</span><span class="sxs-lookup"><span data-stu-id="afd70-130">Traditional command-line tools have their own schemes for requesting and displaying Help.</span></span> <span data-ttu-id="afd70-131">Některé nástroje příkazového řádku použijte **/?**</span><span class="sxs-lookup"><span data-stu-id="afd70-131">Some command-line tools use **/?**</span></span> <span data-ttu-id="afd70-132">k aktivaci zobrazení nápovědy; jiné používají **-?**, **/H**, nebo i  **//** .</span><span class="sxs-lookup"><span data-stu-id="afd70-132">to trigger the Help display; others use **-?**, **/H**, or even **//**.</span></span> <span data-ttu-id="afd70-133">Některé zobrazí nápovědy v okně grafického uživatelského rozhraní, a nikoli v zobrazení konzoly.</span><span class="sxs-lookup"><span data-stu-id="afd70-133">Some will display Help in a GUI window, rather than in the console display.</span></span> <span data-ttu-id="afd70-134">Některé komplexní nástroje, například aktualizační aplikace, rozbalte soubory vnitřním před zobrazení jejich nápovědy.</span><span class="sxs-lookup"><span data-stu-id="afd70-134">Some complex tools, such as application updaters, unpack internal files before displaying their Help.</span></span> <span data-ttu-id="afd70-135">Pokud použijete nesprávný parametr, nástroj může ignorovat zadali a zahájit provádění úlohy automaticky.</span><span class="sxs-lookup"><span data-stu-id="afd70-135">If you use the wrong parameter, the tool might ignore what you typed and begin performing a task automatically.</span></span>

<span data-ttu-id="afd70-136">Když zadáte příkaz v prostředí Windows PowerShell, vše, co zadáte je automaticky analyzovat a předem zpracovány prostředím Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="afd70-136">When you enter a command in Windows PowerShell, everything you enter is automatically parsed and pre-processed by Windows PowerShell.</span></span> <span data-ttu-id="afd70-137">Pokud použijete **-?**</span><span class="sxs-lookup"><span data-stu-id="afd70-137">If you use the **-?**</span></span> <span data-ttu-id="afd70-138">Parametr s rutiny prostředí Windows PowerShell, vždy znamená "Zobrazit mi nápovědy pro tento příkaz".</span><span class="sxs-lookup"><span data-stu-id="afd70-138">parameter with a Windows PowerShell cmdlet, it always means "show me Help for this command".</span></span> <span data-ttu-id="afd70-139">Vývojáři rutiny nemají analyzovat příkaz; Stačí, když se zadat text nápovědy.</span><span class="sxs-lookup"><span data-stu-id="afd70-139">Cmdlet developers do not have to parse the command; they only need to provide the Help text.</span></span>

<span data-ttu-id="afd70-140">Je důležité si uvědomit, že funkce nápovědy prostředí Windows PowerShell jsou k dispozici i v případě, že spustíte tradiční nástroje příkazového řádku v prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="afd70-140">It is important to understand that the Help features of Windows PowerShell are available even when you run traditional command-line tools in Windows PowerShell.</span></span> <span data-ttu-id="afd70-141">Prostředí Windows PowerShell zpracuje parametry a předá výsledky externí nástroje.</span><span class="sxs-lookup"><span data-stu-id="afd70-141">Windows PowerShell processes the parameters and passes the results to the external tools.</span></span>

> [!NOTE]
> <span data-ttu-id="afd70-142">Pokud spustíte grafické aplikace v prostředí Windows PowerShell, otevře se okno pro aplikaci.</span><span class="sxs-lookup"><span data-stu-id="afd70-142">If you run an graphic application in Windows PowerShell, the window for the application opens.</span></span> <span data-ttu-id="afd70-143">Prostředí Windows PowerShell zasáhla pouze při zpracování příkazového řádku zadejte můžete napájení nebo výstup aplikace do okna konzoly; nemá vliv interně fungování aplikace.</span><span class="sxs-lookup"><span data-stu-id="afd70-143">Windows PowerShell intervenes only when processing the command-line input you supply or the application output returned to the console window; it does not affect how the application works internally.</span></span>

### <a name="windows-powershell-uses-some-c-syntax"></a><span data-ttu-id="afd70-144">Prostředí Windows PowerShell používá některé syntaxe jazyka C#</span><span class="sxs-lookup"><span data-stu-id="afd70-144">Windows PowerShell Uses Some C# Syntax</span></span>
<span data-ttu-id="afd70-145">Prostředí Windows PowerShell má syntaxe funkce a klíčová slova, která jsou velmi podobné těm, které jsou v programovací jazyk, C# použít, protože prostředí Windows PowerShell je založena na rozhraní .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="afd70-145">Windows PowerShell has syntax features and keywords that are very similar to those used in the C# programming language, because Windows PowerShell is based on the .NET Framework.</span></span> <span data-ttu-id="afd70-146">Učení prostředí Windows PowerShell budou bylo mnohem snazší výuka C#, pokud vás zajímá v jazyce.</span><span class="sxs-lookup"><span data-stu-id="afd70-146">Learning Windows PowerShell will make it much easier to learn C#, if you are interested in the language.</span></span>

<span data-ttu-id="afd70-147">Pokud si nejste programování v C#, není tato podobnosti důležité.</span><span class="sxs-lookup"><span data-stu-id="afd70-147">If you are not a C# programmer, this similarity is not important.</span></span> <span data-ttu-id="afd70-148">Ale pokud jste již obeznámeni s C#, podobnost můžete nastavit učení mnohem jednodušší prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="afd70-148">However, if you are already familiar with C#, the similarities can make learning Windows PowerShell much easier.</span></span>
