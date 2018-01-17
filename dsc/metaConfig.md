---
ms.date: 2017-10-11
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Konfigurace správce místní konfigurace"
ms.openlocfilehash: 947bc17347204f6f15a24f83b449582afe65a4ee
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="configuring-the-local-configuration-manager"></a>Konfigurace správce místní konfigurace

> Platí pro: Prostředí Windows PowerShell 5.0

Místní Configuration Manager (LCM) je modul z požadovaného konfigurace stavu (DSC).
LCM běží na každý cílový uzel a zodpovídá za analýzy a přijetí konfigurace, které se odesílají do uzlu.
Je také zodpovědná za několik dalších aspektů DSC, včetně následujících.

- Určení režimu aktualizace (push nebo pull).
- Určení, jak často uzlu vrátí a představuje konfigurace.
- Přidružení uzlu službou vyžádání obsahu.
- Zadání částečné konfigurace.

Použít speciální typ konfigurace konfigurace LCM zadat každou z těchto chování.
Následující části popisují postup konfigurace LCM.

> **Poznámka:**: Toto téma se týká LCM byla zavedená v prostředí Windows PowerShell 5.0.
Informace o konfiguraci LCM v prostředí Windows PowerShell 4.0 najdete v tématu [Windows PowerShell 4.0 požadovaného stavu konfigurace správce místní konfigurace](metaconfig4.md).

## <a name="writing-and-enacting-an-lcm-configuration"></a>Psaní a přijetí konfigurace aplikace LCM

Ke konfiguraci LCM, vytvořte a spusťte typu speciální konfigurace, která se použije LCM nastavení.
Pokud chcete zadat informace o nastavení LCM, použijte atribut DscLocalConfigurationManager.
Na obrázku je jednoduchý konfigurace, která nastaví LCM na režim push.

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

