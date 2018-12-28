---
ms.date: 12/12/2018
keywords: DSC, powershell, konfigurace, instalační program
title: Pomocí Import-DSCResource
ms.openlocfilehash: 6bc3c1aa1d34a05e3188666da825322235c0672e
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403779"
---
# <a name="using-import-dscresource"></a>Pomocí Import-DSCResource

`Import-DScResource` je dynamické klíčové slovo, které jde použít jenom uvnitř bloku skriptu konfigurace. `Import-DSCResource` – Klíčové slovo import všechny prostředky potřebné v konfiguraci. Prostředky v rámci `$phsome` jsou importovány automaticky, ale přesto považuje osvědčeným postupem je explicitně importují všechny prostředky používané v vaše [konfigurace](Configurations.md).

Syntaxe pro `Import-DSCResource` je uveden níže.

```syntax
Import-DscResource [-Name <ResourceName(s)>] [-ModuleName <ModuleName(s)>]
```

|Parametr  |Popis  |
|---------|---------|
|`-Name`|Názvy prostředků DSC, která je nutné naimportovat. Pokud není zadán název modulu, tento příkaz vyhledá pro tyto prostředky DSC v rámci tohoto modulu; v opačném případě příkaz vyhledá prostředky DSC v všechny cesty prostředku DSC. Jsou podporovány zástupné znaky.|
|`-ModuleName`|Názvy kontejnerů modulu nebo modul byly.  Pokud chcete zadat prostředky pro import z modulu, příkaz se pokusí importovat pouze tyto prostředky. Pokud zadáte pouze modulu, tento příkaz importuje všechny prostředky DSC v modulu.|

Můžete použít zástupné znaky `-Name` parametr při použití `Import-DSCResource`.

```powershell
Import-DscResource -Name * -ModuleName xActiveDirectory;
```

## <a name="example-use-import-dscresource-within-a-configuration"></a>Příklad: Použití Import-DSCResource v rámci konfigurace

```powershell
Configuration MSDSCConfiguration
{
    # Search for and imports Service, File, and Registry from the module PSDesiredStateConfiguration.
    Import-DSCResource -ModuleName MS_DSC1 -name Service, File, Registry

    # Search for and import Resource1 from the module that defines it.
    # If only –Name parameter is used then resources can belong to different PowerShell modules as well.
    # TimeZone resource is from the ComputerManagementDSC module which is not installed by default.
    Import-DSCResource -Name File, TimeZone

    # Search for and import all DSC resources inside the module PSDesiredStateConfiguration.
    Import-DSCResource -ModuleName PSDesiredStateConfiguration
...
```

> [!NOTE]
> Zadání více hodnot pro názvy prostředků a moduly ve stejném příkazu se nepodporují. Může mít nedeterministické chování, o který prostředek se má načíst z modulu, který v případě, že stejný prostředek existuje v několika modulů. Následující příkaz způsobí chyby během kompilace.
>
> ```powershell
> Import-DscResource -Name UserConfigProvider*,TestLogger1 -ModuleName UserConfigProv,PsModuleForTestLogger
> ```

Co je třeba zvážit při použití pouze název parametru:

- Je náročná operace v závislosti na počet modulů na počítači nainstalovaný.
- Načte první prostředek nenašel se zadaným názvem. V případě níž se nachází více než jeden prostředek se stejným názvem nainstalovaná, může načtení nesprávné prostředků.

Doporučuje se určit `–ModuleName` s `-Name` parametru, jak je popsáno níže.

Toto použití má následující výhody:

- Snižuje dopad na výkon tím, že omezíte rozsah vyhledávání pro zadaný prostředek.
- Definuje explicitně modulu definice prostředků, zajistit, že je načten správný zdroj.

> [!NOTE]
> V Powershellu 5.0 prostředky DSC můžete mít více verzí a verzí lze nainstalovat počítač-souběžně. Toto je implementováno s více verzí modulu prostředků, které jsou obsaženy ve stejné složce modulu.
> Další informace najdete v tématu [pomocí různých verzí prostředků](sxsresource.md).

## <a name="intellisense-with-import-dscresource"></a>Technologie IntelliSense s Import-DSCResource

