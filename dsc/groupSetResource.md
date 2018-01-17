---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
description: "Poskytuje mechanismus ke správě místních skupin na cílový uzel."
title: "GroupSet prostředek DSC"
ms.openlocfilehash: 158cb28747c5fe1987eb62b2cc0f6d6f6fb14332
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="dsc-groupset-resource"></a><span data-ttu-id="0b7ec-104">GroupSet prostředek DSC</span><span class="sxs-lookup"><span data-stu-id="0b7ec-104">DSC GroupSet Resource</span></span>

> <span data-ttu-id="0b7ec-105">Platí pro: Windows prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="0b7ec-105">Applies To: Windows Windows PowerShell 5.0</span></span>

<span data-ttu-id="0b7ec-106">**GroupSet** prostředek v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus ke správě místních skupin na cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="0b7ec-106">The **GroupSet** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage local groups on the target node.</span></span> <span data-ttu-id="0b7ec-107">Tento prostředek je [složené prostředků](authoringResourceComposite.md) , který volá [skupiny prostředků](groupResource.md) pro každou skupinu zadaný v `GroupName` parametr.</span><span class="sxs-lookup"><span data-stu-id="0b7ec-107">This resource is a [composite resource](authoringResourceComposite.md) that calls the [Group resource](groupResource.md) for each group specified in the `GroupName` parameter.</span></span>

<span data-ttu-id="0b7ec-108">Pokud chcete přidat nebo odebrat stejný seznam členů do více než jedné skupiny, odeberte více než jedné skupiny nebo přidat více než jednu skupinu s stejný seznam členů, použijte tento prostředek.</span><span class="sxs-lookup"><span data-stu-id="0b7ec-108">Use this resource when you want to add and/or remove the same list of members to more than one group, remove more than one group, or add more than one group with the same list of members.</span></span>

