---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Začínáme s Windows PowerShellem
ms.assetid: b0e2ad92-875f-421d-b612-f624e644aa69
ms.openlocfilehash: d8f1a416c1618040311ec0ea3b98b28aa432bcf1
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
ms.locfileid: "30949481"
---
# <a name="getting-started-with-windows-powershell"></a><span data-ttu-id="4f172-103">Začínáme s Windows PowerShellem</span><span class="sxs-lookup"><span data-stu-id="4f172-103">Getting Started with Windows PowerShell</span></span>
<span data-ttu-id="4f172-104">Prostředí Windows PowerShell je prostředí příkazového řádku Windows, který je určený pro správce systému.</span><span class="sxs-lookup"><span data-stu-id="4f172-104">Windows PowerShell is a Windows command-line shell designed especially for system administrators.</span></span> <span data-ttu-id="4f172-105">Prostředí Windows PowerShell obsahuje interaktivní řádku a skriptovací prostředí, které můžete použít samostatně nebo v kombinaci.</span><span class="sxs-lookup"><span data-stu-id="4f172-105">Windows PowerShell includes an interactive prompt and a scripting environment that can be used independently or in combination.</span></span>

<span data-ttu-id="4f172-106">Na rozdíl od většiny shells aplikací, které přijmout a vrací text, prostředí Windows PowerShell je postavená na rozhraní .NET Framework common language runtime (CLR) a rozhraní .NET Framework a přijímá a vrátí objekty rozhraní .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="4f172-106">Unlike most shells, which accept and return text, Windows PowerShell is built on top of the .NET Framework common language runtime (CLR) and the .NET Framework, and accepts and returns .NET Framework objects.</span></span> <span data-ttu-id="4f172-107">Tato základní změna v prostředí přináší zcela nové nástroje a metody pro správu a konfiguraci systému Windows.</span><span class="sxs-lookup"><span data-stu-id="4f172-107">This fundamental change in the environment brings entirely new tools and methods to the management and configuration of Windows.</span></span>

<span data-ttu-id="4f172-108">Prostředí Windows PowerShell zavádí koncepci rutiny (vyslovováno "příkazu – umožňují"), jednoduché, jedinou funkcí nástroje příkazového řádku integrovaný do prostředí.</span><span class="sxs-lookup"><span data-stu-id="4f172-108">Windows PowerShell introduces the concept of a cmdlet (pronounced "command-let"), a simple, single-function command-line tool built into the shell.</span></span> <span data-ttu-id="4f172-109">Každou rutinu můžete použít samostatně, ale jejich power je dosaženo pomocí těchto nástrojů jednoduché v kombinaci komplexní úkoly.</span><span class="sxs-lookup"><span data-stu-id="4f172-109">You can use each cmdlet separately, but their power is realized when you use these simple tools in combination to perform complex tasks.</span></span> <span data-ttu-id="4f172-110">Prostředí Windows PowerShell obsahuje víc než sto rutin jader na úrovni basic a můžete napsat vlastní rutiny a sdílet je s ostatními uživateli.</span><span class="sxs-lookup"><span data-stu-id="4f172-110">Windows PowerShell includes more than one hundred basic core cmdlets, and you can write your own cmdlets and share them with other users.</span></span>

<span data-ttu-id="4f172-111">Například mnoho nutný prostředí Windows PowerShell umožňuje přístup k systému souborů v počítači.</span><span class="sxs-lookup"><span data-stu-id="4f172-111">Like many shells, Windows PowerShell gives you access to the file system on the computer.</span></span> <span data-ttu-id="4f172-112">Kromě toho, prostředí Windows PowerShell *zprostředkovatelé* vám umožní přístup k jiným úložištím dat, jako je například registr a úložiště certifikátů digitální podpis, snadno přístup systému souborů.</span><span class="sxs-lookup"><span data-stu-id="4f172-112">In addition, Windows PowerShell *providers* enable you to access other data stores, such as the registry and the digital signature certificate stores, as easily as you access the file system.</span></span>

<span data-ttu-id="4f172-113">Tato příručka Začínáme obsahuje úvod do prostředí Windows PowerShell: jazyk, rutiny, zprostředkovatele a použití objektů.</span><span class="sxs-lookup"><span data-stu-id="4f172-113">This Getting Started guide provides an introduction to Windows PowerShell: the language, the cmdlets, the providers, and the use of objects.</span></span>

<span data-ttu-id="4f172-114">V tomto tématu:</span><span class="sxs-lookup"><span data-stu-id="4f172-114">In this topic:</span></span>

- [<span data-ttu-id="4f172-115">Požadavky na prostředí PowerShell systému Windows</span><span class="sxs-lookup"><span data-stu-id="4f172-115">Windows PowerShell System Requirements</span></span>](../setup/Windows-PowerShell-System-Requirements.md)

- [<span data-ttu-id="4f172-116">Instalace prostředí Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="4f172-116">Installing Windows PowerShell</span></span>](../setup/Installing-Windows-PowerShell.md)

- [<span data-ttu-id="4f172-117">Spuštění prostředí Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="4f172-117">Starting Windows PowerShell</span></span>](../setup/Starting-Windows-PowerShell.md)

- [<span data-ttu-id="4f172-118">Probíhá příprava pomocí prostředí Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="4f172-118">Getting Ready to Use Windows PowerShell</span></span>](Getting-Ready-to-Use-Windows-PowerShell.md)