Při vytváření konfigurace DSC v prostředí ISE Powershellu zajišťující IntelliSence prostředků a vlastnosti prostředků. Definice prostředků v rámci `$pshome` cesta modulu jsou načteny automaticky. Při importu prostředků pomocí `Import-DSCResource` – klíčové slovo, se přidají definice zadaný prostředek a technologie Intellisense je rozbalený se zahrnout schéma importovaných zdrojů.

![Technologie Intellisense prostředků](/media/resource-intellisense.png)

> [!NOTE]
> Od v Powershellu 5.0, tab k dokončování příkazů byl přidán do ISE pro prostředky DSC a jejich vlastnosti. Další informace najdete v tématu [prostředky](../resources/resources.md).

Při kompilaci konfigurace Powershellu definice importovaných zdrojů používá k ověření všechny bloky prostředků v konfiguraci.
Každý blok prostředků se ověří pomocí prostředku schématu definice pro následující pravidla.

- Pouze vlastnosti definované ve schématu se používají.
- Datové typy pro každou vlastnost jsou správné.
- Nejsou zadány vlastnosti klíče.
- Žádná vlastnost jen pro čtení se používá.
- Ověřování na hodnotě mapuje typy.

Vezměte v úvahu následující konfiguraci:

```powershell
Configuration SchemaValidationInCorrectEnumValue
{
    # It is best practice to explicitly import all resources used in your Configuration.
    # This includes resources that are imported automatically, like WindowsFeature.
    Import-DSCResource -Name WindowsFeature
    Node localhost
    {
        WindowsFeature ROLE1
        {
            Name = “Telnet-Client”
            Ensure = “Invalid”
        }
    }
}
```

Tato konfigurace způsobí chybu kompilace.

```output
PSDesiredStateConfiguration\WindowsFeature: At least one of the values ‘Invalid’ is not supported or valid for property ‘Ensure’ on class ‘WindowsFeature’. Please specify only supported values: Present, Absent.
```

Technologie IntelliSense a schéma ověřování umožňuje zachytit další chyby při analýze a kompilaci zabránit komplikacím v době běhu.

> [!NOTE]
> Jednotlivé prostředky DSC můžete mít název a **FriendlyName** definovaná pomocí schématu prostředku. Níže jsou první dva řádky "MSFT_ServiceResource.shema.mof".
> ```syntax
> [ClassVersion("1.0.0"),FriendlyName("Service")]
> class MSFT_ServiceResource : OMI_BaseResource
> ```
> Při použití tohoto prostředku v konfiguraci, můžete zadat **MSFT_ServiceResource** nebo **služby**.

## <a name="powershell-v4-and-v5-differences"></a>Rozdíly v4, tak i v5 prostředí PowerShell

Existuje několik rozdílů, které se zobrazí při vytváření konfigurace v Powershellu 4.0 vs. PowerShell 5.0 nebo novější. V této části budou zvýrazněny rozdíly, že se zobrazí relevantní k tomuto článku.

### <a name="multiple-resource-versions"></a>Více verzí prostředků

Instalace a použití více verzí prostředků vedle sebe nebyla podporovaná v Powershellu 4.0. Pokud si všimnete problémů při importu zdrojů do vaší konfigurace, ujistěte se, že máte jenom jedna verze prostředku nainstalované.

Na obrázku níže, dvě verze **xPSDesiredStateConfiguration** modulu jsou nainstalovány.

![Více verzí prostředků opraveno](/media/multiple-resource-versions-broken.md)

Na nejvyšší úrovni adresáře modulů zkopírujte obsah vaší verze požadovaný modul.

![Více verzí prostředků opraveno](/media/multiple-resource-versions-fixed.md)

### <a name="resource-location"></a>Umístění prostředku

Při vytváření obsahu a kompilace konfigurací, vaše prostředky mohou být uloženy v libovolném adresáři určeném vaše [PSModulePath](/powershell/developer/module/modifying-the-psmodulepath-installation-path). LCM v Powershellu 4.0, vyžaduje všechny moduly prostředků DSC mají být uloženy v části "Program Files\WindowsPowerShell\Modules" nebo `$pshome\Modules`. Od v Powershellu 5.0, byl odebrán tento požadavek a moduly prostředků mohou být uloženy v libovolném adresáři určeném `PSModulePath`.

## <a name="see-also"></a>Viz taky

- [Prostředky](../resources/resources.md)
