---
ms.date: 06/12/2017
contributor: manikb
ms.topic: reference
keywords: gallery,powershell,cmdlet,psget
title: psget_moduledependencypopulation
ms.openlocfilehash: c4c9f203e9c526ff532c2388acb6334515d66934
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="logic-for-preparing-the-module-dependencies-during-publish-operation"></a><span data-ttu-id="d920d-103">Logika pro přípravu závislosti modulu během operace publikování</span><span class="sxs-lookup"><span data-stu-id="d920d-103">Logic for preparing the module dependencies during Publish operation</span></span>
1.  <span data-ttu-id="d920d-104">Moduly, které jsou uvedeny jako součást RequiredModules jsou považovány za jako závislosti.</span><span class="sxs-lookup"><span data-stu-id="d920d-104">Modules listed as part of RequiredModules are considered as dependencies.</span></span>
2.  <span data-ttu-id="d920d-105">Moduly, které jsou uvedeny jako součást NestedModules, jehož základní modul není v části základní zadaný modul, se považují za jako závislosti.</span><span class="sxs-lookup"><span data-stu-id="d920d-105">Modules listed as part of NestedModules, whose module base is not under the specified module base, are considered as dependencies.</span></span>

3.  <span data-ttu-id="d920d-106">Výše závislosti by měla být k dispozici na stejné úložiště cíl, v opačném případě publikovat operace způsobí chybu.</span><span class="sxs-lookup"><span data-stu-id="d920d-106">Above dependencies should be available on the same target repository, otherwise publish operation will result in an error.</span></span>
    <span data-ttu-id="d920d-107">Například: Pokud 'SnippetPx' není k dispozici v úložišti, níže chyba bude vyvolána.</span><span class="sxs-lookup"><span data-stu-id="d920d-107">For example: If 'SnippetPx' is not available on the repository, below error will be thrown.</span></span>
    ```powershell
    Publish-PSArtifactUtility : PowerShellGet cannot resolve the module dependency 'SnippetPx' of the module 'TypePx' on the repository 'LocalRepo'. Verify that the dependent module 'SnippetPx' is available in the repository 'LocalRepo'. If this dependent
    'SnippetPx' is managed externally, add it to the ExternalModuleDependencies entry in the PSData section of the module manifest.
    ```
4.  <span data-ttu-id="d920d-108">Několik závislostí modulu je možné spravovat externě, v takovém případě musí být přidaní do položky ExternalModuleDependencies v části PSData manifestu modulu.</span><span class="sxs-lookup"><span data-stu-id="d920d-108">Some module dependencies can be managed externally, in that case they should be added to the ExternalModuleDependencies entry in the PSData section of the module manifest.</span></span>
    <span data-ttu-id="d920d-109">Následující části ve výše uvedené chybová zpráva</span><span class="sxs-lookup"><span data-stu-id="d920d-109">Below part in the above error message</span></span>
    ```powershell
    If this dependent 'SnippetPx' is managed externally, add it to the ExternalModuleDependencies entry in the PSData section of the module manifest.
    ```

<span data-ttu-id="d920d-110">*Během instalace modulu výše připravené závislosti seznamu se používá pro instalaci závislosti.*</span><span class="sxs-lookup"><span data-stu-id="d920d-110">*During the module installation, above prepared dependencies list is used for installing the dependencies.*</span></span>

<span data-ttu-id="d920d-111">*Zkontrolujte, že vaše modulu závislosti jsou k dispozici v části $env: PSModulePath systému během publikování operaci.*</span><span class="sxs-lookup"><span data-stu-id="d920d-111">*Please ensure that your module’s dependencies are available under $env:PSModulePath on your system during publish operation.*</span></span>