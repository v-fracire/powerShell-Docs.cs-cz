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
# <a name="improvements-to-just-enough-administration-jea"></a>Vylepšení akorát správy (JEA)

## <a name="constrained-file-copy-tofrom-jea-endpoints"></a>Kopírování souborů omezené z JEA koncové body

Nyní můžete vzdáleně kopírovat soubory do/z JEA koncový bod a rest jistotu, že připojující se uživatel nelze zkopírovat jenom *žádné* soubor ve vašem systému.
To je možné nakonfigurováním souboru PSSC jednotku můžete připojit k uživatele připojení uživatelů.
Uživatel je nový PSDrive, které jsou jedinečné pro každé připojující se uživatel a přetrvává napříč relacemi.
Pokud je pro kopírování souborů do nebo z relace JEA Copy-Item, je omezené jenom umožnit přístup k jednotce uživatele.
Pokusy o zkopírování souborů do jiných PSDrive se nezdaří.

Nastavit jednotky uživatele v konfiguračním souboru JEA relace, použijte následující nové pole:

```powershell
MountUserDrive = $true
UserDriveMaximumSize = 10485760    # 10 MB
```

Složka zálohování jednotky uživatele bude vytvořena na `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\DriveRoots\DOMAIN_USER`

Chcete-li využívat jednotky uživatele a zkopírujte soubory do nebo z koncového bodu JEA nakonfigurovaný tak, aby vystavit jednotka uživatele, použijte `-ToSession` a `-FromSession` parametry Copy-Item.

```powershell
# Connect to the JEA endpoint
$jeasession = New-PSSession -ComputerName 'srv01' -ConfigurationName 'UserDemo'

# Copy a file in the local folder to the remote machine.
# Note: you cannot specify the file name or subfolder on the remote machine. You must exactly type "User:"
Copy-Item -Path .\SampleFile.txt -Destination User: -ToSession $jeasession

# Copy the file back from the remote machine to your local machine
Copy-Item -Path User:\SampleFile.txt -Destination . -FromSession $jeasession
```

Poté můžete napsat vlastní funkce a zpracovat data uložená na jednotce uživatele ty zpřístupnit uživatelům v souboru funkce Role.

## <a name="support-for-group-managed-service-accounts"></a>Podpora pro skupinu pro spravované služby účty

V některých případech může úlohy, které uživatel potřebuje provést v relaci JEA potřebovat přístup k prostředkům v místním počítači.
Pokud relaci JEA je nakonfigurovaná pro použití virtuální účet, zobrazí se pokusy o dosažení těchto zdrojů pocházet z identitu místního počítače, nikoli na virtuální účet nebo připojených uživatelů.
V TP5, jsme povolena podpora JEA pro spouštění v kontextu [skupinový účet spravované služby](https://technet.microsoft.com/en-us/library/jj128431(v=ws.11\).aspx) , výrazně usnadňuje přístup k síťovým prostředkům pomocí identitu domény.

Ke konfiguraci relace JEA spuštěna pod účtem gMSA, použijte následující nový klíč v souboru PSSC:

```powershell
# Provide the name of your gMSA account here (don't include a trailing $)
# The local machine must be privileged to use this gMSA in Active Directory
GroupManagedServiceAccount = 'myGMSAforJEA'

# You cannot configure a JEA endpoint to use both a gMSA and virtual account
# You can leave the RunAsVirtualAccount field commented out or explicitly set it to false
RunAsVirtualAccount = $false
```

> **Poznámka:** skupinové účty spravované služby není důvodu izolace nebo omezeným oborem virtuální účty.
> Každý připojující se uživatel budou sdílet stejnou identitu gMSA, který může mít oprávnění v celém podniku.
> Buďte velmi opatrní při výběru používání gMSA a vždy používat pouze virtuální účty, které jsou omezeny na místním počítači, pokud je to možné.

## <a name="conditional-access-policies"></a>Zásady podmíněného přístupu

JEA je skvělým v omezení, co někdo udělat, když jste připojeni k systému pro správu, ale co když je také chcete omezit *při* jiný uživatel pomocí JEA?
Možnosti konfigurace do relace konfigurační soubory (.pssc) můžete určit skupiny zabezpečení, ke kterým musí patřit uživatele, aby bylo možné vytvořit relaci JEA jsme přidali.
To může být zvláště užitečné, pokud ve svém prostředí máte právě v čas (JIT) systému a chcete, aby vaše uživatele zvyšovat jejich oprávnění před přístupem k JEA koncový bod vysokou úrovní oprávnění.

Nové *RequiredGroups* polem v souboru PSSC umožňuje určit logika pro určení, zda uživatel může připojit k JEA.
Skládá se z zadání zatřiďovací tabulku (volitelně vnořená) používající 'A' a 'Nebo' klíčů můžete vytvořit vaše pravidla.
Tady jsou některé příklady, jak využít toto pole:

```powershell
# Example 1: Connecting users must belong to a security group called "elevated-jea"
RequiredGroups = @{ And = 'elevated-jea' }

# Example 2: Connecting users must have signed on with 2 factor authentication or a smart card
# The 2 factor authentication group name is "2FA-logon" and the smart card group name is "smartcard-logon"
RequiredGroups = @{ Or = '2FA-logon', 'smartcard-logon' }

# Example 3: Connecting users must elevate into "elevated-jea" with their JIT system and have logged on with 2FA or a smart card
RequiredGroups = @{ And = 'elevated-jea', @{ Or = '2FA-logon', 'smartcard-logon' }}
```

## <a name="fixed-virtual-accounts-are-now-supported-on-windows-server-2008-r2"></a>Opravené: Virtuální účty jsou nyní podporovány v systému Windows Server 2008 R2
V 5.1 WMF je nyní možné použít virtuální účty v systému Windows Server 2008 R2, povolení konfigurací konzistentní a parity funkcí v systému Windows Server 2008 R2 - 2016.
Virtuální účty zůstávají nepodporované při použití JEA na systému Windows 7.
