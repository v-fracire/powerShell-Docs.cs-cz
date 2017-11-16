---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Manipulace s nimi přímo položky"
ms.assetid: 8cbd4867-917d-41ea-9ff0-b8e765509735
ms.openlocfilehash: d9aa95dcb0da2e8203cbe32d64b95bf33d914166
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/03/2017
---
# <a name="manipulating-items-directly"></a>Manipulace s nimi přímo položky
Prvky, které se zobrazí v prostředí Windows PowerShell jednotky, jako jsou soubory a složky v jednotky systému souborů a klíčů registru v registru jednotky prostředí Windows PowerShell, se nazývají *položky* v prostředí Windows PowerShell. Rutiny pro práci s nimi položky mají podstatným jménem **položky** v jejich názvy.

Výstup **Get-Command - podstatné jméno položky** příkaz zobrazí, že jsou devět položky rutiny prostředí Windows PowerShell.

```
PS> Get-Command -Noun Item

CommandType     Name                            Definition
-----------     ----                            ----------
Cmdlet          Clear-Item                      Clear-Item [-Path] <String[]...
Cmdlet          Copy-Item                       Copy-Item [-Path] <String[]>...
Cmdlet          Get-Item                        Get-Item [-Path] <String[]> ...
Cmdlet          Invoke-Item                     Invoke-Item [-Path] <String[...
Cmdlet          Move-Item                       Move-Item [-Path] <String[]>...
Cmdlet          New-Item                        New-Item [-Path] <String[]> ...
Cmdlet          Remove-Item                     Remove-Item [-Path] <String[...
Cmdlet          Rename-Item                     Rename-Item [-Path] <String>...
Cmdlet          Set-Item                        Set-Item [-Path] <String[]> ...
```

### <a name="creating-new-items-new-item"></a>Vytvoření nové položky (nová položka)
Chcete-li vytvořit novou položku v systému souborů, použijte **nové položky** rutiny. Zahrnout **cesta** parametr s cestou k položce a **ItemType** parametr s hodnotou "soubor" nebo "adresář".

Například vytvořte nový adresář s názvem "New.Directory"in jednotce C:\\dočasné složky, zadejte:

```
PS> New-Item -Path c:\temp\New.Directory -ItemType Directory

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
d----        2006-05-18  11:29 AM            New.Directory
```

Pokud chcete vytvořit soubor, změňte hodnotu **ItemType** parametr "soubor". Například pokud chcete vytvořit soubor s názvem "file1.txt" v adresáři New.Directory, zadejte:

```
PS> New-Item -Path C:\temp\New.Directory\file1.txt -ItemType file

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp\New.Directory

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2006-05-18  11:44 AM          0 file1
```

Chcete-li vytvořit nový klíč registru můžete použít stejný postup. Klíč registru je ve skutečnosti jednodušší vytvořit, protože klíč je jediným typem položku v registru systému Windows. (Položky registru jsou položky *vlastnosti*.) Například pokud chcete vytvořit klíč s názvem "_Test" v podklíči CurrentVersion, zadejte:

```
PS> New-Item -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion_Test

   Hive: Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Micros
oft\Windows\CurrentVersion

SKC  VC Name                           Property
---  -- ----                           --------
  0   0 _Test                          {}
```

Pokud zadáte cestu registru, nezapomeňte zahrnout dvojtečkou (**:**) v prostředí Windows PowerShell jednotka názvy, HKLM: a HKCU:. Bez dvojtečky prostředí Windows PowerShell nelze rozpoznat název jednotky v cestě.

### <a name="why-registry-values-are-not-items"></a>Proč hodnoty registru, které nejsou žádné položky
Při použití **Get-ChildItem** rutiny a vyhledání položek v klíči registru a nikdy se zobrazí skutečné registru nebo jejich hodnot.

Například klíč registru **HKEY_LOCAL_MACHINE\\softwaru\\Microsoft\\Windows\\CurrentVersion\\spustit** obvykle obsahuje několik položky registru které představují aplikace, které jsou spuštěny při spuštění systému.

Ale při použití **Get-ChildItem** a hledat podřízené položky v klíči, uvidíte je **OptionalComponents** podklíčů klíče:

```
PS> Get-ChildItem HKLM:\Software\Microsoft\Windows\CurrentVersion\Run
   Hive: Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\Software\Micros
oft\Windows\CurrentVersion\Run
SKC  VC Name                           Property
---  -- ----                           --------
  3   0 OptionalComponents             {}
```

Přestože by bylo vhodnější položky registru považovat za položky, nelze zadat cestu k položce registru způsobem, který zajistí, že bude jedinečný. Zápis cesty se nerozlišují podklíč registru s názvem **spustit** a **(výchozí)** položky registru v **spustit** podklíč. Navíc vzhledem k tomu, že názvy položek registru může obsahovat znak zpětného lomítka (**\\**), pokud regsitry položky byly položek, zápis cesty nelze použít k rozlišení položku registru s názvem  **Windows\\CurrentVersion\\spustit** z podklíče, který je umístěný v této cestě.

