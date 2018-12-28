---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Přímá manipulace s položkami
ms.assetid: 8cbd4867-917d-41ea-9ff0-b8e765509735
ms.openlocfilehash: 688f9194bd16793331325999c69e88df3e94c976
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404066"
---
# <a name="manipulating-items-directly"></a>Přímá manipulace s položkami

Prvky, které se zobrazí v prostředí Windows PowerShell jednotky, jako jsou soubory a složkami v jednotky systému souborů a klíči registru v registru jednotek Windows Powershellu, se nazývají *položky* v prostředí Windows PowerShell. Rutiny pro práci s nimi položky mají podstatným jménem **položky** v jejich názvy.

Výstup **Get-Command - podstatné jméno položky** příkaz znázorňuje, že jsou devět položky rutiny prostředí Windows PowerShell.

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

Chcete-li vytvořit novou položku v systému souborů, použijte **New-Item** rutiny. Zahrnout **cesta** parametr s cestou k položce a **ItemType** parametr s hodnotou "file" nebo "directory".

Například, chcete-li vytvořit nový adresář s názvem "New.Directory"in C:\\dočasný adresář, zadejte:

```
PS> New-Item -Path c:\temp\New.Directory -ItemType Directory

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
d----        2006-05-18  11:29 AM            New.Directory
```

Vytvoření souboru, změňte hodnotu **ItemType** parametr "file". Například pokud chcete vytvořit soubor s názvem "file1.txt" v adresáři New.Directory, zadejte:

```
PS> New-Item -Path C:\temp\New.Directory\file1.txt -ItemType file

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\temp\New.Directory

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
-a---        2006-05-18  11:44 AM          0 file1
```

Stejný postup můžete použít k vytvoření nového klíče registru. Ve skutečnosti klíč registru je snazší vytvářet, protože klíč je jediným typem položky v registru Windows. (Položky registru jsou položky *vlastnosti*.) Například pokud chcete vytvořit klíč s názvem "_testovat" v podklíči CurrentVersion, zadejte:

```
PS> New-Item -Path HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion_Test

   Hive: Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\SOFTWARE\Micros
oft\Windows\CurrentVersion

SKC  VC Name                           Property
---  -- ----                           --------
  0   0 _Test                          {}
```

Pokud zadáte cestu k registru, nezapomeňte zahrnout dvojtečka (**:**) v prostředí Windows PowerShell jednotka názvy, HKLM: a HKCU:. Bez dvojtečky prostředí Windows PowerShell nedokáže rozpoznat název jednotky v cestě.

### <a name="why-registry-values-are-not-items"></a>Proč hodnoty registru nejsou položky

Při použití **Get-ChildItem** rutiny a vyhledání položek v klíči registru a nikdy se zobrazí položky skutečné registru nebo jejich hodnoty.

Například klíč registru **HKEY_LOCAL_MACHINE\\softwaru\\Microsoft\\Windows\\CurrentVersion\\spustit** obvykle obsahuje několik položek registru které představují aplikace, které běží při spuštění systému.

Ale při použití **Get-ChildItem** hledání podřízených položek v klíči, všechny uvidíte je **OptionalComponents** podklíčů klíče:

```
PS> Get-ChildItem HKLM:\Software\Microsoft\Windows\CurrentVersion\Run

   Hive: Microsoft.PowerShell.Core\Registry::HKEY_LOCAL_MACHINE\Software\Micros
oft\Windows\CurrentVersion\Run
SKC  VC Name                           Property
---  -- ----                           --------
  3   0 OptionalComponents             {}
```

I když bylo by vhodné položky registru považovat za položky, nelze zadat cestu k položce registru způsobem, který zajistí, že se jedná o jedinečný. Cesta notation nerozlišuje mezi podklíč registru s názvem **spustit** a **(výchozí)** položky registru v **spustit** podklíči. Navíc vzhledem k tomu, že názvy položek registru může obsahovat znak zpětného lomítka (**\\**), kdyby položky registru položek, cesta notation nejde použít k rozlišení položku registru s názvem  **Windows\\CurrentVersion\\spustit** z podklíče, který se nachází v této cestě.

### <a name="renaming-existing-items-rename-item"></a>Přejmenování existujících položek (přejmenování položek)

Chcete-li změnit název souboru nebo složky, použijte **přejmenovat položku** rutiny. Následující příkaz změní název **file1.txt** do souboru **fileOne.txt**.

```powershell
Rename-Item -Path C:\temp\New.Directory\file1.txt fileOne.txt
```

**Přejmenovat položku** rutiny můžete změnit název souboru nebo složky, ale nelze jej přesunout položku. Následující příkaz se nezdaří, protože se pokusí přesunout soubor z adresáře New.Directory do svého adresáře Temp.

