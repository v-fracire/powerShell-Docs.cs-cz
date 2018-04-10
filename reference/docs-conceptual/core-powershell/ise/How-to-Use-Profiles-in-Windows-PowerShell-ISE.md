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
---
# <a name="how-to-use-profiles-in-windows-powershell-ise"></a><span data-ttu-id="441ac-103">Použití profilů v prostředí Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="441ac-103">How to Use Profiles in Windows PowerShell ISE</span></span>

<span data-ttu-id="441ac-104">Toto téma vysvětluje, jak používat profily ve Windows PowerShell® Integrované skriptovací prostředí (ISE).</span><span class="sxs-lookup"><span data-stu-id="441ac-104">This topic explains how to use Profiles in Windows PowerShell® Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="441ac-105">Doporučujeme, abyste před provedením úlohy v této části, zkontrolovat [about_Profiles](/powershell/module/microsoft.powershell.core/about/about_profiles), nebo v podokně konzoly, typ, `Get-Help about_Profiles` a stiskněte klávesu **ENTER**.</span><span class="sxs-lookup"><span data-stu-id="441ac-105">We recommend that before performing the tasks in this section, you review [about_Profiles](/powershell/module/microsoft.powershell.core/about/about_profiles), or in the Console Pane, type, `Get-Help about_Profiles` and press **ENTER**.</span></span>

<span data-ttu-id="441ac-106">Profil je skript Windows PowerShell ISE, který automaticky spustí po spuštění novou relaci.</span><span class="sxs-lookup"><span data-stu-id="441ac-106">A profile is a Windows PowerShell ISE script that runs automatically when you start a new session.</span></span>  <span data-ttu-id="441ac-107">Můžete vytvořit jeden nebo více profilů prostředí Windows PowerShell pro Windows PowerShell ISE a použít je k přidání konfigurace prostředí Windows PowerShell nebo Windows PowerShell ISE, příprava pro vaše použití s proměnnými, aliasy, funkce a barev a písem Předvolby, které chcete mít k dispozici.</span><span class="sxs-lookup"><span data-stu-id="441ac-107">You can create one or more Windows PowerShell profiles for Windows PowerShell ISE and use them to add the configure the Windows PowerShell or Windows PowerShell ISE environment, preparing it for your use, with variables, aliases, functions, and color and font preferences that you want available.</span></span> <span data-ttu-id="441ac-108">Profil ovlivňuje všechny Windows PowerShell ISE relace, kterou spouštíte.</span><span class="sxs-lookup"><span data-stu-id="441ac-108">A profile affects every Windows PowerShell ISE session that you start.</span></span>

> [!NOTE]
> <span data-ttu-id="441ac-109">Zásady spouštění prostředí Windows PowerShell Určuje, zda můžete spouštět skripty a načíst profil.</span><span class="sxs-lookup"><span data-stu-id="441ac-109">The Windows PowerShell execution policy determines whether you can run scripts and load a profile.</span></span> <span data-ttu-id="441ac-110">Výchozí zásady spouštění, "S omezeným přístupem," Zabraňuje všechny skripty spuštění, včetně profily.</span><span class="sxs-lookup"><span data-stu-id="441ac-110">The default execution policy, “Restricted,” prevents all scripts from running, including profiles.</span></span> <span data-ttu-id="441ac-111">Pokud použijete zásady "S omezeným přístupem", nelze načíst profil.</span><span class="sxs-lookup"><span data-stu-id="441ac-111">If you use the “Restricted” policy, the profile cannot load.</span></span> <span data-ttu-id="441ac-112">Další informace o provádění zásad najdete v tématu [about_Execution_Policies](/powershell/module/microsoft.powershell.core/about/about_execution_policies).</span><span class="sxs-lookup"><span data-stu-id="441ac-112">For more information about execution policy, see [about_Execution_Policies](/powershell/module/microsoft.powershell.core/about/about_execution_policies).</span></span>

## <a name="selecting-a-profile-to-use-in-the-windows-powershell-ise"></a><span data-ttu-id="441ac-113">Výběr profilu pro použití v systému Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="441ac-113">Selecting a profile to use in the Windows PowerShell ISE</span></span>

<span data-ttu-id="441ac-114">Windows PowerShell ISE podporuje profily pro aktuálního uživatele a všichni uživatelé.</span><span class="sxs-lookup"><span data-stu-id="441ac-114">Windows PowerShell ISE supports profiles for the current user and all users.</span></span> <span data-ttu-id="441ac-115">Podporuje také profily prostředí Windows PowerShell, které platí pro všechny hostitele.</span><span class="sxs-lookup"><span data-stu-id="441ac-115">It also supports the Windows PowerShell profiles that apply to all hosts.</span></span>

