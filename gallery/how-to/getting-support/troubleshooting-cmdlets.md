---
ms.date: 06/12/2017
contributor: manikb
keywords: Galerie prostředí powershell, rutina, psget
title: Řešení potíží s rutinami
ms.openlocfilehash: f5cd9c0cc23fef5891bf02c10b6541ab0f9d418a
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/25/2018
ms.locfileid: "50002458"
---
# <a name="troubleshooting-cmdlets"></a>Řešení potíží s rutinami

## <a name="how-to-resolve-warning-package-your-package-name-failed-to-download-issue"></a>Jak vyřešit "Upozornění: 'váš název balíčku' balíček se nepovedlo stáhnout" problém

Nahlásí se, která `Install-Module` nebo `Update-Module` někdy nezdaří na některých počítačích.
Podle našich šetření, je něco, co můžete dělat s síťové připojení.
Nedávno jsme aktualizovali poskytovatele NuGet tak, aby spolehlivě může stáhnout balíčky.
Můžete postupujte podle pokynů níže proveďte nainstalujte nejnovější sestavení NuGet poskytovatele a potom nainstalovat nebo aktualizovat modul.
Jako příklad dole použijeme modul "Azure".

```powershell
Install-PackageProvider NuGet -MinimumVersion 2.8.5.206 -Force
Launch new PowerShell Console
Update-Module Azure -Verbose
```
