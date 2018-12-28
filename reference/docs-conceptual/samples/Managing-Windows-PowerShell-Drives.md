---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Správa jednotek Windows PowerShellu
ms.assetid: bd809e38-8de9-437a-a250-f30a667d11b4
ms.openlocfilehash: cfc5418e9d2efb1a786817e1b941d75e22291742
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404045"
---
# <a name="managing-windows-powershell-drives"></a><span data-ttu-id="ccb89-103">Správa jednotek Windows PowerShellu</span><span class="sxs-lookup"><span data-stu-id="ccb89-103">Managing Windows PowerShell Drives</span></span>

<span data-ttu-id="ccb89-104">A *jednotku prostředí Windows PowerShell* je umístění úložiště dat, který se zobrazí jako jednotku systému souborů ve Windows Powershellu.</span><span class="sxs-lookup"><span data-stu-id="ccb89-104">A *Windows PowerShell drive* is a data store location that you can access like a file system drive in Windows PowerShell.</span></span> <span data-ttu-id="ccb89-105">Poskytovatelé Windows Powershellu některé jednotky pro vytvoření, jako například jednotky systému souborů (včetně C: a D:), registru jednotky (HKCU: a HKLM:) a jednotky certifikát (Cert:), a můžete vytvořit vlastní jednotek Windows Powershellu.</span><span class="sxs-lookup"><span data-stu-id="ccb89-105">The Windows PowerShell providers create some drives for you, such as the file system drives (including C: and D:), the registry drives (HKCU: and HKLM:), and the certificate drive (Cert:), and you can create your own Windows PowerShell drives.</span></span> <span data-ttu-id="ccb89-106">Tyto disky jsou velmi užitečné, ale jsou k dispozici pouze v rámci prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ccb89-106">These drives are very useful, but they are available only within Windows PowerShell.</span></span> <span data-ttu-id="ccb89-107">Nelze k nim přistupovat pomocí jiných nástrojů Windows, jako je například Průzkumník souborů nebo Cmd.exe.</span><span class="sxs-lookup"><span data-stu-id="ccb89-107">You cannot access them by using other Windows tools, such as File Explorer or Cmd.exe.</span></span>

<span data-ttu-id="ccb89-108">Prostředí Windows PowerShell používá podstatné jméno, **PSDrive**, příkazy, které pracují s prostředím Windows PowerShell jednotky.</span><span class="sxs-lookup"><span data-stu-id="ccb89-108">Windows PowerShell uses the noun, **PSDrive**, for commands that work with Windows PowerShell drives.</span></span> <span data-ttu-id="ccb89-109">Pro seznam prostředí Windows PowerShell jednotek v relaci prostředí Windows PowerShell, použijte **Get-PSDrive** rutiny.</span><span class="sxs-lookup"><span data-stu-id="ccb89-109">For a list of the Windows PowerShell drives in your Windows PowerShell session, use the **Get-PSDrive** cmdlet.</span></span>

```
PS> Get-PSDrive

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
A          FileSystem    A:\
Alias      Alias
C          FileSystem    C:\                                 ...And Settings\me
cert       Certificate   \
D          FileSystem    D:\
Env        Environment
Function   Function
HKCU       Registry      HKEY_CURRENT_USER
HKLM       Registry      HKEY_LOCAL_MACHINE
Variable   Variable
```

<span data-ttu-id="ccb89-110">I když s jednotkami ve vašem systému se liší jednotek v zobrazení seznamu bude vypadat podobně jako na výstupu **Get-PSDrive** výše uvedenému příkazu.</span><span class="sxs-lookup"><span data-stu-id="ccb89-110">Although the drives in the display vary with the drives on your system, the listing will look similar to the output of the **Get-PSDrive** command shown above.</span></span>

