---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Prostředek DSC souboru
ms.openlocfilehash: 7964eabe5f4585600ae80f3e5ff7439c0d954769
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="dsc-file-resource"></a><span data-ttu-id="ef68f-103">Prostředek DSC souboru</span><span class="sxs-lookup"><span data-stu-id="ef68f-103">DSC File Resource</span></span>

> <span data-ttu-id="ef68f-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="ef68f-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="ef68f-105">Prostředek souboru v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus ke správě souborů a složek na cílovém uzlu.</span><span class="sxs-lookup"><span data-stu-id="ef68f-105">The File resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage files and folders on the target node.</span></span>

><span data-ttu-id="ef68f-106">**Poznámka:** Pokud **MatchSource** je nastavena na **$false** (což je výchozí hodnota), obsah, který se má zkopírovat jsou uložené v mezipaměti při prvním se konfigurace použije.</span><span class="sxs-lookup"><span data-stu-id="ef68f-106">**Note:** If the **MatchSource** property is set to **$false** (which is the default value), the contents to be copied are cached the first time the configuration is applied.</span></span>
><span data-ttu-id="ef68f-107">Konfigurace dalších aplikací nebudou kontrolovat aktualizované soubory nebo složky v cestě určeného **SourcePath**.</span><span class="sxs-lookup"><span data-stu-id="ef68f-107">Subsequent applications of the configuration will not check for updated files and/or folders in the path specified by **SourcePath**.</span></span> <span data-ttu-id="ef68f-108">Pokud chcete vyhledat aktualizace na soubory nebo složky v **SourcePath** pokaždé, když se konfigurace použije, nastavte **MatchSource** k **$true**.</span><span class="sxs-lookup"><span data-stu-id="ef68f-108">If you want to check for updates to the files and/or folders in **SourcePath** every time the configuration is applied, set **MatchSource** to **$true**.</span></span>

## <a name="syntax"></a><span data-ttu-id="ef68f-109">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="ef68f-109">Syntax</span></span>
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

## <a name="properties"></a><span data-ttu-id="ef68f-110">Properties</span><span class="sxs-lookup"><span data-stu-id="ef68f-110">Properties</span></span>

