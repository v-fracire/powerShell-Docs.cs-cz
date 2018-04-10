---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Správa služeb
ms.assetid: 7a410e4d-514b-4813-ba0c-0d8cef88df31
ms.openlocfilehash: f3231d1922568e552534f3d3face3864d1610d65
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="managing-services"></a>Správa služeb

Existují osm rutin služby základní určených pro širokou škálu úloh služby. Podíváme se pouze na zobrazení a změna stavu spuštění pro služby, ale seznam rutin služby můžete získat pomocí **Get-Help \&#42;-Service**, a může najít informace o všech rutin služby pomocí **Get-Help < název rutiny >**, jako například **Get-Help novou službu**.

## <a name="getting-services"></a>Než služeb

Služby v místním nebo vzdáleném počítači můžete získat pomocí **Get-Service** rutiny. Stejně jako u **Get-Process**pomocí **Get-Service** příkaz bez parametrů vrátí všechny služby. Můžete filtrovat podle názvu, i pomocí hvězdičky jako zástupný znak:

```
PS> Get-Service -Name se*

Status   Name               DisplayName
------   ----               -----------
Running  seclogon           Secondary Logon
Running  SENS               System Event Notification
Stopped  ServiceLayer       ServiceLayer
```

Protože to není vždy zřejmé novinky skutečné název pro službu, můžete zjistit, že budete muset najít služby podle zobrazovaného názvu. To provedete pomocí konkrétní název, pomocí zástupných znaků nebo pomocí seznamu názvů zobrazení:

```
PS> Get-Service -DisplayName se*

Status   Name               DisplayName
------   ----               -----------
Running  lanmanserver       Server
Running  SamSs              Security Accounts Manager
Running  seclogon           Secondary Logon
Stopped  ServiceLayer       ServiceLayer
Running  wscsvc             Security Center

PS> Get-Service -DisplayName ServiceLayer,Server

Status   Name               DisplayName
------   ----               -----------
Running  lanmanserver       Server
Stopped  ServiceLayer       ServiceLayer
```

Parametr ComputerName rutiny Get-Service můžete získat službu na vzdálených počítačích. Parametr ComputerName přijme více hodnot a zástupné znaky, abyste získali služeb ve více počítačích jedním příkazem. Například následující příkaz získá služby ve vzdáleném počítači Server01.

```powershell
Get-Service -ComputerName Server01
```

## <a name="getting-required-and-dependent-services"></a>Získávání vyžaduje a závislých služeb

Rutina Get-Service má dva parametry, které jsou velmi užitečné v součásti pro správu služby. Parametr DependentServices získá služby, které závisejí na službě. Parametr RequiredServices získá služby, na kterých závisí tato služba.

Tyto parametry se zobrazí pouze hodnoty DependentServices a ServicesDependedOn (alias = RequiredServices) vlastnosti System.ServiceProcess.ServiceController objektu, který vrátí Get-Service, ale zjednodušit příkazy a ujistěte se, získávání Tyto informace mnohem jednodušší.

Následující příkaz získá služby, které LanmanWorkstation služba vyžaduje.

```
PS> Get-Service -Name LanmanWorkstation -RequiredServices

Status   Name               DisplayName
------   ----               -----------
Running  MRxSmb20           SMB 2.0 MiniRedirector
Running  bowser             Bowser
Running  MRxSmb10           SMB 1.x MiniRedirector
Running  NSI                Network Store Interface Service
```

Následující příkaz získá služby, které vyžadují službu LanmanWorkstation.

```
PS> Get-Service -Name LanmanWorkstation -DependentServices

Status   Name               DisplayName
------   ----               -----------
Running  SessionEnv         Terminal Services Configuration
Running  Netlogon           Netlogon
Stopped  Browser            Computer Browser
Running  BITS               Background Intelligent Transfer Ser...
```

Můžete získat i všechny služby, které mají závislosti. Tento příkaz nepodporuje právě, a pak používá rutinu Format-Table pro zobrazení stavu, název, RequiredServices a DependentServices vlastnosti služeb v počítači.