<span data-ttu-id="ccb89-111">Jednotky systému souborů, jsou podmnožinou jednotek Windows Powershellu.</span><span class="sxs-lookup"><span data-stu-id="ccb89-111">File system drives are a subset of the Windows PowerShell drives.</span></span> <span data-ttu-id="ccb89-112">Můžete určit soubor systémové jednotky v položce systému souborů ve sloupci zprostředkovatele.</span><span class="sxs-lookup"><span data-stu-id="ccb89-112">You can identify the file system drives by the FileSystem entry in the Provider column.</span></span> <span data-ttu-id="ccb89-113">(Jednotky systému souborů v prostředí Windows PowerShell je podporováno ve zprostředkovateli Windows Powershellu systému souborů.)</span><span class="sxs-lookup"><span data-stu-id="ccb89-113">(The file system drives in Windows PowerShell are supported by the Windows PowerShell FileSystem provider.)</span></span>

<span data-ttu-id="ccb89-114">Chcete-li zobrazit syntaxi **Get-PSDrive** rutiny, zadejte **Get-Command** příkazů **syntaxe** parametr:</span><span class="sxs-lookup"><span data-stu-id="ccb89-114">To see the syntax of the **Get-PSDrive** cmdlet, type a **Get-Command** command with the **Syntax** parameter:</span></span>

```
PS> Get-Command -Name Get-PSDrive -Syntax

Get-PSDrive [[-Name] <String[]>] [-Scope <String>] [-PSProvider <String[]>] [-V
erbose] [-Debug] [-ErrorAction <ActionPreference>] [-ErrorVariable <String>] [-
OutVariable <String>] [-OutBuffer <Int32>]
```

<span data-ttu-id="ccb89-115">**PSProvider** parametr umožňuje zobrazit pouze pro prostředí Windows PowerShell, které disky jsou podporovány konkrétního poskytovatele.</span><span class="sxs-lookup"><span data-stu-id="ccb89-115">The **PSProvider** parameter lets you display only the Windows PowerShell drives that are supported by a particular provider.</span></span> <span data-ttu-id="ccb89-116">Například pokud chcete zobrazit pouze jednotek Windows Powershellu, které jsou podporovány ve zprostředkovateli Windows Powershellu systému souborů, zadejte **Get-PSDrive** příkazů **PSProvider** parametr a  **Systém souborů** hodnotu:</span><span class="sxs-lookup"><span data-stu-id="ccb89-116">For example, to display only the Windows PowerShell drives that are supported by the Windows PowerShell FileSystem provider, type a **Get-PSDrive** command with the **PSProvider** parameter and the **FileSystem** value:</span></span>

```
PS> Get-PSDrive -PSProvider FileSystem

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
A          FileSystem    A:\
C          FileSystem    C:\                           ...nd Settings\PowerUser
D          FileSystem    D:\
```

<span data-ttu-id="ccb89-117">Chcete-li zobrazit jednotek Windows Powershellu, které představují podregistrům registru, použijte **PSProvider** parametr k zobrazení jen pro prostředí Windows PowerShell disky, které podporuje zprostředkovatel registru Windows Powershellu:</span><span class="sxs-lookup"><span data-stu-id="ccb89-117">To view the Windows PowerShell drives that represent registry hives, use the **PSProvider** parameter to display only the Windows PowerShell drives that are supported by the Windows PowerShell Registry provider:</span></span>

```
PS> Get-PSDrive -PSProvider Registry

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
HKCU       Registry      HKEY_CURRENT_USER
HKLM       Registry      HKEY_LOCAL_MACHINE
```

<span data-ttu-id="ccb89-118">Standardní rutiny umístění můžete použít také s jednotek Windows Powershellu:</span><span class="sxs-lookup"><span data-stu-id="ccb89-118">You can also use the standard Location cmdlets with the Windows PowerShell drives:</span></span>

```
PS> Set-Location HKLM:\SOFTWARE
PS> Push-Location .\Microsoft
PS> Get-Location

Path
----
HKLM:\SOFTWARE\Microsoft
```

