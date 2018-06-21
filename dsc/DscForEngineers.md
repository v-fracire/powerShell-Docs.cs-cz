---
ms.date: 10/13/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Přehled platformy Desired State Configuration pro techniky
ms.openlocfilehash: 30ce8bbb8bd3ea69dbf8ca509ecf523eb8fd915f
ms.sourcegitcommit: bad40d59598ae5597051fa381986316a2d9bf6c8
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/20/2018
ms.locfileid: "36271071"
---
# <a name="desired-state-configuration-overview-for-engineers"></a><span data-ttu-id="3f4b3-103">Přehled platformy Desired State Configuration pro techniky</span><span class="sxs-lookup"><span data-stu-id="3f4b3-103">Desired State Configuration Overview for Engineers</span></span>

<span data-ttu-id="3f4b3-104">Tento dokument je určený pro vývojáře a operace týmy pochopit výhody z prostředí PowerShell požadovaného stavu konfigurace (DSC).</span><span class="sxs-lookup"><span data-stu-id="3f4b3-104">This document is intended for developer and operations teams to understand the benefits of PowerShell Desired State Configuration (DSC).</span></span>
<span data-ttu-id="3f4b3-105">Pro vyšší úroveň zobrazení hodnoty DSC poskytuje, najdete v tématu [potřeby přehled stavu konfigurace pro rozhodují](decisionMaker.md)</span><span class="sxs-lookup"><span data-stu-id="3f4b3-105">For a higher level view of the value DSC provides, please see [Desired State Configuration Overview for Decision Makers](decisionMaker.md)</span></span>

## <a name="benefits-of-desired-state-configuration"></a><span data-ttu-id="3f4b3-106">Výhody Desired State Configuration</span><span class="sxs-lookup"><span data-stu-id="3f4b3-106">Benefits of Desired State Configuration</span></span>

<span data-ttu-id="3f4b3-107">DSC existuje:</span><span class="sxs-lookup"><span data-stu-id="3f4b3-107">DSC exists to:</span></span>

- <span data-ttu-id="3f4b3-108">Snížení složitosti skriptování v systému Windows</span><span class="sxs-lookup"><span data-stu-id="3f4b3-108">Decrease the complexity of scripting in Windows</span></span>
- <span data-ttu-id="3f4b3-109">Zvýšení rychlosti iterace</span><span class="sxs-lookup"><span data-stu-id="3f4b3-109">Increase the speed of iteration</span></span>

<span data-ttu-id="3f4b3-110">Koncept "průběžné nasazování" se stává stále důležitější.</span><span class="sxs-lookup"><span data-stu-id="3f4b3-110">The concept of "continuous deployment" is becoming more important.</span></span>
<span data-ttu-id="3f4b3-111">Průběžné nasazování znamená schopnost nasadit často, potenciálně mnohokrát za den.</span><span class="sxs-lookup"><span data-stu-id="3f4b3-111">Continuous deployment means the ability to deploy frequently, potentially many times per day.</span></span>
<span data-ttu-id="3f4b3-112">Účelem tato nasazení není něco opravit, ale něco publikovaly rychle získat.</span><span class="sxs-lookup"><span data-stu-id="3f4b3-112">The purpose of these deployments are not to fix something but to get something published quickly.</span></span>
<span data-ttu-id="3f4b3-113">Získáním nové funkce prostřednictvím vývoj do operace pro bezproblémové a spolehlivě jako možné snížit čas na hodnotu nové obchodní logiky.</span><span class="sxs-lookup"><span data-stu-id="3f4b3-113">By getting new features through development into operation as smoothly and reliably as possible, you reduce time-to-value of new business logic.</span></span>

