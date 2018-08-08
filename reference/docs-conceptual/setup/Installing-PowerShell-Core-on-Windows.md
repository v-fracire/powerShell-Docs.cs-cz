---
title: Instalace PowerShellu Core ve Windows
description: Informace o instalaci Powershellu Core ve Windows
ms.date: 08/06/2018
ms.openlocfilehash: 84c158b97519194888cf031c57a2a4634120c456
ms.sourcegitcommit: 01ac77cd0b00e4e5e964504563a9212e8002e5e0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/07/2018
ms.locfileid: "39587114"
---
# <a name="installing-powershell-core-on-windows"></a>Instalace PowerShellu Core ve Windows

## <a name="msi"></a>INSTALAČNÍ SLUŽBY MSI

K instalaci prostředí PowerShell na Windows serveru nebo klienta Windows (funguje ve Windows 7 SP1, Server 2008 R2 a novější), stahování balíčku MSI náš GitHub [uvolní][] stránky.

Souboru MSI, který vypadá takto – `PowerShell-<version>-win-<os-arch>.msi`
<!-- TODO: should be updated to point to the Download Center as well -->

Po stažení poklikejte na instalační program a postupujte podle zobrazených výzev.

Je zástupce v nabídce Start po instalaci.

- Ve výchozím nastavení je balíček nainstalován do `$env:ProgramFiles\PowerShell\<version>`
- Můžete spustit prostředí PowerShell pomocí nabídky Start nebo `$env:ProgramFiles\PowerShell\<version>\pwsh.exe`

### <a name="prerequisites"></a>Předpoklady

Pokud chcete povolit vzdálenou komunikaci prostředí PowerShell přes WSMan, nutné splnit následující požadavky:

