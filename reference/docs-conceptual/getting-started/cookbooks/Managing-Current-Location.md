---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Správa aktuálního umístění
ms.assetid: a9f9e7a7-3ea8-47d3-bbb4-6e437f6d4a4a
ms.openlocfilehash: 8d529bf4a85553b95a9cab2739016859662486f2
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
ms.locfileid: "30952218"
---
# <a name="managing-current-location"></a>Správa aktuálního umístění

Při přechodu systémy složky v Průzkumníku souborů, obvykle mají konkrétní pracovní umístění – konkrétně, aktuální otevřít složku. Položky v aktuální složce se dá snadno upravit kliknutím je. Pro rozhraní příkazového řádku, jako je například Cmd.exe když jsou ve stejné složce jako konkrétní soubor, můžete k němu přístup zadání relativně krátkého názvu, namísto nutnosti zadat celou cestu k souboru. Aktuální adresář se nazývá pracovní adresář.

Prostředí Windows PowerShell používá podstatným jménem **umístění** odkazovat na pracovní adresář a implementuje řadu rutin sloužící ke zkoumání a manipulaci s vaši polohu.

### <a name="getting-your-current-location-get-location"></a>Získávání aktuální umístění (Get umístění)

Chcete-li zjistit cestu vaše aktuální umístění adresáře, zadejte **Get-umístění** příkaz:

```
PS> Get-Location
Path
----
C:\Documents and Settings\PowerUser
```

> [!NOTE]
> Rutina Get-umístění je podobná **pwd** příkazu v prostředí BASH. Nastavení umístění rutina je podobná **cd** v Cmd.exe.

### <a name="setting-your-current-location-set-location"></a>Nastavení vaše aktuální umístění (Set umístění)

**Get-umístění** příkaz se používá s **nastavení umístění** příkaz. **Nastavení umístění** příkaz umožňuje zadat vaše aktuální umístění adresáře.

```powershell
Set-Location -Path C:\Windows
```

Po zadání příkazu si všimnete, že neobdržíte žádné přímé zpětnou vazbu o efekt příkazu. Většina příkazů prostředí Windows PowerShell, které provádějí akce vytvořit žádné nebo téměř žádné výstup, protože výstup není vždy užitečné. Chcete-li ověřit, že došlo ke změně úspěšné directory při zadávání **nastavení umístění** příkaz, zahrnují **- PassThru** parametr při zadání **Set-umístění**příkaz:

```
PS> Set-Location -Path C:\Windows -PassThru

Path
----
C:\WINDOWS
```

**- PassThru** parametr můžete použít s mnoha sady příkazů v prostředí Windows PowerShell k vrácení informací o výsledek v případech, ve kterých je žádný výchozí výstup.

Můžete určit cest relativně k vaše aktuální umístění stejným způsobem, jako je by ve většině systému UNIX a Windows příkazu prostředí shell. Ve standardním zápisu pro relativní cesty tečku (**.**) představuje aktuální složce a zdvojených období (**...** ) představuje nadřazeném adresáři vaše aktuální umístění.

Například, pokud jste v **C:\\Windows** složku, tečku (**.**) představuje **C:\\Windows** a dvakrát tečky (**...** ) představují **C:**. Můžete změnit z aktuálního umístění do kořenového adresáře jednotky C: zadáním:

```
PS> Set-Location -Path .. -PassThru

Path
----
C:\
```

Stejný postup funguje na jednotkách prostředí Windows PowerShell, které nejsou jednotky systému souborů, jako například **HKLM:**. Můžete nastavit vaši polohu, aby HKLM\\softwarového klíče v registru zadáním:

```
PS> Set-Location -Path HKLM:\SOFTWARE -PassThru

Path
----
HKLM:\SOFTWARE
```

Můžete změnit umístění adresáře na nadřazeném adresáři, který je kořenem HKLM prostředí PowerShell systému Windows: jednotky pomocí relativní cesty:

