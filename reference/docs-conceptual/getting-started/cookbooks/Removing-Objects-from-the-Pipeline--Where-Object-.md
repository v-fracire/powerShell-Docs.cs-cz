---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Odebírání objektů z kanálu kde objektu"
ms.assetid: 01df8b22-2d22-4e2c-a18d-c004cd3cc284
ms.openlocfilehash: 4140c4c3ebb26223d03ca139992fedf6e184a38b
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/03/2017
---
# <a name="removing-objects-from-the-pipeline-where-object"></a>Odebírání objektů z kanálu (Where-Object)
V prostředí Windows PowerShell často generovat a další objekty předají pro kanál, než má. Můžete zadat vlastnosti konkrétní objekty, které chcete zobrazit pomocí **formát** rutiny, ale nepomůže s problémem odebrání celé objekty ze zobrazení. Můžete filtrovat objekty před koncem kanálu, tak můžete provádět akce na pouze podmnožinu objektů původně vytvořil.

Prostředí Windows PowerShell zahrnuje **Where-Object** rutinu, která umožňuje testování jednotlivých objektů v kanálu a pouze předat podél kanálu pokud splňuje podmínku konkrétní test. Objekty, které se nepředají test se odeberou z kanálu. Zadejte podmínky testu jako hodnota **kde ObjectFilterScript** parametr.

### <a name="performing-simple-tests-with-where-object"></a>Provádění jednoduchých testů s Where-Object
Hodnota **FilterScript** je *bloku skriptu* – jeden nebo více příkazů prostředí Windows PowerShell obklopená složených závorek {} –, která vyhodnotí jako true nebo false. Tyto bloky skriptu může být velmi jednoduchý, ale jejich vytváření vyžaduje znalost o jiný koncept prostředí Windows PowerShell, operátory porovnání. Relační operátor porovnání položek, které se zobrazí na každé straně ho. Operátory porovnání začínat '-' znak a jsou následuje název. Operátory porovnání základní fungovat na téměř k libovolnému druhu objektu. Pokročilejší operátory porovnání může fungovat jenom na text nebo pole.

> [!NOTE]
> Operátory porovnání prostředí Windows PowerShell jsou ve výchozím nastavení se při práci s textem velká a malá písmena.

Z důvodu analýzy aspekty symboly, například <>, a = nejsou používány jako relační operátory. Operátory porovnání místo toho se skládají z písmena. V následující tabulce jsou uvedeny základní relační operátory.

|Relační operátor|Význam|Příklad (vrací hodnotu true)|
|-----------------------|-----------|--------------------------|
|-eq|je rovno|1 - eq 1|
|-ne|Není rovno|1 – ne 2|
|-lt|Je menší než|1 - lt 2|
|-le|Je menší než nebo rovno|1 - le 2|
|-gt|Je větší než|2 - gt 1|
|-ge|Je větší než nebo rovno|2 -ge 1|
|-jako|Je třeba (porovnání zástupný text)|"soubor.doc"-jako "f\*.používat?"|
|-notlike|Není třeba (porovnání zástupný text)|"soubor.doc"-notlike "p\*.doc"|
|-obsahuje|Obsahuje|1,2,3 – obsahuje 1|
|-notcontains|Neobsahuje|1,2,3 - notcontains 4|

WHERE-Object blocích skriptu použít speciální proměnná ($_)' k odkazování na aktuální objekt v kanálu. Tady je příklad toho, jak funguje. Pokud máte seznam čísel a chcete pouze vrátit ty, které jsou menší než 3, můžete filtrovat čísla zadáním Where-Object:

```
PS> 1,2,3,4 | Where-Object -FilterScript {$_ -lt 3}
1
2
```

### <a name="filtering-based-on-object-properties"></a>Filtrování podle vlastnosti objektu
Vzhledem k tomu, že $_ odkazuje na aktuální objekt kanálu, jsme pro naše testy otevřete jeho vlastnosti.

Jako příklad může podíváme na třídě Win32_SystemDriver v rozhraní WMI. Může být stovky ovladače systému na konkrétní systém, ale pouze může být zájem o konkrétní sadu ovladačů systému, jako jsou ty, které jsou aktuálně spuštěné. Pokud chcete zobrazit členy Win32_SystemDriver použít Get-člen (**Get-WmiObject – Třída Win32_SystemDriver | Vlastnost Get-Member - MemberType**) uvidíte, že je odpovídající vlastnost stavu a jeho má hodnotu "Spuštěný", když běží ovladače. Můžete filtrovat ovladače systému výběr jenom spuštěné ty zadáním:

```
Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript {$_.State -eq "Running"}
```

To vytváří ještě dlouhý seznam. Chcete filtrovat, aby pouze vyberte ovladače nastavená na automatické spouštění testování hodnotě StartMode:

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

To nám dává velké množství informací, které již nepotřebujete, protože víme, že jsou spuštěny ovladače. Ve skutečnosti jenom informace, které pravděpodobně potřebujeme v tomto okamžiku jsou název a zobrazovaný název. Následující příkaz obsahuje pouze tyto dvě vlastnosti, což vede k mnohem jednodušší výstup:

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

Existují dva elementy Where-Object ve výše uvedeném příkazu, ale mohou být vyjádřeny v jednom elementu Where-Object pomocí- a logickým operátorem takto:

```
Get-WmiObject -Class Win32_SystemDriver | Where-Object -FilterScript { ($_.State -eq "Running") -and ($_.StartMode -eq "Manual") } | Format-Table -Property Name,DisplayName
```

Standardní logické operátory jsou uvedeny v následující tabulce.

|Logický operátor|Význam|Příklad (vrací hodnotu true)|
|--------------------|-----------|--------------------------|
|- a|Logické a; Hodnota TRUE, pokud jsou splněny obě strany|(1 - eq 1) - a (2 - eq 2).|
|- nebo|Logické nebo; Hodnota TRUE, pokud má jedna strana hodnotu true|(1 - eq 1) - nebo (1 - eq 2).|
|-není|Logický operátor not; obrátí hodnotu true a false|-není (1 - eq 2)|
|\!|Logický operátor not; obrátí hodnotu true a false|\!(1 - eq 2)|

