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
## <a name="how-to-resolve-warning-package-your-package-name-failed-to-download-issue"></a><span data-ttu-id="850df-103">Postup řešení "Upozornění: balíček 'váš název balíčku' stažení se nezdařilo" problém?</span><span class="sxs-lookup"><span data-stu-id="850df-103">How to resolve "WARNING: Package 'your package name' failed to download" issue?</span></span>




<span data-ttu-id="850df-104">Se hlásí, že modul instalace nebo aktualizace modulu někdy dojde k selhání na některé počítače.</span><span class="sxs-lookup"><span data-stu-id="850df-104">It is reported that Install-Module or Update-Module sometimes fails on some machines.</span></span>
<span data-ttu-id="850df-105">Podle našich šetření, je něco dělat s síťové připojení.</span><span class="sxs-lookup"><span data-stu-id="850df-105">Based on our investigation, it is something to do with the networking connection.</span></span>
<span data-ttu-id="850df-106">Nedávno jsme NuGet zprostředkovatele aktualizovat tak, aby ho spolehlivě stáhnout balíčky.</span><span class="sxs-lookup"><span data-stu-id="850df-106">Recently we updated NuGet provider so that it can reliably download packages.</span></span>
<span data-ttu-id="850df-107">Můžete podle pokynů níže nainstalovat poskytovatele NuGet na nejnovější verzi a potom instalaci nebo aktualizaci modulu.</span><span class="sxs-lookup"><span data-stu-id="850df-107">You can follow the instructions below to install the latest build of NuGet provider and then install or update your module.</span></span>
<span data-ttu-id="850df-108">Umožňuje použít modul "Azure" jako příklad níže.</span><span class="sxs-lookup"><span data-stu-id="850df-108">Let's use 'Azure' module as an example below.</span></span>

```powershell
Install-PackageProvider NuGet -MinimumVersion 2.8.5.206 -Force
Launch new PowerShell Console
Update-Module Azure -Verbose
```