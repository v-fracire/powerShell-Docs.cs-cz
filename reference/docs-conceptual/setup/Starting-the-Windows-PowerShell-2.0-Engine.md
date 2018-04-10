---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Spuštění jádra Windows PowerShellu 2.0
ms.assetid: edafc2fa-7576-49c2-bbba-9336f4bcfc28
ms.openlocfilehash: 585e1003554362d11fe99414bd3e80c497799a88
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="starting-the-windows-powershell-20-engine"></a>Spuštění jádra Windows PowerShellu 2.0

Tato část vysvětluje, jak spustit modul Windows PowerShell 2.0 na Windows 8.1, Windows Server 2012 R2, Windows 8 a Windows Server 2012, což zahrnuje modul Windows PowerShell 2.0 a na jiných systémech, na které Windows PowerShell 2.0, prostředí Windows PowerShell 3.0 a prostředí Windows PowerShell 4.0 jsou nainstalovány.

Prostředí Windows PowerShell 4.0 a prostředí Windows PowerShell 3.0 jsou navržená tak, aby byl zpětně kompatibilní s Windows PowerShell 2.0. Rutiny, zprostředkovatelé, moduly snap in, moduly a skripty, které jsou napsané pro prostředí Windows PowerShell 2.0 spustit beze změny v prostředí Windows PowerShell 4.0 a prostředí Windows PowerShell 3.0. Z důvodu změn v zásadách aktivace runtime v rozhraní Microsoft .NET Framework 4, ale programy hostitele prostředí Windows PowerShell, které byly napsané pro prostředí Windows PowerShell 2.0 a kompilovat s Common Language Runtime (CLR) 2.0 nelze spustit bez úprav v systému Windows Prostředí PowerShell 3.0 nebo prostředí Windows PowerShell 4.0, které jsou kompilovat s CLR 4.0. Modul Windows PowerShell 2.0 je určena pro použití pouze v případě stávajícího skriptu nebo hostitele program nelze spustit, protože není kompatibilní s Windows PowerShell 4.0, prostředí Windows PowerShell 3.0 nebo Microsoft .NET Framework 4. Očekává se, že takových případech zřídka.

Mnoho programů, které vyžadují modul Windows PowerShell 2.0 spusťte ji automaticky. Tyto pokyny jsou zahrnuté pro výjimečných případech, ve kterých je potřeba spustit modul ručně.

## <a name="installing-and-enabling-required-programs"></a>Nainstalováním a povolením požadované programy

Před zahájením modul Windows PowerShell 2.0, povolte modul Windows PowerShell 2.0 a Microsoft .NET Framework 3.5 s aktualizací Service Pack 1. Pokyny najdete v tématu [instalace prostředí Windows PowerShell](Installing-Windows-PowerShell.md).

