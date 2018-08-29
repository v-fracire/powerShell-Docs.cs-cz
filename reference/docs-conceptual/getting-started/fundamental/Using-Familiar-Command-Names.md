---
ms.date: 08/27/2018
keywords: rutiny prostředí PowerShell
title: Použití známých názvů příkazů
ms.assetid: 021e2424-c64e-4fa5-aa98-aa6405758d5d
ms.openlocfilehash: 08402aa5b959711c150fff89aa6747b6b43f8aa8
ms.sourcegitcommit: 59727f71dc204785a1bcdedc02716d8340a77aeb
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/28/2018
ms.locfileid: "43134079"
---
# <a name="using-familiar-command-names"></a>Použití známých názvů příkazů

PowerShell podporuje aliasy jako reference k příkazům alternativní názvy. Aliasy umožňuje uživatelům s prostředím v jiné prostředí používat běžné názvy příkazů, které už znáte podobných operací v prostředí PowerShell.

Aliasy přiřadí nový název jiného příkazu. Například Powershellu má vnitřní funkci s názvem `Clear-Host` , který vymaže v okně výstup. Můžete zadat buď `cls` nebo `clear` alias příkazového řádku. Interpretuje tyto aliasy prostředí PowerShell a běží `Clear-Host` funkce.

Tato funkce pomáhá uživatelům předvést prostředí PowerShell. První, většina uživatelů Cmd.exe a Unix mít velký repertoáru příkazů, které uživatelé již znáte pod názvem. Ekvivalenty Powershellu nemusí vytvářet identické výsledky. Výsledky jsou však zavřít dostatek, které uživatelé můžou pracovat bez znalosti názvu příkazu prostředí PowerShell. "Prsty paměti" je jiný hlavní příčiny frustrace při učení nové příkazové okno. Pokud jste použili Cmd.exe let, můžete například reflexively zadat `cls` příkaz pro vymazání obrazovky. Bez aliasu pro `Clear-Host`, zobrazí se chybová zpráva a nebude vědět, co dělat, zrušte výstup.

Následující seznam uvádí některé běžné Cmd.exe a Unix, které můžete použít příkazy v prostředí PowerShell:

|||||
|-|-|-|-|
|CAT|adresář|připojení|Správce prostředků|
|CD|echo|Přesunutí|rmdir|
|chdir|Vymazání|popd|Přejít do režimu spánku|
|Vymazat|H|PS|Řazení|
|specifikace CLS|Historie|pushd|TEE|
|Kopírování|ukončit|PWD|typ|
|del|LP|r|zápis|
|diff|Ls|ren||

`Get-Alias` Rutiny se dozvíte, skutečným názvem nativní příkaz prostředí PowerShell, které jsou spojené s aliasem.

```powershell
PS> Get-Alias cls
```

```Output
CommandType     Name                               Version    Source
-----------     ----                               -------    ------
Alias           cls -> Clear-Host
```

## <a name="interpreting-standard-aliases"></a>Interpretace standardní aliasy

Aliasy jsme popisuje předchozí byly navrženy pro název kompatibilitu s další příkazových prostředích systémů.
Většina aliasy, které jsou integrované do prostředí PowerShell jsou navržené pro zkrácení. Je snazší typu, ale jsou obtížně čitelné, pokud neznáte odkazují na kratší názvy.

Aliasy prostředí PowerShell se pokusí najít kompromis mezi jasné a zkrácení. PowerShell používá standardní sadu aliasy pro běžné podstatná jména a příkazy.

Příklad zkratky:

| Podstatné jméno nebo příkaz | Zkratka |
|--------------|--------------|
| Get          | G            |
| Nastavit          | s            |
| Položka         | Můžu            |
| Umístění     | L            |
| Příkaz      | cm           |
| Alias        | Al           |

Tyto aliasy jsou srozumitelné, když víte, zkrácené názvy.

| Název rutiny    | Alias |
|----------------|-------|
| `Get-Item `    | grafického rozhraní    |
| `Set-Item`     | si    |
| `Get-Location` | GL    |
| `Set-Location` | SL    |
| `Get-Command`  | gcm   |
| `Get-Alias`    | GAL   |

Jakmile jste obeznámeni s aliasy prostředí PowerShell, je snadno uhodnutelné, který **sal** alias odkazuje na `Set-Alias`.

## <a name="creating-new-aliases"></a>Vytváří se nový aliasy

Můžete vytvořit vlastní aliasy pomocí `Set-Alias` rutiny. Například následující příkazy vytvoří standardní rutiny aliasy jsme uvedli:

```powershell
Set-Alias -Name gi -Value Get-Item
Set-Alias -Name si -Value Set-Item
Set-Alias -Name gl -Value Get-Location
Set-Alias -Name sl -Value Set-Location
Set-Alias -Name gcm -Value Get-Command
```

Interně prostředí PowerShell používá podobné příkazy během spouštění, ale nejsou změnit tyto aliasy.
Pokud se pokusíte provést jednu z těchto příkazů, obdržíte chybu s vysvětlením, že alias nelze upravit. Příklad:

```
PS> Set-Alias -Name gi -Value Get-Item
Set-Alias : Alias is not writeable because alias gi is read-only or constant and cannot be written to.
At line:1 char:10
+ Set-Alias  <<<< -Name gi -Value Get-Item
```