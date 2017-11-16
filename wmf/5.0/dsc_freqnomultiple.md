---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
ms.openlocfilehash: 30055cff87159df98029e25409782e0fe2f0bae4
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="frequencies-for-refreshmode-and-configurationmode-dont-need-to-be-multiples-of-each-other"></a><span data-ttu-id="fbf1d-102">Frekvence RefreshMode a ConfigurationMode nemusí být násobky vzájemně</span><span class="sxs-lookup"><span data-stu-id="fbf1d-102">Frequencies for RefreshMode and ConfigurationMode don't need to be multiples of each other</span></span>

<span data-ttu-id="fbf1d-103">V předchozí verzi DSC, LCM zacházeli `RefreshFrequencyMins` a `ConfigurationModeFrequencyMins` jako násobky navzájem.</span><span class="sxs-lookup"><span data-stu-id="fbf1d-103">In the previous version of DSC, the LCM would treat `RefreshFrequencyMins` and `ConfigurationModeFrequencyMins` as multiples of each other.</span></span> <span data-ttu-id="fbf1d-104">V WMF 5.0 RTM jsou zpracovávány tyto vlastnosti navzájem nezávislé.</span><span class="sxs-lookup"><span data-stu-id="fbf1d-104">In WMF 5.0 RTM, these properties are processed independent of each other.</span></span> 

<span data-ttu-id="fbf1d-105">Další informace najdete v tématu [konfigurace správce místní konfigurace](https://msdn.microsoft.com/powershell/dsc/metaconfig).</span><span class="sxs-lookup"><span data-stu-id="fbf1d-105">For more information, see [Configuring the Local Configuration Manager](https://msdn.microsoft.com/powershell/dsc/metaconfig).</span></span>

