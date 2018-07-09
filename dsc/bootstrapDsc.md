---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Konfigurace virtuálních počítačů při prvním spuštění – s využitím DSC
ms.openlocfilehash: 2f228a38379d1e65b31c03594e876f7226474fc3
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893348"
---
# <a name="configure-a-virtual-machines-at-initial-boot-up-by-using-dsc"></a>Konfigurace virtuálních počítačů při prvním spuštění – s využitím DSC

> [!IMPORTANT]
> Platí pro: Windows PowerShell 5.0

## <a name="requirements"></a>Požadavky

> [!NOTE] 
> **DSCAutomationHostEnabled** klíče registru popsané v tomto tématu není k dispozici v Powershellu 4.0.
> Informace o tom, jak nakonfigurovat nové virtuální počítače při prvním spuštění – v Powershellu 4.0 najdete v tématu [Chcete automaticky nakonfigurovat svůj počítače pomocí DSC při spuštění počáteční?] > ()https://blogs.msdn.microsoft.com/powershell/2014/02/28/want-to-automatically-configure-your-machines-using-dsc-at-initial-boot-up/)

Pokud chcete spustit tyto příklady, budete potřebovat:

- Spouštěcí virtuální pevný disk pro práci s. Můžete si stáhnout soubor ISO s zkušební kopii Windows serveru 2016 na [TechNet Evaluation Center](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016). Můžete najít pokyny o tom, jak vytvořit virtuální pevný disk z image ISO v [vytváření spouštěcích virtuálních pevných disků](/previous-versions/windows/it-pro/windows-7/gg318049(v=ws.10)).
- Hostitelský počítač, který má technologie Hyper-V povolena. Informace najdete v tématu [Přehled technologie Hyper-V](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/hh831531(v=ws.11)).

  S využitím DSC, můžete automatizovat instalaci softwaru a konfigurace pro počítač při prvním spuštění.
  Můžete to provést buď vkládání dokument MOF konfigurací nebo metaconfiguration do spouštěcího média (například virtuální pevný disk) tak, že jsou spouštěny během procesu počáteční spouštěcího.
  Toto chování je určená [klíč registru DSCAutomationHostEnabled](DSCAutomationHostEnabled.md) klíče registru pod `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies`.
  Hodnota tohoto klíče je ve výchozím nastavení, 2, který umožňuje DSC na spuštění při spuštění.

  Pokud nechcete, aby DSC na spuštění při spuštění, nastavte hodnotu [klíč registru DSCAutomationHostEnabled](DSCAutomationHostEnabled.md) klíče registru na hodnotu 0.

- Vložit dokument MOF konfigurace do virtuálního pevného disku
- Vložit DSC metaconfiguration do virtuálního pevného disku
- Zakázat DSC v době spuštění

> [!NOTE]
> Můžete vložit obě `Pending.mof` a `MetaConfig.mof` do počítače ve stejnou dobu.
> Pokud je oba soubory, nastavení zadané v `MetaConfig.mof` přednost.

## <a name="inject-a-configuration-mof-document-into-a-vhd"></a>Vložit dokument MOF konfigurace do virtuálního pevného disku

Přijmout při prvním spuštění – konfigurace, můžete vložit dokument MOF zkompilovanou konfiguraci do virtuálního pevného disku jako jeho `Pending.mof` souboru.
Pokud **DSCAutomationHostEnabled** nastavení klíče registru na 2 (výchozí hodnota), DSC, budou platit konfigurace určené `Pending.mof` při spuštění počítače pro první.

V tomto příkladu budeme používat následující konfigurace, které nainstaluje službu IIS v novém počítači:

```powershell
Configuration SampleIISInstall
{
    Import-DscResource -ModuleName 'PSDesiredStateConfiguration'

    node ('localhost')
    {
        WindowsFeature IIS
        {
            Ensure = 'Present'
            Name   = 'Web-Server'
        }
    }
}
```

