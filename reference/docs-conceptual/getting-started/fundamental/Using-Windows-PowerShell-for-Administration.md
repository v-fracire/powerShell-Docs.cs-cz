---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Použití Windows PowerShellu ke správě
ms.assetid: db6334ec-ace6-436d-ab88-77aefc817511
ms.openlocfilehash: 69790ddd6bae26dd18e30af860bad4c749cd86a5
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
ms.locfileid: "30954326"
---
# <a name="using-windows-powershell-for-administration"></a>Použití Windows PowerShellu ke správě
Základní cíl prostředí Windows PowerShell poskytuje lepší, snadnější správu kontrolu nad systémy, interaktivní nebo ze skriptu. Tato kapitola provede řešení mnoha konkrétních problémů z hlediska správy systémy Windows v prostředí Windows PowerShell. I když nejsou už jsme mluvili o skriptech nebo funkcích v Průvodci uživatele Windows PowerShell, řešení lze z skripty nebo jako funkce později. Ukážeme příklady, které obsahují funkce jako součást řešení k řešení problémů.

V rámci řešení popisy uvidíte směs řešení pomocí konkrétní rutiny, obecné rutiny Get-WmiObject a i externí nástroje, které jsou součástí infrastruktury systému Windows a rozhraní .NET Framework. Pomocí externích nástrojů je součástí dlouhodobé záměr návrhu prostředí Windows PowerShell. To i v případě systému roste, uživatelé se průběžně setkají situace, ve kterých k dispozici modulové není udělat všechny objekty, které potřebují. Místo podporovat závislost na rutiny implementace samostatně prostředí Windows PowerShell se pokusí podporovat integrační řešení od všechny možné alternativní scénáře.