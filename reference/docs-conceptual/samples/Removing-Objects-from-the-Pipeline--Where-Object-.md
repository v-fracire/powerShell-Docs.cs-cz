---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Odebrání objektů z kanálu Where-Object
ms.assetid: 01df8b22-2d22-4e2c-a18d-c004cd3cc284
ms.openlocfilehash: c060b93a3823be26ad6c7757acc633bb4fc2fcfa
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404059"
---
# <a name="removing-objects-from-the-pipeline-where-object"></a>Odebrání objektů z kanálu (Where-Object)

V prostředí Windows PowerShell často generovat a předali více objektů do kanálu, než se. Můžete zadat vlastnosti konkrétní objekty zobrazíte pomocí **formátu** rutiny, ale to nepomůže s problémem, který odebrat celé objekty ze zobrazení. Můžete filtrovat objekty do konce profilace, abyste mohli provádět akce s pouze podmnožinu původně vytvořil objekty.

Obsahuje prostředí Windows PowerShell `Where-Object` rutinu, která umožňuje testování jednotlivých objektů v kanálu a pouze předat podél kanálu pokud splňuje podmínku určitého testu. Objekty, které nepředávejte testu se odeberou z kanálu. Jako hodnotu zadáte testovací podmínku `Where-Object` **FilterScript** parametru.

### <a name="performing-simple-tests-with-where-object"></a>Provedením jednoduchých testů s Where-Object

Hodnota **FilterScript** je *bloku skriptu* – jeden nebo více příkazů prostředí Windows PowerShell, které jsou uzavřeny ve složených závorkách {} –, který se vyhodnotí na hodnotu true nebo false. Tyto bloky skriptu může být velmi jednoduchý, ale vytváří, je nutné, abyste znali o jiné koncept prostředí Windows PowerShell, operátory porovnání. Operátor porovnání porovná položky, které se zobrazí na každé straně. Operátory porovnání začínat "-" znaků a jsou následována název. Operátory porovnání základní pracovat na téměř jakýkoli druh objektu. Rozšířené operátory porovnání může fungovat jenom na text nebo pole.

> [!NOTE]
> Ve výchozím nastavení se při práci s textem operátory porovnání prostředí Windows PowerShell jsou malá a velká písmena.

Z důvodu důležité informace o analýze, symboly, jako je například <>, a = nejsou používány jako operátory porovnání. Místo toho operátory porovnání se skládají z písmen. Základní porovnávací operátory jsou uvedeny v následující tabulce.

|Operátor porovnání|Význam|Příklad (vrátí hodnotu true)|
|-----------------------|-----------|--------------------------|
|-eq|je rovno|1 - eq 1|
|-ne|Není rovno|1 - ne 2|
|-lt|je menší než|1 - lt 2|
|-le.|Je menší než nebo rovno|1 - le 2|
|-gt|je větší než|2 - gt 1|
|-ge|Je větší než nebo rovno|2 -ge 1|
|– například|Je třeba (porovnání zástupný text)|"soubor.doc"-jako "f\*.používat?"|
|-notlike|Není podobné (porovnání zástupný text)|"soubor.doc"-notlike "p\*doc"|
|-obsahuje|obsahuje|1,2,3 – obsahuje 1|
|-notcontains|neobsahuje|1,2,3 - notcontains 4|

Bloky skriptu Where-Object používat speciální proměnné `$_` pro odkazování na aktuální objekt v kanálu. Tady je příklad toho, jak funguje. Pokud máte seznam čísel a pouze chcete vrátit těch, které jsou kratší než 3, můžete filtrovat tak, že zadáte čísla Where-Object:

```
PS> 1,2,3,4 | Where-Object -FilterScript {$_ -lt 3}
1
2
```

### <a name="filtering-based-on-object-properties"></a>Filtrování podle vlastností objektu

Protože `$_` odkazuje na aktuální objekt kanálu jsme můžete získat přístup k vlastnostem pro naše testy.

Jako příklad abychom se mohli podívat na Win32_SystemDriver třídu v rozhraní WMI. Může být stovky ovladače systému na konkrétní systém, ale pouze byste měli zájem konkrétní sadu ovladačů systému, jako jsou ty, které jsou aktuálně spuštěny. Pokud používáte k zobrazení členů Win32_SystemDriver Get-Member (**Get-WmiObject – Třída Win32_SystemDriver | Vlastnost Get-Member - MemberType**) uvidíte, že je odpovídající vlastnost stavu, a aby měla hodnotu "Spustit" při spuštění ovladače. Můžete filtrovat ovladače systému vyberete pouze spuštěné ty zadáním:

```powershell
Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript {$_.State -eq 'Running'}
```

To vytváří ještě dlouhý seznam. Můžete chtít filtrovat jenom vybraným nastavená na automatické spouštění otestováním hodnotu StartMode ovladače:

```
PS> Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript {$_.State -eq "Running"} | Where-Object -FilterScript {$_.StartMode -eq "Auto"}

DisplayName : RAS Asynchronous Media Driver
Name        : AsyncMac
State       : Running
Status      : OK
Started     : True

DisplayName : Audio Stub Driver
Name        : audstub
State       : Running
Status      : OK
Started     : True
```

Tento produkt nám nabízí velké množství informací, které už nepotřebujete, protože víme, že jsou spuštěny ovladače. Ve skutečnosti pouze informace, které pravděpodobně potřebujeme v tomto okamžiku jsou název a zobrazovaný název. Následující příkaz zahrnuje pouze tyto dvě vlastnosti, což vede k mnohem jednodušší výstup:

```
PS> Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript {$_.State -eq "Running"} | Where-Object -FilterScript {$_.StartMode -eq "Manual"} | Format-Table -Property Name,DisplayName

Name                                    DisplayName
----                                    -----------
AsyncMac                                RAS Asynchronous Media Driver
Fdc                                     Floppy Disk Controller Driver
Flpydisk                                Floppy Disk Driver
Gpc                                     Generic Packet Classifier
IpNat                                   IP Network Address Translator
mouhid                                  Mouse HID Driver
MRxDAV                                  WebDav Client Redirector
mssmbios                                Microsoft System Management BIOS Driver
```

Existují dva prvky Where-Object v předchozím příkazu, ale dají se vyjádřit v jednom elementu Where-Object s použitím- a logický operátor, následujícím způsobem:

```powershell
Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript { ($_.State -eq 'Running') -and ($_.StartMode -eq 'Manual') } | Format-Table -Property Name,DisplayName
```

Standardní logické operátory jsou uvedeny v následující tabulce.

|Logický operátor|Význam|Příklad (vrátí hodnotu true)|
|--------------------|-----------|--------------------------|
|- a|Logické a; Hodnota TRUE, pokud jsou splněny obě strany|(1 - eq 1) - a (2 - eq 2).|
|- nebo|Logická nebo; Hodnota TRUE, pokud obě strany hodnotu true|(1 - eq 1) - nebo (1 - eq 2).|
|– Ne|Logický operátor not; Vrátí hodnotu true a false|-není (1 - eq 2)|
|\!|Logický operátor not; Vrátí hodnotu true a false|\!(1 - eq 2)|
