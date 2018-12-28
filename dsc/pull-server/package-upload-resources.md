---
ms.date: 12/12/2018
keywords: DSC, powershell, konfigurace, instalační program
title: Balíček a prostředky nahrávání na serveru vyžádané replikace
ms.openlocfilehash: 29a62f96393a53c9e7da57a5e51732dcb0937194
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403661"
---
# <a name="package-and-upload-resources-to-a-pull-server"></a><span data-ttu-id="06427-103">Balíček a prostředky nahrávání na serveru vyžádané replikace</span><span class="sxs-lookup"><span data-stu-id="06427-103">Package and Upload Resources to a Pull Server</span></span>

<span data-ttu-id="06427-104">Následující části se předpokládá, že jste již nastavili serveru vyžádaných replikací s.</span><span class="sxs-lookup"><span data-stu-id="06427-104">The sections below assume that you have already set up a Pull Server.</span></span> <span data-ttu-id="06427-105">Pokud jste nenastavili serveru o přijetí změn, můžete použít následující příručky:</span><span class="sxs-lookup"><span data-stu-id="06427-105">If you have not set up your Pull Server, you can use the following guides:</span></span>

- [<span data-ttu-id="06427-106">Nastavení serveru vyžádané replikace DSC SMB</span><span class="sxs-lookup"><span data-stu-id="06427-106">Set up a DSC SMB Pull Server</span></span>](pullServerSmb.md)
- [<span data-ttu-id="06427-107">Nastavení serveru vyžádané replikace DSC HTTP</span><span class="sxs-lookup"><span data-stu-id="06427-107">Set up a DSC HTTP Pull Server</span></span>](pullServer.md)

<span data-ttu-id="06427-108">Každý cílový uzel je nakonfigurovat ke stažení konfigurace, prostředků a dokonce i oznámit svůj stav.</span><span class="sxs-lookup"><span data-stu-id="06427-108">Each target node can be configured to download configurations, resources, and even report its status.</span></span> <span data-ttu-id="06427-109">Tento článek vám ukáže jak nahrát prostředky, takže jsou k dispozici chcete stahovat a nastavte klienty, aby automaticky stáhnout prostředky.</span><span class="sxs-lookup"><span data-stu-id="06427-109">This article will show you how to upload resources so they are available to be downloaded, and configure clients to download resources automatically.</span></span> <span data-ttu-id="06427-110">Když uzel obdrží přiřazených konfigurací prostřednictvím **o přijetí změn** nebo **Push** (v5), automaticky stáhne všechny prostředky, které konfigurace z umístění zadaného v LCM vyžaduje.</span><span class="sxs-lookup"><span data-stu-id="06427-110">When the Node's receives an assigned Configuration, through **Pull** or **Push** (v5), it automatically downloads any resources required by the Configuration from the location specified in the LCM.</span></span>

## <a name="package-resource-modules"></a><span data-ttu-id="06427-111">Balíček prostředků moduly</span><span class="sxs-lookup"><span data-stu-id="06427-111">Package Resource Modules</span></span>

