---
ms.date: 12/12/2018
keywords: DSC, powershell, konfigurace, instalační program
title: Publikování na serveru vyžádaných replikací s použitím ID konfigurace (v4/v5)
ms.openlocfilehash: 0144fec43d7a8d65b79891567cc0dc3952175343
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403686"
---
# <a name="publish-to-a-pull-server-using-configuration-ids-v4v5"></a>Publikování na serveru vyžádaných replikací s použitím ID konfigurace (v4/v5)

Následující části se předpokládá, že jste již nastavili serveru vyžádaných replikací s. Pokud jste nenastavili serveru o přijetí změn, můžete použít následující příručky:

- [Nastavení serveru vyžádané replikace DSC SMB](pullServerSmb.md)
- [Nastavení serveru vyžádané replikace DSC HTTP](pullServer.md)

Každý cílový uzel je nakonfigurovat ke stažení konfigurace, prostředků a dokonce i oznámit svůj stav. Tento článek vám ukáže jak nahrát prostředky, takže jsou k dispozici chcete stahovat a nastavte klienty, aby automaticky stáhnout prostředky. Když uzel obdrží přiřazených konfigurací prostřednictvím **o přijetí změn** nebo **Push** (v5), automaticky stáhne všechny prostředky, které konfigurace z umístění zadaného v LCM vyžaduje.

## <a name="compile-configurations"></a>Kompilace konfigurace

Prvním krokem při ukládání [konfigurace](../configurations/configurations.md) na serveru vyžádaných replikací s, je pro jejich zkompilování do souborů ".mof". Konfigurace obecných a pro víc klientů, použijete `localhost` v uzlu blokování. Následující příklad ukazuje konfigurační prostředí, které používá `localhost` místo názvu konkrétního klienta.

```powershell
Configuration GenericConfig
{
    Node localhost
    {

    }
}
GenericConfig
```

Jakmile jste zkompilovali obecné konfigurace, měli byste mít "localhost.mof" soubor.

## <a name="renaming-the-mof-file"></a>Přejmenování souboru MOF

Můžete ukládat konfigurační soubory ".mof" na serveru vyžádané replikace pomocí **ConfigurationName** nebo **ConfigurationID**. V závislosti na tom, jak budete chtít nastavit vaši klienti o přijetí změn můžete použít níže správně přejmenovat soubory kompilované ".mof".

### <a name="configuration-ids-guid"></a>Konfigurace ID (GUID)

Budete muset přejmenovat soubor "localhost.mof" k "<GUID>.mof" soubor. Můžete vytvořit náhodnou **Guid** pomocí příkladu níže nebo pomocí [nový identifikátor Guid](/powershell/module/microsoft.powershell.utility/new-guid) rutiny.

```powershell
[System.Guid]::NewGuid()
```

Ukázkový výstup

```output
Guid
----
64856475-939e-41fb-aba5-4469f4006059
```

Přejmenujte soubor ".mof" pomocí libovolné metody přijatelné. V následujícím příkladu [přejmenovat položku](/powershell/module/microsoft.powershell.management/rename-item) rutiny.

```powershell
Rename-Item -Path .\localhost.mof -NewName '64856475-939e-41fb-aba5-4469f4006059.mof'
```

Další informace o používání **GUID** ve vašem prostředí, najdete v článku [plánování GUID](/powershell/dsc/secureserver#guids).

### <a name="configuration-names"></a>Názvy konfigurace

Budete muset přejmenovat soubor "localhost.mof" k "<Configuration Name>.mof" soubor. V následujícím příkladu se používá název konfigurace z předchozí části. Přejmenujte soubor ".mof" pomocí libovolné metody přijatelné. V následujícím příkladu [přejmenovat položku](/powershell/module/microsoft.powershell.management/rename-item) rutiny.

```powershell
Rename-Item -Path .\localhost.mof -NewName 'GenericConfig.mof'
```

## <a name="create-the-checksum"></a>Vytvořit kontrolní součet

Každý soubor ".mof" uloženy na serveru vyžádané replikace nebo sdílenou složku protokolu SMB musí mít přidružený ".checksum" soubor. Tento soubor umožňuje klientům vědět, kdy přidružené ".mof" soubor došlo ke změně a by měl být staženy znovu.

Můžete vytvořit **kontrolního součtu** s [New-DSCCheckSum](/powershell/module/psdesiredstateconfiguration/new-dscchecksum) rutiny. Můžete také spustit `New-DSCCheckSum` proti adresář souborů pomocí `-Path` parametru. Pokud kontrolní součet již existuje, lze vynutit být znovu vytvořen s `-Force` parametru. Následující příklad zadaný adresář obsahující soubor ".mof" z předchozí části a používá `-Force` parametru.

```powershell
New-DscChecksum -Path '.\' -Force
```

Žádný výstup se nezobrazí, ale měli byste vidět "<GUID or Configuration Name>. mof.checksum" soubor.

## <a name="where-to-store-mof-files-and-checksums"></a>Kam se mají ukládat soubory MOF a kontrolní součty

### <a name="on-a-dsc-http-pull-server"></a>Na Server DSC na vyžádání protokolu HTTP

Při nastavení HTTP serveru o přijetí změn, jak je vysvětleno v [nastavení serveru vyžádané replikace DSC HTTP](pullServer.md), určit adresáře pro **ModulePath** a **ConfigurationPath** klíče. **ConfigurationPath** klíč označuje ukládat všechny soubory ".mof". **ConfigurationPath** označuje, kde by měla být uložena všechny soubory ".mof" a ".checksum".

```powershell
    xDscWebService PSDSCPullServer
    {
    ...
        ModulePath              = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Modules"
        ConfigurationPath       = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration"
    ...
    }

```

### <a name="on-an-smb-share"></a>Ve sdílené složce protokolu SMB

Při nastavování klienta o přijetí změn do použít sdílenou složku SMB, zadejte **ConfigurationRepositoryShare**. Všechny soubory ".mof" a ".checksum" soubory pak je ukládat **SourcePath** z **ConfigurationRepositoryShare** bloku.

```powershell
ConfigurationRepositoryShare SMBPullServer
{
    SourcePath = '\\SMBPullServer\Pull'
}
```

## <a name="next-steps"></a>Další kroky

V dalším kroku bude chtít nakonfigurovat klienty o přijetí změn pro vyžádanou zadanou konfiguraci. Další informace naleznete v následujících příručkách:

- [Při nastavování klienta o přijetí změn pomocí ID konfigurace (v4)](pullClientConfigId4.md)
- [Při nastavování klienta o přijetí změn pomocí ID konfigurace (v5)](pullClientConfigId.md)
- [Při nastavování klienta o přijetí změn použití konfiguračních názvů (v5)](pullClientConfigNames.md)

## <a name="see-also"></a>Viz taky

- [Nastavení serveru vyžádané replikace DSC SMB](pullServerSmb.md)
- [Nastavení serveru vyžádané replikace DSC HTTP](pullServer.md)
- [Balíček a prostředky nahrávání na serveru vyžádané replikace](package-upload-resources.md)
