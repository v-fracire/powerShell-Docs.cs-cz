---
ms.date: 12/12/2018
keywords: DSC, powershell, konfigurace, instalační program
title: Konfigurace Local Configuration Manageru v předchozích verzích Windows Powershellu
ms.openlocfilehash: 31ba2ecdaa5a2ff7fcfddb1791c4d00343f4b5d5
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403737"
---
# <a name="configuring-the-local-configuration-manager-in-previous-versions-of-windows-powershell"></a>Konfigurace Local Configuration Manageru v předchozích verzích Windows Powershellu

>Platí pro: Windows PowerShell 4.0

**Informace týkající se k Windows Powershellu 5.0 a novějším, naleznete v tématu [konfigurace Local Configuration Manageru](metaConfig.md).**

Local Configuration Manageru je modul Windows PowerShell Desired State Configuration (DSC).
Běží na všechny cílové uzly a je zodpovědný za volání konfigurační zdroje, které jsou součástí skript konfigurace DSC.
V tomto tématu jsou uvedeny vlastnosti místní Configuration Manageru a popisuje, jak můžete upravit nastavení Local Configuration Manageru na cílový uzel.

## <a name="local-configuration-manager-properties"></a>Vlastnosti místní Configuration Manageru

Následuje seznam vlastnosti Local Configuration Manageru, které můžete nastavit nebo načíst.

