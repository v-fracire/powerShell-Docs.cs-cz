---
ms.date: 12/12/2018
keywords: DSC, powershell, konfigurace, instalační program
title: Publikování na serveru vyžádaných replikací s použitím ID konfigurace (v4/v5)
ms.openlocfilehash: 0144fec43d7a8d65b79891567cc0dc3952175343
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403686"
---
# <a name="publish-to-a-pull-server-using-configuration-ids-v4v5"></a><span data-ttu-id="f3a7f-103">Publikování na serveru vyžádaných replikací s použitím ID konfigurace (v4/v5)</span><span class="sxs-lookup"><span data-stu-id="f3a7f-103">Publish to a Pull Server using Configuration IDs (v4/v5)</span></span>

<span data-ttu-id="f3a7f-104">Následující části se předpokládá, že jste již nastavili serveru vyžádaných replikací s.</span><span class="sxs-lookup"><span data-stu-id="f3a7f-104">The sections below assume that you have already set up a Pull Server.</span></span> <span data-ttu-id="f3a7f-105">Pokud jste nenastavili serveru o přijetí změn, můžete použít následující příručky:</span><span class="sxs-lookup"><span data-stu-id="f3a7f-105">If you have not set up your Pull Server, you can use the following guides:</span></span>

- [<span data-ttu-id="f3a7f-106">Nastavení serveru vyžádané replikace DSC SMB</span><span class="sxs-lookup"><span data-stu-id="f3a7f-106">Set up a DSC SMB Pull Server</span></span>](pullServerSmb.md)
- [<span data-ttu-id="f3a7f-107">Nastavení serveru vyžádané replikace DSC HTTP</span><span class="sxs-lookup"><span data-stu-id="f3a7f-107">Set up a DSC HTTP Pull Server</span></span>](pullServer.md)

<span data-ttu-id="f3a7f-108">Každý cílový uzel je nakonfigurovat ke stažení konfigurace, prostředků a dokonce i oznámit svůj stav.</span><span class="sxs-lookup"><span data-stu-id="f3a7f-108">Each target node can be configured to download configurations, resources, and even report its status.</span></span> <span data-ttu-id="f3a7f-109">Tento článek vám ukáže jak nahrát prostředky, takže jsou k dispozici chcete stahovat a nastavte klienty, aby automaticky stáhnout prostředky.</span><span class="sxs-lookup"><span data-stu-id="f3a7f-109">This article will show you how to upload resources so they are available to be downloaded, and configure clients to download resources automatically.</span></span> <span data-ttu-id="f3a7f-110">Když uzel obdrží přiřazených konfigurací prostřednictvím **o přijetí změn** nebo **Push** (v5), automaticky stáhne všechny prostředky, které konfigurace z umístění zadaného v LCM vyžaduje.</span><span class="sxs-lookup"><span data-stu-id="f3a7f-110">When the Node's receives an assigned Configuration, through **Pull** or **Push** (v5), it automatically downloads any resources required by the Configuration from the location specified in the LCM.</span></span>

## <a name="compile-configurations"></a><span data-ttu-id="f3a7f-111">Kompilace konfigurace</span><span class="sxs-lookup"><span data-stu-id="f3a7f-111">Compile Configurations</span></span>

<span data-ttu-id="f3a7f-112">Prvním krokem při ukládání [konfigurace](../configurations/configurations.md) na serveru vyžádaných replikací s, je pro jejich zkompilování do souborů ".mof".</span><span class="sxs-lookup"><span data-stu-id="f3a7f-112">The first step to storing [Configurations](../configurations/configurations.md) on a Pull Server, is to compile them into ".mof" files.</span></span> <span data-ttu-id="f3a7f-113">Konfigurace obecných a pro víc klientů, použijete `localhost` v uzlu blokování.</span><span class="sxs-lookup"><span data-stu-id="f3a7f-113">To make a configuration generic, and applicable to more clients, use `localhost` in your Node block.</span></span> <span data-ttu-id="f3a7f-114">Následující příklad ukazuje konfigurační prostředí, které používá `localhost` místo názvu konkrétního klienta.</span><span class="sxs-lookup"><span data-stu-id="f3a7f-114">The example below shows a Configuration shell that uses `localhost` instead of a specific client name.</span></span>

```powershell
Configuration GenericConfig
{
    Node localhost
    {

    }
}
GenericConfig
```

<span data-ttu-id="f3a7f-115">Jakmile jste zkompilovali obecné konfigurace, měli byste mít "localhost.mof" soubor.</span><span class="sxs-lookup"><span data-stu-id="f3a7f-115">Once you have compiled your generic configuration, you should have a "localhost.mof" file.</span></span>

