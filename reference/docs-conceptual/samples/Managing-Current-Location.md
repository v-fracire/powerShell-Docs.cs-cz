---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Správa aktuálního umístění
ms.assetid: a9f9e7a7-3ea8-47d3-bbb4-6e437f6d4a4a
ms.openlocfilehash: d1ebc9507a45841e6d4d8219e45c002990e1328c
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403838"
---
# <a name="managing-current-location"></a>Správa aktuálního umístění

Při navigaci systémy složku v Průzkumníku souborů, obvykle mají konkrétní pracovní umístění – konkrétně, aktuální otevřít složku. Položky v aktuální složce lze snadno ovládat klepnutím. Pro rozhraní příkazového řádku, jako je například Cmd.exe když jsou ve stejné složce jako soubor konkrétní můžete přistupovat ho zadání relativně krátký název, spíše než by bylo potřeba zadat celou cestu k souboru. Aktuální adresář je volána v pracovním adresáři.

Prostředí Windows PowerShell používá podstatným jménem **umístění** odkazovat do pracovního adresáře a implementuje řadu rutin k prozkoumání a manipulaci s umístěním.

### <a name="getting-your-current-location-get-location"></a>Získávání aktuální polohu (Get umístění)

Pokud chcete zjistit cestu aktuální umístění adresáře, zadejte **Get-umístění** příkaz:

```
PS> Get-Location
Path
----
C:\Documents and Settings\PowerUser
```

> [!NOTE]
> Rutina Get-umístění je podobná **pwd** příkazu v prostředí BASH. Rutina Set-umístění je podobná **cd** v Cmd.exe.

### <a name="setting-your-current-location-set-location"></a>Nastavení vašeho aktuálního umístění (nastavení umístění)

**Get-umístění** příkaz se používá s **nastavení umístění** příkazu. **Nastavení umístění** příkazu můžete zadat vaše aktuální umístění adresáře.

```powershell
Set-Location -Path C:\Windows
```

Po zadání příkazu, můžete si všimnout, neobdržíte žádné přímé zpětnou vazbu efekt příkazu. Většina příkazů prostředí Windows PowerShell, které provádějí akce vytvořit žádné nebo téměř žádné výstupní, protože není ve výstupu vždy užitečný. Chcete-li ověřit, že došlo ke změně úspěšné adresáře při zadání **nastavení umístění** příkazu, zahrnují **- PassThru** parametr při zadání **Set-umístění**příkaz:

```
PS> Set-Location -Path C:\Windows -PassThru

Path
----
C:\WINDOWS
```

**- PassThru** parametr je možné mnoho sady příkazů v prostředí Windows PowerShell k vrácení informací o výsledek v případech, ve kterých není žádný výchozí výstup.

Můžete určit cest vzhledem ke své aktuální polohy stejným způsobem jako vám by ve většině systému UNIX a Windows command Shell. Ve standardním zápisu pro relativní cesty tečku (**.**) představuje aktuální složky a dvojnásobná období (**...** ) představuje nadřazený adresář složky vašeho aktuálního umístění.

Například, pokud jste **C:\\Windows** složky, tečku (**.**) představuje **C:\\Windows** a dvakrát období (**...** ) představují **C:**. Můžete změnit z aktuálního umístění na kořenové jednotce C: zadáním:

```
PS> Set-Location -Path .. -PassThru

Path
----
C:\
```

Stejný postup funguje u jednotek Windows Powershellu, které nejsou jednotky systému souborů, jako například **HKLM:**. Můžete nastavit vaši polohu k HKLM\\softwarového klíče v registru tak, že zadáte:

```
PS> Set-Location -Path HKLM:\SOFTWARE -PassThru

Path
----
HKLM:\SOFTWARE
```

Dá se změnit umístění adresáře na nadřazeném adresáři, která je kořenem HKLM Windows Powershellu: jednotky pomocí relativní cesty:

```
PS> Set-Location -Path .. -PassThru

Path
----
HKLM:\
```

