---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: Galerie prostředí powershell, rutiny, psget
title: Řešení potíží s rutiny
ms.openlocfilehash: 6295a5b99aa19db933569638d84e490ad81eedc7
ms.sourcegitcommit: e9ad4d85fd7eb72fb5bc37f6ca3ae1282ae3c6d7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/10/2018
---
# <a name="troubleshooting-cmdlets"></a>Řešení potíží s rutiny

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