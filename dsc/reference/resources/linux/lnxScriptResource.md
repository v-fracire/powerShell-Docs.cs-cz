---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: DSC pro Linux nxScript prostředků
ms.openlocfilehash: 339968512ab1c16c4c3785a3a19b00c3fbbf9ea1
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048127"
---
# <a name="dsc-for-linux-nxscript-resource"></a><span data-ttu-id="20b35-103">DSC pro Linux nxScript prostředků</span><span class="sxs-lookup"><span data-stu-id="20b35-103">DSC for Linux nxScript Resource</span></span>

<span data-ttu-id="20b35-104">**NxScript** prostředků v prostředí PowerShell Desired State Configuration (DSC) poskytuje mechanismus pro spouštění skriptů Linux v systému Linux uzlu.</span><span class="sxs-lookup"><span data-stu-id="20b35-104">The **nxScript** resource in PowerShell Desired State Configuration (DSC) provides a mechanism to run Linux scripts on a Linux node.</span></span>

## <a name="syntax"></a><span data-ttu-id="20b35-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="20b35-105">Syntax</span></span>

```
nxScript <string> #ResourceName
{
    GetScript = <string>
    SetScript = <string>
    TestScript = <string>
    [ User = <string> ]
    [ Group = <string> ]
    [ DependsOn = <string[]> ]

}
```

## <a name="properties"></a><span data-ttu-id="20b35-106">Properties</span><span class="sxs-lookup"><span data-stu-id="20b35-106">Properties</span></span>

