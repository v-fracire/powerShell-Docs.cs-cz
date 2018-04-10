---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Systémové požadavky Windows PowerShellu
ms.assetid: 6d1d3c75-3be4-4fc9-8805-ca9b2c454d42
ms.openlocfilehash: a15b5b33b5296befae833e520cfdfbd41a07b122
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="windows-powershell-system-requirements"></a>Systémové požadavky Windows PowerShellu
Toto téma uvádí požadavky na systém pro Windows PowerShell 3.0, prostředí Windows PowerShell 4.0 a prostředí Windows PowerShell 5.0 a speciální funkce, jako je Windows PowerShell Integrované skriptovací prostředí (ISE), příkazů CIM a pracovních postupů.

Windows® 8.1 a Windows Server® 2012 R2 zahrnují všechny požadované programy. Toto téma je určený pro uživatele starší verzí systému Windows.

## <a name="operating-system-requirements"></a>Požadavky na operační systém
Prostředí Windows PowerShell 5.0 se spouští na následující verze systému Windows.

- Windows Server 2016, ve výchozím nastavení nainstalovaná

- Windows Server 2012 R2, nainstalujte [Windows Management Framework 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) ke spuštění prostředí Windows PowerShell 5.0

- Windows Server 2012, nainstalujte [Windows Management Framework 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) ke spuštění prostředí Windows PowerShell 5.0

- Nainstalujte Windows Server 2008 R2 s aktualizací Service Pack 1, [Windows Management Framework 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) ke spuštění prostředí Windows PowerShell 5.0

- Windows 8.1

