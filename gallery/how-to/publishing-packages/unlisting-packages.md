---
ms.date: 06/12/2017
contributor: JKeithB
keywords: Galerie prostředí powershell, rutina, psgallery
title: Vynětí balíčky
ms.openlocfilehash: fb66fd23dae1d4640056a764c31426f61f56d910
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/25/2018
ms.locfileid: "50004019"
---
# <a name="unlisting-packages"></a>Unlisting balíčky

**Proč je odebrat balíček z Galerie prostředí PowerShell, nejsou viditelné jako možnost?**

Galerie prostředí PowerShell nepodporuje uživatelů se odstraňuje natrvalo své balíčky.
To umožňuje ostatním uživatelům provádět závislosti na své balíčky bez starostí o možných konce v budoucnu.
Například pokud modulu Pester závisí na modulu Azure a Azure, odebere se z galerie, pak uživatel může již používá modul Pester.

Místo aby odebrala balíček, ale můžete můžete vyjmutí ze seznamu jej místo toho.

**Co dělá vynětí balíček v galerii prostředí PowerShell dělat?**

Vynětí balíčku, například modul nebo skript ve galerii prostředí PowerShell, bude odebrat z karty balíčky. Kromě toho nesmí být neuvedené v seznamu balíčků zjistitelné pomocí panelu hledání.
Jediný způsob, jak si stáhnout balíček neuvedené v seznamu je zadat přesný název a verzi balíčku.
Z tohoto důvodu vynětí balíčku nebudou přerušeny. Další moduly nebo skripty, které jsou na ní závislé.

Vyjmutí ze seznamu vašeho balíčku, najdete na stránce podrobností balíčku a vyberte možnost "odstranit modul. Zrušte zaškrtnutí políčka "Uvedené" a klikněte na Uložit.

**Jak můžete balíček odstranit?**

Pokud máte scénáře, kdy je nezbytné odstranění balíčku, obraťte se na správce Galerie prostředí PowerShell.
Platný odstranění scénáře jsou:
- Problémy porušení autorských práv.
- Balíček obsahuje potenciálně škodlivý obsah.
- Balíček obsahuje citlivé údaje.

Odeslat odstranit balíček požadavek správcům Galerie prostředí PowerShell, navštivte stránku s podrobnostmi balíčku a vyberte obraťte se na podporu.