```
PS> Set-Location -Path .. -PassThru

Path
----
HKLM:\
```

Můžete zadat nastavení umístění nebo použít některou z předdefinovaných aliasy prostředí Windows PowerShell pro nastavení umístění (cd, chdir, sl). Příklad:

```powershell
cd -Path C:\Windows
```

```powershell
chdir -Path .. -PassThru
```

```powershell
sl -Path HKLM:\SOFTWARE -PassThru
```

### <a name="saving-and-recalling-recent-locations-push-location-and-pop-location"></a>Ukládání a vrací poslední umístění (nabízené umístění a umístění Pop)

Při změně umístění, je užitečné, chcete-li zaznamenávat, kde jste a mohli vrátit do předchozího umístění. **Nabízené umístění** rutiny v prostředí Windows PowerShell vytvoří seřazené historii ("zásobník") directory cesty, kde jste, a můžete krokovat zpět v historii cesty adresářů pomocí doplňkové  **Umístění POP** rutiny.

Například prostředí Windows PowerShell se obvykle spustí v domovskému adresáři uživatele.

```
PS> Get-Location

Path
----
C:\Documents and Settings\PowerUser
```

> [!NOTE]
> Slovo *zásobníku* má zvláštní význam v mnoha programovací nastavení, včetně rozhraní .NET Framework. Poslední položky, které vložíte do zásobníku jako fyzické zásobníky položek, je první položka, který můžete použít ze zásobníku. Přidání položky do zásobníku se colloquially označuje jako "vkládání" položky do zásobníku. Stahování položky ze zásobníku se colloquially označuje jako "odebrání" položku ze zásobníku.

Chcete-li nabízená aktuální umístění do zásobníku a pak přejděte do složky místní nastavení, zadejte:

```powershell
Push-Location -Path "Local Settings"
```

Potom můžete posouvat nastavení místního umístění do zásobníku a a přesuňte do dočasné složky zadáním:

```powershell
Push-Location -Path Temp
```

Můžete ověřit, že jste změnili adresáře zadáním **Get-umístění** příkaz:

```
PS> Get-Location

Path
----
C:\Documents and Settings\PowerUser\Local Settings\Temp
```

Můžete se zpět do naposledy navštívené adresáře zadáním pak pop **umístění Pop** příkazů a změnu ověřit tak, že zadáte **Get-umístění** příkaz:

```
PS> Pop-Location
PS> Get-Location

Path
----
C:\Documents and Settings\me\Local Settings
```

Jenom jako s **nastavení umístění** rutiny, můžete zahrnout **- PassThru** parametr při zadání **umístění Pop** rutiny zobrazíte adresáře, který jste zadali:

```
PS> Pop-Location -PassThru

Path
----
C:\Documents and Settings\PowerUser
```

Můžete taky rutiny umístění s síťových cest. Pokud máte server s názvem FS01 se sdílenou složku s názvem veřejné, vaše umístění můžete změnit zadáním

```powershell
Set-Location \\FS01\Public
```

nebo

```powershell
Push-Location \\FS01\Public
```

Můžete použít **nabízené umístění** a **nastavení umístění** příkazy a změňte umístění na všechny dostupnou jednotku. Například pokud máte místní jednotku CD-ROM s písmenem jednotky D, který obsahuje datový disk CD, můžete změnit umístění na jednotce CD zadáním **D: nastavení umístění** příkaz.

Pokud jednotku je prázdná, zobrazí se následující chybová zpráva:

```
PS> Set-Location D:
Set-Location : Cannot find path 'D:\' because it does not exist.
```

Pokud používáte rozhraní příkazového řádku, není vhodné Průzkumníkovi souborů zkontrolujte dostupné fyzické disky. Průzkumníka souborů můžete by také zobrazit všechna jednotek prostředí Windows PowerShell. Prostředí Windows PowerShell poskytuje sadu příkazů pro manipulaci s jednotky prostředí Windows PowerShell a se věnuje tyto další.