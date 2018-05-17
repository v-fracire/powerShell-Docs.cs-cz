---
ms.date: 03/27/2018
contributor: JKeithB
keywords: Galerie prostředí powershell, psgallery, GDPR
title: Dodržování předpisů GDPR Galerie prostředí PowerShell
ms.openlocfilehash: dca1a82952c284980a84caafa13b2807e47e25a0
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
---
# <a name="powershell-gallery-gdpr-compliance"></a>Dodržování předpisů GDPR Galerie prostředí PowerShell

## <a name="overview"></a>Přehled

V květnu 2018 zákonem Evropského ochrany osobních údajů, obecné Data Protection nařízení (GDPR), se projeví.
GDPR ukládá nové pravidel na společnosti, organizace státní správy, bez zisku a organizace nabídka zboží a služeb na osoby ve Evropské unie (EU), nebo že shromažďovat a analyzovat data svázané s obyvatele Evropské unie.
GDPR platí bez ohledu na to, kde se nacházíte.

> [!NOTE]
> Tento článek popisuje kroky pro odstranění osobní data z Galerie prostředí PowerShell a slouží k podpoře vaší povinností podle GDPR. Pokud hledáte obecné informace o GDPR, přečtěte si téma [GDPR části portálu služby důvěřovat](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).

## <a name="personally-identifiable-data"></a>Identifikovatelné osobní údaje

Galerie prostředí PowerShell se ukládají následující informace, které může poskytovat uživatelům, které můžou obsahovat osobní informace:

* Účet Galerie prostředí PowerShell
* Položky, které jsou publikovány do Galerie prostředí PowerShell
* E-mailové korespondence s týmem Galerie prostředí PowerShell

Většina uživatelů nevytvářejte účet Galerie prostředí PowerShell.
Účet se nevyžaduje, pokud chcete publikovat položku nebo použít funkci "Obraťte se na vlastníka" v galerii prostředí PowerShell.
Kromě e-mailové korespondence iniciováno uživatelem Galerie prostředí PowerShell neukládá identifikovatelné osobní údaje pro uživatele, kteří ještě nevytvořili účet.

Uživatelé, kteří vytvořit účet Galerie prostředí PowerShell můžete publikovat položky galerie prostředí PowerShell.
Tyto položky se měl kódu PowerShell, ale může obsahovat další informace, včetně osobních údajů.
Níže uvedené informace se zobrazí, jak můžete získat všechny položky jste publikovali do Galerie prostředí PowerShell.

## <a name="dsr-export-of-powershell-gallery-data"></a>DSR Export dat Galerie prostředí PowerShell

Následující části popisují, jak Galerie prostředí PowerShell podporuje požadavky na data subjektu (DSR), tím, že vysvětlí, jak exportovat informace uložené v galerii prostředí PowerShell a jak požádat o odstranění těchto informací.

### <a name="email"></a>E-mail

E-mailové korespondence může obsahovat žádné z následujících akcí:

* E-mailu odeslaného na vlastníky Galerie prostředí PowerShell položky Pokud analýza kódu kontrol zjistil potíže s libovolnou položku, kterou jste publikovali do Galerie prostředí PowerShell
* Každý, kdo posílá týmem Galerie prostředí PowerShell pomocí e-mailovou adresu na stránce "Kontaktujte nás" e-mailu (cgadmin@microsoft.com)
* Registrované uživatele, kteří používají funkce "Obraťte se na vlastníka" v galerii prostředí PowerShell k odesílání e-mailu vlastníka položky v galerii prostředí PowerShell

E-maily odesílané do Galerie prostředí PowerShell nebo mít zásady uchovávání informací 90 dní pro podporu vyšetřování možné zabezpečení by měl škodlivý kód zjištěných v galerii prostředí PowerShell.
E-mailů jsou zásadami odstraněny po 90 dnech.

Může požádat o kopie všechny e-maily odesílané do nebo z e-mailovou adresu a Galerie prostředí PowerShell v rámci předchozích 90 dnů.
Požádat o tato korespondence, pošlete e-mail na cgadmin@microsoft.com, s názvem: "DSR žádost o e-mailů týkajících se k tomuto účtu".
V textu zprávy, jaké informace, které jste požádali o stavu (například: pošlete prosím všechny e-maily odesílané nebo přijímané z této e-mailovou adresu.) Všechny e-mailů zahrnující e-mailovou adresu do 90 dnů od žádosti budou odeslány do 7 dnů firmy.

### <a name="powershell-gallery-account-information"></a>Informace o účtu Galerie prostředí PowerShell

Pokud jste vytvořili účet Galerie prostředí PowerShell, můžete najít všechny osobní informace, která byla uložena v galerii prostředí PowerShell provedením následujících kroků:

1. Přihlaste se k Galerie prostředí PowerShell, a potom klikněte na své uživatelské jméno
2. Na další stránku, zobrazí se stránku účtu, který zobrazuje e-mailovou adresu, použité pro účet Galerie prostředí PowerShell

Pokud jste vytvořili více než jeden účet v galerii prostředí PowerShell, musíte tento postup opakujte pro každý účet.

### <a name="items-in-the-powershell-gallery"></a>Položky v galerii prostředí PowerShell

Pro usnadnění Export položky, které jsou publikovány do Galerie prostředí PowerShell, jsme publikovali skriptu "GetPSGalleryItemsForAuthor" do Galerie prostředí PowerShell.
Tento skript exportuje kopii každé verzi každá položka vložena Galerie prostředí PowerShell založený na informacích Autor uložená v položce.

> [!NOTE]
> Autor je uložený v manifestu položky při publikování vaší položky.
> Není zaručeno, že autor se stejnou identitou jako účet, který používáte v galerii prostředí PowerShell.
> Pokud použijete jinou hodnotu v poli autora, musíte zadat tuto hodnotu, při použití tohoto skriptu.

Skript může stáhnout pomocí následujícího příkazu Powershellu:

```powershell
Save-Script GetPSGalleryItemsForAuthor -path <local folder location> -repository psgallery
```

Když pak spustíte skript přímo, spuštěním následujících příkazů prostředí PowerShell:

```powershell
cd <local folder location >
.\GetPSGalleryItemsForAuthor.ps1
```

Zobrazí se výzva k zadání autora a složku ve vašem systému místo položky, které chcete uložit.

## <a name="deleting-personal-data-from-the-powershell-gallery"></a>Odstranění osobní Data z Galerie Powershellu

Pokud chcete odstranit účet Galerie prostředí PowerShell nebo libovolnou položku, kterou vlastníte v galerii prostředí PowerShell, odesílat e-mailu cgadmin@microsoft.com s názvem: "GDPR žádost pro položky vztahující se k tomuto účtu".
V těle zprávy o stavu informacích chcete odstraněné. Příklad:

* Odstraňte prosím verze x.y.z "název položky" Moje položky
* Odstraňte všechny verze "název položky" Moje položky
* Odstraňte Můj účet Galerie prostředí PowerShell

Správci Galerie prostředí PowerShell odpovíte do 7 dnů firmy.
Do 30 dní po odeslání žádosti se odstraní vybrané položky.
