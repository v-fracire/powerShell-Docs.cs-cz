---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "DSC pro Linux nxFile prostředků"
ms.openlocfilehash: 14f1ae31a8409b8874d76a91b8b29595e30fbb46
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-for-linux-nxfile-resource"></a><span data-ttu-id="07bc1-103">DSC pro Linux nxFile prostředků</span><span class="sxs-lookup"><span data-stu-id="07bc1-103">DSC for Linux nxFile Resource</span></span>

<span data-ttu-id="07bc1-104">**NxFile** prostředků v prostředí PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus pro ke správě souborů a adresářů v uzlu systému Linux.</span><span class="sxs-lookup"><span data-stu-id="07bc1-104">The **nxFile** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to to manage files and directories on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="07bc1-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="07bc1-105">Syntax</span></span>

```
nxFile <string> #ResourceName
{
    DestinationPath = <string>
    [ SourcePath = <string> ]
    [ Ensure = <string> { Absent | Present }  ]
    [ Type = <string> { directory | file | link } ]
    [ Contents = <string> ]
    [ Checksum = <string> { ctime | mtime | md5 }  ]
    [ Recurse = <bool> ]
    [ Force = <bool> ]
    [ Links = <string> { follow | manage } ]
    [ Group = <string> ]
    [ Mode = <string> ]
    [ Owner = <string> ]
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a><span data-ttu-id="07bc1-106">Properties</span><span class="sxs-lookup"><span data-stu-id="07bc1-106">Properties</span></span>

|  <span data-ttu-id="07bc1-107">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="07bc1-107">Property</span></span> |  <span data-ttu-id="07bc1-108">Popis</span><span class="sxs-lookup"><span data-stu-id="07bc1-108">Description</span></span> | 
|---|---|
| <span data-ttu-id="07bc1-109">Cílová_cesta</span><span class="sxs-lookup"><span data-stu-id="07bc1-109">DestinationPath</span></span>| <span data-ttu-id="07bc1-110">Určuje umístění, kde chcete zajistit stav pro soubor nebo adresář.</span><span class="sxs-lookup"><span data-stu-id="07bc1-110">Specifies the location where you want to ensure the state for a file or directory.</span></span>| 
| <span data-ttu-id="07bc1-111">Zdrojová cesta</span><span class="sxs-lookup"><span data-stu-id="07bc1-111">SourcePath</span></span>| <span data-ttu-id="07bc1-112">Určuje cestu, ze kterého chcete kopírovat prostředek souboru nebo složky.</span><span class="sxs-lookup"><span data-stu-id="07bc1-112">Specifies the path from which to copy the file or folder resource.</span></span> <span data-ttu-id="07bc1-113">Tato cesta může být místní cesta nebo `http/https/ftp` adresy URL.</span><span class="sxs-lookup"><span data-stu-id="07bc1-113">This path may be a local path, or an `http/https/ftp` URL.</span></span> <span data-ttu-id="07bc1-114">Vzdálené `http/https/ftp` adresy URL jsou pouze podporovaná, až hodnotu **typ** vlastnost je soubor.</span><span class="sxs-lookup"><span data-stu-id="07bc1-114">Remote `http/https/ftp` URLs are only supported when the value of the **Type** property is file.</span></span>| 
| <span data-ttu-id="07bc1-115">Ujistěte se</span><span class="sxs-lookup"><span data-stu-id="07bc1-115">Ensure</span></span>| <span data-ttu-id="07bc1-116">Určuje, jestli se má zkontrolovat, zda soubor existuje.</span><span class="sxs-lookup"><span data-stu-id="07bc1-116">Determines whether to check if the file exists.</span></span> <span data-ttu-id="07bc1-117">Nastavte tuto vlastnost k dispozici"" zajistit, že soubor existuje.</span><span class="sxs-lookup"><span data-stu-id="07bc1-117">Set this property to "Present" to ensure the file exists.</span></span> <span data-ttu-id="07bc1-118">Nastavte ji na "Chybí" zajistěte, aby byl že soubor neexistuje.</span><span class="sxs-lookup"><span data-stu-id="07bc1-118">Set it to "Absent" to ensure the file does not exist.</span></span> <span data-ttu-id="07bc1-119">Výchozí hodnota je "Dispozici".</span><span class="sxs-lookup"><span data-stu-id="07bc1-119">The default value is "Present".</span></span>| 
| <span data-ttu-id="07bc1-120">Typ</span><span class="sxs-lookup"><span data-stu-id="07bc1-120">Type</span></span>| <span data-ttu-id="07bc1-121">Určuje, zda je nakonfigurován prostředek adresář nebo soubor.</span><span class="sxs-lookup"><span data-stu-id="07bc1-121">Specifies whether the resource being configured is a directory or a file.</span></span> <span data-ttu-id="07bc1-122">Nastavením této vlastnosti "adresář" označuje, že prostředek adresáře.</span><span class="sxs-lookup"><span data-stu-id="07bc1-122">Set this property to "directory" to indicate that the resource is a directory.</span></span> <span data-ttu-id="07bc1-123">Nastavte tak, aby "soubor" k označení, že je prostředek soubor.</span><span class="sxs-lookup"><span data-stu-id="07bc1-123">Set it to "file" to indicate that the resource is a file.</span></span> <span data-ttu-id="07bc1-124">Výchozí hodnota je "soubor"</span><span class="sxs-lookup"><span data-stu-id="07bc1-124">The default value is "file"</span></span>| 
| <span data-ttu-id="07bc1-125">Obsah</span><span class="sxs-lookup"><span data-stu-id="07bc1-125">Contents</span></span>| <span data-ttu-id="07bc1-126">Určuje obsah souboru, například konkrétní řetězec.</span><span class="sxs-lookup"><span data-stu-id="07bc1-126">Specifies the contents of a file, such as a particular string.</span></span>| 
| <span data-ttu-id="07bc1-127">Kontrolní součet</span><span class="sxs-lookup"><span data-stu-id="07bc1-127">Checksum</span></span>| <span data-ttu-id="07bc1-128">Definuje typ, který má použít při určování, zda dva soubory jsou stejné.</span><span class="sxs-lookup"><span data-stu-id="07bc1-128">Defines the type to use when determining whether two files are the same.</span></span> <span data-ttu-id="07bc1-129">Pokud **kontrolního součtu** není zadán, pro porovnání se používá pouze název souboru nebo adresáře.</span><span class="sxs-lookup"><span data-stu-id="07bc1-129">If **Checksum** is not specified, only the file or directory name is used for comparison.</span></span> <span data-ttu-id="07bc1-130">Hodnoty: "ctime", "mtime" nebo "md5".</span><span class="sxs-lookup"><span data-stu-id="07bc1-130">Values are: "ctime", "mtime", or "md5".</span></span>| 
| <span data-ttu-id="07bc1-131">Recurse</span><span class="sxs-lookup"><span data-stu-id="07bc1-131">Recurse</span></span>| <span data-ttu-id="07bc1-132">Uvádí, jestli jsou zahrnuté podadresářů.</span><span class="sxs-lookup"><span data-stu-id="07bc1-132">Indicates if subdirectories are included.</span></span> <span data-ttu-id="07bc1-133">Tuto vlastnost nastavit na **$true** k označení, že chcete podadresáře, které mají být zahrnuty.</span><span class="sxs-lookup"><span data-stu-id="07bc1-133">Set this property to **$true** to indicate that you want subdirectories to be included.</span></span> <span data-ttu-id="07bc1-134">Výchozí hodnota je **$false**.</span><span class="sxs-lookup"><span data-stu-id="07bc1-134">The default is **$false**.</span></span> <span data-ttu-id="07bc1-135">**Poznámka:** tato vlastnost je platná pouze když **typu** je nastavena na adresář.</span><span class="sxs-lookup"><span data-stu-id="07bc1-135">**Note:** This property is only valid when the **Type** property is set to directory.</span></span>| 
| <span data-ttu-id="07bc1-136">Force</span><span class="sxs-lookup"><span data-stu-id="07bc1-136">Force</span></span>| <span data-ttu-id="07bc1-137">Některé operace souboru (například přepsání souboru nebo odstranění adresáře, který není prázdný) bude výsledkem chyba.</span><span class="sxs-lookup"><span data-stu-id="07bc1-137">Certain file operations (such as overwriting a file or deleting a directory that is not empty) will result in an error.</span></span> <span data-ttu-id="07bc1-138">Pomocí **Force** vlastnost má přednost před takové chyby.</span><span class="sxs-lookup"><span data-stu-id="07bc1-138">Using the **Force** property overrides such errors.</span></span> <span data-ttu-id="07bc1-139">Výchozí hodnota je **$false**.</span><span class="sxs-lookup"><span data-stu-id="07bc1-139">The default value is **$false**.</span></span>| 
| <span data-ttu-id="07bc1-140">Odkazy</span><span class="sxs-lookup"><span data-stu-id="07bc1-140">Links</span></span>| <span data-ttu-id="07bc1-141">Určuje požadované chování pro symbolické odkazy.</span><span class="sxs-lookup"><span data-stu-id="07bc1-141">Specifies the desired behavior for symbolic links.</span></span> <span data-ttu-id="07bc1-142">Nastavením této vlastnosti "následovat" a postupujte podle symbolické odkazy fungují na cíli odkazy (např.</span><span class="sxs-lookup"><span data-stu-id="07bc1-142">Set this property to "follow" to follow symbolic links and act on the links target (for example.</span></span> <span data-ttu-id="07bc1-143">Zkopírujte soubor místo odkazu).</span><span class="sxs-lookup"><span data-stu-id="07bc1-143">copy the file instead of the link).</span></span> <span data-ttu-id="07bc1-144">Nastavením této vlastnosti "manage" tak, aby fungoval na odkaz (například)</span><span class="sxs-lookup"><span data-stu-id="07bc1-144">Set this property to "manage" to act on the link (for example.</span></span> <span data-ttu-id="07bc1-145">Zkopírujte odkaz sám sebe).</span><span class="sxs-lookup"><span data-stu-id="07bc1-145">copy the link itself).</span></span> <span data-ttu-id="07bc1-146">Nastavte tuto vlastnost "Ignorovat" Ignorovat symbolické odkazy.</span><span class="sxs-lookup"><span data-stu-id="07bc1-146">Set this property to "ignore" to ignore symbolic links.</span></span>| 
| <span data-ttu-id="07bc1-147">Skupina</span><span class="sxs-lookup"><span data-stu-id="07bc1-147">Group</span></span>| <span data-ttu-id="07bc1-148">Název **skupiny** udělil soubor nebo adresář.</span><span class="sxs-lookup"><span data-stu-id="07bc1-148">The name of the **Group** to own the file or directory.</span></span>| 
| <span data-ttu-id="07bc1-149">Režim</span><span class="sxs-lookup"><span data-stu-id="07bc1-149">Mode</span></span>| <span data-ttu-id="07bc1-150">Určuje požadované oprávnění pro prostředek, notaci osmičková nebo symbolické.</span><span class="sxs-lookup"><span data-stu-id="07bc1-150">Specifies the desired permissions for the resource, in octal or symbolic notation.</span></span> <span data-ttu-id="07bc1-151">(například 777 nebo rwxrwxrwx).</span><span class="sxs-lookup"><span data-stu-id="07bc1-151">(for example, 777 or rwxrwxrwx).</span></span> <span data-ttu-id="07bc1-152">Pokud používáte symbolický zápis, neposkytují prvního znaku, který označuje adresář nebo soubor.</span><span class="sxs-lookup"><span data-stu-id="07bc1-152">If using symbolic notation, do not provide the first character which indicates directory or file.</span></span>| 
| <span data-ttu-id="07bc1-153">dependsOn</span><span class="sxs-lookup"><span data-stu-id="07bc1-153">DependsOn</span></span> | <span data-ttu-id="07bc1-154">Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="07bc1-154">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="07bc1-155">Například pokud **ID** prostředku blok skriptu konfigurace, který chcete spustit nejprve je **ResourceName** a její typ je **ResourceType**, pomocí této syntaxe Vlastnost je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="07bc1-155">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>| 

## <a name="additional-information"></a><span data-ttu-id="07bc1-156">Další informace</span><span class="sxs-lookup"><span data-stu-id="07bc1-156">Additional Information</span></span>


<span data-ttu-id="07bc1-157">Linux a Windows pomocí znaky konce řádku různých v textových souborů ve výchozím nastavení, a to může vést k neočekávaným výsledkům při konfiguraci některé soubory na počítač se systémem Linux s __nxFile__.</span><span class="sxs-lookup"><span data-stu-id="07bc1-157">Linux and Windows use different line break characters in text files by default, and this can cause unexpected results when configuring some files on a Linux computer with __nxFile__.</span></span> <span data-ttu-id="07bc1-158">Spravovat obsah souboru Linux při vyloučení problémů způsobených znaky konce řádku neočekávané několika způsoby:</span><span class="sxs-lookup"><span data-stu-id="07bc1-158">There are multiple ways to manage the content of a Linux file while avoiding issues caused by unexpected line break characters:</span></span>

<span data-ttu-id="07bc1-159">Krok 1: Kopírování souboru ze vzdáleného zdroje (http, https nebo ftp): Vytvořte soubor v systému Linux s požadovaný obsah a příprava na web nebo ftp serveru přístupné uzly budete konfigurovat.</span><span class="sxs-lookup"><span data-stu-id="07bc1-159">Step 1: Copy the file from a remote source (http, https, or ftp): create a file on Linux with the desired contents, and stage it on a web or ftp server accessible the node(s) you will configure.</span></span> <span data-ttu-id="07bc1-160">Definování __SourcePath__ vlastnost __nxFile__ prostředek s web nebo ftp adresu URL k souboru.</span><span class="sxs-lookup"><span data-stu-id="07bc1-160">Define the __SourcePath__ property in the __nxFile__ resource with the web or ftp URL to the file.</span></span>

```
Import-DSCResource -Module nx
Node $Node
{
nxFile resolvConf
{
    SourcePath = "http://10.185.85.11/conf/resolv.conf"
    DestinationPath = "/etc/resolv.conf"
    Mode = "644"        
    Type = "file"
    
}
        
}
```


<span data-ttu-id="07bc1-161">Krok 2: Přečtěte si obsah souboru ve skriptu prostředí PowerShell s [Get-Content](https://technet.microsoft.com/en-us/library/hh849787.aspx) po nastavení __$OFS__ vlastnost použít znak Linux konec řádku.</span><span class="sxs-lookup"><span data-stu-id="07bc1-161">Step 2: Read the file contents in the PowerShell script with [Get-Content](https://technet.microsoft.com/en-us/library/hh849787.aspx) after setting the __$OFS__ property to use the Linux line-break character.</span></span>


```
Import-DSCResource -Module nx
Node $Node
{
$OFS = "`n"
$Contents = Get-Content C:\temp\resolv.conf

nxFile resolvConf
{
    DestinationPath = "/etc/resolv.conf"
    Mode = "644"        
    Type = "file"
    Contents = "$Contents"
}

}
```


<span data-ttu-id="07bc1-162">Krok 3: Použití funkce prostředí PowerShell nahradit konce řádků Windows znaky konce řádku Linux.</span><span class="sxs-lookup"><span data-stu-id="07bc1-162">Step 3: Use a PowerShell function to replace Windows line breaks with Linux line-break characters.</span></span>

```
Function LinuxString($inputStr){
    $outputStr = $inputStr.Replace("`r`n","`n")
    $ouputStr += "`n"
    Return $outputStr
}

