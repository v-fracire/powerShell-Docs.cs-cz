---
ms.date: 10/13/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Přehled platformy Desired State Configuration pro techniky
ms.openlocfilehash: 0e599c2218cd2df29dbd0529006be5e1ef17ce5f
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403864"
---
# <a name="desired-state-configuration-overview-for-engineers"></a><span data-ttu-id="98a86-103">Přehled platformy Desired State Configuration pro techniky</span><span class="sxs-lookup"><span data-stu-id="98a86-103">Desired State Configuration Overview for Engineers</span></span>

<span data-ttu-id="98a86-104">Tento dokument je určený pro vývojáře provozní týmy a týmy pochopíte výhody z prostředí PowerShell Desired State Configuration (DSC).</span><span class="sxs-lookup"><span data-stu-id="98a86-104">This document is intended for developer and operations teams to understand the benefits of PowerShell Desired State Configuration (DSC).</span></span>
<span data-ttu-id="98a86-105">Pro vyšší úroveň zobrazení hodnoty DSC poskytuje, najdete [Desired State Configuration přehled pro pracovníky s rozhodovací pravomocí](decisionMaker.md)</span><span class="sxs-lookup"><span data-stu-id="98a86-105">For a higher level view of the value DSC provides, please see [Desired State Configuration Overview for Decision Makers](decisionMaker.md)</span></span>

## <a name="benefits-of-desired-state-configuration"></a><span data-ttu-id="98a86-106">Výhody Desired State Configuration</span><span class="sxs-lookup"><span data-stu-id="98a86-106">Benefits of Desired State Configuration</span></span>

<span data-ttu-id="98a86-107">DSC neexistuje:</span><span class="sxs-lookup"><span data-stu-id="98a86-107">DSC exists to:</span></span>

- <span data-ttu-id="98a86-108">Zjednodušte skriptování ve Windows</span><span class="sxs-lookup"><span data-stu-id="98a86-108">Decrease the complexity of scripting in Windows</span></span>
- <span data-ttu-id="98a86-109">Zvýšení rychlosti iterace</span><span class="sxs-lookup"><span data-stu-id="98a86-109">Increase the speed of iteration</span></span>

<span data-ttu-id="98a86-110">Pojem "průběžné nasazování" je stále důležitější.</span><span class="sxs-lookup"><span data-stu-id="98a86-110">The concept of "continuous deployment" is becoming more important.</span></span>
<span data-ttu-id="98a86-111">Průběžné nasazování znamená možnost nasazení často, potenciálně mnohokrát za den.</span><span class="sxs-lookup"><span data-stu-id="98a86-111">Continuous deployment means the ability to deploy frequently, potentially many times per day.</span></span>
<span data-ttu-id="98a86-112">Účelem těchto nasazeních není nějakou opravu, ale něco publikovaly rychle získat.</span><span class="sxs-lookup"><span data-stu-id="98a86-112">The purpose of these deployments are not to fix something but to get something published quickly.</span></span>
<span data-ttu-id="98a86-113">Získávání nových funkcí prostřednictvím vývoje do operace bezproblémovému a spolehlivě, jako je to možné, můžete snížit dobu realizace nové obchodní logiky.</span><span class="sxs-lookup"><span data-stu-id="98a86-113">By getting new features through development into operation as smoothly and reliably as possible, you reduce time-to-value of new business logic.</span></span>

<span data-ttu-id="98a86-114">Přesunout na cloud computingu implikuje nasazení řešení, které využívá model "deklarativní" šablony, kde je koncový stav prostředí deklarované jako text a publikují do modulu nasazení.</span><span class="sxs-lookup"><span data-stu-id="98a86-114">The move towards cloud computing implies a deployment solution that utilizes a "declarative" template model, where an end state environment is declared as text and published to a deployment engine.</span></span>
<span data-ttu-id="98a86-115">Tento postup nasazení umožňuje rychlé změny ve velkém měřítku, s odolnost proti selhání hrozeb vzhledem k tomu, že v okamžiku nasazení můžete konzistentně opakovat zajistit koncového stavu.</span><span class="sxs-lookup"><span data-stu-id="98a86-115">This deployment technique allows for rapid change, at scale, with resilience against threat of failure because at any time the deployment can be consistently repeated to guarantee an end state.</span></span>
<span data-ttu-id="98a86-116">Vytvoření nástrojů a služeb, které podporují tento styl operace, ať už automation je odpovědí na tyto změny.</span><span class="sxs-lookup"><span data-stu-id="98a86-116">The creation of tools and services that support this style of operations through automation is a response to these changes.</span></span>

