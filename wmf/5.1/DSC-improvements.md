---
ms.date: 06/12/2017
author: JKeithB
ms.topic: reference
keywords: wmf,powershell,setup
title: Vylepšení DSC v WMF 5.1
ms.openlocfilehash: 04bf8ed820d24f1062e05d19c8f3b0c041298979
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="improvements-in-desired-state-configuration-dsc-in-wmf-51"></a><span data-ttu-id="d4de5-103">Vylepšení v požadované konfigurace stavu (DSC) v WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="d4de5-103">Improvements in Desired State Configuration (DSC) in WMF 5.1</span></span>

## <a name="dsc-class-resource-improvements"></a><span data-ttu-id="d4de5-104">Vylepšení prostředků DSC – třída</span><span class="sxs-lookup"><span data-stu-id="d4de5-104">DSC class resource improvements</span></span>

<span data-ttu-id="d4de5-105">V WMF 5.1 vyřešili jsme následující známé problémy:</span><span class="sxs-lookup"><span data-stu-id="d4de5-105">In WMF 5.1, we have fixed the following known issues:</span></span>
* <span data-ttu-id="d4de5-106">Get-DscConfiguration může vrátit prázdné hodnoty (null) nebo chyby, pokud typ tabulky komplexní a hodnoty hash je vrácené funkcí Get() DSC prostředku založené na třídě.</span><span class="sxs-lookup"><span data-stu-id="d4de5-106">Get-DscConfiguration may return empty values (null) or errors if a complex/hash table type is returned by Get() function of a class-based DSC resource.</span></span>
* <span data-ttu-id="d4de5-107">Get-DscConfiguration vrátí chybu, pokud se používá přihlašovací údaje RunAs konfigurace DSC.</span><span class="sxs-lookup"><span data-stu-id="d4de5-107">Get-DscConfiguration returns error if RunAs credential is used in DSC configuration.</span></span>
* <span data-ttu-id="d4de5-108">Na základě třídy prostředků nelze použít v konfiguraci složené.</span><span class="sxs-lookup"><span data-stu-id="d4de5-108">Class-based resource cannot be used in a composite configuration.</span></span>
* <span data-ttu-id="d4de5-109">Spuštění DscConfiguration se zasekne, pokud na základě třídy prostředků má vlastnost vlastní typu.</span><span class="sxs-lookup"><span data-stu-id="d4de5-109">Start-DscConfiguration hangs if class-based resource has a property of its own type.</span></span>
* <span data-ttu-id="d4de5-110">Na základě třídy prostředků nelze použít jako výhradní prostředek.</span><span class="sxs-lookup"><span data-stu-id="d4de5-110">Class-based resource cannot be used as an exclusive resource.</span></span>


## <a name="dsc-resource-debugging-improvements"></a><span data-ttu-id="d4de5-111">Vylepšení ladění prostředek DSC</span><span class="sxs-lookup"><span data-stu-id="d4de5-111">DSC resource debugging improvements</span></span>
<span data-ttu-id="d4de5-112">V WMF 5.0 ladicí program prostředí PowerShell se nezastavil v metodě založené na třídě prostředků (Get/Set nebo Test) přímo.</span><span class="sxs-lookup"><span data-stu-id="d4de5-112">In WMF 5.0, the PowerShell debugger did not stop at the class-based resource method (Get/Set/Test) directly.</span></span>
<span data-ttu-id="d4de5-113">Ladicí program se zastaví v WMF 5.1 na metodu na základě třídy prostředků stejným způsobem jako u prostředků založených na MOF metody.</span><span class="sxs-lookup"><span data-stu-id="d4de5-113">In WMF 5.1, the debugger stops at the class-based resource method in the same way as for MOF-based resources methods.</span></span>