Import-DSCResource -Module nx
Node $Node
{

$Contents = @'
search contoso.com
domain contoso.com
nameserver 10.185.85.11
'@

$Contents = LinuxString $Contents

nxFile resolvConf
{
    DestinationPath = "/etc/resolv.conf"
    Mode = "644"        
    Type = "file"
    Contents = $Contents
    
}
}
```

## <a name="example"></a><span data-ttu-id="07bc1-163">Příklad</span><span class="sxs-lookup"><span data-stu-id="07bc1-163">Example</span></span>

<span data-ttu-id="07bc1-164">Následující příklad zajišťuje, že adresář `/opt/mydir` existuje, a zda existuje soubor s zadaný obsah tohoto adresáře.</span><span class="sxs-lookup"><span data-stu-id="07bc1-164">The following example ensures that the directory `/opt/mydir` exists, and that a file with specified contents exists this directory.</span></span>

```
Import-DSCResource -Module nx 

Node $node {
nxFile DirectoryExample
{
   Ensure = "Present"
   DestinationPath = "/opt/mydir"
   Type = "Directory"
}

nxFile FileExample
{
    Ensure = "Present"
    Destinationpath = "/opt/mydir/myfile"
    Contents=@"
#!/bin/bash`necho "hello world"`n
"@ 
    Mode = “755”
    DependsOn = "[nxFile]DirectoryExample"
} 
}
```

