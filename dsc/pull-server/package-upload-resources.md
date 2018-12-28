---
ms.date: 12/12/2018
keywords: DSC, powershell, konfigurace, instalační program
title: Balíček a prostředky nahrávání na serveru vyžádané replikace
ms.openlocfilehash: 29a62f96393a53c9e7da57a5e51732dcb0937194
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403661"
---
# <a name="package-and-upload-resources-to-a-pull-server"></a>Balíček a prostředky nahrávání na serveru vyžádané replikace

Následující části se předpokládá, že jste již nastavili serveru vyžádaných replikací s. Pokud jste nenastavili serveru o přijetí změn, můžete použít následující příručky:

- [Nastavení serveru vyžádané replikace DSC SMB](pullServerSmb.md)
- [Nastavení serveru vyžádané replikace DSC HTTP](pullServer.md)

Každý cílový uzel je nakonfigurovat ke stažení konfigurace, prostředků a dokonce i oznámit svůj stav. Tento článek vám ukáže jak nahrát prostředky, takže jsou k dispozici chcete stahovat a nastavte klienty, aby automaticky stáhnout prostředky. Když uzel obdrží přiřazených konfigurací prostřednictvím **o přijetí změn** nebo **Push** (v5), automaticky stáhne všechny prostředky, které konfigurace z umístění zadaného v LCM vyžaduje.

## <a name="package-resource-modules"></a>Balíček prostředků moduly

Každý prostředek k dispozici pro klienty ke stažení musí být uložen v souboru ".zip". Následující příklad zobrazí požadované kroky pomocí [xPSDesiredStateConfiguration](https://www.powershellgallery.com/packages/xPSDesiredStateConfiguration/8.4.0.0) prostředků.

> [!NOTE]
> Pokud máte klienty pomocí prostředí PowerShell 4.0, bude muset flaten strukturu složek prostředků a odeberte všechny verze složky. Další informace najdete v tématu [více verzí prostředků](../configurations/import-dscresource.md#multiple-resource-versions).

Adresář prostředků pomocí libovolný nástroj, skript nebo metod, které dáváte přednost dokáže komprimovat. Ve Windows, můžete *klikněte pravým tlačítkem na* na adresář "xPSDesiredStateConfiguration" a vyberte "Odeslat" a potom "Komprimovanou složku".

![Klikněte pravým tlačítkem myši](../media/right-click.gif)

### <a name="naming-the-resource-archive"></a>Pojmenování prostředků archivu

Prostředek archive musí mít názvy v následujícím formátu:

```
{ModuleName}_{Version}.zip
```

V předchozím příkladu by měl být "xPSDesiredStateConfiguration.zip" přejmenováno "xPSDesiredStateConfiguration_8.4.4.0.zip".

### <a name="create-checksums"></a>Vytvořit kontrolní součty

Jakmile modul prostředků byl komprimované a přejmenovat, je potřeba vytvořit **kontrolního součtu**.  **Kontrolního součtu** používají, LCM na straně klienta, k určení, zda prostředek byl změněn a musí být znovu stažena. Můžete vytvořit **kontrolního součtu** s [New-DSCCheckSum](/powershell/module/PSDesiredStateConfiguration/New-DSCCheckSum) rutiny, jak je znázorněno v následujícím příkladu.

```powershell
New-DscChecksum -Path .\xPSDesiredStateConfiguration_8.4.4.0.zip
```

Žádný výstup se nezobrazí, ale měli byste vidět "xPSDesiredStateConfiguration_8.4.4.0.zip.checksum". Můžete také spustit `New-DSCCheckSum` proti adresář souborů pomocí `-Path` parametru. Pokud kontrolní součet již existuje, lze vynutit být znovu vytvořen s `-Force` parametru.

### <a name="where-to-store-resource-archives"></a>Kam se mají ukládat prostředků archivy

#### <a name="on-a-dsc-http-pull-server"></a>Na Server DSC na vyžádání protokolu HTTP

Při nastavení HTTP serveru o přijetí změn, jak je vysvětleno v [nastavení serveru vyžádané replikace DSC HTTP](pullServer.md), určit adresáře pro **ModulePath** a **ConfigurationPath** klíče. **ConfigurationPath** klíč označuje ukládat všechny soubory ".mof". **ModulePath** označuje, kde by měly být uloženy všechny moduly, které prostředek DSC.

```powershell
    xDscWebService PSDSCPullServer
    {
    ...
        ModulePath              = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Modules"
        ConfigurationPath       = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration"
    ...
    }

```

#### <a name="on-an-smb-share"></a>Ve sdílené složce protokolu SMB

Pokud jste zadali **ResourceRepositoryShare**při nastavování vašeho klienta o přijetí změn ukládají archivy a kontrolní součty v **SourcePath** z **ResourceRepositoryShare** bloku.

```powershell
ConfigurationRepositoryShare SMBPullServer
{
    SourcePath = '\\SMBPullServer\Configurations'
}

ResourceRepositoryShare SMBResourceServer
{
    SourcePath = '\\SMBPullServer\Resources'
}
```

Pokud jste zadali jenom **ConfigurationRepositoryShare**při nastavování vašeho klienta o přijetí změn ukládají archivy a kontrolní součty v **SourcePath** z  **ConfigurationRepositoryShare** bloku.

```powershell
ConfigurationRepositoryShare SMBPullServer
{
    SourcePath = '\\SMBPullServer\Pull'
}
```

#### <a name="updating-resources"></a>Aktualizují se prostředky

Můžete vynutit uzlu se aktualizovat jeho prostředky tak, že změníte číslo verze v archivu názvu nebo vytvořením nového kontrolního součtu. Klienta o přijetí změn zkontroluje novějších verzích požadované prostředky, jakož i aktualizovat kontrolní součty, při jeho LCM se aktualizuje.

## <a name="see-also"></a>Viz taky

- [Nastavení serveru vyžádané replikace DSC SMB](pullServerSmb.md)
- [Nastavení serveru vyžádané replikace DSC HTTP](pullServer.md)