|  <span data-ttu-id="ef68f-111">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="ef68f-111">Property</span></span>  |  <span data-ttu-id="ef68f-112">Popis</span><span class="sxs-lookup"><span data-stu-id="ef68f-112">Description</span></span>   |
|---|---|
| <span data-ttu-id="ef68f-113">DestinationPath</span><span class="sxs-lookup"><span data-stu-id="ef68f-113">DestinationPath</span></span>| <span data-ttu-id="ef68f-114">Určuje umístění, kde chcete zajistit stav pro soubor nebo adresář.</span><span class="sxs-lookup"><span data-stu-id="ef68f-114">Indicates the location where you want to ensure the state for a file or directory.</span></span>|
| <span data-ttu-id="ef68f-115">Atributy</span><span class="sxs-lookup"><span data-stu-id="ef68f-115">Attributes</span></span>| <span data-ttu-id="ef68f-116">Určuje požadovaný stav atributy pro cílový soubor nebo adresář.</span><span class="sxs-lookup"><span data-stu-id="ef68f-116">Specifies the desired state of the attributes for the targeted file or directory.</span></span>|
| <span data-ttu-id="ef68f-117">Kontrolní součet</span><span class="sxs-lookup"><span data-stu-id="ef68f-117">Checksum</span></span>| <span data-ttu-id="ef68f-118">Označuje typ kontrolního součtu použít při určování, zda dva soubory jsou stejné.</span><span class="sxs-lookup"><span data-stu-id="ef68f-118">Indicates the checksum type to use when determining whether two files are the same.</span></span> <span data-ttu-id="ef68f-119">Pokud __kontrolního součtu__ není zadán, pro porovnání se používá pouze název souboru nebo adresáře.</span><span class="sxs-lookup"><span data-stu-id="ef68f-119">If __Checksum__ is not specified, only the file or directory name is used for comparison.</span></span> <span data-ttu-id="ef68f-120">Platné hodnoty patří: SHA-1, SHA-256, SHA-512, datum vytvoření, modifiedDate.</span><span class="sxs-lookup"><span data-stu-id="ef68f-120">Valid values include: SHA-1, SHA-256, SHA-512, createdDate, modifiedDate.</span></span>|
| <span data-ttu-id="ef68f-121">Obsah</span><span class="sxs-lookup"><span data-stu-id="ef68f-121">Contents</span></span>| <span data-ttu-id="ef68f-122">Určuje obsah souboru, například konkrétní řetězec.</span><span class="sxs-lookup"><span data-stu-id="ef68f-122">Specifies the contents of a file, such as a particular string.</span></span>|
| <span data-ttu-id="ef68f-123">přihlašovací údaje</span><span class="sxs-lookup"><span data-stu-id="ef68f-123">Credential</span></span>| <span data-ttu-id="ef68f-124">Označuje přihlašovací údaje, které jsou požadovány pro přístup k prostředkům, jako je například zdrojové soubory, pokud je nutný takový přístup.</span><span class="sxs-lookup"><span data-stu-id="ef68f-124">Indicates the credentials that are required to access resources, such as source files, if such access is required.</span></span>|
| <span data-ttu-id="ef68f-125">Ujistěte se</span><span class="sxs-lookup"><span data-stu-id="ef68f-125">Ensure</span></span>| <span data-ttu-id="ef68f-126">Určuje, jestli existuje soubor nebo adresář.</span><span class="sxs-lookup"><span data-stu-id="ef68f-126">Indicates if the file or directory exists.</span></span> <span data-ttu-id="ef68f-127">Nastavením této vlastnosti "Chybí" zajistit, že soubor nebo adresář neexistuje.</span><span class="sxs-lookup"><span data-stu-id="ef68f-127">Set this property to "Absent" to ensure that the file or directory does not exist.</span></span> <span data-ttu-id="ef68f-128">Nastavte ji na "Přítomen" zajistit, že soubor nebo adresář neexistuje.</span><span class="sxs-lookup"><span data-stu-id="ef68f-128">Set it to "Present" to ensure that the file or directory does exist.</span></span> <span data-ttu-id="ef68f-129">Výchozí hodnota je "Dispozici".</span><span class="sxs-lookup"><span data-stu-id="ef68f-129">The default is "Present".</span></span>|
| <span data-ttu-id="ef68f-130">Force</span><span class="sxs-lookup"><span data-stu-id="ef68f-130">Force</span></span>| <span data-ttu-id="ef68f-131">Některé operace souboru (například přepsání souboru nebo odstranění adresáře, který není prázdný) bude výsledkem chyba.</span><span class="sxs-lookup"><span data-stu-id="ef68f-131">Certain file operations (such as overwriting a file or deleting a directory that is not empty) will result in an error.</span></span> <span data-ttu-id="ef68f-132">Pomocí vlastnosti Vynucené přepsání takové chyby.</span><span class="sxs-lookup"><span data-stu-id="ef68f-132">Using the Force property overrides such errors.</span></span> <span data-ttu-id="ef68f-133">Výchozí hodnota je __$false__.</span><span class="sxs-lookup"><span data-stu-id="ef68f-133">The default value is __$false__.</span></span>|
| <span data-ttu-id="ef68f-134">Recurse</span><span class="sxs-lookup"><span data-stu-id="ef68f-134">Recurse</span></span>| <span data-ttu-id="ef68f-135">Uvádí, jestli jsou zahrnuté podadresářů.</span><span class="sxs-lookup"><span data-stu-id="ef68f-135">Indicates if subdirectories are included.</span></span> <span data-ttu-id="ef68f-136">Tuto vlastnost nastavit na __$true__ k označení, že chcete podadresáře, které mají být zahrnuty.</span><span class="sxs-lookup"><span data-stu-id="ef68f-136">Set this property to __$true__ to indicate that you want subdirectories to be included.</span></span> <span data-ttu-id="ef68f-137">Výchozí hodnota je __$false__.</span><span class="sxs-lookup"><span data-stu-id="ef68f-137">The default is __$false__.</span></span> <span data-ttu-id="ef68f-138">**Poznámka:**: Tato vlastnost je platná pouze pokud je vlastnost Typ nastavena na adresář.</span><span class="sxs-lookup"><span data-stu-id="ef68f-138">**Note**: This property is only valid when the Type property is set to Directory.</span></span>|
| <span data-ttu-id="ef68f-139">dependsOn</span><span class="sxs-lookup"><span data-stu-id="ef68f-139">DependsOn</span></span> | <span data-ttu-id="ef68f-140">Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="ef68f-140">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="ef68f-141">Pokud ID konfigurace prostředků skriptu blok, který chcete spustit nejprve je třeba __ResourceName__ a její typ je __ResourceType__, syntaxe pro používání této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="ef68f-141">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|
| <span data-ttu-id="ef68f-142">SourcePath</span><span class="sxs-lookup"><span data-stu-id="ef68f-142">SourcePath</span></span>| <span data-ttu-id="ef68f-143">Určuje cestu, ze které kopírování prostředků souboru nebo složky.</span><span class="sxs-lookup"><span data-stu-id="ef68f-143">Indicates the path from which to copy the file or folder resource.</span></span>|
| <span data-ttu-id="ef68f-144">Typ</span><span class="sxs-lookup"><span data-stu-id="ef68f-144">Type</span></span>| <span data-ttu-id="ef68f-145">Určuje, zda je prostředek konfigurován adresář nebo soubor.</span><span class="sxs-lookup"><span data-stu-id="ef68f-145">Indicates if the resource being configured is a directory or a file.</span></span> <span data-ttu-id="ef68f-146">Nastavením této vlastnosti "Adresář" označuje, že prostředek adresáře.</span><span class="sxs-lookup"><span data-stu-id="ef68f-146">Set this property to "Directory" to indicate that the resource is a directory.</span></span> <span data-ttu-id="ef68f-147">Nastavte ji na File (soubor) znamenat, že prostředek soubor.</span><span class="sxs-lookup"><span data-stu-id="ef68f-147">Set it to "File" to indicate that the resource is a file.</span></span> <span data-ttu-id="ef68f-148">Výchozí hodnota je "Soubor".</span><span class="sxs-lookup"><span data-stu-id="ef68f-148">The default value is “File”.</span></span>|
| <span data-ttu-id="ef68f-149">MatchSource</span><span class="sxs-lookup"><span data-stu-id="ef68f-149">MatchSource</span></span>| <span data-ttu-id="ef68f-150">Pokud se nastaví na výchozí hodnotu z __$false__, pak všechny soubory ve zdroji (například, soubory A, B a C) budou přidány do cílového umístění poprvé se konfigurace použije.</span><span class="sxs-lookup"><span data-stu-id="ef68f-150">If set to the default value of __$false__, then any files on the source (say, files A, B, and C) will be added to the destination the first time the configuration is applied.</span></span> <span data-ttu-id="ef68f-151">Pokud nový soubor (D) je přidán ke zdroji, nebude přidáno do cílového umístění, i v případě, že konfigurace se použije znovu později.</span><span class="sxs-lookup"><span data-stu-id="ef68f-151">If a new file (D) is added to the source, it will not be added to the destination, even when the configuration is re-applied later.</span></span> <span data-ttu-id="ef68f-152">Pokud je hodnota __$true__, potom pokaždé, když se konfigurace použije, do cílového umístění jsou přidávány nové soubory, které následně nalezena ve zdroji (například soubor D v tomto příkladu).</span><span class="sxs-lookup"><span data-stu-id="ef68f-152">If the value is __$true__, then each time the configuration is applied, new files subsequently found on the source (such as file D in this example) are added to the destination.</span></span> <span data-ttu-id="ef68f-153">Výchozí hodnota je **$false**.</span><span class="sxs-lookup"><span data-stu-id="ef68f-153">The default value is **$false**.</span></span>|

## <a name="example"></a><span data-ttu-id="ef68f-154">Příklad</span><span class="sxs-lookup"><span data-stu-id="ef68f-154">Example</span></span>

<span data-ttu-id="ef68f-155">Následující příklad ukazuje, jak použít soubor prostředků zajistit, aby adresáře s cestou `C:\Users\Public\Documents\DSCDemo\DemoSource` ve zdroji (například server "vyžádání") počítače nachází také (spolu s všechny podadresáře) na cílovém uzlu.</span><span class="sxs-lookup"><span data-stu-id="ef68f-155">The following example shows how to use the File resource to ensure that a directory with the path `C:\Users\Public\Documents\DSCDemo\DemoSource` on a source computer (such as the “pull” server) is also present (along with all subdirectories) on the target node.</span></span> <span data-ttu-id="ef68f-156">Také potvrzující zpráva, zapíše do protokolu, po dokončení a obsahuje příkaz k zajištění, že operaci kontrola soubor spouští před operaci protokolování.</span><span class="sxs-lookup"><span data-stu-id="ef68f-156">It also writes a confirmatory message to the log when complete and includes a statement to ensure that the file-checking operation runs prior to the logging operation.</span></span>

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