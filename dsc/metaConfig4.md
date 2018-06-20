---
ms.date: 10/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Konfigurace správce místní konfigurace v předchozích verzích prostředí Windows PowerShell
ms.openlocfilehash: 05e315539e51e31b5a496e8c595ac3695d9a0c97
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
ms.locfileid: "34189376"
---
# <a name="configuring-the-local-configuration-manager-in-previous-versions-of-windows-powershell"></a>Konfigurace správce místní konfigurace v předchozích verzích prostředí Windows PowerShell

>Platí pro: Prostředí Windows PowerShell 4.0

**Informace vztahující se k prostředí Windows PowerShell 5.0 a novější najdete v tématu [konfigurace správce místní konfigurace](metaConfig.md).**

Správce místní konfigurace je modul požadovaného stavu aplikace Windows PowerShell (DSC).
Běží na všechny cílové uzly, a je zodpovědná za volání konfigurace prostředky, které jsou součástí konfigurační skript DSC.
Toto téma obsahuje seznam vlastností správce místní konfigurace a popisuje, jak je možné upravit správce místní konfigurace nastavení na cílový uzel.

## <a name="local-configuration-manager-properties"></a>Vlastnosti správce místní konfigurace

Následuje seznam vlastností správce místní konfigurace, které můžete nastavit nebo načíst.

