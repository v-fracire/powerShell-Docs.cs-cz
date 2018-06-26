---
description: Další informace o historii verzí pro rozšíření konfigurace požadovaného stavu (DSC) v Azure.
ms.date: 06/21/2018
keywords: DSC prostředí powershell, azure, rozšíření
title: Historie verzí Azure rozšíření DSC
ms.openlocfilehash: 25248288291b9bf8efe6ce1eef203a552cd17736
ms.sourcegitcommit: 68093cc12a7a22c53d11ce7d33c18622921a0dd1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/26/2018
ms.locfileid: "36940323"
---
# <a name="azure-desired-state-configuration-extension-version-history"></a>Historie verzí rozšíření konfigurace požadovaná stavu Azure

Rozšíření virtuálního počítače Azure požadovaného stavu konfigurace (DSC) se aktualizuje podle potřeby pro podporu vylepšení a nové funkce Azure, Windows Server a systému Windows Management Framework (WMF) zahrnující prostředí Windows PowerShell.

Tento článek poskytuje informace o každou verzi rozšíření virtuálního počítače Azure DSC, jaké prostředí podporuje a komentáře a poznámky na nové funkce nebo změny.

## <a name="latest-version"></a>Nejnovější verzi

### <a name="version-276"></a>Verze 2.76

- **Datum vydání:**
  - 9 může 2018 (Azure) | 21 červen 2018 (Čína Azure, Azure Government)
- **Podpora operačního systému:**
  - Windows Server 2016
  - Windows Server 2012 R2
  - Windows Server 2012
  - Windows Server 2008 R2 SP1
  - Klient Windows 7/8.1/10
  - Nano Server
- **Podpora produktu WMF:**
  - WMF 5.1
  - WMF 5.0 RTM
  - Aktualizace WMF 4.0
  - FORMÁT WMF 4.0
- **Prostředí:**
  - Azure
  - Azure Čína
  - Azure Government
