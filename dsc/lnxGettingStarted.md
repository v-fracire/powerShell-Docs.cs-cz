---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Začínáme s Desired State Configuration (DSC) pro Linux
ms.openlocfilehash: d436fc3b451efb8a12dfdc44909824934b5fcbe4
ms.sourcegitcommit: e46b868f56f359909ff7c8230b1d1770935cce0e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/13/2018
ms.locfileid: "45523011"
---
# <a name="get-started-with-desired-state-configuration-dsc-for-linux"></a>Začínáme s Desired State Configuration (DSC) pro Linux

Toto téma vysvětluje, jak začít používat prostředí PowerShell Desired State Configuration (DSC) pro Linux. Obecné informace o DSC najdete v tématu [začít pracovat s Windows PowerShell Desired State Configuration](overview.md).

## <a name="supported-linux-operation-system-versions"></a>Podporované verze systému Linux operace

Tyto verze operačních systémů Linux jsou podporovány pro DSC pro Linux.

- CentOS 5, 6 a 7 (x86/x64)
- Debian GNU/Linux 6, 7 a 8 (x86/x64)
- Oracle Linux 5, 6 a 7 (x86/x64)
- Red Hat Enterprise Linux Server 5, 6 a 7 (x86/x64)
- SUSE Linux Enterprise Server 10, 11 a 12 (x86/x64)
- Server se systémem Ubuntu 12.04 LTS, 14.04 LTS a 16.04 LTS (x86/x64)

Následující tabulka popisuje závislosti požadovaný balíček pro DSC pro Linux.

|  Požadovaný balíček |  Popis |  Minimální verze |
|---|---|---|
| knihovnou glibc| Knihovna GNU.| 2... 4 – 31.30|
| Python| Python| 2.4 – 3.4|
| omiserver| Infrastruktura OMI (Open Management Infrastructure)| 1.0.8.1|
| OpenSSL| Knihovny OpenSSL| 0.9.8 nebo 1.0|
| ctypes| Knihovna Python CTypes| Musí odpovídat verzi Pythonu|
| libcurl| knihovny klienta http cURL| 7.15.1|

## <a name="installing-dsc-for-linux"></a>Instalace DSC pro Linux