### <a name="adding-new-windows-powershell-drives-new-psdrive"></a><span data-ttu-id="ccb89-119">Přidání nové prostředí Windows PowerShell (nový PSDrive) jednotky</span><span class="sxs-lookup"><span data-stu-id="ccb89-119">Adding New Windows PowerShell Drives (New-PSDrive)</span></span>

<span data-ttu-id="ccb89-120">Můžete přidat jednotky prostředí Windows PowerShell pomocí **New-PSDrive** příkazu.</span><span class="sxs-lookup"><span data-stu-id="ccb89-120">You can add your own Windows PowerShell drives by using the **New-PSDrive** command.</span></span> <span data-ttu-id="ccb89-121">Získání syntaxe pro **New-PSDrive** příkazu, zadejte **Get-Command** příkazů **syntaxe** parametr:</span><span class="sxs-lookup"><span data-stu-id="ccb89-121">To get the syntax for the **New-PSDrive** command, enter the **Get-Command** command with the **Syntax** parameter:</span></span>

```
PS> Get-Command -Name New-PSDrive -Syntax

New-PSDrive [-Name] <String> [-PSProvider] <String> [-Root] <String> [-Descript
ion <String>] [-Scope <String>] [-Credential <PSCredential>] [-Verbose] [-Debug
] [-ErrorAction <ActionPreference>] [-ErrorVariable <String>] [-OutVariable <St
ring>] [-OutBuffer <Int32>] [-WhatIf] [-Confirm]
```

<span data-ttu-id="ccb89-122">Chcete-li vytvořit novou jednotku prostředí Windows PowerShell, je nutné zadat tři parametry:</span><span class="sxs-lookup"><span data-stu-id="ccb89-122">To create a new Windows PowerShell drive, you must supply three parameters:</span></span>

- <span data-ttu-id="ccb89-123">Název disku (můžete použít libovolný platný název prostředí Windows PowerShell)</span><span class="sxs-lookup"><span data-stu-id="ccb89-123">A name for the drive (you can use any valid Windows PowerShell name)</span></span>

- <span data-ttu-id="ccb89-124">PSProvider (použití systému souborů"" pro umístění systému souborů a umístění registru "registru")</span><span class="sxs-lookup"><span data-stu-id="ccb89-124">The PSProvider (use "FileSystem" for file system locations and "Registry" for registry locations)</span></span>

- <span data-ttu-id="ccb89-125">Kořenový adresář, to znamená, že cesta do kořenového adresáře nové jednotky</span><span class="sxs-lookup"><span data-stu-id="ccb89-125">The root, that is, the path to the root of the new drive</span></span>

<span data-ttu-id="ccb89-126">Můžete například vytvořit jednotku s názvem "Office", který je namapovaný na složku, která obsahuje aplikace Microsoft Office v počítači, jako například **C:\\Program Files\\Microsoft Office\\OFFICE11**.</span><span class="sxs-lookup"><span data-stu-id="ccb89-126">For example, you can create a drive named "Office" that is mapped to the folder that contains the Microsoft Office applications on your computer, such as **C:\\Program Files\\Microsoft Office\\OFFICE11**.</span></span> <span data-ttu-id="ccb89-127">Chcete-li vytvořit jednotku, zadejte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="ccb89-127">To create the drive, type the following command:</span></span>

```
PS> New-PSDrive -Name Office -PSProvider FileSystem -Root "C:\Program Files\Micr
osoft Office\OFFICE11"

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
Office     FileSystem    C:\Program Files\Microsoft Offic...
```

> [!NOTE]
> <span data-ttu-id="ccb89-128">Obecně platí cesty nejsou malá a velká písmena.</span><span class="sxs-lookup"><span data-stu-id="ccb89-128">In general, paths are not case-sensitive.</span></span>