Proces aplikování nastavení na LCM je podobná použití konfigurace DSC.
Vytvoření konfigurace aplikace LCM, zkompilovat do souboru MOF a použijte ho k uzlu.
Na rozdíl od konfigurace DSC, není uplatní konfigurace aplikace LCM voláním [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) rutiny.
Místo toho můžete volat [Set-DscLocalConfigurationManager](https://technet.microsoft.com/en-us/library/dn521621.aspx), zadávání cestu ke konfiguraci LCM MOF jako parametr.
Po můžete uplatní LCM konfigurace, můžete zobrazit vlastnosti LCM voláním [Get-DscLocalConfigurationManager](https://technet.microsoft.com/en-us/library/dn407378.aspx) rutiny.

Konfigurace aplikace LCM může obsahovat bloky pouze pro omezenou sadu prostředků.
V předchozím příkladu pouze prostředek s názvem je **nastavení**.
Dostupné prostředky jsou:

* **ConfigurationRepositoryWeb**: Určuje služby pro vyžádání obsahu HTTP pro konfigurace.
* **ConfigurationRepositoryShare**: Určuje složky protokolu SMB pro konfigurace.
* **ResourceRepositoryWeb**: Určuje služby pro vyžádání obsahu HTTP pro moduly.
* **ResourceRepositoryShare**: Určuje složky protokolu SMB pro moduly.
* **ReportServerWeb**: Určuje služby HTTP přijetí změn, ke které se odesílají sestavy.
* **PartialConfiguration**: poskytuje data povolit částečné konfigurace.

## <a name="basic-settings"></a>Základní nastavení

Než zadáte koncových bodů nebo cesty k vyžádání služby a částečné konfigurace, všechny vlastnosti LCM konfigurované v **nastavení** bloku.
Následující vlastnosti jsou k dispozici v **nastavení** bloku.

|  Vlastnost  |  Typ  |  Popis   |
|----------- |------- |--------------- |
| ActionAfterReboot| řetězec| Určuje, co se stane po restartu během použití konfigurace. Možné hodnoty jsou __"ContinueConfiguration"__ a __"StopConfiguration"__. <ul><li> __ContinueConfiguration__: pokračovat v použití aktuální konfiguraci po restartování počítače. Toto je výchozí hodnota</li><li>__StopConfiguration__: Zastavit aktuální konfiguraci po restartování počítače.</li></ul>|
| AllowModuleOverwrite| BOOL| __$TRUE__ Pokud nové konfigurace stažené z službu vyžádání obsahu se smí přepsat staré na cílovém uzlu. Jinak hodnota $FALSE.|
| CertificateID| řetězec| Kryptografický otisk certifikátu k zabezpečení přihlašovacích údajů předaných v konfiguraci. Další informace najdete v části [chcete zabezpečit přihlašovací údaje v části Konfigurace požadovaného stavu aplikace Windows PowerShell](http://blogs.msdn.com/b/powershell/archive/2014/01/31/want-to-secure-credentials-in-windows-powershell-desired-state-configuration.aspx)?. <br> __Poznámka:__ to probíhá automaticky při použití služby Azure Automation DSC vyžádání obsahu.|
| ConfigurationDownloadManagers| CimInstance[]| Zastaralé. Použití __ConfigurationRepositoryWeb__ a __ConfigurationRepositoryShare__ bloky k definování konfigurace vyžadování koncové body služby.|
| ConfigurationID| řetězec| Pro zpětnou kompatibilitu s starší vyžádání služby verze. Identifikátor GUID, který identifikuje konfiguračního souboru získat ze služby vyžádání obsahu. Uzel načte konfigurace ve službě vyžádání obsahu, pokud se název konfigurace MOF jmenuje ConfigurationID.mof.<br> __Poznámka:__ Pokud nastavíte tuto vlastnost, registraci uzlu službou vyžádání obsahu pomocí __RegistrationKey__ nefunguje. Další informace najdete v tématu [nastavení klienta vyžádání obsahu s názvy konfigurace](pullClientConfigNames.md).|
| ConfigurationMode| řetězec | Určuje, jak LCM ve skutečnosti použije konfiguraci pro cílové uzly. Možné hodnoty jsou __"ApplyOnly"__,__"ApplyandMonitior"__, a __"ApplyandAutoCorrect"__. <ul><li>__ApplyOnly__: DSC aplikuje konfiguraci a další nic neprovádí, pokud je novou konfiguraci instaluje na cílovém uzlu, nebo když je vyžádat novou konfiguraci ze služby. Po počáteční aplikaci novou konfiguraci DSC nekontroluje odlišily z dříve nakonfigurované stavu. Všimněte si, že DSC se pokusí použít konfiguraci, dokud nebude úspěšná, až poté __ApplyOnly__ projeví. </li><li> __ApplyAndMonitor__: Toto je výchozí hodnota. Všechny nové konfigurace se vztahuje LCM. Po počáteční aplikaci novou konfiguraci Pokud cílový uzel drifts z požadovaný stav sestavy DSC nesoulad mezi databází v protokolech. Všimněte si, že DSC se pokusí použít konfiguraci, dokud nebude úspěšná, až poté __ApplyAndMonitor__ projeví.</li><li>__ApplyAndAutoCorrect__: platí všechny nové konfigurace DSC. Po počáteční aplikaci novou konfiguraci Pokud cílový uzel drifts z požadovaný stav DSC sestavy nesoulad mezi databází v protokolech a poté znovu použije aktuální konfiguraci.</li></ul>|
| ConfigurationModeFrequencyMins| UInt32| Jak často v minutách, aktuální konfiguraci je zkontrolovat a použít. Tato vlastnost se ignoruje, pokud je vlastnost ConfigurationMode nastavena na ApplyOnly. Výchozí hodnota je 15.|
| Režim DebugMode| řetězec| Možné hodnoty jsou __žádné__, __ForceModuleImport__, a __všechny__. <ul><li>Nastavte na __žádné__ využívat prostředky uložené v mezipaměti. Toto je výchozí a je třeba používat v produkčních scénářích.</li><li>Nastavení na __ForceModuleImport__, způsobí, že LCM načtením všech modulů prostředků DSC, i když byly dříve načteny a uloží do mezipaměti. To ovlivní výkon DSC operací, jako je každý modul znovu za použití. Obvykle byste tuto hodnotu použijte při ladění prostředku</li><li>V této verzi __všechny__ je stejný jako __ForceModuleImport__</li></ul> |
| RebootNodeIfNeeded| BOOL| Tuto možnost nastavíte na __$true__ k automatickému restartování uzlu po konfiguraci, která vyžaduje restartování počítače se použije. Jinak je nutné ručně restartovat uzel pro všechny konfigurace, kterého se vyžaduje. Výchozí hodnota je __$false__. Pokud chcete používat toto nastavení při restartování podmínku je vydaných něco jiného než DSC (jako je například Instalační služba systému Windows), kombinací toto nastavení se [xPendingReboot](https://github.com/powershell/xpendingreboot) modulu.|
| RefreshMode| řetězec| Určuje, jak LCM získá konfigurace. Možné hodnoty jsou __"Zakázat"__, __"Push"__, a __"Pro vyžádání obsahu"__. <ul><li>__Zakázané__: Konfigurace DSC nebudou k dispozici pro tento uzel.</li><li> __Push__: Konfigurace zahájili volání [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) rutiny. Konfigurace se použije okamžitě na uzlu. Tato hodnota je výchozí.</li><li>__Vyžádání obsahu:__ uzlu nastaven tak, aby pravidelně kontrolovat konfigurace ze služby pull nebo cestu protokolu SMB. Pokud je tato vlastnost nastavena na __pro vyžádání obsahu__, je nutné zadat protokolu HTTP (služba) nebo cestu k protokolu SMB (sdílení) __ConfigurationRepositoryWeb__ nebo __ConfigurationRepositoryShare__ bloku.</li></ul>|
| RefreshFrequencyMins| UInt32| Časový interval v minutách, na kterých LCM kontroluje službu vyžádání obsahu a získat aktualizované konfigurace. Tato hodnota je ignorována, pokud LCM není nakonfigurován v režimu vyžádání obsahu. Výchozí hodnota je 30.|
| ReportManagers| CimInstance[]| Zastaralé. Použití __ReportServerWeb__ bloky k definování koncového bodu odeslat data pro vytváření sestav služby vyžádání obsahu.|
| ResourceModuleManagers| CimInstance[]| Zastaralé. Použití __ResourceRepositoryWeb__ a __ResourceRepositoryShare__ bloky zadat vyžadování služby koncových bodů protokolu HTTP nebo protokol SMB cesty, v uvedeném pořadí.|
| PartialConfigurations| CimInstance| Není implementováno. Nepoužívat.|
| StatusRetentionTimeInDays | UInt32| Počet dnů, po který LCM udržuje stav aktuální konfiguraci.|

## <a name="pull-service"></a>Služba pro vyžádání obsahu

Nastavení DSC umožňují uzlu, který bude spravován stahování modulů a konfigurace a publikování data pro generování sestav, do vzdáleného umístění.
Aktuální možnosti pro vyžádání obsahu službu:

- Služba konfigurace stavu žádaný automatizace Azure
- Instance služby z vlastního systémem Windows Server
- Sdílené složce SMB (nepodporuje publikování data pro generování sestav)

Konfigurace LCM podporuje, definování následující typy koncových bodů pro vyžádání obsahu služby:

- **Konfigurační server**: úložiště konfigurace DSC. Definovat konfigurační servery pomocí **ConfigurationRepositoryWeb** (pro webové servery) a **ConfigurationRepositoryShare** (pro servery založeného na protokolu SMB) bloky.
- **Server prostředků**: úložiště prostředků DSC, zabalené jako moduly Powershellu. Definovat servery prostředků pomocí **ResourceRepositoryWeb** (pro webové servery) a **ResourceRepositoryShare** (pro servery založeného na protokolu SMB) bloky.
- **Server sestav**: služba, která odesílá data sestavy DSC. Definovat servery sestav pomocí **ReportServerWeb** bloky. Webové služby musí být serveru sestav.

**Doporučené řešení**, a s nejvíce funkcemi, které jsou k dispozici, není [Azure Automation DSC](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-getting-started).

Uzly na místě v datových centrech privátní nebo veřejné cloudy, například Azure a AWS můžete spravovat službu Azure.
U privátních prostředí, kde nelze servery připojit přímo k Internetu, zvažte omezení odchozí provoz jenom publikované Azure rozsah IP adres (viz [rozsahy IP Datacentra Azure](https://www.microsoft.com/en-us/download/details.aspx?id=41653)).

Funkce služby online, které nejsou momentálně k dispozici ve službě vyžádání v systému Windows Server:
- Všechna data se šifrují během přenosu a v klidovém stavu
- Klientské certifikáty se vytváří a spravují automaticky
- Ukládat tajné klíče pro centrální správu [hesla nebo přihlašovací údaje](https://docs.microsoft.com/en-us/azure/automation/automation-credentials), nebo [proměnné](https://docs.microsoft.com/en-us/azure/automation/automation-variables) například názvy serverů nebo připojovací řetězce
- Centrálně spravovat uzlu [LCM konfigurace](metaConfig.md#basic-settings)
- Centrálně přiřadit konfigurace pro klienta uzly
- Konfigurace verze se změní na "lesknice skupiny" pro testování dříve, než dorazila produkční
- Grafické vytváření sestav
  - Podrobná sestava stavu na úrovni prostředků DSC členitosti
  - Podrobné chybové zprávy z klientských počítačů pro řešení potíží
- [Integrace s Azure Log Analytics](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-diagnostics) pro výstrahy, automatizované úlohy, aplikace pro Android nebo iOS pro vytváření sestav a výstrahy

Můžete taky informace o nastavení a použití služby pro vyžádání obsahu HTTP v systému Windows Server najdete v tématu [nastavení server DSC za](pullServer.md).
Mějte na paměti, že je omezená implementace s pouze základní funkce ukládání konfigurace nebo moduly a zaznamenávání dat sestav v do místní databáze.

## <a name="configuration-server-blocks"></a>Konfigurace serveru bloky

Chcete-li definovat webové konfigurační server, musíte vytvořit **ConfigurationRepositoryWeb** bloku.
A **ConfigurationRepositoryWeb** definuje následující vlastnosti.

|Vlastnost|Typ|Popis|
|---|---|---|
|AllowUnsecureConnection|BOOL|Nastavte na **$TRUE** umožňující připojení z uzlu k serveru bez ověřování. Nastavte na **$FALSE** tak, aby vyžadovala ověřování.|
|CertificateID|řetězec|Kryptografický otisk certifikátu používá k ověření serveru.|
|ConfigurationNames|řetězec]|Pole názvy konfigurace, které se vyžádat cílový uzel. Ty se používají pouze v případě, že uzel je registrovaný ve službe vyžádání obsahu pomocí **RegistrationKey**. Další informace najdete v tématu [nastavení klienta vyžádání obsahu s názvy konfigurace](pullClientConfigNames.md).|
|RegistrationKey|řetězec|Identifikátor GUID, který registruje uzlu pomocí služby vyžádání obsahu. Další informace najdete v tématu [nastavení klienta vyžádání obsahu s názvy konfigurace](pullClientConfigNames.md).|
|ServerURL|řetězec|Adresa URL služby konfigurace.|

V tématu ukázkového skriptu ke zjednodušení konfigurace hodnota ConfigurationRepositoryWeb pro místní uzlů je k dispozici – [metaconfigurations generování DSC](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-onboarding#generating-dsc-metaconfigurations)

Chcete-li definovat serveru konfigurace založené na protokolu SMB, musíte vytvořit **ConfigurationRepositoryShare** bloku.
A **ConfigurationRepositoryShare** definuje následující vlastnosti.

|Vlastnost|Typ|Popis|
|---|---|---|
|přihlašovací údaje|MSFT_Credential|Přihlašovací údaje použité k ověření ke sdílené složce SMB.|
|SourcePath|řetězec|Cesta sdílené složky SMB.|

## <a name="resource-server-blocks"></a>Blokuje server prostředků

Chcete-li definovat webových prostředků serveru, musíte vytvořit **ResourceRepositoryWeb** bloku.
A **ResourceRepositoryWeb** definuje následující vlastnosti.

|Vlastnost|Typ|Popis|
|---|---|---|
|AllowUnsecureConnection|BOOL|Nastavte na **$TRUE** umožňující připojení z uzlu k serveru bez ověřování. Nastavte na **$FALSE** tak, aby vyžadovala ověřování.|
|CertificateID|řetězec|Kryptografický otisk certifikátu používá k ověření serveru.|
|RegistrationKey|řetězec|Identifikátor GUID, který identifikuje uzlu ke službě vyžádání obsahu.|
|ServerURL|řetězec|Adresa URL konfigurační server.|

V tématu ukázkového skriptu ke zjednodušení konfigurace hodnota ResourceRepositoryWeb pro místní uzlů je k dispozici – [metaconfigurations generování DSC](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-onboarding#generating-dsc-metaconfigurations)

Chcete-li definovat serveru založeného na protokolu SMB prostředků, musíte vytvořit **ResourceRepositoryShare** bloku.
**ResourceRepositoryShare** definuje následující vlastnosti.

|Vlastnost|Typ|Popis|
|---|---|---|
|přihlašovací údaje|MSFT_Credential|Přihlašovací údaje použité k ověření ke sdílené složce SMB. Příklad předávání pověření, naleznete v části [nastavení vyžadování serveru DSC SMB](pullServerSMB.md)|
|SourcePath|řetězec|Cesta sdílené složky SMB.|

## <a name="report-server-blocks"></a>Bloky serveru sestav

Chcete-li definovat serveru sestav, musíte vytvořit **ReportServerWeb** bloku.
Role serveru sestav není kompatibilní se službou protokolu SMB na základě vyžádání obsahu.
**ReportServerWeb** definuje následující vlastnosti.

|Vlastnost|Typ|Popis|
|---|---|---|
|AllowUnsecureConnection|BOOL|Nastavte na **$TRUE** umožňující připojení z uzlu k serveru bez ověřování. Nastavte na **$FALSE** tak, aby vyžadovala ověřování.|
|CertificateID|řetězec|Kryptografický otisk certifikátu používá k ověření serveru.|
|RegistrationKey|řetězec|Identifikátor GUID, který identifikuje uzlu ke službě vyžádání obsahu.|
|ServerURL|řetězec|Adresa URL konfigurační server.|

V tématu ukázkového skriptu ke zjednodušení konfigurace hodnota ReportServerWeb pro místní uzlů je k dispozici – [metaconfigurations generování DSC](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-onboarding#generating-dsc-metaconfigurations)

## <a name="partial-configurations"></a>Částečné konfigurace

Chcete-li definovat částečné konfigurace, musíte vytvořit **PartialConfiguration** bloku.
Další informace o částečné konfiguracích najdete v tématu [konfigurace DSC Partial](partialConfigs.md).
**PartialConfiguration** definuje následující vlastnosti.

|Vlastnost|Typ|Popis|
|---|---|---|
|ConfigurationSource|řetězec]|Pole názvy konfigurace serverů, dříve definované v **ConfigurationRepositoryWeb** a **ConfigurationRepositoryShare** bloky, kde částečné konfigurace načítána z.|
|dependsOn|řetězec {}|Seznam názvů ostatní konfigurace, které je třeba dokončit před použitím této částečné konfigurace.|
|Popis|řetězec|Text sloužící k popisu částečné konfigurace.|
|ExclusiveResources|řetězec]|Pole vylučují toto částečné konfiguraci prostředků.|
|RefreshMode|řetězec|Určuje, jak LCM získá toto částečné konfigurace. Možné hodnoty jsou __"Zakázat"__, __"Push"__, a __"Pro vyžádání obsahu"__. <ul><li>__Zakázané__: Toto částečné nastavení je zakázáno.</li><li> __Push__: částečné konfigurace vložena do uzlu voláním [publikovat DscConfiguration](https://technet.microsoft.com/en-us/library/mt517875.aspx) rutiny. Po všech částečné konfigurací pro uzel se instaluje nebo ze služby, konfigurace lze spustit voláním `Start-DscConfiguration –UseExisting`. Tato hodnota je výchozí.</li><li>__Vyžádání obsahu:__ uzlu nastaven tak, aby pravidelně kontrolovat částečné konfiguraci ze služby vyžádání obsahu. Pokud je tato vlastnost nastavena na __vyžádání__, je nutné zadat vyžadování služby ve službě __ConfigurationSource__ vlastnost. Další informace o přijetí změn služba Azure Automation najdete v tématu [přehled Azure Automation DSC](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-overview).</li></ul>|
|ResourceModuleSource|řetězec]|Pole názvy prostředků serverů, ze kterého mají být staženy požadované prostředky pro tuto konfiguraci částečné. Tyto názvy musí odkazovat na dříve definované v koncové body služby **ResourceRepositoryWeb** a **ResourceRepositoryShare** bloky.|

__Poznámka:__ jsou podporovány částečné konfigurace s Azure Automation DSC, ale je mohly vyžádat pouze jednu konfiguraci z jednotlivých účtů automation na jeden uzel.

## <a name="see-also"></a>Viz také

### <a name="concepts"></a>Koncepty
[Požadovaného stavu konfigurací – přehled](overview.md)

[Začínáme s Azure Automation DSC.](https://docs.microsoft.com/en-us/azure/automation/automation-dsc-getting-started)

### <a name="other-resources"></a>Další prostředky

[Set-DscLocalConfigurationManager](https://technet.microsoft.com/en-us/library/dn521621.aspx)

[Nastavení klienta vyžádání obsahu s názvy konfigurace](pullClientConfigNames.md)
