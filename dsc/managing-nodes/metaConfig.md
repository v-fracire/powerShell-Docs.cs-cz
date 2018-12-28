---
ms.date: 12/12/2018
keywords: DSC, powershell, konfigurace, instalační program
title: Konfigurace Local Configuration Manageru
ms.openlocfilehash: c3ced2376c7d99477c40ae078dcecd775538b350
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403751"
---
# <a name="configuring-the-local-configuration-manager"></a>Konfigurace Local Configuration Manageru

> Platí pro: Windows PowerShell 5.0

Místní Configuration Manageru (LCM) je modul sady Desired State Configuration (DSC).
LCM běží na každý cílový uzel a je zodpovědné za parsování a přijetí konfigurace, které se odesílají do uzlu.
Také je zodpovědná za celou řadou dalších aspektů DSC, včetně následujících.

- Určení režimu aktualizace (nabízení nebo vyžádání).
- Určení, jak často uzlu si vyžádá a představuje konfigurace.
- Uzel přidružení službu přijetí změn.
- Zadání částečné konfigurace.

Použijete ke konfiguraci funkce LCM se každá z těchto projevů zadat speciální typ konfigurace.
Konfigurace LCM v následujících částech.

Windows PowerShell 5.0 zavedená nová nastavení pro správu Local Configuration Manageru.
Informace týkající se konfigurace LCM v Powershellu 4.0 Windows najdete v tématu [konfigurace Local Configuration Manageru v předchozích verzích Windows Powershellu](metaconfig4.md).

## <a name="writing-and-enacting-an-lcm-configuration"></a>Vytváření a konfiguraci služby LCM přijetí

Konfigurace LCM, vytvářet a spouštět speciální typ konfigurace, která se použije LCM nastavení.
Pokud chcete zadat konfiguraci služby LCM, použijte atribut DscLocalConfigurationManager.
Následující uvádí jednoduchý konfigurace, které nastaví LCM na režimu nabízení.

```powershell
[DSCLocalConfigurationManager()]
configuration LCMConfig
{
    Node localhost
    {
        Settings
        {
            RefreshMode = 'Push'
        }
    }
}
```

Použití nastavení LCM proces je podobný aplikování konfigurace DSC.
Vytvořit konfiguraci LCM, zkompilovat jej do souboru MOF a použít ho k uzlu.
Na rozdíl od konfigurace DSC, ne vydává konfiguraci služby LCM voláním [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) rutiny.
Namísto toho zavolejte metodu [Set-DscLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Set-DscLocalConfigurationManager), zadáním cesty ke konfiguraci LCM MOF jako parametr.
Po vás vydává konfigurace LCM, můžete zobrazit vlastnosti LCM voláním [Get-DscLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Get-DscLocalConfigurationManager) rutiny.

Konfigurace LCM služby může obsahovat bloků pouze pro omezenou sadu prostředků.
V předchozím příkladu je jediný zdroj volá **nastavení**.
Jsou k dispozici prostředky:

* **ConfigurationRepositoryWeb**: Určuje službě HTTP o přijetí změn konfigurace.
* **ConfigurationRepositoryShare**: Určuje, do sdílené složky protokolu SMB pro konfigurace.
* **ResourceRepositoryWeb**: Určuje služby HTTP o přijetí změn pro moduly.
* **ResourceRepositoryShare**: Určuje, do sdílené složky protokolu SMB pro moduly.
* **ReportServerWeb**: Určuje, ke které se odesílají zprávy službě o přijetí změn s protokolem HTTP.
* **PartialConfiguration**: poskytuje data k povolení částečné konfigurace.

## <a name="basic-settings"></a>Základní nastavení

Kromě zadání částečné konfigurace a o přijetí změn služby koncové body nebo cesty, všechny vlastnosti LCM konfigurované v **nastavení** bloku.
Následující vlastnosti jsou k dispozici v **nastavení** bloku.

