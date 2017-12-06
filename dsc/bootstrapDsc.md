---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Konfigurace virtuálních počítačů na počáteční spouštěcí up pomocí DSC"
ms.openlocfilehash: c793e36eb9caa194104f9dda2aa1d335b21b676c
ms.sourcegitcommit: 58371abe9db4b9a0e4e1eb82d39a9f9e187355f9
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/05/2017
---
>Platí pro: Prostředí Windows PowerShell 5.0

>**Poznámka:** **DSCAutomationHostEnabled** klíče registru popsané v tomto tématu není k dispozici v prostředí PowerShell 4.0.
Informace o tom, jak konfigurovat nové virtuální počítače na počáteční telefonického spouštění v prostředí PowerShell 4.0 najdete v tématu [chcete automaticky nakonfigurovat vaše počítače pomocí DSC v počáteční spouštěcí up?](https://blogs.msdn.microsoft.com/powershell/2014/02/28/want-to-automatically-configure-your-machines-using-dsc-at-initial-boot-up/)

# <a name="configure-a-virtual-machines-at-initial-boot-up-by-using-dsc"></a>Konfigurace virtuálních počítačů na počáteční spouštěcí up pomocí DSC

## <a name="requirements"></a>Požadavky

Pokud chcete spustit tyto příklady, budete potřebovat:

- Spouštěcí virtuální pevný disk pro práci s. Můžete si stáhnout soubor ISO s zkušební kopie systému Windows Server 2016 na [TechNet Evaluation Center](https://www.microsoft.com/en-us/evalcenter/evaluate-windows-server-2016). Pokyny naleznete v tom, jak vytvořit virtuální pevný disk z bitové kopie ISO na [vytváření spouštěcího virtuální pevné disky](https://technet.microsoft.com/en-us/library/gg318049.aspx).
- Hostitelský počítač, který má technologie Hyper-V povolena. Informace najdete v tématu [Přehled technologie Hyper-V](https://technet.microsoft.com/library/hh831531.aspx).

Pomocí DSC můžete automatizovat instalaci softwaru a konfigurace pro počítač v počáteční spouštěcí up.
To provedete vložením buď MOF dokumentu konfigurace nebo metakonfiguraci do spouštěcí médium (například virtuální pevný disk) tak, aby se při prvním procesu spouštění up spouštět.
Toto chování je zadána [klíč registru DSCAutomationHostEnabled](DSCAutomationHostEnabled.md) klíč registru v **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies**.
Hodnota tohoto klíče je ve výchozím nastavení, 2, který umožňuje DSC na spuštění při spuštění.

Pokud nechcete, aby DSC na spuštění při spuštění, nastavte hodnotu [klíč registru DSCAutomationHostEnabled](DSCAutomationHostEnabled.md) klíč registru na hodnotu 0.

- Vložit dokument MOF konfigurace do virtuální pevný disk
- Vložit metakonfiguraci DSC do virtuálního pevného disku
- Zakázat DSC při spuštění

>**Poznámka:** můžete vložit obě `Pending.mof` a `MetaConfig.mof` do počítače ve stejnou dobu.
Pokud nejsou oba soubory, nastavení zadané v `MetaConfig.mof` přednost.

## <a name="inject-a-configuration-mof-document-into-a-vhd"></a>Vložit dokument MOF konfigurace do virtuální pevný disk

K uplatní konfigurace na počáteční spouštěcí up, můžete vložit dokument MOF kompilované konfigurace do virtuálního pevného disku jako jeho `Pending.mof` souboru.
Pokud **DSCAutomationHostEnabled** klíč registru je nastavena na 2 (výchozí hodnota), DSC se použijí konfigurace definované `Pending.mof` když se počítač spustí službu poprvé.

V tomto příkladu použijeme následující konfiguraci, která nainstaluje službu IIS na novém počítači:

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

### <a name="to-inject-the-configuration-mof-document-on-the-vhd"></a>Vložení dokumentu MOF konfigurace na virtuální pevný disk

1. Připojit virtuální pevný disk, do kterého chcete vložit konfigurace voláním [připojit virtuální pevný disk](https://technet.microsoft.com/library/hh848551.aspx) rutiny. Příklad:

    ```powershell
    Mount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
    ```
2. V počítači se systémem PowerShell 5.0 nebo novější, uložte výše konfiguraci (**SampleIISInstall**) jako soubor skriptu (.ps1) v prostředí PowerShell.

3. V konzole Powershellu přejděte do složky, kam jste uložili soubor .ps1.

4. Spusťte následující příkazy prostředí PowerShell zkompilovat soubor MOF dokumentu (informace o kompilaci konfigurace DSC najdete v tématu [konfigurace DSC](configurations.md):

    ```powershell
    . .\SampleIISInstall.ps1
    SampleIISInstall
    ```

5. Tím se vytvoří `localhost.mof` souboru do nové složky s názvem `SampleIISInstall`.
Přejmenování a přesunutí tento soubor do příslušného umístění na virtuální pevný disk jako `Pending.mof` pomocí [přesunout položku](https://technet.microsoft.comlibrary/hh849852.aspx) rutiny. Příklad:

    ```powershell
        Move-Item -Path C:\DSCTest\SampleIISInstall\localhost.mof -Destination E:\Windows\System32\Configuration\Pending.mof
    ```
6. Odpojte virtuální pevný disk pomocí volání [odpojení virtuálního pevného disku](https://technet.microsoft.com/library/hh848562.aspx) rutiny. Příklad:

    ```powershell
    Dismount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
    ```

7. Vytvoření virtuálního počítače pomocí virtuálního pevného disku, kam jste nainstalovali DSC MOF dokumentu. Po instalaci operačního systému a vyhledá spouštěcí up bude nainstalována služba IIS.
Můžete to ověřit pomocí volání [Get-WindowsFeature](https://technet.microsoft.com/library/jj205469.aspx) rutiny.

## <a name="inject-a-dsc-metaconfiguration-into-a-vhd"></a>Vložit metakonfiguraci DSC do virtuálního pevného disku

Můžete také nakonfigurovat počítač načítat konfigurace v vyhledá spouštěcí up vložením metakonfiguraci (najdete v části [konfigurace místní Configuration Manager (LCM)](metaConfig.md)) do virtuálního pevného disku jako jeho `MetaConfig.mof` souboru.
Pokud **DSCAutomationHostEnabled** klíč registru je nastavena na 2 (výchozí hodnota), DSC se použijí metakonfiguraci definované `MetaConfig.mof` k LCM, když se počítač spustí službu poprvé.
Pokud metakonfiguraci Určuje, že by měl LCM přijetí změn konfigurace z načítacího serveru, počítač se pokusí o konfiguraci z tohoto serveru vyžádané replikace pro vyžádání obsahu na počáteční spouštěcí up.
Informace o nastavení server DSC za najdete v tématu [nastavení webového serveru vyžádané replikace DSC](pullServer.md).

V tomto příkladu použijeme konfiguraci popsané v předchozí části (**SampleIISInstall**) a následující metakonfiguraci:

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

### <a name="to-inject-the-metaconfiguration-mof-document-on-the-vhd"></a>Chcete-li vložit dokument MOF metakonfiguraci na virtuální pevný disk

1. Připojit virtuální pevný disk, do kterého chcete vložit metakonfiguraci voláním [připojit virtuální pevný disk](https://technet.microsoft.com/library/hh848551.aspx) rutiny. Příklad:

    ```powershell
    Mount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
    ```

2. [Nastavení webového serveru vyžádané replikace DSC](pullServer.md)a uložte **SampleIISInistall** konfigurace do příslušné složky.

3. V počítači se systémem PowerShell 5.0 nebo novější, uložit výše metakonfiguraci (**PullClientBootstrap**) jako soubor skriptu (.ps1) v prostředí PowerShell.

4. V konzole Powershellu přejděte do složky, kam jste uložili soubor .ps1.

5. Spusťte následující příkazy prostředí PowerShell zkompilovat soubor MOF dokumentu metakonfiguraci (informace o kompilaci konfigurace DSC najdete v tématu [konfigurace DSC](configurations.md):

    ```powershell
    . .\PullClientBootstrap.ps1
    PullClientBootstrap
    ```

6. Tím se vytvoří `localhost.meta.mof` souboru do nové složky s názvem `PullClientBootstrap`.
Přejmenování a přesunutí tento soubor do příslušného umístění na virtuální pevný disk jako `MetaConfig.mof` pomocí [přesunout položku](https://technet.microsoft.comlibrary/hh849852.aspx) rutiny.

    ```powershell
    Move-Item -Path C:\DSCTest\PullClientBootstrap\localhost.meta.mof -Destination E:\Windows\Sytem32\Configuration\MetaConfig.mof
    ```

7. Odpojte virtuální pevný disk pomocí volání [odpojení virtuálního pevného disku](https://technet.microsoft.com/library/hh848562.aspx) rutiny. Příklad:

    ```powershell
    Dismount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
    ```

8. Vytvoření virtuálního počítače pomocí virtuálního pevného disku, kam jste nainstalovali DSC MOF dokumentu.
Po instalaci operačního systému a vyhledá spouštěcí up DSC načte konfiguraci z načítacího serveru a služby IIS se nainstalují.
Můžete to ověřit pomocí volání [Get-WindowsFeature](https://technet.microsoft.com/library/jj205469.aspx) rutiny.

## <a name="disable-dsc-at-boot-time"></a>Zakázat DSC při spuštění

Výchozí hodnota **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DSCAutomationHostEnabled** klíč je nastavena na 2, což umožňuje konfiguraci DSC ke spuštění, pokud je počítač v aktuální nebo čekající na vyřízení stav. Pokud nechcete, aby konfiguraci, kterou chcete spustit počáteční spouštěcí up, třeba, nastavte hodnotu tohoto klíče na hodnotu 0:

1. Připojit virtuální pevný disk pomocí volání [připojit virtuální pevný disk](https://technet.microsoft.com/library/hh848551.aspx) rutiny. Příklad:

    ```powershell
    Mount-VHD -Path C:\users\public\documents\vhd\Srv16.vhd
    ```

2. Načíst registr **klíče HKLM\Software** podklíčů z virtuálního pevného disku voláním `reg load`.

    ```
    reg load HKLM\Vhd E:\Windows\System32\Config\Software`
    ```

3. Přejděte na **HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\***  pomocí poskytovatele prostředí PowerShell registru.

    ```powershell
    Set-Location HKLM:\Software\Microsoft\Windows\CurrentVersion\Policies`
    ```

4. Změňte hodnotu `DSCAutomationHostEnabled` na hodnotu 0.

    ```powershell
    Set-ItemProperty -Path . -Name DSCAutomationHostEnabled -Value 0
    ```

5. Uvolnění registru tak, že spustíte následující příkazy:

    ```powershell
    [gc]::Collect()
    reg unload HKLM\Vhd
    ```

## <a name="see-also"></a>Viz také

- [Konfigurace DSC](configurations.md)
- [Klíč registru DSCAutomationHostEnabled](DSCAutomationHostEnabled.md)
- [Konfigurace Local Configuration Manageru (LCM)](metaConfig.md)
- [Nastavení webového serveru vyžádané replikace DSC](pullServer.md)

