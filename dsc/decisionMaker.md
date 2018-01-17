---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Přehled stavu konfigurace požadovaných pro rozhodují"
ms.openlocfilehash: cbde5d22f9cf118485a0302e53ee0a75eb4b8843
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="desired-state-configuration-overview-for-decision-makers"></a>Přehled stavu konfigurace požadovaných pro rozhodují

Tento dokument popisuje obchodní výhody použití prostředí PowerShell požadovaného stavu konfigurace (DSC). Není technické příručce.

## <a name="what-is-desired-state-configuration"></a>Co je konfigurace požadovaného stavu?

Požadovaného stavu aplikace Windows PowerShell (DSC) je součástí systému Windows, která je založená na standardech, otevřete platforma pro správu konfigurace. DSC je dostatečně flexibilní, aby fungovat spolehlivě a konzistentní v jednotlivých fázích životního cyklu nasazení (vývoj, testovací, předprodukční, produkční), a také během Škálováním na více systémů. 

DSC se soustředí kolem "[konfigurace](https://msdn.microsoft.com/en-us/powershell/dsc/configurations)".
Konfigurace je snadno číst dokument, který popisuje prostředí počítače ("uzlů"), s konkrétními vlastnostmi. Tyto charakteristiky může být stejně jednoduché jako zajistit, že určité funkce systému Windows je povolený nebo komplexní jako nasazení služby SharePoint. 

DSC má také monitorování a vytváření sestav součástí. Pokud již není kompatibilní s systému, DSC můžete vygenerovat výstrahu v a fungovat na systému. 

## <a name="benefits-of-using-desired-state-configuration"></a>Výhody použití Desired State Configuration

Konfigurace jsou navrženy pro snadno přečíst, ukládat a aktualizovat. Konfigurace deklarovat stavu cílová zařízení musí být v, místo aby se pokyny, jak je uvést v tomto stavu. Díky tomu je mnohem méně nákladná další, přijímat, implementovat a Udržovat konfigurace pomocí DSC. 

Vytvoření konfigurace znamená, že jsou kroky komplexní nasazení zaznamená jako "jednoho zdroje založená" na jednom místě. Díky tomu mnohem méně náchylný opakované nasazení určitou sadu počítačů. Pak provedení nasazení rychlejší a spolehlivější což umožňuje rychlost na nasazení komplexní.

Konfigurace je také možné sdílet prostřednictvím [Galerie prostředí PowerShell](https://powershellgallery.com) znamená běžné scénáře a osvědčené postupy možná již existuje pro práci, je třeba provést.


## <a name="desired-state-configuration-and-devops"></a>Konfigurace požadovaného stavu a DevOps

[DevOps](http://blogs.technet.com/b/ashleymcglone/archive/2015/11/20/devops-for-n00bs-ie-windows-people.aspx) je kombinací osoby, proces a nástroje, které umožňují pro rychlé nasazení a iterace zaměřuje na hodnotu koncovým uživatelům, ať už interní nebo externí. DSC byla vytvořena DevOps v paměti. S konfigurací jedné definovat prostředí znamená, že vývojáři mohou kódování požadavky do konfigurace, zkontrolujte, že konfigurace do správy zdrojového kódu a oddělení můžete snadno nasadit kód aniž by museli projít k chybám Manuální procesy. 

Konfigurace jsou také [řízené daty](https://msdn.microsoft.com/en-us/powershell/dsc/configdata), což usnadňuje ops týmy identifikovat a změnit prostředí bez zásahu vývojáře. 

## <a name="desired-state-configuration-on--and-off-premises"></a>Požadované konfigurace stavu na - a mimo pracoviště

DSC umožňuje spravovat místní i mimo pracoviště nasazení. Pro místní řešení pro DSC má [načítacího serveru](https://msdn.microsoft.com/en-us/powershell/dsc/pullserver) který slouží k centralizovat správu počítačů a tvorba sestav o jejich stav. Pro cloudové řešení pro DSC je použít kdekoli Windows použitelné. Existují také určité nabídky z Azure postaveny na konfigurace požadovaného stavu jako [Azure Automation](https://azure.microsoft.com/en-us/documentation/services/automation/), který centralizuje sestavy DSC. 

## <a name="dsc-and-compatibility"></a>DSC a kompatibility

I když DSC byla zavedena v systému Windows Server 2012 R2, je k dispozici pro operační systémy nižší úrovně prostřednictvím balíčku Windows Management Framework (WMF). Další informace o WMF naleznete na [domovské stránky prostředí PowerShell](https://msdn.microsoft.com/en-us/powershell/). 

DSC můžete také použít ke správě systému Linux. Další informace najdete v tématu [Začínáme s DSC pro Linux](https://msdn.microsoft.com/en-us/powershell/dsc/lnxgettingstarted).

