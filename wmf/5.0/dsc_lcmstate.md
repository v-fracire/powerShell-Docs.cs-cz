---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: db9b48c188b3bfe2e20c06875606a285922f55a6
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
---
# <a name="detailed-information-about-lcm-state"></a><span data-ttu-id="86d16-102">Podrobné informace o stavu LCM</span><span class="sxs-lookup"><span data-stu-id="86d16-102">Detailed information about LCM state</span></span>

<span data-ttu-id="86d16-103">Provedli jsme vylepšení v vystavení údaje týkající se stavu LCM.</span><span class="sxs-lookup"><span data-stu-id="86d16-103">We have made improvements in exposing details about the LCM state.</span></span> <span data-ttu-id="86d16-104">LCMState, který je vrácen rutinou Get-DscLocalConfigurationManager teď může obsahovat následující hodnoty:</span><span class="sxs-lookup"><span data-stu-id="86d16-104">The LCMState that is returned by Get-DscLocalConfigurationManager can now contain the following values:</span></span>

* <span data-ttu-id="86d16-105">**Nečinnosti**</span><span class="sxs-lookup"><span data-stu-id="86d16-105">**Idle**</span></span>
* <span data-ttu-id="86d16-106">**Moc práce**</span><span class="sxs-lookup"><span data-stu-id="86d16-106">**Busy**</span></span>
* <span data-ttu-id="86d16-107">**PendingReboot**</span><span class="sxs-lookup"><span data-stu-id="86d16-107">**PendingReboot**</span></span>
* <span data-ttu-id="86d16-108">**PendingConfiguration**</span><span class="sxs-lookup"><span data-stu-id="86d16-108">**PendingConfiguration**</span></span>

<span data-ttu-id="86d16-109">Také jsme přidali ve vlastnosti LCMStateDetail, který obsahuje další informace o stavu.</span><span class="sxs-lookup"><span data-stu-id="86d16-109">We have also added an LCMStateDetail property that contains more information about the state.</span></span>