- **AllowModuleOverwrite**: Určuje, jestli nové konfigurace stažené ze služby konfigurace můžou přepsat staré na cílovém uzlu. Možné hodnoty jsou True a False.
- **CertificateID**: Kryptografický otisk certifikát používaný k zabezpečení přihlašovacích údajů předaných v konfiguraci. Další informace najdete v části [chcete zabezpečené přihlašovací údaje ve Windows Powershellu Desired State Configuration?](https://blogs.msdn.microsoft.com/powershell/2014/01/31/want-to-secure-credentials-in-windows-powershell-desired-state-configuration/).
- **ConfigurationID**: Určuje identifikátor GUID, který se používá k získání příslušného konfiguračního souboru ze služby o přijetí změn. Identifikátor GUID se zajistí, že je získat přístup k souboru správná konfigurace.
- **ConfigurationMode**: Určuje, jak Local Configuration Manageru ve skutečnosti aplikuje konfiguraci na cílové uzly. To můžete provést následující hodnoty:
  - **ApplyOnly**: Pomocí této možnosti aplikuje konfiguraci DSC a neprovede žádnou další akci, pokud se detekuje nová konfigurace, buď ve můžete odesílat na novou konfiguraci přímo k cílovému uzlu nebo pokud se připojujete k službu přijetí změn a DSC zjišťuje nové konfigurace při zkontroluje službu přijetí změn. Pokud cílový uzel konfigurace drifts, nedojde k žádné akci.
  - **ApplyAndMonitor**: Pomocí této možnosti (což je výchozí hodnota) DSC platí pro všechny nové konfigurace odesílaných přímo na cílový uzel nebo zjištěná na službu přijetí změn. Po tomto datu Pokud konfigurace cílový uzel drifts z konfiguračního souboru, sestavy DSC nesrovnalosti v protokolech. Další informace o protokolování DSC najdete v tématu [pomocí protokoly událostí a diagnostice chyby v Desired State Configuration](http://blogs.msdn.com/b/powershell/archive/2014/01/03/using-event-logs-to-diagnose-errors-in-desired-state-configuration.aspx).
  - **ApplyAndAutoCorrect**: Pomocí této možnosti DSC platí pro všechny nové konfigurace odesílaných přímo na cílový uzel nebo zjištěná na službu přijetí změn. Po tomto datu Pokud konfigurace cílový uzel drifts z konfiguračního souboru, DSC sestavy nesrovnalosti v protokolech a poté se pokusí upravit konfigurace cílového uzlu zpřístupnit v souladu s konfiguračním souboru.
- **ConfigurationModeFrequencyMins**: Představuje frekvenci (v minutách), kdy použití DSC na pozadí pokouší implementovat aktuální konfiguraci na cílový uzel. Výchozí hodnota je 15. Tuto hodnotu lze nastavit ve spojení s RefreshMode. Pokud RefreshMode nastaven na VYŽÁDÁNÍ, cílový uzel kontaktuje službu konfigurace v intervalu nastavil RefreshFrequencyMins a stáhne aktuální konfiguraci. Bez ohledu na hodnotu RefreshMode v intervalu nastavil ConfigurationModeFrequencyMins, použije modul konzistence nejnovější konfigurace, který jste stáhli na cílový uzel. RefreshFrequencyMins musí být nastavená na celé násobky ConfigurationModeFrequencyMins.
- **Přihlašovací údaje**: Určuje přihlašovací údaje (stejně jako u Get-Credential) požadovaná pro přístup k vzdálené prostředky, jako například kontaktovat službu configuration.
- **DownloadManagerCustomData**: Představuje pole, která obsahuje vlastní data specifická pro správce stahování.
- **DownloadManagerName**: Určuje název, konfigurace a správce stahování modulů.
- **RebootNodeIfNeeded**: Některé změny konfigurace na cílový uzel může požadovat, aby změny použít až po restartování. S hodnotou **True**, tato vlastnost se uzel restartuje, ihned poté, co byla konfigurace platí zcela bez dalšího upozornění. Pokud **False** (výchozí hodnota), se dokončí konfigurace, ale uzel je ručně restartovat, aby změny projevily.
- **RefreshFrequencyMins**: Používá, když jste vytvořili službu přijetí změn. Představuje frekvenci (v minutách), jakou správce místní konfigurace kontaktuje načítací služba stáhněte aktuální konfiguraci. Tuto hodnotu lze nastavit ve spojení s ConfigurationModeFrequencyMins. Pokud RefreshMode nastaven na VYŽÁDÁNÍ, cílový uzel kontaktuje načítací služba v intervalu nastavil RefreshFrequencyMins a stáhne aktuální konfiguraci. Modul konzistence v intervalu nastavil ConfigurationModeFrequencyMins, poté použije nejnovější konfigurace, který jste stáhli na cílový uzel. Pokud RefreshFrequencyMins není nastavená na celé násobky ConfigurationModeFrequencyMins, systém bude zaokrouhlení nahoru. Výchozí hodnota je 30.
- **RefreshMode**: Možné hodnoty jsou **Push** (výchozí) a **o přijetí změn**. V konfiguraci "push" je nutné umístit konfigurační soubor na každém cílovém uzlu pomocí libovolného klientského počítače. V režimu "pull" musíte nastavit službu přijetí změn pro Local Configuration Manageru kontaktovat a přístup ke konfiguračním souborům.

### <a name="example-of-updating-local-configuration-manager-settings"></a>Příklad aktualizuje se nastavení Local Configuration Manageru

Nastavení cílovému uzlu Local Configuration Manageru můžete aktualizovat zahrnutím **LocalConfigurationManager** blokovat uvnitř bloku uzlu v konfigurační skript, jak je znázorněno v následujícím příkladu.

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

Spuštění skriptu v předchozím příkladu generuje soubor MOF, který určuje a ukládá požadovaná nastavení.
Chcete-li použít nastavení, můžete použít **Set-DscLocalConfigurationManager** rutiny, jak je znázorněno v následujícím příkladu.

```powershell
Set-DscLocalConfigurationManager -Path "c:\users\public\dsc"
```

> **Poznámka:**: Pro **cesta** parametr, musíte zadat stejnou cestu, která jste zadali pro **OutputPath** parametr při vyvolání konfigurace v předchozím příkladu.

Pokud chcete zobrazit aktuální nastavení Local Configuration Manageru, můžete použít **Get-DscLocalConfigurationManager** rutiny.
Pokud vyvoláte této rutiny bez parametrů, ve výchozím nastavení ho se nastavení Local Configuration Manageru pro uzel, na kterém jste spustili.
Chcete-li zadat jiný uzel, použijte **CimSession** parametr s touto rutinou.
