---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: wmf,powershell,setup
title: Vylepšení DSC ve WMF 5.1
ms.openlocfilehash: 92f82d62550e105a187fd7c0c58b49367c646a7e
ms.sourcegitcommit: e46b868f56f359909ff7c8230b1d1770935cce0e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/13/2018
ms.locfileid: "45523018"
---
# <a name="improvements-in-desired-state-configuration-dsc-in-wmf-51"></a><span data-ttu-id="2c2fe-103">Vylepšení Desired State Configuration (DSC) ve WMF 5.1</span><span class="sxs-lookup"><span data-stu-id="2c2fe-103">Improvements in Desired State Configuration (DSC) in WMF 5.1</span></span>

## <a name="dsc-class-resource-improvements"></a><span data-ttu-id="2c2fe-104">Vylepšení prostředků třídy DSC</span><span class="sxs-lookup"><span data-stu-id="2c2fe-104">DSC class resource improvements</span></span>

<span data-ttu-id="2c2fe-105">Ve WMF 5.1 jsme vyřešili následující známé problémy:</span><span class="sxs-lookup"><span data-stu-id="2c2fe-105">In WMF 5.1, we have fixed the following known issues:</span></span>

- <span data-ttu-id="2c2fe-106">Get-DscConfiguration může vrátit prázdné hodnoty (null) nebo chyby, pokud je typ tabulky komplexní a hodnoty hash vrácená funkcí Get() prostředku DSC založené na třídě.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-106">Get-DscConfiguration may return empty values (null) or errors if a complex/hash table type is returned by Get() function of a class-based DSC resource.</span></span>
- <span data-ttu-id="2c2fe-107">Get-DscConfiguration vrátí chybu, pokud se přihlašovací údaje Spustit jako se používá v konfiguraci DSC.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-107">Get-DscConfiguration returns error if RunAs credential is used in DSC configuration.</span></span>
- <span data-ttu-id="2c2fe-108">Založené na třídě prostředků nelze použít v složené konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-108">Class-based resource cannot be used in a composite configuration.</span></span>
- <span data-ttu-id="2c2fe-109">Start-DscConfiguration přestane reagovat, pokud má vlastnost vlastní typ založené na třídě prostředků.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-109">Start-DscConfiguration hangs if class-based resource has a property of its own type.</span></span>
- <span data-ttu-id="2c2fe-110">Založené na třídě prostředků nelze použít jako výhradní prostředků.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-110">Class-based resource cannot be used as an exclusive resource.</span></span>

## <a name="dsc-resource-debugging-improvements"></a><span data-ttu-id="2c2fe-111">Vylepšení ladění prostředků DSC</span><span class="sxs-lookup"><span data-stu-id="2c2fe-111">DSC resource debugging improvements</span></span>

<span data-ttu-id="2c2fe-112">Ve WMF 5.0 ladicí program Powershellu se nezastavil u metody založené na třídě prostředků (Get/Set/Test) přímo.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-112">In WMF 5.0, the PowerShell debugger did not stop at the class-based resource method (Get/Set/Test) directly.</span></span>
<span data-ttu-id="2c2fe-113">Ladicí program se zastaví ve WMF 5.1 u metody založené na třídě prostředků stejným způsobem jako u metody založené na souboru MOF prostředky.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-113">In WMF 5.1, the debugger stops at the class-based resource method in the same way as for MOF-based resources methods.</span></span>

## <a name="dsc-pull-client-supports-tls-11-and-tls-12"></a><span data-ttu-id="2c2fe-114">DSC o přijetí změn klient podporuje protokol TLS 1.1 a TLS 1.2</span><span class="sxs-lookup"><span data-stu-id="2c2fe-114">DSC pull client supports TLS 1.1 and TLS 1.2</span></span>

