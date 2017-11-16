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
# <a name="frequencies-for-refreshmode-and-configurationmode-dont-need-to-be-multiples-of-each-other"></a>Frekvence RefreshMode a ConfigurationMode nemusí být násobky vzájemně

V předchozí verzi DSC, LCM zacházeli `RefreshFrequencyMins` a `ConfigurationModeFrequencyMins` jako násobky navzájem. V WMF 5.0 RTM jsou zpracovávány tyto vlastnosti navzájem nezávislé. 

Další informace najdete v tématu [konfigurace správce místní konfigurace](https://msdn.microsoft.com/powershell/dsc/metaconfig).

