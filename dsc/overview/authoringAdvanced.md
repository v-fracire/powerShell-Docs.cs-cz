---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Tvorba rozšířeného DSC pro skládání a spolupráci
ms.openlocfilehash: 3e40ba94de0a53c1c9663553c4ec443b5e0df3fd
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403848"
---
# <a name="advanced-dsc-authoring-for-composition-and-collaboration"></a><span data-ttu-id="a56c1-103">Tvorba rozšířeného DSC pro skládání a spolupráci</span><span class="sxs-lookup"><span data-stu-id="a56c1-103">Advanced DSC Authoring for Composition and Collaboration</span></span>

<span data-ttu-id="a56c1-104">Tento článek popisuje typy přístupů k dispozici pro kombinování konfigurací a prostředků.</span><span class="sxs-lookup"><span data-stu-id="a56c1-104">This article describes the types of approaches available for combining configurations and resources.</span></span>
<span data-ttu-id="a56c1-105">Cíl pro každý scénář je stejný, snižuje složitost, pokud upřednostňované více konfigurací k dosažení serveru koncový stav nasazení.</span><span class="sxs-lookup"><span data-stu-id="a56c1-105">The goal for each scenario is the same, to reduce complexity when multiple configurations are preferred to reach a server deployment end state.</span></span>
<span data-ttu-id="a56c1-106">Příkladem tohoto objektu může být několik týmů podílejících se na výsledek nasazení na server, jako je například vlastníka aplikace zachování stavu aplikace a centrální tým uvolnění změny základní nastavení zabezpečení.</span><span class="sxs-lookup"><span data-stu-id="a56c1-106">An example of this would be multiple teams contributing to the outcome of a server deployment, such as an application owner maintaining the application state and a central team releasing changes to security baselines.</span></span>
<span data-ttu-id="a56c1-107">Je podrobně popsaný detailů každý přístup, včetně výhod a rizik.</span><span class="sxs-lookup"><span data-stu-id="a56c1-107">The nuances of each approach including the benefits and risks are detailed here.</span></span>

![Kanál](../images/Pipeline.jpg)

## <a name="types-of-collaborative-authoring-techniques"></a><span data-ttu-id="a56c1-109">Typy spolupráce pro vytváření techniky</span><span class="sxs-lookup"><span data-stu-id="a56c1-109">Types of Collaborative Authoring Techniques</span></span>

<span data-ttu-id="a56c1-110">Existují dvě řešení vytvořené místní nástroje Configuration Manager povolit tento koncept:</span><span class="sxs-lookup"><span data-stu-id="a56c1-110">There are two solutions built in to Local Configuration Manager to enable this concept:</span></span>

| <span data-ttu-id="a56c1-111">Koncept</span><span class="sxs-lookup"><span data-stu-id="a56c1-111">Concept</span></span> | <span data-ttu-id="a56c1-112">Podrobné informace</span><span class="sxs-lookup"><span data-stu-id="a56c1-112">Detailed Information</span></span>
|-|-
| <span data-ttu-id="a56c1-113">Částečné konfigurace</span><span class="sxs-lookup"><span data-stu-id="a56c1-113">Partial Configurations</span></span> | [<span data-ttu-id="a56c1-114">Dokumentace ke službě</span><span class="sxs-lookup"><span data-stu-id="a56c1-114">Documentation</span></span>](../pull-server/partialConfigs.md)
| <span data-ttu-id="a56c1-115">Složené prostředky</span><span class="sxs-lookup"><span data-stu-id="a56c1-115">Composite Resources</span></span> | [<span data-ttu-id="a56c1-116">Dokumentace ke službě</span><span class="sxs-lookup"><span data-stu-id="a56c1-116">Documentation</span></span>](../resources/authoringResourceComposite.md)

## <a name="understanding-the-impact-of-each-approach"></a><span data-ttu-id="a56c1-117">Principy vlivu obou těchto přístupů</span><span class="sxs-lookup"><span data-stu-id="a56c1-117">Understanding The Impact of Each Approach</span></span>

<span data-ttu-id="a56c1-118">Některé z těchto řešení je možné spravovat výsledek nasazení na server.</span><span class="sxs-lookup"><span data-stu-id="a56c1-118">Either of these solutions can be used to manage the outcome of a server deployment.</span></span>
<span data-ttu-id="a56c1-119">Je však značný dopad každý přístup.</span><span class="sxs-lookup"><span data-stu-id="a56c1-119">However, there is significant difference in the impact of using each approach.</span></span>

