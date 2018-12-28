---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Použití platformy DSC na Nano Serveru
ms.openlocfilehash: fd81fe56d16100f45d9ee2dfd8fdc303c2a6c17a
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403727"
---
# <a name="using-dsc-on-nano-server"></a>Použití platformy DSC na Nano Serveru

> Platí pro: Windows PowerShell 5.0

**DSC na Nano serveru** je volitelný balíček v `NanoServer\Packages` složky média systému Windows Server 2016. Balíček lze nainstalovat při vytváření virtuálního pevného disku pro Nano Server tak, že zadáte **Microsoft-NanoServer-DSC-Package** jako hodnotu **balíčky** parametr **rutiny New-NanoServerImage**  funkce. Například při vytváření virtuálního pevného disku pro virtuální počítač, tento příkaz může vypadat nějak takto:

```powershell
New-NanoServerImage -Edition Standard -DeploymentType Guest -MediaPath f:\ -BasePath .\Base -TargetPath .\Nano1\Nano.vhd -ComputerName Nano1 -Packages Microsoft-NanoServer-DSC-Package
```

Informace o instalaci a použití Nano serveru, jakož i jak spravovat Nano serveru pomocí vzdálené komunikace Powershellu najdete v tématu [Začínáme s Nano serverem](/windows-server/get-started/getting-started-with-nano-server).

## <a name="dsc-features-available-on-nano-server"></a>Funkce DSC na Nano serveru k dispozici

Protože Nano Server podporuje pouze omezená sada rozhraní API ve srovnání s plnou verzí Windows serveru, DSC na Nano serveru s DSC běžící na úplné SKU prozatím úplnou paritu nemá. DSC na Nano serveru je v aktivním vývoji a ještě není kompletní funkce.

Následující funkce DSC jsou nyní dostupné na Nano serveru:

Režimech nabízení a vyžadování

- Všechny rutiny DSC, které existují na plnou verzi Windows serveru, včetně následujících:
- [Get-DscLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Get-DscLocalConfigurationManager)
- [Set-DscLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Set-DscLocalConfigurationManager)
- [Enable-DscDebug](/powershell/module/PSDesiredStateConfiguration/Enable-DscDebug)
- [Zakázat DscDebug](/powershell/module/PSDesiredStateConfiguration/Disable-DscDebug)
- [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration)
- [Stop-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Stop-DscConfiguration)
- [Get-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Get-DscConfiguration)
- [Test-DscConfiguration](/powershell/module/psdesiredstateconfiguration/Test-DSCConfiguration)
- [Publikování DscConfiguraiton](/powershell/module/PSDesiredStateConfiguration/Publish-DscConfiguration)
- [Update-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Update-DscConfiguration)
- [Restore-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Restore-DscConfiguration)
- [Odebrat DscConfigurationDocument](/powershell/module/PSDesiredStateConfiguration/Remove-DscConfigurationDocument)
- [Get-DscConfigurationStatus](/powershell/module/PSDesiredStateConfiguration/Get-DscConfigurationStatus)
- [Invoke-DscResource](/powershell/module/PSDesiredStateConfiguration/Invoke-DscResource)
- [Find-DscResource](https://technet.microsoft.com/en-us/library/mt517874.aspx)
- [Get-DscResource](/powershell/module/PSDesiredStateConfiguration/Get-DscResource)
- [New-DscChecksum](/powershell/module/PSDesiredStateConfiguration/New-DSCCheckSum)

- Kompilace konfigurací (viz [konfigurací DSC](../configurations/configurations.md))

  **Problém:** Heslo šifrování (viz [zabezpečení souboru MOF](../pull-server/secureMOF.md)) během konfigurace kompilace nefunguje.

- Kompilování metaconfigurations (viz [konfigurace Local Configuration Manageru](../managing-nodes/metaConfig.md))

- S prostředkem v kontextu uživatele (viz [DSC spuštěná s pověřeními uživatele (Spustit jako)](../configurations/runAsUser.md))

- Prostředky založené na třídě (viz [psaní vlastního prostředku DSC pomocí tříd Powershellu](../resources/authoringResourceClass.md))

- Ladění prostředků DSC (viz [prostředky DSC ladění](../troubleshooting/debugResource.md))

  **Problém:** Nefunguje, pokud prostředek používá PsDscRunAsCredential (naleznete v tématu [DSC spuštěná s pověřeními uživatele](../configurations/runAsUser.md))

- [Určení závislostí mezi uzly](../configurations/crossNodeDependencies.md)

- [Správa verzí prostředků](../configurations/sxsResource.md)

- Načítacího klienta (konfigurace a prostředky) (viz [nastavení načítacího klienta použití konfiguračních názvů](../pull-server/pullClientConfigNames.md))

- [Částečné konfigurace (pull a push)](../pull-server/partialConfigs.md)

- [Generování sestav na serveru vyžádané replikace](../pull-server/reportServer.md)

- Šifrování MOF

- Protokolování událostí

- Generování sestav v Azure Automation DSC

- Prostředky, které jsou plně funkční

- **Archiv**
- **Prostředí**
- **Soubor**
- **Protokol**
- **ProcessSet**
- **registru**
- **Skript**
- **WindowsPackageCab**
- **WindowsProcess**
- **WaitForAll** (viz [určení závislostí mezi uzly](../configurations/crossNodeDependencies.md))
- **WaitForAny** (viz [určení závislostí mezi uzly](../configurations/crossNodeDependencies.md))
- **WaitForSome** (viz [určení závislostí mezi uzly](../configurations/crossNodeDependencies.md))

- Prostředky, které jsou částečně funkční
- **Skupina**
- **GroupSet**

  **Problém:** Nad prostředky selhat, pokud je konkrétní instanci volána dvakrát (spuštění dvakrát se stejnou konfigurací)

- **Služba**
- **ServiceSet**

  **Problém:** Funguje jenom pro spuštění/zastavení služby (stav). Selže, pokud se jeden pokusí změnit další atributy služby jako typ spuštění, přihlašovací údaje, popis atd. Je podobný vyvolána chyba:

  *Nepovedlo se najít typ [management.managementobject]: Ověřte, že je načteno sestavení obsahující tohoto typu.*

- Prostředky, které nejsou funkční
- **Uživatel**

## <a name="dsc-features-not-available-on-nano-server"></a>Funkce DSC na Nano serveru není k dispozici

Následující funkce DSC nejsou aktuálně dostupné na Nano serveru:

- Dešifrování dokument MOF se změna šifrovaná hesla
- Server o přijetí změn – nelze nastavit aktuálně serveru vyžádané replikace na Nano serveru
- Cokoli, co není v seznamu funkcí funguje

## <a name="using-custom-dsc-resources-on-nano-server"></a>Použití vlastní prostředky DSC na Nano serveru

Kvůli omezené sady rozhraní API pro Windows a knihovny CLR na Nano serveru k dispozici prostředky DSC, pracující na plnou verzi CLR Windows nemusí pracovat na Nano serveru.
Dokončení začátku do konce testování před nasazením jakékoli vlastní prostředky DSC do produkčního prostředí.

## <a name="see-also"></a>Viz také

- [Začínáme s Nano serverem](/windows-server/get-started/getting-started-with-nano-server)
