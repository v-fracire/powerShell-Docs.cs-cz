---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
ms.openlocfilehash: 4fc146f84588d368ac3eb819e3acb4cb8c5d8793
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="detailed-information-about-lcm-state"></a><span data-ttu-id="cf6ab-102">Podrobné informace o stavu LCM</span><span class="sxs-lookup"><span data-stu-id="cf6ab-102">Detailed information about LCM state</span></span>

<span data-ttu-id="cf6ab-103">Provedli jsme vylepšení v vystavení údaje týkající se stavu LCM.</span><span class="sxs-lookup"><span data-stu-id="cf6ab-103">We have made improvements in exposing details about the LCM state.</span></span> <span data-ttu-id="cf6ab-104">LCMState, který je vrácen rutinou Get-DscLocalConfigurationManager teď může obsahovat následující hodnoty:</span><span class="sxs-lookup"><span data-stu-id="cf6ab-104">The LCMState that is returned by Get-DscLocalConfigurationManager can now contain the following values:</span></span>

* <span data-ttu-id="cf6ab-105">**Nečinnosti**</span><span class="sxs-lookup"><span data-stu-id="cf6ab-105">**Idle**</span></span>
* <span data-ttu-id="cf6ab-106">**Moc práce**</span><span class="sxs-lookup"><span data-stu-id="cf6ab-106">**Busy**</span></span>
* <span data-ttu-id="cf6ab-107">**PendingReboot**</span><span class="sxs-lookup"><span data-stu-id="cf6ab-107">**PendingReboot**</span></span>
* <span data-ttu-id="cf6ab-108">**PendingConfiguration**</span><span class="sxs-lookup"><span data-stu-id="cf6ab-108">**PendingConfiguration**</span></span>

<span data-ttu-id="cf6ab-109">Také jsme přidali ve vlastnosti LCMStateDetail, který obsahuje další informace o stavu.</span><span class="sxs-lookup"><span data-stu-id="cf6ab-109">We have also added an LCMStateDetail property that contains more information about the state.</span></span>

