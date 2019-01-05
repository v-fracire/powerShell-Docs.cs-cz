---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředek DSC File
ms.openlocfilehash: e5f7a91e5f19c8c7bbada090804d8f29a7cfedd5
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048186"
---
# <a name="dsc-file-resource"></a><span data-ttu-id="52e4b-103">Prostředek DSC File</span><span class="sxs-lookup"><span data-stu-id="52e4b-103">DSC File Resource</span></span>

> <span data-ttu-id="52e4b-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="52e4b-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="52e4b-105">Prostředek File ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus ke správě souborů a složek na cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="52e4b-105">The File resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage files and folders on the target node.</span></span>

><span data-ttu-id="52e4b-106">**Poznámka:** Pokud **MatchSource** je nastavena na **$false** (což je výchozí hodnota), obsahu, které se mají zkopírovat jsou uložené v mezipaměti při prvním tato konfigurace používá.</span><span class="sxs-lookup"><span data-stu-id="52e4b-106">**Note:** If the **MatchSource** property is set to **$false** (which is the default value), the contents to be copied are cached the first time the configuration is applied.</span></span>
><span data-ttu-id="52e4b-107">Následné žádosti z konfigurace nebude kontrolovat aktualizované soubory nebo složky v cestě určené **SourcePath**.</span><span class="sxs-lookup"><span data-stu-id="52e4b-107">Subsequent applications of the configuration will not check for updated files and/or folders in the path specified by **SourcePath**.</span></span> <span data-ttu-id="52e4b-108">Pokud chcete vyhledat aktualizace pro soubory a složky v **SourcePath** pokaždé, když se tato konfigurace používá, nastavte **MatchSource** k **$true**.</span><span class="sxs-lookup"><span data-stu-id="52e4b-108">If you want to check for updates to the files and/or folders in **SourcePath** every time the configuration is applied, set **MatchSource** to **$true**.</span></span>

## <a name="syntax"></a><span data-ttu-id="52e4b-109">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="52e4b-109">Syntax</span></span>
```
File [string] #ResourceName
{
    DestinationPath = [string]
    [ Attributes = [string[]] { Archive | Hidden | ReadOnly | System }]
    [ Checksum = [string] { CreatedDate | ModifiedDate | SHA-1 | SHA-256 | SHA-512 } ]
    [ Contents = [string] ]
    [ Credential = [PSCredential] ]
    [ Ensure = [string] { Absent | Present } ]
    [ Force = [bool] ]
    [ Recurse = [bool] ]
    [ DependsOn = [string[]] ]
    [ SourcePath = [string] ]
    [ Type = [string] { Directory | File } ]
    [ MatchSource = [bool] ]
}
```

## <a name="properties"></a><span data-ttu-id="52e4b-110">Properties</span><span class="sxs-lookup"><span data-stu-id="52e4b-110">Properties</span></span>

