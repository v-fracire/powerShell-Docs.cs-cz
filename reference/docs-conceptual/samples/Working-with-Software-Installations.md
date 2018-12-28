---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Práce s nainstalovaným softwarem
ms.assetid: 51a12fe9-95f6-4ffc-81a5-4fa72a5bada9
ms.openlocfilehash: bb97ad37c4295351c0fc2e3c6e1209c8dd673f06
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404102"
---
# <a name="working-with-software-installations"></a><span data-ttu-id="23a5b-103">Práce s nainstalovaným softwarem</span><span class="sxs-lookup"><span data-stu-id="23a5b-103">Working with Software Installations</span></span>

<span data-ttu-id="23a5b-104">Aplikace, které jsou navrženy pro použití Instalační služby systému Windows je přístupná prostřednictvím služby WMI **objektu Win32_Product** třídy, ale u některých aplikací není používán Dnes pomocí Instalační služby systému Windows.</span><span class="sxs-lookup"><span data-stu-id="23a5b-104">Applications that are designed to use Windows Installer can be accessed through WMI's **Win32_Product** class, but not all applications in use today use the Windows Installer.</span></span> <span data-ttu-id="23a5b-105">Vzhledem k tomu, že instalační služby systému Windows poskytuje širokou škálu standardní techniky pro práci s instalovat aplikace, jsme se soustředí hlavně na těchto aplikací.</span><span class="sxs-lookup"><span data-stu-id="23a5b-105">Because the Windows Installer provides the widest range of standard techniques for working with installable applications, we will focus primarily on those applications.</span></span> <span data-ttu-id="23a5b-106">Aplikace, které používají rutiny alternativní nastavení nebude obecně spravovaný Instalační služby systému Windows.</span><span class="sxs-lookup"><span data-stu-id="23a5b-106">Applications that use alternate setup routines will generally not be managed by the Windows Installer.</span></span> <span data-ttu-id="23a5b-107">Konkrétní postupy pro práci s těmito aplikacemi bude záviset na instalační program softwaru a rozhodnutí vývojáře aplikace.</span><span class="sxs-lookup"><span data-stu-id="23a5b-107">Specific techniques for working with those applications will depend on the installer software and decisions made by the application developer.</span></span>

> [!NOTE]
> <span data-ttu-id="23a5b-108">Aplikace, které jsou nainstalovány pomocí kopírování souborů aplikace do počítače obvykle nelze spravovat pomocí technik popsaných tady.</span><span class="sxs-lookup"><span data-stu-id="23a5b-108">Applications that are installed by copying the application files to the computer usually cannot be managed by using techniques discussed here.</span></span> <span data-ttu-id="23a5b-109">Tyto aplikace jako soubory a složky, můžete spravovat pomocí technik popsaných v části "Práce se soubory a složky".</span><span class="sxs-lookup"><span data-stu-id="23a5b-109">You can manage these applications as files and folders by using the techniques discussed in the "Working With Files and Folders" section.</span></span>

### <a name="listing-windows-installer-applications"></a><span data-ttu-id="23a5b-110">Výpis aplikací Instalační služby systému Windows</span><span class="sxs-lookup"><span data-stu-id="23a5b-110">Listing Windows Installer Applications</span></span>

<span data-ttu-id="23a5b-111">K zobrazení seznamu aplikací nainstalovaných Instalační služby systému Windows na místním nebo vzdáleném systému, použijte následující jednoduchý dotaz rozhraní WMI:</span><span class="sxs-lookup"><span data-stu-id="23a5b-111">To list the applications installed with the Windows Installer on a local or remote system, use the following simple WMI query:</span></span>

```
PS> Get-WmiObject -Class Win32_Product -ComputerName .

IdentifyingNumber : {7131646D-CD3C-40F4-97B9-CD9E4E6262EF}
Name              : Microsoft .NET Framework 2.0
Vendor            : Microsoft Corporation
Version           : 2.0.50727
Caption           : Microsoft .NET Framework 2.0
```

<span data-ttu-id="23a5b-112">Chcete-li zobrazit všechny vlastnosti objektu Win32_Product objektu na obrazovce, použijte parametr vlastnosti formátování rutin, jako je například rutinu Format-List s hodnotou \* (vše).</span><span class="sxs-lookup"><span data-stu-id="23a5b-112">To display all of the properties of the Win32_Product object to the display, use the Properties parameter of the formatting cmdlets, such as the Format-List cmdlet, with a value of \* (all).</span></span>

