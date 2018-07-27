---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: wmf,powershell,setup
contributor: ryanpu
title: Vylepšení funkce Just Enough Administration (JEA)
ms.openlocfilehash: 66cbacb78f8a365e9c8556c7c56b3c3525de7395
ms.sourcegitcommit: c3f1a83b59484651119630f3089aa51b6e7d4c3c
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/26/2018
ms.locfileid: "39267861"
---
# <a name="improvements-to-just-enough-administration-jea"></a><span data-ttu-id="cdcca-103">Vylepšení funkce Just Enough Administration (JEA)</span><span class="sxs-lookup"><span data-stu-id="cdcca-103">Improvements to Just Enough Administration (JEA)</span></span>

## <a name="constrained-file-copy-tofrom-jea-endpoints"></a><span data-ttu-id="cdcca-104">Kopírování omezené souborů z koncových bodů JEA</span><span class="sxs-lookup"><span data-stu-id="cdcca-104">Constrained file copy to/from JEA endpoints</span></span>

<span data-ttu-id="cdcca-105">Můžete teď vzdáleně zkopírovat soubory do/z JEA koncový bod a rest Buďte bez obav, že je připojující se uživatel nelze zkopírovat pouze *jakékoli* souboru ve vašem systému.</span><span class="sxs-lookup"><span data-stu-id="cdcca-105">You can now remotely copy files to/from a JEA endpoint and rest assured that the connecting user can't copy just *any* file on your system.</span></span> <span data-ttu-id="cdcca-106">To je možné pomocí konfigurace souboru PSSC jednotku můžete připojit k uživatele pro připojení uživatelů.</span><span class="sxs-lookup"><span data-stu-id="cdcca-106">This is possible by configuring your PSSC file to mount a user drive for connecting users.</span></span> <span data-ttu-id="cdcca-107">Jednotka uživatel je nový PSDrive, který je jedinečný pro každé připojení uživatele a se uchovávají napříč relacemi.</span><span class="sxs-lookup"><span data-stu-id="cdcca-107">The user drive is a new PSDrive that is unique to each connecting user and persists across sessions.</span></span> <span data-ttu-id="cdcca-108">Když `Copy-Item` se použije ke zkopírování souborů do nebo z relace JEA, jsou omezené pouze umožňující přístup k jednotce uživatele.</span><span class="sxs-lookup"><span data-stu-id="cdcca-108">When `Copy-Item` is used to copy files to or from a JEA session, it is constrained to only allow access to the user drive.</span></span> <span data-ttu-id="cdcca-109">Pokusy o zkopírování souborů do jiných PSDrive se nezdaří.</span><span class="sxs-lookup"><span data-stu-id="cdcca-109">Attempts to copy files to any other PSDrive will fail.</span></span>

<span data-ttu-id="cdcca-110">Nastavení jednotky uživatele v konfiguračním souboru JEA relace, použijte následující nová pole:</span><span class="sxs-lookup"><span data-stu-id="cdcca-110">To set up the user drive in your JEA session configuration file, use the following new fields:</span></span>

```powershell
MountUserDrive = $true
UserDriveMaximumSize = 10485760    # 10 MB
```

<span data-ttu-id="cdcca-111">Složka zálohování disku uživatele bude vytvořena na `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\DriveRoots\DOMAIN_USER`</span><span class="sxs-lookup"><span data-stu-id="cdcca-111">The folder backing the user drive will be created at `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\DriveRoots\DOMAIN_USER`</span></span>

<span data-ttu-id="cdcca-112">Chcete-li využívají jednotky uživatele a kopírovat soubory do/z koncového bodu JEA zpřístupňuje jednotka uživatele, použijte `-ToSession` a `-FromSession` parametry na `Copy-Item`.</span><span class="sxs-lookup"><span data-stu-id="cdcca-112">To utilize the user drive and copy files to/from a JEA endpoint configured to expose the User drive, use the `-ToSession` and `-FromSession` parameters on `Copy-Item`.</span></span>