## <a name="renaming-the-mof-file"></a><span data-ttu-id="f3a7f-116">Přejmenování souboru MOF</span><span class="sxs-lookup"><span data-stu-id="f3a7f-116">Renaming the MOF file</span></span>

<span data-ttu-id="f3a7f-117">Můžete ukládat konfigurační soubory ".mof" na serveru vyžádané replikace pomocí **ConfigurationName** nebo **ConfigurationID**.</span><span class="sxs-lookup"><span data-stu-id="f3a7f-117">You can store Configuration ".mof" files on a Pull Server by **ConfigurationName** or **ConfigurationID**.</span></span> <span data-ttu-id="f3a7f-118">V závislosti na tom, jak budete chtít nastavit vaši klienti o přijetí změn můžete použít níže správně přejmenovat soubory kompilované ".mof".</span><span class="sxs-lookup"><span data-stu-id="f3a7f-118">Depending on how you plan to set up your pull clients, you can choose a section below to properly rename your compiled ".mof" files.</span></span>

### <a name="configuration-ids-guid"></a><span data-ttu-id="f3a7f-119">Konfigurace ID (GUID)</span><span class="sxs-lookup"><span data-stu-id="f3a7f-119">Configuration IDs (GUID)</span></span>

<span data-ttu-id="f3a7f-120">Budete muset přejmenovat soubor "localhost.mof" k "<GUID>.mof" soubor.</span><span class="sxs-lookup"><span data-stu-id="f3a7f-120">You will need to rename your "localhost.mof" file to "<GUID>.mof" file.</span></span> <span data-ttu-id="f3a7f-121">Můžete vytvořit náhodnou **Guid** pomocí příkladu níže nebo pomocí [nový identifikátor Guid](/powershell/module/microsoft.powershell.utility/new-guid) rutiny.</span><span class="sxs-lookup"><span data-stu-id="f3a7f-121">You can create a random **Guid** using the example below, or by using the [New-Guid](/powershell/module/microsoft.powershell.utility/new-guid) cmdlet.</span></span>

```powershell
[System.Guid]::NewGuid()
```

<span data-ttu-id="f3a7f-122">Ukázkový výstup</span><span class="sxs-lookup"><span data-stu-id="f3a7f-122">Sample Output</span></span>

```output
Guid
----
64856475-939e-41fb-aba5-4469f4006059
```

<span data-ttu-id="f3a7f-123">Přejmenujte soubor ".mof" pomocí libovolné metody přijatelné.</span><span class="sxs-lookup"><span data-stu-id="f3a7f-123">You can then rename your ".mof" file using any acceptable method.</span></span> <span data-ttu-id="f3a7f-124">V následujícím příkladu [přejmenovat položku](/powershell/module/microsoft.powershell.management/rename-item) rutiny.</span><span class="sxs-lookup"><span data-stu-id="f3a7f-124">The example below, uses the [Rename-Item](/powershell/module/microsoft.powershell.management/rename-item) cmdlet.</span></span>

```powershell
Rename-Item -Path .\localhost.mof -NewName '64856475-939e-41fb-aba5-4469f4006059.mof'
```