- **Poznámky:** tato verze používá DSC, jak je zahrnutá v systému Windows Server 2016; pro další operační systémy Windows se instaluje [Windows Management Framework 5.1](https://blogs.msdn.microsoft.com/powershell/2016/12/06/wmf-5-1-releasing-january-2017/) (instalaci WMF vyžaduje restart). Pro Nano Server je nainstalována DSC role do virtuálního počítače.
- **Nové funkce:**
  - Zlepšování rozšíření metadat pro substatus a dalších menšími opravami chyb.

## <a name="supported-versions"></a>Podporované verze

> [!WARNING]
> Verze 2.4 prostřednictvím 2.13 použijte WMF 5.0 Public Preview, jejichž podpisové certifikáty vyprší za srpna 2016.  Další informace o tomto problému najdete v tématu [příspěvku na blogu](https://blogs.msdn.microsoft.com/powershell/2016/05/24/azure-dsc-extension-versions-2-4-up-to-2-13-will-retire-in-august/).

### <a name="version-275"></a>Verze 2,75

- **Datum vydání:** 5 března 2018
- **Podpora operačního systému:** systému Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1, Windows klienta 7/8.1/10, Nano Server
- **Podpora produktu WMF:** WMF 5.1, WMF 5.0 RTM, aktualizace WMF 4.0, WMF 4.0
- **Prostředí:** Azure
- **Poznámky:** tato verze používá DSC, jak je zahrnutá v systému Windows Server 2016; pro další operační systémy Windows se instaluje [Windows Management Framework 5.1](https://blogs.msdn.microsoft.com/powershell/2016/12/06/wmf-5-1-releasing-january-2017/) (instalaci WMF vyžaduje restart). Pro Nano Server je nainstalována DSC role do virtuálního počítače.
- **Nové funkce:**
  - Po Githubu poslední přesun do protokolu TLS 1.2 nelze připojit virtuální počítač pro Azure Automation DSC pomocí šablon DIY Resource Manageru, které jsou k dispozici na webu Azure Marketplace nebo pomocí rozšíření DSC získat žádné konfiguraci hostované na Githubu. Zobrazí se zpráva podobná následující při nasazování rozšíření:

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

  - Teď se vynucuje TLS 1.2, v nové verzi rozšíření. Při nasazování rozšíření, pokud již máte AutoUpgradeMinorVersion = true v šabloně Resource Manager, pak rozšíření získají autoupgraded k 2,75. Pro ruční aktualizace, zadejte `TypeHandlerVersion = 2.75` v šabloně Resource Manager.

### <a name="version-270---272"></a>Verze 2.70 2.72

- **Datum vydání:** 13 listopadu 2017
- **Podpora operačního systému:** systému Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1, Windows klienta 7/8.1/10, Nano Server
- **Podpora produktu WMF:** WMF 5.1, WMF 5.0 RTM, aktualizace WMF 4.0, WMF 4.0
- **Prostředí:** Azure
- **Poznámky:** tato verze používá DSC, jak je zahrnutá v systému Windows Server 2016; pro další operační systémy Windows se instaluje [Windows Management Framework 5.1](https://blogs.msdn.microsoft.com/powershell/2016/12/06/wmf-5-1-releasing-january-2017/) (instalaci WMF vyžaduje restart). Pro Nano Server je nainstalována DSC role do virtuálního počítače.
- **Nové funkce:**
  - Chyb opravy a vylepšení, která zjednodušuje použití Azure Automation DSC prostřednictvím portálu uživatelského rozhraní, jakož i šablony Resource Manageru.  Další informace najdete v tématu [výchozí konfigurační skript](https://docs.microsoft.com/en-us/azure/virtual-machines/windows/extensions-dsc-overview#default-configuration-script) v rozšíření DSC dokumentaci.

### <a name="version-226"></a>Verze 2.26

- **Datum vydání:** 9. června 2017
- **Podpora operačního systému:** systému Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1, Windows klienta 7/8.1/10, Nano Server
- **Podpora produktu WMF:** WMF 5.1, WMF 5.0 RTM, aktualizace WMF 4.0, WMF 4.0
- **Prostředí:** Azure
- **Poznámky:** tato verze používá DSC, jak je zahrnutá v systému Windows Server 2016; pro další operační systémy Windows se instaluje [Windows Management Framework 5.1](https://blogs.msdn.microsoft.com/powershell/2016/12/06/wmf-5-1-releasing-january-2017/) (instalaci WMF vyžaduje restart). Pro Nano Server je nainstalována DSC role do virtuálního počítače.
- **Nové funkce:**
  - Vylepšení telemetrie.

### <a name="version-225"></a>Verze 2.25

- **Datum vydání:** 2 června 2017
- **Podpora operačního systému:** systému Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1, Windows klienta 7/8.1/10, Nano Server
- **Podpora produktu WMF:** WMF 5.1, WMF 5.0 RTM, aktualizace WMF 4.0, WMF 4.0
- **Prostředí:** Azure
- **Poznámky:** tato verze používá DSC, jak je zahrnutá v systému Windows Server 2016; pro další operační systémy Windows se instaluje [Windows Management Framework 5.1](https://blogs.msdn.microsoft.com/powershell/2016/12/06/wmf-5-1-releasing-january-2017/) (instalaci WMF vyžaduje restart). Pro Nano Server je nainstalována DSC role do virtuálního počítače.
- **Nové funkce:**
  - Několik oprav chyb a další menší vylepšení byly přidány.

### <a name="version-224"></a>Verze 2,24

- **Datum vydání:** 13. dubna 2017
- **Podpora operačního systému:** systému Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1, Nano Server
- **Podpora produktu WMF:** WMF 5.1, WMF 5.0 RTM, aktualizace WMF 4.0, WMF 4.0
- **Prostředí:** Azure
- **Poznámky:** tato verze používá DSC, jak je zahrnutá v systému Windows Server 2016; pro další operační systémy Windows se instaluje [Windows Management Framework 5.1](https://blogs.msdn.microsoft.com/powershell/2016/12/06/wmf-5-1-releasing-january-2017/) (instalaci WMF vyžaduje restart). Pro Nano Server je nainstalována DSC role do virtuálního počítače.
- **Nové funkce:**
  - Zpřístupní virtuálních počítačů UUID & ID agenta DSC jako rozšíření metadat. Byly přidány další menší vylepšení.

### <a name="version-223"></a>Verze 2.23

- **Datum vydání:** 15. března 2017
- **Podpora operačního systému:** systému Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1, Nano Server
- **Podpora produktu WMF:** WMF 5.1, WMF 5.0 RTM, aktualizace WMF 4.0, WMF 4.0
- **Prostředí:** Azure
- **Poznámky:** tato verze používá DSC, jak je zahrnutá v systému Windows Server 2016; pro další operační systémy Windows se instaluje [Windows Management Framework 5.1](https://blogs.msdn.microsoft.com/powershell/2016/12/06/wmf-5-1-releasing-january-2017/) (instalaci WMF vyžaduje restart). Pro Nano Server je nainstalována DSC role do virtuálního počítače.
- **Nové funkce:**
  - Byly přidány spoustu dalších vylepšení a opravy chyb.

### <a name="version-222"></a>Verze 2.22

- **Datum vydání:** 8 února 2017
- **Podpora operačního systému:** systému Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1, Nano Server
- **Podpora produktu WMF:** WMF 5.1, WMF 5.0 RTM, aktualizace WMF 4.0, WMF 4.0
- **Prostředí:** Azure
- **Poznámky:** tato verze používá DSC, jak je zahrnutá v systému Windows Server 2016; pro další operační systémy Windows se instaluje [Windows Management Framework 5.1](https://blogs.msdn.microsoft.com/powershell/2016/12/06/wmf-5-1-releasing-january-2017/) (instalaci WMF vyžaduje restart). Pro Nano Server je nainstalována DSC role do virtuálního počítače.
- **Nové funkce:**
  - Rozšíření DSC teď obsahuje podporu WMF 5.1.
  - Vedlejší že byly přidány další vylepšení.

### <a name="version-221"></a>Verze 2.21

- **Datum vydání:** 2. prosince 2016
- **Podpora operačního systému:** systému Windows Server 2016, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1, Nano Server
- **Podpora produktu WMF:** WMF 5.1 Preview, WMF 5.0 RTM, aktualizace WMF 4.0, WMF 4.0
- **Prostředí:** Azure
- **Poznámky:** tato verze používá DSC, jak je zahrnutá v systému Windows Server 2016; pro další operační systémy Windows se instaluje [Windows Management Framework 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/) (instalaci WMF vyžaduje restart). Pro Nano Server je nainstalována DSC role do virtuálního počítače.
- **Nové funkce:**
  - Rozšíření DSC je nyní k dispozici na Nano Server. Tato verze obsahuje především změn kódu pro spuštění rozšíření na Nano Server.
  - Vedlejší že byly přidány další vylepšení.

### <a name="version-220"></a>Verze 2,20

- **Datum vydání:** 2 srpna 2016
- **Podpora operačního systému:** Windows Server 2016 Technical Preview, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1
- **Podpora produktu WMF:** WMF 5.1 Preview, WMF 5.0 RTM, aktualizace WMF 4.0, WMF 4.0
- **Prostředí:** Azure
- **Poznámky:** tato verze používá DSC, jak je zahrnutá ve Windows serveru 2016 Technical Preview; pro další operační systémy Windows se instaluje [Windows Management Framework 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/) (instalaci WMF vyžaduje restart).
- **Nové funkce:**
  - Podpora produktu WMF 5.1 Preview. Při prvním publikování, tato verze je volitelný upgrade a jste museli zadat Wmfversion = ' 5.1PP' v šablonách Resource Manager k instalaci WMF 5.1 preview. Wmfversion = 'nejnovější' stále nainstaluje [WMF 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/). Další informace o WMF 5.1 preview najdete v tématu [tomto blogu]( https://blogs.msdn.microsoft.com/powershell/2016/07/16/announcing-windows-management-framework-wmf-5-1-preview/).
  - Ostatní opravy malé a vylepšení byly přidány.

### <a name="version--219"></a>Verze 2.19

- **Datum vydání:** 3. června 2016
- **Podpora operačního systému:** Windows Server 2016 Technical Preview, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1
- **Podpora produktu WMF:** WMF 5.0 RTM, aktualizace WMF 4.0, WMF 4.0
- **Prostředí:** Azure, Azure Číně Azure Government.
- **Poznámky:** tato verze používá DSC, jak je zahrnutá ve Windows serveru 2016 Technical Preview; pro další operační systémy Windows se instaluje [Windows Management Framework 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/) (instalaci WMF vyžaduje restart).
- **Nové funkce:**
  - Rozšíření DSC je nyní zařazený, nemá pro Azure China. Tato verze obsahuje především opravy pro spuštění rozšíření na Azure China.

### <a name="version-218"></a>Verze 2.18

- **Datum vydání:** 3. června 2016
- **Podpora operačního systému:** Windows Server 2016 Technical Preview, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1
- **Podpora produktu WMF:** WMF 5.0 RTM, aktualizace WMF 4.0, WMF 4.0
- **Prostředí:** Azure
- **Poznámky:** tato verze používá DSC, jak je zahrnutá ve Windows serveru 2016 Technical Preview; pro další operační systémy Windows se instaluje [Windows Management Framework 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/) (instalaci WMF vyžaduje restart).
- **Nové funkce:**
  - Ujistěte se, telemetrie neblokující když dojde k chybě při stažení opravy hotfix telemetrie (známý problém Azure DNS) nebo během instalace.
  - Pro dočasné potíže vyřešte, kde rozšíření zastaví zpracování konfigurace po restartu systému. To se vyvolá rozšíření DSC zůstat v přechod stavu.
  - Ostatní opravy malé a vylepšení byly přidány.

### <a name="version-217"></a>Verze 2.17

- **Datum vydání:** 26. dubna 2016
- **Podpora operačního systému:** Windows Server 2016 Technical Preview, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1
- **Podpora produktu WMF:** WMF 5.0 RTM, aktualizace WMF 4.0, WMF 4.0
- **Prostředí:** Azure
- **Poznámky:** tato verze používá DSC, jak je zahrnutá ve Windows serveru 2016 Technical Preview; pro další operační systémy Windows se instaluje [Windows Management Framework 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/) (instalaci WMF vyžaduje restart).
- **Nové funkce:**
  - Podpora produktu WMF 4.0 Update. Další informace o aktualizace WMF 4.0 najdete v tématu [tomto blogu](https://blogs.msdn.microsoft.com/powershell/2016/01/19/windows-management-framework-wmf-4-0-update-now-available-for-windows-server-2012-windows-server-2008-r2-sp1-and-windows-7-sp1/).
  - Logika opakovaných pokusů o chybách, které se vyskytují během instalace rozšíření DSC nebo při aplikování konfigurace DSC post rozšíření nainstalovat. V rámci této změny bude rozšíření instalaci opakovat, pokud se předchozí instalace nezdařila nebo znovu uplatní konfigurace DSC, který měl předtím selhal, maximálně třikrát dokud nebude dosaženo stavu dokončení (úspěch nebo chyba), nebo pokud novou žádost pochází. Pokud rozšíření nezdaří z důvodu neplatné uživatelské nastavení nebo uživatelský vstup, není opakujte. Rozšíření v takovém případě musí být volána znovu s novou žádost a opravte nastavení uživatele. Poznámka: Rozšíření DSC je závislá na agenta virtuálního počítače Azure pro opakované pokusy. Agent virtuálního počítače Azure vyvolá rozšíření s poslední chybných požadavků, dokud nebude dosaženo stavu úspěch nebo chyba.

### <a name="version-216"></a>Verze 2,16

- **Datum vydání:** 21. dubna 2016
- **Podpora operačního systému:** Windows Server 2016 Technical Preview, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1
- **Podpora produktu WMF:** WMF 5.0 RTM, WMF 4.0
- **Prostředí:** Azure
- **Poznámky:** tato verze používá DSC, jak je zahrnutá ve Windows serveru 2016 Technical Preview; pro další operační systémy Windows se instaluje [Windows Management Framework 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/) (instalaci WMF vyžaduje restart).
- **Nové funkce:**
  - Zlepšení zpracování chyb a další menšími opravami chyb.
  - Nové vlastnosti v rozšíření DSC nastavení. Povolit rozšíření DSC se přidá 'ForcePullAndApply' v AdvancedOptions uplatní konfigurace DSC, pokud režim aktualizace je vyžadování (na rozdíl od výchozí režim Push). Další informace naleznete v [tomto blogu](https://blogs.msdn.microsoft.com/powershell/2016/02/26/arm-dsc-extension-settings/) získat další informace o nastavení rozšíření DSC.

### <a name="version-215"></a>Verze 2,15

- **Datum vydání:** 14. března 2016
- **Podpora operačního systému:** Windows Server 2016 Technical Preview, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1
- **Podpora produktu WMF:** WMF 5.0 RTM, WMF 4.0
- **Prostředí:** Azure
- **Poznámky:** tato verze používá DSC, jak je zahrnutá ve Windows serveru 2016 Technical Preview; pro další operační systémy Windows se instaluje [Windows Management Framework 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/) (instalaci WMF vyžaduje restart).
- **Nové funkce:**
  - Ve verzi rozšíření 2.14 byly součástí změny k instalaci WMF RTM. Při upgradu z verze rozšíření 2.13.2.0 k 2.14.0.0, můžete si všimnout, že některé rutiny DSC selhat nebo konfiguraci selže s chybou –, ne nalezena Instance s danými hodnotami vlastností'. Další informace najdete v tématu [poznámky k verzi DSC](https://msdn.microsoft.com/en-us/powershell/wmf/limitation_dsc). Alternativní řešení těchto problémů byly přidány v 2.15 verzi.
  - Bohužel Pokud již máte nainstalovanou verzi 2.14 a běží do jedné z výše uvedených dva problémy, musíte provést tyto kroky ručně.  V zvýšenými relaci prostředí PowerShell:
    - `Remove-Item -Path $env:SystemRoot\system32\Configuration\DSCEngineCache.mof`
    - `mofcomp $env:windir\system32\wbem\DscCoreConfProv.mof`

### <a name="version-214"></a>Verze 2.14

- **Datum vydání:** 25. února 2016
- **Podpora operačního systému:** Windows Server 2016 Technical Preview, Windows Server 2012 R2, Windows Server 2012, Windows Server 2008 R2 SP1
- **Podpora produktu WMF:** WMF 5.0 RTM, WMF 4.0
- **Prostředí:** Azure
- **Poznámky:** tato verze používá DSC, jak je zahrnutá ve Windows serveru 2016 Technical Preview; pro další operační systémy Windows se instaluje [Windows Management Framework 5.0 RTM](https://blogs.msdn.microsoft.com/powershell/2015/12/16/windows-management-framework-wmf-5-0-rtm-is-now-available/) (instalaci WMF vyžaduje restart).
- **Nové funkce:**
  - Používá WMF RTM.
  - Umožňuje shromažďování dat za účelem zlepšení kvality rozšíření DSC. Další informace najdete v tématu [na blogu](https://blogs.msdn.microsoft.com/powershell/2016/02/02/azure-dsc-extension-data-collection-2/).
  - Poskytuje formátu aktualizované nastavení pro rozšíření v šabloně Resource Manager. Další informace najdete v tématu [na blogu](https://blogs.msdn.microsoft.com/powershell/2016/02/26/arm-dsc-extension-settings/).
  - Opravy chyb a další rozšíření.

## <a name="next-steps"></a>Další kroky

- Další informace o DSC Powershellu, přejděte na [centru dokumentace prostředí PowerShell](overview.md).
- Zkontrolujte [šablony Resource Manageru pro rozšíření DSC](/azure/virtual-machines/windows/extensions-dsc-template).
- Pro další funkce, které můžete spravovat pomocí DSC Powershellu a pro další prostředky DSC, přejděte [Galerie prostředí PowerShell](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0).
- Podrobnosti o předávání citlivých parametrů do konfigurace najdete v tématu [spravovat pověření bezpečně s obslužná rutina rozšíření DSC](/azure/virtual-machines/windows/extensions-dsc-credentials).