- Nainstalujte [Universal C Runtime](https://www.microsoft.com/download/details.aspx?id=50410) na verze Windows starší než Windows 10.
  Je dostupná prostřednictvím přímé stažení nebo aktualizace Windows.
  Opravit plně (včetně nepovinné balíčky), podporované systémy se již databázi máte nainstalované.
- Nainstalujte Windows 7 a Windows Server 2008 R2 Windows Management Frameworku (WMF) 4.0 nebo novější.

## <a name="zip"></a>PSČ

Chcete-li povolit pokročilé scénáře nasazení jsou k dispozici binární archivy ZIP prostředí PowerShell.
Třeba poznamenat, že při použití archivu ZIP, nezískáte kontroly požadavků jako balíček Instalační služby MSI.
Takže v pořadí pro vzdálenou komunikaci přes WSMan fungovala správně na verze Windows starší než Windows 10, je třeba Ujistěte se, že [požadavky](#prerequisites) jsou splněny.

## <a name="deploying-on-windows-iot"></a>Nasazení s využitím Windows IoT

Windows IoT již obsahuje prostředí Windows PowerShell, který budeme používat k nasazení prostředí PowerShell Core 6.

1. Vytvoření `PSSession` cílové zařízení

   ```powershell
   $s = New-PSSession -ComputerName <deviceIp> -Credential Administrator
   ```

2. Zkopírujte balíček ZIP do zařízení

   ```powershell
   # change the destination to however you had partitioned it with sufficient
   # space for the zip and the unzipped contents
   # the path should be local to the device
   Copy-Item .\PowerShell-6.0.2-win-arm32.zip -Destination u:\users\administrator\Downloads -ToSession $s
   ```

3. Připojte se k zařízení a rozbalte archiv

   ```powershell
   Enter-PSSession $s
   cd u:\users\administrator\downloads
   Expand-Archive .\PowerShell-6.0.2-win-arm32.zip
   ```

4. Instalační program vzdálené komunikace prostředí PowerShell Core 6

   ```powershell
   cd .\PowerShell-6.0.2-win-arm32
   # Be sure to use the -PowerShellHome parameter otherwise it'll try to create a new
   # endpoint with Windows PowerShell 5.1
   .\Install-PowerShellRemoting.ps1 -PowerShellHome .
   # You'll get an error message and will be disconnected from the device because it has to restart WinRM
   ```

5. Připojení ke koncovému bodu PowerShell Core 6 na zařízení

   ```powershell
   # Be sure to use the -Configuration parameter.  If you omit it, you will connect to Windows PowerShell 5.1
   Enter-PSSession -ComputerName <deviceIp> -Credential Administrator -Configuration powershell.6.0.2
   ```

## <a name="deploying-on-nano-server"></a>Nasazení na Nano serveru

Tyto pokyny předpokládají, že verze Powershellu je již spuštěna na image Nano serveru a, je generováno pomocí [Image Builder pro Nano Server](/windows-server/get-started/deploy-nano-server).
Nano Server je "bezobslužný" operační systém. Binární soubory jádra můžete nasadit pomocí dvěma způsoby.

1. Offline – připojení disku VHD Nano serveru a rozbalte obsah souboru zip do zvoleného umístění v rámci připojené image.
2. Online – přeneste soubor zip po relaci Powershellu a rozbalte ho do zvoleného umístění.

V obou případech je nutné na verzi Windows 10 x64 ZIP balíčku a bude nutné ke spuštění příkazů v rámci instance prostředí PowerShell "Administrator".

### <a name="offline-deployment-of-powershell-core"></a>Offline nasazení Powershellu Core

1. Použijte váš nástroj pro zipování Oblíbené dekomprimovat balíček do adresáře v rámci připojené image Nano serveru.
2. Odpojte image a spustit ho.
3. Připojte se k instanci doručených zpráv Windows powershellu.
4. Postupujte podle pokynů a vytvořte koncový bod pomocí vzdálené komunikace ["Další instance technikou"](#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).

### <a name="online-deployment-of-powershell-core"></a>Online nasazení Powershellu Core

Následující kroky vás provedou nasazení Powershellu Core ke spuštěné instanci Nano serveru a konfigurace jeho vzdálený koncový bod.

- Připojte se k instanci doručených zpráv Windows powershellu

  ```powershell
  $session = New-PSSession -ComputerName <Nano Server IP address> -Credential <An Administrator account on the system>
  ```

- Zkopírujte soubor na instanci Nano serveru

  ```powershell
  Copy-Item <local PS Core download location>\powershell-<version>-win-x64.zip c:\ -ToSession $session
  ```

- Do relace PSSession

  ```powershell
  Enter-PSSession $session
  ```

- Extrahování souboru ZIP

  ```powershell
  # Insert the appropriate version.
  Expand-Archive -Path C:\powershell-<version>-win-x64.zip -DestinationPath "C:\PowerShellCore_<version>"
  ```

- Pokud chcete vzdálené komunikace založená na službě WSMan, postupujte podle pokynů a vytvořte koncový bod vzdálené komunikace pomocí ["Další instance technikou"](../core-powershell/WSMan-Remoting-in-PowerShell-Core.md#executed-by-another-instance-of-powershell-on-behalf-of-the-instance-that-it-will-register).

## <a name="instructions-to-create-a-remoting-endpoint"></a>Pokyny k vytvoření koncového bodu vzdálené komunikace

PowerShell Core podporuje protokol vzdálené komunikace prostředí PowerShell (PSRP) prostřednictvím služby WSMan a SSH.
Další informace viz:

- [SSH vzdálené komunikace v Powershellu Core][ssh-remoting]
- [Vzdálená komunikace WSMan v Powershellu Core][wsman-remoting]

## <a name="artifact-installation-instructions"></a>Pokyny k instalaci artefaktu

Publikujeme archiv s bity CoreCLR při každém sestavení CI s [AppVeyor][].

Instalace Powershellu Core v CoreCLR artefaktu:

1. Stáhněte si balíček ZIP z **artefakty** kartu konkrétním sestavení.
2. Soubor ZIP odblokovat: klikněte pravým tlačítkem v Průzkumníku souborů -> Vlastnosti -> Zkontrolujte použití pole -> odblokovat
3. Extrahujte soubor zip do `bin` adresáře
4. `./bin/pwsh.exe`

<!-- [download-center]: TODO -->

[uvolní]: https://github.com/PowerShell/PowerShell/releases
[ssh-remoting]: ../core-powershell/SSH-Remoting-in-PowerShell-Core.md
[wsman-remoting]: ../core-powershell/WSMan-Remoting-in-PowerShell-Core.md
[AppVeyor]: https://ci.appveyor.com/project/PowerShell/powershell