##<a name="syntax"></a><span data-ttu-id="0b7ec-109">Syntaxe ##</span><span class="sxs-lookup"><span data-stu-id="0b7ec-109">Syntax##</span></span>
```
Group [string] #ResourceName
{
    GroupName = [string[]]
    [ Ensure = [string] { Absent | Present }  ]
    [ MembersToInclude = [string[]] ]
    [ MembersToExclude = [string[]] ]
    [ Credential = [PSCredential] ]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a><span data-ttu-id="0b7ec-110">Properties</span><span class="sxs-lookup"><span data-stu-id="0b7ec-110">Properties</span></span>

|  <span data-ttu-id="0b7ec-111">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="0b7ec-111">Property</span></span>  |  <span data-ttu-id="0b7ec-112">Popis</span><span class="sxs-lookup"><span data-stu-id="0b7ec-112">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="0b7ec-113">Název skupiny</span><span class="sxs-lookup"><span data-stu-id="0b7ec-113">GroupName</span></span>| <span data-ttu-id="0b7ec-114">Názvy skupin, pro které chcete zajistit určitý stav.</span><span class="sxs-lookup"><span data-stu-id="0b7ec-114">The names of the groups for which you want to ensure a specific state.</span></span>| 
| <span data-ttu-id="0b7ec-115">MembersToExclude</span><span class="sxs-lookup"><span data-stu-id="0b7ec-115">MembersToExclude</span></span>| <span data-ttu-id="0b7ec-116">Pomocí této vlastnosti se odebrat členy ze stávajícího členství skupin.</span><span class="sxs-lookup"><span data-stu-id="0b7ec-116">Use this property to remove members from the existing membership of the groups.</span></span> <span data-ttu-id="0b7ec-117">Hodnota této vlastnosti je pole řetězce ve formátu *domény*\\*uživatelské jméno*.</span><span class="sxs-lookup"><span data-stu-id="0b7ec-117">The value of this property is an array of strings of the form *Domain*\\*UserName*.</span></span> <span data-ttu-id="0b7ec-118">Pokud tuto vlastnost nastavit v konfiguraci, nepoužívejte **členy** vlastnost.</span><span class="sxs-lookup"><span data-stu-id="0b7ec-118">If you set this property in a configuration, do not use the **Members** property.</span></span> <span data-ttu-id="0b7ec-119">Tím dojde k chybě.</span><span class="sxs-lookup"><span data-stu-id="0b7ec-119">Doing so will generate an error.</span></span>| 
| <span data-ttu-id="0b7ec-120">přihlašovací údaje</span><span class="sxs-lookup"><span data-stu-id="0b7ec-120">Credential</span></span>| <span data-ttu-id="0b7ec-121">Přihlašovací údaje potřebné pro přístup k vzdálené prostředky.</span><span class="sxs-lookup"><span data-stu-id="0b7ec-121">The credentials required to access remote resources.</span></span> <span data-ttu-id="0b7ec-122">**Poznámka:**: Tento účet musí mít příslušná oprávnění služby Active Directory přidat všechny jiné než místní účty do skupiny; jinak dojde k chybě.</span><span class="sxs-lookup"><span data-stu-id="0b7ec-122">**Note**: This account must have the appropriate Active Directory permissions to add all non-local accounts to the group; otherwise, an error will occur.</span></span>
| <span data-ttu-id="0b7ec-123">Ujistěte se</span><span class="sxs-lookup"><span data-stu-id="0b7ec-123">Ensure</span></span>| <span data-ttu-id="0b7ec-124">Určuje, zda existují skupiny.</span><span class="sxs-lookup"><span data-stu-id="0b7ec-124">Indicates whether the groups exist.</span></span> <span data-ttu-id="0b7ec-125">Nastavením této vlastnosti "Chybí" zajistit, že skupiny nejsou k dispozici.</span><span class="sxs-lookup"><span data-stu-id="0b7ec-125">Set this property to "Absent" to ensure that the groups do not exist.</span></span> <span data-ttu-id="0b7ec-126">Nastavení jej do "K dispozici" (výchozí hodnota) zajišťuje, že existují skupiny.</span><span class="sxs-lookup"><span data-stu-id="0b7ec-126">Setting it to "Present" (the default value) ensures that the groups exist.</span></span>| 
| <span data-ttu-id="0b7ec-127">Členové</span><span class="sxs-lookup"><span data-stu-id="0b7ec-127">Members</span></span>| <span data-ttu-id="0b7ec-128">Pomocí této vlastnosti můžete nahradit členství v aktuální skupině zadaný členy.</span><span class="sxs-lookup"><span data-stu-id="0b7ec-128">Use this property to replace the current group membership with the specified members.</span></span> <span data-ttu-id="0b7ec-129">Hodnota této vlastnosti je pole řetězce ve formátu *domény*\\*uživatelské jméno*.</span><span class="sxs-lookup"><span data-stu-id="0b7ec-129">The value of this property is an array of strings of the form *Domain*\\*UserName*.</span></span> <span data-ttu-id="0b7ec-130">Pokud tuto vlastnost nastavit v konfiguraci, nepoužívejte buď **MembersToExclude** nebo **MembersToInclude** vlastnost.</span><span class="sxs-lookup"><span data-stu-id="0b7ec-130">If you set this property in a configuration, do not use either the **MembersToExclude** or **MembersToInclude** property.</span></span> <span data-ttu-id="0b7ec-131">Tím dojde k chybě.</span><span class="sxs-lookup"><span data-stu-id="0b7ec-131">Doing so will generate an error.</span></span>| 
| <span data-ttu-id="0b7ec-132">MembersToInclude</span><span class="sxs-lookup"><span data-stu-id="0b7ec-132">MembersToInclude</span></span>| <span data-ttu-id="0b7ec-133">Postup přidání členů do stávajícího členství skupiny pomocí této vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="0b7ec-133">Use this property to add members to the existing membership of the group.</span></span> <span data-ttu-id="0b7ec-134">Hodnota této vlastnosti je pole řetězce ve formátu *domény*\\*uživatelské jméno*.</span><span class="sxs-lookup"><span data-stu-id="0b7ec-134">The value of this property is an array of strings of the form *Domain*\\*UserName*.</span></span> <span data-ttu-id="0b7ec-135">Pokud tuto vlastnost nastavit v konfiguraci, nepoužívejte **členy** vlastnost.</span><span class="sxs-lookup"><span data-stu-id="0b7ec-135">If you set this property in a configuration, do not use the **Members** property.</span></span> <span data-ttu-id="0b7ec-136">Tím dojde k chybě.</span><span class="sxs-lookup"><span data-stu-id="0b7ec-136">Doing so will generate an error.</span></span>| 
| <span data-ttu-id="0b7ec-137">dependsOn</span><span class="sxs-lookup"><span data-stu-id="0b7ec-137">DependsOn</span></span> | <span data-ttu-id="0b7ec-138">Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="0b7ec-138">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="0b7ec-139">Pokud ID konfigurace prostředků skriptu blok, který chcete spustit nejprve je třeba __ResourceName__ a její typ je __ResourceType__, syntaxe pro používání této vlastnosti je ' DependsOn = "[Typ prostředku] ResourceName"".</span><span class="sxs-lookup"><span data-stu-id="0b7ec-139">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is \`DependsOn = "[ResourceType]ResourceName"\`\`.</span></span>| 

## <a name="example-1"></a><span data-ttu-id="0b7ec-140">Příklad 1</span><span class="sxs-lookup"><span data-stu-id="0b7ec-140">Example 1</span></span>

<span data-ttu-id="0b7ec-141">Následující příklad ukazuje, jak zajistit, že jsou k dispozici dvě skupiny s názvem "myGroup" a "myOtherGroup".</span><span class="sxs-lookup"><span data-stu-id="0b7ec-141">The following example shows how to ensure that two groups called "myGroup" and "myOtherGroup" are present.</span></span> 

```powershell
configuration GroupSetTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Node localhost
    {
        GroupSet GroupSetTest
        {
            GroupName        = @("myGroup", "myOtherGroup")
            Ensure           = "Present"
            MembersToInclude = @("contoso\alice", "contoso\bob")
            MembersToExclude = $("contoso\john")
            Credential       = Get-Credential
        }
    }
}
$cd = @{
    AllNodes = @(
        @{
            NodeName                    = 'localhost'
            PSDscAllowPlainTextPassword = $true
            PSDscAllowDomainUser        = $true
        }
    )
}


GroupSetTest -ConfigurationData $cd
```

><span data-ttu-id="0b7ec-142">**Poznámka:** tento příklad používá pro jednoduchost přihlašovací údaje ve formátu prostého textu.</span><span class="sxs-lookup"><span data-stu-id="0b7ec-142">**Note:** This example uses plaintext credentials for simplicity.</span></span> <span data-ttu-id="0b7ec-143">Informace o tom, jak šifrování přihlašovacích údajů v konfiguračním souboru MOF najdete v tématu [zabezpečení souboru MOF](secureMOF.md).</span><span class="sxs-lookup"><span data-stu-id="0b7ec-143">For information about how to encrypt credentials in the configuration MOF file, see [Securing the MOF File](secureMOF.md).</span></span>


