---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: gallery,powershell,cmdlet,psget
title: psget_cmdlets_troubleshooting
ms.openlocfilehash: bc49dc78b8205d1194ddfe4bdca98b3e681860bd
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
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