## <a name="dsc-pull-client-supports-tls-11-and-tls-12"></a><span data-ttu-id="d4de5-114">DSC vyžádání klient podporuje protokol TLS 1.1 a TLS 1.2</span><span class="sxs-lookup"><span data-stu-id="d4de5-114">DSC pull client supports TLS 1.1 and TLS 1.2</span></span>
<span data-ttu-id="d4de5-115">Dříve klient pro vyžádání obsahu DSC podporována pouze SSL3.0 a TLS1.0 přes připojení prostřednictvím protokolu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d4de5-115">Previously, the DSC pull client only supported SSL3.0 and TLS1.0 over HTTPS connections.</span></span>
<span data-ttu-id="d4de5-116">Při vynucené bezpečnější protokoly, by klient pro vyžádání obsahu přestane fungovat.</span><span class="sxs-lookup"><span data-stu-id="d4de5-116">When forced to use more secure protocols, the pull client would stop functioning.</span></span>
<span data-ttu-id="d4de5-117">V 5.1 WMF klient vyžádání DSC už podporuje protokol SSL 3.0 a přidává podporu pro bezpečnější protokoly TLS 1.1 a TLS 1.2.</span><span class="sxs-lookup"><span data-stu-id="d4de5-117">In WMF 5.1, the DSC pull client no longer supports SSL 3.0 and adds support for the more secure TLS 1.1 and TLS 1.2 protocols.</span></span>

## <a name="improved-pull-server-registration"></a><span data-ttu-id="d4de5-118">Registrace serveru vylepšené vyžádání obsahu</span><span class="sxs-lookup"><span data-stu-id="d4de5-118">Improved pull server registration</span></span> ##

<span data-ttu-id="d4de5-119">V dřívějších verzích WMF souběžných registrace/reporting požadavky na server DSC za při použití databáze ESENT povede k LCM selhání k registraci nebo sestavy.</span><span class="sxs-lookup"><span data-stu-id="d4de5-119">In the earlier versions of WMF, simultaneous registrations/reporting requests to a DSC pull server while using the ESENT database would lead to LCM failing to register and/or report.</span></span>
<span data-ttu-id="d4de5-120">V takových případech protokolů událostí na serveru vyžádané replikace se chyba "Název Instance již používán."</span><span class="sxs-lookup"><span data-stu-id="d4de5-120">In such cases, the event logs on the pull server has the error "Instance Name already in use."</span></span>
<span data-ttu-id="d4de5-121">Důvodem byla nezadají používá pro přístup k databázi ESENT ve scénáři s více procesy.</span><span class="sxs-lookup"><span data-stu-id="d4de5-121">This was due to an incorrect pattern being used to access the ESENT database in a multi-threaded scenario.</span></span>
<span data-ttu-id="d4de5-122">V 5.1 WMF tento problém byl opraven.</span><span class="sxs-lookup"><span data-stu-id="d4de5-122">In WMF 5.1, this issue has been fixed.</span></span>
<span data-ttu-id="d4de5-123">Souběžné registrace nebo generování sestav (zahrnující ESENT databáze), funguje bez potíží WMF 5.1.</span><span class="sxs-lookup"><span data-stu-id="d4de5-123">Concurrent registrations or reporting (involving ESENT database) works fine in WMF 5.1.</span></span>
<span data-ttu-id="d4de5-124">Tento problém se vztahuje pouze na databázi ESENT a doporučení se netýká do databáze OLEDB.</span><span class="sxs-lookup"><span data-stu-id="d4de5-124">This issue is applicable only to the ESENT database and does not apply to the OLEDB database.</span></span>

## <a name="enable-circular-log-on-esent-database-instance"></a><span data-ttu-id="d4de5-125">Povolit cyklického protokolu ESENT instanci databáze</span><span class="sxs-lookup"><span data-stu-id="d4de5-125">Enable Circular log on ESENT database instance</span></span>
<span data-ttu-id="d4de5-126">V eariler verzi DSC PullServer byly soubory protokolů databáze ESENT naplňování místa na disku becouse pullserver, které při vytváření instance databáze bez cyklické protokolování.</span><span class="sxs-lookup"><span data-stu-id="d4de5-126">In eariler version of DSC-PullServer, the ESENT database log files were filling up the disk space of the pullserver becouse the database instance was being created without circular logging.</span></span> <span data-ttu-id="d4de5-127">V této verzi máte možnost řídit chování cyklické protokolování instanci pomocí souboru web.config pullserver.</span><span class="sxs-lookup"><span data-stu-id="d4de5-127">In this release, you have the option to control the circular logging behavior of the instance using the web.config of the pullserver.</span></span> <span data-ttu-id="d4de5-128">Ve výchozím nastavení CircularLogging nastavena na hodnotu TRUE.</span><span class="sxs-lookup"><span data-stu-id="d4de5-128">By default CircularLogging is set to TRUE.</span></span>
```
<appSettings>
    <add key="dbprovider" value="ESENT" />
    <add key="dbconnectionstr" value="C:\Program Files\WindowsPowerShell\DscService\Devices.edb" />
    <add key="CheckpointDepthMaxKB" value="512" />
    <add key="UseCircularESENTLogs" value="TRUE" />
  </appSettings>
```
## <a name="pull-partial-configuration-naming-convention"></a><span data-ttu-id="d4de5-129">Zásady vytváření názvů částečné konfigurace pro vyžádání obsahu</span><span class="sxs-lookup"><span data-stu-id="d4de5-129">Pull partial configuration naming convention</span></span>
<span data-ttu-id="d4de5-130">V předchozí verzi, zásady vytváření názvů pro částečné konfigurace byla, název souboru MOF v služba nebo server vyžádané replikace musí shodovat s názvem částečné konfigurace zadaný v nastavení správce místní konfigurace, která zase musí odpovídat Název konfigurace vložených v souboru MOF.</span><span class="sxs-lookup"><span data-stu-id="d4de5-130">In the previous release, the naming convention for a partial configuration was that the MOF file name in the pull server/service should match the partial configuration name specified in the local configuration manager settings that in turn must match the configuration name embedded in the MOF file.</span></span>