|  <span data-ttu-id="52e4b-111">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="52e4b-111">Property</span></span>  |  <span data-ttu-id="52e4b-112">Popis</span><span class="sxs-lookup"><span data-stu-id="52e4b-112">Description</span></span>   |
|---|---|
| <span data-ttu-id="52e4b-113">DestinationPath</span><span class="sxs-lookup"><span data-stu-id="52e4b-113">DestinationPath</span></span>| <span data-ttu-id="52e4b-114">Označuje umístění, kam chcete zajistit stavu pro soubor nebo adresář.</span><span class="sxs-lookup"><span data-stu-id="52e4b-114">Indicates the location where you want to ensure the state for a file or directory.</span></span>|
| <span data-ttu-id="52e4b-115">Atributy</span><span class="sxs-lookup"><span data-stu-id="52e4b-115">Attributes</span></span>| <span data-ttu-id="52e4b-116">Určuje požadovaný stav atributy pro cílový soubor nebo adresář.</span><span class="sxs-lookup"><span data-stu-id="52e4b-116">Specifies the desired state of the attributes for the targeted file or directory.</span></span>|
| <span data-ttu-id="52e4b-117">Kontrolní součet</span><span class="sxs-lookup"><span data-stu-id="52e4b-117">Checksum</span></span>| <span data-ttu-id="52e4b-118">Určuje typ kontrolního součtu pro zjištění, zda dva soubory jsou stejné.</span><span class="sxs-lookup"><span data-stu-id="52e4b-118">Indicates the checksum type to use when determining whether two files are the same.</span></span> <span data-ttu-id="52e4b-119">Pokud __kontrolního součtu__ není zadán, pouze název souboru nebo složky se používá pro porovnání.</span><span class="sxs-lookup"><span data-stu-id="52e4b-119">If __Checksum__ is not specified, only the file or directory name is used for comparison.</span></span> <span data-ttu-id="52e4b-120">Platné hodnoty jsou: SHA-1, SHA-256, SHA-512, datum vytvoření, modifiedDate.</span><span class="sxs-lookup"><span data-stu-id="52e4b-120">Valid values include: SHA-1, SHA-256, SHA-512, createdDate, modifiedDate.</span></span>|
| <span data-ttu-id="52e4b-121">Obsah</span><span class="sxs-lookup"><span data-stu-id="52e4b-121">Contents</span></span>| <span data-ttu-id="52e4b-122">Určuje obsah souboru, jako je například konkrétní řetězec.</span><span class="sxs-lookup"><span data-stu-id="52e4b-122">Specifies the contents of a file, such as a particular string.</span></span>|
| <span data-ttu-id="52e4b-123">Přihlašovací údaje</span><span class="sxs-lookup"><span data-stu-id="52e4b-123">Credential</span></span>| <span data-ttu-id="52e4b-124">Určuje přihlašovací údaje, které jsou požadovány pro přístup k prostředkům, jako je například zdrojové soubory, pokud takový přístup je povinný.</span><span class="sxs-lookup"><span data-stu-id="52e4b-124">Indicates the credentials that are required to access resources, such as source files, if such access is required.</span></span>|
| <span data-ttu-id="52e4b-125">Zkontrolujte</span><span class="sxs-lookup"><span data-stu-id="52e4b-125">Ensure</span></span>| <span data-ttu-id="52e4b-126">Určuje, jestli existuje soubor nebo adresář.</span><span class="sxs-lookup"><span data-stu-id="52e4b-126">Indicates if the file or directory exists.</span></span> <span data-ttu-id="52e4b-127">Nastavte tuto vlastnost na "Chybí" Ujistěte se, že soubor nebo adresář neexistuje.</span><span class="sxs-lookup"><span data-stu-id="52e4b-127">Set this property to "Absent" to ensure that the file or directory does not exist.</span></span> <span data-ttu-id="52e4b-128">Nastavte ho na "Obsahuje" Ujistěte se, že soubor nebo adresář neexistuje.</span><span class="sxs-lookup"><span data-stu-id="52e4b-128">Set it to "Present" to ensure that the file or directory does exist.</span></span> <span data-ttu-id="52e4b-129">Výchozí hodnota je "K dispozici".</span><span class="sxs-lookup"><span data-stu-id="52e4b-129">The default is "Present".</span></span>|
| <span data-ttu-id="52e4b-130">Force</span><span class="sxs-lookup"><span data-stu-id="52e4b-130">Force</span></span>| <span data-ttu-id="52e4b-131">Určité operace se soubory (například soubor přepsání nebo odstranění adresáře, který není prázdný) dojde chybě.</span><span class="sxs-lookup"><span data-stu-id="52e4b-131">Certain file operations (such as overwriting a file or deleting a directory that is not empty) will result in an error.</span></span> <span data-ttu-id="52e4b-132">Pomocí vlastnosti vynucení přepsání tyto chyby.</span><span class="sxs-lookup"><span data-stu-id="52e4b-132">Using the Force property overrides such errors.</span></span> <span data-ttu-id="52e4b-133">Výchozí hodnota je __$false__.</span><span class="sxs-lookup"><span data-stu-id="52e4b-133">The default value is __$false__.</span></span>|
| <span data-ttu-id="52e4b-134">Recurse</span><span class="sxs-lookup"><span data-stu-id="52e4b-134">Recurse</span></span>| <span data-ttu-id="52e4b-135">Uvádí, jestli jsou zahrnuté podadresářů.</span><span class="sxs-lookup"><span data-stu-id="52e4b-135">Indicates if subdirectories are included.</span></span> <span data-ttu-id="52e4b-136">Tuto vlastnost nastavte na __$true__ k označení, že chcete, aby podadresářů, které mají být zahrnuty.</span><span class="sxs-lookup"><span data-stu-id="52e4b-136">Set this property to __$true__ to indicate that you want subdirectories to be included.</span></span> <span data-ttu-id="52e4b-137">Výchozí hodnota je __$false__.</span><span class="sxs-lookup"><span data-stu-id="52e4b-137">The default is __$false__.</span></span> <span data-ttu-id="52e4b-138">**Poznámka:**: Tato vlastnost je platná pouze v případě vlastnost Type je nastavená na adresář.</span><span class="sxs-lookup"><span data-stu-id="52e4b-138">**Note**: This property is only valid when the Type property is set to Directory.</span></span>|
| <span data-ttu-id="52e4b-139">DependsOn</span><span class="sxs-lookup"><span data-stu-id="52e4b-139">DependsOn</span></span> | <span data-ttu-id="52e4b-140">Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="52e4b-140">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="52e4b-141">Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba __ResourceName__ a jejím typem je __ResourceType__, syntaxe pro použití této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="52e4b-141">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="52e4b-142">SourcePath</span><span class="sxs-lookup"><span data-stu-id="52e4b-142">SourcePath</span></span>| <span data-ttu-id="52e4b-143">Označuje cestu, ze kterého chcete kopírovat zdroje souboru nebo složky.</span><span class="sxs-lookup"><span data-stu-id="52e4b-143">Indicates the path from which to copy the file or folder resource.</span></span>|
| <span data-ttu-id="52e4b-144">Type</span><span class="sxs-lookup"><span data-stu-id="52e4b-144">Type</span></span>| <span data-ttu-id="52e4b-145">Určuje, zda je nakonfigurován prostředek je adresář nebo soubor.</span><span class="sxs-lookup"><span data-stu-id="52e4b-145">Indicates if the resource being configured is a directory or a file.</span></span> <span data-ttu-id="52e4b-146">Nastavte tuto vlastnost na "Directory" k označení, že je prostředek adresáře.</span><span class="sxs-lookup"><span data-stu-id="52e4b-146">Set this property to "Directory" to indicate that the resource is a directory.</span></span> <span data-ttu-id="52e4b-147">Nastavte ho na "File" označuje, že soubor prostředku.</span><span class="sxs-lookup"><span data-stu-id="52e4b-147">Set it to "File" to indicate that the resource is a file.</span></span> <span data-ttu-id="52e4b-148">Výchozí hodnota je "File".</span><span class="sxs-lookup"><span data-stu-id="52e4b-148">The default value is “File”.</span></span>|
| <span data-ttu-id="52e4b-149">MatchSource</span><span class="sxs-lookup"><span data-stu-id="52e4b-149">MatchSource</span></span>| <span data-ttu-id="52e4b-150">Pokud nastavena na výchozí hodnotu __$false__, pak všechny soubory ve zdroji (například soubory A, B a C) budou přidány do cílového umístění poprvé, tato konfigurace používá.</span><span class="sxs-lookup"><span data-stu-id="52e4b-150">If set to the default value of __$false__, then any files on the source (say, files A, B, and C) will be added to the destination the first time the configuration is applied.</span></span> <span data-ttu-id="52e4b-151">Pokud nový soubor (D) je přidán ke zdroji, nebude přidána do umístění, i když tato konfigurace používá znovu později.</span><span class="sxs-lookup"><span data-stu-id="52e4b-151">If a new file (D) is added to the source, it will not be added to the destination, even when the configuration is re-applied later.</span></span> <span data-ttu-id="52e4b-152">Pokud je hodnota __$true__, pak pokaždé, když tato konfigurace používá, do cíle jsou přidávány nové soubory, které jsou následně nalezena ve zdroji (například D soubor v tomto příkladu).</span><span class="sxs-lookup"><span data-stu-id="52e4b-152">If the value is __$true__, then each time the configuration is applied, new files subsequently found on the source (such as file D in this example) are added to the destination.</span></span> <span data-ttu-id="52e4b-153">Výchozí hodnota je **$false**.</span><span class="sxs-lookup"><span data-stu-id="52e4b-153">The default value is **$false**.</span></span>|

