---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Použití profilů v prostředí Windows PowerShell ISE
ms.assetid: 0219626a-6da5-4acc-b630-d058e8b29cc6
ms.openlocfilehash: 8789d6283457f790fdea27657abb2612304e10a1
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
ms.locfileid: "30951218"
---
# <a name="how-to-use-profiles-in-windows-powershell-ise"></a>Použití profilů v prostředí Windows PowerShell ISE

Toto téma vysvětluje, jak používat profily ve Windows PowerShell® Integrované skriptovací prostředí (ISE). Doporučujeme, abyste před provedením úlohy v této části, zkontrolovat [about_Profiles](/powershell/module/microsoft.powershell.core/about/about_profiles), nebo v podokně konzoly, typ, `Get-Help about_Profiles` a stiskněte klávesu **ENTER**.

Profil je skript Windows PowerShell ISE, který automaticky spustí po spuštění novou relaci.  Můžete vytvořit jeden nebo více profilů prostředí Windows PowerShell pro Windows PowerShell ISE a použít je k přidání konfigurace prostředí Windows PowerShell nebo Windows PowerShell ISE, příprava pro vaše použití s proměnnými, aliasy, funkce a barev a písem Předvolby, které chcete mít k dispozici. Profil ovlivňuje všechny Windows PowerShell ISE relace, kterou spouštíte.

> [!NOTE]
> Zásady spouštění prostředí Windows PowerShell Určuje, zda můžete spouštět skripty a načíst profil. Výchozí zásady spouštění, "S omezeným přístupem," Zabraňuje všechny skripty spuštění, včetně profily. Pokud použijete zásady "S omezeným přístupem", nelze načíst profil. Další informace o provádění zásad najdete v tématu [about_Execution_Policies](/powershell/module/microsoft.powershell.core/about/about_execution_policies).

## <a name="selecting-a-profile-to-use-in-the-windows-powershell-ise"></a>Výběr profilu pro použití v systému Windows PowerShell ISE

Windows PowerShell ISE podporuje profily pro aktuálního uživatele a všichni uživatelé. Podporuje také profily prostředí Windows PowerShell, které platí pro všechny hostitele.

Profil, který používáte, je určen podle způsobu použití prostředí Windows PowerShell a Windows PowerShell ISE.

- Pokud používáte pouze ISE Windows PowerShell ke spouštění prostředí Windows PowerShell, uložte všechny položky v jednom ISE konkrétní profilů, jako je například CurrentUserCurrentHost profil pro Windows PowerShell ISE nebo AllUsersCurrentHost pro Windows PowerShell ISE.

- Pokud používáte více hostitelských aplikací ke spouštění prostředí Windows PowerShell, uložte funkce, aliasy, proměnné a příkazy v profilu, který má vliv na všechny hostitele programy, jako je například CurrentUserAllHosts nebo AllUsersAllHosts a uložit ISE specifické funkce, jako je barev a písem vlastní nastavení v profilu CurrentUserCurrentHost profil Windows PowerShell ISE nebo AllUsersCurrentHost pro Windows PowerShell ISE.

Níže jsou uvedeny profily, které můžete vytvořit a použít v systému Windows PowerShell ISE. Každý profil je uložen na konkrétní cestu.

| Typ profilu | Cesta profilu |
| --- | --- |
| **Aktuální uživatel, prostředí PowerShell ISE**| `$PROFILE.CurrentUserCurrentHost`, nebo `$PROFILE` |
| **Všichni uživatelé, prostředí PowerShell ISE**| `$PROFILE.AllUsersCurrentHost` |
| **Aktuální uživatel, všechny hostitele**| `$PROFILE.CurrentUserAllHosts` |
| **Všichni uživatelé, všechny hostitele** | `$PROFILE.AllUsersAllHosts` |

## <a name="to-create-a-new-profile"></a>Chcete-li vytvořit nový profil

Chcete-li vytvořit nové "aktuální uživatel, Windows PowerShell ISE" profil, spusťte tento příkaz:

```powershell
if (!(Test-Path -Path $PROFILE ))
{ New-Item -Type File -Path $PROFILE -Force }
```

Chcete-li vytvořit novou "Všichni uživatelé, Windows PowerShell ISE" profil, spusťte tento příkaz:

```powershell
if (!(Test-Path -Path $PROFILE.AllUsersCurrentHost))
{ New-Item -Type File -Path $PROFILE.AllUsersCurrentHost -Force }
```

Chcete-li vytvořit nový profil "aktuální uživatel všechny hostitelem", spusťte tento příkaz:

```powershell
if (!(Test-Path -Path $PROFILE.CurrentUserAllHosts))
{ New-Item -Type File -Path $PROFILE.CurrentUserAllHosts -Force }
```

Chcete-li vytvořit nový profil "všichni uživatelé, všechny hostitelem", zadejte:

```powershell
if (!(Test-Path -Path $PROFILE.AllUsersAllHosts))
{ New-Item -Type File -Path $PROFILE.AllUsersAllHosts -Force }
```

## <a name="to-edit-a-profile"></a>Chcete-li upravit profil

1. Chcete-li spustit tento profil, spusťte příkaz psedit s proměnné, která určuje profil, který chcete upravit. Chcete-li například otevřete "aktuální uživatel, Windows PowerShell ISE" profilu, zadejte: `psEdit $PROFILE`

2. Některé položky přidáte do vašeho profilu. Následuje několik příkladů, jak začít:

   - Chcete-li změnit výchozí barvu pozadí panelu konzoly na modrou v souboru typ profilu: `$psISE.Options.OutputPaneBackground = 'blue'` . Další informace o $psISE proměnné najdete v tématu [odkaz na Windows PowerShell ISE objektu modelu](The-ISE-Object-Model-Hierarchy.md).

   - Chcete-li změnit velikost písma až 20 číslic v profilu typ souboru: `$psISE.Options.FontSize =20`

3. Uložte soubor profilu, na **soubor** nabídky, klikněte na tlačítko **Uložit**. Při příštím otevření Windows PowerShell ISE, vaše vlastní nastavení se projeví.

## <a name="see-also"></a>Viz také

- [about_Profiles](/powershell/module/microsoft.powershell.core/about/about_profiles)
- [Představení Windows PowerShell ISE](Introducing-the-Windows-PowerShell-ISE.md)