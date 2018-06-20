---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: DSC pro Linux nxFile prostředků
ms.openlocfilehash: f1eb98092049ae837d144ccf99a84fe5614144e0
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
ms.locfileid: "34189852"
---
# <a name="dsc-for-linux-nxfile-resource"></a>DSC pro Linux nxFile prostředků

**NxFile** prostředků v prostředí PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus pro ke správě souborů a adresářů v uzlu systému Linux.

## <a name="syntax"></a>Syntaxe

```
nxFile <string> #ResourceName
{
    DestinationPath = <string>
    [ SourcePath = <string> ]
    [ Ensure = <string> { Absent | Present }  ]
    [ Type = <string> { directory | file | link } ]
    [ Contents = <string> ]
    [ Checksum = <string> { ctime | mtime | md5 }  ]
    [ Recurse = <bool> ]
    [ Force = <bool> ]
    [ Links = <string> { follow | manage } ]
    [ Group = <string> ]
    [ Mode = <string> ]
    [ Owner = <string> ]
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a>Properties

|  Vlastnost |  Popis |
|---|---|
| Cílová_cesta| Určuje umístění, kde chcete zajistit stav pro soubor nebo adresář.|
| SourcePath| Určuje cestu, ze kterého chcete kopírovat prostředek souboru nebo složky. Tato cesta může být místní cesta nebo `http/https/ftp` adresy URL. Vzdálené `http/https/ftp` adresy URL jsou pouze podporovaná, až hodnotu **typ** vlastnost je soubor.|
| Ujistěte se| Určuje, jestli se má zkontrolovat, zda soubor existuje. Nastavte tuto vlastnost k dispozici"" zajistit, že soubor existuje. Nastavte ji na "Chybí" zajistěte, aby byl že soubor neexistuje. Výchozí hodnota je "Dispozici".|
| Typ| Určuje, zda je nakonfigurován prostředek adresář nebo soubor. Nastavením této vlastnosti "adresář" označuje, že prostředek adresáře. Nastavte tak, aby "soubor" k označení, že je prostředek soubor. Výchozí hodnota je "soubor"|
| Obsah| Určuje obsah souboru, například konkrétní řetězec.|
| Kontrolní součet| Definuje typ, který má použít při určování, zda dva soubory jsou stejné. Pokud **kontrolního součtu** není zadán, pro porovnání se používá pouze název souboru nebo adresáře. Hodnoty: "ctime", "mtime" nebo "md5".|
| Recurse| Uvádí, jestli jsou zahrnuté podadresářů. Tuto vlastnost nastavit na **$true** k označení, že chcete podadresáře, které mají být zahrnuty. Výchozí hodnota je **$false**. **Poznámka:** tato vlastnost je platná pouze když **typu** je nastavena na adresář.|
| Force| Některé operace souboru (například přepsání souboru nebo odstranění adresáře, který není prázdný) bude výsledkem chyba. Pomocí **Force** vlastnost má přednost před takové chyby. Výchozí hodnota je **$false**.|
| Odkazy| Určuje požadované chování pro symbolické odkazy. Nastavením této vlastnosti "následovat" a postupujte podle symbolické odkazy fungují na cíli odkazy (např. Zkopírujte soubor místo odkazu). Nastavením této vlastnosti "manage" tak, aby fungoval na odkaz (například) Zkopírujte odkaz sám sebe). Nastavte tuto vlastnost "Ignorovat" Ignorovat symbolické odkazy.|
| Skupina| Název **skupiny** udělil soubor nebo adresář.|
| Režim| Určuje požadované oprávnění pro prostředek, notaci osmičková nebo symbolické. (například 777 nebo rwxrwxrwx). Pokud používáte symbolický zápis, neposkytují prvního znaku, který označuje adresář nebo soubor.|
| dependsOn | Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Například pokud **ID** prostředku blok skriptu konfigurace, který chcete spustit nejprve je **ResourceName** a její typ je **ResourceType**, pomocí této syntaxe Vlastnost je `DependsOn = "[ResourceType]ResourceName"`.|

## <a name="additional-information"></a>Další informace


Linux a Windows pomocí znaky konce řádku různých v textových souborů ve výchozím nastavení, a to může vést k neočekávaným výsledkům při konfiguraci některé soubory na počítač se systémem Linux s __nxFile__. Spravovat obsah souboru Linux při vyloučení problémů způsobených znaky konce řádku neočekávané několika způsoby:

Krok 1: Kopírování souboru ze vzdáleného zdroje (http, https nebo ftp): Vytvořte soubor v systému Linux s požadovaný obsah a příprava na web nebo ftp serveru přístupné uzly budete konfigurovat. Definování __SourcePath__ vlastnost __nxFile__ prostředek s web nebo ftp adresu URL k souboru.

```
Import-DSCResource -Module nx
Node $Node
{
nxFile resolvConf
{
    SourcePath = "http://10.185.85.11/conf/resolv.conf"
    DestinationPath = "/etc/resolv.conf"
    Mode = "644"
    Type = "file"

}

}
```


Krok 2: Přečtěte si obsah souboru ve skriptu prostředí PowerShell s [Get-Content](https://technet.microsoft.com/library/hh849787.aspx) po nastavení __$OFS__ vlastnost použít znak Linux konec řádku.


```
Import-DSCResource -Module nx
Node $Node
{
$OFS = "`n"
$Contents = Get-Content C:\temp\resolv.conf

nxFile resolvConf
{
    DestinationPath = "/etc/resolv.conf"
    Mode = "644"
    Type = "file"
    Contents = "$Contents"
}

}
```


Krok 3: Použití funkce prostředí PowerShell nahradit konce řádků Windows znaky konce řádku Linux.

```
Function LinuxString($inputStr){
    $outputStr = $inputStr.Replace("`r`n","`n")
    $ouputStr += "`n"
    Return $outputStr
}

Import-DSCResource -Module nx
Node $Node
{

$Contents = @'
search contoso.com
domain contoso.com
nameserver 10.185.85.11
'@

$Contents = LinuxString $Contents

nxFile resolvConf
{
    DestinationPath = "/etc/resolv.conf"
    Mode = "644"
    Type = "file"
    Contents = $Contents

}
}
```

## <a name="example"></a>Příklad

Následující příklad zajišťuje, že adresář `/opt/mydir` existuje, a zda existuje soubor s zadaný obsah tohoto adresáře.

```
Import-DSCResource -Module nx

Node $node {
nxFile DirectoryExample
{
   Ensure = "Present"
   DestinationPath = "/opt/mydir"
   Type = "Directory"
}

nxFile FileExample
{
    Ensure = "Present"
    Destinationpath = "/opt/mydir/myfile"
    Contents=@"
#!/bin/bash`necho "hello world"`n
"@
    Mode = “755”
    DependsOn = "[nxFile]DirectoryExample"
}
}
```