<span data-ttu-id="d4de5-131">Najdete níže snímky:</span><span class="sxs-lookup"><span data-stu-id="d4de5-131">See the snapshots below:</span></span>

<span data-ttu-id="d4de5-132">• Místní konfigurační nastavení, která definuje konfiguraci částečné uzlu je povoleno přijímat.</span><span class="sxs-lookup"><span data-stu-id="d4de5-132">•   Local configuration settings which defines a partial configuration that a node is allowed to receive.</span></span>

![Ukázka metakonfiguraci](../images/MetaConfigPartialOne.png)

<span data-ttu-id="d4de5-134">• Ukázka částečné konfigurace definice</span><span class="sxs-lookup"><span data-stu-id="d4de5-134">•   Sample partial configuration definition</span></span>

```powershell
Configuration PartialOne
{
    Node('localhost')
    {
        File test
        {
            DestinationPath = "$env:TEMP\partialconfigexample.txt"
            Contents = 'Partial Config Example'
        }
    }
}
PartialOne
```

<span data-ttu-id="d4de5-135">• 'ConfigurationName' vložený vygenerovaný soubor MOF.</span><span class="sxs-lookup"><span data-stu-id="d4de5-135">•   'ConfigurationName' embedded in the generated MOF file.</span></span>

![Ukázkový soubor generovaný mof](../images/PartialGeneratedMof.png)

<span data-ttu-id="d4de5-137">• Název souboru v úložišti konfigurace vyžádání obsahu</span><span class="sxs-lookup"><span data-stu-id="d4de5-137">•   FileName in the pull configuration repository</span></span>

![Název souboru v úložišti konfigurace](../images/PartialInConfigRepository.png)

<span data-ttu-id="d4de5-139">Název služby Azure Automation generované soubory MOF jako `<ConfigurationName>.<NodeName>.mof`.</span><span class="sxs-lookup"><span data-stu-id="d4de5-139">Azure Automation service name generated MOF files as `<ConfigurationName>.<NodeName>.mof`.</span></span>
<span data-ttu-id="d4de5-140">Konfigurace níže tak zkompiluje do PartialOne.localhost.mof.</span><span class="sxs-lookup"><span data-stu-id="d4de5-140">So the configuration below compiles to PartialOne.localhost.mof.</span></span>

<span data-ttu-id="d4de5-141">Z tohoto důvodu bylo možné na vyžádání, jednu konfiguraci částečné ze služby Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="d4de5-141">This made it impossible to pull one of your partial configuration from Azure Automation service.</span></span>

```powershell
Configuration PartialOne
{
    Node('localhost')
    {
        File test
        {
            DestinationPath = "$env:TEMP\partialconfigexample.txt"
            Contents = 'Partial Config Example'
        }
    }
}
PartialOne
```

