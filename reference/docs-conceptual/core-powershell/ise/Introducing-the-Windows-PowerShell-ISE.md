---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Představení Windows PowerShell ISE"
ms.openlocfilehash: 75242c20548e2e83397867214417a48806c897ec
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/08/2017
---
# <a name="introducing-the-windows-powershell-ise"></a><span data-ttu-id="3c101-103">Představení Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="3c101-103">Introducing the Windows PowerShell ISE</span></span>
<span data-ttu-id="3c101-104">Systému Windows PowerShell Integrované skriptovací prostředí (ISE) je hostitelskou aplikaci pro Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3c101-104">The Windows PowerShell Integrated Scripting Environment (ISE) is a host application for Windows PowerShell.</span></span> <span data-ttu-id="3c101-105">V systému Windows PowerShell ISE můžete spustit příkazy a zápisu, test a ladění skriptů v jednom systému Windows grafické uživatelské rozhraní pomocí víceřádkovým úpravy, dokončování pomocí tabulátorů, barevné zvýrazňování syntaxe, selektivní provádění, Kontextová nápověda a podpora pro jazyky zprava doleva.</span><span class="sxs-lookup"><span data-stu-id="3c101-105">In Windows PowerShell ISE, you can run commands and write, test, and debug scripts in a single Windows-based graphic user interface with multiline editing, tab completion, syntax coloring, selective execution, context-sensitive help, and support for right-to-left languages.</span></span>
<span data-ttu-id="3c101-106">Položky nabídky a klávesové zkratky můžete provádět mnoho úloh, které můžete provést v konzole Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3c101-106">You can use menu items and keyboard shortcuts to perform many of the same tasks that you would perform in the Windows PowerShell console.</span></span>  <span data-ttu-id="3c101-107">Například při ladění skript v systému Windows PowerShell ISE k nastavení boru přerušení řádku ve skriptu, klikněte pravým tlačítkem myši na řádek kódu a pak klikněte na tlačítko **Přepnout zarážku**.</span><span class="sxs-lookup"><span data-stu-id="3c101-107">For example, when you debug a script in the Windows PowerShell ISE, to set a line breakpoint in a script, right-click the line of code, and then click **Toggle Breakpoint**.</span></span>

<span data-ttu-id="3c101-108">Zkuste tyto funkce v systému Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="3c101-108">Try these features in Windows PowerShell ISE.</span></span>

- <span data-ttu-id="3c101-109">Víceřádkové úpravy: Chcete-li vložit prázdný řádek v rámci aktuálního řádku podokna příkazu stiskněte SHIFT + ENTER.</span><span class="sxs-lookup"><span data-stu-id="3c101-109">Multiline editing: To insert a blank line under the current line in the Command pane, press SHIFT+ENTER.</span></span>

- <span data-ttu-id="3c101-110">Selektivní provádění: součástí skript spustit, vyberte text, který chcete spustit a potom klikněte na **spustit skript** tlačítko.</span><span class="sxs-lookup"><span data-stu-id="3c101-110">Selective execution: To run part of a script, select the text you want to run, and then click the **Run Script** button.</span></span> <span data-ttu-id="3c101-111">Nebo stiskněte klávesu F5.</span><span class="sxs-lookup"><span data-stu-id="3c101-111">Or, press F5.</span></span>

- <span data-ttu-id="3c101-112">Kontextová nápověda: typ **Invoke-Item**, a potom stiskněte klávesu F1.</span><span class="sxs-lookup"><span data-stu-id="3c101-112">Context-sensitive help: Type **Invoke-Item**, and then press F1.</span></span> <span data-ttu-id="3c101-113">Téma nápovědy pro otevření souboru nápovědy **Invoke-Item** rutiny.</span><span class="sxs-lookup"><span data-stu-id="3c101-113">The Help file opens to the Help topic for the **Invoke-Item** cmdlet.</span></span>

<span data-ttu-id="3c101-114">Windows PowerShell ISE umožňuje přizpůsobit některé aspekty její vzhled.</span><span class="sxs-lookup"><span data-stu-id="3c101-114">The Windows PowerShell ISE lets you customize some aspects of its appearance.</span></span> <span data-ttu-id="3c101-115">Je také vlastní profil prostředí Windows PowerShell, kam můžete ukládat funkcí, aliasy, proměnné a příkazy, které používáte v systému Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="3c101-115">It also has its own Windows PowerShell profile, where you can store functions, aliases, variables, and commands you use in the Windows PowerShell ISE.</span></span>

### <a name="to-start-the-windows-powershell-ise"></a><span data-ttu-id="3c101-116">Spusťte Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="3c101-116">To start the Windows PowerShell ISE</span></span>

1. <span data-ttu-id="3c101-117">Udělejte jednu z těchto věcí:</span><span class="sxs-lookup"><span data-stu-id="3c101-117">Do one of the following:</span></span>

    -   <span data-ttu-id="3c101-118">Klikněte na tlačítko **spustit**, přejděte na příkaz **všechny programy**, přejděte na příkaz **Windows PowerShell V2**a potom klikněte na **Windows PowerShell ISE**.</span><span class="sxs-lookup"><span data-stu-id="3c101-118">Click **Start**, point to **All Programs**, point to **Windows PowerShell V2**, and then click **Windows PowerShell ISE**.</span></span>

    -   <span data-ttu-id="3c101-119">V konzole Windows PowerShell Cmd.exe nebo v poli Spustit typu **powershell_ise.exe**.</span><span class="sxs-lookup"><span data-stu-id="3c101-119">In the Windows PowerShell console Cmd.exe, or in the Run box, type, **powershell_ise.exe**.</span></span>

### <a name="to-get-help-in-the-windows-powershell-ise"></a><span data-ttu-id="3c101-120">Jak získat nápovědu v systému Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="3c101-120">To get Help in the Windows PowerShell ISE</span></span>

- <span data-ttu-id="3c101-121">Na **pomoci** nabídky, klikněte na tlačítko **nápovědy prostředí Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="3c101-121">On the **Help** menu, click **Windows PowerShell Help**.</span></span> <span data-ttu-id="3c101-122">Nebo stisknete klávesu F1.</span><span class="sxs-lookup"><span data-stu-id="3c101-122">Or, press F1.</span></span> <span data-ttu-id="3c101-123">Soubor, který otevírá popisuje Windows PowerShell ISE a prostředí Windows PowerShell, včetně všech objektů v nápovědě k dispozici z rutiny Get-Help.</span><span class="sxs-lookup"><span data-stu-id="3c101-123">The file that opens describes Windows PowerShell ISE and Windows PowerShell, including all of the help available from the Get-Help cmdlet.</span></span>

