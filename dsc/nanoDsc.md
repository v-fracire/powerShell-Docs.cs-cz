---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Pomocí DSC na Nano Server"
ms.openlocfilehash: c8f3669ee9c2ed6107c14ba9f4460d82276e1932
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2018
---
# <a name="using-dsc-on-nano-server"></a>Pomocí DSC na Nano Server

> Platí pro: Prostředí Windows PowerShell 5.0

**DSC na Nano Server** je volitelný balíček v `NanoServer\Packages` složky na médiu systému Windows Server 2016. Balíček lze nainstalovat, když vytvoříte virtuální pevný disk pro Nano Server tak, že zadáte **Microsoft NanoServer DSC balíček** jako hodnotu **balíčky** parametr **New-NanoServerImage**  funkce. Například pokud vytváříte virtuální pevný disk pro virtuální počítač, příkaz vypadat takto:

```powershell
New-NanoServerImage -Edition Standard -DeploymentType Guest -MediaPath f:\ -BasePath .\Base -TargetPath .\Nano1\Nano.vhd -ComputerName Nano1 -Packages Microsoft-NanoServer-DSC-Package
```

Informace o instalaci a použití Nano Server a také jak spravovat Nano Server s vzdálenou komunikaci prostředí PowerShell najdete v tématu [Začínáme s Nano Server](https://technet.microsoft.com/library/mt126167.aspx).


## <a name="dsc-features-available-on-nano-server"></a>DSC funkce dostupné na Nano Server

 Protože Nano Server podporuje omezenou sadu rozhraní API ve srovnání s plnou verzí systému Windows Server, DSC na Nano Server nemá úplné funkčně rovnocenné s DSC na úplné SKU prozatím spuštěna. DSC na Nano Server je v active vývoj a ještě není funkce dokončení.
 
 Následující funkce DSC jsou aktuálně k dispozici na Nano Server: 


* Režimech nabízení a vyžadování

* Všechny rutiny DSC, které existují na plnou verzi Windows serveru, včetně následujících: 
  * [Get-DscLocalConfigurationManager](https://technet.microsoft.com/library/dn407378.aspx)
  * [Set-DscLocalConfigurationManager](https://technet.microsoft.com/library/dn521621.aspx)     
  * [Enable-DscDebug](https://technet.microsoft.com/en-us/library/mt517870.aspx)
  * [Disable-DscDebug](https://technet.microsoft.com/en-us/library/mt517872.aspx)       
  * [Počáteční DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx)
  * [Stop-DscConfiguration](https://technet.microsoft.com/en-us/library/mt143542.aspx)
  * [Get-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407379.aspx)
  * [Test-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx)      
  * [Publish-DscConfiguraiton](https://technet.microsoft.com/en-us/library/mt517875.aspx) 
  * [Update-DscConfiguration](https://technet.microsoft.com/en-us/library/mt143541.aspx)
  * [Obnovení DscConfiguration](https://technet.microsoft.com/en-us/library/dn407383.aspx)
  * [Remove-DscConfigurationDocument](https://technet.microsoft.com/en-us/library/mt143544.aspx)
  * [Get-DscConfigurationStatus](https://technet.microsoft.com/en-us/library/mt517868.aspx)
  * [Vyvolání DscResource](https://technet.microsoft.com/en-us/library/mt517869.aspx)
  * [Najít DscResource](https://technet.microsoft.com/en-us/library/mt517874.aspx)
  * [Get-DscResource](https://technet.microsoft.com/en-us/library/dn521625.aspx)
  * [New-DscChecksum](https://technet.microsoft.com/en-us/library/dn521622.aspx)    

* Kompilování konfigurace (viz [konfigurace DSC](configurations.md))

  **Problém:** šifrování hesla (viz [zabezpečení souboru MOF](securemof.md)) během konfigurace kompilace nefunguje.

* Kompilování metaconfigurations (viz [konfigurace správce místní konfigurace](metaConfig.md))

* Systémem prostředků v kontextu uživatele (viz [DSC spuštěná s pověřeními uživatele (Spustit jako)](runAsUser.md))

* Prostředky na základě – třída (najdete v části [zápis vlastní prostředek DSC pomocí prostředí PowerShell třídy](authoringResourceClass.md))

* Ladění prostředků DSC (viz [prostředky DSC ladění](debugresource.md))
  
  **Problém:** nefunguje, pokud prostředek používá PsDscRunAsCredential (viz [DSC spuštěná s pověřeními uživatele](runAsUser.md))

* [Určení závislostí mezi uzly](crossNodeDependencies.md) 

* [Správa verzí prostředků](sxsResource.md)

* Vyžádání klienta (konfigurace a prostředků) (v tématu [nastavení vyžadování klienta pomocí názvy konfigurace](pullClientConfigNames.md))

* [Částečné konfigurace (pull a push)](partialConfigs.md)

* [Vytváření sestav na server vyžádané replikace](reportServer.md) 

* Šifrování MOF

* Protokolování událostí

* Generování sestav služby Azure Automation DSC

* Prostředky, které jsou plně funkční
  * [Archiv](archiveResource.md)
  * [Prostředí](environmentResource.md)
  * [Soubor](fileResource.md)
  * [Protokolu](logResource.md)
  * ProcessSet
  * [Registru](registryResource.md)
  * [Skript](scriptResource.md)
  * WindowsPackageCab
  * [WindowsProcess](windowsProcessResource.md)
  * WaitForAll (viz [určení závislostí mezi uzly](crossNodeDependencies.md))
  * WaitForAny (viz [určení závislostí mezi uzly](crossNodeDependencies.md))
  * WaitForSome (viz [určení závislostí mezi uzly](crossNodeDependencies.md))

* Prostředky, které jsou částečně funkční
  * [Skupina](groupResource.md)
  * GroupSet
  
  **Problém:** výše prostředků nezdaří, pokud je konkrétní instanci volala dvakrát (spouštění dvakrát stejnou konfiguraci)
  
  * [Služby](serviceResource.md)
  * ServiceSet
  
  **Problém:** funguje jenom pro spuštění nebo zastavení služby (stav). Selže, pokud se jeden pokusí změnit další atributy služby jako startuptype, přihlašovací údaje, popis atd... Vyvolána chyba je podobná:
  
  *Nelze najít typ [management.managementobject]: Ověřte, že je načteno sestavení obsahující tohoto typu.*
  
* Prostředky, které nejsou funkční
  * [Uživatel](userResource.md)
  

## <a name="dsc-features-not-available-on-nano-server"></a>DSC funkce není k dispozici v Nano Server

Následující funkce DSC nejsou momentálně k dispozici na Nano Server:

* Dešifrování MOF dokument s šifrované Změna hesla 
* Vyžádání obsahu Server--nemůžete nastavit aktuálně na server vyžádané replikace v Nano Server
* Všechno, co se nenachází v seznamu funkce funguje

## <a name="using-custom-dsc-resources-on-nano-server"></a>Pomocí vlastní prostředky DSC v Nano Server
 
Z důvodu omezenou sadu rozhraní API systému Windows a CLR knihovny k dispozici na serveru Nano prostředků DSC, které fungují na plnou verzi Windows CLR nemusí pracovat na Nano Server. Dokončení začátku do konce testování před nasazením jakékoli vlastní prostředky DSC v produkčním prostředí.

## <a name="see-also"></a>Viz také
- [Začínáme s Nano Server](https://technet.microsoft.com/library/mt126167.aspx)

