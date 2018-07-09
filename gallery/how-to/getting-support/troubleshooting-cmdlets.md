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
# <a name="troubleshooting-cmdlets"></a><span data-ttu-id="21322-103">Řešení potíží s rutinami</span><span class="sxs-lookup"><span data-stu-id="21322-103">Troubleshooting cmdlets</span></span>

## <a name="how-to-resolve-warning-package-your-package-name-failed-to-download-issue"></a><span data-ttu-id="21322-104">Jak vyřešit "Upozornění: 'váš název balíčku' balíček se nepovedlo stáhnout" problém</span><span class="sxs-lookup"><span data-stu-id="21322-104">How to resolve "WARNING: Package 'your package name' failed to download" issue</span></span>

<span data-ttu-id="21322-105">Nahlásí se, která `Install-Module` nebo `Update-Module` někdy nezdaří na některých počítačích.</span><span class="sxs-lookup"><span data-stu-id="21322-105">It is reported that `Install-Module` or `Update-Module` sometimes fails on some machines.</span></span>
<span data-ttu-id="21322-106">Podle našich šetření, je něco, co můžete dělat s síťové připojení.</span><span class="sxs-lookup"><span data-stu-id="21322-106">Based on our investigation, it is something to do with the networking connection.</span></span>
<span data-ttu-id="21322-107">Nedávno jsme aktualizovali poskytovatele NuGet tak, aby spolehlivě může stáhnout balíčky.</span><span class="sxs-lookup"><span data-stu-id="21322-107">Recently we updated NuGet provider so that it can reliably download packages.</span></span>
<span data-ttu-id="21322-108">Můžete postupujte podle pokynů níže proveďte nainstalujte nejnovější sestavení NuGet poskytovatele a potom nainstalovat nebo aktualizovat modul.</span><span class="sxs-lookup"><span data-stu-id="21322-108">You can follow the instructions below to install the latest build of NuGet provider and then install or update your module.</span></span>
<span data-ttu-id="21322-109">Jako příklad dole použijeme modul "Azure".</span><span class="sxs-lookup"><span data-stu-id="21322-109">Let's use 'Azure' module as an example below.</span></span>

```powershell
Install-PackageProvider NuGet -MinimumVersion 2.8.5.206 -Force
Launch new PowerShell Console
Update-Module Azure -Verbose
```