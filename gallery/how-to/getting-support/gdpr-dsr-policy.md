---
ms.date: 03/27/2018
contributor: JKeithB
keywords: Galerie prostředí powershell, psgallery GDPR
title: Dodržování předpisů GDPR Galerie prostředí PowerShell
ms.openlocfilehash: 14b82fa07df52f02f0d7577cb0eef70faa4285a2
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893242"
---
# <a name="powershell-gallery-gdpr-compliance"></a>Dodržování předpisů GDPR Galerie prostředí PowerShell

## <a name="overview"></a>Přehled

V květnu 2018 zákony Evropské ochrany osobních údajů, obecného Protection Regulation (GDPR), se projeví.
GDPR ukládá nová pravidla pro společnosti, státních úřadů, – neziskové organizace a jinými organizacemi, že nabídka zboží a služby lidem v Evropské unii (EU) nebo které shromažďovat a analyzovat data svázaná s pobytem v EU.
GDPR se vztahuje bez ohledu na to, kde se nachází.

> [!NOTE]
> Tento článek popisuje kroky pro odstranění osobních údajů z Galerie prostředí PowerShell a slouží k podpoře vaší povinností v GDPR. Pokud potřebujete obecné informace o podle nařízení GDPR, najdete v článku [GDPR část Service Trust portal](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted).

## <a name="personally-identifiable-data"></a>Osobně identifikovatelných dat

Galerie prostředí PowerShell se ukládají následující informace, který může zadat uživatele, které mohou obsahovat osobní údaje:

- Účet Galerie prostředí PowerShell
- Publikování položek v galerii prostředí PowerShell
- E-mailové korespondence s týmem Galerie prostředí PowerShell

Většina uživatelů, nevytvářejte účet Galerie prostředí PowerShell.
Účet není povinný, pokud se chystáte publikovat položku nebo použít funkci "Kontaktujte vlastníka" v galerii prostředí PowerShell.
Galerie prostředí PowerShell než e-mailové korespondence iniciované příslušným uživatelem, neukládá identifikovatelné osobní údaje pro uživatele, kteří ještě nevytvořili účet.

Uživatelé, kteří vytvořit účet Galerie prostředí PowerShell můžete publikovat položky v galerii prostředí PowerShell.
Tyto položky se očekává, že se kód Powershellu, ale může obsahovat další informace, včetně osobních údajů.
Níže uvedené informace se zobrazí, jak získat všechny položky v galerii prostředí PowerShell jste publikovali.

## <a name="dsr-export-of-powershell-gallery-data"></a>Export PSÚ dat Galerie prostředí PowerShell

Následující části popisují, jak v galerii prostředí PowerShell podporuje žádosti údajů (PSÚ), tak s vysvětlením, jak exportovat informace uložené v galerii prostředí PowerShell a jak požádat o odstranění těchto informací.

### <a name="email"></a>E-mail

E-mailové korespondence může obsahovat žádný z následujících akcí:

- E-mailu odeslaného pro vlastníky položky, pokud analýza kódu vyhledá zjistila problém s libovolnou položku, kterou jste publikovali v galerii prostředí PowerShell Galerie prostředí PowerShell
- E-mailu odeslaného kdokoli v týmu Galerie prostředí PowerShell pomocí e-mailovou adresu v stránky "Kontaktujte nás" [cgadmin@microsoft.com](mailto:cgadmin@microsoft.com)
- Registrovaný uživatelů, kteří používají funkci "Kontaktujte vlastníka" v galerii prostředí PowerShell k odesílání e-mailu na vlastníka položky v galerii prostředí PowerShell

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

### <a name="items-in-the-powershell-gallery"></a>Položky v galerii prostředí PowerShell

Pro usnadnění exportu položky publikována do Galerie prostředí PowerShell, jsme publikovali skriptu "GetPSGalleryItemsForAuthor" v galerii prostředí PowerShell.
Tento skript exportuje kopie každé verze každé položky do Galerie prostředí PowerShell na základě Autor informací uložených v položce.

> [!NOTE]
> Autor se ukládají v manifestu položky při publikování položky.
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

Zobrazí výzva k zadání jeho autorovi a složku ve vašem systému, požadované položky, které chcete uložit.

## <a name="deleting-personal-data-from-the-powershell-gallery"></a>Odstranění osobní údaje z Galerie prostředí PowerShell

Chcete-li odstranit svůj účet Galerie prostředí PowerShell nebo libovolnou položku, kterou vlastníte ve galerii prostředí PowerShell, pošlete e-mail na adresu cgadmin@microsoft.com s názvem: "Žádosti GDPR o položky vztahující se k tomuto účtu".
V těle zprávy o stavu jaké informace chcete odstraněné. Příklad:

- Odstraňte prosím verze x.y.z Moje položky "název"
- Odstraňte prosím všechny verze Moje položky "název"
- Odstraňte prosím svůj účet Galerie prostředí PowerShell

Správci Galerie prostředí PowerShell odpovíte do 7 pracovních dnů.
Do 30 dní po odeslání žádosti se odstraní zadané položky.