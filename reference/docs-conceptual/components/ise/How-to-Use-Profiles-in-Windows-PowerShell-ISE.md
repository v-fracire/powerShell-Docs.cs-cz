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
# <a name="how-to-use-profiles-in-windows-powershell-ise"></a><span data-ttu-id="6fefa-103">Použití profilů v prostředí Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="6fefa-103">How to Use Profiles in Windows PowerShell ISE</span></span>

<span data-ttu-id="6fefa-104">Toto téma vysvětluje, jak používat profily ve Windows Powershellu® integrovaném skriptovacím prostředí (ISE).</span><span class="sxs-lookup"><span data-stu-id="6fefa-104">This topic explains how to use Profiles in Windows PowerShell® Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="6fefa-105">Doporučujeme vám, před provedením úkolů v této části, abyste si přečetli [about_Profiles](/powershell/module/microsoft.powershell.core/about/about_profiles), nebo na panelu konzoly, typ, `Get-Help about_Profiles` a stiskněte klávesu **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="6fefa-105">We recommend that before performing the tasks in this section, you review [about_Profiles](/powershell/module/microsoft.powershell.core/about/about_profiles), or in the Console Pane, type, `Get-Help about_Profiles` and press **ENTER**.</span></span>

<span data-ttu-id="6fefa-106">Profil je skript Windows PowerShell ISE, který se spustí automaticky při spuštění nové relace.</span><span class="sxs-lookup"><span data-stu-id="6fefa-106">A profile is a Windows PowerShell ISE script that runs automatically when you start a new session.</span></span>  <span data-ttu-id="6fefa-107">Můžete vytvořit jeden nebo více profilů prostředí Windows PowerShell pro Windows PowerShell ISE a využít k přidání konfigurace prostředí Windows PowerShell nebo Windows PowerShell ISE Příprava pro své použití, s proměnnými, aliasy, funkce a barev a písem Předvolby, které chcete mít k dispozici.</span><span class="sxs-lookup"><span data-stu-id="6fefa-107">You can create one or more Windows PowerShell profiles for Windows PowerShell ISE and use them to add the configure the Windows PowerShell or Windows PowerShell ISE environment, preparing it for your use, with variables, aliases, functions, and color and font preferences that you want available.</span></span> <span data-ttu-id="6fefa-108">Profil, který ovlivňuje všechny Windows PowerShell ISE relace, kterou spouštíte.</span><span class="sxs-lookup"><span data-stu-id="6fefa-108">A profile affects every Windows PowerShell ISE session that you start.</span></span>

> [!NOTE]
> <span data-ttu-id="6fefa-109">Zásady spouštění prostředí Windows PowerShell Určuje, zda můžete spustit skripty a načíst profil.</span><span class="sxs-lookup"><span data-stu-id="6fefa-109">The Windows PowerShell execution policy determines whether you can run scripts and load a profile.</span></span> <span data-ttu-id="6fefa-110">Výchozí zásadu spouštění, "S omezeným přístupem," Zabraňuje všechny skripty spuštění, včetně profilů.</span><span class="sxs-lookup"><span data-stu-id="6fefa-110">The default execution policy, “Restricted,” prevents all scripts from running, including profiles.</span></span> <span data-ttu-id="6fefa-111">Pokud používáte zásady "Omezeno", nelze načíst profil.</span><span class="sxs-lookup"><span data-stu-id="6fefa-111">If you use the “Restricted” policy, the profile cannot load.</span></span> <span data-ttu-id="6fefa-112">Další informace o spuštění zásady, najdete v části [about_Execution_Policies](/powershell/module/microsoft.powershell.core/about/about_execution_policies).</span><span class="sxs-lookup"><span data-stu-id="6fefa-112">For more information about execution policy, see [about_Execution_Policies](/powershell/module/microsoft.powershell.core/about/about_execution_policies).</span></span>

## <a name="selecting-a-profile-to-use-in-the-windows-powershell-ise"></a><span data-ttu-id="6fefa-113">Vyberte profil, který chcete použít v prostředí Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="6fefa-113">Selecting a profile to use in the Windows PowerShell ISE</span></span>

<span data-ttu-id="6fefa-114">Windows PowerShell ISE podporuje profily pro aktuálního uživatele a všechny uživatele.</span><span class="sxs-lookup"><span data-stu-id="6fefa-114">Windows PowerShell ISE supports profiles for the current user and all users.</span></span> <span data-ttu-id="6fefa-115">Podporuje také profily Windows Powershellu, které se vztahují na všechny hostitele.</span><span class="sxs-lookup"><span data-stu-id="6fefa-115">It also supports the Windows PowerShell profiles that apply to all hosts.</span></span>

<span data-ttu-id="6fefa-116">Profil, který používáte se určuje podle způsobu použití prostředí Windows PowerShell a Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="6fefa-116">The profile that you use is determined by how you use Windows PowerShell and Windows PowerShell ISE.</span></span>