<span data-ttu-id="ccb89-129">Můžete odkazovat na novou jednotku prostředí Windows PowerShell, stejně jako u všech jednotek Windows Powershellu – podle názvu, za nímž následuje dvojtečka (**:**).</span><span class="sxs-lookup"><span data-stu-id="ccb89-129">You refer to the new Windows PowerShell drive as you do all Windows PowerShell drives -- by its name followed by a colon (**:**).</span></span>

<span data-ttu-id="ccb89-130">Jednotku prostředí Windows PowerShell můžete provádět mnoho úloh mnohem jednodušší.</span><span class="sxs-lookup"><span data-stu-id="ccb89-130">A Windows PowerShell drive can make many tasks much simpler.</span></span> <span data-ttu-id="ccb89-131">Některé z vašich nejdůležitějších klíče v registru Windows mít například extrémně dlouhé cesty, díky kterým jsou náročné na přístup a obtížně mějte na paměti.</span><span class="sxs-lookup"><span data-stu-id="ccb89-131">For example, some of the most important keys in the Windows registry have extremely long paths, making them cumbersome to access and difficult to remember.</span></span> <span data-ttu-id="ccb89-132">Informace o důležitých konfiguraci se nachází v části **HKEY_LOCAL_MACHINE\\softwaru\\Microsoft\\Windows\\CurrentVersion**.</span><span class="sxs-lookup"><span data-stu-id="ccb89-132">Critical configuration information resides under **HKEY_LOCAL_MACHINE\\SOFTWARE\\Microsoft\\Windows\\CurrentVersion**.</span></span> <span data-ttu-id="ccb89-133">K zobrazení a změně položek v klíči registru CurrentVersion, můžete vytvořit jednotku prostředí Windows PowerShell, který je integrován v tento klíč tak, že zadáte:</span><span class="sxs-lookup"><span data-stu-id="ccb89-133">To view and change items in the CurrentVersion registry key, you can create a Windows PowerShell drive that is rooted in that key by typing:</span></span>

```
PS> New-PSDrive -Name cvkey -PSProvider Registry -Root HKLM\Software\Microsoft\W
indows\CurrentVersion

Name       Provider      Root                                   CurrentLocation
----       --------      ----                                   ---------------
cvkey      Registry      HKLM\Software\Microsoft\Windows\...
```

<span data-ttu-id="ccb89-134">Můžete změnit umístění **cvkey:** jednotka stejně jako jakoukoli jinou jednotkou:''</span><span class="sxs-lookup"><span data-stu-id="ccb89-134">You can then change location to the **cvkey:** drive as you would any other drive:\`\`</span></span>

`PS> cd cvkey:`

<span data-ttu-id="ccb89-135">nebo:</span><span class="sxs-lookup"><span data-stu-id="ccb89-135">or:</span></span>

```
PS> Set-Location cvkey: -PassThru

