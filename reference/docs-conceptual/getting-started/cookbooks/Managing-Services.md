---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Správa služeb
ms.assetid: 7a410e4d-514b-4813-ba0c-0d8cef88df31
ms.openlocfilehash: e2388f5d73a320a69faae0772c8403a7d77f8b52
ms.sourcegitcommit: 77f62a55cac8c13d69d51eef5fade18f71d66955
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/17/2018
ms.locfileid: "39094166"
---
# <a name="managing-services"></a>Správa služeb

Nejsou k dispozici osm jader rutiny, navržená pro širokou škálu úloh služby. Se podíváme jenom na zobrazení a změna stavu spuštění pro služby, ale můžete získat seznam rutin služby pomocí **Get-Help \*– služba**, a informace o všech rutin služby můžete najít pomocí  **Get-Help \<název rutiny\>**, jako například **Get-Help novou službu**.

## <a name="getting-services"></a>Získání služby

Služby na místním nebo vzdáleném počítači můžete získat pomocí **Get-Service** rutiny. Stejně jako u **Get-Process**, použije **Get-Service** příkaz bez parametrů vrátí všechny služby. Můžete filtrovat podle názvu, dokonce i pomocí hvězdičky jako zástupný znak:

```
PS> Get-Service -Name se*

Status   Name               DisplayName
------   ----               -----------
Running  seclogon           Secondary Logon
Running  SENS               System Event Notification
Stopped  ServiceLayer       ServiceLayer
```

Protože není vždy zřejmé novinky o reálný název služby, může se stát, že je nutné vyhledat podle zobrazovaného názvu služby. Máte to podle konkrétního názvu pomocí zástupných znaků, nebo pomocí seznamu zobrazované názvy:

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

Parametru ComputerName rutiny Get-Service můžete použít k získání služby na vzdálených počítačích. Parametr ComputerName přijímá více hodnot a zástupné znaky, abyste se mohli služeb ve více počítačích pomocí jediného příkazu. Například v následujícím příkazu je získán služby na vzdáleném počítači Server01.

```powershell
Get-Service -ComputerName Server01
```

## <a name="getting-required-and-dependent-services"></a>Získání požadovaných a závislé služby

Rutina Get-Service má dva parametry, které jsou velmi užitečné při správy služeb. Parametr DependentServices získá služeb, které závisí na službě. Parametr RequiredServices získá služeb, na které závisí tato služba.

Tyto parametry se zobrazí pouze hodnoty DependentServices a ServicesDependedOn (alias = RequiredServices) vlastnosti objektu System.ServiceProcess.ServiceController zjednodušující Get-služba vrátí hodnotu, ale příkazy a ujistěte se, získání Tyto informace mnohem jednodušší.

V následujícím příkazu je získán služby, které vyžaduje služba LanmanWorkstation.

```
PS> Get-Service -Name LanmanWorkstation -RequiredServices

Status   Name               DisplayName
------   ----               -----------
Running  MRxSmb20           SMB 2.0 MiniRedirector
Running  bowser             Bowser
Running  MRxSmb10           SMB 1.x MiniRedirector
Running  NSI                Network Store Interface Service
```

V následujícím příkazu je získán služby, které vyžaduje služba LanmanWorkstation.

```
PS> Get-Service -Name LanmanWorkstation -DependentServices

Status   Name               DisplayName
------   ----               -----------
Running  SessionEnv         Terminal Services Configuration
Running  Netlogon           Netlogon
Stopped  Browser            Computer Browser
Running  BITS               Background Intelligent Transfer Ser...
```

Dokonce můžete získat všechny služby, které mají závislosti. Právě tohle dělá následující příkaz a poté použije rutinu Format-Table k zobrazení stavu, název, RequiredServices a DependentServices vlastnosti služeb v počítači.

```powershell
Get-Service -Name * | Where-Object {$_.RequiredServices -or $_.DependentServices} | Format-Table -Property Status, Name, RequiredServices, DependentServices -auto
```

## <a name="stopping-starting-suspending-and-restarting-services"></a>Zastavení, spuštění, pozastavení a restartování služeb
Všechny rutiny služby mají stejný obecný tvar. Služby je možné zadat tak běžný název nebo zobrazovaný název a seznamy a zástupné znaky jako hodnoty. K zastavení služby zařazování tisku, použijte:

```powershell
Stop-Service -Name spooler
```

Chcete-li spustit službu zařazování tisku, jakmile je zastaven, použijte:

```powershell
Start-Service -Name spooler
```

Pozastavení služby zařazování tisku, použijte:

```powershell
Suspend-Service -Name spooler
```

**Restart-Service** rutiny funguje stejným způsobem jako u jiných rutin služby, ale ukážeme některé příklady složitější pro něj. V nejjednodušší použití zadejte název služby:

```
PS> Restart-Service -Name spooler

WARNING: Waiting for service 'Print Spooler (Spooler)' to finish starting...
WARNING: Waiting for service 'Print Spooler (Spooler)' to finish starting...
PS>
```

Můžete si všimnout, získejte opakované zpráva upozornění o zařazování tisku spuštění. Při provádění operace služby, která se nějakou dobu trvá, prostředí Windows PowerShell vás upozorní, že se stále pokouší o provedení úlohy.

Pokud chcete restartovat víc služeb, můžete získat seznam služeb, filtrovat je a pak proveďte restart:

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

Tyto rutiny služby nemají parametr ComputerName, můžete je ale spustit ve vzdáleném počítači pomocí rutiny Invoke-Command. Například následující příkaz restartuje službu zařazování tisku na vzdáleném počítači Server01.

```powershell
Invoke-Command -ComputerName Server01 {Restart-Service Spooler}
```

## <a name="setting-service-properties"></a>Nastavení vlastnosti služby

Rutina Set-Service změní vlastnosti služby na místním nebo vzdáleném počítači. Vzhledem k tomu, že stav služby je vlastnost, můžete použít tuto rutinu pro spuštění, zastavení a pozastavení služby. Rutina Set-Service má také parametr typ spuštění, která umožňuje změnit typ spuštění služby.

Pokud chcete použít nastavení služby ve Windows Vista a novějších verzích Windows, otevřete prostředí Windows PowerShell pomocí možnosti "Spustit jako správce".

Další informace najdete v tématu [Set-Service [m2]](https://technet.microsoft.com/library/b71e29ed-372b-4e32-a4b7-5eb6216e56c3)

## <a name="see-also"></a>Viz také

- [Get-Service [m2]](https://technet.microsoft.com/en-us/library/0a09cb22-0a1c-4a79-9851-4e53075f9cf6)
- [Set-Service [m2]](https://technet.microsoft.com/library/b71e29ed-372b-4e32-a4b7-5eb6216e56c3)
- [Restart-Service [m2]](https://technet.microsoft.com/en-us/library/45acf50d-2277-4523-baf7-ce7ced977d0f)
- [Pozastavit – služba [m2]](https://technet.microsoft.com/en-us/library/c8492b87-0e21-4faf-8054-3c83c2ec2826)