<span data-ttu-id="d4de5-142">V WMF 5.1, může mít jako název částečné konfigurace v rámci serveru nebo služby z vlastního `<ConfigurationName>.<NodeName>.mof`.</span><span class="sxs-lookup"><span data-stu-id="d4de5-142">In WMF 5.1, a partial configuration in the pull server/service can be named as `<ConfigurationName>.<NodeName>.mof`.</span></span>
<span data-ttu-id="d4de5-143">Navíc pokud je počítač se stahování konfigurací jedné z vyžádání služba nebo server pak konfigurační soubor na vyžádání obsahu server konfigurace úložiště může mít libovolný název souboru.</span><span class="sxs-lookup"><span data-stu-id="d4de5-143">Moreover, if a machine is pulling a single configuration from a pull server/service then the configuration file on the pull server configuration repository can have any file name.</span></span>
<span data-ttu-id="d4de5-144">Tato pojmenování flexibilitu vám umožní spravovat uzly částečně službou Azure Automation, kde některé konfigurace pro váš uzel pochází z Azure Automation DSC a částečné konfigurace, které můžete spravovat místně.</span><span class="sxs-lookup"><span data-stu-id="d4de5-144">This naming flexibility allows you to manage your nodes partially by Azure Automation service, where some configuration for your node is coming from Azure Automation DSC and with a partial configuration that you manage locally.</span></span>

<span data-ttu-id="d4de5-145">Metakonfiguraci níže nastaví uzlu jako spravované obě služby místně a také pomocí Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="d4de5-145">The metaconfiguration below sets up a node to be managed both locally as well as by Azure Automation service.</span></span>

```powershell
  [DscLocalConfigurationManager()]
   Configuration RegistrationMetaConfig
   {
        Settings
        {
            RefreshFrequencyMins = 30
            RefreshMode = "PULL"
        }

        ConfigurationRepositoryWeb web
        {
            ServerURL =  $endPoint
            RegistrationKey = $registrationKey
            ConfigurationNames = $configurationName
        }

        # Partial configuration managed by Azure Automation service.
        PartialConfiguration PartialConfigurationManagedByAzureAutomation
        {
            ConfigurationSource = "[ConfigurationRepositoryWeb]Web"
        }

        # This partial configuration is managed locally.
        PartialConfiguration OnPremisesConfig
        {
            RefreshMode = "PUSH"
            ExclusiveResources = @("Script")
        }

   }

   RegistrationMetaConfig
   Set-DscLocalConfigurationManager -Path .\RegistrationMetaConfig -Verbose
 ```

# <a name="using-psdscrunascredential-with-dsc-composite-resources"></a><span data-ttu-id="d4de5-146">Pomocí PsDscRunAsCredential složené prostředky DSC</span><span class="sxs-lookup"><span data-stu-id="d4de5-146">Using PsDscRunAsCredential with DSC composite resources</span></span>