## <a name="partial-configurations"></a><span data-ttu-id="a56c1-120">Částečné konfigurace</span><span class="sxs-lookup"><span data-stu-id="a56c1-120">Partial Configurations</span></span>

<span data-ttu-id="a56c1-121">Při použití částečné konfigurace Local Configuration Manageru je nakonfigurován ke správě více konfigurací nezávisle na sobě.</span><span class="sxs-lookup"><span data-stu-id="a56c1-121">When using Partial Configurations, Local Configuration Manager is configured to manage multiple configurations independently.</span></span>
<span data-ttu-id="a56c1-122">Konfigurace jsou zkompilovány nezávisle a posléze přiřazeny k uzlu.</span><span class="sxs-lookup"><span data-stu-id="a56c1-122">Configurations are compiled independently and then assigned to the node.</span></span>
<span data-ttu-id="a56c1-123">To vyžaduje LCM předem nakonfigurovat název každé konfigurace.</span><span class="sxs-lookup"><span data-stu-id="a56c1-123">This requires LCM to be configured in advance with the name of each configuration.</span></span>

![PartialConfiguration](../images/PartialConfiguration.jpg)

<span data-ttu-id="a56c1-125">Částečné konfigurace poskytují dvě nebo více, týmy úplnou kontrolu nad konfigurací serveru, často bez výhodou komunikaci nebo spolupráci.</span><span class="sxs-lookup"><span data-stu-id="a56c1-125">Partial Configurations provide two, or more, teams complete control over configuration of a server, often without the benefit of communication or collaboration.</span></span>

<span data-ttu-id="a56c1-126">Zákazníkům poskytli zpětnou vazbu, která to může způsobit konflikty prostředků, neúmyslné přepsání a nakonec i ke ztrátě true konfigurace ovládacího prvku prostředku.</span><span class="sxs-lookup"><span data-stu-id="a56c1-126">Customers have provided feedback that this can lead to resource conflicts, unintentional overrides, and ultimately loss of true configuration control of the asset.</span></span>

<span data-ttu-id="a56c1-127">Kromě toho zákazníci poskytli zpětnou vazbu, že při použití tohoto modelu, každý řídicí změny konfigurace týmy by problém nahlásili plně otestovat přes kanál pro vydávání verzí, což vede k neočekávaným výsledkům v produkčním prostředí.</span><span class="sxs-lookup"><span data-stu-id="a56c1-127">Additionally, customers have provided feedback that when using this model, each controlling teams configuration changes are unlikely to be fully tested through a release pipeline, leading to unexpected results in production.</span></span>

<span data-ttu-id="a56c1-128">**Je velmi důležité, že jeden kanál použije k vyhodnocení, všechny změny verze na servery.**</span><span class="sxs-lookup"><span data-stu-id="a56c1-128">**It is critical that a single pipeline be used to evaluate all changes release to servers.**</span></span>

<span data-ttu-id="a56c1-129">Na následující ilustraci tým B uvolní jejich částečné konfigurace do týmu a týmu A pak spustí jejich testy na serveru s obě konfigurace použité.</span><span class="sxs-lookup"><span data-stu-id="a56c1-129">In the illustration below, Team B releases their partial configuration to Team A. Team A then runs their tests against a server with both configurations applied.</span></span>
<span data-ttu-id="a56c1-130">V tomto modelu má pouze jeden autority oprávnění k provádění změn v produkčním prostředí.</span><span class="sxs-lookup"><span data-stu-id="a56c1-130">In this model, only one authority has permission to make changes in production.</span></span>

![PartialSinglePipeline](../images/PartialSinglePipeline.jpg)

<span data-ttu-id="a56c1-132">Když jsou změny dělat tým B, by měl odesílání žádostí o přijetí změn pro tým A jeho zdrojový ovládací prvek prostředí.</span><span class="sxs-lookup"><span data-stu-id="a56c1-132">When changes are required from Team B, they should submit a Pull Request against Team A's source control environment.</span></span>
<span data-ttu-id="a56c1-133">Tým A by pak zkontrolujte změny pomocí automatizace testování a produkční verzi po spolehnout, že změny nebude způsobovat chyby v aplikacím nebo službám, které jsou hostované na daném serveru.</span><span class="sxs-lookup"><span data-stu-id="a56c1-133">Team A would then review the changes using test automation and release to production when there is confidence that the changes will not cause errors in the applications or services hosted by the server.</span></span>