- **AllowModuleOverwrite**: Určuje, jestli nové konfigurace stažené ze služby konfigurace se smí přepsat staré na cílovém uzlu. Možné hodnoty jsou True a False.
- **CertificateID**: kryptografický otisk certifikátu k zabezpečení přihlašovacích údajů předán v konfiguraci. Další informace najdete v části [chcete zabezpečit přihlašovací údaje v části Konfigurace požadovaného stavu aplikace Windows PowerShell?](http://blogs.msdn.com/b/powershell/archive/2014/01/31/want-to-secure-credentials-in-windows-powershell-desired-state-configuration.aspx).
- **ConfigurationID**: označuje identifikátor GUID, který se použije k získání příslušného konfiguračního souboru ze služby vyžádání obsahu. Identifikátor GUID zajistí, aby měli přístup správný konfigurační soubor.
- **ConfigurationMode**: Určuje, jak správce místní konfigurace ve skutečnosti použije konfiguraci pro cílové uzly. Může trvat následující hodnoty:
  - **ApplyOnly**: DSC s tuto možnost, bude konfigurace a další nic neprovádí, pokud je zjištěn novou konfiguraci, ať již odesílání novou konfiguraci přímo na cílovém uzlu, nebo pokud se připojujete k vyžádání služby a DSC Při kontrole se službou vyžádání obsahu, zjistí novou konfiguraci. Pokud cílový uzel konfigurace drifts, nebyla provedena žádná akce.
  - **ApplyAndMonitor**: pomocí této možnosti (což je výchozí nastavení), DSC platí všechny nové konfigurace, které jste se odešle přímo na cílový uzel nebo zjištěná na vyžádání služby. Po tomto datu Pokud konfigurace cílový uzel drifts z konfiguračního souboru, sestavy DSC nesoulad mezi databází v protokolech. Další informace o protokolování DSC najdete v tématu [pomocí protokoly událostí a diagnostikovat chyby v Konfigurace požadovaného stavu](http://blogs.msdn.com/b/powershell/archive/2014/01/03/using-event-logs-to-diagnose-errors-in-desired-state-configuration.aspx).
  - **ApplyAndAutoCorrect**: pomocí této možnosti DSC platí nové konfigurace, které jste se odešle přímo na cílový uzel nebo zjištěná na vyžádání služby. Po tomto datu Pokud konfigurace cílový uzel drifts z konfiguračního souboru, DSC sestavy nesoulad mezi databází v protokolech a poté se pokusí úpravou konfigurace cílového uzlu uvést v souladu s konfiguračního souboru.
- **ConfigurationModeFrequencyMins**: představuje frekvenci (v minutách), s jakou se aplikace DSC běžící na pozadí pokouší implementovat na cílový uzel aktuální konfiguraci. Výchozí hodnota je 15. Tuto hodnotu můžete nastavit ve spojení s RefreshMode. Pokud RefreshMode je nastaven na VYŽÁDÁNÍ, cílový uzel kontaktuje službu konfigurace v intervalu nastaven RefreshFrequencyMins a stáhne aktuální konfiguraci. Bez ohledu na hodnotu RefreshMode v intervalu určeném podle ConfigurationModeFrequencyMins, použije modul konzistence s nejnovější konfigurací, který byl stažen do cílový uzel. RefreshFrequencyMins musí být nastavena na celé číslo násobkem ConfigurationModeFrequencyMins.
- **Přihlašovací údaje**: označuje přihlašovací údaje (stejně jako u Get-Credential) požadovaná pro přístup k vzdálené prostředky, například ke kontaktování služby konfigurace.
- **DownloadManagerCustomData**: představuje pole, které obsahuje vlastní data specifická pro správce stahování.
- **DownloadManagerName**: Určuje název konfigurace a správce stahování modulu.
- **RebootNodeIfNeeded**: změny konfigurace na cílový uzel může požadovat, aby změny projeví až po restartování. S hodnotou **True**, tato vlastnost bude uzel se restartuje hned, jak byla konfigurace úplně platí bez další upozornění. Pokud **False** (výchozí hodnota), se dokončí konfigurace, ale uzlu je ručně restartovat, aby změny vstoupily v platnost.
- **RefreshFrequencyMins**: použít při nastavování služby vyžádání obsahu. Představuje frekvenci (v minutách), s jakou správce místní konfigurace kontaktuje službu vyžádání obsahu stáhnout aktuální konfiguraci. Tuto hodnotu můžete nastavit ve spojení s ConfigurationModeFrequencyMins. Pokud RefreshMode je nastaven na VYŽÁDÁNÍ, cílový uzel kontaktuje službu vyžádání obsahu v intervalu nastaven RefreshFrequencyMins a stáhne aktuální konfiguraci. V intervalu ve ConfigurationModeFrequencyMins nastavení použije modul konzistence pak nejnovější konfigurace, který byl stažen do cílový uzel. Pokud RefreshFrequencyMins není nastavený na celé číslo násobkem ConfigurationModeFrequencyMins, systém se zaokrouhlí nahoru. Výchozí hodnota je 30.
- **RefreshMode**: možné hodnoty jsou **Push** (výchozí) a **pro vyžádání obsahu**. V konfiguraci "push" musíte umístit soubor konfigurace na každý cílový uzel pomocí libovolného klientského počítače. V režimu "vyžádání" musíte nastavit službu přijetí změn pro správce místní konfigurace a obraťte se na přístup ke konfiguračním souborům.

### <a name="example-of-updating-local-configuration-manager-settings"></a>Příklad aktualizuje se nastavení správce místní konfigurace

Správce místní konfigurace nastavení cílový uzel můžete aktualizovat tak, že začleníte **LocalConfigurationManager** blokovat uvnitř bloku uzlu v konfigurační skript, jak je znázorněno v následujícím příkladu.

```powershell
Configuration ExampleConfig
{
    Node “Server001”
    {
        LocalConfigurationManager
        {
            ConfigurationID = "646e48cb-3082-4a12-9fd9-f71b9a562d4e"
            ConfigurationModeFrequencyMins = 45
            ConfigurationMode = "ApplyAndAutocorrect"
            RefreshMode = "Pull"
            RefreshFrequencyMins = 90
            DownloadManagerName = "WebDownloadManager"
            DownloadManagerCustomData = (@{ServerUrl="https://$PullService/psdscpullserver.svc"})
            CertificateID = "71AA68562316FE3F73536F1096B85D66289ED60E"
            Credential = $cred
            RebootNodeIfNeeded = $true
            AllowModuleOverwrite = $false
        }
# One or more resource blocks can be added here
    }
}

# The following line invokes the configuration and creates a file called Server001.meta.mof at the specified path
ExampleConfig -OutputPath "c:\users\public\dsc"
```

Spouštění skriptu v předchozím příkladu generuje soubor MOF, který určuje a ukládá požadovaná nastavení.
Chcete-li použít nastavení, můžete použít **Set-DscLocalConfigurationManager** rutiny, jak je znázorněno v následujícím příkladu.

```powershell
Set-DscLocalConfigurationManager -Path "c:\users\public\dsc"
```

> **Poznámka:**: pro **cesta** parametr, musíte zadat stejnou cestu, která jste zadali pro **OutputPath** parametr při vyvolání konfigurace v předchozím příkladu.

Pokud chcete zobrazit aktuální nastavení správce místní konfigurace, můžete použít **Get-DscLocalConfigurationManager** rutiny.
Pokud vyvolání Tato rutina bez parametrů, ve výchozím nastavení se získají správce místní konfigurace nastavení pro uzel, na kterém jste spustili.
Pokud chcete zadat jiný uzel, použijte **CimSession** parametr pomocí této rutiny.