- Windows 7 s aktualizací Service Pack 1, nainstalujte [Windows Management Framework 5.0](https://www.microsoft.com/en-us/download/details.aspx?id=50395) ke spuštění prostředí Windows PowerShell 5.0

Prostředí Windows PowerShell 4.0 se spouští na následující verze systému Windows.

- Windows 8.1, ve výchozím nastavení nainstalovaná

- Windows Server 2012 R2, která je ve výchozím nastavení nainstalovaná

- Windows® 7 s aktualizací Service Pack 1, nainstalujte [Windows Management Framework 4.0](https://www.microsoft.com/en-us/download/details.aspx?id=40855) ke spuštění prostředí Windows PowerShell 4.0

- Nainstalujte Windows Server® 2008 R2 s aktualizací Service Pack 1, [Windows Management Framework 4.0](https://www.microsoft.com/en-us/download/details.aspx?id=40855) ke spuštění prostředí Windows PowerShell 4.0

Prostředí Windows PowerShell 3.0 se spouští na následující verze systému Windows.

- Windows 8, ve výchozím nastavení nainstalovaná

- Windows Server 2012, ve výchozím nastavení nainstalovaná

- Windows® 7 s aktualizací Service Pack 1, nainstalujte [Windows Management Framework 3.0](https://www.microsoft.com/en-us/download/details.aspx?id=34595) ke spuštění prostředí Windows PowerShell 3.0

- Nainstalujte Windows Server® 2008 R2 s aktualizací Service Pack 1, [Windows Management Framework 3.0](https://www.microsoft.com/en-us/download/details.aspx?id=34595) ke spuštění prostředí Windows PowerShell 3.0

- Nainstalujte Windows Server 2008 s aktualizací Service Pack 2, [Windows Management Framework 3.0](https://www.microsoft.com/en-us/download/details.aspx?id=34595) ke spuštění prostředí Windows PowerShell 3.0

## <a name="microsoft-net-framework-requirements"></a>Požadavky na rozhraní Microsoft .NET Framework
Prostředí Windows PowerShell 5.0 vyžaduje úplnou instalaci rozhraní Microsoft .NET Framework 4.5. Windows 8.1 a Windows Server 2012 R2 obsahují rozhraní Microsoft .NET Framework 4.5 ve výchozím nastavení.

Prostředí Windows PowerShell 4.0 vyžaduje úplnou instalaci rozhraní Microsoft .NET Framework 4.5. Windows 8.1 a Windows Server 2012 R2 obsahují rozhraní Microsoft .NET Framework 4.5 ve výchozím nastavení.

Prostředí Windows PowerShell 3.0 vyžaduje úplnou instalaci rozhraní Microsoft .NET Framework 4. Windows 8 a Windows Server 2012 obsahují rozhraní Microsoft .NET Framework 4.5 ve výchozím nastavení, které tento požadavek plnit.

Chcete-li nainstalovat rozhraní Microsoft .NET Framework 4.5 (dotNetFx45_Full_setup.exe), přečtěte si téma [rozhraní Microsoft .NET Framework 4.5](http://go.microsoft.com/fwlink/?LinkID=242919) na webu Microsoft Download Center.

Chcete-li nainstalovat úplnou instalaci rozhraní Microsoft .NET Framework 4 (dotNetFx40_Full_setup.exe), přečtěte si téma [rozhraní Microsoft .NET Framework 4 (Webová instalační služba)](http://go.microsoft.com/fwlink/?LinkID=212931) na webu Microsoft Download Center.

## <a name="windows-management-framework-40"></a>Windows Management Framework 4.0
Prostředí Windows PowerShell 5.0 vyžaduje Windows Management Framework 4.0 na předinstalován na Windows Server 2008 R2 SP1 a Windows 7 SP1.

## <a name="ws-management-30"></a>Služba WS-Management 3.0
Prostředí Windows PowerShell 3.0 a prostředí Windows PowerShell 4.0 vyžadují 3.0 WS-Management, který podporuje Vzdálená správa systému Windows a protokol služby WSMan. Tento program je součástí Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows Management Framework 4.0 a Windows Management Framework 3.0.

## <a name="windows-management-instrumentation-30"></a>Windows Management Instrumentation 3.0
Prostředí Windows PowerShell 3.0 a prostředí Windows PowerShell 4.0 vyžadují Windows Management Instrumentation 3.0 (WMI). Tento program je součástí Windows 8.1, Windows Server 2012 R2, Windows 8, Windows Server 2012, Windows Management Framework 4.0 a Windows Management Framework 3.0. Pokud tento program není nainstalován v počítači, funkcí, které vyžadují rozhraní WMI, například příkazů CIM, se nespustí.

## <a name="common-language-runtime-40"></a>Modul Common Language Runtime 4.0
Prostředí Windows PowerShell 3.0, prostředí Windows PowerShell 4.0 a prostředí Windows PowerShell 5.0 kompilovány proti Common Language Runtime (CLR) 4.0.

## <a name="graphical-user-interface-requirements"></a>Požadavky na grafické uživatelské rozhraní
Prostředí Windows PowerShell je aplikace pomocí konzoly, která nevyžaduje grafické uživatelské rozhraní. Jako takový ho dobře vhodná pro počítače, které nemají obrazovky nebo monitorování nebo uživatelského rozhraní, jako možnosti instalace jádra serveru systému Windows Server 2012 R2 nebo Windows Server 2012.

Ale některé položky, například následující, vyžadují grafické uživatelské rozhraní. Podrobnosti najdete v tématu nápovědy pro každou položku.

- Integrované skriptovací prostředí (ISE) v prostředí Windows PowerShell

- Rutina

    1.  [Out-GridView](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.utility/out-gridview)

    2.  [Zobrazit – příkaz](https://docs.microsoft.com/en-us/powershell/module/Microsoft.PowerShell.Utility/Show-Command)

    3.  [Show-ControlPanelItem](https://docs.microsoft.com/en-us/powershell/module/Microsoft.PowerShell.Management/Show-ControlPanelItem)

    4.  [Show-EventLog](https://docs.microsoft.com/en-us/powershell/module/Microsoft.PowerShell.Management/Show-EventLog)

- Parameters

    1.  **ShowWindow** parametr [Get-Help](https://docs.microsoft.com/en-us/powershell/module/Microsoft.PowerShell.Core/Get-Help) rutiny.

    2.  **ShowSecurityDescriptorUI** parametr [Register-PSSessionConfiguration](https://docs.microsoft.com/en-us/powershell/module/Microsoft.PowerShell.Core/Register-PSSessionConfiguration) a [Set-PSSessionConfiguration](https://docs.microsoft.com/en-us/powershell/module/Microsoft.PowerShell.Core/Set-PSSessionConfiguration) rutiny.

## <a name="windows-powershell-engine-requirements"></a>Požadavky na modul prostředí PowerShell systému Windows
Prostředí Windows PowerShell 4.0 je navržený jako zpětně kompatibilní s Windows PowerShell 3.0 a prostředí Windows PowerShell 2.0. Rutiny, zprostředkovatelé, moduly snap in, moduly a skripty, které jsou napsané pro prostředí Windows PowerShell 2.0 a prostředí Windows PowerShell 3.0 spustit v prostředí Windows PowerShell 4.0 beze změny.

Z důvodu změn v zásadách aktivace runtime v rozhraní Microsoft .NET Framework 4, ale programy hostitele prostředí Windows PowerShell, které byly napsané pro prostředí Windows PowerShell 2.0 a kompilovat s Common Language Runtime (CLR) 2.0 nelze spustit bez úprav v systému Windows Prostředí PowerShell 3.0, který je kompilovat s CLR 4.0.

Modul prostředí Windows PowerShell 2.0 vyžaduje rozhraní Microsoft .NET Framework 2.0.50727 minimálně. Tento požadavek splněn pomocí rozhraní Microsoft .NET Framework 3.5 Service Pack 1. Tento požadavek není splněna rozhraní Microsoft .NET Framework 4 a novější verze rozhraní Microsoft .NET Framework.

Informace o přidávání nebo instalace modulu prostředí Windows PowerShell 2.0 a přidání nebo instalaci požadované verze rozhraní Microsoft .NET Framework najdete v tématu [instalace modulu Windows PowerShell 2.0](Installing-the-Windows-PowerShell-2.0-Engine.md). Informace o spouštění modulu Windows PowerShell 2.0 naleznete v tématu [spouštění modulu Windows PowerShell 2.0](Starting-the-Windows-PowerShell-2.0-Engine.md).

## <a name="windows-preinstallation-environment"></a>Předinstalační prostředí systému Windows
Prostředí Windows PowerShell 2.0, prostředí Windows PowerShell 3.0 a prostředí Windows PowerShell 4.0 spustit v prostředí Windows Preinstallation Environment (Windows PE). Následující rutiny ale podporované nejsou.

- [Background Intelligent Transfer Service (BITS) rutiny](http://go.microsoft.com/fwlink/?LinkId=257514)

- [Get-EventLog](https://docs.microsoft.com/en-us/powershell/module/Microsoft.PowerShell.Management/Get-EventLog)

- [Get-WinEvent](https://docs.microsoft.com/en-us/powershell/module/Microsoft.PowerShell.Diagnostics/Get-WinEvent)

- [Save-Help](https://docs.microsoft.com/en-us/powershell/module/Microsoft.PowerShell.Core/Save-Help)

- [Update-Help](https://docs.microsoft.com/en-us/powershell/module/Microsoft.PowerShell.Core/Update-Help)

Navíc **WinRM** služby není k dispozici v systému Windows PE.

## <a name="see-also"></a>Viz také
- [Začínáme s prostředím Windows PowerShell](../getting-started/Getting-Started-with-Windows-PowerShell.md)
- [Instalace prostředí Windows PowerShell](Installing-Windows-PowerShell.md)
- [Spuštění prostředí Windows PowerShell](Starting-Windows-PowerShell.md)