<span data-ttu-id="3f4b3-114">Přesuňte směrem cloud computing znamená nasazení řešení, které využívá model "deklarativní" šablony, kde je deklarován jako text prostředí end stavu a je publikována ve službě modul nasazení.</span><span class="sxs-lookup"><span data-stu-id="3f4b3-114">The move towards cloud computing implies a deployment solution that utilizes a "declarative" template model, where an end state environment is declared as text and published to a deployment engine.</span></span>
<span data-ttu-id="3f4b3-115">Tento postup nasazení umožňuje rychlé změnu ve velkém měřítku, s odolnost proti selhání riziko, protože kdykoli nasazení lze konzistentně opakovat zaručit stavu pro koncové.</span><span class="sxs-lookup"><span data-stu-id="3f4b3-115">This deployment technique allows for rapid change, at scale, with resilience against threat of failure because at any time the deployment can be consistently repeated to guarantee an end state.</span></span>
<span data-ttu-id="3f4b3-116">Vytvoření nástrojů a služeb, které podporují tento styl operací prostřednictvím automatizace je odpovědí na tyto změny.</span><span class="sxs-lookup"><span data-stu-id="3f4b3-116">The creation of tools and services that support this style of operations through automation is a response to these changes.</span></span>

<span data-ttu-id="3f4b3-117">DSC je platforma, která poskytuje deklarativní a idempotent (repeatable) nasazení, konfiguraci a shoda.</span><span class="sxs-lookup"><span data-stu-id="3f4b3-117">DSC is a platform that provides declarative and idempotent (repeatable) deployment, configuration and conformance.</span></span>
<span data-ttu-id="3f4b3-118">Platforma DSC umožňuje ujistěte, že součástí vašeho datového centra mají správnou konfiguraci, která zabraňuje chyby a brání selhání nákladná nasazení.</span><span class="sxs-lookup"><span data-stu-id="3f4b3-118">The DSC platform enables you to ensure that the components of your data center have the correct configuration, which avoids errors and prevents costly deployment failures.</span></span>
<span data-ttu-id="3f4b3-119">DSC podle konfigurace DSC považuje jako součást kódu aplikace, umožňuje průběžné nasazování.</span><span class="sxs-lookup"><span data-stu-id="3f4b3-119">By treating DSC configurations as part of application code, DSC enables continuous deployment.</span></span>
<span data-ttu-id="3f4b3-120">Konfigurace DSC je třeba aktualizovat v rámci aplikace, zajistíte, že znalosti potřebné k nasazení aplikace je vždy aktuální a připravené k použití.</span><span class="sxs-lookup"><span data-stu-id="3f4b3-120">The DSC configuration should be updated as a part of the application, ensuring that the knowledge needed to deploy the application is always up-to-date and ready to be used.</span></span>

## <a name="i-have-powershell-why-do-i-need-desired-state-configuration"></a><span data-ttu-id="3f4b3-121">"Mám prostředí PowerShell, proč je důležité konfigurace požadovaného stavu?"</span><span class="sxs-lookup"><span data-stu-id="3f4b3-121">"I have PowerShell, why do I need Desired State Configuration?"</span></span>

<span data-ttu-id="3f4b3-122">Záměr samostatné konfigurace DSC, nebo "co chcete udělat", provedení, nebo "jak chcete provést."</span><span class="sxs-lookup"><span data-stu-id="3f4b3-122">DSC configurations separate intent, or "what I want to do", from execution, or "how I want to do it."</span></span>
<span data-ttu-id="3f4b3-123">To znamená, že logiku spouštění je obsažena v prostředky.</span><span class="sxs-lookup"><span data-stu-id="3f4b3-123">This means the logic of execution is contained within the resources.</span></span>
<span data-ttu-id="3f4b3-124">Uživatelé nemusí vědět, jak implementovat nebo nasazení funkce, pokud prostředek DSC této funkce je k dispozici.</span><span class="sxs-lookup"><span data-stu-id="3f4b3-124">Users do not have to know how to implement or deploy a feature when a DSC resource for that feature is available.</span></span>
<span data-ttu-id="3f4b3-125">To umožňuje uživatelům zaměřit se na strukturu jejich nasazení.</span><span class="sxs-lookup"><span data-stu-id="3f4b3-125">This allows the user to focus on the structure of their deployment.</span></span>