|  <span data-ttu-id="20b35-107">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="20b35-107">Property</span></span> |  <span data-ttu-id="20b35-108">Popis</span><span class="sxs-lookup"><span data-stu-id="20b35-108">Description</span></span> |
|---|---|
| <span data-ttu-id="20b35-109">GetScript</span><span class="sxs-lookup"><span data-stu-id="20b35-109">GetScript</span></span>| <span data-ttu-id="20b35-110">Poskytuje skript, který se spustí při vyvolání [Get-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521625.aspx) rutiny.</span><span class="sxs-lookup"><span data-stu-id="20b35-110">Provides a script that runs when you invoke the [Get-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521625.aspx) cmdlet.</span></span> <span data-ttu-id="20b35-111">Skript musí začínat shebang, jako je například #! / bin/bash.</span><span class="sxs-lookup"><span data-stu-id="20b35-111">The script must begin with a shebang, such as #!/bin/bash.</span></span>|
| <span data-ttu-id="20b35-112">SetScript</span><span class="sxs-lookup"><span data-stu-id="20b35-112">SetScript</span></span>| <span data-ttu-id="20b35-113">Obsahuje skript.</span><span class="sxs-lookup"><span data-stu-id="20b35-113">Provides a script.</span></span> <span data-ttu-id="20b35-114">Při vyvolání [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) rutiny **TestScript** spustí první.</span><span class="sxs-lookup"><span data-stu-id="20b35-114">When you invoke the [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) cmdlet, the **TestScript** runs first.</span></span> <span data-ttu-id="20b35-115">Pokud **TestScript** bloku vrátí výstupní kód než 0, **SetScript** blok se spustí.</span><span class="sxs-lookup"><span data-stu-id="20b35-115">If the **TestScript** block returns an exit code other than 0, the **SetScript** block will run.</span></span> <span data-ttu-id="20b35-116">Pokud **TestScript** vrátí ukončovací kód 0, **SetScript** se nespustí.</span><span class="sxs-lookup"><span data-stu-id="20b35-116">If the **TestScript** returns an exit code of 0, the **SetScript** will not run.</span></span> <span data-ttu-id="20b35-117">Skript musí začínat shebang, jako například `#!/bin/bash`.</span><span class="sxs-lookup"><span data-stu-id="20b35-117">The script must begin with a shebang, such as `#!/bin/bash`.</span></span>|
| <span data-ttu-id="20b35-118">TestScript</span><span class="sxs-lookup"><span data-stu-id="20b35-118">TestScript</span></span>| <span data-ttu-id="20b35-119">Obsahuje skript.</span><span class="sxs-lookup"><span data-stu-id="20b35-119">Provides a script.</span></span> <span data-ttu-id="20b35-120">Při vyvolání [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) , tento skript spustí.</span><span class="sxs-lookup"><span data-stu-id="20b35-120">When you invoke the [Start-DscConfiguration](https://technet.microsoft.com/en-us/library/dn521623.aspx) cmdlet, this script runs.</span></span> <span data-ttu-id="20b35-121">Pokud se vrátí výstupní kód než 0, se spustí SetScript.</span><span class="sxs-lookup"><span data-stu-id="20b35-121">If it returns an exit code other than 0, the SetScript will run.</span></span> <span data-ttu-id="20b35-122">Vrátí ukončovací kód 0,-li **SetScript** se nespustí.</span><span class="sxs-lookup"><span data-stu-id="20b35-122">If it returns an exit code of 0, the **SetScript** will not run.</span></span> <span data-ttu-id="20b35-123">**TestScript** poběží i v případě vyvolání [Test-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) rutiny.</span><span class="sxs-lookup"><span data-stu-id="20b35-123">The **TestScript** also runs when you invoke the [Test-DscConfiguration](https://technet.microsoft.com/en-us/library/dn407382.aspx) cmdlet.</span></span> <span data-ttu-id="20b35-124">V takovém případě však **SetScript** se nespustí, bez ohledu na to, jaké ukončovací kód je vrácen z **TestScript**.</span><span class="sxs-lookup"><span data-stu-id="20b35-124">However, in this case, the **SetScript** will not run, no matter what exit code is returned from the **TestScript**.</span></span> <span data-ttu-id="20b35-125">**TestScript** musí vrátit ukončovací kód 0, pokud skutečnou konfiguraci odpovídá aktuální konfigurace požadovaného stavu a východ kódu jiné než 0, pokud neodpovídá.</span><span class="sxs-lookup"><span data-stu-id="20b35-125">The **TestScript** must return an exit code of 0 if the actual configuration matches the current desired state configuration, and an exit code other than 0 if it does not match.</span></span> <span data-ttu-id="20b35-126">(Aktuální konfigurace požadovaného stavu je poslední konfigurace plnění na uzlu, který používá DSC).</span><span class="sxs-lookup"><span data-stu-id="20b35-126">(The current desired state configuration is the last configuration enacted on the node that is using DSC).</span></span> <span data-ttu-id="20b35-127">Skript musí začínat shebang, jako je například 1#!/bin/bash.1</span><span class="sxs-lookup"><span data-stu-id="20b35-127">The script must begin with a shebang, such as 1#!/bin/bash.1</span></span>|
| <span data-ttu-id="20b35-128">Uživatel</span><span class="sxs-lookup"><span data-stu-id="20b35-128">User</span></span>| <span data-ttu-id="20b35-129">Uživatel ke spuštění skriptu jako.</span><span class="sxs-lookup"><span data-stu-id="20b35-129">The user to run the script as.</span></span>|
| <span data-ttu-id="20b35-130">Skupina</span><span class="sxs-lookup"><span data-stu-id="20b35-130">Group</span></span>| <span data-ttu-id="20b35-131">Skupina pro spuštění skriptu jako.</span><span class="sxs-lookup"><span data-stu-id="20b35-131">The group to run the script as.</span></span>|
| <span data-ttu-id="20b35-132">DependsOn</span><span class="sxs-lookup"><span data-stu-id="20b35-132">DependsOn</span></span> | <span data-ttu-id="20b35-133">Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="20b35-133">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="20b35-134">Například pokud **ID** prostředku bloku skriptu konfigurace, který chcete spustit nejdřív ale **ResourceName** a jejím typem je **ResourceType**, syntaxe pro použití této funkce Vlastnost je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="20b35-134">For example, if the **ID** of the resource configuration script block that you want to run first is **ResourceName** and its type is **ResourceType**, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

## <a name="example"></a><span data-ttu-id="20b35-135">Příklad</span><span class="sxs-lookup"><span data-stu-id="20b35-135">Example</span></span>

<span data-ttu-id="20b35-136">Následující příklad ukazuje použití **nxScript** prostředků k provedení další správa konfigurace.</span><span class="sxs-lookup"><span data-stu-id="20b35-136">The following example demonstrates the use of the **nxScript** resource to perform additional configuration management.</span></span>

```
Import-DSCResource -Module nx

Node $node {
nxScript KeepDirEmpty{

    GetScript = @"
#!/bin/bash
ls /tmp/mydir/ | wc -l
"@

    SetScript = @"
#!/bin/bash
rm -rf /tmp/mydir/*
"@

    TestScript = @'
#!/bin/bash
filecount=`ls /tmp/mydir | wc -l`
if [ $filecount -gt 0 ]
then
    exit 1
else
    exit 0
fi
'@
}
}
```