Path
----
cvkey:\
```

<span data-ttu-id="ccb89-136">Rutina New-PsDrive přidá novou jednotku pouze do aktuální relace prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ccb89-136">The New-PsDrive cmdlet adds the new drive only to the current Windows PowerShell session.</span></span> <span data-ttu-id="ccb89-137">Pokud zavřete okno prostředí Windows PowerShell, dojde ke ztrátě novou jednotku.</span><span class="sxs-lookup"><span data-stu-id="ccb89-137">If you close the Windows PowerShell window, the new drive is lost.</span></span> <span data-ttu-id="ccb89-138">Pokud chcete uložit jednotku prostředí Windows PowerShell, použijte rutinu Export-konzoly exportovat aktuální relace prostředí Windows PowerShell a pak použijte PowerShell.exe **PSConsoleFile** importujte ho.</span><span class="sxs-lookup"><span data-stu-id="ccb89-138">To save a Windows PowerShell drive, use the Export-Console cmdlet to export the current Windows PowerShell session, and then use the PowerShell.exe **PSConsoleFile** parameter to import it.</span></span> <span data-ttu-id="ccb89-139">Nebo přidejte nové jednotky k vašemu profilu Windows Powershellu.</span><span class="sxs-lookup"><span data-stu-id="ccb89-139">Or, add the new drive to your Windows PowerShell profile.</span></span>

### <a name="deleting-windows-powershell-drives-remove-psdrive"></a><span data-ttu-id="ccb89-140">Odstraňuje se prostředí Windows PowerShell jednotek (Remove-PSDrive)</span><span class="sxs-lookup"><span data-stu-id="ccb89-140">Deleting Windows PowerShell Drives (Remove-PSDrive)</span></span>

<span data-ttu-id="ccb89-141">Jednotky z prostředí Windows PowerShell můžete odstranit pomocí **odebrat PSDrive** rutiny.</span><span class="sxs-lookup"><span data-stu-id="ccb89-141">You can delete drives from Windows PowerShell by using the **Remove-PSDrive** cmdlet.</span></span> <span data-ttu-id="ccb89-142">**Odebrat PSDrive** rutina je snadno použitelný; Chcete-li odstranit určitou jednotku prostředí Windows PowerShell, stačí zadat název jednotku prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="ccb89-142">The **Remove-PSDrive** cmdlet is easy to use; to delete a specific Windows PowerShell drive, you just supply the Windows PowerShell drive name.</span></span>

<span data-ttu-id="ccb89-143">Například, pokud jste přidali **Office:** Jednotku prostředí Windows PowerShell, jak je znázorněno **New-PSDrive** tématu, můžete ho odstranit tak, že zadáte:</span><span class="sxs-lookup"><span data-stu-id="ccb89-143">For example, if you added the **Office:** Windows PowerShell drive, as shown in the **New-PSDrive** topic, you can delete it by typing:</span></span>

```powershell
Remove-PSDrive -Name Office
```

<span data-ttu-id="ccb89-144">Chcete-li odstranit **cvkey:** Prostředí Windows PowerShell jednotka, také ukazuje **New-PSDrive** tématu, použijte následující příkaz:</span><span class="sxs-lookup"><span data-stu-id="ccb89-144">To delete the **cvkey:** Windows PowerShell drive, also shown in the **New-PSDrive** topic, use the following command:</span></span>

```powershell
Remove-PSDrive -Name cvkey
```

<span data-ttu-id="ccb89-145">Je snadné odstranit jednotku prostředí Windows PowerShell, ale nemůžete odstranit, když jste na jednotce.</span><span class="sxs-lookup"><span data-stu-id="ccb89-145">It's easy to delete a Windows PowerShell drive, but you can't delete it while you are in the drive.</span></span> <span data-ttu-id="ccb89-146">Příklad:</span><span class="sxs-lookup"><span data-stu-id="ccb89-146">For example:</span></span>

```
PS> cd office:
PS Office:\> remove-psdrive -name office
Remove-PSDrive : Cannot remove drive 'Office' because it is in use.
At line:1 char:15
+ remove-psdrive  <<<< -name office
```

### <a name="adding-and-removing-drives-outside-windows-powershell"></a><span data-ttu-id="ccb89-147">Přidávání a odebírání jednotek mimo prostředí Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="ccb89-147">Adding and Removing Drives Outside Windows PowerShell</span></span>

<span data-ttu-id="ccb89-148">Zjistí jednotky se systémem souborů, které jsou přidány nebo odebrány ve Windows, včetně síťové jednotky, které jsou mapovány, jednotky USB, které jsou připojeny a jednotek, které jsou odstraněny pomocí prostředí Windows PowerShell **použití** příkaz nebo  **WScript.NetworkMapNetworkDrive** a **RemoveNetworkDrive** metody ze skriptu Windows Script Host (WSH).</span><span class="sxs-lookup"><span data-stu-id="ccb89-148">Windows PowerShell detects file system drives that are added or removed in Windows, including network drives that are mapped, USB drives that are attached, and drives that are deleted by using either the **net use** command or the **WScript.NetworkMapNetworkDrive** and **RemoveNetworkDrive** methods from a Windows Script Host (WSH) script.</span></span>