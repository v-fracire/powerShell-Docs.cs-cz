---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Spuštění jádra Windows PowerShellu 2.0
ms.assetid: edafc2fa-7576-49c2-bbba-9336f4bcfc28
ms.openlocfilehash: b600c1f5ea122df9bd53132ccc8edbbc6fa1e9f6
ms.sourcegitcommit: 221b7daab7f597f8b2e4864cf9b5d9dda9b9879b
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 11/27/2018
ms.locfileid: "52320784"
---
# <a name="starting-the-windows-powershell-20-engine"></a>Spuštění jádra Windows PowerShellu 2.0

Tato část vysvětluje, jak spustit modul Windows PowerShell 2.0 ve Windows 8.1, Windows Server 2012 R2, Windows 8 a Windows Server 2012, mezi které patří modul Windows PowerShell 2.0 a v ostatních systémech, na které Windows PowerShell 2.0, prostředí Windows PowerShell instalují se 3.0 a Windows PowerShell 4.0.

Windows PowerShell 4.0 a Windows PowerShell 3.0 jsou navrženy jako zpětně kompatibilní s Windows PowerShell 2.0. Rutiny, poskytovatelů, moduly snap in, moduly a skriptech psaných pro Windows PowerShell 2.0 bez jakýchkoli změn ve Windows Powershellu 4.0 a Windows PowerShell 3.0. Z důvodu změn v zásadách aktivace modulu runtime v rozhraní Microsoft .NET Framework 4, ale programy hostitele prostředí Windows PowerShell, které byly napsány pro Windows PowerShell 2.0 a zkompilován s Common Language Runtime (CLR) 2.0 nelze spustit bez jakýchkoli úprav ve Windows Prostředí PowerShell 3.0 nebo Windows PowerShell 4.0, které jsou kompilovány pomocí CLR 4.0. Modul Windows PowerShell 2.0 je určena pro použití pouze v případě stávajícího skriptu nebo hostitele program nelze spustit, protože není kompatibilní s Windows PowerShell 4.0, Windows PowerShell 3.0 nebo Microsoft .NET Framework 4. Očekává se, že tyto případy docházet zřídka.

Mnoho aplikací, které vyžadují modul Windows PowerShell 2.0 je automatické spouštění. Tyto pokyny jsou uvedené pro výjimečné situace, ve kterých je potřeba spustit modul ručně.

## <a name="installing-and-enabling-required-programs"></a>Instalace a povolení požadované programy

Před zahájením modul Windows PowerShell 2.0, povolte modul Windows PowerShell 2.0 a Microsoft .NET Framework 3.5 s aktualizací Service Pack 1. Pokyny najdete v tématu [instalace prostředí Windows PowerShell](Installing-Windows-PowerShell.md).