<span data-ttu-id="98a86-117">DSC je platforma, která poskytuje deklarativní a nasazení (opakovatelné) idempotentní, konfigurace a přizpůsobení.</span><span class="sxs-lookup"><span data-stu-id="98a86-117">DSC is a platform that provides declarative and idempotent (repeatable) deployment, configuration and conformance.</span></span>
<span data-ttu-id="98a86-118">Platforma DSC umožňuje součástí vašeho datového centra zajistit správnou konfiguraci, která zabraňuje chybám a zabraňuje chybám při nasazování nákladné.</span><span class="sxs-lookup"><span data-stu-id="98a86-118">The DSC platform enables you to ensure that the components of your data center have the correct configuration, which avoids errors and prevents costly deployment failures.</span></span>
<span data-ttu-id="98a86-119">DSC podle konfigurace DSC se zpracuje jako část kódu aplikace, umožňuje průběžné nasazování.</span><span class="sxs-lookup"><span data-stu-id="98a86-119">By treating DSC configurations as part of application code, DSC enables continuous deployment.</span></span>
<span data-ttu-id="98a86-120">Konfigurace DSC se musí aktualizovat jako součást aplikace zajišťující, že znalosti potřebné k nasazení aplikace je vždy aktuální a připravená k použití.</span><span class="sxs-lookup"><span data-stu-id="98a86-120">The DSC configuration should be updated as a part of the application, ensuring that the knowledge needed to deploy the application is always up-to-date and ready to be used.</span></span>

## <a name="i-have-powershell-why-do-i-need-desired-state-configuration"></a><span data-ttu-id="98a86-121">"Mám prostředí PowerShell, proč je nutné Desired State Configuration?"</span><span class="sxs-lookup"><span data-stu-id="98a86-121">"I have PowerShell, why do I need Desired State Configuration?"</span></span>

<span data-ttu-id="98a86-122">Záměr samostatné konfigurace DSC nebo "co chci provést", spuštění nebo "jak chci udělat."</span><span class="sxs-lookup"><span data-stu-id="98a86-122">DSC configurations separate intent, or "what I want to do", from execution, or "how I want to do it."</span></span>
<span data-ttu-id="98a86-123">To znamená, že logika zpracování je obsažen v prostředcích.</span><span class="sxs-lookup"><span data-stu-id="98a86-123">This means the logic of execution is contained within the resources.</span></span>
<span data-ttu-id="98a86-124">Uživatelé nebudou mít k určení, jak implementovat nebo nasadit funkci, když prostředek DSC této funkce je k dispozici.</span><span class="sxs-lookup"><span data-stu-id="98a86-124">Users do not have to know how to implement or deploy a feature when a DSC resource for that feature is available.</span></span>
<span data-ttu-id="98a86-125">To mu umožní se zaměřují na strukturu jejich nasazení.</span><span class="sxs-lookup"><span data-stu-id="98a86-125">This allows the user to focus on the structure of their deployment.</span></span>

<span data-ttu-id="98a86-126">Jako příklad skripty prostředí PowerShell by měl vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="98a86-126">As an example, PowerShell scripts should look like this:</span></span>
```powershell
# Create a share in Windows Server 8
New-SmbShare -Name MyShare -Path C:\Demo\Temp -FullAccess Alice -ReadAccess Bob
```
<span data-ttu-id="98a86-127">Tento skript je jednoduché, srozumitelné a jednoduché.</span><span class="sxs-lookup"><span data-stu-id="98a86-127">This script is simple, comprehensible, and straightforward.</span></span>
<span data-ttu-id="98a86-128">Ale pokud se pokusíte vložení tohoto skriptu do produkčního prostředí, budete spouštět na několik problémů.</span><span class="sxs-lookup"><span data-stu-id="98a86-128">However, if you try putting that script into production, you will run into several issues.</span></span>
<span data-ttu-id="98a86-129">Co se stane, když spuštění dvakrát za sebou skriptu?</span><span class="sxs-lookup"><span data-stu-id="98a86-129">What happens if that script is run twice in a row?</span></span>
<span data-ttu-id="98a86-130">Co se stane, pokud Bob dříve měli úplný přístup ke sdílené složce?</span><span class="sxs-lookup"><span data-stu-id="98a86-130">What happens if Bob previously had Full Access to the share?</span></span>