## <a name="example"></a><span data-ttu-id="52e4b-154">Příklad</span><span class="sxs-lookup"><span data-stu-id="52e4b-154">Example</span></span>

<span data-ttu-id="52e4b-155">Následující příklad ukazuje způsob použití souborů prostředků a zkontrolujte, že adresář s cestou `C:\Users\Public\Documents\DSCDemo\DemoSource` zdroje počítače (třeba server "o přijetí změn") je také k dispozici (spolu s všechny podadresáře) na cílovém uzlu.</span><span class="sxs-lookup"><span data-stu-id="52e4b-155">The following example shows how to use the File resource to ensure that a directory with the path `C:\Users\Public\Documents\DSCDemo\DemoSource` on a source computer (such as the “pull” server) is also present (along with all subdirectories) on the target node.</span></span> <span data-ttu-id="52e4b-156">Také zapíše potvrzovací zprávu do protokolu po dokončení a obsahuje prohlášení, ujistěte se, že operace kontroly souborů předchází operace protokolování.</span><span class="sxs-lookup"><span data-stu-id="52e4b-156">It also writes a confirmatory message to the log when complete and includes a statement to ensure that the file-checking operation runs prior to the logging operation.</span></span>

```powershell
Configuration FileResourceDemo
{
    Node "localhost"
    {
        File DirectoryCopy
        {
            Ensure = "Present"  # You can also set Ensure to "Absent"
            Type = "Directory" # Default is "File".
            Recurse = $true # Ensure presence of subdirectories, too
            SourcePath = "C:\Users\Public\Documents\DSCDemo\DemoSource"
            DestinationPath = "C:\Users\Public\Documents\DSCDemo\DemoDestination"
        }

        Log AfterDirectoryCopy
        {
            # The message below gets written to the Microsoft-Windows-Desired State Configuration/Analytic log
            Message = "Finished running the file resource with ID DirectoryCopy"
            DependsOn = "[File]DirectoryCopy" # This means run "DirectoryCopy" first.
        }
    }
}
```