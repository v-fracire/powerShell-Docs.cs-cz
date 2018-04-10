---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: baa35e9acd24d6f6155acf617a0d2c2210742af7
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="detailed-information-about-lcm-state"></a><span data-ttu-id="3920d-102">Podrobné informace o stavu LCM</span><span class="sxs-lookup"><span data-stu-id="3920d-102">Detailed information about LCM state</span></span>

<span data-ttu-id="3920d-103">Provedli jsme vylepšení v vystavení údaje týkající se stavu LCM.</span><span class="sxs-lookup"><span data-stu-id="3920d-103">We have made improvements in exposing details about the LCM state.</span></span> <span data-ttu-id="3920d-104">LCMState, který je vrácen rutinou Get-DscLocalConfigurationManager teď může obsahovat následující hodnoty:</span><span class="sxs-lookup"><span data-stu-id="3920d-104">The LCMState that is returned by Get-DscLocalConfigurationManager can now contain the following values:</span></span>

* <span data-ttu-id="3920d-105">**Nečinnosti**</span><span class="sxs-lookup"><span data-stu-id="3920d-105">**Idle**</span></span>
* <span data-ttu-id="3920d-106">**Moc práce**</span><span class="sxs-lookup"><span data-stu-id="3920d-106">**Busy**</span></span>
* <span data-ttu-id="3920d-107">**PendingReboot**</span><span class="sxs-lookup"><span data-stu-id="3920d-107">**PendingReboot**</span></span>
* <span data-ttu-id="3920d-108">**PendingConfiguration**</span><span class="sxs-lookup"><span data-stu-id="3920d-108">**PendingConfiguration**</span></span>

<span data-ttu-id="3920d-109">Také jsme přidali ve vlastnosti LCMStateDetail, který obsahuje další informace o stavu.</span><span class="sxs-lookup"><span data-stu-id="3920d-109">We have also added an LCMStateDetail property that contains more information about the state.</span></span>