<span data-ttu-id="d4de5-147">Jsme doplnili podporu pro používání [ *PsDscRunAsCredential* ](https://msdn.microsoft.com/cs-cz/powershell/dsc/runasuser) s DSC [složené](https://msdn.microsoft.com/en-us/powershell/dsc/authoringresourcecomposite) prostředky.</span><span class="sxs-lookup"><span data-stu-id="d4de5-147">We have added support for using [*PsDscRunAsCredential*](https://msdn.microsoft.com/cs-cz/powershell/dsc/runasuser) with DSC [Composite](https://msdn.microsoft.com/en-us/powershell/dsc/authoringresourcecomposite) resources.</span></span>

<span data-ttu-id="d4de5-148">Teď můžete zadat hodnotu pro PsDscRunAsCredential při použití složené prostředků v konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="d4de5-148">You can now specify a value for PsDscRunAsCredential when using composite resources inside configurations.</span></span>
<span data-ttu-id="d4de5-149">-Li zadána, všechny prostředky spustit uvnitř složené prostředků jako uživatel RunAs.</span><span class="sxs-lookup"><span data-stu-id="d4de5-149">When specified, all resources run inside a composite resource as a RunAs user.</span></span>
<span data-ttu-id="d4de5-150">Volá-li prostředek složené jiný prostředek složený, všechny její prostředky jsou provést, protože uživatele RunAs.</span><span class="sxs-lookup"><span data-stu-id="d4de5-150">If a composite resource calls another composite resource, all of its resources are also executed as RunAs user.</span></span>
<span data-ttu-id="d4de5-151">Pověření spustit jako rozšířeny všechny úrovně hierarchie složené prostředků.</span><span class="sxs-lookup"><span data-stu-id="d4de5-151">RunAs credentials are propagated to any level of the composite resource hierarchy.</span></span>
<span data-ttu-id="d4de5-152">Pokud žádný prostředek uvnitř složené prostředků určuje vlastní hodnotu pro PsDscRunAsCredential, výsledky sloučení chyby při kompilaci konfigurace.</span><span class="sxs-lookup"><span data-stu-id="d4de5-152">If any resource inside a composite resource specifies its own value for PsDscRunAsCredential, a merge error results during configuration compilation.</span></span>

<span data-ttu-id="d4de5-153">Tento příklad ukazuje použití se [WindowsFeatureSet](https://msdn.microsoft.com/en-us/powershell/wmf/dsc_newresources) složené prostředků, které jsou součástí modulu PSDesiredStateConfiguration.</span><span class="sxs-lookup"><span data-stu-id="d4de5-153">This example shows usage with [WindowsFeatureSet](https://msdn.microsoft.com/en-us/powershell/wmf/dsc_newresources) composite resource included in PSDesiredStateConfiguration module.</span></span>



```powershell

Configuration InstallWindowsFeature
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration

    Node $AllNodes.NodeName
    {
        WindowsFeatureSet features
        {
            Name = @("Telnet-Client","SNMP-Service")
            Ensure = "Present"
            IncludeAllSubFeature = $true
            PsDscRunAsCredential = Get-Credential
        }
    }

}

$configData = @{
    AllNodes = @(
        @{
            NodeName             = 'localhost'
            PSDscAllowDomainUser = $true
            CertificateFile      = 'C:\publicKeys\targetNode.cer'
            Thumbprint           = '7ee7f09d-4be0-41aa-a47f-96b9e3bdec25'
        }
    )
}


InstallWindowsFeature -ConfigurationData $configData

```

##<a name="dsc-module-and-configuration-signing-validations"></a><span data-ttu-id="d4de5-154">Modul DSC a podepisování ověření konfigurace</span><span class="sxs-lookup"><span data-stu-id="d4de5-154">DSC module and configuration signing validations</span></span>
<span data-ttu-id="d4de5-155">V DSC konfigurace a moduly jsou distribuovány do spravovaných počítačů z načítacího serveru.</span><span class="sxs-lookup"><span data-stu-id="d4de5-155">In DSC, configurations and modules are distributed to managed computers from the pull server.</span></span>
<span data-ttu-id="d4de5-156">Pokud ohrožení zabezpečení serveru vyžádané replikace útočník může potenciálně upravit konfigurace a modulů na tomto serveru a jeho distribuován do všech spravovaných uzlech, ohrožení všechny z nich.</span><span class="sxs-lookup"><span data-stu-id="d4de5-156">If the pull server is compromised, an attacker can potentially modify the configurations and modules on the pull server and have it distributed to all managed nodes, compromising all of them.</span></span>

 <span data-ttu-id="d4de5-157">V WMF 5.1, podporuje ověření digitálních podpisů v katalogu a konfigurace DSC (. Soubory MOF).</span><span class="sxs-lookup"><span data-stu-id="d4de5-157">In WMF 5.1, DSC supports validating the digital signatures on catalog and configuration (.MOF) files.</span></span>
<span data-ttu-id="d4de5-158">Tato funkce nebude uzly spuštěn konfigurace nebo modul soubory nejsou podepsány důvěryhodným podepisující osoba nebo které mají bylo manipulováno po byly podepsány důvěryhodným podepisující osoba.</span><span class="sxs-lookup"><span data-stu-id="d4de5-158">This feature prevents nodes from executing configurations or module files which are not signed by a trusted signer or which have been tampered with after they have been signed by trusted signer.</span></span>



###<a name="how-to-sign-configuration-and-module"></a><span data-ttu-id="d4de5-159">Postup konfigurace přihlášení a modulu</span><span class="sxs-lookup"><span data-stu-id="d4de5-159">How to sign configuration and module</span></span>
***
* <span data-ttu-id="d4de5-160">Konfigurační soubory (. Soubory MOF): existující rutiny prostředí PowerShell [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) je rozšířeno pro podporu podepisování souborů MOF.</span><span class="sxs-lookup"><span data-stu-id="d4de5-160">Configuration Files (.MOFs): The existing PowerShell cmdlet [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) is extended to support signing of MOF files.</span></span>
* <span data-ttu-id="d4de5-161">Moduly: Podepisování modulů se provádí podepisování katalogu modul odpovídající pomocí následujících kroků:</span><span class="sxs-lookup"><span data-stu-id="d4de5-161">Modules: Signing of modules is done by signing the corresponding module catalog using the following steps:</span></span>
    1. <span data-ttu-id="d4de5-162">Vytvořte soubor katalogu: soubor katalogu obsahuje kolekci kryptografické hodnoty hash nebo kryptografické otisky.</span><span class="sxs-lookup"><span data-stu-id="d4de5-162">Create a catalog file: A catalog file contains a collection of cryptographic hashes or thumbprints.</span></span>
       <span data-ttu-id="d4de5-163">Každý kryptografický otisk odpovídá souboru, který je součástí modulu.</span><span class="sxs-lookup"><span data-stu-id="d4de5-163">Each thumbprint corresponds to a file that is included in the module.</span></span>
       <span data-ttu-id="d4de5-164">K dispozici novou rutinu [New-FileCatalog](https://technet.microsoft.com/library/cc732148.aspx), byl přidán do povolit uživatelům vytvářet soubor katalogu pro jejich modul.</span><span class="sxs-lookup"><span data-stu-id="d4de5-164">The new cmdlet [New-FileCatalog](https://technet.microsoft.com/library/cc732148.aspx), has been added to enable users to create a catalog file for their module.</span></span>
    2. <span data-ttu-id="d4de5-165">Podepsání souboru katalogu: použití [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) k podepsání souboru katalogu.</span><span class="sxs-lookup"><span data-stu-id="d4de5-165">Sign the catalog file: Use [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) to sign the catalog file.</span></span>
    3. <span data-ttu-id="d4de5-166">Umístěte soubor katalogu naleznete ve složce modulu.</span><span class="sxs-lookup"><span data-stu-id="d4de5-166">Place the catalog file inside the module folder.</span></span>
<span data-ttu-id="d4de5-167">Podle konvence třeba modul katalogu soubor uložit ve složce modulu se stejným názvem jako modul.</span><span class="sxs-lookup"><span data-stu-id="d4de5-167">By convention, module catalog file should be placed under the module folder with the same name as the module.</span></span>

###<a name="localconfigurationmanager-settings-to-enable-signing-validations"></a><span data-ttu-id="d4de5-168">LocalConfigurationManager nastavení pro povolení podpisový ověření</span><span class="sxs-lookup"><span data-stu-id="d4de5-168">LocalConfigurationManager settings to enable signing validations</span></span>

####<a name="pull"></a><span data-ttu-id="d4de5-169">Pro vyžádání obsahu</span><span class="sxs-lookup"><span data-stu-id="d4de5-169">Pull</span></span>
<span data-ttu-id="d4de5-170">LocalConfigurationManager uzlu provede podpisový ověření modulů a na základě aktuální nastavení konfigurace.</span><span class="sxs-lookup"><span data-stu-id="d4de5-170">The LocalConfigurationManager of a node performs signing validation of modules and configurations based on its current settings.</span></span>
<span data-ttu-id="d4de5-171">Ověření podpisu je ve výchozím nastavení zakázané.</span><span class="sxs-lookup"><span data-stu-id="d4de5-171">By default, signature validation is disabled.</span></span>
<span data-ttu-id="d4de5-172">Ověření podpisu můžete povolit přidáním 'SignatureValidation' blok k definici meta konfigurace uzlu jako uvedené níže:</span><span class="sxs-lookup"><span data-stu-id="d4de5-172">Signature validation can enabled by adding the ‘SignatureValidation’ block to the meta-configuration definition of the node as shown below:</span></span>

```powershell
[DSCLocalConfigurationManager()]
Configuration EnableSignatureValidation
{
    Settings
    {
        RefreshMode = 'PULL'
    }

    ConfigurationRepositoryWeb pullserver{
      ConfigurationNames = 'sql'
      ServerURL = 'http://localhost:8080/PSDSCPullServer/PSDSCPullServer.svc'
      AllowUnsecureConnection = $true
      RegistrationKey = 'd6750ff1-d8dd-49f7-8caf-7471ea9793fc' # Replace this with correct registration key.
    }
    SignatureValidation validations{
        # By default, LCM uses the default Windows trusted publisher store to validate the certificate chain. If TrustedStorePath property is specified, LCM uses this custom store for retrieving the trusted publishers to validate the content.
        TrustedStorePath = 'Cert:\LocalMachine\DSCStore'
        SignedItemType = 'Configuration','Module'         # This is a list of DSC artifacts, for which LCM need to verify their digital signature before executing them on the node.
    }

}
EnableSignatureValidation
Set-DscLocalConfigurationManager -Path .\EnableSignatureValidation -Verbose
 ```

<span data-ttu-id="d4de5-173">Nastavení výše metakonfiguraci na uzlu umožňuje ověření podpisu stažené konfigurace a moduly.</span><span class="sxs-lookup"><span data-stu-id="d4de5-173">Setting the above metaconfiguration on a node enables signature validation on downloaded configurations and modules.</span></span>
<span data-ttu-id="d4de5-174">Správce místní konfigurace provede následující kroky k ověření digitálních podpisů.</span><span class="sxs-lookup"><span data-stu-id="d4de5-174">The Local Configuration Manager performs the following steps to verify the digital signatures.</span></span>

1. <span data-ttu-id="d4de5-175">Ověření podpisu na konfigurační soubor (. MOF) je platná.</span><span class="sxs-lookup"><span data-stu-id="d4de5-175">Verify the signature on a configuration file (.MOF) is valid.</span></span>
   <span data-ttu-id="d4de5-176">Používá rutinu prostředí PowerShell [Get-AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx), což je rozšířená v 5.1 pro podporu ověřování podpisu MOF.</span><span class="sxs-lookup"><span data-stu-id="d4de5-176">It uses the PowerShell cmdlet [Get-AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx), which is extended in 5.1 to support MOF signature validation.</span></span>
2. <span data-ttu-id="d4de5-177">Ověřte, že certifikační autority, která oprávnění podepisující je důvěryhodný.</span><span class="sxs-lookup"><span data-stu-id="d4de5-177">Verify the certificate authority that authorized the signer is trusted.</span></span>
3. <span data-ttu-id="d4de5-178">Stáhněte si modul nebo prostředků závislosti konfigurace do dočasného umístění.</span><span class="sxs-lookup"><span data-stu-id="d4de5-178">Download module/resource dependencies of the configuration to a temp location.</span></span>
4. <span data-ttu-id="d4de5-179">Ověření podpisu katalogu zahrnuty do vnitřní modul.</span><span class="sxs-lookup"><span data-stu-id="d4de5-179">Verify the signature of the catalog included inside the module.</span></span>
    * <span data-ttu-id="d4de5-180">Najít `<moduleName>.cat` souboru a ověřte jeho podpis pomocí rutiny [Get-AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx).</span><span class="sxs-lookup"><span data-stu-id="d4de5-180">Find a `<moduleName>.cat` file and verify its signature using the cmdlet  [Get-AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx).</span></span>
    * <span data-ttu-id="d4de5-181">Ověřte, že certifikační autorita, která ověření podpisu je důvěryhodný.</span><span class="sxs-lookup"><span data-stu-id="d4de5-181">Verify the certification authority that authenticated the signer is trusted.</span></span>
    * <span data-ttu-id="d4de5-182">Ověřte obsah moduly nikdo neoprávněně pomocí nové rutiny [Test FileCatalog](https://technet.microsoft.com/library/cc732148.aspx).</span><span class="sxs-lookup"><span data-stu-id="d4de5-182">Verify the content of the modules has not been tampered using the new cmdlet [Test-FileCatalog](https://technet.microsoft.com/library/cc732148.aspx).</span></span>
5. <span data-ttu-id="d4de5-183">Instalace modulu pro $env: ProgramFiles\WindowsPowerShell\Modules\\</span><span class="sxs-lookup"><span data-stu-id="d4de5-183">Install-Module to $env:ProgramFiles\WindowsPowerShell\Modules\\</span></span>
6. <span data-ttu-id="d4de5-184">Konfigurace procesů</span><span class="sxs-lookup"><span data-stu-id="d4de5-184">Process configuration</span></span>

> <span data-ttu-id="d4de5-185">Poznámka: Ověřování podpisu v modulu katalogu a konfigurace se provádí pouze při použití konfigurace systému poprvé, nebo pokud je modul stáhli a nainstalovali.</span><span class="sxs-lookup"><span data-stu-id="d4de5-185">Note: Signature validation on module-catalog and configuration is only performed when the configuration is applied to the system for the first time or when the module is downloaded and installed.</span></span>
<span data-ttu-id="d4de5-186">Spustí konzistence neověřují podpis Current.mof nebo jeho závislé součásti modulu.</span><span class="sxs-lookup"><span data-stu-id="d4de5-186">Consistency runs do not validate the signature of Current.mof or its module dependencies.</span></span>
<span data-ttu-id="d4de5-187">Pokud ověření došlo k chybě v jakékoli fázi, například pokud konfigurace načtený z je vyžádání obsahu server bez znaménka, pak ukončí zpracování konfigurace s následující chybou a jsou odstraněny všechny dočasné soubory.</span><span class="sxs-lookup"><span data-stu-id="d4de5-187">If verification has failed at any stage, for instance, if the configuration pulled from the pull server is unsigned, then processing of the configuration terminates with the error shown below and all temporary files are deleted.</span></span>

![Ukázková konfigurace výstupní chyby](../images/PullUnsignedConfigFail.png)

<span data-ttu-id="d4de5-189">Podobně stahování modulu, jehož katalogu není podepsané má za následek následující chybě:</span><span class="sxs-lookup"><span data-stu-id="d4de5-189">Similarly, pulling a module whose catalog is not signed results in the following error:</span></span>

![Ukázka modul výstupní chyby](../images/PullUnisgnedCatalog.png)

####<a name="push"></a><span data-ttu-id="d4de5-191">Push</span><span class="sxs-lookup"><span data-stu-id="d4de5-191">Push</span></span>
<span data-ttu-id="d4de5-192">Konfigurace doručit pomocí nabízené instalace může být úmyslně poškozena úrovni jeho zdroje před jeho doručit do uzlu.</span><span class="sxs-lookup"><span data-stu-id="d4de5-192">A configuration delivered by using push might be tampered with at its source before it delivered to the node.</span></span>
<span data-ttu-id="d4de5-193">Správce místní konfigurace se provádí podobným způsobem ověření podpisu pro stisknutí nebo publikované konfigurace.</span><span class="sxs-lookup"><span data-stu-id="d4de5-193">The Local Configuration Manager performs similar signature validation steps for pushed or published configuration(s).</span></span>
<span data-ttu-id="d4de5-194">Níže je kompletní příklad, jak ověřit podpis nabízená instalace.</span><span class="sxs-lookup"><span data-stu-id="d4de5-194">Below is a complete example of signature validation for push.</span></span>

* <span data-ttu-id="d4de5-195">Povolte ověřování podpisu na uzlu.</span><span class="sxs-lookup"><span data-stu-id="d4de5-195">Enable signature validation on the node.</span></span>

```powershell
[DSCLocalConfigurationManager()]
Configuration EnableSignatureValidation
{
    Settings
    {
        RefreshMode = 'PUSH'
    }
    SignatureValidation validations{
        TrustedStorePath = 'Cert:\LocalMachine\DSCStore'
        SignedItemType =  'Configuration','Module'
    }

}
EnableSignatureValidation
Set-DscLocalConfigurationManager -Path .\EnableSignatureValidation -Verbose
```
* <span data-ttu-id="d4de5-196">Vytvořte vzorový konfigurační soubor.</span><span class="sxs-lookup"><span data-stu-id="d4de5-196">Create a sample configuration file.</span></span>

```powershell
# Sample configuration
Configuration Test
{

    File foo
    {
        DestinationPath =  "$env:TEMP\signingTest.txt"
        Contents = "ABC"
    }
}
Test
```

* <span data-ttu-id="d4de5-197">Zkuste, když zavedete nepodepsané konfiguračního souboru uzlu.</span><span class="sxs-lookup"><span data-stu-id="d4de5-197">Try pushing the unsigned configuration file in to the node.</span></span>

```powershell
Start-DscConfiguration -Path .\Test -Wait -Verbose -Force
```
![ErrorUnsignedMofPushed](../images/PushUnsignedMof.png)

* <span data-ttu-id="d4de5-199">Zaregistrujte konfiguračního souboru pomocí certifikátu pro podepisování kódu.</span><span class="sxs-lookup"><span data-stu-id="d4de5-199">Sign the configuration file using code-signing certificate.</span></span>

![SignMofFile](../images/SignMofFile.png)

* <span data-ttu-id="d4de5-201">Zkuste vkládání podepsaného souboru MOF.</span><span class="sxs-lookup"><span data-stu-id="d4de5-201">Try pushing the signed MOF file.</span></span>

![SignMofFile](../images/PushSignedMof.png)