<span data-ttu-id="3f4b3-126">Jako příklad skriptů prostředí PowerShell by měl vypadat takto:</span><span class="sxs-lookup"><span data-stu-id="3f4b3-126">As an example, PowerShell scripts should look like this:</span></span>
```powershell
# Create a share in Windows Server 8
New-SmbShare -Name MyShare -Path C:\Demo\Temp -FullAccess Alice -ReadAccess Bob
```
<span data-ttu-id="3f4b3-127">Tento skript je jednoduché, srozumitelné a přehledné.</span><span class="sxs-lookup"><span data-stu-id="3f4b3-127">This script is simple, comprehensible, and straightforward.</span></span>
<span data-ttu-id="3f4b3-128">Ale pokud se pokusíte vložení skriptu do produkčního prostředí, budete spouštět do několika problémy.</span><span class="sxs-lookup"><span data-stu-id="3f4b3-128">However, if you try putting that script into production, you will run into several issues.</span></span>
<span data-ttu-id="3f4b3-129">Co se stane, když, skript je spuštěn v řádku dvakrát?</span><span class="sxs-lookup"><span data-stu-id="3f4b3-129">What happens if that script is run twice in a row?</span></span>
<span data-ttu-id="3f4b3-130">Co se stane, když Bob dříve mají plný přístup ke sdílené složce?</span><span class="sxs-lookup"><span data-stu-id="3f4b3-130">What happens if Bob previously had Full Access to the share?</span></span>

<span data-ttu-id="3f4b3-131">Pro kompenzaci tyto problémy, bude vypadat blíže něco podobného jako "Skutečná" verze skriptu:</span><span class="sxs-lookup"><span data-stu-id="3f4b3-131">To compensate for these issues, a "real" version of the script will look closer to something like:</span></span>
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

<span data-ttu-id="3f4b3-132">Tento skript je složitější s dostatkem logiku a zpracování chyb.</span><span class="sxs-lookup"><span data-stu-id="3f4b3-132">This script is more complex, with plenty of logic and error handling.</span></span>
<span data-ttu-id="3f4b3-133">Skript je složitější, protože se už oznamující, co chcete done, ale *jak to udělat*.</span><span class="sxs-lookup"><span data-stu-id="3f4b3-133">The script is more complex because you are no longer stating what you want done, but *how to do it*.</span></span>

<span data-ttu-id="3f4b3-134">DSC umožňuje určit, co chcete done a logiku je abstrahované rychle.</span><span class="sxs-lookup"><span data-stu-id="3f4b3-134">DSC allows you to say what you want done, and the underlying logic is abstracted away.</span></span>

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

<span data-ttu-id="3f4b3-135">Tento skript je řádně formátovaný a přehledné ke čtení.</span><span class="sxs-lookup"><span data-stu-id="3f4b3-135">This script is cleanly formatted and straightforward to read.</span></span>
<span data-ttu-id="3f4b3-136">Se stále nachází na logické cesty a zpracování chyb [prostředků](resources.md) implementace, ale neviditelné autorovi skriptu.</span><span class="sxs-lookup"><span data-stu-id="3f4b3-136">The logic paths and error handling are still present in the [resource](resources.md) implementation, but invisible to the script author.</span></span>

## <a name="separating-environment-from-structure"></a><span data-ttu-id="3f4b3-137">Oddělení prostředí z struktura</span><span class="sxs-lookup"><span data-stu-id="3f4b3-137">Separating Environment from Structure</span></span>