<span data-ttu-id="f3a7f-125">Další informace o používání **GUID** ve vašem prostředí, najdete v článku [plánování GUID](/powershell/dsc/secureserver#guids).</span><span class="sxs-lookup"><span data-stu-id="f3a7f-125">For more information about using **Guids** in your environment, see [Plan for Guids](/powershell/dsc/secureserver#guids).</span></span>

### <a name="configuration-names"></a><span data-ttu-id="f3a7f-126">Názvy konfigurace</span><span class="sxs-lookup"><span data-stu-id="f3a7f-126">Configuration Names</span></span>

<span data-ttu-id="f3a7f-127">Budete muset přejmenovat soubor "localhost.mof" k "<Configuration Name>.mof" soubor.</span><span class="sxs-lookup"><span data-stu-id="f3a7f-127">You will need to rename your "localhost.mof" file to "<Configuration Name>.mof" file.</span></span> <span data-ttu-id="f3a7f-128">V následujícím příkladu se používá název konfigurace z předchozí části.</span><span class="sxs-lookup"><span data-stu-id="f3a7f-128">In the following example, the configuration name from the previous section is used.</span></span> <span data-ttu-id="f3a7f-129">Přejmenujte soubor ".mof" pomocí libovolné metody přijatelné.</span><span class="sxs-lookup"><span data-stu-id="f3a7f-129">You can then rename your ".mof" file using any acceptable method.</span></span> <span data-ttu-id="f3a7f-130">V následujícím příkladu [přejmenovat položku](/powershell/module/microsoft.powershell.management/rename-item) rutiny.</span><span class="sxs-lookup"><span data-stu-id="f3a7f-130">The example below, uses the [Rename-Item](/powershell/module/microsoft.powershell.management/rename-item) cmdlet.</span></span>

```powershell
Rename-Item -Path .\localhost.mof -NewName 'GenericConfig.mof'
```

## <a name="create-the-checksum"></a><span data-ttu-id="f3a7f-131">Vytvořit kontrolní součet</span><span class="sxs-lookup"><span data-stu-id="f3a7f-131">Create the CheckSum</span></span>

<span data-ttu-id="f3a7f-132">Každý soubor ".mof" uloženy na serveru vyžádané replikace nebo sdílenou složku protokolu SMB musí mít přidružený ".checksum" soubor.</span><span class="sxs-lookup"><span data-stu-id="f3a7f-132">Each ".mof" file stored on a Pull Server, or SMB share needs to have an associated ".checksum" file.</span></span> <span data-ttu-id="f3a7f-133">Tento soubor umožňuje klientům vědět, kdy přidružené ".mof" soubor došlo ke změně a by měl být staženy znovu.</span><span class="sxs-lookup"><span data-stu-id="f3a7f-133">This file lets clients know when the associated ".mof" file has changed and should be downloaded again.</span></span>

<span data-ttu-id="f3a7f-134">Můžete vytvořit **kontrolního součtu** s [New-DSCCheckSum](/powershell/module/psdesiredstateconfiguration/new-dscchecksum) rutiny.</span><span class="sxs-lookup"><span data-stu-id="f3a7f-134">You can create a **CheckSum** with the [New-DSCCheckSum](/powershell/module/psdesiredstateconfiguration/new-dscchecksum) cmdlet.</span></span> <span data-ttu-id="f3a7f-135">Můžete také spustit `New-DSCCheckSum` proti adresář souborů pomocí `-Path` parametru.</span><span class="sxs-lookup"><span data-stu-id="f3a7f-135">You can also run `New-DSCCheckSum` against a directory of files using the `-Path` parameter.</span></span> <span data-ttu-id="f3a7f-136">Pokud kontrolní součet již existuje, lze vynutit být znovu vytvořen s `-Force` parametru.</span><span class="sxs-lookup"><span data-stu-id="f3a7f-136">If a checksum already exists, you can force it to be re-created with the `-Force` parameter.</span></span> <span data-ttu-id="f3a7f-137">Následující příklad zadaný adresář obsahující soubor ".mof" z předchozí části a používá `-Force` parametru.</span><span class="sxs-lookup"><span data-stu-id="f3a7f-137">The following example specified a directory containing the ".mof" file from the previous section, and uses the `-Force` parameter.</span></span>

```powershell
New-DscChecksum -Path '.\' -Force
```

<span data-ttu-id="f3a7f-138">Žádný výstup se nezobrazí, ale měli byste vidět "<GUID or Configuration Name>. mof.checksum" soubor.</span><span class="sxs-lookup"><span data-stu-id="f3a7f-138">No output will be shown, but you should now see a "<GUID or Configuration Name>.mof.checksum" file.</span></span>

## <a name="where-to-store-mof-files-and-checksums"></a><span data-ttu-id="f3a7f-139">Kam se mají ukládat soubory MOF a kontrolní součty</span><span class="sxs-lookup"><span data-stu-id="f3a7f-139">Where to store MOF files and CheckSums</span></span>

### <a name="on-a-dsc-http-pull-server"></a><span data-ttu-id="f3a7f-140">Na Server DSC na vyžádání protokolu HTTP</span><span class="sxs-lookup"><span data-stu-id="f3a7f-140">On a DSC HTTP Pull Server</span></span>

<span data-ttu-id="f3a7f-141">Při nastavení HTTP serveru o přijetí změn, jak je vysvětleno v [nastavení serveru vyžádané replikace DSC HTTP](pullServer.md), určit adresáře pro **ModulePath** a **ConfigurationPath** klíče.</span><span class="sxs-lookup"><span data-stu-id="f3a7f-141">When you set up your HTTP Pull Server, as explained in [Set up a DSC HTTP Pull Server](pullServer.md), you specify directories for the **ModulePath** and **ConfigurationPath** keys.</span></span> <span data-ttu-id="f3a7f-142">**ConfigurationPath** klíč označuje ukládat všechny soubory ".mof".</span><span class="sxs-lookup"><span data-stu-id="f3a7f-142">The **ConfigurationPath** key indicates where any ".mof" files should be stored.</span></span> <span data-ttu-id="f3a7f-143">**ConfigurationPath** označuje, kde by měla být uložena všechny soubory ".mof" a ".checksum".</span><span class="sxs-lookup"><span data-stu-id="f3a7f-143">The **ConfigurationPath** indicates where any ".mof" files and ".checksum" files should be stored.</span></span>

```powershell
    xDscWebService PSDSCPullServer
    {
    ...
        ModulePath              = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Modules"
        ConfigurationPath       = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration"
    ...
    }

```

### <a name="on-an-smb-share"></a><span data-ttu-id="f3a7f-144">Ve sdílené složce protokolu SMB</span><span class="sxs-lookup"><span data-stu-id="f3a7f-144">On an SMB Share</span></span>

<span data-ttu-id="f3a7f-145">Při nastavování klienta o přijetí změn do použít sdílenou složku SMB, zadejte **ConfigurationRepositoryShare**.</span><span class="sxs-lookup"><span data-stu-id="f3a7f-145">When you set up a Pull Client to use an SMB share, you specify a **ConfigurationRepositoryShare**.</span></span> <span data-ttu-id="f3a7f-146">Všechny soubory ".mof" a ".checksum" soubory pak je ukládat **SourcePath** z **ConfigurationRepositoryShare** bloku.</span><span class="sxs-lookup"><span data-stu-id="f3a7f-146">All ".mof" files and ".checksum" files should then be stored in the **SourcePath** directory from the **ConfigurationRepositoryShare** block.</span></span>

```powershell
ConfigurationRepositoryShare SMBPullServer
{
    SourcePath = '\\SMBPullServer\Pull'
}
```

## <a name="next-steps"></a><span data-ttu-id="f3a7f-147">Další kroky</span><span class="sxs-lookup"><span data-stu-id="f3a7f-147">Next Steps</span></span>

<span data-ttu-id="f3a7f-148">V dalším kroku bude chtít nakonfigurovat klienty o přijetí změn pro vyžádanou zadanou konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="f3a7f-148">Next, you will want to configure Pull Clients to pull the specified configuration.</span></span> <span data-ttu-id="f3a7f-149">Další informace naleznete v následujících příručkách:</span><span class="sxs-lookup"><span data-stu-id="f3a7f-149">For more information, see one of the following guides:</span></span>

- [<span data-ttu-id="f3a7f-150">Při nastavování klienta o přijetí změn pomocí ID konfigurace (v4)</span><span class="sxs-lookup"><span data-stu-id="f3a7f-150">Set up a Pull Client using Configuration IDs (v4)</span></span>](pullClientConfigId4.md)
- [<span data-ttu-id="f3a7f-151">Při nastavování klienta o přijetí změn pomocí ID konfigurace (v5)</span><span class="sxs-lookup"><span data-stu-id="f3a7f-151">Set up a Pull Client using Configuration IDs (v5)</span></span>](pullClientConfigId.md)
- [<span data-ttu-id="f3a7f-152">Při nastavování klienta o přijetí změn použití konfiguračních názvů (v5)</span><span class="sxs-lookup"><span data-stu-id="f3a7f-152">Set up a Pull Client using Configuration Names (v5)</span></span>](pullClientConfigNames.md)

## <a name="see-also"></a><span data-ttu-id="f3a7f-153">Viz taky</span><span class="sxs-lookup"><span data-stu-id="f3a7f-153">See also</span></span>

- [<span data-ttu-id="f3a7f-154">Nastavení serveru vyžádané replikace DSC SMB</span><span class="sxs-lookup"><span data-stu-id="f3a7f-154">Set up a DSC SMB Pull Server</span></span>](pullServerSmb.md)
- [<span data-ttu-id="f3a7f-155">Nastavení serveru vyžádané replikace DSC HTTP</span><span class="sxs-lookup"><span data-stu-id="f3a7f-155">Set up a DSC HTTP Pull Server</span></span>](pullServer.md)
- [<span data-ttu-id="f3a7f-156">Balíček a prostředky nahrávání na serveru vyžádané replikace</span><span class="sxs-lookup"><span data-stu-id="f3a7f-156">Package and Upload Resources to a Pull Server</span></span>](package-upload-resources.md)
