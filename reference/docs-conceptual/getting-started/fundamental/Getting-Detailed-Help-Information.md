---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Získání podrobné nápovědy
ms.assetid: 6fb4daf7-8607-4a3e-b692-f77631adc1b9
ms.openlocfilehash: 29c24af3f688f9388893044952442910e793842d
ms.sourcegitcommit: 01d6985ed190a222e9da1da41596f524f607a5bc
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/07/2018
ms.locfileid: "34483028"
---
# <a name="getting-detailed-help-information"></a>Získání podrobné nápovědy
Prostředí Windows PowerShell obsahuje podrobné témata nápovědy, které vysvětlují koncepty prostředí Windows PowerShell a jazyk prostředí Windows PowerShell. Existují také témata nápovědy pro každou rutiny a zprostředkovatele a témata nápovědy pro mnoho funkcí a skriptů.

Můžete zobrazit tato témata nápovědy na příkazovém řádku nebo zobrazit nedávno aktualizované verze těchto témat v Microsoft TechNet Library. Mnoho programy, které hostí prostředí Windows PowerShell, jako je Windows Integrované skriptovací prostředí PowerShell, zadejte další pomoc funkce, jako je kontextová nápověda a zkompilovaný soubor nápovědy (CHM.).

## <a name="getting-help-for-cmdlets"></a>Získání nápovědy k rutinám
Chcete-li získat nápovědu o rutinách prostředí Windows PowerShell, použijte [Get-Help [m2]](https://technet.microsoft.com/library/2d7fe1b4-0025-4580-a911-d81922dd6cd2) rutiny. Například pro získání nápovědy pro [Get-ChildItem [m2]](https://technet.microsoft.com/library/4b270d63-c995-45b8-b5b4-3f8887efbfcc) rutiny, zadejte:

```
get-help get-childitem
```

nebo

```
get-childitem -?
```

Dokonce můžete získat nápovědu o rutinu Get-Help. Příklad:

```
get-help get-help
```

Pokud chcete získat seznam všech témat nápovědy rutinu v relaci, zadejte:

```
get-help -category cmdlet
```

Chcete-li zobrazit jednu stránku každého tématu nápovědy v čase, použijte **pomoci** funkce nebo jeho alias **man**. Například pokud chcete zobrazit nápovědu pro rutinu Get-ChildItem, zadejte

```
man get-childitem
```

nebo

```
help get-childitem
```

Chcete-li zobrazit podrobné informace o rutiny, funkce nebo skriptu, včetně popisu jeho parametry a příkladů jeho použití, použijte *podrobné* parametru rutiny Get-Help. Chcete-li získat podrobné informace o rutině Get-ChildItem, zadejte například:

```
get-help get-childitem -detailed
```

Chcete-li zobrazit veškerý obsah v tématu nápovědy, použijte *úplné* parametru rutiny Get-Help. Například pokud chcete zobrazit veškerý obsah v tématu nápovědy pro rutinu Get-ChildItem, zadejte:

```
get-help get-childitem -full
```

Chcete-li získat podrobnou nápovědu k parametry rutiny, použijte *parametr* parametru rutiny Get-Help. Například získat podrobné nápovědy pro všechny parametry rutiny Get-ChildItem, zadejte:

```
get-help get-childitem -parameter *
```

Chcete-li zobrazit pouze v příkladech v tématu nápovědy, použijte *příklad* parametr Get-Help. Například pokud chcete zobrazit jenom příklady v tématu nápovědy pro rutinu Get-ChildItem, zadejte:

```
get-help get-childitem -examples
```

Informace o tom, jak psát témata nápovědy k rutinám, které můžete psát najdete v tématu [postup nápovědě k rutině zápisu](https://go.microsoft.com/fwlink/?LinkID=123415) v knihovně MSDN.

## <a name="getting-conceptual-help"></a>Koncepční nápovědy
Rutinu Get-Help také zobrazí informace o koncepční témata v prostředí Windows PowerShell, včetně témata týkající se jazyka prostředí Windows PowerShell. Koncepční témata nápovědy začínat předponu "about_", jako je například about_line_editing. (Název koncepční téma je třeba zadat v angličtině i na jiných než anglických verzí prostředí Windows PowerShell.)

Chcete-li zobrazit seznam koncepční témata, zadejte:

```
get-help about_*
```

Pokud chcete zobrazit na určité téma nápovědy, zadejte například název tématu:

```
get-help about_command_syntax
```

Parametry Get-Help, jako například *podrobné*, *parametr*, a *příklady*, nemají vliv na zobrazení koncepční témata nápovědy.

## <a name="getting-help-about-providers"></a>Získání nápovědy o zprostředkovatelích
Rutina Get-Help zobrazí informace o poskytovatelích prostředí Windows PowerShell. Chcete-li získat nápovědu pro zprostředkovatele, zadejte "Get-Help" následuje název zprostředkovatele. Například chcete-li získat nápovědu pro zprostředkovatele registru, zadejte:

```
get-help registry
```

Chcete-li získat seznam všech témat nápovědy zprostředkovatele v relaci, zadejte

```
get-help -category provider
```

Parametry Get-Help, jako například *podrobné*, *parametr*, a *příklady*, nemají vliv na zobrazení témat nápovědy zprostředkovatele.

## <a name="getting-help-about-scripts-and-functions"></a>Získání nápovědy o skriptech a funkcích
Mnoho funkcí v prostředí Windows PowerShell a skriptů mít témata nápovědy. Použijte rutinu Get-Help zobrazíte témata nápovědy pro skriptech a funkcích.

Pokud chcete zobrazit nápovědu pro funkci, zadejte "get-help" následuje název funkce. Například pro získání nápovědy pro funkce Disable-PSRemoting, zadejte:

```
get-help disable-psremoting
```

Chcete-li zobrazit nápovědu pro skript, zadejte plně kvalifikovanou cestu k souboru skriptu. Pokud se skript v cestě, která je uvedena v proměnné prostředí Path, můžete vynechat cestu z příkazu.

Pokud máte skript s názvem "TestScript.ps1" v jednotce C:, například\\directory PS testu chcete zobrazit téma nápovědy pro skript, typ:

```
get-help c:\ps-test\TestScript.ps1
```

Parametry, které byly navrženy pro zobrazení rutiny pomoci, jako například *podrobné*, *úplné*, *příklady*, a *parametr*, pracovní pro skript nápovědy a funkce Nápověda, příliš. Ale když zobrazit všechny nápovědu zadáním "get-help \*", Nápověda pro funkce a skripty se nezobrazí.

Informace o vytváření témata nápovědy pro funkce a skripty, najdete v tématu [about_Functions [m2]](https://technet.microsoft.com/library/61d40692-5300-4de9-a9b5-bae31815e105), [about_Scripts](https://technet.microsoft.com/library/7dc08334-dcfe-450b-b949-0554855623af), a [about_Comment_Based_Help](https://technet.microsoft.com/library/99a81ccc-21a0-49ec-a1b3-9efe2b4c0bbf).

## <a name="getting-help-online"></a>Online nápovědy
Pokud jste připojeni k Internetu, je jedním z nejlepší způsoby, jak získat nápovědu zobrazte témata nápovědy online. Protože online téma se dají snadno aktualizovat, jsou může zajistit nejaktuálnější obsah.

Chcete-li získat online nápovědu, zkuste *Online* parametru rutiny Get-Help. *Online* parametr funguje rutiny Get-Help jenom pro rutinu nápovědy, funkce nápovědy a skriptu nápovědy. Nelze použít *Online* parametr s koncepční (o) témata nebo témata nápovědy zprostředkovatele. Navíc vzhledem k tomu, že tato funkce je volitelný, ale nefunguje pro všechny rutiny, funkce nebo téma nápovědy skriptu.

Ale všechna témata nápovědy pocházející pomocí prostředí Windows PowerShell, včetně zprostředkovatele nápovědy a koncepční (témata nápovědy o) jsou k dispozici online v [prostředí Windows PowerShell](http://go.microsoft.com/fwlink/?LinkID=107116) části Microsoft TechNet Library.

Použít *Online* parametru rutiny Get-Help, použijte následující příkaz Formát.

```
get-help <command-name> -online
```

Například získat online verzi tématu nápovědy o rutinu Get-ChildItem, zadejte:

```
get-help get-childitem -online
```

Pokud je k dispozici online verzi tématu nápovědy, otevře se ve výchozím prohlížeči.

Pokud online nápovědy je podporováno pro téma nápovědy, můžete také zobrazit internetové adresy (URL) tématu nápovědy. Internetové adresy se zobrazí v části tématu nápovědy související odkazy.

Například najdete v části Adresa URL pro online verzi rutinu Add-Computer, zadejte:

```
get-help add-computer
```

V prvním řádku související odkazy části tohoto tématu jsou uvedeny níže.

```
Online version: http://go.microsoft.com/fwlink/?LinkID=135194
```

Informace o tom, jak poskytnout online podpory společnosti Microsoft pro vaše témata nápovědy najdete v tématu [about_Comment_Based_Help](https://technet.microsoft.com/library/99a81ccc-21a0-49ec-a1b3-9efe2b4c0bbf)a zobrazit [postup nápovědě k rutině zápisu](https://go.microsoft.com/fwlink/?LinkID=123415) v knihovně MSDN.

## <a name="see-also"></a>Viz také
- [about_Functions [m2]](https://technet.microsoft.com/library/61d40692-5300-4de9-a9b5-bae31815e105)
- [about_Scripts](https://technet.microsoft.com/library/7dc08334-dcfe-450b-b949-0554855623af)
- [about_Comment_Based_Help](https://technet.microsoft.com/library/99a81ccc-21a0-49ec-a1b3-9efe2b4c0bbf)
- [Get-Help [m2]](https://technet.microsoft.com/library/2d7fe1b4-0025-4580-a911-d81922dd6cd2)