|  Vlastnost  |  Typ  |  Popis   |
|----------- |------- |--------------- |
| ActionAfterReboot| řetězec| Určuje, co se stane po restartování během konfigurace aplikace. Možné hodnoty jsou __"ContinueConfiguration"__ a __"StopConfiguration"__. <ul><li> __ContinueConfiguration__: Pokračujte v používání aktuální konfiguraci po restartování počítače. Toto je výchozí hodnota</li><li>__StopConfiguration__: Zastavte aktuální konfiguraci po restartování počítače.</li></ul>|
| AllowModuleOverwrite| BOOL| __$TRUE__ Pokud nové konfigurace stažené z službu přijetí změn se může přepsat staré na cílovém uzlu. Jinak $FALSE.|
| CertificateID| řetězec| Kryptografický otisk certifikát používaný k zabezpečení přihlašovacích údajů předaných v konfiguraci. Další informace najdete v části [chcete zabezpečené přihlašovací údaje ve Windows Powershellu Desired State Configuration](http://blogs.msdn.com/b/powershell/archive/2014/01/31/want-to-secure-credentials-in-windows-powershell-desired-state-configuration.aspx)?. <br> __Poznámka:__ je při použití služby Azure Automation DSC o přijetí změn automaticky spravován.|
| ConfigurationDownloadManagers| [] CimInstance| Zastaralé. Použití __ConfigurationRepositoryWeb__ a __ConfigurationRepositoryShare__ koncové body služby bloky k definování o přijetí změn konfigurace.|
| ConfigurationID| řetězec| Pro zpětnou kompatibilitu s starší o přijetí změn služby verzí. Identifikátor GUID, který identifikuje konfiguračního souboru získat ze služby o přijetí změn. Uzel přetáhne konfigurace na službu přijetí změn, pokud se název konfigurace MOF jmenuje ConfigurationID.mof.<br> __Poznámka:__ Pokud tuto vlastnost nastavíte registraci uzlu službou o přijetí změn pomocí __RegistrationKey__ nefunguje. Další informace najdete v tématu [nastavení načítacího klienta s názvy konfigurace](../pull-server/pullClientConfigNames.md).|
| ConfigurationMode| řetězec | Určuje, jak LCM skutečně aplikuje konfiguraci na cílové uzly. Možné hodnoty jsou __"ApplyOnly"__,__"ApplyAndMonitor"__, a __"ApplyAndAutoCorrect"__. <ul><li>__ApplyOnly__: DSC aplikuje konfiguraci a neprovede žádnou další akci, pokud nová konfigurace se vloží do cílového uzlu nebo když nová konfigurace se stáhne ze služby. Po počáteční použití nové konfigurace DSC nekontroluje odchylky od dříve nakonfigurované stavu. Všimněte si, že DSC se pokusí použít konfiguraci, dokud nebude úspěšná, až poté __ApplyOnly__ projeví. </li><li> __ApplyAndMonitor__: Tato hodnota je výchozí. LCM platí všechny nové konfigurace. Po počáteční aplikaci novou konfiguraci Pokud cílový uzel drifts z požadovaného stavu sestavy DSC nesrovnalosti v protokolech. Všimněte si, že DSC se pokusí použít konfiguraci, dokud nebude úspěšná, až poté __ApplyAndMonitor__ projeví.</li><li>__ApplyAndAutoCorrect__: DSC platí všechny nové konfigurace. Po počáteční aplikaci novou konfiguraci Pokud cílový uzel drifts z požadovaného stavu DSC sestavy nesrovnalosti v protokolech a poté znovu použije aktuální konfiguraci.</li></ul>|
| ConfigurationModeFrequencyMins| UInt32| Jak často během několika minut, aktuální konfigurace je zaškrtnuto a použít. Tato vlastnost se ignoruje, pokud je vlastnost ConfigurationMode nastavena na ApplyOnly. Výchozí hodnota je 15.|
| Režim DebugMode| řetězec| Možné hodnoty jsou __žádný__, __ForceModuleImport__, a __všechny__. <ul><li>Nastavte na __žádný__ používat prostředky uložené v mezipaměti. Toto je výchozí a by měl používat v produkčních scénářích.</li><li>Nastavení na hodnotu __ForceModuleImport__, způsobí, že funkce LCM se znovu načíst všechny moduly prostředků DSC, i když mají byla dříve načtena a uložili do mezipaměti. Toto nastavení ovlivňuje výkon operací DSC jako při použití opětovném načtení nástroje každý modul. Obvykle byste tuto hodnotu použijete při ladění zdroje</li><li>V této verzi __všechny__ je stejná jako __ForceModuleImport__</li></ul> |
| RebootNodeIfNeeded| BOOL| Nastavte na __$true__ k automatickému restartování uzlu po konfiguraci, která vyžaduje restartování počítače se použije. V opačném případě budete muset ručně restartovat uzel pro všechny konfigurace, který jej vyžaduje. Výchozí hodnota je __$false__. Pokud chcete použít toto nastavení při restartování podmínka je vydaných něco jiného než DSC (například Instalační služby systému Windows), zkombinovat tato nastavení se [xPendingReboot](https://github.com/powershell/xpendingreboot) modulu.|
| RefreshMode| řetězec| Určuje, jak LCM získá konfigurace. Možné hodnoty jsou __"Zakázáno"__, __"Push"__, a __"Pull"__. <ul><li>__Zakázané__: Konfigurace DSC jsou zakázané pro tento uzel.</li><li> __Push__: Konfigurace lze inicializovat pomocí volání [Start-DscConfiguration](/powershell/module/psdesiredstateconfiguration/start-dscconfiguration) rutiny. Konfigurace se okamžitě použije k uzlu. Tato hodnota je výchozí.</li><li>__Stáhněte si:__ Uzel je nakonfigurován na pravidelně vyhledávat konfigurace ze služby o přijetí změn nebo cesta k protokolu SMB. Pokud je tato vlastnost nastavená na __o přijetí změn__, musíte zadat cestu protokolu SMB (sdílené složky) v případě protokolu HTTP (služba) __ConfigurationRepositoryWeb__ nebo __ConfigurationRepositoryShare__ bloku.</li></ul>|
| RefreshFrequencyMins| Uint32| Časový interval v minutách, na kterých LCM zkontroluje službu přijetí změn, chcete-li získat aktualizované konfigurace. Tato hodnota je ignorována, pokud LCM není nakonfigurované v režimu o přijetí změn. Výchozí hodnota je 30.|
| ReportManagers| [] CimInstance| Zastaralé. Použití __ReportServerWeb__ bloky k definování koncového bodu odeslat data pro generování sestav o přijetí změn služby.|
| ResourceModuleManagers| [] CimInstance| Zastaralé. Použití __ResourceRepositoryWeb__ a __ResourceRepositoryShare__ bloky k definování o přijetí změn služeb koncových bodů HTTP nebo cesty k protokolu SMB, v uvedeném pořadí.|
| PartialConfigurations| CimInstance| Není implementováno. Nepoužívat.|
| StatusRetentionTimeInDays | UInt32| Počet dní, po které LCM sleduje stav aktuální konfiguraci.|

## <a name="pull-service"></a>Načítací služba

Konfigurace LCM podporuje definovat následující typy koncových bodů služby o přijetí změn:

- **Konfigurační server**: Úložiště pro konfiguraci DSC. Definování konfiguračních serverů s použitím **ConfigurationRepositoryWeb** (pro webové servery) a **ConfigurationRepositoryShare** (pro servery založené na protokolu SMB) bloky.
- **Server prostředků**: Úložiště prostředků DSC, lze zabalit jako moduly Powershellu. Definovat servery prostředků pomocí **ResourceRepositoryWeb** (pro webové servery) a **ResourceRepositoryShare** (pro servery založené na protokolu SMB) bloky.
- **Server sestav**: Služba, která odesílá data sestavy DSC. Definovat servery sestav pomocí **ReportServerWeb** bloky. Webové služby musí být server sestav.

Další podrobnosti o přijetí změn služby najdete v tématu, [Desired State Configuration načítací služba](../pull-server/pullServer.md).

## <a name="configuration-server-blocks"></a>Konfigurace serveru bloky

Chcete-li definovat konfiguraci webového serveru, vytvoříte **ConfigurationRepositoryWeb** bloku.
A **ConfigurationRepositoryWeb** definuje následující vlastnosti.

|Vlastnost|Typ|Popis|
|---|---|---|
|AllowUnsecureConnection|BOOL|Nastavte na **$TRUE** umožňující připojení k serveru bez ověřování z uzlu. Nastavte na **$FALSE** tak, aby vyžadovala ověřování.|
|CertificateID|řetězec|Kryptografický otisk certifikátu používá k ověření serveru.|
|ConfigurationNames|Řetězec]|Pole názvů konfigurací i cílový uzel. Ty se používají pouze v případě, že uzel je registrovaný ve službe o přijetí změn s využitím **RegistrationKey**. Další informace najdete v tématu [nastavení načítacího klienta s názvy konfigurace](../pull-server/pullClientConfigNames.md).|
|RegistrationKey|řetězec|Identifikátor GUID, který registruje uzel službou o přijetí změn. Další informace najdete v tématu [nastavení načítacího klienta s názvy konfigurace](../pull-server/pullClientConfigNames.md).|
|URL serveru|řetězec|Adresa URL služby konfigurace.|

Ukázkový skript pro zjednodušení konfigurace hodnotu ConfigurationRepositoryWeb místních uzlech je k dispozici – viz [metaconfigurations generování DSC](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-onboarding#generating-dsc-metaconfigurations)

Chcete-li definovat založenou na protokolu SMB konfigurační server, vytvoříte **ConfigurationRepositoryShare** bloku.
A **ConfigurationRepositoryShare** definuje následující vlastnosti.

|Vlastnost|Typ|Popis|
|---|---|---|
|Přihlašovací údaje|MSFT_Credential|Přihlašovací údaje pro ověření do sdílené složky SMB.|
|SourcePath|řetězec|Cesta sdílenou složku SMB.|

## <a name="resource-server-blocks"></a>Bloků serveru prostředků

Chcete-li definovat prostředek založený na web server, vytvoříte **ResourceRepositoryWeb** bloku.
A **ResourceRepositoryWeb** definuje následující vlastnosti.

|Vlastnost|Typ|Popis|
|---|---|---|
|AllowUnsecureConnection|BOOL|Nastavte na **$TRUE** umožňující připojení k serveru bez ověřování z uzlu. Nastavte na **$FALSE** tak, aby vyžadovala ověřování.|
|CertificateID|řetězec|Kryptografický otisk certifikátu používá k ověření serveru.|
|RegistrationKey|řetězec|Identifikátor GUID, který identifikuje uzel, který má službu přijetí změn.|
|URL serveru|řetězec|Adresa URL konfiguračního serveru.|

Ukázkový skript pro zjednodušení konfigurace hodnotu ResourceRepositoryWeb místních uzlech je k dispozici – viz [metaconfigurations generování DSC](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-onboarding#generating-dsc-metaconfigurations)

Chcete-li definovat serveru prostředek založený na protokolu SMB, vytvoříte **ResourceRepositoryShare** bloku.
**ResourceRepositoryShare** definuje následující vlastnosti.

|Vlastnost|Typ|Popis|
|---|---|---|
|Přihlašovací údaje|MSFT_Credential|Přihlašovací údaje pro ověření do sdílené složky SMB. Příklad předávání přihlašovacích údajů, naleznete v tématu [nastavení serveru vyžádané replikace SMB pro DSC](../pull-server/pullServerSMB.md)|
|SourcePath|řetězec|Cesta sdílenou složku SMB.|

## <a name="report-server-blocks"></a>Bloků serveru sestav

Chcete-li definovat serveru sestav, vytvoříte **ReportServerWeb** bloku.
Role serveru sestav není kompatibilní s službu přijetí změn na základě protokolu SMB.
**ReportServerWeb** definuje následující vlastnosti.

|Vlastnost|Typ|Popis|
|---|---|---|
|AllowUnsecureConnection|BOOL|Nastavte na **$TRUE** umožňující připojení k serveru bez ověřování z uzlu. Nastavte na **$FALSE** tak, aby vyžadovala ověřování.|
|CertificateID|řetězec|Kryptografický otisk certifikátu používá k ověření serveru.|
|RegistrationKey|řetězec|Identifikátor GUID, který identifikuje uzel, který má službu přijetí změn.|
|URL serveru|řetězec|Adresa URL konfiguračního serveru.|

Ukázkový skript pro zjednodušení konfigurace hodnotu ReportServerWeb místních uzlech je k dispozici – viz [metaconfigurations generování DSC](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-onboarding#generating-dsc-metaconfigurations)

## <a name="partial-configurations"></a>Částečné konfigurace

Chcete-li definovat částečné konfigurace, vytvoříte **PartialConfiguration** bloku.
Další informace o částečné konfigurace najdete v tématu [konfigurací DSC částečné](../pull-server/partialConfigs.md).
**PartialConfiguration** definuje následující vlastnosti.

|Vlastnost|Typ|Popis|
|---|---|---|
|ConfigurationSource|řetězec]|Pole názvy konfigurace serverů definovanou dříve ve **ConfigurationRepositoryWeb** a **ConfigurationRepositoryShare** bloky, ve kterém se použije částečné konfigurace.|
|DependsOn|Řetězec{}|Seznam názvů ostatní konfigurace, kterou je potřeba provést před použitím této částečné konfigurace.|
|Popis|řetězec|Text, který slouží k popisu částečné konfigurace.|
|ExclusiveResources|řetězec]|Pole výhradně pro tuto dílčí konfiguraci prostředků.|
|RefreshMode|řetězec|Určuje, jak LCM získá toto částečné konfigurace. Možné hodnoty jsou __"Zakázáno"__, __"Push"__, a __"Pull"__. <ul><li>__Zakázané__: Tato částečná konfigurace je zakázaná.</li><li> __Push__: Částečné konfigurace se vloží do uzlu voláním [Publish-DscConfiguration](/powershell/module/PSDesiredStateConfiguration/Publish-DscConfiguration) rutiny. Poté, co všechny částečné konfigurace uzlu jsou vloženy nebo získaných ze služby, konfigurace lze spustit voláním `Start-DscConfiguration –UseExisting`. Tato hodnota je výchozí.</li><li>__Stáhněte si:__ Uzel je nakonfigurován na pravidelně kontrolovat částečné konfiguraci ze služby o přijetí změn. Pokud je tato vlastnost nastavená na __o přijetí změn__, je nutné zadat službu přijetí změn v __ConfigurationSource__ vlastnost. Další informace o službě Azure Automation o přijetí změn najdete v tématu [Přehled služby Azure Automation DSC](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-overview).</li></ul>|
|ResourceModuleSource|řetězec]|Pole názvy prostředků serverů, z nichž lze stáhnout požadované prostředky pro tuto konfiguraci částečné. Tyto názvy musí odkazovat na dříve definované v koncových bodů služby **ResourceRepositoryWeb** a **ResourceRepositoryShare** bloky.|

__Poznámka:__ částečné konfigurace jsou podporované s Azure Automation DSC, ale je mohly vyžádat pouze jednu konfiguraci z jednotlivých účtů automation podle počtu uzlů.

## <a name="see-also"></a>Viz také

### <a name="concepts"></a>Koncepty
[Přehled Desired State Configuration](../overview/overview.md)

[Začínáme s Azure Automation DSC](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-getting-started)

### <a name="other-resources"></a>Další prostředky

[Set-DscLocalConfigurationManager](/powershell/module/PSDesiredStateConfiguration/Set-DscLocalConfigurationManager)

[Nastavení načítacího klienta s názvy konfigurace](../pull-server/pullClientConfigNames.md)