## <a name="composite-resources"></a><span data-ttu-id="a56c1-134">Složené prostředky</span><span class="sxs-lookup"><span data-stu-id="a56c1-134">Composite Resources</span></span>

<span data-ttu-id="a56c1-135">Složený prostředek je jednoduše konfigurace DSC lze zabalit jako prostředek.</span><span class="sxs-lookup"><span data-stu-id="a56c1-135">A composite resource is simply a DSC Configuration packaged as a resource.</span></span>
<span data-ttu-id="a56c1-136">Neexistují žádné zvláštní požadavky pro konfiguraci LCM tak, aby přijímal složené prostředky.</span><span class="sxs-lookup"><span data-stu-id="a56c1-136">There are no special requirements for configuring LCM to accept composite resources.</span></span>
<span data-ttu-id="a56c1-137">Prostředky se používají v rámci nové konfigurace a výsledky kompilace jednotlivých v jednom souboru MOF.</span><span class="sxs-lookup"><span data-stu-id="a56c1-137">The resources are used within a new configuration and a single compilation results in one MOF file.</span></span>

![CompositeResource](../images/CompositeResource.jpg)

<span data-ttu-id="a56c1-139">Existují dva běžné scénáře pro složené prostředky.</span><span class="sxs-lookup"><span data-stu-id="a56c1-139">There are two common scenarios for composite resources.</span></span>
<span data-ttu-id="a56c1-140">První je ke snížení složitosti a abstraktní jedinečné koncepty.</span><span class="sxs-lookup"><span data-stu-id="a56c1-140">The first is to reduce complexity and abstract unique concepts.</span></span>
<span data-ttu-id="a56c1-141">Druhá je umožnit směrných plánech a zabalené aplikace týmu bez obav nasadit prostřednictvím jejich kanál pro vydávání verzí do produkčního prostředí po všech testů bylo úspěšných.</span><span class="sxs-lookup"><span data-stu-id="a56c1-141">The second is to allow baselines to be packaged for an application team to safely deploy through their release pipeline to production after all tests have passed.</span></span>

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

<span data-ttu-id="a56c1-142">Složené prostředky podporovat složení a spolupráce pomocí kanálu při vytváření provozních splatnosti</span><span class="sxs-lookup"><span data-stu-id="a56c1-142">Composite resources promote both composition and collaboration using a pipeline while building operational maturity</span></span>

<span data-ttu-id="a56c1-143">Už používáte složené prostředky nevěděli ho.</span><span class="sxs-lookup"><span data-stu-id="a56c1-143">You might be already using composite resources without realizing it.</span></span>
<span data-ttu-id="a56c1-144">Příkladem je **ServiceSet**.</span><span class="sxs-lookup"><span data-stu-id="a56c1-144">An example is **ServiceSet**.</span></span>
<span data-ttu-id="a56c1-145">Tento prostředek slouží ke správě stavu několik služeb, které Windows bez jejich uvedení v seznamu jednotlivě.</span><span class="sxs-lookup"><span data-stu-id="a56c1-145">This resource manages the state of multiple Windows Services without listing them individually.</span></span>
<span data-ttu-id="a56c1-146">Vlastnost Name přijímá pole řetězců k poskytnutí názvu jednotlivých služeb.</span><span class="sxs-lookup"><span data-stu-id="a56c1-146">The Name property accepts an array of strings to provide the name of each service.</span></span>
<span data-ttu-id="a56c1-147">Při kompilaci konfigurace MOF bude obsahovat jedinečný oddíl služby pro každou z názvů předaných ServiceSet.</span><span class="sxs-lookup"><span data-stu-id="a56c1-147">When the configuration is compiled, the MOF will contain a unique Service section for each of the Names passed to ServiceSet.</span></span>

<span data-ttu-id="a56c1-148">Organizace můžou mít "agents" nebo "middleware", který musí být nainstalován na každém serveru.</span><span class="sxs-lookup"><span data-stu-id="a56c1-148">Organizations might have "agents" or "middleware" that should be installed on every server.</span></span>
<span data-ttu-id="a56c1-149">Složený prostředek je nejlepší odpověď ke správě závislostí, instalaci a konfiguraci těchto nástrojů a pomůcek.</span><span class="sxs-lookup"><span data-stu-id="a56c1-149">A composite resource is the best answer to managing the dependencies, setup, and configuration of any such tools and utilities.</span></span>

