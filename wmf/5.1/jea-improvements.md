---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: wmf,powershell,setup
contributor: ryanpu
title: Vylepšení akorát správy (JEA)
ms.openlocfilehash: 47a58a6fae9f3a41ec527ec1f77ac1c196336669
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
ms.locfileid: "34222413"
---
# <a name="improvements-to-just-enough-administration-jea"></a><span data-ttu-id="0e7ce-103">Vylepšení akorát správy (JEA)</span><span class="sxs-lookup"><span data-stu-id="0e7ce-103">Improvements to Just Enough Administration (JEA)</span></span>

## <a name="constrained-file-copy-tofrom-jea-endpoints"></a><span data-ttu-id="0e7ce-104">Kopírování souborů omezené z JEA koncové body</span><span class="sxs-lookup"><span data-stu-id="0e7ce-104">Constrained file copy to/from JEA endpoints</span></span>

<span data-ttu-id="0e7ce-105">Nyní můžete vzdáleně kopírovat soubory do/z JEA koncový bod a rest jistotu, že připojující se uživatel nelze zkopírovat jenom *žádné* soubor ve vašem systému.</span><span class="sxs-lookup"><span data-stu-id="0e7ce-105">You can now remotely copy files to/from a JEA endpoint and rest assured that the connecting user can't copy just *any* file on your system.</span></span>
<span data-ttu-id="0e7ce-106">To je možné nakonfigurováním souboru PSSC jednotku můžete připojit k uživatele připojení uživatelů.</span><span class="sxs-lookup"><span data-stu-id="0e7ce-106">This is possible by configuring your PSSC file to mount a user drive for connecting users.</span></span>
<span data-ttu-id="0e7ce-107">Uživatel je nový PSDrive, které jsou jedinečné pro každé připojující se uživatel a přetrvává napříč relacemi.</span><span class="sxs-lookup"><span data-stu-id="0e7ce-107">The user drive is a new PSDrive that is unique to each connecting user and persists across sessions.</span></span>
<span data-ttu-id="0e7ce-108">Pokud je pro kopírování souborů do nebo z relace JEA Copy-Item, je omezené jenom umožnit přístup k jednotce uživatele.</span><span class="sxs-lookup"><span data-stu-id="0e7ce-108">When Copy-Item is used to copy files to or from a JEA session, it is constrained to only allow access to the user drive.</span></span>
<span data-ttu-id="0e7ce-109">Pokusy o zkopírování souborů do jiných PSDrive se nezdaří.</span><span class="sxs-lookup"><span data-stu-id="0e7ce-109">Attempts to copy files to any other PSDrive will fail.</span></span>

<span data-ttu-id="0e7ce-110">Nastavit jednotky uživatele v konfiguračním souboru JEA relace, použijte následující nové pole:</span><span class="sxs-lookup"><span data-stu-id="0e7ce-110">To set up the user drive in your JEA session configuration file, use the following new fields:</span></span>

```powershell
MountUserDrive = $true
UserDriveMaximumSize = 10485760    # 10 MB
```

<span data-ttu-id="0e7ce-111">Složka zálohování jednotky uživatele bude vytvořena na `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\DriveRoots\DOMAIN_USER`</span><span class="sxs-lookup"><span data-stu-id="0e7ce-111">The folder backing the user drive will be created at `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\DriveRoots\DOMAIN_USER`</span></span>

<span data-ttu-id="0e7ce-112">Chcete-li využívat jednotky uživatele a zkopírujte soubory do nebo z koncového bodu JEA nakonfigurovaný tak, aby vystavit jednotka uživatele, použijte `-ToSession` a `-FromSession` parametry Copy-Item.</span><span class="sxs-lookup"><span data-stu-id="0e7ce-112">To utilize the user drive and copy files to/from a JEA endpoint configured to expose the User drive, use the `-ToSession` and `-FromSession` parameters on Copy-Item.</span></span>

```powershell
# Connect to the JEA endpoint
$jeasession = New-PSSession -ComputerName 'srv01' -ConfigurationName 'UserDemo'

# Copy a file in the local folder to the remote machine.
# Note: you cannot specify the file name or subfolder on the remote machine. You must exactly type "User:"
Copy-Item -Path .\SampleFile.txt -Destination User: -ToSession $jeasession

# Copy the file back from the remote machine to your local machine
Copy-Item -Path User:\SampleFile.txt -Destination . -FromSession $jeasession
```