```
PS> Get-WmiObject -Class Win32_Product -ComputerName . | Where-Object -FilterScript {$_.Name -eq "Microsoft .NET Framework 2.0"} | Format-List -Property *

Name              : Microsoft .NET Framework 2.0
Version           : 2.0.50727
InstallState      : 5
Caption           : Microsoft .NET Framework 2.0
Description       : Microsoft .NET Framework 2.0
IdentifyingNumber : {7131646D-CD3C-40F4-97B9-CD9E4E6262EF}
InstallDate       : 20060506
InstallDate2      : 20060506000000.000000-000
InstallLocation   :
PackageCache      : C:\WINDOWS\Installer\619ab2.msi
SKUNumber         :
Vendor            : Microsoft Corporation
```

<span data-ttu-id="23a5b-113">Nebo můžete použít **Get-WmiObject filtr** parametr vybrat jenom rozhraní Microsoft .NET Framework 2.0.</span><span class="sxs-lookup"><span data-stu-id="23a5b-113">Or, you could use the **Get-WmiObject Filter** parameter to select only Microsoft .NET Framework 2.0.</span></span> <span data-ttu-id="23a5b-114">Vzhledem k tomu, že filtr použité v tomto příkazu je filtr rozhraní WMI, používá syntaxi dotazu jazyka WQL (WMI), není syntaxe prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="23a5b-114">Because the filter used in this command is a WMI filter, it uses WMI Query Language (WQL) syntax, not Windows PowerShell syntax.</span></span> <span data-ttu-id="23a5b-115">Místo toho:</span><span class="sxs-lookup"><span data-stu-id="23a5b-115">Instead,:</span></span>

```powershell
Get-WmiObject -Class Win32_Product -ComputerName . -Filter "Name='Microsoft .NET Framework 2.0'"| Format-List -Property *
```

