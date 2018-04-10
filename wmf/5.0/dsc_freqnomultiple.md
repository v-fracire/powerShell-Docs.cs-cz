---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: e1faf71436c8ba0ae02a166ce06d03de9f66f094
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="frequencies-for-refreshmode-and-configurationmode-dont-need-to-be-multiples-of-each-other"></a><span data-ttu-id="17999-102">Frekvence RefreshMode a ConfigurationMode nemusí být násobky vzájemně</span><span class="sxs-lookup"><span data-stu-id="17999-102">Frequencies for RefreshMode and ConfigurationMode don't need to be multiples of each other</span></span>

<span data-ttu-id="17999-103">V předchozí verzi DSC, LCM zacházeli `RefreshFrequencyMins` a `ConfigurationModeFrequencyMins` jako násobky navzájem.</span><span class="sxs-lookup"><span data-stu-id="17999-103">In the previous version of DSC, the LCM would treat `RefreshFrequencyMins` and `ConfigurationModeFrequencyMins` as multiples of each other.</span></span> <span data-ttu-id="17999-104">V WMF 5.0 RTM jsou zpracovávány tyto vlastnosti navzájem nezávislé.</span><span class="sxs-lookup"><span data-stu-id="17999-104">In WMF 5.0 RTM, these properties are processed independent of each other.</span></span>

<span data-ttu-id="17999-105">Další informace najdete v tématu [konfigurace správce místní konfigurace](https://msdn.microsoft.com/powershell/dsc/metaconfig).</span><span class="sxs-lookup"><span data-stu-id="17999-105">For more information, see [Configuring the Local Configuration Manager](https://msdn.microsoft.com/powershell/dsc/metaconfig).</span></span>