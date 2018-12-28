---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Přehled platformy Desired State Configuration pro pracovníky s rozhodovací pravomocí
ms.openlocfilehash: ce554d4bb994d4b1816d9d9c24599e4ef0e1c593
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403698"
---
# <a name="desired-state-configuration-overview-for-decision-makers"></a>Přehled platformy Desired State Configuration pro pracovníky s rozhodovací pravomocí

Tento dokument popisuje výhodách pro firmy pomocí Windows Powershellu Desired State Configuration (DSC). Nejedná se o technický průvodce.

## <a name="what-is-desired-state-configuration"></a>Co je Desired State Configuration?

Prostředí PowerShell Desired State Configuration je platforma pro správu konfigurace integrovaný do Windows, která je založená na otevřených standardech. DSC je dostatečně flexibilní, aby funkce konzistentně a spolehlivě v jednotlivých fázích životního cyklu nasazení (vývojové, testovací, předprodukčním prostředí, produkční), stejně jako při škálování na víc systémů.

DSC se soustředí kolem [konfigurace](../configurations/configurations.md).
Konfigurace je snadné čtení dokumentu, který popisuje prostředí skládá z počítače ("uzly") s konkrétními vlastnostmi.
Tyto vlastnosti lze jednoduše zajištění, že se že konkrétní funkce Windows je povolený nebo komplexního, jako při nasazování služby SharePoint.

DSC má také monitorování a vytváření sestav, integrované.
Pokud již není kompatibilní s systému, DSC můžete vygenerovat výstrahu a Jednejte a opravte systém.

## <a name="benefits-of-using-desired-state-configuration"></a>Výhody použití Desired State Configuration

Konfigurace jsou určeny k snadno přečíst, ukládat a aktualizovat.
Konfigurace deklarace zařízení cílový stav by měl být v, místo psaní pokyny, jak uvést v tomto stavu.
Díky tomu je mnohem méně nákladné na další, přijmout, implementaci a údržbu konfigurací pomocí DSC.

Vytvoření konfigurace znamená, že složité nasazení kroky se zaznamenají jako "jediný zdroj pravdivých informací" na jednom místě.
Tím je mnohem méně náchylný opakované nasazení konkrétní sady počítačů.
Zase provádět nasazení, rychlejší a spolehlivější umožňující rychlé vyřízení na komplexních nasazení.

Konfigurace jsou také sdílet prostřednictvím [Galerie prostředí PowerShell](https://powershellgallery.com) znamená běžné scénáře a osvědčené postupy možná již existuje pro práci, kterou je potřeba udělat.


## <a name="desired-state-configuration-and-devops"></a>Desired State Configuration a DevOps

DSC byla navržena s [DevOps](http://blogs.technet.com/b/ashleymcglone/archive/2015/11/20/devops-for-n00bs-ie-windows-people.aspx) na paměti, kombinaci lidi, procesy a nástroje, které umožňují rychlé nasazení a iterace, zaměřuje na poskytování hodnoty koncovým uživatelům, ať už interní nebo externí.
S konfigurací jedné definice prostředí znamená, že vývojáři můžou kódování jejich požadavky na konfiguraci, zkontrolujte, že konfigurace do správy zdrojového kódu a týmy, které operace můžete snadno nasadit kód bez nutnosti přejít náchylné k chybě ruční procesy.

Konfigurace jsou také [řízené daty](../configurations/configData.md), což usnadňuje ops tak může identifikovat a změnit prostředí bez zásahu pro vývojáře.

## <a name="desired-state-configuration-on-premises-and-off-premises"></a>Desired State Configuration On-Premises a mimo pracoviště
DSC umožňuje spravovat místní a provozovaných nasazení.
Pro místní řešení má DSC [serveru vyžádané replikace](../pull-server/pullServer.md) , který umožňuje centralizovat správu počítačů a tvorba sestav o stavu.
Cloudová řešení je DSC použít všude, kde je možné použít Windows.
Existují také určité nabídky z Azure postavená na Desired State Configuration, jako například [Azure Automation](https://azure.microsoft.com/en-us/documentation/services/automation/), který centralizuje, vytvářet sestavy DSC.

## <a name="dsc-and-compatibility"></a>DSC a kompatibility

Přestože DSC byla zavedena v systému Windows Server 2012 R2, je dostupná pro operační systémy nižší úrovně prostřednictvím balíček Windows Management Frameworku (WMF).
Další informace o WMF najdete na [domovské stránce Powershellu](/powershell/).

DSC můžete také použít ke správě systému Linux. Další informace najdete v tématu [Začínáme s DSC pro Linux](../getting-started/lnxGettingStarted.md).