```powershell
Get-Service -Name * | Where-Object {$_.RequiredServices -or $_.DependentServices} | Format-Table -Property Status, Name, RequiredServices, DependentServices -auto
```

## <a name="stopping-starting-suspending-and-restarting-services"></a>Zastavení, spuštění, pozastavení a restartování služby
Všechny rutiny služby mají stejné obecné formuláře. Služby lze zadat běžný název nebo zobrazovaný název a proveďte seznamy a zástupné znaky jako hodnoty. Chcete-li zastavit služby zařazování tisku, použijte:

```powershell
Stop-Service -Name spooler
```

Služba zařazování tisku spustit po je zastaven, použijte:

```powershell
Start-Service -Name spooler
```

Pozastavení služby zařazování tisku, použijte:

```powershell
Suspend-Service -Name spooler
```

**Restart-Service** rutiny funguje stejným způsobem jako u ostatních rutin služby, ale ukážeme některé příklady složitější pro ni. V nejjednodušší použití zadejte název služby:

```
PS> Restart-Service -Name spooler

WARNING: Waiting for service 'Print Spooler (Spooler)' to finish starting...
WARNING: Waiting for service 'Print Spooler (Spooler)' to finish starting...
PS>
```

Si všimnete, získat opakovaných upozornění o zařazování tisku spuštění. Při provádění operace služby, který nějakou dobu trvá, prostředí Windows PowerShell vás upozorní, že se stále pokouší o provedení úlohy.

Pokud chcete restartovat víc služeb, můžete získat seznam služeb, filtrovat je a pak proveďte restartování:

```
PS> Get-Service | Where-Object -FilterScript {$_.CanStop} | Restart-Service

WARNING: Waiting for service 'Computer Browser (Browser)' to finish stopping...
WARNING: Waiting for service 'Computer Browser (Browser)' to finish stopping...
Restart-Service : Cannot stop service 'Logical Disk Manager (dmserver)' because
 it has dependent services. It can only be stopped if the Force flag is set.
At line:1 char:57
+ Get-Service | Where-Object -FilterScript {$_.CanStop} | Restart-Service <<<<
WARNING: Waiting for service 'Print Spooler (Spooler)' to finish starting...
WARNING: Waiting for service 'Print Spooler (Spooler)' to finish starting...
```

Tyto rutiny služby není parametr ComputerName, ale je bylo možné spouštět ve vzdáleném počítači pomocí rutiny Invoke-Command. Například následující příkaz restartuje službu zařazování tisku ve vzdáleném počítači Server01.

```powershell
Invoke-Command -ComputerName Server01 {Restart-Service Spooler}
```

## <a name="setting-service-properties"></a>Vlastnosti nastavení služby

Rutina Set-Service změní vlastnosti služby v místním nebo vzdáleném počítači. Vzhledem k tomu, že stav služby je vlastnost, můžete tuto rutinu spuštění, zastavení a pozastavení služby. Rutina Set-Service má také StartupType parametr, který vám umožní změnit typ spuštění služby.

Chcete-li používat nastavení služby ve Windows Vista a novějších verzích systému Windows, otevřete prostředí Windows PowerShell pomocí možnosti "Spustit jako správce".

Další informace najdete v tématu [Set-Service [m2]](https://technet.microsoft.com/library/b71e29ed-372b-4e32-a4b7-5eb6216e56c3)

## <a name="see-also"></a>Viz také

- [Get-Service [m2]](https://technet.microsoft.com/en-us/library/0a09cb22-0a1c-4a79-9851-4e53075f9cf6)
- [Set-Service [m2]](https://technet.microsoft.com/library/b71e29ed-372b-4e32-a4b7-5eb6216e56c3)
- [Restart-Service [m2]](https://technet.microsoft.com/en-us/library/45acf50d-2277-4523-baf7-ce7ced977d0f)
- [Pozastavení služby [m2]](https://technet.microsoft.com/en-us/library/c8492b87-0e21-4faf-8054-3c83c2ec2826)