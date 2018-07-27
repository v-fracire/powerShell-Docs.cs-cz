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
# <a name="improvements-to-just-enough-administration-jea"></a>Vylepšení funkce Just Enough Administration (JEA)

## <a name="constrained-file-copy-tofrom-jea-endpoints"></a>Kopírování omezené souborů z koncových bodů JEA

Můžete teď vzdáleně zkopírovat soubory do/z JEA koncový bod a rest Buďte bez obav, že je připojující se uživatel nelze zkopírovat pouze *jakékoli* souboru ve vašem systému. To je možné pomocí konfigurace souboru PSSC jednotku můžete připojit k uživatele pro připojení uživatelů. Jednotka uživatel je nový PSDrive, který je jedinečný pro každé připojení uživatele a se uchovávají napříč relacemi. Když `Copy-Item` se použije ke zkopírování souborů do nebo z relace JEA, jsou omezené pouze umožňující přístup k jednotce uživatele. Pokusy o zkopírování souborů do jiných PSDrive se nezdaří.

Nastavení jednotky uživatele v konfiguračním souboru JEA relace, použijte následující nová pole:

```powershell
MountUserDrive = $true
UserDriveMaximumSize = 10485760    # 10 MB
```

Složka zálohování disku uživatele bude vytvořena na `$env:LOCALAPPDATA\Microsoft\Windows\PowerShell\DriveRoots\DOMAIN_USER`

Chcete-li využívají jednotky uživatele a kopírovat soubory do/z koncového bodu JEA zpřístupňuje jednotka uživatele, použijte `-ToSession` a `-FromSession` parametry na `Copy-Item`.

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

Poté můžete napsat vlastní funkce pro zpracování dat uložených v jednotce uživatele a ty zpřístupníte uživatelům v souboru funkce Role.

## <a name="support-for-group-managed-service-accounts"></a>Podpora pro skupiny spravovaná služba účty

V některých případech může úkol, který uživatel potřebuje provést v relaci JEA potřebovat přístup k prostředkům v místním počítači. Při relaci JEA je konfigurován pro použití virtuální účet, zobrazí se jakékoli pokusy o dosažení těchto zdrojů pocházet z místního počítače identitu, ne účet virtuální nebo připojeného uživatele. Tp5, zavedli jsme podporu pro spuštění v kontextu JEA [skupinový účet spravované služby](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj128431\(v=ws.11\)), výrazně usnadňují přístup k síťovým prostředkům pomocí identitu domény.

Pokud chcete nakonfigurovat, aby spouštěla pod účtem gMSA JEA relace, použijte následující nový klíč v souboru PSSC:

```powershell
# Provide the name of your gMSA account here (don't include a trailing $)
# The local machine must be privileged to use this gMSA in Active Directory
GroupManagedServiceAccount = 'myGMSAforJEA'

# You cannot configure a JEA endpoint to use both a gMSA and virtual account
# You can leave the RunAsVirtualAccount field commented out or explicitly set it to false
RunAsVirtualAccount = $false
```

> [!NOTE]
> Skupinové účty spravované služby nedávají izolace nebo omezený rozsah virtuální účty.
> Každý připojující se uživatel budou sdílet stejnou identitu gMSA, který může mít oprávnění v celé organizaci. Buďte velmi opatrní při výběru používat gMSA a vždy preferují virtuální účty, které jsou omezené na místním počítači, pokud je to možné.

## <a name="conditional-access-policies"></a>Zásady podmíněného přístupu

JEA se skvěle hodí k omezení, co uživatel udělat, když jste připojeni k systému pro správu, ale co když je také chcete omezit *při* někdo použít JEA? Přidali jsme možnosti konfigurace do relace konfigurační soubory (.pssc) umožňuje zadat skupiny zabezpečení, ke kterým musí patřit uživatele, aby bylo možné navázat relaci JEA. To může být zvláště užitečné, pokud máte systém právě In Time (JIT) ve vašem prostředí a chtít, aby uživatelé před přístupem k koncový bod vysoce privilegované JEA zvýšení svých oprávnění.

Nové *RequiredGroups* polem v souboru PSSC umožňuje zadat logiku k určení, zda uživatel může připojit k JEA. Skládá se z zadání zatřiďovací tabulku (volitelně vnořené), který používá "A" a "Nebo" klíče k vytvoření pravidla. Tady je několik příkladů toho, jak využít toto pole:

```powershell
# Example 1: Connecting users must belong to a security group called "elevated-jea"
RequiredGroups = @{ And = 'elevated-jea' }

# Example 2: Connecting users must have signed on with 2 factor authentication or a smart card
# The 2 factor authentication group name is "2FA-logon" and the smart card group name is "smartcard-logon"
RequiredGroups = @{ Or = '2FA-logon', 'smartcard-logon' }

# Example 3: Connecting users must elevate into "elevated-jea" with their JIT system and have logged on with 2FA or a smart card
RequiredGroups = @{ And = 'elevated-jea', @{ Or = '2FA-logon', 'smartcard-logon' }}
```

## <a name="fixed-virtual-accounts-are-now-supported-on-windows-server-2008-r2"></a>Opraveno: Virtuální účty jsou nyní podporovány v systému Windows Server 2008 R2

Ve WMF 5.1 budete teď moct použít virtuální účty v systému Windows Server 2008 R2, povolení konzistentními konfiguracemi a paritu funkcí ve Windows serveru 2008 R2 – 2016. Virtuální účty zůstávají nepodporované při použití funkce JEA ve Windows 7.