<span data-ttu-id="0e7ce-113">Poté můžete napsat vlastní funkce a zpracovat data uložená na jednotce uživatele ty zpřístupnit uživatelům v souboru funkce Role.</span><span class="sxs-lookup"><span data-stu-id="0e7ce-113">You can then write custom functions to process the data stored in the user drive and make those available to users in your Role Capability file.</span></span>

## <a name="support-for-group-managed-service-accounts"></a><span data-ttu-id="0e7ce-114">Podpora pro skupinu pro spravované služby účty</span><span class="sxs-lookup"><span data-stu-id="0e7ce-114">Support for Group Managed Service Accounts</span></span>

<span data-ttu-id="0e7ce-115">V některých případech může úlohy, které uživatel potřebuje provést v relaci JEA potřebovat přístup k prostředkům v místním počítači.</span><span class="sxs-lookup"><span data-stu-id="0e7ce-115">In some cases, a task a user needs to perform in a JEA session may need to access resources beyond the local machine.</span></span>
<span data-ttu-id="0e7ce-116">Pokud relaci JEA je nakonfigurovaná pro použití virtuální účet, zobrazí se pokusy o dosažení těchto zdrojů pocházet z identitu místního počítače, nikoli na virtuální účet nebo připojených uživatelů.</span><span class="sxs-lookup"><span data-stu-id="0e7ce-116">When a JEA session is configured to use a virtual account, any attempt to reach such resources will appear to come from the local machine's identity, not the virtual account or connected user.</span></span>
<span data-ttu-id="0e7ce-117">V TP5, jsme povolena podpora JEA pro spouštění v kontextu [skupinový účet spravované služby](https://technet.microsoft.com/en-us/library/jj128431(v=ws.11\).aspx) , výrazně usnadňuje přístup k síťovým prostředkům pomocí identitu domény.</span><span class="sxs-lookup"><span data-stu-id="0e7ce-117">In TP5, we have enabled support for running JEA under the context of a [Group Managed Service Account](https://technet.microsoft.com/en-us/library/jj128431(v=ws.11\).aspx), making it much easier to access network resources by using a domain identity.</span></span>

<span data-ttu-id="0e7ce-118">Ke konfiguraci relace JEA spuštěna pod účtem gMSA, použijte následující nový klíč v souboru PSSC:</span><span class="sxs-lookup"><span data-stu-id="0e7ce-118">To configure a JEA session to run under a gMSA account, use the following new key in your PSSC file:</span></span>

```powershell
# Provide the name of your gMSA account here (don't include a trailing $)
# The local machine must be privileged to use this gMSA in Active Directory
GroupManagedServiceAccount = 'myGMSAforJEA'

# You cannot configure a JEA endpoint to use both a gMSA and virtual account
# You can leave the RunAsVirtualAccount field commented out or explicitly set it to false
RunAsVirtualAccount = $false
```

> <span data-ttu-id="0e7ce-119">**Poznámka:** skupinové účty spravované služby není důvodu izolace nebo omezeným oborem virtuální účty.</span><span class="sxs-lookup"><span data-stu-id="0e7ce-119">**Note:** Group Managed Service Accounts do not afford the isolation or limited scope of virtual accounts.</span></span>
> <span data-ttu-id="0e7ce-120">Každý připojující se uživatel budou sdílet stejnou identitu gMSA, který může mít oprávnění v celém podniku.</span><span class="sxs-lookup"><span data-stu-id="0e7ce-120">Every connecting user will share the same gMSA identity, which may have permissions across your entire enterprise.</span></span>
> <span data-ttu-id="0e7ce-121">Buďte velmi opatrní při výběru používání gMSA a vždy používat pouze virtuální účty, které jsou omezeny na místním počítači, pokud je to možné.</span><span class="sxs-lookup"><span data-stu-id="0e7ce-121">Be very careful when selecting to use a gMSA, and always prefer virtual accounts which are limited to the local machine when possible.</span></span>

## <a name="conditional-access-policies"></a><span data-ttu-id="0e7ce-122">Zásady podmíněného přístupu</span><span class="sxs-lookup"><span data-stu-id="0e7ce-122">Conditional access policies</span></span>

<span data-ttu-id="0e7ce-123">JEA je skvělým v omezení, co někdo udělat, když jste připojeni k systému pro správu, ale co když je také chcete omezit *při* jiný uživatel pomocí JEA?</span><span class="sxs-lookup"><span data-stu-id="0e7ce-123">JEA is great at limiting what someone can do when they've connected to a system to manage it, but what if you also want to limit *when* someone can use JEA?</span></span>
<span data-ttu-id="0e7ce-124">Možnosti konfigurace do relace konfigurační soubory (.pssc) můžete určit skupiny zabezpečení, ke kterým musí patřit uživatele, aby bylo možné vytvořit relaci JEA jsme přidali.</span><span class="sxs-lookup"><span data-stu-id="0e7ce-124">We have added configuration options into the session configuration files (.pssc) to let you specify security groups to which a user must belong in order to establish a JEA session.</span></span>
<span data-ttu-id="0e7ce-125">To může být zvláště užitečné, pokud ve svém prostředí máte právě v čas (JIT) systému a chcete, aby vaše uživatele zvyšovat jejich oprávnění před přístupem k JEA koncový bod vysokou úrovní oprávnění.</span><span class="sxs-lookup"><span data-stu-id="0e7ce-125">This can be particularly helpful if you have a Just In Time (JIT) system in your environment, and want to make your users elevate their privileges before accessing a highly-privileged JEA endpoint.</span></span>

<span data-ttu-id="0e7ce-126">Nové *RequiredGroups* polem v souboru PSSC umožňuje určit logika pro určení, zda uživatel může připojit k JEA.</span><span class="sxs-lookup"><span data-stu-id="0e7ce-126">The new *RequiredGroups* field in the PSSC file allows you to specify the logic to determine if a user can connect to JEA.</span></span>
<span data-ttu-id="0e7ce-127">Skládá se z zadání zatřiďovací tabulku (volitelně vnořená) používající 'A' a 'Nebo' klíčů můžete vytvořit vaše pravidla.</span><span class="sxs-lookup"><span data-stu-id="0e7ce-127">It consists of specifying a hashtable (optionally nested) that uses the 'And' and 'Or' keys to construct your rules.</span></span>
<span data-ttu-id="0e7ce-128">Tady jsou některé příklady, jak využít toto pole:</span><span class="sxs-lookup"><span data-stu-id="0e7ce-128">Here are some examples of how to leverage this field:</span></span>

```powershell
# Example 1: Connecting users must belong to a security group called "elevated-jea"
RequiredGroups = @{ And = 'elevated-jea' }

# Example 2: Connecting users must have signed on with 2 factor authentication or a smart card
# The 2 factor authentication group name is "2FA-logon" and the smart card group name is "smartcard-logon"
RequiredGroups = @{ Or = '2FA-logon', 'smartcard-logon' }

# Example 3: Connecting users must elevate into "elevated-jea" with their JIT system and have logged on with 2FA or a smart card
RequiredGroups = @{ And = 'elevated-jea', @{ Or = '2FA-logon', 'smartcard-logon' }}
```

## <a name="fixed-virtual-accounts-are-now-supported-on-windows-server-2008-r2"></a><span data-ttu-id="0e7ce-129">Opravené: Virtuální účty jsou nyní podporovány v systému Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="0e7ce-129">Fixed: Virtual accounts are now supported on Windows Server 2008 R2</span></span>
<span data-ttu-id="0e7ce-130">V 5.1 WMF je nyní možné použít virtuální účty v systému Windows Server 2008 R2, povolení konfigurací konzistentní a parity funkcí v systému Windows Server 2008 R2 - 2016.</span><span class="sxs-lookup"><span data-stu-id="0e7ce-130">In WMF 5.1, you are now able to use virtual accounts on Windows Server 2008 R2, enabling consistent configurations and feature parity across Windows Server 2008 R2 - 2016.</span></span>
<span data-ttu-id="0e7ce-131">Virtuální účty zůstávají nepodporované při použití JEA na systému Windows 7.</span><span class="sxs-lookup"><span data-stu-id="0e7ce-131">Virtual accounts remain unsupported when using JEA on Windows 7.</span></span>
