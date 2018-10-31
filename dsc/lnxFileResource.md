---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: DSC pro Linux prostředek nxFile
ms.openlocfilehash: 80969ba2ea6247fcd616a301d951403a840c851d
ms.sourcegitcommit: e76665315fd928bf85210778f1fea2be15264fea
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/30/2018
ms.locfileid: "50225705"
---
# <a name="dsc-for-linux-nxfile-resource"></a>DSC pro Linux prostředek nxFile

**NxFile** prostředků v prostředí PowerShell Desired State Configuration (DSC) poskytuje mechanismus ke správě soubory a adresáře na uzlu systému Linux.

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
| DestinationPath| Určuje umístění, kam chcete zajistit stavu pro soubor nebo adresář.|
| SourcePath| Určuje cestu, ze kterého chcete kopírovat zdroje souboru nebo složky. Tento způsob může být místní cesta nebo `http/https/ftp` adresy URL. Vzdálené `http/https/ftp` adresy URL jsou pouze podporovaná, až hodnotu **typ** vlastností je soubor.|
| Zkontrolujte| Určuje, jestli se má zkontrolovat, zda soubor existuje. Nastavte tuto vlastnost na "Obsahuje" Ujistěte se, že soubor existuje. Nastavte ho na "Chybí" Ujistěte se, že soubor neexistuje. Výchozí hodnota je "K dispozici".|
| Typ| Určuje, zda je adresář nebo soubor prostředků, která se právě nastavuje. Nastavte tuto vlastnost na "directory" k označení, že je prostředek adresáře. Nastavte na "file" označuje, že soubor prostředku. Výchozí hodnota je "file"|
| Obsah| Určuje obsah souboru, jako je například konkrétní řetězec.|
| Kontrolní součet| Definuje typ, který má použít při určování, zda dva soubory jsou stejné. Pokud **kontrolního součtu** není zadán, pouze název souboru nebo složky se používá pro porovnání. Hodnoty jsou: "ctime", "mtime" nebo "md5".|
| Recurse| Uvádí, jestli jsou zahrnuté podadresářů. Tuto vlastnost nastavte na **$true** k označení, že chcete, aby podadresářů, které mají být zahrnuty. Výchozí hodnota je **$false**. **Poznámka:** tato vlastnost je platná pouze při **typ** je nastavena na adresář.|
| Force| Určité operace se soubory (například soubor přepsání nebo odstranění adresáře, který není prázdný) dojde chybě. Použití **platnost** vlastnost potlačuje tyto chyby. Výchozí hodnota je **$false**.|
| Odkazy| Určuje požadované chování pro symbolické odkazy. Nastavte tuto vlastnost na "sledovat" sledovat symbolické odkazy a reagovat na cílové odkazy (např. Zkopírujte soubor místo odkazu). Nastavte tuto vlastnost na "manage" tak, aby fungoval na odkaz (např. Zkopírujte odkaz pro samotné). Nastavte tuto vlastnost na "Ignorovat" pro ignorování symbolické odkazy.|
| Skupina| Název **skupiny** vlastnictví souboru nebo adresáře.|
| Režim| Určuje požadované oprávnění pro prostředek, v symbolické nebo osmičkové soustavě. (například 777 nebo rwxrwxrwx). Používáte-li symbolický zápisu, se neposkytuje prvního znaku, který označuje adresář nebo soubor.|
| DependsOn | Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován. Například pokud **ID** prostředku bloku skriptu konfigurace, který chcete spustit nejdřív ale **ResourceName** a jejím typem je **ResourceType**, syntaxe pro použití této funkce Vlastnost je `DependsOn = "[ResourceType]ResourceName"`.|

## <a name="additional-information"></a>Další informace


Operačních systémů Linux a Windows pomocí znaky konce řádku různých v textových souborech ve výchozím nastavení, a to může způsobit neočekávané výsledky při konfiguraci některé soubory na počítači s Linuxem pomocí __nxFile__. Správa obsahu Linuxový soubor při obcházení potíže způsobené službou znaky konců řádků neočekávané několika způsoby:

Krok 1: Zkopírujte soubor ze vzdáleného zdroje (http, https nebo ftp): Vytvořte soubor v Linuxu se požadovaný obsah a jejich přípravy na web nebo ftp server přístupné uzly, které budete konfigurovat. Definovat __SourcePath__ vlastnost __nxFile__ prostředků s adresou URL webu nebo ftp do souboru.

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


Krok 2: Přečtěte si obsah souboru v skriptu prostředí PowerShell pomocí [Get-Content](https://technet.microsoft.com/library/hh849787.aspx) po nastavení __$OFS__ vlastnost pomocí znaku konce řádku Linux.


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


Krok 3: Použití funkce prostředí PowerShell k nahraďte Linux oddělených koncem řádku znaky konce řádku Windows.

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

Následující příklad zajistí, že adresář `/opt/mydir` existuje, a jestli existuje soubor se zadaným obsah tohoto adresáře.

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