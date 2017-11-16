---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Začínáme s potřeby konfigurace stavu (DSC) pro Linux"
ms.openlocfilehash: fd4820d27de5958a325032ca3fc202a521c131b4
ms.sourcegitcommit: 28e71b0ae868014523631fec3f5417de751944f3
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/25/2017
---
# <a name="get-started-with-desired-state-configuration-dsc-for-linux"></a>Začínáme s potřeby konfigurace stavu (DSC) pro Linux

Toto téma vysvětluje, jak začít používat prostředí PowerShell požadovaného stavu konfigurace (DSC) pro Linux. Obecné informace o DSC najdete v tématu [začít pracovat s konfigurace požadovaného stavu aplikace Windows PowerShell](overview.md).

## <a name="supported-linux-operation-system-versions"></a>Podporované verze systému Linux operace

Následující verze operačního systému Linux jsou podporovány pro DSC pro Linux.
- CentOS 5, 6 a 7 (x86/x64)
- Debian GNU/Linux 6, 7 a 8 (x86/x64)
- Oracle Linux 5, 6 a 7 (x86/x64)
- Red Hat Enterprise Linux Server 5, 6 a 7 (x86/x64)
- SUSE Linux Enterprise Server 10, 11 a 12 (x86/x64)
- Ubuntu Server 12.04 LTS, 14.04 LTS a 16.04 LTS (x86/x64)

Následující tabulka popisuje závislosti požadovaný balíček pro DSC pro Linux.

|  Požadovaný balíček |  Popis |  Minimální verze | 
|---|---|---|
| Glibc| Knihovna GNU| 2…4 – 31.30| 
| Python| Python| 2.4 – 3.4| 
| omiserver| Infrastruktura OMI (Open Management Infrastructure)| 1.0.8.1| 
| OpenSSL| Knihovny OpenSSL| 0.9.8 nebo 1.0| 
| ctypes| Knihovna Python CTypes| Musí odpovídat verzi jazyka Python| 
| libcurl| Klientská knihovna pro cURL http| 7.15.1| 

## <a name="installing-dsc-for-linux"></a>Instalace DSC pro Linux

