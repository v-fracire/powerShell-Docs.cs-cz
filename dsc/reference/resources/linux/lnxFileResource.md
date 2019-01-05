---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: DSC pro Linux prostředek nxFile
ms.openlocfilehash: 80969ba2ea6247fcd616a301d951403a840c851d
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048210"
---
# <a name="dsc-for-linux-nxfile-resource"></a><span data-ttu-id="8a495-103">DSC pro Linux prostředek nxFile</span><span class="sxs-lookup"><span data-stu-id="8a495-103">DSC for Linux nxFile Resource</span></span>

<span data-ttu-id="8a495-104">**NxFile** prostředků v prostředí PowerShell Desired State Configuration (DSC) poskytuje mechanismus ke správě soubory a adresáře na uzlu systému Linux.</span><span class="sxs-lookup"><span data-stu-id="8a495-104">The **nxFile** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to manage files and directories on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="8a495-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="8a495-105">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="8a495-106">Properties</span><span class="sxs-lookup"><span data-stu-id="8a495-106">Properties</span></span>

|  <span data-ttu-id="8a495-107">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="8a495-107">Property</span></span> |  <span data-ttu-id="8a495-108">Popis</span><span class="sxs-lookup"><span data-stu-id="8a495-108">Description</span></span> |
|---|---|
| <span data-ttu-id="8a495-109">DestinationPath</span><span class="sxs-lookup"><span data-stu-id="8a495-109">DestinationPath</span></span>| <span data-ttu-id="8a495-110">Určuje umístění, kam chcete zajistit stavu pro soubor nebo adresář.</span><span class="sxs-lookup"><span data-stu-id="8a495-110">Specifies the location where you want to ensure the state for a file or directory.</span></span>|
| <span data-ttu-id="8a495-111">SourcePath</span><span class="sxs-lookup"><span data-stu-id="8a495-111">SourcePath</span></span>| <span data-ttu-id="8a495-112">Určuje cestu, ze kterého chcete kopírovat zdroje souboru nebo složky.</span><span class="sxs-lookup"><span data-stu-id="8a495-112">Specifies the path from which to copy the file or folder resource.</span></span> <span data-ttu-id="8a495-113">Tento způsob může být místní cesta nebo `http/https/ftp` adresy URL.</span><span class="sxs-lookup"><span data-stu-id="8a495-113">This path may be a local path, or an `http/https/ftp` URL.</span></span> <span data-ttu-id="8a495-114">Vzdálené `http/https/ftp` adresy URL jsou pouze podporovaná, až hodnotu **typ** vlastností je soubor.</span><span class="sxs-lookup"><span data-stu-id="8a495-114">Remote `http/https/ftp` URLs are only supported when the value of the **Type** property is file.</span></span>|
| <span data-ttu-id="8a495-115">Zkontrolujte</span><span class="sxs-lookup"><span data-stu-id="8a495-115">Ensure</span></span>| <span data-ttu-id="8a495-116">Určuje, jestli se má zkontrolovat, zda soubor existuje.</span><span class="sxs-lookup"><span data-stu-id="8a495-116">Determines whether to check if the file exists.</span></span> <span data-ttu-id="8a495-117">Nastavte tuto vlastnost na "Obsahuje" Ujistěte se, že soubor existuje.</span><span class="sxs-lookup"><span data-stu-id="8a495-117">Set this property to "Present" to ensure the file exists.</span></span> <span data-ttu-id="8a495-118">Nastavte ho na "Chybí" Ujistěte se, že soubor neexistuje.</span><span class="sxs-lookup"><span data-stu-id="8a495-118">Set it to "Absent" to ensure the file does not exist.</span></span> <span data-ttu-id="8a495-119">Výchozí hodnota je "K dispozici".</span><span class="sxs-lookup"><span data-stu-id="8a495-119">The default value is "Present".</span></span>|
| <span data-ttu-id="8a495-120">Type</span><span class="sxs-lookup"><span data-stu-id="8a495-120">Type</span></span>| <span data-ttu-id="8a495-121">Určuje, zda je adresář nebo soubor prostředků, která se právě nastavuje.</span><span class="sxs-lookup"><span data-stu-id="8a495-121">Specifies whether the resource being configured is a directory or a file.</span></span> <span data-ttu-id="8a495-122">Nastavte tuto vlastnost na "directory" k označení, že je prostředek adresáře.</span><span class="sxs-lookup"><span data-stu-id="8a495-122">Set this property to "directory" to indicate that the resource is a directory.</span></span> <span data-ttu-id="8a495-123">Nastavte na "file" označuje, že soubor prostředku.</span><span class="sxs-lookup"><span data-stu-id="8a495-123">Set it to "file" to indicate that the resource is a file.</span></span> <span data-ttu-id="8a495-124">Výchozí hodnota je "file"</span><span class="sxs-lookup"><span data-stu-id="8a495-124">The default value is "file"</span></span>|
| <span data-ttu-id="8a495-125">Obsah</span><span class="sxs-lookup"><span data-stu-id="8a495-125">Contents</span></span>| <span data-ttu-id="8a495-126">Určuje obsah souboru, jako je například konkrétní řetězec.</span><span class="sxs-lookup"><span data-stu-id="8a495-126">Specifies the contents of a file, such as a particular string.</span></span>|
| <span data-ttu-id="8a495-127">Kontrolní součet</span><span class="sxs-lookup"><span data-stu-id="8a495-127">Checksum</span></span>| <span data-ttu-id="8a495-128">Definuje typ, který má použít při určování, zda dva soubory jsou stejné.</span><span class="sxs-lookup"><span data-stu-id="8a495-128">Defines the type to use when determining whether two files are the same.</span></span> <span data-ttu-id="8a495-129">Pokud **kontrolního součtu** není zadán, pouze název souboru nebo složky se používá pro porovnání.</span><span class="sxs-lookup"><span data-stu-id="8a495-129">If **Checksum** is not specified, only the file or directory name is used for comparison.</span></span> <span data-ttu-id="8a495-130">Hodnoty jsou: "ctime", "mtime" nebo "md5".</span><span class="sxs-lookup"><span data-stu-id="8a495-130">Values are: "ctime", "mtime", or "md5".</span></span>|
| <span data-ttu-id="8a495-131">Recurse</span><span class="sxs-lookup"><span data-stu-id="8a495-131">Recurse</span></span>| <span data-ttu-id="8a495-132">Uvádí, jestli jsou zahrnuté podadresářů.</span><span class="sxs-lookup"><span data-stu-id="8a495-132">Indicates if subdirectories are included.</span></span> <span data-ttu-id="8a495-133">Tuto vlastnost nastavte na **$true** k označení, že chcete, aby podadresářů, které mají být zahrnuty.</span><span class="sxs-lookup"><span data-stu-id="8a495-133">Set this property to **$true** to indicate that you want subdirectories to be included.</span></span> <span data-ttu-id="8a495-134">Výchozí hodnota je **$false**.</span><span class="sxs-lookup"><span data-stu-id="8a495-134">The default is **$false**.</span></span> <span data-ttu-id="8a495-135">**Poznámka:** Tato vlastnost je platná pouze při **typ** je nastavena na adresář.</span><span class="sxs-lookup"><span data-stu-id="8a495-135">**Note:** This property is only valid when the **Type** property is set to directory.</span></span>|
| <span data-ttu-id="8a495-136">Force</span><span class="sxs-lookup"><span data-stu-id="8a495-136">Force</span></span>| <span data-ttu-id="8a495-137">Určité operace se soubory (například soubor přepsání nebo odstranění adresáře, který není prázdný) dojde chybě.</span><span class="sxs-lookup"><span data-stu-id="8a495-137">Certain file operations (such as overwriting a file or deleting a directory that is not empty) will result in an error.</span></span> <span data-ttu-id="8a495-138">Použití **platnost** vlastnost potlačuje tyto chyby.</span><span class="sxs-lookup"><span data-stu-id="8a495-138">Using the **Force** property overrides such errors.</span></span> <span data-ttu-id="8a495-139">Výchozí hodnota je **$false**.</span><span class="sxs-lookup"><span data-stu-id="8a495-139">The default value is **$false**.</span></span>|
| <span data-ttu-id="8a495-140">Odkazy</span><span class="sxs-lookup"><span data-stu-id="8a495-140">Links</span></span>| <span data-ttu-id="8a495-141">Určuje požadované chování pro symbolické odkazy.</span><span class="sxs-lookup"><span data-stu-id="8a495-141">Specifies the desired behavior for symbolic links.</span></span> <span data-ttu-id="8a495-142">Nastavte tuto vlastnost na "sledovat" sledovat symbolické odkazy a reagovat na cílové odkazy (např.</span><span class="sxs-lookup"><span data-stu-id="8a495-142">Set this property to "follow" to follow symbolic links and act on the links target (for example.</span></span> <span data-ttu-id="8a495-143">Zkopírujte soubor místo odkazu).</span><span class="sxs-lookup"><span data-stu-id="8a495-143">copy the file instead of the link).</span></span> <span data-ttu-id="8a495-144">Nastavte tuto vlastnost na "manage" tak, aby fungoval na odkaz (např.</span><span class="sxs-lookup"><span data-stu-id="8a495-144">Set this property to "manage" to act on the link (for example.</span></span> <span data-ttu-id="8a495-145">Zkopírujte odkaz pro samotné).</span><span class="sxs-lookup"><span data-stu-id="8a495-145">copy the link itself).</span></span> <span data-ttu-id="8a495-146">Nastavte tuto vlastnost na "Ignorovat" pro ignorování symbolické odkazy.</span><span class="sxs-lookup"><span data-stu-id="8a495-146">Set this property to "ignore" to ignore symbolic links.</span></span>|
| <span data-ttu-id="8a495-147">Skupina</span><span class="sxs-lookup"><span data-stu-id="8a495-147">Group</span></span>| <span data-ttu-id="8a495-148">Název **skupiny** vlastnictví souboru nebo adresáře.</span><span class="sxs-lookup"><span data-stu-id="8a495-148">The name of the **Group** to own the file or directory.</span></span>|
| <span data-ttu-id="8a495-149">Režim</span><span class="sxs-lookup"><span data-stu-id="8a495-149">Mode</span></span>| <span data-ttu-id="8a495-150">Určuje požadované oprávnění pro prostředek, v symbolické nebo osmičkové soustavě.</span><span class="sxs-lookup"><span data-stu-id="8a495-150">Specifies the desired permissions for the resource, in octal or symbolic notation.</span></span> <span data-ttu-id="8a495-151">(například 777 nebo rwxrwxrwx).</span><span class="sxs-lookup"><span data-stu-id="8a495-151">(for example, 777 or rwxrwxrwx).</span></span> <span data-ttu-id="8a495-152">Používáte-li symbolický zápisu, se neposkytuje prvního znaku, který označuje adresář nebo soubor.</span><span class="sxs-lookup"><span data-stu-id="8a495-152">If using symbolic notation, do not provide the first character which indicates directory or file.</span></span>|
| <span data-ttu-id="8a495-153">DependsOn</span><span class="sxs-lookup"><span data-stu-id="8a495-153">DependsOn</span></span> | <span data-ttu-id="8a495-154">Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="8a495-154">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="8a495-155">Například pokud **ID** prostředku bloku skriptu konfigurace, který chcete spustit nejdřív ale **ResourceName** a jejím typem je **ResourceType**, syntaxe pro použití této funkce Vlastnost je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="8a495-155">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

