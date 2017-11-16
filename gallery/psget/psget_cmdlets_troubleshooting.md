---
ms.date: 2017-06-12
contributor: manikb
ms.topic: reference
keywords: "Galerie prostředí powershell, rutiny, psget"
title: psget_cmdlets_troubleshooting
ms.openlocfilehash: ccb39f44e8d11f1e2a912da0c4f18b700e836c91
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
## <a name="how-to-resolve-warning-package-your-package-name-failed-to-download-issue"></a>Postup řešení "Upozornění: balíček 'váš název balíčku' stažení se nezdařilo" problém?




Se hlásí, že modul instalace nebo aktualizace modulu někdy dojde k selhání na některé počítače.
Podle našich šetření, je něco dělat s síťové připojení.
Nedávno jsme NuGet zprostředkovatele aktualizovat tak, aby ho spolehlivě stáhnout balíčky.
Můžete podle pokynů níže nainstalovat poskytovatele NuGet na nejnovější verzi a potom instalaci nebo aktualizaci modulu.
Umožňuje použít modul "Azure" jako příklad níže.

```powershell
Install-PackageProvider NuGet -MinimumVersion 2.8.5.206 -Force
Launch new PowerShell Console
Update-Module Azure -Verbose
```

