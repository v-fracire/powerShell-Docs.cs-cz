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
# <a name="logic-for-preparing-the-module-dependencies-during-publish-operation"></a>Logika pro přípravu závislosti modulu během operace publikování
1.  Moduly, které jsou uvedeny jako součást RequiredModules jsou považovány za jako závislosti.
2.  Moduly, které jsou uvedeny jako součást NestedModules, jehož základní modul není v části základní zadaný modul, se považují za jako závislosti.

3.  Výše závislosti by měla být k dispozici na stejné úložiště cíl, v opačném případě publikovat operace způsobí chybu.
    Například: Pokud 'SnippetPx' není k dispozici v úložišti, níže chyba bude vyvolána.
    ```powershell
    Publish-PSArtifactUtility : PowerShellGet cannot resolve the module dependency 'SnippetPx' of the module 'TypePx' on the repository 'LocalRepo'. Verify that the dependent module 'SnippetPx' is available in the repository 'LocalRepo'. If this dependent
    'SnippetPx' is managed externally, add it to the ExternalModuleDependencies entry in the PSData section of the module manifest.
    ```
4.  Několik závislostí modulu je možné spravovat externě, v takovém případě musí být přidaní do položky ExternalModuleDependencies v části PSData manifestu modulu.
    Následující části ve výše uvedené chybová zpráva
    ```powershell
    If this dependent 'SnippetPx' is managed externally, add it to the ExternalModuleDependencies entry in the PSData section of the module manifest.
    ```

*Během instalace modulu výše připravené závislosti seznamu se používá pro instalaci závislosti.*

*Zkontrolujte, že vaše modulu závislosti jsou k dispozici v části $env: PSModulePath systému během publikování operaci.*