## <a name="additional-information"></a><span data-ttu-id="8a495-156">Další informace</span><span class="sxs-lookup"><span data-stu-id="8a495-156">Additional Information</span></span>


<span data-ttu-id="8a495-157">Operačních systémů Linux a Windows pomocí znaky konce řádku různých v textových souborech ve výchozím nastavení, a to může způsobit neočekávané výsledky při konfiguraci některé soubory na počítači s Linuxem pomocí __nxFile__.</span><span class="sxs-lookup"><span data-stu-id="8a495-157">Linux and Windows use different line break characters in text files by default, and this can cause unexpected results when configuring some files on a Linux computer with __nxFile__.</span></span> <span data-ttu-id="8a495-158">Správa obsahu Linuxový soubor při obcházení potíže způsobené službou znaky konců řádků neočekávané několika způsoby:</span><span class="sxs-lookup"><span data-stu-id="8a495-158">There are multiple ways to manage the content of a Linux file while avoiding issues caused by unexpected line break characters:</span></span>

<span data-ttu-id="8a495-159">Krok 1: Zkopírujte soubor ze vzdáleného zdroje (http, https nebo ftp): Vytvořte soubor v Linuxu se požadovaný obsah a jejich přípravy na web nebo ftp server přístupné uzly, které budete konfigurovat.</span><span class="sxs-lookup"><span data-stu-id="8a495-159">Step 1: Copy the file from a remote source (http, https, or ftp): create a file on Linux with the desired contents, and stage it on a web or ftp server accessible the node(s) you will configure.</span></span> <span data-ttu-id="8a495-160">Definovat __SourcePath__ vlastnost __nxFile__ prostředků s adresou URL webu nebo ftp do souboru.</span><span class="sxs-lookup"><span data-stu-id="8a495-160">Define the __SourcePath__ property in the __nxFile__ resource with the web or ftp URL to the file.</span></span>

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


