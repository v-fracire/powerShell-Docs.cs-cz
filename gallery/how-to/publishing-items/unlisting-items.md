---
ms.date: 06/12/2017
contributor: JKeithB
ms.topic: conceptual
keywords: Galerie prostředí powershell, rutiny, psgallery
title: Vynětí položek ze seznamu
ms.openlocfilehash: 35dcd283ddace5aec62d692b0ede12ae0bada765
ms.sourcegitcommit: e9ad4d85fd7eb72fb5bc37f6ca3ae1282ae3c6d7
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/10/2018
---
# <a name="unlisting-items"></a>Vynětí položek ze seznamu

**Proč je odebrání položky z Galerie prostředí PowerShell, nejsou viditelné jako možnost?**

Galerie prostředí PowerShell nepodporuje uživatele trvale odstranit jejich položky.
To umožňuje ostatním uživatelům trvat závislosti na vaší položky bez obav o možných zalomení v budoucnu.
Například pokud modul Pester závisí na modulu Azure a Azure, odebere se z galerie, pak uživatel může už používá modul Pester.

Místo odebírání položku, ale můžete můžete unlist ho místo.

**Jaké jsou unlisting položku v galerii prostředí PowerShell se?**

Unlisting položku jako je například modul nebo skriptu v galerii prostředí PowerShell ji odeberte z karty položky. Kromě toho nebude neuvedené položky zjistitelný pomocí panelu vyhledávání.
Jediný způsob, jak stáhnout neuvedené položku je zadejte přesně název a verzi položky.
Z tohoto důvodu nebude unlisting položku Rozdělit další moduly nebo skripty, které jsou na ní závislé.

Chcete-li unlist vaší položky, naleznete na stránce Podrobnosti položky a vyberte Odstranit položku. Zrušte zaškrtnutí políčka 'uvedené a klikněte na tlačítko Uložit.

**Jak můžete odebrat položku?**

Pokud dojde k scénář, kde je nutné odstranění položky, obraťte se na správce Galerie prostředí PowerShell.
Platný odstranění scénáře jsou:
- Problémy věci porušení autorských práv.
- Položka obsahuje potenciálně nebezpečný obsah.
- Položka obsahuje citlivá data.

Odeslání odstranit položku požadavku na správcům Galerie prostředí PowerShell, navštivte stránku s podrobnostmi položky na a vyberte obraťte se na podporu.