### <a name="renaming-existing-items-rename-item"></a>Přejmenování existující položky (přejmenování položky)
Chcete-li změnit název souboru nebo složky, použijte **přejmenování položky** rutiny. Tento příkaz změní název **file1.txt** do souboru **fileOne.txt**.

```
PS> Rename-Item -Path C:\temp\New.Directory\file1.txt fileOne.txt
```

**Přejmenování položky** rutiny můžete změnit název souboru nebo složce, ale nemůžete ho přesunout položku. Následující příkaz selže, protože se pokouší přesunout soubor z adresáře New.Directory do dočasné složky.

```
PS> Rename-Item -Path C:\temp\New.Directory\fileOne.txt c:\temp\fileOne.txt
Rename-Item : Cannot rename because the target specified is not a path.
At line:1 char:12
+ Rename-Item  <<<< -Path C:\temp\New.Directory\fileOne c:\temp\fileOne.txt
```

### <a name="moving-items-move-item"></a>Přesouvání položek (Move-Item)
Chcete-li přesunout soubor nebo složku, použijte **přesunout položku** rutiny.

Například následující příkaz přesune adresáři New.Directory z jednotce C:\\dočasný adresář na kořenové jednotce C:. Chcete-li ověřit, že položka byla přesunuta, zahrňte **PassThru** parametr **přesunout položku** rutiny. Bez **Passthru**, **přesunout položku** rutiny nezobrazí žádné výsledky.

```
PS> Move-Item -Path C:\temp\New.Directory -Destination C:\ -PassThru

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
d----        2006-05-18  12:14 PM            New.Directory
```

### <a name="copying-items-copy-item"></a>Kopírování položek (Copy-Item)
Pokud jste obeznámeni s operace kopírování v jiné prostředí, můžete zjistit, chování **Copy-Item** rutiny v prostředí Windows PowerShell jako neobvyklé. Při kopírování položku z jednoho umístění do druhého, Copy-Item nekopíruje obsah ve výchozím nastavení.

Například pokud zkopírujete **New.Directory** adresář z jednotky C: na jednotce C:\\dočasného adresáře příkazu úspěšné, ale soubory v adresáři New.Directory nebudou zkopírovány.

```
PS> Copy-Item -Path C:\New.Directory -Destination C:\temp
```

Pokud chcete zobrazovat obsah **C:\\temp\\New.Directory**, zjistíte, že neobsahuje žádné soubory:

```
PS> Get-ChildItem -Path C:\temp\New.Directory
PS>
```

Proč není **Copy-Item** rutiny zkopírujte obsah do nového umístění?

**Copy-Item** rutiny byla navržená tak, aby být obecný; není právě pro kopírování souborů a složek. Navíc i v případě, že kopírování souborů a složek, můžete chtít kopírovat pouze kontejneru a není položky v něm.

Kopírovat veškerý obsah složky, zahrňte **Recurse** parametr **Copy-Item** rutiny v příkazu. Pokud jste již zkopírovali adresáři bez obsahu, přidejte **Force** parametr, který můžete přepsat prázdné složky.

```
PS> Copy-Item -Path C:\New.Directory -Destination C:\temp -Recurse -Force -Passthru
    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
d----        2006-05-18   1:53 PM            New.Directory

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp\New.Directory

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2006-05-18  11:44 AM          0 file1
```

### <a name="deleting-items-remove-item"></a>Odstraňování položek (Remove-Item)
Chcete-li odstranit soubory a složky, použijte **odebrat položky** rutiny. Rutiny prostředí Windows PowerShell, jako například **odebrat položky**, který způsobit významné, nedá se vrátit změny se často výzvu k potvrzení, když zadáte jeho příkazy. Například pokud se pokusíte odebrat **New.Directory** složku, zobrazí se výzva k potvrzení příkazu, protože složka obsahuje soubory:

```
PS> Remove-Item C:\New.Directory

Confirm
The item at C:\temp\New.Directory has children and the -recurse parameter was not
specified. If you continue, all children will be removed with the item. Are you
 sure you want to continue?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):
```

Protože **Ano** je výchozí odpověď, a odstranit složku a její soubory, stiskněte **Enter** klíč. Chcete-li odebrat složku bez potvrzení, použijte **-Recurse** parametr.

```
PS> Remove-Item C:\temp\New.Directory -Recurse
```

### <a name="executing-items-invoke-item"></a>Provádění položky (Invoke-Item)
Používá prostředí Windows PowerShell **Invoke-Item** rutina k provedení výchozí akce pro soubor nebo složku. Tato výchozí akce je dáno výchozí obslužnou rutinu aplikace v registru; účinek je stejný jako v případě, že dvakrát kliknete na položky v Průzkumníku souborů.

Předpokládejme například, že spustíte následující příkaz:

```
PS> Invoke-Item C:\WINDOWS
```

Okno Průzkumníka, který je umístěný v C:\\se zobrazí Windows, stejně jako kdyby měl dvakrát kliknuli jednotce C:\\složka systému Windows.

Pokud jste vyvolání **Boot.ini** souboru v systému starší než Windows Vista:

```
PS> Invoke-Item C:\boot.ini
```

Pokud je typ souboru .ini přidružený Poznámkový blok, soubor boot.ini se otevře v poznámkovém bloku.

