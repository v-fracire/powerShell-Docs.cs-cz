---
ms.date: 08/27/2018
keywords: rutiny prostředí PowerShell
title: Získání podrobné nápovědy
ms.assetid: 6fb4daf7-8607-4a3e-b692-f77631adc1b9
ms.openlocfilehash: 8b56f003fdef38b0f126cfe82eefcc145cc54783
ms.sourcegitcommit: 3402a478cf118c11a5642038eb117bc76553e3ab
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53411595"
---
# <a name="getting-detailed-help-information"></a>Získání podrobné nápovědy

PowerShell zahrnuje podrobné články nápovědy, které vysvětluje koncepty prostředí PowerShell a jazyku prostředí PowerShell. Existují také články nápovědy pro jednotlivé rutiny a zprostředkovatele a pro mnoho funkcí a skriptů.

Tyto články nápovědy může zobrazit na příkazovém řádku nebo zobrazení naposledy aktualizované verze v těchto článcích [Powershellu](/powershell/scripting/overview) online dokumentaci.

## <a name="getting-help-for-cmdlets"></a>Získání nápovědy pro rutiny

Chcete-li získat nápovědu o rutinách prostředí PowerShell, použijte [Get-Help](/powershell/module/microsoft.powershell.core/Get-Help) rutiny. Například, chcete-li získat nápovědu pro `Get-ChildItem` rutiny, typ:

```powershell
Get-Help Get-ChildItem
```

nebo

```powershell
Get-ChildItem -?
```

Nápovědu získáte i o rutinu Get-Help. Příklad:

```powershell
Get-Help Get-Help
```

Pokud chcete získat seznam všech rutin články nápovědy v relaci, zadejte:

```powershell
Get-Help -Category Cmdlet
```

Chcete-li zobrazit jednu stránku každého článku nápovědy v čase, použijte `help` funkci nebo její alias `man`.
Například chcete-li zobrazit nápovědu pro `Get-ChildItem` rutiny, typ

```powershell
man Get-ChildItem
```

nebo

```powershell
help Get-ChildItem
```

Chcete-li zobrazit podrobné informace, použijte **podrobné** parametr `Get-Help` rutiny. Například, chcete-li získat podrobné informace `Get-ChildItem` rutiny, typ:

```powershell
Get-Help Get-ChildItem -Detailed
```

Chcete-li zobrazit veškerý obsah v článku nápovědy, použijte **úplné** parametr `Get-Help` rutiny. Například, chcete-li zobrazit veškerý obsah v článku nápovědy `Get-ChildItem` rutiny, typ:

```powershell
Get-Help Get-ChildItem -Full
```

Chcete-li získat podrobnou nápovědu k parametry rutiny, použijte **parametr** parametr `Get-Help` rutiny. Například, chcete-li získat podrobnou nápovědu pro všechny parametry `Get-ChildItem` rutiny, typ:

```powershell
Get-Help Get-ChildItem -Parameter *
```

Chcete-li zobrazit pouze v příkladech v článku nápovědy, použijte **příklady** parametr `Get-Help`.
Chcete-li například zobrazit pouze v příkladech v tomto článku nápovědy pro `Get-ChildItem `rutiny, typ:

```powershell
Get-Help Get-ChildItem -Examples
```

Informace o tom, jak psát články nápovědy pro rutiny, které píšete, naleznete v tématu [jak napsat nápovědě k rutině](/powershell/developer/help/writing-help-for-windows-powershell-cmdlets).

## <a name="getting-conceptual-help"></a>Koncepční nápovědy

`Get-Help` Rutina taky zobrazí informace o koncepčních článků v prostředí PowerShell, včetně články o jazyce Powershellu. Koncepční články začínají předponou "about_", například about_line_editing nápovědy. (Název konceptuální článek musí být zadaná v angličtině i na jiných než anglických verzí Powershellu.)

Pokud chcete zobrazit seznam koncepčních článků, zadejte:

```powershell
Get-Help about_*
```

Pokud chcete zobrazit konkrétní článek nápovědy, zadejte název článku, například:

```powershell
Get-Help about_command_syntax
```

Parametry `Get-Help`, jako například **podrobné**, **parametr**, a **příklady**, nemají žádný vliv na displeji koncepční články nápovědy.

## <a name="getting-help-about-providers"></a>Získání nápovědy o zprostředkovatelích