<span data-ttu-id="2c2fe-115">Dříve DSC načítacího klienta podporuje jenom SSL3.0 a protokol TLS 1.0 prostřednictvím připojení prostřednictvím protokolu HTTPS.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-115">Previously, the DSC pull client only supported SSL3.0 and TLS1.0 over HTTPS connections.</span></span>
<span data-ttu-id="2c2fe-116">Při vynucené bezpečnější protokoly by načítacího klienta přestane fungovat.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-116">When forced to use more secure protocols, the pull client would stop functioning.</span></span>
<span data-ttu-id="2c2fe-117">Ve WMF 5.1 DSC načítacího klienta už podporuje protokol SSL 3.0 a přidává podporu pro bezpečnější protokoly TLS 1.1 a TLS 1.2.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-117">In WMF 5.1, the DSC pull client no longer supports SSL 3.0 and adds support for the more secure TLS 1.1 and TLS 1.2 protocols.</span></span>

## <a name="improved-pull-server-registration"></a><span data-ttu-id="2c2fe-118">Registrace serveru Vylepšený o přijetí změn</span><span class="sxs-lookup"><span data-stu-id="2c2fe-118">Improved pull server registration</span></span>

<span data-ttu-id="2c2fe-119">V dřívějších verzích WMF souběžných registrací/reporting požadavků na serveru vyžádané replikace DSC při používání databáze ESENT povede k LCM selhání registrace a/nebo sestavy.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-119">In the earlier versions of WMF, simultaneous registrations/reporting requests to a DSC pull server while using the ESENT database would lead to LCM failing to register and/or report.</span></span>
<span data-ttu-id="2c2fe-120">V takovém případě protokolů událostí na serveru vyžádané replikace obsahuje chybu "Název Instance již používán."</span><span class="sxs-lookup"><span data-stu-id="2c2fe-120">In such cases, the event logs on the pull server has the error "Instance Name already in use."</span></span>
<span data-ttu-id="2c2fe-121">Důvodem byla nesprávné způsob, jak získat přístup k databázi ESENT ve scénáři s více procesy.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-121">This was due to an incorrect pattern being used to access the ESENT database in a multi-threaded scenario.</span></span>
<span data-ttu-id="2c2fe-122">Ve WMF 5.1 Tento problém vyřešen.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-122">In WMF 5.1, this issue has been fixed.</span></span>
<span data-ttu-id="2c2fe-123">Souběžných registrací nebo vytváření sestav (zahrnující ESENT databáze) funguje bez problémů ve WMF 5.1.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-123">Concurrent registrations or reporting (involving ESENT database) works fine in WMF 5.1.</span></span>
<span data-ttu-id="2c2fe-124">Tento problém se vztahuje pouze na databázi ESENT a se nedá použít u databáze OLEDB.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-124">This issue is applicable only to the ESENT database and does not apply to the OLEDB database.</span></span>

## <a name="enable-circular-log-on-esent-database-instance"></a><span data-ttu-id="2c2fe-125">Povolit cyklického protokolu v instanci databáze ESENT</span><span class="sxs-lookup"><span data-stu-id="2c2fe-125">Enable Circular log on ESENT database instance</span></span>

<span data-ttu-id="2c2fe-126">Ve verzi eariler DSC PullServer byly soubory protokolů databáze ESENT zaplnění místa na disku becouse pullserver, které při vytváření instance databáze bez cyklické protokolování.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-126">In eariler version of DSC-PullServer, the ESENT database log files were filling up the disk space of the pullserver becouse the database instance was being created without circular logging.</span></span> <span data-ttu-id="2c2fe-127">V této verzi máte možnost řídit chování instance pomocí souboru web.config pullserver cyklické protokolování.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-127">In this release, you have the option to control the circular logging behavior of the instance using the web.config of the pullserver.</span></span> <span data-ttu-id="2c2fe-128">Ve výchozím nastavení je CircularLogging nastavena na hodnotu TRUE.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-128">By default CircularLogging is set to TRUE.</span></span>

```
<appSettings>
    <add key="dbprovider" value="ESENT" />
    <add key="dbconnectionstr" value="C:\Program Files\WindowsPowerShell\DscService\Devices.edb" />
    <add key="CheckpointDepthMaxKB" value="512" />
    <add key="UseCircularESENTLogs" value="TRUE" />
  </appSettings>
```

