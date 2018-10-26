# <a name="microsoft-open-source-code-of-conduct"></a>Pravidla chování pro Microsoft Open Source

Tento projekt se řídí [Pravidly chování pro Microsoft Open Source](https://opensource.microsoft.com/codeofconduct/).
Další informace najdete na stránce s [nejčastějšími dotazy k Pravidlům chování](https://opensource.microsoft.com/codeofconduct/faq/), případně se můžete obrátit na [opencode@microsoft.com](mailto:opencode@microsoft.com), pokud máte další otázky nebo komentáře.

[![Stav sestavení](https://ci.appveyor.com/api/projects/status/onshefxnc4g4pv87/branch/staging?svg=true)](https://ci.appveyor.com/project/PowerShell/powershell-docs/branch/staging)

## <a name="powershell-documentation"></a>Dokumentace k prostředí PowerShell

Vítejte v úložišti prostředí PowerShell Docs, bydlení oficiální dokumentaci k Powershellu.

## <a name="repository-structure"></a>Struktura úložiště

Každý z následující složky nejvyšší úrovně v tomto úložišti obsahuje sady DocSet, který je publikován do [Microsoft Docs](https://docs.microsoft.com/powershell).

- [/Developer/](https://docs.microsoft.com/powershell/developer/) je budoucí Domovská stránka dokumentace ke službě SDK prostředí PowerShell
  - Průběžně migrujeme tohoto obsahu z MSDN
- [/DSC/](https://docs.microsoft.com/powershell/dsc/) je pro funkci Desired State Configuration
- [/Gallery/](https://docs.microsoft.com/powershell/gallery) je [Galerie prostředí PowerShell](https://www.powershellgallery.com/)
- [/jea/](https://docs.microsoft.com/powershell/jea/) je pro funkci Just Enough Administration
- [/Reference/](https://docs.microsoft.com/powershell/scripting/) je pro koncepční témata prostředí PowerShell a odkaz na modul napříč verze 3.0, 4.0, 5.0, 5.1 a 6.0
  - Tento obsah je také zdroj obsahu nápovědy načítána `Get-Help` rutiny
- [/WMF](https://docs.microsoft.com/powershell/wmf/readme) obsahuje zprávu k vydání verze pro Windows Management Framework, balíček, který slouží k distribuci nové verze prostředí PowerShell na předchozích verzích Windows.

## <a name="contributing"></a>Přispívání

Příspěvky do tohoto úložiště prostřednictvím sloučíme aktivně [žádosti o přijetí změn](https://help.github.com/articles/using-pull-requests/) do *pracovní* větve.
Mějte prosím na paměti, že odešlete žádost o přijetí změn je nutné nejprve [licenční smlouvou o příspěvcích](https://cla.microsoft.com/) tak, aby byl v komunitě můžete používat vaše příspěvky.

Další informace o přispívání, přečtěte si naše [příručky pro přispěvatele](CONTRIBUTING.md).
Příručky pro přispěvatele obsahuje podrobné informace o tom, jak přispívat dokumentaci, navrhované nástroje a styl a formátování požadavky.
Použijte prosím problém a žádostí o přijetí změn šablony k udržení dokumentaci konzistentní napříč verzemi.

## <a name="licenses"></a>Licence

Existují dva soubory s licencí pro tento projekt.
Licence MIT se vztahuje na kód obsažený v tomto úložišti.
Licence Creative Commons license platí v dokumentaci.