<span data-ttu-id="8a495-161">Krok 2: Číst obsah souboru v skriptu prostředí PowerShell pomocí [Get-Content](https://technet.microsoft.com/library/hh849787.aspx) po nastavení __$OFS__ vlastnost pomocí znaku konce řádku Linux.</span><span class="sxs-lookup"><span data-stu-id="8a495-161">Step 2: Read the file contents in the PowerShell script with [Get-Content](https://technet.microsoft.com/library/hh849787.aspx) after setting the __$OFS__ property to use the Linux line-break character.</span></span>


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


<span data-ttu-id="8a495-162">Krok 3: Funkce prostředí PowerShell použijte k nahrazení Windows zalomení řádků s Linux znaky konce řádku.</span><span class="sxs-lookup"><span data-stu-id="8a495-162">Step 3: Use a PowerShell function to replace Windows line breaks with Linux line-break characters.</span></span>

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

## <a name="example"></a><span data-ttu-id="8a495-163">Příklad</span><span class="sxs-lookup"><span data-stu-id="8a495-163">Example</span></span>

<span data-ttu-id="8a495-164">Následující příklad zajistí, že adresář `/opt/mydir` existuje, a jestli existuje soubor se zadaným obsah tohoto adresáře.</span><span class="sxs-lookup"><span data-stu-id="8a495-164">The following example ensures that the directory `/opt/mydir` exists, and that a file with specified contents exists this directory.</span></span>

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