## <a name="pull-partial-configuration-naming-convention"></a><span data-ttu-id="2c2fe-129">O přijetí změn zásady vytváření názvů částečné konfigurace</span><span class="sxs-lookup"><span data-stu-id="2c2fe-129">Pull partial configuration naming convention</span></span>

<span data-ttu-id="2c2fe-130">V předchozí verzi zásady vytváření názvů pro částečné konfigurace bylo, že název souboru MOF v serveru nebo služby o přijetí změn by měl odpovídat názvu konfigurace částečné zadaný v nastavení místního configuration manager, které pak musí odpovídat Název konfigurace vložený do souboru MOF.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-130">In the previous release, the naming convention for a partial configuration was that the MOF file name in the pull server/service should match the partial configuration name specified in the local configuration manager settings that in turn must match the configuration name embedded in the MOF file.</span></span>

<span data-ttu-id="2c2fe-131">Zobrazit snímky níže:</span><span class="sxs-lookup"><span data-stu-id="2c2fe-131">See the snapshots below:</span></span>

- <span data-ttu-id="2c2fe-132">Místní konfigurační nastavení, která definuje částečné konfigurace, který uzel může přijímat.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-132">Local configuration settings which defines a partial configuration that a node is allowed to receive.</span></span>

![Ukázka metaconfiguration](../images/MetaConfigPartialOne.png)

- <span data-ttu-id="2c2fe-134">Ukázková definice částečné konfigurace</span><span class="sxs-lookup"><span data-stu-id="2c2fe-134">Sample partial configuration definition</span></span>

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

- <span data-ttu-id="2c2fe-135">"ConfigurationName" vložen do generovaného souboru MOF.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-135">'ConfigurationName' embedded in the generated MOF file.</span></span>

![Ukázkový soubor generovaný soubor mof](../images/PartialGeneratedMof.png)

- <span data-ttu-id="2c2fe-137">Název souboru v úložišti o přijetí změn konfigurace.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-137">FileName in the pull configuration repository</span></span>

![Název souboru v úložišti konfigurace.](../images/PartialInConfigRepository.png)

<span data-ttu-id="2c2fe-139">Název služby Azure Automation generované soubory MOF jako `<ConfigurationName>.<NodeName>.mof`.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-139">Azure Automation service name generated MOF files as `<ConfigurationName>.<NodeName>.mof`.</span></span>
<span data-ttu-id="2c2fe-140">Konfigurace níže tak kompiluje PartialOne.localhost.mof.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-140">So the configuration below compiles to PartialOne.localhost.mof.</span></span>

<span data-ttu-id="2c2fe-141">Kvůli tomu bylo možné pro akce pull, jedna částečná konfigurace ze služby Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-141">This made it impossible to pull one of your partial configuration from Azure Automation service.</span></span>

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

<span data-ttu-id="2c2fe-142">Ve WMF 5.1 částečné konfigurace v serveru nebo služby o přijetí změn může mít název jako `<ConfigurationName>.<NodeName>.mof`.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-142">In WMF 5.1, a partial configuration in the pull server/service can be named as `<ConfigurationName>.<NodeName>.mof`.</span></span>
<span data-ttu-id="2c2fe-143">Kromě toho pokud počítač s konfigurací jedné z o přijetí změn táhne server nebo služba potom konfiguračního souboru v úložišti konfigurace serveru o přijetí změn může mít libovolný název souboru.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-143">Moreover, if a machine is pulling a single configuration from a pull server/service then the configuration file on the pull server configuration repository can have any file name.</span></span>
<span data-ttu-id="2c2fe-144">Pojmenování díky této flexibilitě vám umožní spravovat uzly částečně ve službě Azure Automation, kde některé konfigurace pro uzel pochází z Azure Automation DSC a s částečnou konfigurací, které spravujete místně.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-144">This naming flexibility allows you to manage your nodes partially by Azure Automation service, where some configuration for your node is coming from Azure Automation DSC and with a partial configuration that you manage locally.</span></span>