<span data-ttu-id="98a86-131">Jako kompenzaci za tyto problémy, bude vypadat blíž ke něco jako "real" verze skriptu:</span><span class="sxs-lookup"><span data-stu-id="98a86-131">To compensate for these issues, a "real" version of the script will look closer to something like:</span></span>
```powershell
# But actually creating a share in an idempotent way would be

$shareExists = $false
$smbShare = Get-SmbShare -Name $Name -ErrorAction SilentlyContinue
if($smbShare -ne $null)
{
    Write-Verbose -Message "Share with name $Name exists"
    $shareExists = $true
}

if ($shareExists -eq $false)
{
    Write-Verbose "Creating share $Name to ensure it is Present"
    New-SmbShare @psboundparameters
}
else
{
    # Need to call either Set-SmbShare or *ShareAccess cmdlets
    if ($psboundparameters.ContainsKey("ChangeAccess"))
    {
       #...etc, etc, etc
    }
}
```

<span data-ttu-id="98a86-132">Tento skript je složitější, s spoustu logiky a zpracování chyb.</span><span class="sxs-lookup"><span data-stu-id="98a86-132">This script is more complex, with plenty of logic and error handling.</span></span>
<span data-ttu-id="98a86-133">Skript je složitější, protože jsou již uvedením, co chcete Hotovo, ale *jak na to*.</span><span class="sxs-lookup"><span data-stu-id="98a86-133">The script is more complex because you are no longer stating what you want done, but *how to do it*.</span></span>

<span data-ttu-id="98a86-134">DSC umožňuje určit, co chcete Hotovo a logiku je abstrahovaný okamžitě.</span><span class="sxs-lookup"><span data-stu-id="98a86-134">DSC allows you to say what you want done, and the underlying logic is abstracted away.</span></span>

```powershell
# A configuration is a special kind of PowerShell function
Configuration Sample_Share
{
   Import-DscResource -Module xSmbShare
   # Nodes are the endpoint we wish to configure
   # A Configuration block can have zero or more Node blocks
   Node $NodeName
   {
      # Next, specify one or more resource blocks
      # Resources are simply PowerShell modules that
      # implement the logic of "how" to execute a task
      xSmbShare MySMBShare
      {
          Ensure      = "Present"
          Name        = "MyShare"
          Path        = "C:\Demo\Temp"
          ReadAccess  = "Bob"
          FullAccess  = "Alice"
          Description = "This is an updated description for this share"
      }
   }
}
#Run the function to compile the configuration
Sample_Share
#Pass the configuration to the nodes we defined and configure them
Start-DscConfiguration Sample_Share
```

<span data-ttu-id="98a86-135">Tento skript je čistě naformátovaný a je jednoduché ke čtení.</span><span class="sxs-lookup"><span data-stu-id="98a86-135">This script is cleanly formatted and straightforward to read.</span></span>
<span data-ttu-id="98a86-136">Jsou stále k dispozici v logické cesty a zpracování chyb [prostředků](../resources/resources.md) implementaci, ale neviditelné autorovi skriptu.</span><span class="sxs-lookup"><span data-stu-id="98a86-136">The logic paths and error handling are still present in the [resource](../resources/resources.md) implementation, but invisible to the script author.</span></span>

## <a name="separating-environment-from-structure"></a><span data-ttu-id="98a86-137">Oddělení prostředí ze struktury</span><span class="sxs-lookup"><span data-stu-id="98a86-137">Separating Environment from Structure</span></span>