<span data-ttu-id="441ac-116">Profil, který používáte, je určen podle způsobu použití prostředí Windows PowerShell a Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="441ac-116">The profile that you use is determined by how you use Windows PowerShell and Windows PowerShell ISE.</span></span>

- <span data-ttu-id="441ac-117">Pokud používáte pouze ISE Windows PowerShell ke spouštění prostředí Windows PowerShell, uložte všechny položky v jednom ISE konkrétní profilů, jako je například CurrentUserCurrentHost profil pro Windows PowerShell ISE nebo AllUsersCurrentHost pro Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="441ac-117">If you use only Windows PowerShell ISE to run Windows PowerShell, then save all your items in one of the ISE-specific profiles, such as the CurrentUserCurrentHost profile for Windows PowerShell ISE or the AllUsersCurrentHost profile for Windows PowerShell ISE.</span></span>

- <span data-ttu-id="441ac-118">Pokud používáte více hostitelských aplikací ke spouštění prostředí Windows PowerShell, uložte funkce, aliasy, proměnné a příkazy v profilu, který má vliv na všechny hostitele programy, jako je například CurrentUserAllHosts nebo AllUsersAllHosts a uložit ISE specifické funkce, jako je barev a písem vlastní nastavení v profilu CurrentUserCurrentHost profil Windows PowerShell ISE nebo AllUsersCurrentHost pro Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="441ac-118">If you use multiple host programs to run Windows PowerShell, save your functions, aliases, variables, and commands in a profile that affects all host programs, such as the CurrentUserAllHosts or the AllUsersAllHosts profile, and save ISE-specific features, like color and font customization in the CurrentUserCurrentHost profile for Windows PowerShell ISE profile or the AllUsersCurrentHost profile for Windows PowerShell ISE.</span></span>

<span data-ttu-id="441ac-119">Níže jsou uvedeny profily, které můžete vytvořit a použít v systému Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="441ac-119">The following are profiles that can be created and used in Windows PowerShell ISE.</span></span> <span data-ttu-id="441ac-120">Každý profil je uložen na konkrétní cestu.</span><span class="sxs-lookup"><span data-stu-id="441ac-120">Each profile is saved to its own specific path.</span></span>

| <span data-ttu-id="441ac-121">Typ profilu</span><span class="sxs-lookup"><span data-stu-id="441ac-121">Profile Type</span></span> | <span data-ttu-id="441ac-122">Cesta profilu</span><span class="sxs-lookup"><span data-stu-id="441ac-122">Profile Path</span></span> |
| --- | --- |
| <span data-ttu-id="441ac-123">**Aktuální uživatel, prostředí PowerShell ISE**</span><span class="sxs-lookup"><span data-stu-id="441ac-123">**Current user, PowerShell ISE**</span></span>| <span data-ttu-id="441ac-124">`$PROFILE.CurrentUserCurrentHost`, nebo `$PROFILE`</span><span class="sxs-lookup"><span data-stu-id="441ac-124">`$PROFILE.CurrentUserCurrentHost`, or `$PROFILE`</span></span> |
| <span data-ttu-id="441ac-125">**Všichni uživatelé, prostředí PowerShell ISE**</span><span class="sxs-lookup"><span data-stu-id="441ac-125">**All users, PowerShell ISE**</span></span>| `$PROFILE.AllUsersCurrentHost` |
| <span data-ttu-id="441ac-126">**Aktuální uživatel, všechny hostitele**</span><span class="sxs-lookup"><span data-stu-id="441ac-126">**Current user, All hosts**</span></span>| `$PROFILE.CurrentUserAllHosts` |
| <span data-ttu-id="441ac-127">**Všichni uživatelé, všechny hostitele**</span><span class="sxs-lookup"><span data-stu-id="441ac-127">**All users, All hosts**</span></span> | `$PROFILE.AllUsersAllHosts` |

## <a name="to-create-a-new-profile"></a><span data-ttu-id="441ac-128">Chcete-li vytvořit nový profil</span><span class="sxs-lookup"><span data-stu-id="441ac-128">To create a new profile</span></span>

<span data-ttu-id="441ac-129">Chcete-li vytvořit nové "aktuální uživatel, Windows PowerShell ISE" profil, spusťte tento příkaz:</span><span class="sxs-lookup"><span data-stu-id="441ac-129">To create a new “Current user, Windows PowerShell ISE” profile, run this command:</span></span>

```powershell
if (!(Test-Path -Path $PROFILE ))
{ New-Item -Type File -Path $PROFILE -Force }
```

<span data-ttu-id="441ac-130">Chcete-li vytvořit novou "Všichni uživatelé, Windows PowerShell ISE" profil, spusťte tento příkaz:</span><span class="sxs-lookup"><span data-stu-id="441ac-130">To create a new “All users, Windows PowerShell ISE” profile, run this command:</span></span>

