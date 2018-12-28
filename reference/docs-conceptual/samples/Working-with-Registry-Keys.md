---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Práce s klíči registru
ms.assetid: 91bfaecd-8684-48b4-ad86-065dfe6dc90a
ms.openlocfilehash: a9d08f2f6b5803980dec45a4e266ad66879c8c8d
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404104"
---
# <a name="working-with-registry-keys"></a>Práce s klíči registru

Vzhledem k tomu klíče registru položky na jednotkách prostředí Windows PowerShell, práce s nimi je velmi podobně jako při práci se soubory a složkami. Jeden kritický rozdíl je, že všechny položky v prostředí Windows PowerShell jednotku založenou na registru je kontejner, stejně jako složky na jednotce systému souborů. Vlastnosti položek, ne rozdílných položek jsou však položky registru a jejich přidružené hodnoty.

### <a name="listing-all-subkeys-of-a-registry-key"></a>Výpis všech podklíčů klíče registru

Můžete zobrazit všechny položky přímo z klíče registru pomocí **Get-ChildItem**. Přidat nepovinný **platnost** parametr zobrazení skrytých nebo položky system. Tento příkaz například zobrazí položek přímo v rámci jednotku prostředí Windows PowerShell HKCU:, která odpovídá podregistr registru HKEY_CURRENT_USER:

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

Toto jsou nejvyšší úrovně klíče viditelné v klíči HKEY_CURRENT_USER v editoru registru (Regedit.exe).

Cesta v registru můžete také určit zadáním názvu registru zprostředkovatele, za nímž následuje "**::**". Celý název registru zprostředkovatele **Microsoft.PowerShell.Core\\registru**, ale to lze zkrátit jenom **registru**. Některé z následujících příkazů bude zobrazovat obsah přímo pod HKCU:

```powershell
Get-ChildItem -Path Registry::HKEY_CURRENT_USER
Get-ChildItem -Path Microsoft.PowerShell.Core\Registry::HKEY_CURRENT_USER
Get-ChildItem -Path Registry::HKCU
Get-ChildItem -Path Microsoft.PowerShell.Core\Registry::HKCU
Get-ChildItem HKCU:
```

Tyto příkazy zobrazí seznam pouze přímo obsažené položky, podobně jako pomocí jeho Cmd.exe **DIR** příkazu nebo **ls** v prostředí systému UNIX. Zobrazit položky obsažené, je třeba zadat **Recurse** parametru. Chcete-li vypsat všechny klíče registru v HKCU, použijte následující příkaz (Tato operace může trvat extrémně dlouhou dobu.):

```powershell
Get-ChildItem -Path hkcu:\ -Recurse
```

**Rutina Get-ChildItem** můžete provádět složité filtrování možnosti prostřednictvím jeho **cesta**, **filtr**, **zahrnout**, a **vyloučit**parametry, ale tyto parametry jsou obvykle pouze na základě názvu. Pokud chcete provádět složité filtrování založené na jiné vlastnosti položek pomocí **Where-Object** rutiny. Následující příkaz vyhledá všechny klíče v rámci HKCU:\\softwaru, které mají více než jedna podklíče a také mít přesně čtyři hodnoty:

```powershell
Get-ChildItem -Path HKCU:\Software -Recurse | Where-Object -FilterScript {($_.SubKeyCount -le 1) -and ($_.ValueCount -eq 4) }
```

### <a name="copying-keys"></a>Kopírování klíčů

Kopírování se provádí pomocí **Copy-Item**. Následující příkaz zkopíruje HKLM:\\softwaru\\Microsoft\\Windows\\CurrentVersion a všechny jeho vlastnosti na HKCU:\\, vytváří se nový klíč s názvem "CurrentVersion":

```powershell
Copy-Item -Path 'HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion' -Destination hkcu:
```

Pokud byste zkontrolovat tento nový klíč v editoru registru nebo pomocí **Get-ChildItem**, všimnete si, že nemáte kopie podklíče obsažené v novém umístění. Aby bylo možné kopírovat veškerý obsah kontejneru, je třeba zadat **Recurse** parametru. Chcete-li předchozí příkaz rekurzivního kopírování, použijete tento příkaz:

```powershell
Copy-Item -Path 'HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion' -Destination hkcu: -Recurse
```

Stále můžete použít jiné nástroje, které už máte k dispozici k provedení kopie systému souborů. Všechny nástroje pro úpravu registru – včetně reg.exe, regini.exe a regedit.exe—and objektů modelu COM, které podporují úpravy registru (například WScript.Shell a služby WMI StdRegProv třídy) může být použito v rámci prostředí Windows PowerShell.

### <a name="creating-keys"></a>Vytvoření klíčů

Vytvoření nové klíče v registru je jednodušší než vytvoření nové položky v systému souborů. Protože všechny klíče registru jsou kontejnery, není nutné určit typ položky; můžete jednoduše zadat explicitní cestu, například:

```powershell
New-Item -Path hkcu:\software_DeleteMe
```

Můžete také cestu založenou na poskytovateli k zadání klíče:

```powershell
New-Item -Path Registry::HKCU_DeleteMe
```

### <a name="deleting-keys"></a>Odstranění klíče

Odstranění položek je v podstatě stejný pro všechny poskytovatele. Následující příkazy odeberou tiše položky:

```powershell
Remove-Item -Path hkcu:\Software_DeleteMe
Remove-Item -Path 'hkcu:\key with spaces in the name'
```

### <a name="removing-all-keys-under-a-specific-key"></a>Odebrat všechny klíče v rámci konkrétního klíče

Odebírat položky, které můžete odebrat pomocí **Remove-Item**, ale zobrazí se výzva k potvrzení odebrání, pokud položka obsahuje cokoli. Například, pokud jsme pokus o odstranění HKCU:\\CurrentVersion podklíč jsme vytvořili, zobrazí toto:

```
Remove-Item -Path hkcu:\CurrentVersion

Confirm
The item at HKCU:\CurrentVersion\AdminDebug has children and the -recurse
parameter was not specified. If you continue, all children will be removed with
 the item. Are you sure you want to continue?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):
```

Chcete-li odstranit obsažené položky bez výzvy, zadejte **-Recurse** parametr:

```powershell
Remove-Item -Path HKCU:\CurrentVersion -Recurse
```

Pokud chcete odebrat všechny položky v rámci HKCU:\\CurrentVersion, ale ne HKCU:\\CurrentVersion samotné, můžete místo toho použít:

```powershell
Remove-Item -Path HKCU:\CurrentVersion\* -Recurse
```