### <a name="to-inject-the-configuration-mof-document-on-the-vhd"></a>Chcete-li vložit dokument MOF konfigurace na virtuální pevný disk

1. Připojit virtuální pevný disk, do které chcete vložit konfiguraci voláním [připojit virtuální pevný disk](/powershell/module/hyper-v/mount-vhd) rutiny. Příklad:

   ```powershell
   Mount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
   ```

2. V počítači se systémem PowerShell 5.0 nebo novější, uložte konfiguraci uvedené výš (**SampleIISInstall**) jako soubor skriptu (.ps1) prostředí PowerShell.

3. V konzole Powershellu přejděte do složky, kam jste uložili soubor .ps1.

4. Spusťte následující příkazy prostředí PowerShell pro kompilaci dokument MOF (informace o kompilaci konfigurace DSC najdete v tématu [konfigurací DSC](configurations.md):

   ```powershell
   . .\SampleIISInstall.ps1
   SampleIISInstall
   ```

5. Tím se vytvoří `localhost.mof` souboru do nové složky s názvem `SampleIISInstall`.
   Přejmenování a přesunutí tohoto souboru do správného umístění na virtuálním pevném disku jako `Pending.mof` pomocí [přesunout položku](https://technet.microsoft.comlibrary/hh849852.aspx) rutiny. Příklad:

   ```powershell
       Move-Item -Path C:\DSCTest\SampleIISInstall\localhost.mof -Destination E:\Windows\System32\Configuration\Pending.mof
   ```

6. Odpojte virtuální pevný disk pomocí volání [Dismount-VHD](/powershell/module/hyper-v/dismount-vhd) rutiny. Příklad:

   ```powershell
   Dismount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
   ```

7. Vytvoření virtuálního počítače pomocí virtuálního pevného disku, kam jste nainstalovali dokument DSC MOF.

Po počáteční spouštěcí nahoru a instalace operačního systému se nainstaluje službu IIS.
Můžete to ověřit pomocí volání [Get-WindowsFeature](https://technet.microsoft.com/library/jj205469.aspx) rutiny.

## <a name="inject-a-dsc-metaconfiguration-into-a-vhd"></a>Vložit DSC metaconfiguration do virtuálního pevného disku

Můžete také nakonfigurovat počítač k o přijetí změn konfigurace při počáteční spuštění-vložením metaconfiguration (viz [konfigurace místní Configuration Manageru (LCM)](metaConfig.md)) do virtuálního pevného disku jako jeho `MetaConfig.mof` souboru.
Pokud **DSCAutomationHostEnabled** nastavení klíče registru na 2 (výchozí hodnota), DSC, má platit metaconfiguration určené `MetaConfig.mof` k LCM, když se počítač spustí do první.
Pokud metaconfiguration určuje LCM by měla o přijetí změn konfigurace ze serveru vyžádané replikace, počítač se pokusí o přijetí změn konfigurace z tohoto serveru vyžádané replikace při prvním spuštění.
Informace o nastavení serveru vyžádané replikace DSC najdete v tématu [nastavení webového serveru vyžádané replikace DSC](pullServer.md).

V tomto příkladu použijeme konfiguraci popsané v předchozí části (**SampleIISInstall**) a následující metaconfiguration:

```powershell
[DSCLocalConfigurationManager()]
configuration PullClientBootstrap
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Pull'
            RefreshFrequencyMins = 30
            RebootNodeIfNeeded = $true
        }
        ConfigurationRepositoryWeb CONTOSO-PullSrv
        {
            ServerURL = 'https://CONTOSO-PullSrv:8080/PSDSCPullServer.svc'
            RegistrationKey = '140a952b-b9d6-406b-b416-e0f759c9c0e4'
            ConfigurationNames = @('SampleIISInstall')
        }
    }
}
```

### <a name="to-inject-the-metaconfiguration-mof-document-on-the-vhd"></a>Chcete-li vložit dokument MOF metaconfiguration virtuální pevný disk

1. Připojit virtuální pevný disk, do které chcete vložit metaconfiguration voláním [připojit virtuální pevný disk](/powershell/module/hyper-v/mount-vhd) rutiny. Příklad:

   ```powershell
   Mount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
   ```

2. [Nastavení webového serveru vyžádané replikace DSC](pullServer.md)a uložit **SampleIISInistall** konfigurace do příslušné složky.

3. V počítači se systémem PowerShell 5.0 nebo novější, uložit výše metaconfiguration (**PullClientBootstrap**) jako soubor skriptu (.ps1) prostředí PowerShell.

4. V konzole Powershellu přejděte do složky, kam jste uložili soubor .ps1.

5. Spusťte následující příkazy prostředí PowerShell pro kompilaci dokument MOF metaconfiguration (informace o kompilaci konfigurace DSC najdete v tématu [konfigurací DSC](configurations.md):

   ```powershell
   . .\PullClientBootstrap.ps1
   PullClientBootstrap
   ```

6. Tím se vytvoří `localhost.meta.mof` souboru do nové složky s názvem `PullClientBootstrap`.
   Přejmenování a přesunutí tohoto souboru do správného umístění na virtuálním pevném disku jako `MetaConfig.mof` pomocí [přesunout položku](https://technet.microsoft.comlibrary/hh849852.aspx) rutiny.

   ```powershell
   Move-Item -Path C:\DSCTest\PullClientBootstrap\localhost.meta.mof -Destination E:\Windows\System32\Configuration\MetaConfig.mof
   ```

7. Odpojte virtuální pevný disk pomocí volání [Dismount-VHD](/powershell/module/hyper-v/dismount-vhd) rutiny. Příklad:

   ```powershell
   Dismount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
   ```

8. Vytvoření virtuálního počítače pomocí virtuálního pevného disku, kam jste nainstalovali dokument DSC MOF.

Po počáteční spouštěcí nahoru a instalace operačního systému DSC bude o přijetí změn konfigurace ze serveru vyžádané replikace a nainstaluje službu IIS.
Můžete to ověřit pomocí volání [Get-WindowsFeature](https://technet.microsoft.com/library/jj205469.aspx) rutiny.

## <a name="disable-dsc-at-boot-time"></a>Zakázat DSC v době spuštění

Ve výchozím nastavení mají hodnotu `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DSCAutomationHostEnabled` klíč nastavený na 2, který umožňuje konfiguraci DSC ke spouštění, pokud je počítač ve stavu čekající na vyřízení nebo aktuální. Pokud nechcete, aby konfiguraci, kterou chcete spustit při prvním spuštění-, třeba proto nastavíte hodnotu tohoto klíče na hodnotu 0:

1. Připojit virtuální pevný disk pomocí volání [připojit virtuální pevný disk](/powershell/module/hyper-v/mount-vhd) rutiny. Příklad:

   ```powershell
   Mount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
   ```

2. Načtení registru `HKLM\Software` podklíče z virtuálního pevného disku voláním `reg load`.

   ```powershell
   reg load HKLM\Vhd E:\Windows\System32\Config\Software`
   ```

3. Přejděte `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\*` pomocí poskytovatele prostředí PowerShell registru.

   ```powershell
   Set-Location HKLM:\Software\Microsoft\Windows\CurrentVersion\Policies`
   ```

4. Změňte hodnotu vlastnosti `DSCAutomationHostEnabled` na hodnotu 0.

   ```powershell
   Set-ItemProperty -Path . -Name DSCAutomationHostEnabled -Value 0
   ```

5. Uvolněte registru spuštěním následujících příkazů:

   ```powershell
   [gc]::Collect()
   reg unload HKLM\Vhd
   ```

## <a name="see-also"></a>Viz také

[Konfigurace DSC](configurations.md)

[Klíč registru DSCAutomationHostEnabled](DSCAutomationHostEnabled.md)

[Konfigurace Local Configuration Manageru (LCM)](metaConfig.md)

[Nastavení webového serveru vyžádané replikace DSC](pullServer.md)