<span data-ttu-id="98a86-138">Běžným vzorem v DevOps je, aby více prostředí pro nasazení.</span><span class="sxs-lookup"><span data-stu-id="98a86-138">A common pattern in DevOps is to have multiple environments for deployment.</span></span>
<span data-ttu-id="98a86-139">Například může být "dev" prostředí umožňuje rychle prototypu nový kód.</span><span class="sxs-lookup"><span data-stu-id="98a86-139">For example, there might be a "dev" environment used to quickly prototype new code.</span></span>
<span data-ttu-id="98a86-140">Kódu z prostředí "dev" přejde do prostředí "test", kde jiní lidé ověřte nové funkce.</span><span class="sxs-lookup"><span data-stu-id="98a86-140">The code from the "dev" environment goes into a "test" environment, where other people verify the new functionality.</span></span>
<span data-ttu-id="98a86-141">Nakonec kód přejde do stavu "produkční" nebo produkčním prostředí živého webu.</span><span class="sxs-lookup"><span data-stu-id="98a86-141">Finally, the code goes into "prod", or the live site production environment.</span></span>

<span data-ttu-id="98a86-142">Konfigurace DSC podle tohoto kanálu dev-test-prod prostřednictvím [konfigurační data](../configurations/configData.md).</span><span class="sxs-lookup"><span data-stu-id="98a86-142">DSC configurations accommodate this dev-test-prod pipeline through the use of [configuration data](../configurations/configData.md).</span></span>
<span data-ttu-id="98a86-143">To dále abstrahuje rozdíl mezi struktura konfiguraci z uzlů, které se spravují.</span><span class="sxs-lookup"><span data-stu-id="98a86-143">This further abstracts the difference between the structure of the configuration from the nodes that are managed.</span></span>
<span data-ttu-id="98a86-144">Můžete například definovat konfiguraci, která vyžaduje SQL server, server služby IIS a server střední vrstvy.</span><span class="sxs-lookup"><span data-stu-id="98a86-144">For example, you can define a configuration that requires a SQL server, an IIS server, and a middle-tier server.</span></span>
<span data-ttu-id="98a86-145">Bez ohledu na to, jaké uzly zobrazí různé části této konfigurace tyto tři prvky bude k dispozici vždy.</span><span class="sxs-lookup"><span data-stu-id="98a86-145">Regardless of what nodes receive the different pieces of this configuration, those three elements will always be present.</span></span>
<span data-ttu-id="98a86-146">Konfigurační data můžete použít tak, aby odkazoval všechny tři prvky na stejném počítači pro vývoj prostředí, samostatné tři prvky do tří různých počítačů pro testovací prostředí a nakonec na všech provozních serverech pro produkční prostředí.</span><span class="sxs-lookup"><span data-stu-id="98a86-146">You can use configuration data to point all three elements towards the same machine for a dev environment, separate out the three elements to three different machines for a test environment, and finally towards all your production servers for the prod environment.</span></span>
<span data-ttu-id="98a86-147">Pokud chcete nasadit do různých prostředí, můžete vyvolat **Start-DscConfiguration** správnou konfiguraci dat pro prostředí, kterou chcete cílit.</span><span class="sxs-lookup"><span data-stu-id="98a86-147">To deploy to the different environments, you can invoke **Start-DscConfiguration** with the correct configuration data for the environment you want to target.</span></span>

## <a name="see-also"></a><span data-ttu-id="98a86-148">Viz také</span><span class="sxs-lookup"><span data-stu-id="98a86-148">See Also</span></span>

[<span data-ttu-id="98a86-149">Konfigurace</span><span class="sxs-lookup"><span data-stu-id="98a86-149">Configurations</span></span>](../configurations/configurations.md)

[<span data-ttu-id="98a86-150">Konfigurační Data</span><span class="sxs-lookup"><span data-stu-id="98a86-150">Configuration Data</span></span>](../configurations/configData.md)

[<span data-ttu-id="98a86-151">Prostředky</span><span class="sxs-lookup"><span data-stu-id="98a86-151">Resources</span></span>](../resources/resources.md)