```
PS> Rename-Item -Path C:\temp\New.Directory\fileOne.txt c:\temp\fileOne.txt
Rename-Item : Cannot rename because the target specified is not a path.
At line:1 char:12
+ Rename-Item  <<<< -Path C:\temp\New.Directory\fileOne c:\temp\fileOne.txt
```

### <a name="moving-items-move-item"></a>Přesun položek (přesunutí položek)

Chcete-li přesunout soubor nebo složku, použijte **přesunout položku** rutiny.

Například následující příkaz přesune New.Directory adresáře C:\\dočasný adresář na kořenové jednotce C:. Chcete-li ověřit, že položka byla přesunuta, zahrňte **PassThru** parametr **přesunout položku** rutiny. Bez **Passthru**, **přesunout položku** rutiny nezobrazí žádné výsledky.

```
PS> Move-Item -Path C:\temp\New.Directory -Destination C:\ -PassThru

    Directory: Microsoft.Windows PowerShell.Core\FileSystem::C:\

Mode                LastWriteTime     Length Name
----                -------------     ------ ----
d----        2006-05-18  12:14 PM            New.Directory
```

### <a name="copying-items-copy-item"></a>Kopírování položek (Copy-Item)

Pokud jste se seznámili s operací kopírování v jiné prostředí, můžete se setkat chování **Copy-Item** rutiny v prostředí Windows PowerShell na neobvyklé. Při kopírování položky z jednoho umístění do druhého, Copy-Item nekopíruje obsah ve výchozím nastavení.

Například pokud kopírujete **New.Directory** z jednotky C: do C: adresáře\\dočasný adresář, příkaz proběhne úspěšně, ale soubory v adresáři New.Directory nejsou zkopírovány.

```powershell
Copy-Item -Path C:\New.Directory -Destination C:\temp
```

Pokud zobrazíte obsah **C:\\temp\\New.Directory**, zjistíte, že neobsahuje žádné soubory:

```
PS> Get-ChildItem -Path C:\temp\New.Directory
PS>
```

Proč není **Copy-Item** rutiny zkopírovat obsah do nového umístění?

**Copy-Item** rutiny byla navržena jako obecný; není jenom pro kopírování souborů a složek. Navíc i v případě, že kopírování souborů a složek, můžete zkopírovat pouze kontejneru a ne na položky v něm.

Kopírovat veškerý obsah do složky, zahrňte **Recurse** parametr **Copy-Item** rutiny v příkazu. Pokud už jste zkopírovali adresáře, aniž by jeho obsah, přidejte **platnost** parametr, který umožňuje přepsat prázdné složky.

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

### <a name="deleting-items-remove-item"></a>Odstranění položek (Remove-Item)

Chcete-li odstranit soubory a složky, použijte **Remove-Item** rutiny. Rutiny prostředí Windows PowerShell, jako například **odebrat položku**, můžete díky významné, nevratné změny se často výzvu k potvrzení, když zadáte jeho příkazy. Například, pokud se pokusíte odebrat **New.Directory** složky, budete vyzváni k potvrzení příkazu, protože složka obsahuje soubory:

```
PS> Remove-Item C:\New.Directory

Confirm
The item at C:\temp\New.Directory has children and the -recurse parameter was not
specified. If you continue, all children will be removed with the item. Are you
 sure you want to continue?
[Y] Yes  [A] Yes to All  [N] No  [L] No to All  [S] Suspend  [?] Help
(default is "Y"):
```

Protože **Ano** je výchozí odpovědí, odstraňte složku a její soubory, stiskněte **Enter** klíč. Chcete-li odebrat složku bez potvrzení, použijte **-Recurse** parametru.

```powershell
Remove-Item C:\temp\New.Directory -Recurse
```

### <a name="executing-items-invoke-item"></a>Provádění položky (Invoke-Item)

Používá prostředí Windows PowerShell **Invoke-Item** rutina k provedení výchozí akce pro soubor nebo složku. Tato výchozí akce je určená výchozí obslužnou rutinu aplikace v registru. efekt je stejný, jako kdyby jste dvakrát klikněte na položku v Průzkumníku souborů.

Předpokládejme například, že spustíte následující příkaz:

```powershell
Invoke-Item C:\WINDOWS
```

Okno Průzkumníka, který se nachází v C:\\se zobrazí Windows, stejně jako v případě, kdyby jste dvakrát kliknuli C:\\složku Windows.

Pokud vyvoláte **Boot.ini** souboru v systému starší než Windows Vista:

```powershell
Invoke-Item C:\boot.ini
```

Pokud typ souboru INI souvisí s Poznámkový blok, soubor boot.ini se otevře v poznámkovém bloku.