<span data-ttu-id="23a5b-116">Všimněte si, že dotazy WQL často znaky, jako jsou mezery ani rovnítko, které mají speciální význam v prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="23a5b-116">Note that WQL queries frequently use characters, such as spaces or equal signs, that have a special meaning in Windows PowerShell.</span></span> <span data-ttu-id="23a5b-117">Z tohoto důvodu je vhodné vždy hodnotu parametru filtru uzavřete do uvozovek.</span><span class="sxs-lookup"><span data-stu-id="23a5b-117">For this reason, it is prudent to always enclose the value of the Filter parameter in quotation marks.</span></span> <span data-ttu-id="23a5b-118">Můžete také použít řídicí znak prostředí Windows PowerShell prvními (\`), i když je možná lepší čitelnost.</span><span class="sxs-lookup"><span data-stu-id="23a5b-118">You can also use the Windows PowerShell escape character, a backtick (\`), although it may not improve readability.</span></span> <span data-ttu-id="23a5b-119">Následující příkaz je ekvivalentní předchozí příkaz vrátí stejné výsledky, ale prvními používá k uvození zvláštní znaky, namísto uvozovky u filtru celý řetězec.</span><span class="sxs-lookup"><span data-stu-id="23a5b-119">The following command is equivalent to the previous command and returns the same results, but uses the backtick to escape special characters, instead of quoting the entire filter string.</span></span>

```powershell
Get-WmiObject -Class Win32_Product -ComputerName . -Filter Name`=`'Microsoft` .NET` Framework` 2.0`' | Format-List -Property *
```

<span data-ttu-id="23a5b-120">K zobrazení seznamu pouze vlastnosti, které vás zajímají, použijte vlastnost parametru formátování rutin seznam požadovaných vlastností.</span><span class="sxs-lookup"><span data-stu-id="23a5b-120">To list only the properties that interest you, use the Property parameter of the formatting cmdlets to list the desired properties.</span></span>

```
Get-WmiObject -Class Win32_Product -ComputerName . | Format-List -Property Name,InstallDate,InstallLocation,PackageCache,Vendor,Version,IdentifyingNumber
...
Name              : HighMAT Extension to Microsoft Windows XP CD Writing Wizard
InstallDate       : 20051022
InstallLocation   : C:\Program Files\HighMAT CD Writing Wizard\
PackageCache      : C:\WINDOWS\Installer\113b54.msi
Vendor            : Microsoft Corporation
Version           : 1.1.1905.1
IdentifyingNumber : {FCE65C4E-B0E8-4FBD-AD16-EDCBE6CD591F}
...
```

<span data-ttu-id="23a5b-121">A konečně k vyhledání pouze názvy nainstalovaných aplikací, jednoduché **formátu celou** zjednodušuje výstup příkazu:</span><span class="sxs-lookup"><span data-stu-id="23a5b-121">Finally, to find only the names of installed applications, a simple **Format-Wide** statement simplifies the output:</span></span>

```powershell
Get-WmiObject -Class Win32_Product -ComputerName .  | Format-Wide -Column 1
```

<span data-ttu-id="23a5b-122">I když teď máme několik způsobů, jak podívejte se na aplikace, které se používá pro instalace Instalační služby systému Windows, jsme nebyly považovány za jiné aplikace.</span><span class="sxs-lookup"><span data-stu-id="23a5b-122">Although we now have several ways to look at applications that used the Windows Installer for installation, we have not considered other applications.</span></span> <span data-ttu-id="23a5b-123">Vzhledem k tomu, že většinu standardních aplikací zaregistrovat jejich odinstalační program s Windows, budeme pracovat s těmi, která místně, hledání v registru Windows.</span><span class="sxs-lookup"><span data-stu-id="23a5b-123">Because most standard applications register their uninstaller with Windows, we can work with those locally by finding them in the Windows registry.</span></span>

### <a name="listing-all-uninstallable-applications"></a><span data-ttu-id="23a5b-124">Výpis všech aplikací bez možnosti odinstalace</span><span class="sxs-lookup"><span data-stu-id="23a5b-124">Listing All Uninstallable Applications</span></span>

<span data-ttu-id="23a5b-125">Ačkoli neexistuje žádné zaručené způsob, jak najít všechny aplikace v systému, je možné najít všechny programy s výpisy zobrazí v dialogovém okně Přidat nebo odebrat programy.</span><span class="sxs-lookup"><span data-stu-id="23a5b-125">Although there is no guaranteed way to find every application on a system, it is possible to find all programs with listings displayed in the Add or Remove Programs dialog box.</span></span> <span data-ttu-id="23a5b-126">Přidat nebo odebrat programy najde tyto aplikace v následujícím klíči registru:</span><span class="sxs-lookup"><span data-stu-id="23a5b-126">Add or Remove Programs finds these applications in the following registry key:</span></span>

<span data-ttu-id="23a5b-127">**HKEY_LOCAL_MACHINE\\softwaru\\Microsoft\\Windows\\CurrentVersion\\odinstalovat**.</span><span class="sxs-lookup"><span data-stu-id="23a5b-127">**HKEY_LOCAL_MACHINE\\Software\\Microsoft\\Windows\\CurrentVersion\\Uninstall**.</span></span>

<span data-ttu-id="23a5b-128">Můžeme také můžete prozkoumat tento klíč chcete hledat aplikace.</span><span class="sxs-lookup"><span data-stu-id="23a5b-128">We can also examine this key to find applications.</span></span> <span data-ttu-id="23a5b-129">Aby bylo snazší zobrazit klíč odinstalovat, jsme namapujete jednotku prostředí Windows PowerShell do tohoto umístění registru:</span><span class="sxs-lookup"><span data-stu-id="23a5b-129">To make it easier to view the Uninstall key, we can map a Windows PowerShell drive to this registry location:</span></span>

```
PS> New-PSDrive -Name Uninstall -PSProvider Registry -Root HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Uninstall

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
Uninstall  Registry      HKEY_LOCAL_MACHINE\SOFTWARE\Micr...
```

> [!NOTE]
> <span data-ttu-id="23a5b-130">**HKLM:** jednotka mapovaná do kořenového adresáře **HKEY_LOCAL_MACHINE**, takže jsme použili v cestě ke klíči odinstalovat tuto jednotku.</span><span class="sxs-lookup"><span data-stu-id="23a5b-130">The **HKLM:** drive is mapped to the root of **HKEY_LOCAL_MACHINE**, so we used that drive in the path to the Uninstall key.</span></span> <span data-ttu-id="23a5b-131">Místo **HKLM:** jsme mohli zadali cestu registru pomocí **HKLM** nebo **HKEY_LOCAL_MACHINE**.</span><span class="sxs-lookup"><span data-stu-id="23a5b-131">Instead of **HKLM:** we could have specified the registry path by using either **HKLM** or **HKEY_LOCAL_MACHINE**.</span></span> <span data-ttu-id="23a5b-132">Výhodou použití existujícího disku registru je, že jsme dokončování pomocí tabulátoru – použít tak, aby vyplnil v názvech klíčů, takže jsme není potřeba je zadat.</span><span class="sxs-lookup"><span data-stu-id="23a5b-132">The advantage of using an existing registry drive is that we can use tab-completion to fill in the keys names, so we do not need to type them.</span></span>

<span data-ttu-id="23a5b-133">Teď máme jednotky s názvem "Odinstalovat", který je možné rychle a jednoduše vyhledejte instalace aplikací.</span><span class="sxs-lookup"><span data-stu-id="23a5b-133">We now have a drive named "Uninstall" that can be used to quickly and conveniently look for application installations.</span></span> <span data-ttu-id="23a5b-134">Počet nainstalovaných aplikací nám můžete najít určeno spočítáním počet klíčů registru v odinstalaci: Jednotku prostředí Windows PowerShell:</span><span class="sxs-lookup"><span data-stu-id="23a5b-134">We can find the number of installed applications by counting the number of registry keys in the Uninstall: Windows PowerShell drive:</span></span>

```
PS> (Get-ChildItem -Path Uninstall:).Count
459
```

<span data-ttu-id="23a5b-135">Jsme můžete hledat v seznamu aplikací dál pomocí celé řady metod, počínaje **Get-ChildItem**.</span><span class="sxs-lookup"><span data-stu-id="23a5b-135">We can search this list of applications further by using a variety of techniques, beginning with **Get-ChildItem**.</span></span> <span data-ttu-id="23a5b-136">Chcete získat seznam aplikací a uložit je do **$UninstallableApplications** proměnné, použijte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="23a5b-136">To get a list of applications and save them in the **$UninstallableApplications** variable, use the following command:</span></span>

```powershell
$UninstallableApplications = Get-ChildItem -Path Uninstall:
```

> [!NOTE]
> <span data-ttu-id="23a5b-137">Dlouhý název proměnné pro přehlednost používáme.</span><span class="sxs-lookup"><span data-stu-id="23a5b-137">We are using a lengthy variable name here for clarity.</span></span> <span data-ttu-id="23a5b-138">V praxi neexistuje žádný důvod používat dlouhé názvy.</span><span class="sxs-lookup"><span data-stu-id="23a5b-138">In actual use, there is no reason to use long names.</span></span> <span data-ttu-id="23a5b-139">I když používáte – dokončování pomocí tabulátoru pro názvy proměnných, můžete také použít 1 – 2 znaky názvu pro rychlost.</span><span class="sxs-lookup"><span data-stu-id="23a5b-139">Although you can use tab-completion for variable names, you can also use 1-2 character names for speed.</span></span> <span data-ttu-id="23a5b-140">Delší a popisné názvy jsou nejužitečnější, když vyvíjíte kód pro další použití.</span><span class="sxs-lookup"><span data-stu-id="23a5b-140">Longer, descriptive names are most useful when you are developing code for reuse.</span></span>

<span data-ttu-id="23a5b-141">K zobrazení hodnot z položky registru v klíčích registru pod odinstalovat, použijte metodu GetValue klíče registru.</span><span class="sxs-lookup"><span data-stu-id="23a5b-141">To display the values of the registry entries in the registry keys under Uninstall, use the GetValue method of the registry keys.</span></span> <span data-ttu-id="23a5b-142">Hodnota metody je název položky registru.</span><span class="sxs-lookup"><span data-stu-id="23a5b-142">The value of the method is the name of the registry entry.</span></span>

<span data-ttu-id="23a5b-143">Například pokud chcete vyhledat názvy zobrazení aplikací v klíči odinstalovat, použijte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="23a5b-143">For example, to find the display names of applications in the Uninstall key, use the following command:</span></span>

```powershell
Get-ChildItem -Path Uninstall: | ForEach-Object -Process { $_.GetValue('DisplayName') }
```

<span data-ttu-id="23a5b-144">Není zaručeno, že tyto hodnoty jsou jedinečné.</span><span class="sxs-lookup"><span data-stu-id="23a5b-144">There is no guarantee that these values are unique.</span></span> <span data-ttu-id="23a5b-145">Dva nainstalované položky se zobrazí jako "Windows Media Encoder 9 Series" v následujícím příkladu:</span><span class="sxs-lookup"><span data-stu-id="23a5b-145">In the following example, two installed items appear as "Windows Media Encoder 9 Series":</span></span>

```
PS> Get-ChildItem -Path Uninstall: | Where-Object -FilterScript { $_.GetValue("DisplayName") -eq "Windows Media Encoder 9 Series"}

   Hive: Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Micros
oft\Windows\CurrentVersion\Uninstall

SKC  VC Name                           Property
---  -- ----                           --------
  0   3 Windows Media Encoder 9        {DisplayName, DisplayIcon, UninstallS...
  0  24 {E38C00D0-A68B-4318-A8A6-F7... {AuthorizedCDFPrefix, Comments, Conta...
```

### <a name="installing-applications"></a><span data-ttu-id="23a5b-146">Instalace aplikací</span><span class="sxs-lookup"><span data-stu-id="23a5b-146">Installing Applications</span></span>

<span data-ttu-id="23a5b-147">Můžete použít **objektu Win32_Product** třídy nainstalovat balíčky Instalační služby systému Windows, vzdáleně nebo místně.</span><span class="sxs-lookup"><span data-stu-id="23a5b-147">You can use the **Win32_Product** class to install Windows Installer packages, remotely or locally.</span></span>

> [!NOTE]
> <span data-ttu-id="23a5b-148">Ve Windows Vista, Windows Server 2008 a novějších verzích Windows jak nainstalovat aplikaci, je nutné spustit prostředí Windows PowerShell pomocí možnosti "Spustit jako správce".</span><span class="sxs-lookup"><span data-stu-id="23a5b-148">On Windows Vista, Windows Server 2008, and later versions of Windows, to install an application, you must start Windows PowerShell with the "Run as administrator" option.</span></span>

<span data-ttu-id="23a5b-149">Při instalaci vzdáleně, použijte cestu sítě (Universal Naming Convention) pro zadání cesty k balíčku MSI, protože subsystém rozhraní WMI nerozumí cest prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="23a5b-149">When installing remotely, use a Universal Naming Convention (UNC) network path to specify the path to the .msi package, because the WMI subsystem does not understand Windows PowerShell paths.</span></span> <span data-ttu-id="23a5b-150">Například k instalaci balíčku NewPackage.msi umístěný ve sdílené síťové složce \\ \\AppServ\\dsp na vzdáleném počítači PC01, zadejte následující příkaz na příkazovém řádku Windows Powershellu:</span><span class="sxs-lookup"><span data-stu-id="23a5b-150">For example, to install the NewPackage.msi package located in the network share \\\\AppServ\\dsp on the remote computer PC01, type the following command at the Windows PowerShell prompt:</span></span>

```powershell
(Get-WMIObject -ComputerName PC01 -List | Where-Object -FilterScript {$_.Name -eq 'Win32_Product'}).Install(\\AppSrv\dsp\NewPackage.msi)
```

<span data-ttu-id="23a5b-151">Aplikace, které nepoužívají technologie instalačního programu Windows mohou mít metody specifické pro aplikaci pro automatické nasazení.</span><span class="sxs-lookup"><span data-stu-id="23a5b-151">Applications that do not use Windows Installer technology may have application-specific methods available for automated deployment.</span></span> <span data-ttu-id="23a5b-152">Pokud chcete zjistit, zda je metoda pro automatizaci nasazení, naleznete v dokumentaci k aplikaci nebo se obraťte na systém pro podporu dodavatele aplikace.</span><span class="sxs-lookup"><span data-stu-id="23a5b-152">To determine whether there is a method for deployment automation, check the documentation for the application or consult the application vendor's support system.</span></span> <span data-ttu-id="23a5b-153">V některých případech i v případě, že na dodavatele aplikace není návrhu konkrétně aplikace pro automatizaci instalace, pravděpodobně výrobce instalačního programu softwaru některé postupy pro automatizaci.</span><span class="sxs-lookup"><span data-stu-id="23a5b-153">In some cases, even if the application vendor did not specifically design the application for installation automation, the installer software manufacturer may have some techniques for automation.</span></span>

### <a name="removing-applications"></a><span data-ttu-id="23a5b-154">Odebírání aplikací</span><span class="sxs-lookup"><span data-stu-id="23a5b-154">Removing Applications</span></span>

<span data-ttu-id="23a5b-155">Odebírá se balíček Instalační služby systému Windows pomocí prostředí Windows PowerShell funguje v přibližně stejným způsobem jako instalaci balíčku.</span><span class="sxs-lookup"><span data-stu-id="23a5b-155">Removing a Windows Installer package by using Windows PowerShell works in approximately the same way as installing a package.</span></span> <span data-ttu-id="23a5b-156">Tady je příklad, který vybere balíček odinstalovat na základě jeho názvu; v některých případech může být jednodušší filtr s **IdentifyingNumber**:</span><span class="sxs-lookup"><span data-stu-id="23a5b-156">Here is an example that selects the package to uninstall based on its name; in some cases it may be easier to filter with the **IdentifyingNumber**:</span></span>

```powershell
(Get-WmiObject -Class Win32_Product -Filter "Name='ILMerge'" -ComputerName . ).Uninstall()
```

<span data-ttu-id="23a5b-157">Odebrání dalších aplikací není tak jednoduché to zase, i když dělat místně.</span><span class="sxs-lookup"><span data-stu-id="23a5b-157">Removing other applications is not quite so simple, even when done locally.</span></span> <span data-ttu-id="23a5b-158">Jsme najít odinstalace řetězce příkazového řádku pro tyto aplikace tak, že extrahují **UninstallString** vlastnost.</span><span class="sxs-lookup"><span data-stu-id="23a5b-158">We can find the command line uninstallation strings for these applications by extracting the **UninstallString** property.</span></span> <span data-ttu-id="23a5b-159">Tato metoda funguje pro aplikace Instalační služby systému Windows a pro starší programy uvedené pod klíčem odinstalace:</span><span class="sxs-lookup"><span data-stu-id="23a5b-159">This method works for Windows Installer applications and for older programs appearing under the Uninstall key:</span></span>

```powershell
Get-ChildItem -Path Uninstall: | ForEach-Object -Process { $_.GetValue('UninstallString') }
```

<span data-ttu-id="23a5b-160">Výstup můžete filtrovat podle zobrazovaného názvu, pokud chcete, můžete:</span><span class="sxs-lookup"><span data-stu-id="23a5b-160">You can filter the output by the display name, if you like:</span></span>

```powershell
Get-ChildItem -Path Uninstall: | Where-Object -FilterScript { $_.GetValue('DisplayName') -like 'Win*'} | ForEach-Object -Process { $_.GetValue('UninstallString') }
```

<span data-ttu-id="23a5b-161">Tyto řetězce však nemusí být možné přímo použít z příkazového řádku Windows Powershellu bez určitými úpravami.</span><span class="sxs-lookup"><span data-stu-id="23a5b-161">However, these strings may not be directly usable from the Windows PowerShell prompt without some modification.</span></span>

### <a name="upgrading-windows-installer-applications"></a><span data-ttu-id="23a5b-162">Upgrade aplikace Instalační služby systému Windows</span><span class="sxs-lookup"><span data-stu-id="23a5b-162">Upgrading Windows Installer Applications</span></span>

<span data-ttu-id="23a5b-163">Pokud chcete upgradovat aplikaci, budete muset znát název aplikace a cestu pro balíček s upgradem aplikace.</span><span class="sxs-lookup"><span data-stu-id="23a5b-163">To upgrade an application, you need to know the name of the application and the path to the application upgrade package.</span></span> <span data-ttu-id="23a5b-164">Pomocí těchto informací můžete upgradovat aplikaci pomocí jediného příkazu Windows Powershellu:</span><span class="sxs-lookup"><span data-stu-id="23a5b-164">With that information, you can upgrade an application with a single Windows PowerShell command:</span></span>

```powershell
(Get-WmiObject -Class Win32_Product -ComputerName . -Filter "Name='OldAppName'").Upgrade(\\AppSrv\dsp\OldAppUpgrade.msi)
```