```powershell
# Connect to the JEA endpoint
$jeasession = New-PSSession -ComputerName 'srv01' -ConfigurationName 'UserDemo'

# Copy a file in the local folder to the remote machine.
# Note: you cannot specify the file name or subfolder on the remote machine.
# You must exactly type "User:"
Copy-Item -Path .\SampleFile.txt -Destination User: -ToSession $jeasession

# Copy the file back from the remote machine to your local machine
Copy-Item -Path User:\SampleFile.txt -Destination . -FromSession $jeasession
```

<span data-ttu-id="cdcca-113">Poté můžete napsat vlastní funkce pro zpracování dat uložených v jednotce uživatele a ty zpřístupníte uživatelům v souboru funkce Role.</span><span class="sxs-lookup"><span data-stu-id="cdcca-113">You can then write custom functions to process the data stored in the user drive and make those available to users in your Role Capability file.</span></span>

## <a name="support-for-group-managed-service-accounts"></a><span data-ttu-id="cdcca-114">Podpora pro skupiny spravovaná služba účty</span><span class="sxs-lookup"><span data-stu-id="cdcca-114">Support for Group Managed Service Accounts</span></span>

<span data-ttu-id="cdcca-115">V některých případech může úkol, který uživatel potřebuje provést v relaci JEA potřebovat přístup k prostředkům v místním počítači.</span><span class="sxs-lookup"><span data-stu-id="cdcca-115">In some cases, a task a user needs to perform in a JEA session may need to access resources beyond the local machine.</span></span> <span data-ttu-id="cdcca-116">Při relaci JEA je konfigurován pro použití virtuální účet, zobrazí se jakékoli pokusy o dosažení těchto zdrojů pocházet z místního počítače identitu, ne účet virtuální nebo připojeného uživatele.</span><span class="sxs-lookup"><span data-stu-id="cdcca-116">When a JEA session is configured to use a virtual account, any attempt to reach such resources will appear to come from the local machine's identity, not the virtual account or connected user.</span></span> <span data-ttu-id="cdcca-117">Tp5, zavedli jsme podporu pro spuštění v kontextu JEA [skupinový účet spravované služby](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj128431\(v=ws.11\)), výrazně usnadňují přístup k síťovým prostředkům pomocí identitu domény.</span><span class="sxs-lookup"><span data-stu-id="cdcca-117">In TP5, we have enabled support for running JEA under the context of a [Group Managed Service Account](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj128431\(v=ws.11\)), making it much easier to access network resources by using a domain identity.</span></span>

<span data-ttu-id="cdcca-118">Pokud chcete nakonfigurovat, aby spouštěla pod účtem gMSA JEA relace, použijte následující nový klíč v souboru PSSC:</span><span class="sxs-lookup"><span data-stu-id="cdcca-118">To configure a JEA session to run under a gMSA account, use the following new key in your PSSC file:</span></span>

```powershell
# Provide the name of your gMSA account here (don't include a trailing $)
# The local machine must be privileged to use this gMSA in Active Directory
GroupManagedServiceAccount = 'myGMSAforJEA'

# You cannot configure a JEA endpoint to use both a gMSA and virtual account
# You can leave the RunAsVirtualAccount field commented out or explicitly set it to false
RunAsVirtualAccount = $false
```

> [!NOTE]
> <span data-ttu-id="cdcca-119">Skupinové účty spravované služby nedávají izolace nebo omezený rozsah virtuální účty.</span><span class="sxs-lookup"><span data-stu-id="cdcca-119">Group Managed Service Accounts do not afford the isolation or limited scope of virtual accounts.</span></span>
> <span data-ttu-id="cdcca-120">Každý připojující se uživatel budou sdílet stejnou identitu gMSA, který může mít oprávnění v celé organizaci.</span><span class="sxs-lookup"><span data-stu-id="cdcca-120">Every connecting user will share the same gMSA identity, which may have permissions across your entire enterprise.</span></span> <span data-ttu-id="cdcca-121">Buďte velmi opatrní při výběru používat gMSA a vždy preferují virtuální účty, které jsou omezené na místním počítači, pokud je to možné.</span><span class="sxs-lookup"><span data-stu-id="cdcca-121">Be very careful when selecting to use a gMSA, and always prefer virtual accounts which are limited to the local machine when possible.</span></span>

## <a name="conditional-access-policies"></a><span data-ttu-id="cdcca-122">Zásady podmíněného přístupu</span><span class="sxs-lookup"><span data-stu-id="cdcca-122">Conditional access policies</span></span>

