# <a name="advanced-dsc-authoring-for-composition-and-collaboration"></a>Pokročilé vytváření složení a spolupráci DSC

Tento článek popisuje typy přístupů k dispozici pro kombinování konfigurací a prostředků.
Cíl pro každý scénář je stejný, snižuje složitost, pokud upřednostňované více konfigurací k dosažení serveru koncový stav nasazení.
Příkladem tohoto objektu může být několik týmů podílejících se na výsledek nasazení na server, jako je například vlastníka aplikace zachování stavu aplikace a centrální tým uvolnění změny základní nastavení zabezpečení.
Je podrobně popsaný detailů každý přístup, včetně výhod a rizik.

![Kanál](images/Pipeline.jpg)

## <a name="types-of-collaborative-authoring-techniques"></a>Typy spolupráce pro vytváření techniky

Existují dvě řešení vytvořené místní nástroje Configuration Manager povolit tento koncept:

| Koncept | Podrobné informace
|-|-
| Částečné konfigurace | [Dokumentace ke službě](partialconfigs.md)
| Složené prostředky | [Dokumentace ke službě](authoringresourcecomposite.md)

## <a name="understanding-the-impact-of-each-approach"></a>Principy vlivu obou těchto přístupů

Některé z těchto řešení je možné spravovat výsledek nasazení na server.
Je však značný dopad každý přístup.

## <a name="partial-configurations"></a>Částečné konfigurace

Při použití částečné konfigurace Local Configuration Manageru je nakonfigurován ke správě více konfigurací nezávisle na sobě.
Konfigurace jsou zkompilovány nezávisle a posléze přiřazeny k uzlu.
To vyžaduje LCM předem nakonfigurovat název každé konfigurace.

![PartialConfiguration](images/PartialConfiguration.jpg)

Částečné konfigurace poskytují dvě nebo více, týmy úplnou kontrolu nad konfigurací serveru, často bez výhodou komunikaci nebo spolupráci.

Zákazníkům poskytli zpětnou vazbu, která to může způsobit konflikty prostředků, neúmyslné přepsání a nakonec i ke ztrátě true konfigurace ovládacího prvku prostředku.

Kromě toho zákazníci poskytli zpětnou vazbu, že při použití tohoto modelu, každý řídicí změny konfigurace týmy by problém nahlásili plně otestovat přes kanál pro vydávání verzí, což vede k neočekávaným výsledkům v produkčním prostředí.

**Je velmi důležité, že jeden kanál použije k vyhodnocení, všechny změny verze na servery.**

Na následující ilustraci tým B uvolní jejich částečné konfigurace do týmu a týmu A pak spustí jejich testy na serveru s obě konfigurace použité.
V tomto modelu má pouze jeden autority oprávnění k provádění změn v produkčním prostředí.

![PartialSinglePipeline](images/PartialSinglePipeline.jpg)

Když jsou změny dělat tým B, by měl odesílání žádostí o přijetí změn pro tým A jeho zdrojový ovládací prvek prostředí.
Tým A by pak zkontrolujte změny pomocí automatizace testování a produkční verzi po spolehnout, že změny nebude způsobovat chyby v aplikacím nebo službám, které jsou hostované na daném serveru.

## <a name="composite-resources"></a>Složené prostředky

Složený prostředek je jednoduše konfigurace DSC lze zabalit jako prostředek.
Neexistují žádné zvláštní požadavky pro konfiguraci LCM tak, aby přijímal složené prostředky.
Prostředky se používají v rámci nové konfigurace a výsledky kompilace jednotlivých v jednom souboru MOF.

![CompositeResource](images/CompositeResource.jpg)

Existují dva běžné scénáře pro složené prostředky.
První je ke snížení složitosti a abstraktní jedinečné koncepty.
Druhá je umožnit směrných plánech a zabalené aplikace týmu bez obav nasadit prostřednictvím jejich kanál pro vydávání verzí do produkčního prostředí po všech testů bylo úspěšných.

```PowerShell
Configuration Name
{
  File 1
  {
    Ensure = “Present”
    Path = “c:\inetpub\file1.zip”
    Source = “http://uri/file1.zip”
  }
  Service A
  {
    Ensure = “Present”
    Name = “ServiceA”
    Status = “Running”
  }
  SecurityBaseline Settings
  {
    Ensure = “Present”
    Datacenter = “NorthAmerica”
  }
}
```

Složené prostředky podporovat složení a spolupráce pomocí kanálu při vytváření provozních splatnosti

Už používáte složené prostředky nevěděli ho.
Příkladem je **ServiceSet**.
Tento prostředek slouží ke správě stavu několik služeb, které Windows bez jejich uvedení v seznamu jednotlivě.
Vlastnost Name přijímá pole řetězců k poskytnutí názvu jednotlivých služeb.
Při kompilaci konfigurace MOF bude obsahovat jedinečný oddíl služby pro každou z názvů předaných ServiceSet.

Organizace můžou mít "agents" nebo "middleware", který musí být nainstalován na každém serveru.
Složený prostředek je nejlepší odpověď ke správě závislostí, instalaci a konfiguraci těchto nástrojů a pomůcek.

Osoba nebo tým odpovědný za řešení, které zahrnují více serverů autory konfigurace obsahující jejich požadavky.
V dalším kroku konfigurace by se zabalil jako složený prostředek podle pokynů uvedených v dokumentaci složených prostředků.
Nakonec by se měly zveřejňovat nový složený prostředek do umístění, jako jsou sdílené složky nebo NuGet informačního kanálu, kde aplikace týmy, které můžou využívat v jejich konfigurace.

Pokaždé, když tým vydání nové verze, že by zvýší číslo verze v manifestu modulu pro jejich složený prostředek.
Aplikační týmy zahrnují složených prostředků v konfiguraci, kterou vytváření pro správu závislostí aplikací.
Když týmy Operations/Security vydat novou verzi svého prostředku, oznámí aplikační týmy nové změny.

Aplikační týmy můžou aktivovat vydání do produkčního prostředí, kde pouze změny má směrné plány.
Nicméně to představuje příležitost k vyhodnocení dopadu na aplikace před riziko výpadku služby.

Poznámka: zpětnou vazbu týkající se použití složené prostředky je součástí kritice, provádění změn vyžaduje kompilaci a uvolněním nové MOF.
Toto chování je záměrné.
Každé nové verze konfigurace by měl obsahovat statický odkaz na konkrétní verzi každého prostředku a testy před dosažením produkční uzly serveru by měl být ověřen.
Proces testování a uvolnění změny ze správy zdrojového kódu vytvoří prostředí bezpečný pro uvolnění změnu v hodnotě malou, avšak často dávky.

Další informace o použití kanály pro vydávání ke správě základní infrastruktury, najdete v dokumentu White Paper: [Model kanálu The Release](http://aka.ms/thereleasepipelinemodel).