Systémy na které Windows Management Framework 4.0 nebo Windows Management Framework 3.0 jsou nainstalovány mají všechny požadované součásti. Není potřeba žádná další konfigurace. Informace o instalaci [Windows Management Framework 4.0](https://go.microsoft.com/fwlink/?LinkID=293881) nebo Windows Management Framework 3.0, najdete v článku [instalace prostředí Windows PowerShell](Installing-Windows-PowerShell.md).

## <a name="how-to-start-the-windows-powershell-20-engine"></a>Spuštění jádra Windows Powershellu 2.0

Při spuštění prostředí Windows PowerShell ve výchozím nastavení spustí nejnovější verzi. Spusťte prostředí Windows PowerShell s modulem Windows PowerShell 2.0, použijte parametr verze PowerShell.exe. Spustit příkaz na příkazovém řádku prostředí Windows PowerShell a Cmd.exe včetně.

```
PowerShell.exe -Version 2
```

## <a name="how-to-start-a-remote-session-with-the-windows-powershell-20-engine"></a>Spuštění vzdálené relace s modul Windows Powershellu 2.0

Pro spuštění jádra Windows Powershellu 2.0 ve vzdálené relaci, vytvořte konfiguraci relace (také označované jako "koncový bod") na vzdáleném počítači, který načte modul Windows PowerShell 2.0. Konfigurace relace je uložen na vzdáleném počítači a je možné žádný uživatel oprávnění k vytváření relací, které používají modul Windows PowerShell 2.0.

Toto je pokročilá úloha, která se obvykle provádí správce systému.

Následující postup používá **PSVersion** parametr [Register-PSSessionConfiguration](https://technet.microsoft.com/library/e9152ae2-bd6d-4056-9bc7-dc1893aa29ea) rutina pro vytvoření konfigurace relace, která využívá modul Windows PowerShell 2.0. Můžete také použít **verze prostředí PowerShell** parametr [New-PSSessionConfigurationFile](https://technet.microsoft.com/library/5f3e3633-6e90-479c-aea9-ba45a1954866) rutina pro vytvoření relace konfigurační soubor pro relaci, která načte modul Windows PowerShell 2.0 a můžete použít **PSVersion** parametr [Set-PSSessionConfiguration](https://technet.microsoft.com/library/b21fbad3-1759-4260-b206-dcb8431cd6ea) parametr, chcete-li změnit konfiguraci relace, kterou chcete použít modul Windows PowerShell 2.0.

Další informace o relaci konfigurační soubory, naleznete v tématu [about_Session_Configuration_Files](https://technet.microsoft.com/library/c7217447-1ebf-477b-a8ef-4dbe9a1473b8). Informace o konfiguracích relace, včetně nastavení a zabezpečení, najdete v části [about_Session_Configurations [v4]](https://technet.microsoft.com/library/a2fbe12a-350c-4d04-be50-24102824e3ab).

#### <a name="to-start-a-remote-windows-powershell-20-session"></a>Chcete-li spustit vzdálenou relaci Windows Powershellu 2.0

1. Chcete-li vytvořit konfiguraci relace, která vyžaduje modul Windows PowerShell 2.0, použijte **PSVersion** parametr [Register-PSSessionConfiguration](https://technet.microsoft.com/library/e9152ae2-bd6d-4056-9bc7-dc1893aa29ea) rutina s hodnotou "2.0". Tento příkaz spusťte na počítači na "na straně serveru" nebo na konci přijímajícího připojení.

   Následující ukázkový příkaz vytvoří na počítači Server01 konfigurace PS2 relace. Ke spuštění tohoto příkazu, spusťte Windows PowerShell 4.0 nebo Windows Powershellu 3.0 se **spustit jako správce** možnost.

   ```powershell
   Register-PSSessionConfiguration -Name PS2 -PSVersion 2.0
   ```

2. Vytvořte relaci na Server01 počítači, který používá konfiguraci relace PS2, použijte **ConfigurationName** parametr rutiny, které vytvořit vzdálené relace, například [New-PSSession](https://technet.microsoft.com/library/76f6628c-054c-4eda-ba7a-a6f28daaa26f) rutiny.

   Při spuštění relace, který používá konfiguraci relace, modul Windows PowerShell 2.0 se automaticky načtou do relace.

   Následující příkaz spustí relaci Server01 počítače, který používá konfiguraci relace PS2. Tento příkaz uloží danou relaci do proměnné $s.

   ```powershell
   $s = New-PSSession -ComputerName Server01 -ConfigurationName PS2
   ```

## <a name="how-to-start-a-background-job-with-the-windows-powershell-20-engine"></a>Spuštění úlohy na pozadí pomocí modulu Windows Powershellu 2.0

Chcete-li spustit úlohu na pozadí pomocí modulu Windows PowerShell 2.0, použijte **PSVersion** parametr [Start-Job](https://technet.microsoft.com/library/2bc04935-0deb-4ec0-b856-d7290cca6442) rutiny.

Následující příkaz spustí úlohu na pozadí pomocí modulu Windows Powershellu 2.0

```powershell
Start-Job {Get-Process} -PSVersion 2.0
```

Další informace o úlohách na pozadí, naleznete v tématu [about_Jobs](/powershell/module/microsoft.powershell.core/about/about_jobs).