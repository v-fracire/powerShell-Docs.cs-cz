---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: a3ac215396206fba62bce303733429d60722ee6b
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
---
# <a name="frequencies-for-refreshmode-and-configurationmode-dont-need-to-be-multiples-of-each-other"></a><span data-ttu-id="df192-102">Frekvence RefreshMode a ConfigurationMode nemusí být násobky vzájemně</span><span class="sxs-lookup"><span data-stu-id="df192-102">Frequencies for RefreshMode and ConfigurationMode don't need to be multiples of each other</span></span>

<span data-ttu-id="df192-103">V předchozí verzi DSC, LCM zacházeli `RefreshFrequencyMins` a `ConfigurationModeFrequencyMins` jako násobky navzájem.</span><span class="sxs-lookup"><span data-stu-id="df192-103">In the previous version of DSC, the LCM would treat `RefreshFrequencyMins` and `ConfigurationModeFrequencyMins` as multiples of each other.</span></span> <span data-ttu-id="df192-104">V WMF 5.0 RTM jsou zpracovávány tyto vlastnosti navzájem nezávislé.</span><span class="sxs-lookup"><span data-stu-id="df192-104">In WMF 5.0 RTM, these properties are processed independent of each other.</span></span>

<span data-ttu-id="df192-105">Další informace najdete v tématu [konfigurace správce místní konfigurace](https://msdn.microsoft.com/powershell/dsc/metaconfig).</span><span class="sxs-lookup"><span data-stu-id="df192-105">For more information, see [Configuring the Local Configuration Manager](https://msdn.microsoft.com/powershell/dsc/metaconfig).</span></span>