<span data-ttu-id="2c2fe-145">Metaconfiguration níže nastaví uzel za spravované obě služby místně i ve službě Azure Automation.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-145">The metaconfiguration below sets up a node to be managed both locally as well as by Azure Automation service.</span></span>

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

## <a name="using-psdscrunascredential-with-dsc-composite-resources"></a><span data-ttu-id="2c2fe-146">Pomocí PsDscRunAsCredential složené prostředky DSC</span><span class="sxs-lookup"><span data-stu-id="2c2fe-146">Using PsDscRunAsCredential with DSC composite resources</span></span>

<span data-ttu-id="2c2fe-147">Přidali jsme podporu pro používání [ *PsDscRunAsCredential* ](https://msdn.microsoft.com/cs-cz/powershell/dsc/runasuser) s DSC [složené](https://msdn.microsoft.com/powershell/dsc/authoringresourcecomposite) prostředky.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-147">We have added support for using [*PsDscRunAsCredential*](https://msdn.microsoft.com/cs-cz/powershell/dsc/runasuser) with DSC [Composite](https://msdn.microsoft.com/powershell/dsc/authoringresourcecomposite) resources.</span></span>

<span data-ttu-id="2c2fe-148">Nyní můžete zadat hodnotu pro PsDscRunAsCredential při použití složené prostředky uvnitř konfigurace.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-148">You can now specify a value for PsDscRunAsCredential when using composite resources inside configurations.</span></span>
<span data-ttu-id="2c2fe-149">-Li zadána, spustit všechny prostředky uvnitř složených prostředků jako uživatele RunAs.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-149">When specified, all resources run inside a composite resource as a RunAs user.</span></span>
<span data-ttu-id="2c2fe-150">Volá-li složený prostředek jiný složený prostředek, všechny její prostředky jsou spouštěny, jako uživatele RunAs.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-150">If a composite resource calls another composite resource, all of its resources are also executed as RunAs user.</span></span>
<span data-ttu-id="2c2fe-151">Pověření spustit jako se rozšíří na libovolné úrovni hierarchie složených prostředků.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-151">RunAs credentials are propagated to any level of the composite resource hierarchy.</span></span>
<span data-ttu-id="2c2fe-152">Pokud prostředek uvnitř složených prostředků určuje jeho vlastní hodnotě. pro PsDscRunAsCredential, Chyba sloučení výsledků během kompilace konfigurace.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-152">If any resource inside a composite resource specifies its own value for PsDscRunAsCredential, a merge error results during configuration compilation.</span></span>

<span data-ttu-id="2c2fe-153">Tento příklad ukazuje použití s [WindowsFeatureSet](https://msdn.microsoft.com/powershell/wmf/dsc_newresources) složených prostředků zahrnuté v modulu PSDesiredStateConfiguration.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-153">This example shows usage with [WindowsFeatureSet](https://msdn.microsoft.com/powershell/wmf/dsc_newresources) composite resource included in PSDesiredStateConfiguration module.</span></span>

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

## <a name="dsc-module-and-configuration-signing-validations"></a><span data-ttu-id="2c2fe-154">Modul DSC a konfiguraci podepisování ověření</span><span class="sxs-lookup"><span data-stu-id="2c2fe-154">DSC module and configuration signing validations</span></span>

<span data-ttu-id="2c2fe-155">V DSC, konfigurace a moduly jsou rozděleny do spravovaných počítačů ze serveru vyžádané replikace.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-155">In DSC, configurations and modules are distributed to managed computers from the pull server.</span></span>
<span data-ttu-id="2c2fe-156">Pokud dojde k narušení serveru vyžádané replikace útočník potenciálně upravit konfigurace a moduly na tomto serveru a byl distribuován do všech spravovaných uzlů, tím bylo narušeno všechny z nich.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-156">If the pull server is compromised, an attacker can potentially modify the configurations and modules on the pull server and have it distributed to all managed nodes, compromising all of them.</span></span>

<span data-ttu-id="2c2fe-157">Ve WMF 5.1 podporuje ověřují digitální podpisy v katalogu a konfigurace DSC (. Soubory MOF).</span><span class="sxs-lookup"><span data-stu-id="2c2fe-157">In WMF 5.1, DSC supports validating the digital signatures on catalog and configuration (.MOF) files.</span></span>
<span data-ttu-id="2c2fe-158">Tato funkce zabraňuje uzly provádění konfigurace nebo modul soubory nejsou podepsány důvěryhodným podepisující osoba nebo který bylo pravděpodobně úmyslně po byly podepsány důvěryhodným podepisující osoba.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-158">This feature prevents nodes from executing configurations or module files which are not signed by a trusted signer or which have been tampered with after they have been signed by trusted signer.</span></span>

### <a name="how-to-sign-configuration-and-module"></a><span data-ttu-id="2c2fe-159">Jak zaregistrovat modul a konfigurace</span><span class="sxs-lookup"><span data-stu-id="2c2fe-159">How to sign configuration and module</span></span>

***
* <span data-ttu-id="2c2fe-160">Konfigurační soubory (. Soubory MOF): existující rutiny Powershellu [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) je rozšířeno pro podporu podepisování souborů MOF.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-160">Configuration Files (.MOFs): The existing PowerShell cmdlet [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) is extended to support signing of MOF files.</span></span>
* <span data-ttu-id="2c2fe-161">Moduly: Podepisování modulů se provádí po přihlášení odpovídající modulu katalogu pomocí následujících kroků:</span><span class="sxs-lookup"><span data-stu-id="2c2fe-161">Modules: Signing of modules is done by signing the corresponding module catalog using the following steps:</span></span>
    1. <span data-ttu-id="2c2fe-162">Vytvořte soubor katalogu: soubor katalogu obsahuje kolekci kryptografické hodnoty hash nebo kryptografické otisky.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-162">Create a catalog file: A catalog file contains a collection of cryptographic hashes or thumbprints.</span></span>
       <span data-ttu-id="2c2fe-163">Každý kryptografický otisk odpovídá souboru, který je součástí modulu.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-163">Each thumbprint corresponds to a file that is included in the module.</span></span>
       <span data-ttu-id="2c2fe-164">Nová rutina [New-FileCatalog](https://technet.microsoft.com/library/cc732148.aspx), byl přidán do povolí uživatelům vytvářet soubor katalogu pro jejich modulu.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-164">The new cmdlet [New-FileCatalog](https://technet.microsoft.com/library/cc732148.aspx), has been added to enable users to create a catalog file for their module.</span></span>
    2. <span data-ttu-id="2c2fe-165">Podepsat soubor katalogu: použití [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) k podepsání souboru katalogu.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-165">Sign the catalog file: Use [Set-AuthenticodeSignature](https://technet.microsoft.com/library/hh849819.aspx) to sign the catalog file.</span></span>
    3. <span data-ttu-id="2c2fe-166">Umístěte soubor katalogu ve složce modulu.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-166">Place the catalog file inside the module folder.</span></span>
<span data-ttu-id="2c2fe-167">Podle konvence modulu katalogu má být umístěn ve složce modulu se stejným názvem jako modul.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-167">By convention, module catalog file should be placed under the module folder with the same name as the module.</span></span>

### <a name="localconfigurationmanager-settings-to-enable-signing-validations"></a><span data-ttu-id="2c2fe-168">LocalConfigurationManager nastavení pro povolení ověření podpisu</span><span class="sxs-lookup"><span data-stu-id="2c2fe-168">LocalConfigurationManager settings to enable signing validations</span></span>

#### <a name="pull"></a><span data-ttu-id="2c2fe-169">O přijetí změn</span><span class="sxs-lookup"><span data-stu-id="2c2fe-169">Pull</span></span>

<span data-ttu-id="2c2fe-170">LocalConfigurationManager uzel provádí podpisový ověření modulů a konfigurací na základě aktuální nastavení.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-170">The LocalConfigurationManager of a node performs signing validation of modules and configurations based on its current settings.</span></span>
<span data-ttu-id="2c2fe-171">Ověření podpisu je ve výchozím nastavení zakázána.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-171">By default, signature validation is disabled.</span></span>
<span data-ttu-id="2c2fe-172">Ověření podpisu je povolit tak, že přidáte blok "SignatureValidation" definici meta konfigurace typu uzlu jak je znázorněno níže:</span><span class="sxs-lookup"><span data-stu-id="2c2fe-172">Signature validation can enabled by adding the ‘SignatureValidation’ block to the meta-configuration definition of the node as shown below:</span></span>

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
        # If the TrustedStorePath property is provided then LCM will use the custom path. Otherwise, the LCM will use default trusted store path (Cert:\LocalMachine\DSCStore) to find the signing certificate.
        TrustedStorePath = 'Cert:\LocalMachine\DSCStore'
        SignedItemType = 'Configuration','Module'         # This is a list of DSC artifacts, for which LCM need to verify their digital signature before executing them on the node.
    }

}
EnableSignatureValidation
Set-DscLocalConfigurationManager -Path .\EnableSignatureValidation -Verbose
```

<span data-ttu-id="2c2fe-173">V uzlu nastavení výše metaconfiguration umožňuje ověřit podpis staženého konfigurace a moduly.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-173">Setting the above metaconfiguration on a node enables signature validation on downloaded configurations and modules.</span></span>
<span data-ttu-id="2c2fe-174">Local Configuration Manageru provede následující kroky k ověření digitálních podpisů.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-174">The Local Configuration Manager performs the following steps to verify the digital signatures.</span></span>

1. <span data-ttu-id="2c2fe-175">Ověření podpisu pro soubor konfigurace (. Platnost MOF).</span><span class="sxs-lookup"><span data-stu-id="2c2fe-175">Verify the signature on a configuration file (.MOF) is valid.</span></span>
   <span data-ttu-id="2c2fe-176">Použije rutinu prostředí PowerShell [Get-AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx), což je rozšířená 5.1 pro podporu ověřování podpisu MOF.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-176">It uses the PowerShell cmdlet [Get-AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx), which is extended in 5.1 to support MOF signature validation.</span></span>
2. <span data-ttu-id="2c2fe-177">Ověřte, že certifikační autorita, která oprávnění podpisu je důvěryhodný.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-177">Verify the certificate authority that authorized the signer is trusted.</span></span>
3. <span data-ttu-id="2c2fe-178">Stáhněte si závislosti modulu nebo prostředek konfigurace do dočasného umístění.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-178">Download module/resource dependencies of the configuration to a temp location.</span></span>
4. <span data-ttu-id="2c2fe-179">Ověření podpisu katalogu, zahrnuty uvnitř modulu.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-179">Verify the signature of the catalog included inside the module.</span></span>
    * <span data-ttu-id="2c2fe-180">Najít `<moduleName>.cat` souboru a ověření jeho podpisu pomocí rutiny [Get-AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx).</span><span class="sxs-lookup"><span data-stu-id="2c2fe-180">Find a `<moduleName>.cat` file and verify its signature using the cmdlet  [Get-AuthenticodeSignature](https://technet.microsoft.com/library/hh849805.aspx).</span></span>
    * <span data-ttu-id="2c2fe-181">Ověřte, že certifikační autorita, která ověření podpisu je důvěryhodný.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-181">Verify the certification authority that authenticated the signer is trusted.</span></span>
    * <span data-ttu-id="2c2fe-182">Ověřte obsah moduly nikdo neoprávněně nemanipuloval pomocí nové rutiny [testovací FileCatalog](https://technet.microsoft.com/library/cc732148.aspx).</span><span class="sxs-lookup"><span data-stu-id="2c2fe-182">Verify the content of the modules has not been tampered using the new cmdlet [Test-FileCatalog](https://technet.microsoft.com/library/cc732148.aspx).</span></span>
5. <span data-ttu-id="2c2fe-183">Install-Module k $env: ProgramFiles\WindowsPowerShell\Modules\\</span><span class="sxs-lookup"><span data-stu-id="2c2fe-183">Install-Module to $env:ProgramFiles\WindowsPowerShell\Modules\\</span></span>
6. <span data-ttu-id="2c2fe-184">Konfigurace procesu</span><span class="sxs-lookup"><span data-stu-id="2c2fe-184">Process configuration</span></span>

> <span data-ttu-id="2c2fe-185">Poznámka: Ověření podpisu v modulu katalogu a konfigurace se provádí pouze při použití konfigurace k systému poprvé nebo když je stažen a nainstalován modul.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-185">Note: Signature validation on module-catalog and configuration is only performed when the configuration is applied to the system for the first time or when the module is downloaded and installed.</span></span>
<span data-ttu-id="2c2fe-186">Spuštění konzistence nelze ověřit podpis Current.mof nebo jeho závislosti modulu.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-186">Consistency runs do not validate the signature of Current.mof or its module dependencies.</span></span>
<span data-ttu-id="2c2fe-187">Pokud ověření se nezdařilo v jakékoli fázi, například pokud konfigurace získaných z serveru vyžádané replikace je bez znaménka, pak zpracování konfigurace skončí s chybou je uvedeno níže a se odstraní všechny dočasné soubory.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-187">If verification has failed at any stage, for instance, if the configuration pulled from the pull server is unsigned, then processing of the configuration terminates with the error shown below and all temporary files are deleted.</span></span>

![Konfigurace výstupu Chyba vzorku](../images/PullUnsignedConfigFail.png)

<span data-ttu-id="2c2fe-189">Obdobně souhrnné informace modulu, jehož katalog není podepsaný za následek následující chybě:</span><span class="sxs-lookup"><span data-stu-id="2c2fe-189">Similarly, pulling a module whose catalog is not signed results in the following error:</span></span>

![Ukázka chyby výstupu modulu](../images/PullUnisgnedCatalog.png)

#### <a name="push"></a><span data-ttu-id="2c2fe-191">nabízených oznámení</span><span class="sxs-lookup"><span data-stu-id="2c2fe-191">Push</span></span>

<span data-ttu-id="2c2fe-192">Předtím, než se doručí do uzlu, může být úmyslně konfigurace doručit pomocí nabízené instalace v jejich zdroji.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-192">A configuration delivered by using push might be tampered with at its source before it delivered to the node.</span></span>
<span data-ttu-id="2c2fe-193">Místní Configuration Manager provádí podobným způsobem ověření podpisu pro vložené nebo publikované konfigurace.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-193">The Local Configuration Manager performs similar signature validation steps for pushed or published configuration(s).</span></span>
<span data-ttu-id="2c2fe-194">Níže je úplný Příklad ověření podpisu pro nabízené oznámení.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-194">Below is a complete example of signature validation for push.</span></span>

- <span data-ttu-id="2c2fe-195">Povolení ověření podpisu na uzlu.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-195">Enable signature validation on the node.</span></span>

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

- <span data-ttu-id="2c2fe-196">Vytvořte ukázkový konfigurační soubor.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-196">Create a sample configuration file.</span></span>

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

- <span data-ttu-id="2c2fe-197">Zkuste doručením (push) bez znaménka konfiguračního souboru uzlu.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-197">Try pushing the unsigned configuration file in to the node.</span></span>

```powershell
Start-DscConfiguration -Path .\Test -Wait -Verbose -Force
```

![ErrorUnsignedMofPushed](../images/PushUnsignedMof.png)

- <span data-ttu-id="2c2fe-199">Podepište konfigurační soubor pomocí certifikátu pro podepisování kódu.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-199">Sign the configuration file using code-signing certificate.</span></span>

![SignMofFile](../images/SignMofFile.png)

- <span data-ttu-id="2c2fe-201">Zkuste nahráním podepsaného souboru MOF.</span><span class="sxs-lookup"><span data-stu-id="2c2fe-201">Try pushing the signed MOF file.</span></span>

![SignMofFile](../images/PushSignedMof.png)