- <span data-ttu-id="6fefa-117">Pokud používáte pouze Windows PowerShell ISE ke spouštění prostředí Windows PowerShell, uložte všechny položky v jednom z ISE konkrétní profily, jako je například CurrentUserCurrentHost profil pro Windows PowerShell ISE nebo AllUsersCurrentHost pro Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="6fefa-117">If you use only Windows PowerShell ISE to run Windows PowerShell, then save all your items in one of the ISE-specific profiles, such as the CurrentUserCurrentHost profile for Windows PowerShell ISE or the AllUsersCurrentHost profile for Windows PowerShell ISE.</span></span>

- <span data-ttu-id="6fefa-118">Pokud používáte více hostitelských aplikací ke spouštění prostředí Windows PowerShell, uložte funkce, aliasy, proměnné a příkazy v profilu, který má vliv na všechny hostitele programy, jako je například CurrentUserAllHosts nebo profil AllUsersAllHosts a uložit ISE specifické funkce, jako jsou barev a písma vlastního nastavení v profilu CurrentUserCurrentHost pro Windows PowerShell ISE nebo AllUsersCurrentHost profil pro Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="6fefa-118">If you use multiple host programs to run Windows PowerShell, save your functions, aliases, variables, and commands in a profile that affects all host programs, such as the CurrentUserAllHosts or the AllUsersAllHosts profile, and save ISE-specific features, like color and font customization in the CurrentUserCurrentHost profile for Windows PowerShell ISE profile or the AllUsersCurrentHost profile for Windows PowerShell ISE.</span></span>

<span data-ttu-id="6fefa-119">Následují profily, které můžete vytvořit a použít v prostředí Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="6fefa-119">The following are profiles that can be created and used in Windows PowerShell ISE.</span></span> <span data-ttu-id="6fefa-120">Každý profil je uložen na konkrétní cestu.</span><span class="sxs-lookup"><span data-stu-id="6fefa-120">Each profile is saved to its own specific path.</span></span>

| <span data-ttu-id="6fefa-121">Typ profilu</span><span class="sxs-lookup"><span data-stu-id="6fefa-121">Profile Type</span></span> | <span data-ttu-id="6fefa-122">Cesta k profilu</span><span class="sxs-lookup"><span data-stu-id="6fefa-122">Profile Path</span></span> |
| --- | --- |
| <span data-ttu-id="6fefa-123">**Aktuální uživatel, prostředí PowerShell ISE**</span><span class="sxs-lookup"><span data-stu-id="6fefa-123">**Current user, PowerShell ISE**</span></span>| <span data-ttu-id="6fefa-124">`$PROFILE.CurrentUserCurrentHost`, nebo `$PROFILE`</span><span class="sxs-lookup"><span data-stu-id="6fefa-124">`$PROFILE.CurrentUserCurrentHost`, or `$PROFILE`</span></span> |
| <span data-ttu-id="6fefa-125">**Všichni uživatelé, prostředí PowerShell ISE**</span><span class="sxs-lookup"><span data-stu-id="6fefa-125">**All users, PowerShell ISE**</span></span>| `$PROFILE.AllUsersCurrentHost` |
| <span data-ttu-id="6fefa-126">**Aktuální uživatel, všichni hostitelé**</span><span class="sxs-lookup"><span data-stu-id="6fefa-126">**Current user, All hosts**</span></span>| `$PROFILE.CurrentUserAllHosts` |
| <span data-ttu-id="6fefa-127">**Všichni uživatelé, všichni hostitelé**</span><span class="sxs-lookup"><span data-stu-id="6fefa-127">**All users, All hosts**</span></span> | `$PROFILE.AllUsersAllHosts` |

## <a name="to-create-a-new-profile"></a><span data-ttu-id="6fefa-128">Chcete-li vytvořit nový profil</span><span class="sxs-lookup"><span data-stu-id="6fefa-128">To create a new profile</span></span>

<span data-ttu-id="6fefa-129">Chcete-li vytvořit nové "aktuální uživatel, Windows PowerShell ISE" profilu, spusťte tento příkaz:</span><span class="sxs-lookup"><span data-stu-id="6fefa-129">To create a new “Current user, Windows PowerShell ISE” profile, run this command:</span></span>

```powershell
if (!(Test-Path -Path $PROFILE ))
{ New-Item -Type File -Path $PROFILE -Force }
```

<span data-ttu-id="6fefa-130">Chcete-li vytvořit nový "Všichni uživatelé, Windows PowerShell ISE" profilu, spusťte tento příkaz:</span><span class="sxs-lookup"><span data-stu-id="6fefa-130">To create a new “All users, Windows PowerShell ISE” profile, run this command:</span></span>

