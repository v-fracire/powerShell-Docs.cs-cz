---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: db9b48c188b3bfe2e20c06875606a285922f55a6
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
ms.locfileid: "34219857"
---
# <a name="detailed-information-about-lcm-state"></a>Podrobné informace o stavu LCM

Provedli jsme vylepšení v vystavení údaje týkající se stavu LCM. LCMState, který je vrácen rutinou Get-DscLocalConfigurationManager teď může obsahovat následující hodnoty:

* **Nečinnosti**
* **Moc práce**
* **PendingReboot**
* **PendingConfiguration**

Také jsme přidali ve vlastnosti LCMStateDetail, který obsahuje další informace o stavu.
