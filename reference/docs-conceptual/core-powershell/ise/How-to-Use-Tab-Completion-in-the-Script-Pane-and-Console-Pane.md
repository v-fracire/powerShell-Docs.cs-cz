---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Použití klávesy Tab k dokončování příkazů ve skriptovacím podokně a v podokně konzoly
ms.assetid: 3b752c3c-0bd0-4eca-a2d3-2d5a37fd9d84
ms.openlocfilehash: 24a3f00987ff5ca4bf82d1a3206857ec3c4b3f09
ms.sourcegitcommit: 6749f67c32e05999e10deb9d45f90f45ac21a599
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/08/2018
ms.locfileid: "48851131"
---
# <a name="how-to-use-tab-completion-in-the-script-pane-and-console-pane"></a><span data-ttu-id="0a160-103">Použití klávesy Tab k dokončování příkazů ve skriptovacím podokně a v podokně konzoly</span><span class="sxs-lookup"><span data-stu-id="0a160-103">How to Use Tab Completion in the Script Pane and Console Pane</span></span>

<span data-ttu-id="0a160-104">Dokončování pomocí tabulátoru poskytuje automatické Nápověda při zadávání v podokně se skriptem nebo v příkazovém podokně.</span><span class="sxs-lookup"><span data-stu-id="0a160-104">Tab completion provides automatic help when you are typing in the Script Pane or in the Command Pane.</span></span> <span data-ttu-id="0a160-105">Abyste mohli využít tuto funkci, postupujte následovně:</span><span class="sxs-lookup"><span data-stu-id="0a160-105">Use the following steps to take advantage of this feature:</span></span>

## <a name="to-automatically-complete-a-command-entry"></a><span data-ttu-id="0a160-106">Automatické dokončení položky příkazu</span><span class="sxs-lookup"><span data-stu-id="0a160-106">To automatically complete a command entry</span></span>

<span data-ttu-id="0a160-107">V okně příkazu nebo skriptu zadejte několik znaků příkaz a dvakrát stiskněte klávesu TAB k výběru požadované dokončování textu.</span><span class="sxs-lookup"><span data-stu-id="0a160-107">In the Command Pane or Script Pane, type a few characters of a command and then press TAB to select the desired completion text.</span></span> <span data-ttu-id="0a160-108">Pokud více položek začíná zadaným textem, který jste původně zadali a pak pokračujte stisknutím klávesy Tab, dokud nenajdete položku, kterou chcete.</span><span class="sxs-lookup"><span data-stu-id="0a160-108">If multiple items begin with the text that you initially typed, then continue pressing Tab until the item you want appears.</span></span> <span data-ttu-id="0a160-109">TAB k dokončování příkazů může pomoct tak, že napíšete název rutiny, název parametru, název proměnné, název vlastnosti objektu nebo cestu k souboru.</span><span class="sxs-lookup"><span data-stu-id="0a160-109">Tab completion can help with typing a cmdlet name, parameter name, variable name, object property name, or a file path.</span></span>

> [!NOTE]
> <span data-ttu-id="0a160-110">V podokně se skriptem klávesy TAB automaticky dokončí příkaz pouze při úpravách .ps1, .psd1 nebo soubory .psm1.</span><span class="sxs-lookup"><span data-stu-id="0a160-110">In the Script Pane, pressing TAB will automatically complete a command only when you are editing .ps1, .psd1, or .psm1 files.</span></span> <span data-ttu-id="0a160-111">Dokončování pomocí tabulátoru funguje kdykoli, když píšete v příkazovém podokně.</span><span class="sxs-lookup"><span data-stu-id="0a160-111">Tab completion works any time when you are typing in the Command Pane.</span></span>

## <a name="to-automatically-complete-a-cmdlet-parameter-entry"></a><span data-ttu-id="0a160-112">Automatické dokončení vstupní parametr rutiny</span><span class="sxs-lookup"><span data-stu-id="0a160-112">To automatically complete a cmdlet parameter entry</span></span>

<span data-ttu-id="0a160-113">V podokně podokna příkazu nebo skriptu zadejte rutinu, za nímž následuje pomlčka a dvakrát stiskněte klávesu TAB.</span><span class="sxs-lookup"><span data-stu-id="0a160-113">In the Command Pane or Script pane, type a cmdlet followed by a dash and then press TAB.</span></span>

<span data-ttu-id="0a160-114">Zadejte například `Get-Process -` a stiskněte klávesu TAB více než jednou pro každý z parametrů pro rutinu zase zobrazení.</span><span class="sxs-lookup"><span data-stu-id="0a160-114">For example, type `Get-Process -` and then press TAB multiple times to display each of the parameters for the cmdlet in turn.</span></span>

## <a name="see-also"></a><span data-ttu-id="0a160-115">Viz také</span><span class="sxs-lookup"><span data-stu-id="0a160-115">See Also</span></span>

- [<span data-ttu-id="0a160-116">Představení Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="0a160-116">Introducing the Windows PowerShell ISE</span></span>](Introducing-the-Windows-PowerShell-ISE.md)
- [<span data-ttu-id="0a160-117">Vytvoření karty Powershellu</span><span class="sxs-lookup"><span data-stu-id="0a160-117">How to Create a PowerShell Tab</span></span>](How-to-Create-a-PowerShell-Tab-in-Windows-PowerShell-ISE.md)