Můžete zadat nastavení umístění nebo použijte některý z předdefinovaných aliasy prostředí Windows PowerShell pro nastavení umístění (cd, chdir, sl). Příklad:

```powershell
cd -Path C:\Windows
```

```powershell
chdir -Path .. -PassThru
```

```powershell
sl -Path HKLM:\SOFTWARE -PassThru
```

### <a name="saving-and-recalling-recent-locations-push-location-and-pop-location"></a>Ukládání a vrací nedávných umístění (umístění nabízených oznámení a umístění Pop)

Při změně umístění, je vhodné zaznamenávat kdy byly a bude moct vrátit do předchozího umístění. **Nabízených umístění** rutiny v prostředí Windows PowerShell vytvoří seřazený historii ("zásobníku") adresář cesty, kde máte, a můžete krokovat zpět historie cesty k adresářům s využitím doplňující  **Umístění POP** rutiny.

Například prostředí Windows PowerShell se obvykle spouští domovského adresáře uživatele.

```
PS> Get-Location

Path
----
C:\Documents and Settings\PowerUser
```

> [!NOTE]
> Slovo *zásobníku* má zvláštní význam v mnoha programovacích nastavení, včetně rozhraní .NET Framework. Podobně jako fyzického zásobníku položky poslední položky, kterou chcete vložit do zásobníku je první položka, která si můžete vyžádat ze zásobníku. Přidání položky do zásobníku je colloquially označuje jako "doručením (push)" položky do zásobníku. Stahování položky ze zásobníku se colloquially označuje jako "vyjímání" položky ze zásobníku.

Pokud chcete vložit do aktuálního umístění do zásobníku a pak přejděte do složky místní nastavení, zadejte:

```powershell
Push-Location -Path "Local Settings"
```

Potom můžete vložit umístění místní nastavení do zásobníku a přejít ke složce Temp tak, že zadáte:

```powershell
Push-Location -Path Temp
```

Můžete ověřit, že jste změnili adresáře tak, že zadáte **Get-umístění** příkaz:

```
PS> Get-Location

Path
----
C:\Documents and Settings\PowerUser\Local Settings\Temp
```

Můžete se pak automaticky zpátky do naposledy navštívenému adresáři zadáním **umístění Pop** příkaz a zkontrolujte změnu tak, že zadáte **Get-umístění** příkaz:

```
PS> Pop-Location
PS> Get-Location

Path
----
C:\Documents and Settings\me\Local Settings
```

Stejně jako u **nastavení umístění** rutiny, můžete zahrnout **- PassThru** parametr při zadání **umístění Pop** rutiny adresáře, který jste zadali:

```
PS> Pop-Location -PassThru

Path
----
C:\Documents and Settings\PowerUser
```

Můžete také použít rutiny umístění s síťových cest. Pokud máte server s názvem FS01 se do sdílené složky s názvem veřejné své umístění můžete změnit tak, že zadáte

```powershell
Set-Location \\FS01\Public
```

nebo

```powershell
Push-Location \\FS01\Public
```

Můžete použít **nabízených umístění** a **nastavení umístění** příkazy a změňte umístění pro všechny dostupnou jednotku. Například pokud máte místní jednotku CD-ROM s písmenem jednotky D, která obsahuje datový disk CD, můžete změnit umístění na jednotce CD tak, že zadáte **D: nastavení umístění** příkazu.

Pokud jednotka je prázdná, zobrazí se následující chybová zpráva:

```
PS> Set-Location D:
Set-Location : Cannot find path 'D:\' because it does not exist.
```

Při použití rozhraní příkazového řádku, není vhodné používat Průzkumníka souborů pro zjištění dostupné fyzické disky. Také Průzkumníka souborů by ukazují, všechny jednotky prostředí Windows PowerShell. Prostředí Windows PowerShell poskytuje sadu příkazů pro zpracování jednotky Windows Powershellu a mluvíme o tyto další.
