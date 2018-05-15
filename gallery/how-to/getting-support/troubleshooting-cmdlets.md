---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: Galerie prostředí powershell, rutiny, psget
title: Řešení potíží s rutiny
ms.openlocfilehash: 6295a5b99aa19db933569638d84e490ad81eedc7
ms.sourcegitcommit: e9ad4d85fd7eb72fb5bc37f6ca3ae1282ae3c6d7
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/10/2018
---
# <a name="troubleshooting-cmdlets"></a><span data-ttu-id="c05b5-103">Řešení potíží s rutiny</span><span class="sxs-lookup"><span data-stu-id="c05b5-103">Troubleshooting cmdlets</span></span>

## <a name="how-to-resolve-warning-package-your-package-name-failed-to-download-issue"></a><span data-ttu-id="c05b5-104">Postup řešení "Upozornění: balíček 'váš název balíčku' stažení se nezdařilo" problém?</span><span class="sxs-lookup"><span data-stu-id="c05b5-104">How to resolve "WARNING: Package 'your package name' failed to download" issue?</span></span>

<span data-ttu-id="c05b5-105">Se hlásí, že modul instalace nebo aktualizace modulu někdy dojde k selhání na některé počítače.</span><span class="sxs-lookup"><span data-stu-id="c05b5-105">It is reported that Install-Module or Update-Module sometimes fails on some machines.</span></span>
<span data-ttu-id="c05b5-106">Podle našich šetření, je něco dělat s síťové připojení.</span><span class="sxs-lookup"><span data-stu-id="c05b5-106">Based on our investigation, it is something to do with the networking connection.</span></span>
<span data-ttu-id="c05b5-107">Nedávno jsme NuGet zprostředkovatele aktualizovat tak, aby ho spolehlivě stáhnout balíčky.</span><span class="sxs-lookup"><span data-stu-id="c05b5-107">Recently we updated NuGet provider so that it can reliably download packages.</span></span>
<span data-ttu-id="c05b5-108">Můžete podle pokynů níže nainstalovat poskytovatele NuGet na nejnovější verzi a potom instalaci nebo aktualizaci modulu.</span><span class="sxs-lookup"><span data-stu-id="c05b5-108">You can follow the instructions below to install the latest build of NuGet provider and then install or update your module.</span></span>
<span data-ttu-id="c05b5-109">Umožňuje použít modul "Azure" jako příklad níže.</span><span class="sxs-lookup"><span data-stu-id="c05b5-109">Let's use 'Azure' module as an example below.</span></span>

```powershell
Install-PackageProvider NuGet -MinimumVersion 2.8.5.206 -Force
Launch new PowerShell Console
Update-Module Azure -Verbose
```