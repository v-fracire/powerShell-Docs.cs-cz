---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Použití známých názvů příkazů
ms.assetid: 021e2424-c64e-4fa5-aa98-aa6405758d5d
ms.openlocfilehash: 37fc6dfad5a2f1363254744141dcab1e13aa5066
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="using-familiar-command-names"></a>Použití známých názvů příkazů
Pomocí mechanismus názvem *aliasy*, prostředí Windows PowerShell umožňuje uživatelům k odkazování na příkazy alternativní názvy. Aliasy umožňuje uživatelům s prostředí v jiné součásti pro běžné názvy příkazů, které již znáte k provádění podobných operací v prostředí Windows PowerShell znovu použít. I když nebude prostředí Windows PowerShell aliasy podrobně probereme, můžete je je stále používat, jak začít pracovat v prostředí Windows PowerShell.

Aliasy přidruží název příkazu, který zadáte jiný příkaz. Například prostředí Windows PowerShell má interní funkci s názvem **Clear-Host** který vymaže okně výstupu. Pokud zadáte buď **specifikací cls** nebo **vymazat** příkaz na příkazovém řádku prostředí Windows PowerShell interpretuje, že se jedná o alias **Clear-Host** funkce a spustí  **Clear-Host** funkce.

Tato funkce vám pomůže uživatelům další prostředí Windows PowerShell. První, většina uživatelů Cmd.exe a UNIX má velký rozsah příkazy, které uživatelé již znáte podle názvu a i když prostředí Windows PowerShell ekvivalenty nemusí poskytovat stejné výsledky, jsou dostatečně Zavřít ve formuláři, který uživatelé mohou používat pracovat bez nutnosti nejprve pamatovat názvy prostředí Windows PowerShell. Druhou hlavní zdroj před dozvědět nové prostředí, pokud je uživatel již obeznámeni s jinou prostředí, je chyby, které jsou způsobeny "prstem paměti". Pokud jste použili Cmd.exe let, když máte úplná výstupu na obrazovku a chcete jej vyčistit, reflexively zadejte **specifikací cls** příkaz a stiskněte klávesu ENTER. Bez zástupce pro **Clear-Host** funkce v prostředí Windows PowerShell, jednoduše zobrazí chybová zpráva "**'specifikací cls' nebyl rozpoznán jako rutiny, funkce, spustitelného programu nebo souboru skriptu.**" a být ponecháno s žádné představu o tom, co dělat, zrušte výstup.

Toto je stručný seznam běžných Cmd.exe a UNIX příkazy, které můžete použít v prostředí Windows PowerShell:

|||||
|-|-|-|-|
|CAT|Dir|připojení|rm|
|cd|zobrazení výsledků|Přesunutí|rmdir –|
|chdir –|vymazání|popd|Přejít do režimu spánku|
|Zrušte zaškrtnutí|h|ps|Řazení|
|specifikací CLS|Historie|pushd|typu t|
|Kopírování|příkaz kill|pwd|typ|
|del|lp|r|zápis|
|diff|ls|ren||

Pokud se přistihnete pomocí jedné z těchto příkazů reflexively a chcete se dozvědět skutečné jméno nativní příkazu prostředí Windows PowerShell, můžete použít **Get-Alias** příkaz:

```
PS> Get-Alias cls

CommandType     Name                            Definition
-----------     ----                            ----------
Alias           cls                             Clear-Host
```

Chcete-li příklady lépe čitelný, Průvodce uživatele systému Windows PowerShell obecně nevyužívá aliasy. Ale zároveň budete vědět více o aliasech již v rané fázi můžete stále bude užitečné, pokud pracujete s libovolnými fragmenty kódu prostředí Windows PowerShell z jiného zdroje nebo chcete definovat vlastní aliasy. Zbývající část tohoto oddílu popisuje standardní aliasy a jak definovat vlastní aliasy.

### <a name="interpreting-standard-aliases"></a>Interpretace standardní aliasy
Na rozdíl od zástupci popsané výše, které byly navrženy pro název kompatibilitu s dalších rozhraní, jsou navrženy pro jako stručný výtah obecně aliasy integrovaný do prostředí Windows PowerShell. Názvy těchto kratší lze rychle zadat, ale není možné číst, pokud si nejste jisti, co použijí pro referenci.

Prostředí Windows PowerShell se pokusí ohrozit mezi přehlednost a jako stručný výtah tím, že poskytuje sadu standardní aliasy, které jsou založeny na názvy sdružená vlastnost pro běžné operace a podstatná jména. To umožňuje základní sady aliasy pro běžné rutin, které jsou čitelný, když znáte názvy sdružená. Například v standardní aliasy příkaz **získat** je zkratka **g**, příkaz **nastavit** je zkratka **s**, podstatné jméno **Položky** je zkratka **i**, podstatným jménem **umístění** je zkratka **l**a podstatné jméno příkaz je zkratka **cm**.

Zde je stručný příklad k objasnění, jak to funguje. Standardní aliasu pro Get-Item pochází z kombinování **g** pro Get a **i** pro položku: **grafického rozhraní**. Standardní aliasu pro sadu položek pochází z kombinování **s** pro sadu a **i** pro položku: **si**. Standardní aliasu pro Get-umístění pochází z kombinování **g** pro Get a **l** k umístění, **gl**. Standardní aliasu pro nastavení umístění pochází z kombinování **s** pro sadu a **l** k umístění, **sl**. Standardní aliasu pro Get-Command pochází z kombinování **g** pro Get a **cm** pro příkaz, **gcm**. Neexistuje žádné rutiny Set-Command, ale pokud nebyly, jsme budou moci snadno uhodnout, že standardní alias pochází z **s** pro sadu a **cm** pro příkaz: **scm**. Kromě toho uživatelé obeznámeni s aliasy prostředí Windows PowerShell, který dojde **scm** budou moci snadno uhodnout, že alias odkazuje na příkazu Set.

### <a name="creating-new-aliases"></a>Vytvoření nové aliasy
Můžete vytvořit vlastní aliasy pomocí rutiny Set-Alias. Můžete například vytvořit následující příkazy aliasy standardní rutiny popsané v interpretace standardní aliasy:

```
Set-Alias -Name gi -Value Get-Item
Set-Alias -Name si -Value Set-Item
Set-Alias -Name gl -Value Get-Location
Set-Alias -Name sl -Value Set-Location
Set-Alias -Name gcm -Value Get-Command
```

Interně používá příkazy, jako je to při spuštění prostředí Windows PowerShell, ale tyto aliasy nejsou změnit. Pokud se pokusíte provést jednu z těchto příkazů ve skutečnosti, obdržíte chybu, která vysvětluje, že nemůže být upraven alias. Příklad:

```
PS> Set-Alias -Name gi -Value Get-Item
Set-Alias : Alias is not writeable because alias gi is read-only or constant and cannot be written to.
At line:1 char:10
+ Set-Alias  <<<< -Name gi -Value Get-Item
```