```powershell
if (!(Test-Path -Path $PROFILE.AllUsersCurrentHost))
{ New-Item -Type File -Path $PROFILE.AllUsersCurrentHost -Force }
```

<span data-ttu-id="441ac-131">Chcete-li vytvořit nový profil "aktuální uživatel všechny hostitelem", spusťte tento příkaz:</span><span class="sxs-lookup"><span data-stu-id="441ac-131">To create a new “Current user, All Hosts” profile, run this command:</span></span>

```powershell
if (!(Test-Path -Path $PROFILE.CurrentUserAllHosts))
{ New-Item -Type File -Path $PROFILE.CurrentUserAllHosts -Force }
```

<span data-ttu-id="441ac-132">Chcete-li vytvořit nový profil "všichni uživatelé, všechny hostitelem", zadejte:</span><span class="sxs-lookup"><span data-stu-id="441ac-132">To create a new “All users, All Hosts” profile, type:</span></span>

```powershell
if (!(Test-Path -Path $PROFILE.AllUsersAllHosts))
{ New-Item -Type File -Path $PROFILE.AllUsersAllHosts -Force }
```

## <a name="to-edit-a-profile"></a><span data-ttu-id="441ac-133">Chcete-li upravit profil</span><span class="sxs-lookup"><span data-stu-id="441ac-133">To edit a profile</span></span>

1. <span data-ttu-id="441ac-134">Chcete-li spustit tento profil, spusťte příkaz psedit s proměnné, která určuje profil, který chcete upravit.</span><span class="sxs-lookup"><span data-stu-id="441ac-134">To open the profile, run the command psedit with the variable that specifies the profile you want to edit.</span></span> <span data-ttu-id="441ac-135">Chcete-li například otevřete "aktuální uživatel, Windows PowerShell ISE" profilu, zadejte: `psEdit $PROFILE`</span><span class="sxs-lookup"><span data-stu-id="441ac-135">For example, to open the “Current user, Windows PowerShell ISE” profile, type: `psEdit $PROFILE`</span></span>

2. <span data-ttu-id="441ac-136">Některé položky přidáte do vašeho profilu.</span><span class="sxs-lookup"><span data-stu-id="441ac-136">Add some items to your profile.</span></span> <span data-ttu-id="441ac-137">Následuje několik příkladů, jak začít:</span><span class="sxs-lookup"><span data-stu-id="441ac-137">The following are a few examples to get you started:</span></span>

   - <span data-ttu-id="441ac-138">Chcete-li změnit výchozí barvu pozadí panelu konzoly na modrou v souboru typ profilu: `$psISE.Options.OutputPaneBackground = 'blue'` .</span><span class="sxs-lookup"><span data-stu-id="441ac-138">To change the default background color of the Console Pane to blue, in the profile file type: `$psISE.Options.OutputPaneBackground = 'blue'` .</span></span> <span data-ttu-id="441ac-139">Další informace o $psISE proměnné najdete v tématu [odkaz na Windows PowerShell ISE objektu modelu](The-ISE-Object-Model-Hierarchy.md).</span><span class="sxs-lookup"><span data-stu-id="441ac-139">For more information about the $psISE variable, see [Windows PowerShell ISE Object Model Reference](The-ISE-Object-Model-Hierarchy.md).</span></span>

   - <span data-ttu-id="441ac-140">Chcete-li změnit velikost písma až 20 číslic v profilu typ souboru: `$psISE.Options.FontSize =20`</span><span class="sxs-lookup"><span data-stu-id="441ac-140">To change font size to 20, in the profile file type: `$psISE.Options.FontSize =20`</span></span>

3. <span data-ttu-id="441ac-141">Uložte soubor profilu, na **soubor** nabídky, klikněte na tlačítko **Uložit**.</span><span class="sxs-lookup"><span data-stu-id="441ac-141">To save your profile file, on the **File** menu, click **Save**.</span></span> <span data-ttu-id="441ac-142">Při příštím otevření Windows PowerShell ISE, vaše vlastní nastavení se projeví.</span><span class="sxs-lookup"><span data-stu-id="441ac-142">Next time you open the Windows PowerShell ISE, your customizations are applied.</span></span>

## <a name="see-also"></a><span data-ttu-id="441ac-143">Viz také</span><span class="sxs-lookup"><span data-stu-id="441ac-143">See Also</span></span>

- [<span data-ttu-id="441ac-144">about_Profiles</span><span class="sxs-lookup"><span data-stu-id="441ac-144">about_Profiles</span></span>](/powershell/module/microsoft.powershell.core/about/about_profiles)
- [<span data-ttu-id="441ac-145">Představení Windows PowerShell ISE</span><span class="sxs-lookup"><span data-stu-id="441ac-145">Introducing the Windows PowerShell ISE</span></span>](Introducing-the-Windows-PowerShell-ISE.md)