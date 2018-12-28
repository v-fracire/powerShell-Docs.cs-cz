---
description: Další informace o historii verzí pro rozšíření Desired State Configuration (DSC) v Azure.
ms.date: 06/21/2018
keywords: DSC, powershell, azure, rozšíření
title: Historie verzí rozšíření DSC Azure
ms.openlocfilehash: 2c076e3beccc15e99af2327820916d7a4d28da68
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403819"
---
# <a name="azure-desired-state-configuration-extension-version-history"></a>Historie verzí rozšíření Azure Desired State Configuration

Rozšíření Azure Desired State Configuration (DSC) virtuálního počítače se aktualizuje podle potřeby pro podporu vylepšení a nových funkcí, které zajišťuje Azure, Windows Server a Windows Management Frameworku (WMF), který obsahuje prostředí Windows PowerShell.

Tento článek obsahuje informace o každé verzi rozšíření virtuálního počítače DSC Azure, jakých prostředích ji podporuje a komentáře a poznámky na nové funkce nebo změny.

## <a name="latest-version"></a>Nejnovější verze

### <a name="version-276"></a>Verze 2.76

- **Datum vydání:**
  - 9 květen 2018 (Azure) | 21 červen. května 2018 (Azure China, Azure Government)
- **Podpora operačního systému:**
  - Windows Server 2016
  - Windows Server 2012 R2
  - Windows Server 2012
  - Windows Server 2008 R2 SP1
  - Klient Windows 7/8.1/10
  - Nano Server
- **Podpora WMF:**
  - WMF 5.1
  - WMF 5.0 RTM
  - Aktualizace WMF 4.0
  - WMF 4.0
- **Prostředí:**
  - Azure
  - Azure (Čína)
  - Azure Government