Systémy, na kterém [Windows Management Framework 4.0](http://go.microsoft.com/fwlink/?LinkID=293881) nebo Windows Management Framework 3.0 jsou nainstalovány všechny požadované součásti. Není potřeba žádná další konfigurace. Informace o instalaci [Windows Management Framework 4.0](http://go.microsoft.com/fwlink/?LinkID=293881) nebo Windows Management Framework 3.0, najdete v části [instalace prostředí Windows PowerShell](Installing-Windows-PowerShell.md).

## <a name="how-to-start-the-windows-powershell-20-engine"></a>Jak spustit modul Windows PowerShell 2.0

Při spuštění prostředí Windows PowerShell ve výchozím nastavení spustí nejnovější verze. Spuštění prostředí Windows PowerShell se modul Windows PowerShell 2.0, použijte parametr verze PowerShell.exe. Můžete spustit příkaz na příkazovém řádku prostředí Windows PowerShell a Cmd.exe včetně.

```
PowerShell.exe -Version 2
```

## <a name="how-to-start-a-remote-session-with-the-windows-powershell-20-engine"></a>Spuštění vzdálené relace s modul Windows PowerShell 2.0

Pokud chcete spustit modul Windows PowerShell 2.0 ve vzdálené relaci, vytvořte konfiguraci relace (také označované jako "koncový bod") na vzdáleném počítači, který načte modul Windows PowerShell 2.0. Konfigurace relace je uložený na vzdáleném počítači a použít kterýkoli uživatel oprávnění k vytváření relací, které používají modul Windows PowerShell 2.0.

Toto je pokročilé úlohy, které se obvykle provádí pomocí správce systému.

Následující postup používá **PSVersion** parametr [Register-PSSessionConfiguration](https://technet.microsoft.com/en-us/library/e9152ae2-bd6d-4056-9bc7-dc1893aa29ea) rutiny pro vytvoření konfigurace relace, které používá modul Windows PowerShell 2.0. Můžete také **verze prostředí PowerShell** parametr [New-PSSessionConfigurationFile](https://technet.microsoft.com/en-us/library/5f3e3633-6e90-479c-aea9-ba45a1954866) rutiny k vytvoření relace konfigurační soubor pro relaci, která načte modul Windows PowerShell 2.0 a můžete použít **PSVersion** parametr [Set-PSSessionConfiguration](https://technet.microsoft.com/en-us/library/b21fbad3-1759-4260-b206-dcb8431cd6ea) parametr Chcete-li změnit konfiguraci relace, kterou chcete použít modul Windows PowerShell 2.0.

Další informace o relaci konfigurační soubory, najdete v části [about_Session_Configuration_Files](https://technet.microsoft.com/en-us/library/c7217447-1ebf-477b-a8ef-4dbe9a1473b8). Informace o konfiguracích relace, včetně instalace a zabezpečení, najdete v článku [about_Session_Configurations [v4]](https://technet.microsoft.com/en-us/library/a2fbe12a-350c-4d04-be50-24102824e3ab).

#### <a name="to-start-a-remote-windows-powershell-20-session"></a>Spusťte vzdálenou relaci prostředí Windows PowerShell 2.0

1. Chcete-li vytvořit konfiguraci relace, která vyžaduje modul Windows PowerShell 2.0, použijte **PSVersion** parametr [Register-PSSessionConfiguration](https://technet.microsoft.com/en-us/library/e9152ae2-bd6d-4056-9bc7-dc1893aa29ea) rutiny s hodnotou "2.0". Tento příkaz spusťte v počítači "na straně serveru" nebo přijímající stranou připojení.

   Následující ukázkový příkaz vytvoří na počítači Server01 konfiguraci relace PS2. Chcete-li spustit tento příkaz, spusťte prostředí Windows PowerShell 4.0 nebo prostředí Windows PowerShell 3.0 s **spustit jako správce** možnost.

   ```powershell
   Register-PSSessionConfiguration -Name PS2 -PSVersion 2.0
   ```

2. Pro vytvoření relace v počítači Server01, který používá konfiguraci relace PS2, použijte **ConfigurationName** parametr rutin, které vytvářet vzdálené relace, jako [New-PSSession](https://technet.microsoft.com/en-us/library/76f6628c-054c-4eda-ba7a-a6f28daaa26f) rutiny.

   Když se spustí relace, který používá konfiguraci relace, modul Windows PowerShell 2.0 je automaticky načíst do relace.

   Tento příkaz spustí relaci Server01 počítače, který používá konfiguraci relace PS2. Příkaz uloží danou relaci do proměnné $s.

   ```powershell
   $s = New-PSSession -ComputerName Server01 -ConfigurationName PS2
   ```

## <a name="how-to-start-a-background-job-with-the-windows-powershell-20-engine"></a>Jak spustit úlohu na pozadí se modul Windows PowerShell 2.0

Spusťte úlohu na pozadí se modul Windows PowerShell 2.0 pomocí **PSVersion** parametr [Start-Job](https://technet.microsoft.com/en-us/library/2bc04935-0deb-4ec0-b856-d7290cca6442) rutiny.

Tento příkaz spustí úlohu na pozadí s modul Windows PowerShell 2.0

```powershell
Start-Job {Get-Process} -PSVersion 2.0
```

Další informace o úlohy na pozadí najdete v tématu [about_Jobs](/powershell/module/microsoft.powershell.core/about/about_jobs).