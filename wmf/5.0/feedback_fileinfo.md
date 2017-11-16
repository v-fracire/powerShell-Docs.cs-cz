---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
ms.openlocfilehash: 587f3f592f4aab53c95bbc6d37ea37d7f2364aec
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="updates-to-fileinfo-object"></a>Aktualizace FileInfo objekt
Informace o verzi souboru může být zavádějící, obzvláště v případech, kdy byl soubor opravit. Tato verze WMF 5.0 přidává nové **FileVersionRaw** a **ProductVersionRaw** skriptu vlastnosti FileInfo objektů. Zde jsou vlastnosti, jako je zobrazena pro powershell.exe (za předpokladu, že $pid je ID procesu prostředí PowerShell):

```powershell
PS C:\> Get-Process -Id $pid -FileVersionInfo | fl *version* -Force


FileVersionRaw    : 10.0.10586.117
ProductVersionRaw : 10.0.10586.117
FileVersion       : 10.0.10586.117 (th2_release.160212-2359)
ProductVersion    : 10.0.10586.117