```powershell
if (!(Test-Path -Path $PROFILE.AllUsersCurrentHost))
{ New-Item -Type File -Path $PROFILE.AllUsersCurrentHost -Force }
```

<span data-ttu-id="6fefa-131">Chcete-li vytvořit nový profil "aktuálního uživatele, všechny hostitelem", spusťte tento příkaz:</span><span class="sxs-lookup"><span data-stu-id="6fefa-131">To create a new “Current user, All Hosts” profile, run this command:</span></span>

```powershell
if (!(Test-Path -Path $PROFILE.CurrentUserAllHosts))
{ New-Item -Type File -Path $PROFILE.CurrentUserAllHosts -Force }
```

<span data-ttu-id="6fefa-132">Pokud chcete vytvořit nový profil "všichni uživatelé, všechny hostitelem", zadejte:</span><span class="sxs-lookup"><span data-stu-id="6fefa-132">To create a new “All users, All Hosts” profile, type:</span></span>

```powershell
if (!(Test-Path -Path $PROFILE.AllUsersAllHosts))
{ New-Item -Type File -Path $PROFILE.AllUsersAllHosts -Force }
```

## <a name="to-edit-a-profile"></a><span data-ttu-id="6fefa-133">Chcete-li upravit profil</span><span class="sxs-lookup"><span data-stu-id="6fefa-133">To edit a profile</span></span>

1. <span data-ttu-id="6fefa-134">Otevřete profil spuštění příkazu psedit s proměnnou, která určuje profil, který chcete upravit.</span><span class="sxs-lookup"><span data-stu-id="6fefa-134">To open the profile, run the command psedit with the variable that specifies the profile you want to edit.</span></span> <span data-ttu-id="6fefa-135">Například, chcete-li otevřít "aktuálním uživatelem, Windows PowerShell ISE" profilu, zadejte: `psEdit $PROFILE`</span><span class="sxs-lookup"><span data-stu-id="6fefa-135">For example, to open the “Current user, Windows PowerShell ISE” profile, type: `psEdit $PROFILE`</span></span>

2. <span data-ttu-id="6fefa-136">Některé položky přidejte do svého profilu.</span><span class="sxs-lookup"><span data-stu-id="6fefa-136">Add some items to your profile.</span></span> <span data-ttu-id="6fefa-137">Následuje několik příkladů, které vám pomůžou začít:</span><span class="sxs-lookup"><span data-stu-id="6fefa-137">The following are a few examples to get you started:</span></span>

   - <span data-ttu-id="6fefa-138">Chcete-li změnit výchozí barvu pozadí panelu konzoly na modrou typu souboru profilu: `$psISE.Options.OutputPaneBackground = 'blue'` .</span><span class="sxs-lookup"><span data-stu-id="6fefa-138">To change the default background color of the Console Pane to blue, in the profile file type: `$psISE.Options.OutputPaneBackground = 'blue'` .</span></span> <span data-ttu-id="6fefa-139">Další informace o proměnné $psISE najdete v tématu [referenční dokumentace objektového modelu Windows PowerShell ISE](object-model/The-ISE-Object-Model-Hierarchy.md).</span><span class="sxs-lookup"><span data-stu-id="6fefa-139">For more information about the $psISE variable, see [Windows PowerShell ISE Object Model Reference](object-model/The-ISE-Object-Model-Hierarchy.md).</span></span>

   - <span data-ttu-id="6fefa-140">Chcete-li změnit velikost písma na 20 typu souboru profilu: `$psISE.Options.FontSize =20`</span><span class="sxs-lookup"><span data-stu-id="6fefa-140">To change font size to 20, in the profile file type: `$psISE.Options.FontSize =20`</span></span>

3. <span data-ttu-id="6fefa-141">K uložení souboru profilu na **souboru** nabídky, klikněte na tlačítko **Uložit**.</span><span class="sxs-lookup"><span data-stu-id="6fefa-141">To save your profile file, on the **File** menu, click **Save**.</span></span> <span data-ttu-id="6fefa-142">Při příštím otevření prostředí PowerShell ISE Windows se použijí vlastní nastavení.</span><span class="sxs-lookup"><span data-stu-id="6fefa-142">Next time you open the Windows PowerShell ISE, your customizations are applied.</span></span>

## <a name="see-also"></a><span data-ttu-id="6fefa-143">Viz také</span><span class="sxs-lookup"><span data-stu-id="6fefa-143">See Also</span></span>

- [<span data-ttu-id="6fefa-144">about_Profiles</span><span class="sxs-lookup"><span data-stu-id="6fefa-144">about_Profiles</span></span>](/powershell/module/microsoft.powershell.core/about/about_profiles)
- [<span data-ttu-id="6fefa-145">Představení Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="6fefa-145">Introducing the Windows PowerShell ISE</span></span>](Introducing-the-Windows-PowerShell-ISE.md)