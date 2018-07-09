---
ms.date: 06/12/2017
contributor: manikb
keywords: Galerie prostředí powershell, rutina, psget
title: Řešení potíží s rutinami
ms.openlocfilehash: c0a1fbcafd8c4443dc9d628c54c4c525d9701861
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37892470"
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