<span data-ttu-id="a56c1-150">Osoba nebo tým odpovědný za řešení, které zahrnují více serverů autory konfigurace obsahující jejich požadavky.</span><span class="sxs-lookup"><span data-stu-id="a56c1-150">The person or team responsible for solutions that span multiple servers authors a configuration containing their requirements.</span></span>
<span data-ttu-id="a56c1-151">V dalším kroku konfigurace by se zabalil jako složený prostředek podle pokynů uvedených v dokumentaci složených prostředků.</span><span class="sxs-lookup"><span data-stu-id="a56c1-151">Next, the configuration would be packaged as a composite resource using instructions provided in the composite resource documentation.</span></span>
<span data-ttu-id="a56c1-152">Nakonec by se měly zveřejňovat nový složený prostředek do umístění, jako jsou sdílené složky nebo NuGet informačního kanálu, kde aplikace týmy, které můžou využívat v jejich konfigurace.</span><span class="sxs-lookup"><span data-stu-id="a56c1-152">Finally, the new composite resource should be published to a location such as a file share or NuGet feed where application teams can consume it in their configurations.</span></span>

<span data-ttu-id="a56c1-153">Pokaždé, když tým vydání nové verze, že by zvýší číslo verze v manifestu modulu pro jejich složený prostředek.</span><span class="sxs-lookup"><span data-stu-id="a56c1-153">Each time the team releases a new version, they would increment the version number in the module manifest for their composite resource.</span></span>
<span data-ttu-id="a56c1-154">Aplikační týmy zahrnují složených prostředků v konfiguraci, kterou vytváření pro správu závislostí aplikací.</span><span class="sxs-lookup"><span data-stu-id="a56c1-154">The application teams include the composite resource in the configuration they author for managing application dependencies.</span></span>
<span data-ttu-id="a56c1-155">Když týmy Operations/Security vydat novou verzi svého prostředku, oznámí aplikační týmy nové změny.</span><span class="sxs-lookup"><span data-stu-id="a56c1-155">When the Operations/Security teams release a new version of their resource, they notify the application teams of a new change.</span></span>

<span data-ttu-id="a56c1-156">Aplikační týmy můžou aktivovat vydání do produkčního prostředí, kde pouze změny má směrné plány.</span><span class="sxs-lookup"><span data-stu-id="a56c1-156">The application teams might trigger a release to production where the only change is to baselines.</span></span>
<span data-ttu-id="a56c1-157">Nicméně to představuje příležitost k vyhodnocení dopadu na aplikace před riziko výpadku služby.</span><span class="sxs-lookup"><span data-stu-id="a56c1-157">However, this provides an opportunity to evaluate impact to applications before risk of a service outage.</span></span>

<span data-ttu-id="a56c1-158">Poznámka: zpětnou vazbu týkající se použití složené prostředky je součástí kritice, provádění změn vyžaduje kompilaci a uvolněním nové MOF.</span><span class="sxs-lookup"><span data-stu-id="a56c1-158">Note - Feedback regarding the use of composite resources has included criticism that making changes requires compiling and releasing a new MOF.</span></span>
<span data-ttu-id="a56c1-159">Toto chování je záměrné.</span><span class="sxs-lookup"><span data-stu-id="a56c1-159">This is by design.</span></span>
<span data-ttu-id="a56c1-160">Každé nové verze konfigurace by měl obsahovat statický odkaz na konkrétní verzi každého prostředku a testy před dosažením produkční uzly serveru by měl být ověřen.</span><span class="sxs-lookup"><span data-stu-id="a56c1-160">Each new configuration release should include a static reference to a specific version of each resource, and should be validated by tests before reaching production server nodes.</span></span>
<span data-ttu-id="a56c1-161">Proces testování a uvolnění změny ze správy zdrojového kódu vytvoří prostředí bezpečný pro uvolnění změnu v hodnotě malou, avšak často dávky.</span><span class="sxs-lookup"><span data-stu-id="a56c1-161">The process of testing and releasing changes from source control creates a safe environment for releasing change in small but frequent batches.</span></span>

<span data-ttu-id="a56c1-162">Další informace o použití kanály pro vydávání ke správě základní infrastruktury najdete v dokumentu White Paper: [Model kanálu verze](../further-reading/whitepapers.md).</span><span class="sxs-lookup"><span data-stu-id="a56c1-162">For more information about using release pipelines to manage core infrastructure, see the whitepaper: [The Release Pipeline Model](../further-reading/whitepapers.md).</span></span>