<span data-ttu-id="06427-112">Každý prostředek k dispozici pro klienty ke stažení musí být uložen v souboru ".zip".</span><span class="sxs-lookup"><span data-stu-id="06427-112">Each resource available for a client to download must be stored in a ".zip" file.</span></span> <span data-ttu-id="06427-113">Následující příklad zobrazí požadované kroky pomocí [xPSDesiredStateConfiguration](https://www.powershellgallery.com/packages/xPSDesiredStateConfiguration/8.4.0.0) prostředků.</span><span class="sxs-lookup"><span data-stu-id="06427-113">The example below will show the required steps using the [xPSDesiredStateConfiguration](https://www.powershellgallery.com/packages/xPSDesiredStateConfiguration/8.4.0.0) resource.</span></span>

> [!NOTE]
> <span data-ttu-id="06427-114">Pokud máte klienty pomocí prostředí PowerShell 4.0, bude muset flaten strukturu složek prostředků a odeberte všechny verze složky.</span><span class="sxs-lookup"><span data-stu-id="06427-114">If you have any clients using PowerShell 4.0, you will need to flaten the resource folder structure and remove any version folders.</span></span> <span data-ttu-id="06427-115">Další informace najdete v tématu [více verzí prostředků](../configurations/import-dscresource.md#multiple-resource-versions).</span><span class="sxs-lookup"><span data-stu-id="06427-115">For more information, see [Multiple Resource Versions](../configurations/import-dscresource.md#multiple-resource-versions).</span></span>

<span data-ttu-id="06427-116">Adresář prostředků pomocí libovolný nástroj, skript nebo metod, které dáváte přednost dokáže komprimovat.</span><span class="sxs-lookup"><span data-stu-id="06427-116">You can compress the resource directory using any utility, script, or method that you prefer.</span></span> <span data-ttu-id="06427-117">Ve Windows, můžete *klikněte pravým tlačítkem na* na adresář "xPSDesiredStateConfiguration" a vyberte "Odeslat" a potom "Komprimovanou složku".</span><span class="sxs-lookup"><span data-stu-id="06427-117">In Windows, you can *right-click* on the "xPSDesiredStateConfiguration" directory, and select "Send To", then "Compressed Folder".</span></span>

![Klikněte pravým tlačítkem myši](../media/right-click.gif)

### <a name="naming-the-resource-archive"></a><span data-ttu-id="06427-119">Pojmenování prostředků archivu</span><span class="sxs-lookup"><span data-stu-id="06427-119">Naming the Resource Archive</span></span>

<span data-ttu-id="06427-120">Prostředek archive musí mít názvy v následujícím formátu:</span><span class="sxs-lookup"><span data-stu-id="06427-120">The Resource archive needs to be named with the following format:</span></span>

```
{ModuleName}_{Version}.zip
```

<span data-ttu-id="06427-121">V předchozím příkladu by měl být "xPSDesiredStateConfiguration.zip" přejmenováno "xPSDesiredStateConfiguration_8.4.4.0.zip".</span><span class="sxs-lookup"><span data-stu-id="06427-121">In the example above, "xPSDesiredStateConfiguration.zip" should be renamed "xPSDesiredStateConfiguration_8.4.4.0.zip".</span></span>

### <a name="create-checksums"></a><span data-ttu-id="06427-122">Vytvořit kontrolní součty</span><span class="sxs-lookup"><span data-stu-id="06427-122">Create CheckSums</span></span>

<span data-ttu-id="06427-123">Jakmile modul prostředků byl komprimované a přejmenovat, je potřeba vytvořit **kontrolního součtu**.</span><span class="sxs-lookup"><span data-stu-id="06427-123">Once the Resource module has been compressed and renamed, you need to create a **CheckSum**.</span></span>  <span data-ttu-id="06427-124">**Kontrolního součtu** používají, LCM na straně klienta, k určení, zda prostředek byl změněn a musí být znovu stažena.</span><span class="sxs-lookup"><span data-stu-id="06427-124">The **CheckSum** is used, by the LCM on the client, to determine if the resource has been changed, and needs to be downloaded again.</span></span> <span data-ttu-id="06427-125">Můžete vytvořit **kontrolního součtu** s [New-DSCCheckSum](/powershell/module/PSDesiredStateConfiguration/New-DSCCheckSum) rutiny, jak je znázorněno v následujícím příkladu.</span><span class="sxs-lookup"><span data-stu-id="06427-125">You can create a **CheckSum** with the [New-DSCCheckSum](/powershell/module/PSDesiredStateConfiguration/New-DSCCheckSum) cmdlet, as shown in the example below.</span></span>

```powershell
New-DscChecksum -Path .\xPSDesiredStateConfiguration_8.4.4.0.zip
```

<span data-ttu-id="06427-126">Žádný výstup se nezobrazí, ale měli byste vidět "xPSDesiredStateConfiguration_8.4.4.0.zip.checksum".</span><span class="sxs-lookup"><span data-stu-id="06427-126">No output will be shown, but you should now see a "xPSDesiredStateConfiguration_8.4.4.0.zip.checksum".</span></span> <span data-ttu-id="06427-127">Můžete také spustit `New-DSCCheckSum` proti adresář souborů pomocí `-Path` parametru.</span><span class="sxs-lookup"><span data-stu-id="06427-127">You can also run `New-DSCCheckSum` against a directory of files using the `-Path` parameter.</span></span> <span data-ttu-id="06427-128">Pokud kontrolní součet již existuje, lze vynutit být znovu vytvořen s `-Force` parametru.</span><span class="sxs-lookup"><span data-stu-id="06427-128">If a checksum already exists, you can force it to be re-created with the `-Force` parameter.</span></span>

### <a name="where-to-store-resource-archives"></a><span data-ttu-id="06427-129">Kam se mají ukládat prostředků archivy</span><span class="sxs-lookup"><span data-stu-id="06427-129">Where to store Resource Archives</span></span>

#### <a name="on-a-dsc-http-pull-server"></a><span data-ttu-id="06427-130">Na Server DSC na vyžádání protokolu HTTP</span><span class="sxs-lookup"><span data-stu-id="06427-130">On a DSC HTTP Pull Server</span></span>

<span data-ttu-id="06427-131">Při nastavení HTTP serveru o přijetí změn, jak je vysvětleno v [nastavení serveru vyžádané replikace DSC HTTP](pullServer.md), určit adresáře pro **ModulePath** a **ConfigurationPath** klíče.</span><span class="sxs-lookup"><span data-stu-id="06427-131">When you set up your HTTP Pull Server, as explained in [Set up a DSC HTTP Pull Server](pullServer.md), you specify directories for the **ModulePath** and **ConfigurationPath** keys.</span></span> <span data-ttu-id="06427-132">**ConfigurationPath** klíč označuje ukládat všechny soubory ".mof".</span><span class="sxs-lookup"><span data-stu-id="06427-132">The **ConfigurationPath** key indicates where any ".mof" files should be stored.</span></span> <span data-ttu-id="06427-133">**ModulePath** označuje, kde by měly být uloženy všechny moduly, které prostředek DSC.</span><span class="sxs-lookup"><span data-stu-id="06427-133">The **ModulePath** indicates where any DSC Resource Modules should be stored.</span></span>

```powershell
    xDscWebService PSDSCPullServer
    {
    ...
        ModulePath              = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Modules"
        ConfigurationPath       = "$env:PROGRAMFILES\WindowsPowerShell\DscService\Configuration"
    ...
    }

```

#### <a name="on-an-smb-share"></a><span data-ttu-id="06427-134">Ve sdílené složce protokolu SMB</span><span class="sxs-lookup"><span data-stu-id="06427-134">On an SMB Share</span></span>

<span data-ttu-id="06427-135">Pokud jste zadali **ResourceRepositoryShare**při nastavování vašeho klienta o přijetí změn ukládají archivy a kontrolní součty v **SourcePath** z **ResourceRepositoryShare** bloku.</span><span class="sxs-lookup"><span data-stu-id="06427-135">If you specified a **ResourceRepositoryShare**, when setting up your Pull Client, store archives and checksums in the **SourcePath** directory from the **ResourceRepositoryShare** block.</span></span>

```powershell
ConfigurationRepositoryShare SMBPullServer
{
    SourcePath = '\\SMBPullServer\Configurations'
}

ResourceRepositoryShare SMBResourceServer
{
    SourcePath = '\\SMBPullServer\Resources'
}
```

<span data-ttu-id="06427-136">Pokud jste zadali jenom **ConfigurationRepositoryShare**při nastavování vašeho klienta o přijetí změn ukládají archivy a kontrolní součty v **SourcePath** z  **ConfigurationRepositoryShare** bloku.</span><span class="sxs-lookup"><span data-stu-id="06427-136">If you specified only a **ConfigurationRepositoryShare**, when setting up your Pull Client, store archives and checksums in the **SourcePath** directory from the **ConfigurationRepositoryShare** block.</span></span>

```powershell
ConfigurationRepositoryShare SMBPullServer
{
    SourcePath = '\\SMBPullServer\Pull'
}
```

#### <a name="updating-resources"></a><span data-ttu-id="06427-137">Aktualizují se prostředky</span><span class="sxs-lookup"><span data-stu-id="06427-137">Updating resources</span></span>

<span data-ttu-id="06427-138">Můžete vynutit uzlu se aktualizovat jeho prostředky tak, že změníte číslo verze v archivu názvu nebo vytvořením nového kontrolního součtu.</span><span class="sxs-lookup"><span data-stu-id="06427-138">You can force a Node to update its resources by changing the version number in the archive's name, or by creating a new checksum.</span></span> <span data-ttu-id="06427-139">Klienta o přijetí změn zkontroluje novějších verzích požadované prostředky, jakož i aktualizovat kontrolní součty, při jeho LCM se aktualizuje.</span><span class="sxs-lookup"><span data-stu-id="06427-139">The Pull Client will check for newer versions of required resources, as well as updated checksums, when its LCM refreshes.</span></span>

## <a name="see-also"></a><span data-ttu-id="06427-140">Viz taky</span><span class="sxs-lookup"><span data-stu-id="06427-140">See also</span></span>

- [<span data-ttu-id="06427-141">Nastavení serveru vyžádané replikace DSC SMB</span><span class="sxs-lookup"><span data-stu-id="06427-141">Set up a DSC SMB Pull Server</span></span>](pullServerSmb.md)
- [<span data-ttu-id="06427-142">Nastavení serveru vyžádané replikace DSC HTTP</span><span class="sxs-lookup"><span data-stu-id="06427-142">Set up a DSC HTTP Pull Server</span></span>](pullServer.md)