<span data-ttu-id="3f4b3-138">Běžné vzoru v DevOps je mít několik prostředí pro nasazení.</span><span class="sxs-lookup"><span data-stu-id="3f4b3-138">A common pattern in DevOps is to have multiple environments for deployment.</span></span>
<span data-ttu-id="3f4b3-139">Například může být prostředí "dev" umožňuje rychle prototypu nový kód.</span><span class="sxs-lookup"><span data-stu-id="3f4b3-139">For example, there might be a "dev" environment used to quickly prototype new code.</span></span>
<span data-ttu-id="3f4b3-140">Kód z prostředí "dev" přejde do prostředí s "test", které jiní lidé ověřte nové funkce.</span><span class="sxs-lookup"><span data-stu-id="3f4b3-140">The code from the "dev" environment goes into a "test" environment, where other people verify the new functionality.</span></span>
<span data-ttu-id="3f4b3-141">Nakonec kód přejde do stavu "produkčního" nebo živý web produkčního prostředí.</span><span class="sxs-lookup"><span data-stu-id="3f4b3-141">Finally, the code goes into "prod", or the live site production environment.</span></span>

<span data-ttu-id="3f4b3-142">Konfigurace DSC zohlednit tento kanál dev-test produkčnímu prostřednictvím [konfigurační data](configData.md).</span><span class="sxs-lookup"><span data-stu-id="3f4b3-142">DSC configurations accommodate this dev-test-prod pipeline through the use of [configuration data](configData.md).</span></span>
<span data-ttu-id="3f4b3-143">Tato další abstrahuje rozdíl mezi strukturu konfigurace z uzlů, které jsou spravovány.</span><span class="sxs-lookup"><span data-stu-id="3f4b3-143">This further abstracts the difference between the structure of the configuration from the nodes that are managed.</span></span>
<span data-ttu-id="3f4b3-144">Můžete například definovat konfigurace, která vyžaduje SQL server, server se službou IIS a server střední vrstvy.</span><span class="sxs-lookup"><span data-stu-id="3f4b3-144">For example, you can define a configuration that requires a SQL server, an IIS server, and a middle-tier server.</span></span>
<span data-ttu-id="3f4b3-145">Bez ohledu na to, jaké uzly zobrazí různé části této konfigurace bude mít tyto tři prvky vždy existuje.</span><span class="sxs-lookup"><span data-stu-id="3f4b3-145">Regardless of what nodes receive the different pieces of this configuration, those three elements will always be present.</span></span>
<span data-ttu-id="3f4b3-146">Konfigurační data můžete použít tak, aby odkazoval na stejném počítači pro vývoj prostředí, samostatné tři prvky do tří různých počítačů pro testovací prostředí, všechny tři prvky a v neposlední řadě směrem všech provozních serverů pro produkčnímu prostředí.</span><span class="sxs-lookup"><span data-stu-id="3f4b3-146">You can use configuration data to point all three elements towards the same machine for a dev environment, separate out the three elements to three different machines for a test environment, and finally towards all your production servers for the prod environment.</span></span>
<span data-ttu-id="3f4b3-147">Nasadit do různých prostředích, můžete vyvolat **Start-DscConfiguration** s daty správnou konfiguraci pro prostředí, který chcete cílit.</span><span class="sxs-lookup"><span data-stu-id="3f4b3-147">To deploy to the different environments, you can invoke **Start-DscConfiguration** with the correct configuration data for the environment you want to target.</span></span>

## <a name="see-also"></a><span data-ttu-id="3f4b3-148">Viz také</span><span class="sxs-lookup"><span data-stu-id="3f4b3-148">See Also</span></span>

[<span data-ttu-id="3f4b3-149">Konfigurace</span><span class="sxs-lookup"><span data-stu-id="3f4b3-149">Configurations</span></span>](configurations.md)

[<span data-ttu-id="3f4b3-150">Konfigurační Data</span><span class="sxs-lookup"><span data-stu-id="3f4b3-150">Configuration Data</span></span>](configData.md)

[<span data-ttu-id="3f4b3-151">Prostředky</span><span class="sxs-lookup"><span data-stu-id="3f4b3-151">Resources</span></span>](resources.md)
