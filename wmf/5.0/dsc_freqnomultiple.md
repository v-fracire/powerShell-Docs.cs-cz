---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: a3ac215396206fba62bce303733429d60722ee6b
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
---
# <a name="frequencies-for-refreshmode-and-configurationmode-dont-need-to-be-multiples-of-each-other"></a>Frekvence RefreshMode a ConfigurationMode nemusí být násobky vzájemně

V předchozí verzi DSC, LCM zacházeli `RefreshFrequencyMins` a `ConfigurationModeFrequencyMins` jako násobky navzájem. V WMF 5.0 RTM jsou zpracovávány tyto vlastnosti navzájem nezávislé.

Další informace najdete v tématu [konfigurace správce místní konfigurace](https://msdn.microsoft.com/powershell/dsc/metaconfig).