Je nutné nainstalovat [Open Management Infrastructure (OMI)](https://github.com/Microsoft/omi) před instalací DSC pro Linux.

### <a name="installing-omi"></a>Instalace OMI

Konfigurace stavu požadovaného pro Linux vyžaduje server CIM infrastruktury OMI (Open Management Infrastructure), verze 1.0.8.1 nebo novější. OMI si můžete stáhnout z otevřené skupiny: [Open Management Infrastructure (OMI)](https://github.com/Microsoft/omi).

Pokud chcete nainstalovat OMI, nainstalujte balíček, který je vhodný pro váš systém Linux (.rpm nebo .deb) a verzí OpenSSL (ssl_098 nebo ssl_100) a architektura (x64/x86). Ot. / min balíčky jsou vhodné pro CentOS, Red Hat Enterprise Linux, Oracle Linux a SUSE Linux Enterprise Server. Bázi DEB balíčky jsou vhodné pro Debian GNU/Linux a Ubuntu Server. Ssl_098 balíčky jsou vhodné pro počítače s OpenSSL 0.9.8 nainstalována při ssl_100 balíčky jsou vhodné pro počítače s OpenSSL 1.0 nainstalovaný.

> **Poznámka:**: Chcete-li zjistit, že nainstalovaná verze OpenSSL, spusťte příkaz `openssl version`.

Spusťte následující příkaz k instalaci v systému CentOS 7 x64 OMI.

`# sudo rpm -Uvh omiserver-1.0.8.ssl_100.rpm`

### <a name="installing-dsc"></a>Instalace DSC

DSC pro Linux je k dispozici ke stažení [zde](https://github.com/Microsoft/PowerShell-DSC-for-Linux/releases/latest). 

Pokud chcete nainstalovat DSC, nainstalujte balíček, který je vhodný pro váš systém Linux (.rpm nebo .deb) a verzí OpenSSL (ssl_098 nebo ssl_100) a architektura (x64/x86). Ot. / min balíčky jsou vhodné pro CentOS, Red Hat Enterprise Linux, Oracle Linux a SUSE Linux Enterprise Server. Bázi DEB balíčky jsou vhodné pro Debian GNU/Linux a Ubuntu Server. Ssl_098 balíčky jsou vhodné pro počítače s OpenSSL 0.9.8 nainstalována při ssl_100 balíčky jsou vhodné pro počítače s OpenSSL 1.0 nainstalovaný.

> **Poznámka:**: Chcete-li zjistit, že nainstalovaná verze OpenSSL, spusťte verze openssl příkaz.
 
Spusťte následující příkaz k instalaci v systému CentOS 7 x64 DSC.

`# sudo rpm -Uvh dsc-1.0.0-254.ssl_100.x64.rpm`


## <a name="using-dsc-for-linux"></a>Pro Linux pomocí DSC

Následující části popisují, jak vytvořit a spustit konfigurace DSC na počítače se systémem Linux.

### <a name="creating-a-configuration-mof-document"></a>Vytvoření dokumentu MOF konfigurace

Klíčové slovo konfigurace Windows Powershellu se používá k vytvoření konfiguraci pro počítače Linux, stejně jako pro počítače se systémem Windows. Následující kroky popisují vytvoření dokumentu konfigurace pro počítač se systémem Linux pomocí prostředí Windows PowerShell.

1. Naimportujte modul nx. Modul Windows PowerShell nx obsahuje schéma pro předdefinované prostředky pro DSC pro systémy Linux a musí být nainstalované do místního počítače a importovat v konfiguraci.

    – Chcete-li nainstalovat modul nx, zkopírujte adresář modulu nx buď `$env:USERPROFILE\Documents\WindowsPowerShell\Modules\` nebo `$PSHOME\Modules`. Modul nx je součástí DSC Linux instalačního balíčku (MSI). Chcete-li importovat modul nx ve vaší konfiguraci, použijte __Import DSCResource__ příkaz:
    
```powershell
Configuration ExampleConfiguration{
   
    Import-DSCResource -Module nx

}
```
2. Definice konfigurace a generování dokumentu konfigurace:

```powershell
Configuration ExampleConfiguration{
   
    Import-DscResource -Module nx
 
    Node  "linuxhost.contoso.com"{
    nxFile ExampleFile {

        DestinationPath = "/tmp/example"
        Contents = "hello world `n"
        Ensure = "Present"
        Type = "File"
    }

    }
}
ExampleConfiguration -OutputPath:"C:\temp" 
```

### <a name="push-the-configuration-to-the-linux-computer"></a>Nabízená konfiguraci počítače se systémem Linux

Konfigurace dokumenty (soubory MOF) můžete vloží do počítač Linux pomocí [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) rutiny. Chcete-li použít tuto rutinu spolu s [Get-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407379.aspx), nebo [Test DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) rutin vzdáleně na počítač se systémem Linux, je nutné použít CIMSession. [New-CimSession](http://go.microsoft.com/fwlink/?LinkId=227967) rutina se používá k vytvoření CIMSession do počítače se systémem Linux.

Následující kód ukazuje, jak vytvořit CIMSession pro DSC pro Linux.

```powershell
$Node = "ostc-dsc-01"
$Credential = Get-Credential -UserName:"root" -Message:"Enter Password:"

#Ignore SSL certificate validation
#$opt = New-CimSessionOption -UseSsl:$true -SkipCACheck:$true -SkipCNCheck:$true -SkipRevocationCheck:$true

#Options for a trusted SSL certificate
$opt = New-CimSessionOption -UseSsl:$true 
$Sess=New-CimSession -Credential:$credential -ComputerName:$Node -Port:5986 -Authentication:basic -SessionOption:$opt -OperationTimeoutSec:90 
```

> **Poznámka:**:
* "Push" režimu musí být přihlašovací údaje uživatele root uživatele na počítače se systémem Linux.
* Pro Linux, New-CimSession musí použít s parametrem – UseSSL nastaveným na $true, podporovaná jsou jenom připojení protokolem SSL/TLS pro DSC.
* Certifikát SSL používaný OMI (DSC) je zadána v souboru: `/opt/omi/etc/omiserver.conf` s vlastnostmi: pemfile a keyfile.
Pokud tento certifikát není důvěryhodný počítači s Windows, kterou používáte [New-CimSession](http://go.microsoft.com/fwlink/?LinkId=227967) na rutinu, můžete ignorovat ověření certifikátu s možnostmi CIMSession:`-SkipCACheck:$true -SkipCNCheck:$true -SkipRevocationCheck:$true`

Spusťte následující příkaz pro uložení konfigurace DSC k uzlu Linux.

`Start-DscConfiguration -Path:"C:\temp" -CimSession:$Sess -Wait -Verbose`

### <a name="distribute-the-configuration-with-a-pull-server"></a>Distribuce konfigurace serveru vyžádané replikace

Konfigurace můžete rozdělit počítač se systémem Linux pomocí serveru vyžádané replikace, stejně jako pro počítače se systémem Windows. Pokyny k používání serveru vyžádané replikace, najdete v části [Windows PowerShell požadovaného stavu konfigurace vyžadování servery](pullServer.md). Další informace a omezení související s použitím počítače se systémem Linux s načítacího serveru najdete v tématu poznámky k verzi pro konfigurace požadovaného stavu pro Linux.

### <a name="working-with-configurations-locally"></a>Práce s konfigurací místně

DSC pro Linux obsahuje skripty pro práci s konfiguraci z místního počítače se systémem Linux. Tyto skripty jsou najít v `/opt/microsoft/dsc/Scripts` a zahrnují následující:
* GetDscConfiguration.py

 Vrátí aktuální konfiguraci použita na počítač. Podobně jako rutiny Get-DscConfiguration rutinu prostředí Windows PowerShell.

`# sudo ./GetDscConfiguration.py`

* GetDscLocalConfigurationManager.py

 Vrátí aktuální meta konfigurace použita na počítač. Podobně jako rutiny [Get-DSCLocalConfigurationManager](https://technet.microsoft.com/en-us/library/dn407378.aspx) rutiny.

`# sudo ./GetDscLocalConfigurationManager.py`

* InstallModule.py

 Nainstaluje vlastní modul prostředků DSC. Vyžaduje cestu k souboru ZIP obsahující modulu objektu sdílené knihovny a soubory MOF schématu.

`# sudo ./InstallModule.py /tmp/cnx_Resource.zip`

* RemoveModule.py

 Odebere modul vlastní prostředek DSC. Vyžaduje název modulu odebrat.

`# sudo ./RemoveModule.py cnx_Resource`

* StartDscLocalConfigurationManager.py 

 Konfigurační soubor MOF se vztahuje na počítač. Podobně jako [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) rutiny. Vyžaduje cesta ke konfiguraci MOF použít.

`# sudo ./StartDscLocalConfigurationManager.py –configurationmof /tmp/localhost.mof`

* SetDscLocalConfigurationManager.py

 Soubor MOF Meta konfigurace se vztahuje na počítač. Podobně jako [Set-DSCLocalConfigurationManager](https://technet.microsoft.com/en-us/library/dn521621.aspx) rutiny. Vyžaduje cestu k MOF konfigurace Meta použít.

`# sudo ./SetDscLocalConfigurationManager.py –configurationmof /tmp/localhost.meta.mof`

## <a name="powershell-desired-state-configuration-for-linux-log-files"></a>Prostředí PowerShell konfigurace požadovaného stavu pro soubory protokolů systému Linux

Následující soubory protokolu jsou generovány pro DSC pro Linux zprávy.

|Soubor protokolu|Adresář|Popis|
|---|---|---|
|omiserver.log|/var/OPT/OMI/log|Zprávy týkající se operace server OMI CIM.|
|DSC.log|/var/OPT/OMI/log|Zprávy týkající se operace operace prostředků místní Configuration Manager (LCM) a DSC.|

