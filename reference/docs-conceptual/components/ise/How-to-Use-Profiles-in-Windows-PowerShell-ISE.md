---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Použití profilů v prostředí Windows PowerShell ISE
ms.assetid: 0219626a-6da5-4acc-b630-d058e8b29cc6
ms.openlocfilehash: b319aa089c2a4a7008acd9850f15342dac70aee2
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403798"
---
# <a name="how-to-use-profiles-in-windows-powershell-ise"></a>Použití profilů v prostředí Windows PowerShell ISE

Toto téma vysvětluje, jak používat profily ve Windows Powershellu® integrovaném skriptovacím prostředí (ISE). Doporučujeme vám, před provedením úkolů v této části, abyste si přečetli [about_Profiles](/powershell/module/microsoft.powershell.core/about/about_profiles), nebo na panelu konzoly, typ, `Get-Help about_Profiles` a stiskněte klávesu **ENTER**.

Profil je skript Windows PowerShell ISE, který se spustí automaticky při spuštění nové relace.  Můžete vytvořit jeden nebo více profilů prostředí Windows PowerShell pro Windows PowerShell ISE a využít k přidání konfigurace prostředí Windows PowerShell nebo Windows PowerShell ISE Příprava pro své použití, s proměnnými, aliasy, funkce a barev a písem Předvolby, které chcete mít k dispozici. Profil, který ovlivňuje všechny Windows PowerShell ISE relace, kterou spouštíte.

> [!NOTE]
> Zásady spouštění prostředí Windows PowerShell Určuje, zda můžete spustit skripty a načíst profil. Výchozí zásadu spouštění, "S omezeným přístupem," Zabraňuje všechny skripty spuštění, včetně profilů. Pokud používáte zásady "Omezeno", nelze načíst profil. Další informace o spuštění zásady, najdete v části [about_Execution_Policies](/powershell/module/microsoft.powershell.core/about/about_execution_policies).

## <a name="selecting-a-profile-to-use-in-the-windows-powershell-ise"></a>Vyberte profil, který chcete použít v prostředí Windows PowerShell ISE

Windows PowerShell ISE podporuje profily pro aktuálního uživatele a všechny uživatele. Podporuje také profily Windows Powershellu, které se vztahují na všechny hostitele.

Profil, který používáte se určuje podle způsobu použití prostředí Windows PowerShell a Windows PowerShell ISE.

- Pokud používáte pouze Windows PowerShell ISE ke spouštění prostředí Windows PowerShell, uložte všechny položky v jednom z ISE konkrétní profily, jako je například CurrentUserCurrentHost profil pro Windows PowerShell ISE nebo AllUsersCurrentHost pro Windows PowerShell ISE.

- Pokud používáte více hostitelských aplikací ke spouštění prostředí Windows PowerShell, uložte funkce, aliasy, proměnné a příkazy v profilu, který má vliv na všechny hostitele programy, jako je například CurrentUserAllHosts nebo profil AllUsersAllHosts a uložit ISE specifické funkce, jako jsou barev a písma vlastního nastavení v profilu CurrentUserCurrentHost pro Windows PowerShell ISE nebo AllUsersCurrentHost profil pro Windows PowerShell ISE.

Následují profily, které můžete vytvořit a použít v prostředí Windows PowerShell ISE. Každý profil je uložen na konkrétní cestu.

| Typ profilu | Cesta k profilu |
| --- | --- |
| **Aktuální uživatel, prostředí PowerShell ISE**| `$PROFILE.CurrentUserCurrentHost`, nebo `$PROFILE` |
| **Všichni uživatelé, prostředí PowerShell ISE**| `$PROFILE.AllUsersCurrentHost` |
| **Aktuální uživatel, všichni hostitelé**| `$PROFILE.CurrentUserAllHosts` |
| **Všichni uživatelé, všichni hostitelé** | `$PROFILE.AllUsersAllHosts` |

## <a name="to-create-a-new-profile"></a>Chcete-li vytvořit nový profil

Chcete-li vytvořit nové "aktuální uživatel, Windows PowerShell ISE" profilu, spusťte tento příkaz:

```powershell
if (!(Test-Path -Path $PROFILE ))
{ New-Item -Type File -Path $PROFILE -Force }
```

Chcete-li vytvořit nový "Všichni uživatelé, Windows PowerShell ISE" profilu, spusťte tento příkaz:

```powershell
if (!(Test-Path -Path $PROFILE.AllUsersCurrentHost))
{ New-Item -Type File -Path $PROFILE.AllUsersCurrentHost -Force }
```

Chcete-li vytvořit nový profil "aktuálního uživatele, všechny hostitelem", spusťte tento příkaz:

```powershell
if (!(Test-Path -Path $PROFILE.CurrentUserAllHosts))
{ New-Item -Type File -Path $PROFILE.CurrentUserAllHosts -Force }
```

Pokud chcete vytvořit nový profil "všichni uživatelé, všechny hostitelem", zadejte:

```powershell
if (!(Test-Path -Path $PROFILE.AllUsersAllHosts))
{ New-Item -Type File -Path $PROFILE.AllUsersAllHosts -Force }
```

## <a name="to-edit-a-profile"></a>Chcete-li upravit profil

1. Otevřete profil spuštění příkazu psedit s proměnnou, která určuje profil, který chcete upravit. Například, chcete-li otevřít "aktuálním uživatelem, Windows PowerShell ISE" profilu, zadejte: `psEdit $PROFILE`

2. Některé položky přidejte do svého profilu. Následuje několik příkladů, které vám pomůžou začít:

   - Chcete-li změnit výchozí barvu pozadí panelu konzoly na modrou typu souboru profilu: `$psISE.Options.OutputPaneBackground = 'blue'` . Další informace o proměnné $psISE najdete v tématu [referenční dokumentace objektového modelu Windows PowerShell ISE](object-model/The-ISE-Object-Model-Hierarchy.md).

   - Chcete-li změnit velikost písma na 20 typu souboru profilu: `$psISE.Options.FontSize =20`

3. K uložení souboru profilu na **souboru** nabídky, klikněte na tlačítko **Uložit**. Při příštím otevření prostředí PowerShell ISE Windows se použijí vlastní nastavení.

## <a name="see-also"></a>Viz také

- [about_Profiles](/powershell/module/microsoft.powershell.core/about/about_profiles)
- [Představení Windows PowerShell ISE](Introducing-the-Windows-PowerShell-ISE.md)