- **Poznámky:** Tato verze používá DSC, jak je zahrnutá ve Windows serveru 2016; pro další operační systémy Windows, nainstaluje [Windows Management Framework 5.1](https://blogs.msdn.microsoft.com/powershell/2016/12/06/wmf-5-1-releasing-january-2017/) (instalaci WMF vyžaduje restart). Pro Nano Server je nainstalována DSC role na virtuálním počítači.
- **Nové funkce:**
  - Zlepšení rozšíření metadat pro substatus a ostatní opravy menších chyb.

## <a name="supported-versions"></a>Podporované verze

> [!WARNING]
> Verze 2.4 prostřednictvím 2,13 použijte WMF 5.0 ve verzi Public Preview v srpnu 2016 vypršela platnost, podpisové certifikáty.  Další informace o tomto problému najdete v tématu [blogový příspěvek](https://blogs.msdn.microsoft.com/powershell/2016/05/24/azure-dsc-extension-versions-2-4-up-to-2-13-will-retire-in-august/).

### <a name="version-275"></a>Verze 2,75

- **Datum vydání:** 5. března 2018
- **Podpora operačního systému:** Klienta Windows Server 2012, Windows Server 2008 R2 SP1, Windows Server 2016, Windows Server 2012 R2, Windows 7/8.1/10 Nano serveru
- **Podpora WMF:** WMF 5.1, WMF 5.0 RTM WMF 4.0 Update, WMF 4.0
- **Prostředí:** Azure
- **Poznámky:** Tato verze používá DSC, jak je zahrnutá ve Windows serveru 2016; pro další operační systémy Windows, nainstaluje [Windows Management Framework 5.1](https://blogs.msdn.microsoft.com/powershell/2016/12/06/wmf-5-1-releasing-january-2017/) (instalaci WMF vyžaduje restart). Pro Nano Server je nainstalována DSC role na virtuálním počítači.
- **Nové funkce:**
  - Po Githubu poslední přejít na protokol TLS 1.2 nejde připojit virtuální počítač, který Azure Automation DSC pomocí šablon rozběhněte zcela Resource Manageru, které jsou k dispozici na webu Azure Marketplace nebo použít rozšíření DSC zobrazíte všechny konfigurace hostovaného na Githubu. Zobrazí se zpráva podobná následující při zavádění rozšíření:

    ```json
    {
        "code": "DeploymentFailed",
        "message": "At least one resource deployment operation failed. Please list deployment operations for details. Please see https://aka.ms/arm-debug for usage details.",
        "details": [{
            "code": "Conflict",
            "message": "{
                \"status\": \"Failed\",
                \"error\": {
                    \"code\": \"ResourceDeploymentFailure\",
                    \"message\": \"The resource operation completed with terminal provisioning state 'Failed'.\",
                    \"details\": [ {
                        \"code\": \"VMExtensionProvisioningError\",
                        \"message\": \"VM has reported a failure when processing extension 'Microsoft.Powershell.DSC'.
                        Error message: \\\"The DSC Extension failed to execute: Error downloading
                        https://github.com/Azure/azure-quickstart-templates/raw/master/dsc-extension-azure-automation-pullserver/UpdateLCMforAAPull.zip
                        after 29 attempts: The request was aborted: Could not create SSL/TLS secure channel..\\nMore information about the failure can
                        be found in the logs located under 'C:\\\\WindowsAzure\\\\Logs\\\\Plugins\\\\Microsoft.Powershell.DSC\\\\2.74.0.0' on the VM.\\\".\"
                    } ]
                }
            }"
        }]
    }
    ```

  - V nové verzi rozšíření je nyní vynucena TLS 1.2. Při nasazení rozšíření, pokud jste už měli verzi AutoUpgradeMinorVersion = true v šabloně Resource Manageru a rozšíření se zobrazí autoupgraded k 2,75. Ruční aktualizace, zadejte `TypeHandlerVersion = 2.75` v šabloně Resource Manageru.

### <a name="version-270---272"></a>Verze 2.70 2.72

- **Datum vydání:** 13. listopadu 2017
- **Podpora operačního systému:** Klienta Windows Server 2012, Windows Server 2008 R2 SP1, Windows Server 2016, Windows Server 2012 R2, Windows 7/8.1/10 Nano serveru
- **Podpora WMF:** WMF 5.1, WMF 5.0 RTM WMF 4.0 Update, WMF 4.0
- **Prostředí:** Azure
- **Poznámky:** Tato verze používá DSC, jak je zahrnutá ve Windows serveru 2016; pro další operační systémy Windows, nainstaluje [Windows Management Framework 5.1](https://blogs.msdn.microsoft.com/powershell/2016/12/06/wmf-5-1-releasing-january-2017/) (instalaci WMF vyžaduje restart). Pro Nano Server je nainstalována DSC role na virtuálním počítači.
- **Nové funkce:**
  - Chyba opravy a vylepšení, která zjednodušuje použití DSC Azure Automation na portálu uživatelského rozhraní, stejně jako šablonu Resource Manageru.  Další informace najdete v tématu [výchozí konfigurační skript](/azure/virtual-machines/extensions/dsc-overview) v dokumentaci k rozšíření DSC.

### <a name="version-226"></a>Verze 2.26

- **Datum vydání:** 9. června 2017
- **Podpora operačního systému:** Klienta Windows Server 2012, Windows Server 2008 R2 SP1, Windows Server 2016, Windows Server 2012 R2, Windows 7/8.1/10 Nano serveru
- **Podpora WMF:** WMF 5.1, WMF 5.0 RTM WMF 4.0 Update, WMF 4.0
- **Prostředí:** Azure
- **Poznámky:** Tato verze používá DSC, jak je zahrnutá ve Windows serveru 2016; pro další operační systémy Windows, nainstaluje [Windows Management Framework 5.1](https://blogs.msdn.microsoft.com/powershell/2016/12/06/wmf-5-1-releasing-january-2017/) (instalaci WMF vyžaduje restart). Pro Nano Server je nainstalována DSC role na virtuálním počítači.
- **Nové funkce:**
  - Vylepšení telemetrie.

### <a name="version-225"></a>Verze 2.25

- **Datum vydání:** 2. června 2017
- **Podpora operačního systému:** Klienta Windows Server 2012, Windows Server 2008 R2 SP1, Windows Server 2016, Windows Server 2012 R2, Windows 7/8.1/10 Nano serveru
- **Podpora WMF:** WMF 5.1, WMF 5.0 RTM WMF 4.0 Update, WMF 4.0
- **Prostředí:** Azure
- **Poznámky:** Tato verze používá DSC, jak je zahrnutá ve Windows serveru 2016; pro další operační systémy Windows, nainstaluje [Windows Management Framework 5.1](https://blogs.msdn.microsoft.com/powershell/2016/12/06/wmf-5-1-releasing-january-2017/) (instalaci WMF vyžaduje restart). Pro Nano Server je nainstalována DSC role na virtuálním počítači.
- **Nové funkce:**
  - Několik oprav chyb a další drobná vylepšení byly přidány.

### <a name="version-224"></a>Verze 2,24

- **Datum vydání:** 13. dubna 2017
- **Podpora operačního systému:** Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1, Nano Server
- **Podpora WMF:** WMF 5.1, WMF 5.0 RTM WMF 4.0 Update, WMF 4.0
- **Prostředí:** Azure
- **Poznámky:** Tato verze používá DSC, jak je zahrnutá ve Windows serveru 2016; pro další operační systémy Windows, nainstaluje [Windows Management Framework 5.1](https://blogs.msdn.microsoft.com/powershell/2016/12/06/wmf-5-1-releasing-january-2017/) (instalaci WMF vyžaduje restart). Pro Nano Server je nainstalována DSC role na virtuálním počítači.
- **Nové funkce:**
  - Uvádí jako metadata rozšíření virtuálního počítače UUID & ID agenta DSC. Byly přidány další drobná vylepšení.

### <a name="version-223"></a>Verze 2.23

- **Datum vydání:** 15. března 2017
- **Podpora operačního systému:** Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1, Nano Server
- **Podpora WMF:** WMF 5.1, WMF 5.0 RTM WMF 4.0 Update, WMF 4.0
- **Prostředí:** Azure
- **Poznámky:** Tato verze používá DSC, jak je zahrnutá ve Windows serveru 2016; pro další operační systémy Windows, nainstaluje [Windows Management Framework 5.1](https://blogs.msdn.microsoft.com/powershell/2016/12/06/wmf-5-1-releasing-january-2017/) (instalaci WMF vyžaduje restart). Pro Nano Server je nainstalována DSC role na virtuálním počítači.
- **Nové funkce:**
  - Řadu oprav chyb a další vylepšení byly přidány.

### <a name="version-222"></a>Verze 2.22

- **Datum vydání:** 8. února 2017
- **Podpora operačního systému:** Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1, Nano Server
- **Podpora WMF:** WMF 5.1, WMF 5.0 RTM WMF 4.0 Update, WMF 4.0
- **Prostředí:** Azure
- **Poznámky:** Tato verze používá DSC, jak je zahrnutá ve Windows serveru 2016; pro další operační systémy Windows, nainstaluje [Windows Management Framework 5.1](https://blogs.msdn.microsoft.com/powershell/2016/12/06/wmf-5-1-releasing-january-2017/) (instalaci WMF vyžaduje restart). Pro Nano Server je nainstalována DSC role na virtuálním počítači.
- **Nové funkce:**
  - Rozšíření DSC teď obsahují podporu pro WMF 5.1.
  - Vedlejší že byly přidány další vylepšení.

### <a name="version-221"></a>Verze 2.21

- **Datum vydání:** 2. prosince 2016
- **Podpora operačního systému:** Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1, Nano Server
- **Podpora WMF:** WMF 5.1 ve verzi Preview, WMF 5.0 RTM, WMF 4.0 Update, WMF 4.0
- **Prostředí:** Azure
- **Poznámky:** Tato verze používá DSC, jak je zahrnutá ve Windows serveru 2016; pro další operační systémy Windows, nainstaluje [Windows Management Framework 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/) (instalaci WMF vyžaduje restart). Pro Nano Server je nainstalována DSC role na virtuálním počítači.
- **Nové funkce:**
  - Rozšíření DSC je teď dostupné na Nano serveru. Tato verze obsahuje především změny kódu pro spuštění rozšíření na Nano serveru.
  - Vedlejší že byly přidány další vylepšení.

### <a name="version-220"></a>Verze 2,20

- **Datum vydání:** 2. srpna 2016
- **Podpora operačního systému:** Windows Server 2016 Technical Preview, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1
- **Podpora WMF:** WMF 5.1 ve verzi Preview, WMF 5.0 RTM, WMF 4.0 Update, WMF 4.0
- **Prostředí:** Azure
- **Poznámky:** Tato verze používá DSC, jak je zahrnutá ve Windows serveru 2016 Technical Preview; pro další operační systémy Windows, nainstaluje [Windows Management Framework 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/) (instalaci WMF vyžaduje restart).
- **Nové funkce:**
  - Podpora pro WMF 5.1 ve verzi Preview. Při prvním publikování, tato verze byla volitelný upgrade a jste museli zadat Wmfversion = "5.1PP' v šablonách Resource Manageru k instalaci WMF 5.1 ve verzi preview. Wmfversion = 'latest' stále instaluje [WMF 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/). Další informace o WMF 5.1 ve verzi preview, najdete v části [tento blog]( https://blogs.msdn.microsoft.com/powershell/2016/07/16/announcing-windows-management-framework-wmf-5-1-preview/).
  - Podverze ostatní opravy a vylepšení byly přidány.

### <a name="version--219"></a>Verze 2.19

- **Datum vydání:** 3. června 2016
- **Podpora operačního systému:** Windows Server 2016 Technical Preview, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1
- **Podpora WMF:** WMF 5.0 RTM, WMF 4.0 Update, WMF 4.0
- **Prostředí:** Azure, Azure China, Azure Government
- **Poznámky:** Tato verze používá DSC, jak je zahrnutá ve Windows serveru 2016 Technical Preview; pro další operační systémy Windows, nainstaluje [Windows Management Framework 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/) (instalaci WMF vyžaduje restart).
- **Nové funkce:**
  - Rozšíření DSC je teď připojený k Azure China. Tato verze primárně obsahuje opravy pro rozšíření a systémem Azure China.

### <a name="version-218"></a>Verze 2.18

- **Datum vydání:** 3. června 2016
- **Podpora operačního systému:** Windows Server 2016 Technical Preview, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1
- **Podpora WMF:** WMF 5.0 RTM, WMF 4.0 Update, WMF 4.0
- **Prostředí:** Azure
- **Poznámky:** Tato verze používá DSC, jak je zahrnutá ve Windows serveru 2016 Technical Preview; pro další operační systémy Windows, nainstaluje [Windows Management Framework 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/) (instalaci WMF vyžaduje restart).
- **Nové funkce:**
  - Ujistěte se, telemetrie neblokující dojde k chybě při stažení opravy hotfix telemetrie (známý problém Azure DNS) nebo během instalace.
  - Oprava pro občasný problém, kdy přestane rozšíření zpracování konfigurace po restartu. To byla příčinou rozšíření DSC tak si zachováte přechod stavu.
  - Podverze ostatní opravy a vylepšení byly přidány.

### <a name="version-217"></a>Verze 2.17

- **Datum vydání:** 26. dubna 2016
- **Podpora operačního systému:** Windows Server 2016 Technical Preview, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1
- **Podpora WMF:** WMF 5.0 RTM, WMF 4.0 Update, WMF 4.0
- **Prostředí:** Azure
- **Poznámky:** Tato verze používá DSC, jak je zahrnutá ve Windows serveru 2016 Technical Preview; pro další operační systémy Windows, nainstaluje [Windows Management Framework 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/) (instalaci WMF vyžaduje restart).
- **Nové funkce:**
  - Podpora pro WMF 4.0 Update. Další informace o aktualizace WMF 4.0 najdete v tématu [tento blog](https://blogs.msdn.microsoft.com/powershell/2016/01/19/windows-management-framework-wmf-4-0-update-now-available-for-windows-server-2012-windows-server-2008-r2-sp1-and-windows-7-sp1/).
  - Logika opakovaných pokusů o chybách, které se vyskytují během instalace rozšíření DSC nebo při aplikování konfigurace DSC příspěvku rozšíření nainstalujte. Jako součást této změny bude rozšíření znovu zkuste nainstalovat, pokud předchozí instalace se nezdařila nebo znovu přijmout konfiguraci DSC, která předtím selhala, maximálně třikrát dokud nebude dosaženo stavu dokončení (úspěch nebo chyba), nebo pokud novou žádost pochází. Pokud rozšíření se nepovedlo kvůli neplatné uživatelské nastavení/uživatelský vstup, nebude opakovat. V takovém případě rozšíření musí být vyvolána znovu s novou žádost o a opravte nastavení uživatele. Poznámka: Rozšíření DSC je závislá na agenta virtuálního počítače Azure pro opakované pokusy. Agent virtuálního počítače Azure vyvolá rozšíření s poslední neúspěšným požadavkem, dokud nebude dosaženo stavu úspěch nebo chyba.

### <a name="version-216"></a>Verze 2,16

- **Datum vydání:** 21. dubna 2016
- **Podpora operačního systému:** Windows Server 2016 Technical Preview, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1
- **Podpora WMF:** WMF 5.0 RTM, WMF 4.0
- **Prostředí:** Azure
- **Poznámky:** Tato verze používá DSC, jak je zahrnutá ve Windows serveru 2016 Technical Preview; pro další operační systémy Windows, nainstaluje [Windows Management Framework 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/) (instalaci WMF vyžaduje restart).
- **Nové funkce:**
  - Zlepšení zpracování chyb a ostatní opravy menších chyb.
  - Nové vlastnosti v nastavení rozšíření DSC. Povolení rozšíření DSC se přidá "ForcePullAndApply" v AdvancedOptions vydává konfigurací DSC při aktualizaci režimu je o přijetí změn (na rozdíl od výchozí režimu nabízení). Další informace najdete [tento blog](https://blogs.msdn.microsoft.com/powershell/2016/02/26/arm-dsc-extension-settings/) zobrazíte další informace o nastavení rozšíření DSC.

### <a name="version-215"></a>Verze 2,15

- **Datum vydání:** 14. března 2016
- **Podpora operačního systému:** Windows Server 2016 Technical Preview, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1
- **Podpora WMF:** WMF 5.0 RTM, WMF 4.0
- **Prostředí:** Azure
- **Poznámky:** Tato verze používá DSC, jak je zahrnutá ve Windows serveru 2016 Technical Preview; pro další operační systémy Windows, nainstaluje [Windows Management Framework 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/) (instalaci WMF vyžaduje restart).
- **Nové funkce:**
  - Ve verzi rozšíření 2.14 byly součástí změny k instalaci WMF RTM. Při upgradu z verze rozšíření 2.13.2.0 k 2.14.0.0, můžete si všimnout, že selhání některých rutin DSC nebo konfigurace se nezdaří s chybou – 'No nalezena Instance s dané hodnoty vlastností'. Další informace najdete v tématu [poznámky k verzi DSC](https://msdn.microsoft.com/en-us/powershell/wmf/limitation_dsc). Alternativní řešení těchto problémů byly přidány ve verzi 2.15.
  - Bohužel Pokud už máte nainstalovanou verzi 2.14 a běží na jednu z výše uvedené dva problémy, je potřeba tyto kroky provést ručně.  V relaci Powershellu se zvýšenými oprávněními:
    - `Remove-Item -Path $env:SystemRoot\system32\Configuration\DSCEngineCache.mof`
    - `mofcomp $env:windir\system32\wbem\DscCoreConfProv.mof`

### <a name="version-214"></a>Verze 2.14

- **Datum vydání:** 25. února 2016
- **Podpora operačního systému:** Windows Server 2016 Technical Preview, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1
- **Podpora WMF:** WMF 5.0 RTM, WMF 4.0
- **Prostředí:** Azure
- **Poznámky:** Tato verze používá DSC, jak je zahrnutá ve Windows serveru 2016 Technical Preview; pro další operační systémy Windows, nainstaluje [Windows Management Framework 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/) (instalaci WMF vyžaduje restart).
- **Nové funkce:**
  - Používá WMF RTM.
  - Povolí shromažďování dat za účelem zlepšení kvality rozšíření DSC. Další informace najdete v tématu [blogu](https://blogs.msdn.microsoft.com/powershell/2016/02/02/azure-dsc-extension-data-collection-2/).
  - Poskytuje formátu aktualizované nastavení pro rozšíření v šabloně Resource Manageru. Další informace najdete v tématu [blogu](https://blogs.msdn.microsoft.com/powershell/2016/02/26/arm-dsc-extension-settings/).
  - Opravy chyb a další vylepšení.

## <a name="next-steps"></a>Další kroky

- Další informace o prostředí PowerShell DSC, přejděte [centrum dokumentace k Powershellu](../overview/overview.md).
- Zkontrolujte [šablony Resource Manageru pro rozšíření DSC](/azure/virtual-machines/extensions/dsc-template).
- Další funkce, které můžete spravovat pomocí prostředí PowerShell DSC a další prostředky DSC, přejděte [Galerie prostředí PowerShell](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0).
- Podrobnosti o předání parametrů citlivé na konfigurace najdete v tématu [Správa přihlašovacích údajů, bezpečně se obslužné rutiny rozšíření DSC](/azure/virtual-machines/extensions/dsc-credentials).