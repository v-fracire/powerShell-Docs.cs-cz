---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
ms.openlocfilehash: 6356902193fc6ec651b2f7e53f8885cb59f17542
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="updates-to-fileinfo-object"></a>Aktualizace objektu FileInfo
Informace o verzi souboru může být zavádějící, obzvláště v případech, kdy byl soubor opravit. Tato verze WMF 5.0 přidává nové **FileVersionRaw** a **ProductVersionRaw** skriptu vlastnosti FileInfo objektů. Zde jsou vlastnosti, jako je zobrazena pro powershell.exe (za předpokladu, že $pid je ID procesu prostředí PowerShell):

```powershell
PS C:\> Get-Process -Id $pid -FileVersionInfo | fl *version* -Force


FileVersionRaw    : 10.0.10586.117
ProductVersionRaw : 10.0.10586.117
FileVersion       : 10.0.10586.117 (th2_release.160212-2359)
ProductVersion    : 10.0.10586.117