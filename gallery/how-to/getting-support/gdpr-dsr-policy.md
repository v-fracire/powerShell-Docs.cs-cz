---
ms.date: 03/27/2018
contributor: JKeithB
keywords: Galerie prostředí powershell, psgallery GDPR
title: Dodržování předpisů GDPR Galerie prostředí PowerShell
ms.openlocfilehash: fb1191d8a1cd12d5994e41238c384eb504d0c261
ms.sourcegitcommit: 98b7cfd8ad5718efa8e320526ca76c3cc4141d78
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/25/2018
ms.locfileid: "50002646"
---
# <a name="powershell-gallery-gdpr-compliance"></a>Dodržování předpisů GDPR Galerie prostředí PowerShell

## <a name="overview"></a>Přehled

V květnu 2018 zákony Evropské ochrany osobních údajů, obecného Protection Regulation (GDPR), vstoupily v platnost.
GDPR ukládá nová pravidla pro společnosti, státních úřadů, – neziskové organizace a jinými organizacemi, že nabídka zboží a služby lidem v Evropské unii (EU) nebo které shromažďovat a analyzovat data svázaná s pobytem v EU.
GDPR se vztahuje bez ohledu na to, kde se nachází.

> [!NOTE]
> Tento článek popisuje kroky pro odstranění osobních údajů z Galerie prostředí PowerShell a slouží k podpoře vaší povinností v GDPR. Pokud potřebujete obecné informace o podle nařízení GDPR, najdete v článku [GDPR část Service Trust portal](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).

## <a name="personally-identifiable-data"></a>Osobně identifikovatelných dat

Galerie prostředí PowerShell se ukládají následující informace, který může zadat uživatele, které mohou obsahovat osobní údaje:

- Účet Galerie prostředí PowerShell
- Balíčky, které jsou publikované v galerii prostředí PowerShell
- E-mailové korespondence s týmem Galerie prostředí PowerShell

Většina uživatelů, nevytvářejte účet Galerie prostředí PowerShell.
Účet není povinný, pokud se chystáte publikovat balíček nebo použít funkci "Kontaktujte vlastníka" v galerii prostředí PowerShell.
Galerie prostředí PowerShell než e-mailové korespondence iniciované příslušným uživatelem, neukládá identifikovatelné osobní údaje pro uživatele, kteří ještě nevytvořili účet.

Uživatele, kteří vytvářejí účet Galerie prostředí PowerShell můžete publikovat balíčky do Galerie prostředí PowerShell.
Tyto balíčky jsou očekávány kódu Powershellu, ale může obsahovat další informace, včetně osobních údajů.
Níže uvedené informace se zobrazí, jak získat všechny balíčky jste publikovali v galerii prostředí PowerShell.

## <a name="dsr-export-of-powershell-gallery-data"></a>Export PSÚ dat Galerie prostředí PowerShell

Následující části popisují, jak v galerii prostředí PowerShell podporuje žádosti údajů (PSÚ), tak s vysvětlením, jak exportovat informace uložené v galerii prostředí PowerShell a jak požádat o odstranění těchto informací.

### <a name="email"></a>E-mail

E-mailové korespondence může obsahovat žádný z následujících akcí:

- E-mailu odeslaného pro vlastníky Galerie prostředí PowerShell balíčky, pokud analýza kódu vyhledá zjistili potíže v balíčcích, které jste publikovali v galerii prostředí PowerShell
- E-mailu odeslaného kdokoli v týmu Galerie prostředí PowerShell pomocí e-mailovou adresu v stránky "Kontaktujte nás" [cgadmin@microsoft.com](mailto:cgadmin@microsoft.com)
- Registrovaný uživatelů, kteří používají funkci "Kontaktujte vlastníka" v galerii prostředí PowerShell k odesílání e-mailu vlastníka balíčku v galerii prostředí PowerShell

E-mailů podle nebo v galerii prostředí PowerShell mají zásady uchovávání 90 dnů pro podporu možné bezpečnostní vyšetřování by měl škodlivý kód nalezených v galerii prostředí PowerShell.
E-maily se odstraní podle zásad po 90 dnech.

Může vyžadovat zkopíruje všechny e-maily odesílané do nebo z e-mailovou adresu a Galerie prostředí PowerShell v rámci za předchozích 90 dnů.
Žádost o tuto komunikaci, pošlete e-mailu [ cgadmin@microsoft.com ](mailto:cgadmin@microsoft.com), s názvem: "Žádost PSÚ ohledně e-mailů týkajících se k tomuto účtu".
V textu zprávy, jaké informace, které jste požádali stavu (například: odešlete všechny e-maily odesílané nebo přijímané z tohoto e-mailovou adresu.) Všechny e-mailů týkajících se e-mailovou adresu do 90 dnů od žádosti se odešlou do 7 pracovních dnů.

### <a name="powershell-gallery-account-information"></a>Informace o účtu Galerie prostředí PowerShell

Pokud jste vytvořili účet Galerie prostředí PowerShell, můžete najít všechny osobní informace, které jsou uložená v galerii prostředí PowerShell pomocí následujících kroků:

1. Přihlaste se v galerii prostředí PowerShell a potom klikněte na své uživatelské jméno
2. Na další stránku, zobrazí se na stránku účtu, který zobrazuje e-mailovou adresu použije pro účet Galerie prostředí PowerShell

Pokud vytvoříte více než jeden účet v galerii prostředí PowerShell, musíte tento postup opakujte pro každý účet.

### <a name="packages-in-the-powershell-gallery"></a>Balíčky v galerii prostředí PowerShell

Pro usnadnění export balíčky, které jsou publikované v galerii prostředí PowerShell, jsme publikovali skriptu "GetPSGalleryItemsForAuthor" v galerii prostředí PowerShell.
Tento skript exportuje kopie každé verze každého balíčku do Galerie prostředí PowerShell na základě Autor informací uložených v balíčku.

> [!NOTE]
> Autor se ukládají v manifestu balíčku, když publikujete balíček.
> Není zaručeno, že autor se stejnou identitou jako účet, který použijete v galerii prostředí PowerShell.
> Pokud použijete jinou hodnotu v poli Autor, je potřeba zadat tuto hodnotu při použití tohoto skriptu.

Skript může stáhnout pomocí následujícího příkazu Powershellu:

```powershell
Save-Script Get-repository psgallery
```

Potom spustíte skript přímo, spuštěním následujících příkazů Powershellu:

```powershell
# cd <local folder location>
.\GetPSGalleryItemsForAuthor.ps1
```

Zobrazí výzva k zadání jeho autorovi a složku ve vašem systému, požadované balíčky, které se má uložit.

## <a name="deleting-personal-data-from-the-powershell-gallery"></a>Odstranění osobní údaje z Galerie prostředí PowerShell

Chcete-li odstranit svůj účet Galerie prostředí PowerShell nebo všechny balíčky, které vlastníte v galerii prostředí PowerShell, pošlete e-mail na adresu cgadmin@microsoft.com s názvem: "Žádosti GDPR o položky vztahující se k tomuto účtu".
V těle zprávy o stavu jaké informace chcete odstraněné. Příklad:

- Odstraňte prosím verze x.y.z Můj balíček "název balíčku"
- Odstraňte prosím všechny verze balíčku "název balíčku"
- Odstraňte prosím svůj účet Galerie prostředí PowerShell

Správci Galerie prostředí PowerShell odpovíte do 7 pracovních dnů.
Do 30 dní po odeslání žádosti se odstraní balíčky zadané.