Je nutné nainstalovat [Open Management Infrastructure (OMI)](https://github.com/Microsoft/omi) před instalací DSC pro Linux.

### <a name="installing-omi"></a>Instalace infrastruktury OMI

Desired State Configuration pro Linux vyžaduje server CIM Open Management Infrastructure (OMI), verze 1.0.8.1 nebo novější. OMI je možné stáhnout z The Open Group: [Open Management Infrastructure (OMI)](https://github.com/Microsoft/omi).

Instalace infrastruktury OMI, nainstalujte balíček, který je vhodný pro systém Linux (.rpm nebo .deb) a verze OpenSSL (ssl_098 nebo ssl_100) a architektura (x64/x86). Ot. / min balíčky jsou vhodné pro CentOS, Red Hat Enterprise Linux, SUSE Linux Enterprise Server a Oracle Linux. DEB balíčky jsou vhodné pro Debian GNU/Linux a Ubuntu Server. Ssl_098 balíčky jsou vhodné pro počítače s OpenSSL 0.9.8 nainstalovali při ssl_100 balíčky jsou vhodné pro počítače s OpenSSL 1.0 nainstalované.

> [!NOTE]
> Pokud chcete zjistit nainstalovanou verzi OpenSSL, spusťte příkaz `openssl version`.

Spusťte následující příkaz k instalaci v systému CentOS 7 x64 OMI.

`# sudo rpm -Uvh omiserver-1.0.8.ssl_100.rpm`

### <a name="installing-dsc"></a>Instalaci DSC

DSC pro Linux je k dispozici ke stažení [tady](https://github.com/Microsoft/PowerShell-DSC-for-Linux/releases/tag/v1.1.1-294).

K instalaci DSC, nainstalujte balíček, který je vhodný pro systém Linux (.rpm nebo .deb) a verze OpenSSL (ssl_098 nebo ssl_100) a architektura (x64/x86). Ot. / min balíčky jsou vhodné pro CentOS, Red Hat Enterprise Linux, SUSE Linux Enterprise Server a Oracle Linux. DEB balíčky jsou vhodné pro Debian GNU/Linux a Ubuntu Server. Ssl_098 balíčky jsou vhodné pro počítače s OpenSSL 0.9.8 nainstalovali při ssl_100 balíčky jsou vhodné pro počítače s OpenSSL 1.0 nainstalované.

> [!NOTE]
> K určení Instalovatelné verze OpenSSL, spusťte příkaz verze openssl.

Spusťte následující příkaz k instalaci v systému CentOS 7 x64 DSC.

`# sudo rpm -Uvh dsc-1.0.0-254.ssl_100.x64.rpm`

## <a name="using-dsc-for-linux"></a>Pomocí DSC pro Linux

Následující části popisují, jak vytvářet a spouštět konfigurací DSC na počítače s Linuxem.

### <a name="creating-a-configuration-mof-document"></a>Vytvoření dokumentu MOF konfigurace

Konfigurace Windows Powershellu – klíčové slovo se používá pro vytvoření konfigurace pro počítače s Linuxem, stejně jako u počítačů s Windows. Následující kroky popisují vytvoření dokumentu konfigurace pro počítač s Linuxem pomocí Windows Powershellu.

1. Naimportujte modul nx. Modul prostředí Windows PowerShell nx obsahuje schéma pro integrované prostředky pro DSC pro Linux a musí být nainstalované na místním počítači a importu v konfiguraci.

   - Pokud chcete nainstalovat modul nx, zkopírujte adresář modulu nx buď `$env:USERPROFILE\Documents\WindowsPowerShell\Modules\` nebo `$PSHOME\Modules`. Modul nx je součástí DSC pro Linux instalační balíček. Chcete-li importovat modul nx v konfiguraci, použijte `Import-DSCResource` příkaz:

   ```powershell
   Configuration ExampleConfiguration{

    Import-DSCResource -Module nx

   }
   ```

2. Definice konfigurace a generovat dokument konfigurace:

   ```powershell
   Configuration ExampleConfiguration
   {
        Import-DscResource -Module nx

        Node  "linuxhost.contoso.com"
        {
            nxFile ExampleFile 
            {
                DestinationPath = "/tmp/example"
                Contents = "hello world `n"
                Ensure = "Present"
                Type = "File"
            }
        }
   }

   ExampleConfiguration -OutputPath:"C:\temp"
   ```

### <a name="push-the-configuration-to-the-linux-computer"></a>Push v konfiguraci pro počítače s Linuxem

Konfigurace dokumentů (soubory MOF) je možné nabídnout pro Linux pomocí počítače [Start-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Start-DscConfiguration) rutiny. Chcete-li použít tuto rutinu spolu s [Get-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Get-DscConfiguration), nebo [Test-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Test-DscConfiguration) rutiny, vzdáleně k počítači s Linuxem, je nutné použít CIMSession. [New-CimSession](http://go.microsoft.com/fwlink/?LinkId=227967) rutina se používá k vytvoření CIMSession do počítače s Linuxem.

Následující kód ukazuje, jak vytvořit CIMSession DSC pro Linux.

```powershell
$Node = "ostc-dsc-01"
$Credential = Get-Credential -UserName:"root" -Message:"Enter Password:"

#Ignore SSL certificate validation
#$opt = New-CimSessionOption -UseSsl:$true -SkipCACheck:$true -SkipCNCheck:$true -SkipRevocationCheck:$true

#Options for a trusted SSL certificate
$opt = New-CimSessionOption -UseSsl:$true
$Sess=New-CimSession -Credential:$credential -ComputerName:$Node -Port:5986 -Authentication:basic -SessionOption:$opt -OperationTimeoutSec:90
```

> [!NOTE]
> Pro režim "Push" musí být přihlašovací údaje uživatele kořenového uživatele na počítači s Linuxem.
> Pro DSC pro Linux, jsou podporovány pouze připojení SSL/TLS `New-CimSession` musí použít s parametrem – UseSSL nastaveným na $true.
> Certifikát SSL používaný OMI (DSC) je zadán v souboru: `/opt/omi/etc/omiserver.conf` s vlastnostmi: pemfile a keyfile.
> Pokud tento certifikát není důvěryhodný počítač Windows, kterou používáte [New-CimSession](http://go.microsoft.com/fwlink/?LinkId=227967) na rutinu, můžete přeskočit ověření certifikátu s parametry CIMSession: `-SkipCACheck:$true -SkipCNCheck:$true -SkipRevocationCheck:$true`

Spusťte následující příkaz tak, aby nabízel konfigurace DSC k uzlu systému Linux.

`Start-DscConfiguration -Path:"C:\temp" -CimSession:$Sess -Wait -Verbose`

### <a name="distribute-the-configuration-with-a-pull-server"></a>Distribuce konfigurace serveru vyžádané replikace

Konfigurace lze distribuovat na počítači s Linuxem pomocí serveru vyžádané replikace, stejně jako u počítačů s Windows. Pokyny k používání serveru vyžádané replikace najdete v tématu [Windows PowerShell Desired State Configuration o přijetí změn servery](pullServer.md). Další informace a omezení týkající se počítače s Linuxem pomocí serveru vyžádané replikace najdete v tématu poznámky k verzi pro Desired State Configuration pro Linux.

### <a name="working-with-configurations-locally"></a>Práce s konfigurací místně

DSC pro Linux zahrnuje skriptů pro práci s konfigurací z místního počítače s Linuxem. Tyto skripty jsou vyhledejte v `/opt/microsoft/dsc/Scripts` a zahrnují následující:

- GetDscConfiguration.py

Vrátí aktuální konfiguraci použita na počítač. Podobně jako rutiny Windows Powershellu `Get-DscConfiguration` rutiny.

`# sudo ./GetDscConfiguration.py`

- GetDscLocalConfigurationManager.py

Vrátí aktuální meta konfigurace použita na počítač. Podobně jako rutiny [Get-DSCLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Get-DscLocalConfigurationManager) rutiny.

`# sudo ./GetDscLocalConfigurationManager.py`

- InstallModule.py

Nainstaluje vlastní modul zdroje DSC. Vyžaduje se cesta k souboru ZIP obsahující modul sdíleného objektu knihovny a soubory MOF schématu.

`# sudo ./InstallModule.py /tmp/cnx_Resource.zip`

- RemoveModule.py

Odebere vlastního modulu prostředků DSC. Vyžaduje název modulu, který chcete odebrat.

`# sudo ./RemoveModule.py cnx_Resource`

- StartDscLocalConfigurationManager.py

Konfiguračního souboru MOF se vztahuje na počítač. Podobně jako [Start-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Start-DscConfiguration) rutiny. Vyžaduje cesta ke konfiguraci MOF, který chcete použít.

`# sudo ./StartDscLocalConfigurationManager.py –configurationmof /tmp/localhost.mof`

- SetDscLocalConfigurationManager.py

Soubor MOF Meta konfigurace se vztahuje na počítač. Podobně jako [Set-DSCLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Set-DscLocalConfigurationManager) rutiny. Vyžaduje cesta ke konfiguraci MOF Meta použít.

`# sudo ./SetDscLocalConfigurationManager.py –configurationmof /tmp/localhost.meta.mof`

## <a name="powershell-desired-state-configuration-for-linux-log-files"></a>Prostředí PowerShell Desired State Configuration pro soubory protokolů systému Linux

Následující soubory protokolu jsou generovány pro DSC pro Linux zprávy.

|Soubor protokolu|Adresář|Popis|
|---|---|---|
|**omiserver.log**|`/var/opt/omi/log`|Zprávy týkající se fungování server OMI CIM.|
|**DSC.log**|`/var/opt/omi/log`|Zprávy týkající se fungování operace prostředků místní Configuration Manageru (LCM) a DSC.|