`Get-Help` Rutina zobrazí informace o poskytovatelích prostředí PowerShell. Chcete-li získat nápovědu pro zprostředkovatele, zadejte `Get-Help` za nímž následuje název zprostředkovatele. Chcete-li získat nápovědu pro zprostředkovatele registru, zadejte například:

```powershell
Get-Help registry
```

Chcete-li získat seznam všech poskytovatele články nápovědy v relaci, zadejte

```powershell
Get-Help -Category provider
```

Parametry `Get-Help`, jako například **podrobné**, **parametr**, a **příklady**, nemají žádný vliv na displeji články nápovědy zprostředkovatele.

## <a name="getting-help-about-scripts-and-functions"></a>Získání nápovědy o skriptech a funkcích

Mnoho funkcí v prostředí PowerShell a skripty mají články nápovědy. Použití `Get-Help` rutiny článků nápovědy, skriptech a funkcích.

Chcete-li zobrazit nápovědu pro funkci, zadejte `Get-Help` následovaný názvem funkce. Například, chcete-li získat nápovědu pro `Disable-PSRemoting` funkci, zadejte:

```powershell
Get-Help Disable-PSRemoting
```

Chcete-li zobrazit nápovědu pro skript, zadejte cestu k souboru skriptu. Pokud skript není v cestě uvedené v proměnné prostředí Path, musíte použít plně kvalifikovanou cestu.

Například, pokud máte skript volá "TestScript.ps1" c:\\PS testovací adresář, chcete-li zobrazit článek nápovědy pro skript, typ:

```powershell
Get-Help c:\ps-test\TestScript.ps1
```

Parametry, které jsou navržené k zobrazování pracovní nápovědy rutiny pro skript a funkce pomáhají příliš. Však není nápovědy pro funkce a skripty zobrazený při spuštění `Get-Help *`.

Informace o psaní článků nápovědy, funkcí a skriptů najdete v následujících článcích:

- [about_Functions](/powershell/module/microsoft.powershell.core/about/about_functions)
- [about_Scripts](/powershell/module/microsoft.powershell.core/about/about_scripts)
- [about_Comment_Based_Help](/powershell/module/microsoft.powershell.core/about/about_comment_based_help)

## <a name="getting-help-online"></a>Získat online nápovědu

Zobrazení online článků nápovědy, který je jedním z nejlepších způsobů, jak získat pomoc. Online články jsou snáze aktualizovat a poskytovat nejaktuálnější obsah.

Chcete-li získat nápovědu online, použijte **Online** parametr `Get-Help` rutiny. Všech článků nápovědy, které jsou součástí prostředí PowerShell, včetně zprostředkovatele nápovědy a koncepční (články nápovědy o) jsou k dispozici online v [Powershellu](/powershell/scripting/powershell-scripting) dokumentaci.

> [!NOTE]
> Nelze použít **Online** parametr s koncepční (about_\*) nebo zprostředkovatele články nápovědy.
> Online nápovědy je volitelné, takže nefunguje pro všechny rutiny, funkce nebo skriptu.

Například, chcete-li získat online verzi nápovědy článku `Get-ChildItem` rutiny, typ:

```powershell
Get-Help Get-ChildItem -Online
```

Prostředí PowerShell otevře článek ve vašem výchozím prohlížeči. Pokud se podporuje online nápovědy pro článek nápovědy, můžete také zobrazit adresu URL článek nápovědy. Adresa URL se zobrazí v části související odkazy na článek nápovědy.

Pokud chcete zobrazit adresu URL pro online verzi rutinu Add-Computer, zadejte například:

```powershell
Get-Help Add-Computer
```

První řádek v souvisejících odkazů části tohoto článku je uveden níže.

```Output
Online version: http://go.microsoft.com/fwlink/?LinkId=821564
```

Informace o tom, jak poskytovat online podporu pro vaše články nápovědy najdete v tématu [about_Comment_Based_Help](/powershell/module/microsoft.powershell.core/about/about_comment_based_help).

## <a name="see-also"></a>Viz taky

- [about_Functions](/powershell/module/microsoft.powershell.core/about/about_functions)
- [about_Scripts](/powershell/module/microsoft.powershell.core/about/about_scripts)
- [about_Comment_Based_Help](/powershell/module/microsoft.powershell.core/about/about_comment_based_help)
- [Get-Help](/powershell/module/microsoft.powershell.core/get-help)