<span data-ttu-id="cdcca-123">JEA se skvěle hodí k omezení, co uživatel udělat, když jste připojeni k systému pro správu, ale co když je také chcete omezit *při* někdo použít JEA?</span><span class="sxs-lookup"><span data-stu-id="cdcca-123">JEA is great at limiting what someone can do when they've connected to a system to manage it, but what if you also want to limit *when* someone can use JEA?</span></span> <span data-ttu-id="cdcca-124">Přidali jsme možnosti konfigurace do relace konfigurační soubory (.pssc) umožňuje zadat skupiny zabezpečení, ke kterým musí patřit uživatele, aby bylo možné navázat relaci JEA.</span><span class="sxs-lookup"><span data-stu-id="cdcca-124">We have added configuration options into the session configuration files (.pssc) to let you specify security groups to which a user must belong in order to establish a JEA session.</span></span> <span data-ttu-id="cdcca-125">To může být zvláště užitečné, pokud máte systém právě In Time (JIT) ve vašem prostředí a chtít, aby uživatelé před přístupem k koncový bod vysoce privilegované JEA zvýšení svých oprávnění.</span><span class="sxs-lookup"><span data-stu-id="cdcca-125">This can be particularly helpful if you have a Just In Time (JIT) system in your environment, and want to make your users elevate their privileges before accessing a highly-privileged JEA endpoint.</span></span>

<span data-ttu-id="cdcca-126">Nové *RequiredGroups* polem v souboru PSSC umožňuje zadat logiku k určení, zda uživatel může připojit k JEA.</span><span class="sxs-lookup"><span data-stu-id="cdcca-126">The new *RequiredGroups* field in the PSSC file allows you to specify the logic to determine if a user can connect to JEA.</span></span> <span data-ttu-id="cdcca-127">Skládá se z zadání zatřiďovací tabulku (volitelně vnořené), který používá "A" a "Nebo" klíče k vytvoření pravidla.</span><span class="sxs-lookup"><span data-stu-id="cdcca-127">It consists of specifying a hashtable (optionally nested) that uses the 'And' and 'Or' keys to construct your rules.</span></span> <span data-ttu-id="cdcca-128">Tady je několik příkladů toho, jak využít toto pole:</span><span class="sxs-lookup"><span data-stu-id="cdcca-128">Here are some examples of how to leverage this field:</span></span>

```powershell
# Example 1: Connecting users must belong to a security group called "elevated-jea"
RequiredGroups = @{ And = 'elevated-jea' }

# Example 2: Connecting users must have signed on with 2 factor authentication or a smart card
# The 2 factor authentication group name is "2FA-logon" and the smart card group name is "smartcard-logon"
RequiredGroups = @{ Or = '2FA-logon', 'smartcard-logon' }

# Example 3: Connecting users must elevate into "elevated-jea" with their JIT system and have logged on with 2FA or a smart card
RequiredGroups = @{ And = 'elevated-jea', @{ Or = '2FA-logon', 'smartcard-logon' }}
```

## <a name="fixed-virtual-accounts-are-now-supported-on-windows-server-2008-r2"></a><span data-ttu-id="cdcca-129">Opraveno: Virtuální účty jsou nyní podporovány v systému Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="cdcca-129">Fixed: Virtual accounts are now supported on Windows Server 2008 R2</span></span>

<span data-ttu-id="cdcca-130">Ve WMF 5.1 budete teď moct použít virtuální účty v systému Windows Server 2008 R2, povolení konzistentními konfiguracemi a paritu funkcí ve Windows serveru 2008 R2 – 2016.</span><span class="sxs-lookup"><span data-stu-id="cdcca-130">In WMF 5.1, you are now able to use virtual accounts on Windows Server 2008 R2, enabling consistent configurations and feature parity across Windows Server 2008 R2 - 2016.</span></span> <span data-ttu-id="cdcca-131">Virtuální účty zůstávají nepodporované při použití funkce JEA ve Windows 7.</span><span class="sxs-lookup"><span data-stu-id="cdcca-131">Virtual accounts remain unsupported when using JEA on Windows 7.</span></span>