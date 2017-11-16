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
# <a name="detailed-information-about-lcm-state"></a>Podrobné informace o stavu LCM

Provedli jsme vylepšení v vystavení údaje týkající se stavu LCM. LCMState, který je vrácen rutinou Get-DscLocalConfigurationManager teď může obsahovat následující hodnoty:

* **Nečinnosti**
* **Moc práce**
* **PendingReboot**
* **PendingConfiguration**

Také jsme přidali ve vlastnosti LCMStateDetail, který obsahuje další informace o stavu.

