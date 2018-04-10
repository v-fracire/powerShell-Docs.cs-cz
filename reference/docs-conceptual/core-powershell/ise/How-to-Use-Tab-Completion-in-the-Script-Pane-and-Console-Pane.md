---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Použití klávesy Tab k dokončování příkazů ve skriptovacím podokně a v podokně konzoly
ms.assetid: 3b752c3c-0bd0-4eca-a2d3-2d5a37fd9d84
ms.openlocfilehash: e1f8146b6113a82fd3d857c98550ec2e459715a4
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="how-to-use-tab-completion-in-the-script-pane-and-console-pane"></a><span data-ttu-id="12b85-103">Použití klávesy Tab k dokončování příkazů ve skriptovacím podokně a v podokně konzoly</span><span class="sxs-lookup"><span data-stu-id="12b85-103">How to Use Tab Completion in the Script Pane and Console Pane</span></span>

<span data-ttu-id="12b85-104">Dokončování pomocí tabulátorů poskytuje automatickou pomoc při psaní v podokně skriptu nebo v podokně příkaz.</span><span class="sxs-lookup"><span data-stu-id="12b85-104">Tab completion provides automatic help when you are typing in the Script Pane or in the Command Pane.</span></span> <span data-ttu-id="12b85-105">Pokud chcete využít výhod tuto funkci použijte následující postup:</span><span class="sxs-lookup"><span data-stu-id="12b85-105">Use the following steps to take advantage of this feature:</span></span>

## <a name="to-automatically-complete-a-command-entry"></a><span data-ttu-id="12b85-106">K dokončení automaticky zadání příkazu</span><span class="sxs-lookup"><span data-stu-id="12b85-106">To automatically complete a command entry</span></span>

<span data-ttu-id="12b85-107">V okně příkazu nebo skriptu zadejte pár znaků příkaz a stiskněte klávesu TAB vyberte požadovanou dokončení text.</span><span class="sxs-lookup"><span data-stu-id="12b85-107">In the Command Pane or Script Pane, type a few characters of a command and then press TAB to select the desired completion text.</span></span> <span data-ttu-id="12b85-108">Více položek začínat text, který jste původně zadali, pokračujte stisknutím klávesy Tab, dokud se nezobrazí položku, kterou chcete.</span><span class="sxs-lookup"><span data-stu-id="12b85-108">If multiple items begin with the text that you initially typed, then continue pressing Tab until the item you want appears.</span></span> <span data-ttu-id="12b85-109">Dokončování pomocí tabulátorů může pomoct s zadáte název rutiny, název parametru, název proměnné, název vlastnosti objektu nebo cestu k souboru.</span><span class="sxs-lookup"><span data-stu-id="12b85-109">Tab completion can help with typing a cmdlet name, parameter name, variable name, object property name, or a file path.</span></span>

> [!NOTE]
> <span data-ttu-id="12b85-110">V podokně skriptu stisknutím klávesy TAB automaticky dokončí příkaz jenom v případě, že jsou úpravy, .ps1, .psd1 nebo soubory .psm1.</span><span class="sxs-lookup"><span data-stu-id="12b85-110">In the Script Pane, pressing TAB will automatically complete a command only when you are editing .ps1, .psd1, or .psm1 files.</span></span> <span data-ttu-id="12b85-111">Dokončování pomocí tabulátorů funguje kdykoli, kdy text v podokně příkaz.</span><span class="sxs-lookup"><span data-stu-id="12b85-111">Tab completion works any time when you are typing in the Command Pane.</span></span>

## <a name="to-automatically-complete-a-cmdlet-parameter-entry"></a><span data-ttu-id="12b85-112">Chcete-li automaticky dokončení zadání parametru rutiny</span><span class="sxs-lookup"><span data-stu-id="12b85-112">To automatically complete a cmdlet parameter entry</span></span>

<span data-ttu-id="12b85-113">V podokně podokně příkaz nebo skript zadejte rutiny následované pomlčkou a potom stiskněte klávesu TAB.</span><span class="sxs-lookup"><span data-stu-id="12b85-113">In the Command Pane or Script pane, type a cmdlet followed by a dash, and then press TAB.</span></span>

<span data-ttu-id="12b85-114">Můžete například zadat `Get-Process -` a stiskněte klávesu TAB více než jednou pro každou z parametrů poskytnutých rutině zase zobrazení.</span><span class="sxs-lookup"><span data-stu-id="12b85-114">For example, type `Get-Process -` and then press TAB multiple times to display each of the parameters for the cmdlet in turn.</span></span>

## <a name="see-also"></a><span data-ttu-id="12b85-115">Viz také</span><span class="sxs-lookup"><span data-stu-id="12b85-115">See Also</span></span>

- [<span data-ttu-id="12b85-116">Představení Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="12b85-116">Introducing the Windows PowerShell ISE</span></span>](Introducing-the-Windows-PowerShell-ISE.md)
- [<span data-ttu-id="12b85-117">Postup vytvoření karty prostředí PowerShell</span><span class="sxs-lookup"><span data-stu-id="12b85-117">How to Create a PowerShell Tab</span></span>](How-to-Create-a-PowerShell-Tab-in-Windows-PowerShell-ISE.md)