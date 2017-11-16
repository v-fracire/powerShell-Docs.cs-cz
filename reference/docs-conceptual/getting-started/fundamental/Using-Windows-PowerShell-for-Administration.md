---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Pomocí prostředí Windows PowerShell pro správu"
ms.assetid: db6334ec-ace6-436d-ab88-77aefc817511
ms.openlocfilehash: fa87745b9be04d14de37a308d870b73c5a98cf83
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/03/2017
---
# <a name="using-windows-powershell-for-administration"></a>Pomocí prostředí Windows PowerShell pro správu
Základní cíl prostředí Windows PowerShell poskytuje lepší, snadnější správu kontrolu nad systémy, interaktivní nebo ze skriptu. Tato kapitola provede řešení mnoha konkrétních problémů z hlediska správy systémy Windows v prostředí Windows PowerShell. I když nejsou už jsme mluvili o skriptech nebo funkcích v Průvodci uživatele Windows PowerShell, řešení lze z skripty nebo jako funkce později. Ukážeme příklady, které obsahují funkce jako součást řešení k řešení problémů.

V rámci řešení popisy uvidíte směs řešení pomocí konkrétní rutiny, obecné rutiny Get-WmiObject a i externí nástroje, které jsou součástí infrastruktury systému Windows a rozhraní .NET Framework. Pomocí externích nástrojů je součástí dlouhodobé záměr návrhu prostředí Windows PowerShell. To i v případě systému roste, uživatelé se průběžně setkají situace, ve kterých k dispozici modulové není udělat všechny objekty, které potřebují. Místo podporovat závislost na rutiny implementace samostatně prostředí Windows PowerShell se pokusí podporovat integrační řešení od všechny možné alternativní scénáře.

