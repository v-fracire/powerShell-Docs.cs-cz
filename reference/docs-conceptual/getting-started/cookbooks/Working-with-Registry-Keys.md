---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Práce s klíče registru"
ms.assetid: 91bfaecd-8684-48b4-ad86-065dfe6dc90a
ms.openlocfilehash: efb2c016afa2212c2907c0740ad26c4e4cddd3af
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/03/2017
---
# <a name="working-with-registry-keys"></a>Práce s klíče registru
Protože jsou klíče registru položky v prostředí Windows PowerShell jednotky, je velmi podobné práce se soubory a složky práci s nimi. Jeden kritické rozdílem je, že každá položka na jednotce založenou na registru prostředí Windows PowerShell je kontejner, stejně jako složky na jednotce systému souborů. Vlastnosti těchto položek, není odlišné položky jsou však položky registru a jejich přidružené hodnoty.

### <a name="listing-all-subkeys-of-a-registry-key"></a>Výpis všech podklíčů klíče registru
Můžete zobrazit všechny položky přímo v klíči registru pomocí **Get-ChildItem**. Přidejte volitelné **Force** parametr zobrazení skrytý nebo položky system. Tento příkaz například zobrazí položky přímo v rámci jednotku prostředí Windows PowerShell HKCU:, která odpovídá podregistr registru HKEY_CURRENT_USER:

```
PS> Get-ChildItem -Path hkcu:\

   Hive: Microsoft.PowerShell.Core\Registry::HKEY_CURRENT_USER

SKC  VC Name                           Property
---  -- ----                           --------
  2   0 AppEvents                      {}
  7  33 Console                        {ColorTable00, ColorTable01, ColorTab...
 25   1 Control Panel                  {Opened}
  0   5 Environment                    {APR_ICONV_PATH, INCLUDE, LIB, TEMP...}
  1   7 Identities                     {Last Username, Last User ...
  4   0 Keyboard Layout                {}
...
```

Toto jsou nejvyšší úrovně klíče viditelné HKEY_CURRENT_USER v editoru registru (Regedit.exe).

Cesta v registru můžete také určit tak, že zadáte název zprostředkovatele registru, za nímž následují "**::**". Celý název zprostředkovatele registru **Microsoft.PowerShell.Core\\registru**, ale to může být zkrátí tak, aby právě **registru**. Některé z následujících příkazů zobrazí seznam obsah přímo pod HKCU:

```
Get-ChildItem -Path Registry::HKEY_CURRENT_USER
Get-ChildItem -Path Microsoft.PowerShell.Core\Registry::HKEY_CURRENT_USER
Get-ChildItem -Path Registry::HKCU
Get-ChildItem -Path Microsoft.PowerShell.Core\Registry::HKCU
Get-ChildItem HKCU:
```

Tyto příkazy seznamu jenom přímo obsažených položek, podobně jako pomocí jeho Cmd.exe **DIR** příkaz nebo **ls** v prostředí systému UNIX. Chcete-li zobrazit položky, je potřeba zadat **Recurse** parametr. K zobrazení seznamu všechny klíče registru ve HKCU, použijte následující příkaz (Tato operace může trvat velmi dlouho.):

```
Get-ChildItem -Path hkcu:\ -Recurse
```

**Get-ChildItem** můžete provádět komplexní možnosti filtrování prostřednictvím jeho **cesta**, **filtru**, **zahrnout**, a **vyloučit** parametry, ale tyto parametry jsou obvykle pouze na základě názvu. Můžete provádět komplexní filtrování založené na jiné vlastnosti položky pomocí **Where-Object**rutiny. Následující příkaz vyhledá všechny klíče v rámci HKCU:\\softwaru, které mají více než jeden podklíčů a také mít přesně čtyři hodnoty:

```
Get-ChildItem -Path HKCU:\Software -Recurse | Where-Object -FilterScript {($_.SubKeyCount -le 1) -and ($_.ValueCount -eq 4) }
```

### <a name="copying-keys"></a>Kopírování klíče
Kopírování provádí pomocí **Copy-Item**. Následující příkaz zkopíruje HKLM:\\softwaru\\Microsoft\\Windows\\CurrentVersion a všechny její vlastnosti, aby HKCU:\\, vytváří nový klíč s názvem "CurrentVersion":

```
Copy-Item -Path 'HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion' -Destination hkcu:
```

Pokud byste zkontrolovat tento nový klíč, v editoru registru nebo pomocí **Get-ChildItem**, si všimnete nemají kopie podklíče obsažené v novém umístění. Aby bylo možné kopírovat veškerý obsah kontejneru, je třeba zadat **Recurse** parametr. Chcete-li předchozí příkaz rekurzivní kopírování, použijete tento příkaz:

```
Copy-Item -Path 'HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion' -Destination hkcu: -Recurse
```

Můžete dál používat jiné nástroje, které už máte k dispozici ke zkopírování souborů. Všechny nástroje pro úpravu registru – včetně reg.exe, regini.exe a regedit.exe—and objektů COM, které podporují úpravy registru (například na rozhraní WMI a WScript.Shell třídy StdRegProv) můžete ji použít v rámci prostředí Windows PowerShell.

### <a name="creating-keys"></a>Vytváření klíčů
Vytvoření nového klíče v registru je jednodušší než vytvoření nové položky v systému souborů. Protože všechny klíče registru jsou kontejnery, není potřeba zadat typ položky; je jednoduše zadat explicitní cestu, jako například:

```
New-Item -Path hkcu:\software_DeleteMe
```

Cestu založenou na poskytovateli můžete také zadat klíč:

```
New-Item -Path Registry::HKCU_DeleteMe
```

### <a name="deleting-keys"></a>Odstraňování kláves
Odstraňování položek je v podstatě stejný pro všechny poskytovatele. Následující příkazy bezobslužně odebere položky:

```
Remove-Item -Path hkcu:\Software_DeleteMe
Remove-Item -Path 'hkcu:\key with spaces in the name'
```

### <a name="removing-all-keys-under-a-specific-key"></a>Odebrání všechny klíče v rámci konkrétního klíče
Položky lze odebrat pomocí **odebrat položky**, ale zobrazí se výzva k potvrzení odebrání, pokud položka obsahuje cokoliv jiného. Například, pokud jsme pokusu o odstranění HKCU:\\CurrentVersion podklíč jsme vytvořili, vidíte, toto:

```
Remove-Item -Path hkcu:\CurrentVersion

Confirm
The item at HKCU:\CurrentVersion\AdminDebug has children and the -recurse
parameter was not specified. If you continue, all children will be removed with
 the item. Are you sure you want to continue?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):
```

Chcete-li odstranit položky bez výzvy k potvrzení, zadejte **-Recurse** parametr:

```
Remove-Item -Path HKCU:\CurrentVersion -Recurse
```

Pokud chcete odebrat všechny položky v rámci HKCU:\\CurrentVersion, ale není HKCU:\\CurrentVersion sám sebe, můžete místo toho použít:

```
Remove-Item -Path HKCU:\CurrentVersion\* -Recurse
```

