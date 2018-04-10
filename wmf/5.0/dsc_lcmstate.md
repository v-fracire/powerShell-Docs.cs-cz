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
# <a name="detailed-information-about-lcm-state"></a>Podrobné informace o stavu LCM

Provedli jsme vylepšení v vystavení údaje týkající se stavu LCM. LCMState, který je vrácen rutinou Get-DscLocalConfigurationManager teď může obsahovat následující hodnoty:

* **Nečinnosti**
* **Moc práce**
* **PendingReboot**
* **PendingConfiguration**

Také jsme přidali ve vlastnosti LCMStateDetail, který obsahuje další informace o stavu.