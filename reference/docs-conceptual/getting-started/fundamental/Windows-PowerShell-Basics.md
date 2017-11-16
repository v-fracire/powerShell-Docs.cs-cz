---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Základy prostředí PowerShell systému Windows"
ms.assetid: 6b3cbbc8-060c-4877-b00b-7300dbbe4e28
ms.openlocfilehash: 7b5cdfce876aa7d5559fe772379829011b275a02
ms.sourcegitcommit: d6ab9ab5909ed59cce4ce30e29457e0e75c7ac12
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/08/2017
---
# <a name="windows-powershell-basics"></a><span data-ttu-id="ab878-103">Základy prostředí PowerShell systému Windows</span><span class="sxs-lookup"><span data-stu-id="ab878-103">Windows PowerShell Basics</span></span>
<span data-ttu-id="ab878-104">Grafické uživatelské rozhraní pomocí některé základní pojmy, které jsou dobře známé pro většinu uživatelů počítače.</span><span class="sxs-lookup"><span data-stu-id="ab878-104">Graphical user interfaces use some basic concepts that are well known to most computer users.</span></span> <span data-ttu-id="ab878-105">Uživatelé využívají znalosti těchto rozhraní k provádění úloh.</span><span class="sxs-lookup"><span data-stu-id="ab878-105">Users rely on the familiarity of those interfaces to accomplish tasks.</span></span> <span data-ttu-id="ab878-106">Operační systémy představovat grafické reprezentace položky, které mohou procházet, obvykle pomocí rozevíracích nabídek pro přístup k určité funkce a kontext nabídky pro přístup k funkci konkrétní uživatelé.</span><span class="sxs-lookup"><span data-stu-id="ab878-106">Operating systems present users with a graphical representation of items that can be browsed, usually with drop-down menus for accessing specific functionality and context menus for accessing context-specific functionality.</span></span>

<span data-ttu-id="ab878-107">Rozhraní příkazového řádku (CLI), jako je Windows PowerShell, musíte použít jiný přístup ke zveřejnění informací, protože nemá nabídek nebo grafické systémy pomoct uživateli.</span><span class="sxs-lookup"><span data-stu-id="ab878-107">A command-line interface (CLI), such as Windows PowerShell, must use a different approach to expose information, because it does not have menus or graphical systems to help the user.</span></span> <span data-ttu-id="ab878-108">Musíte znát názvy příkazů, abyste mohli používat.</span><span class="sxs-lookup"><span data-stu-id="ab878-108">You need to know command names before you can use them.</span></span> <span data-ttu-id="ab878-109">I když můžete zadat komplexní příkazy, které odpovídají funkcí v prostředí s grafickým uživatelským rozhraním, musí seznámit s běžně používané příkazy a parametry příkazu.</span><span class="sxs-lookup"><span data-stu-id="ab878-109">Although you can type complex commands that are equivalent to the features in a GUI environment, you must become familiar with commonly-used commands and command parameters.</span></span>

<span data-ttu-id="ab878-110">Většina CLIs nemají vzorů, které pomáhají uživatelům další rozhraní.</span><span class="sxs-lookup"><span data-stu-id="ab878-110">Most CLIs do not have patterns that can help the user to learn the interface.</span></span> <span data-ttu-id="ab878-111">Protože CLIs byly první součásti pro operační systém, mnoha názvy příkazů a názvy parametrů nebyly vybrány libovolně.</span><span class="sxs-lookup"><span data-stu-id="ab878-111">Because CLIs were the first operating system shells, many command names and parameter names were selected arbitrarily.</span></span> <span data-ttu-id="ab878-112">Názvy ve formátu Terse zasílaná příkazů obecně členové přes vymazat některé ze stávajících.</span><span class="sxs-lookup"><span data-stu-id="ab878-112">Terse command names were generally chosen over clear ones.</span></span> <span data-ttu-id="ab878-113">I když systémů nápovědy a příkaz návrhu standardy jsou integrovány většina CLIs, budou mít byla obecně navržené pro kompatibilitu s nejdřívější příkazy, tak sadu příkazů nástroje ve rozhodnutí desetiletí před stále tvaru.</span><span class="sxs-lookup"><span data-stu-id="ab878-113">Although help systems and command design standards are integrated into most CLIs, they have been generally designed for compatibility with the earliest commands, so the command set is still shaped by decisions made decades ago.</span></span>

<span data-ttu-id="ab878-114">Prostředí Windows PowerShell byla navržená tak, že chcete využít výhod historické znalosti CLIs uživatele.</span><span class="sxs-lookup"><span data-stu-id="ab878-114">Windows PowerShell was designed to take advantage of a user's historic knowledge of CLIs.</span></span> <span data-ttu-id="ab878-115">V této kapitole se věnuje některé základní nástroje a koncepty, které vám pomůže rychle další prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ab878-115">In this chapter, we will talk about some basic tools and concepts that you can use to learn Windows PowerShell quickly.</span></span> <span data-ttu-id="ab878-116">Patří mezi ně:</span><span class="sxs-lookup"><span data-stu-id="ab878-116">They include:</span></span>

- <span data-ttu-id="ab878-117">Pomocí příkazu Get</span><span class="sxs-lookup"><span data-stu-id="ab878-117">Using Get-Command</span></span>

- <span data-ttu-id="ab878-118">Pomocí příkazů Cmd.exe a UNIX</span><span class="sxs-lookup"><span data-stu-id="ab878-118">Using Cmd.exe and UNIX commands</span></span>

- <span data-ttu-id="ab878-119">Pomocí externích příkazů</span><span class="sxs-lookup"><span data-stu-id="ab878-119">Using External Commands</span></span>

- <span data-ttu-id="ab878-120">Pomocí karty dokončení</span><span class="sxs-lookup"><span data-stu-id="ab878-120">Using Tab-Completion</span></span>

- <span data-ttu-id="ab878-121">Pomocí Get-Help</span><span class="sxs-lookup"><span data-stu-id="ab878-121">Using Get-Help</span></span>

