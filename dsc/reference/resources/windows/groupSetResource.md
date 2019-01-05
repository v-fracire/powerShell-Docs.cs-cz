---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
description: Poskytuje mechanismus ke správě místních skupin na cílový uzel.
title: Prostředek Groupset DSC
ms.openlocfilehash: afe4c4d33ac5620c411481e93d76a1f90c26deb9
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048158"
---
# <a name="dsc-groupset-resource"></a><span data-ttu-id="27d45-104">Prostředek Groupset DSC</span><span class="sxs-lookup"><span data-stu-id="27d45-104">DSC GroupSet Resource</span></span>

> <span data-ttu-id="27d45-105">Platí pro: Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="27d45-105">Applies To: Windows PowerShell 5.0</span></span>

<span data-ttu-id="27d45-106">**GroupSet** prostředků ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus ke správě místních skupin na cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="27d45-106">The **GroupSet** resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage local groups on the target node.</span></span> <span data-ttu-id="27d45-107">Tento prostředek je [složený prostředek](../../../resources/authoringResourceComposite.md) , která volá [skupině prostředků](groupResource.md) pro každou skupinu podle `GroupName` parametru.</span><span class="sxs-lookup"><span data-stu-id="27d45-107">This resource is a [composite resource](../../../resources/authoringResourceComposite.md) that calls the [Group resource](groupResource.md) for each group specified in the `GroupName` parameter.</span></span>

<span data-ttu-id="27d45-108">Použijte tento prostředek, pokud chcete přidat nebo odebrat stejný seznam členů do více než jedné skupiny, odebrání více než jedné skupině nebo přidat více než jednu skupinu pomocí stejného seznamu členů.</span><span class="sxs-lookup"><span data-stu-id="27d45-108">Use this resource when you want to add and/or remove the same list of members to more than one group, remove more than one group, or add more than one group with the same list of members.</span></span>

## <a name="syntax"></a><span data-ttu-id="27d45-109">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="27d45-109">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="27d45-110">Properties</span><span class="sxs-lookup"><span data-stu-id="27d45-110">Properties</span></span>

|  <span data-ttu-id="27d45-111">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="27d45-111">Property</span></span>  |  <span data-ttu-id="27d45-112">Popis</span><span class="sxs-lookup"><span data-stu-id="27d45-112">Description</span></span>   |
|---|---|
| <span data-ttu-id="27d45-113">Název skupiny</span><span class="sxs-lookup"><span data-stu-id="27d45-113">GroupName</span></span>| <span data-ttu-id="27d45-114">Názvy skupin, pro které chcete zajistit určitý stav.</span><span class="sxs-lookup"><span data-stu-id="27d45-114">The names of the groups for which you want to ensure a specific state.</span></span>|
| <span data-ttu-id="27d45-115">MembersToExclude</span><span class="sxs-lookup"><span data-stu-id="27d45-115">MembersToExclude</span></span>| <span data-ttu-id="27d45-116">Tuto vlastnost použijte k odebrání členů ze stávajícího členství skupin.</span><span class="sxs-lookup"><span data-stu-id="27d45-116">Use this property to remove members from the existing membership of the groups.</span></span> <span data-ttu-id="27d45-117">Hodnota této vlastnosti je pole řetězců formuláře *domény*\\*uživatelské jméno*.</span><span class="sxs-lookup"><span data-stu-id="27d45-117">The value of this property is an array of strings of the form *Domain*\\*UserName*.</span></span> <span data-ttu-id="27d45-118">Pokud byste tuto vlastnost nastavit v konfiguraci, nepoužívejte **členy** vlastnost.</span><span class="sxs-lookup"><span data-stu-id="27d45-118">If you set this property in a configuration, do not use the **Members** property.</span></span> <span data-ttu-id="27d45-119">Tím dojde k chybě.</span><span class="sxs-lookup"><span data-stu-id="27d45-119">Doing so will generate an error.</span></span>|
| <span data-ttu-id="27d45-120">Přihlašovací údaje</span><span class="sxs-lookup"><span data-stu-id="27d45-120">Credential</span></span>| <span data-ttu-id="27d45-121">Na pověření potřebná pro přístup ke vzdáleným prostředkům.</span><span class="sxs-lookup"><span data-stu-id="27d45-121">The credentials required to access remote resources.</span></span> <span data-ttu-id="27d45-122">**Poznámka:**: Tento účet musí mít příslušná oprávnění služby Active Directory přidat všechny jiné než místní účty do skupiny; v opačném případě dojde k chybě.</span><span class="sxs-lookup"><span data-stu-id="27d45-122">**Note**: This account must have the appropriate Active Directory permissions to add all non-local accounts to the group; otherwise, an error will occur.</span></span>
| <span data-ttu-id="27d45-123">Zkontrolujte</span><span class="sxs-lookup"><span data-stu-id="27d45-123">Ensure</span></span>| <span data-ttu-id="27d45-124">Udává, zda existuje skupiny.</span><span class="sxs-lookup"><span data-stu-id="27d45-124">Indicates whether the groups exist.</span></span> <span data-ttu-id="27d45-125">Nastavte tuto vlastnost na "Chybí" Ujistěte se, že skupiny neexistují.</span><span class="sxs-lookup"><span data-stu-id="27d45-125">Set this property to "Absent" to ensure that the groups do not exist.</span></span> <span data-ttu-id="27d45-126">Nastavení "Prezentovat" (výchozí hodnota) zajišťuje, že existují skupiny.</span><span class="sxs-lookup"><span data-stu-id="27d45-126">Setting it to "Present" (the default value) ensures that the groups exist.</span></span>|
| <span data-ttu-id="27d45-127">Členové</span><span class="sxs-lookup"><span data-stu-id="27d45-127">Members</span></span>| <span data-ttu-id="27d45-128">Tuto vlastnost použijte k nahrazení aktuální členství ve skupině se zadanými členy.</span><span class="sxs-lookup"><span data-stu-id="27d45-128">Use this property to replace the current group membership with the specified members.</span></span> <span data-ttu-id="27d45-129">Hodnota této vlastnosti je pole řetězců formuláře *domény*\\*uživatelské jméno*.</span><span class="sxs-lookup"><span data-stu-id="27d45-129">The value of this property is an array of strings of the form *Domain*\\*UserName*.</span></span> <span data-ttu-id="27d45-130">Pokud byste tuto vlastnost nastavit v konfiguraci, nepoužívejte buď **MembersToExclude** nebo **MembersToInclude** vlastnost.</span><span class="sxs-lookup"><span data-stu-id="27d45-130">If you set this property in a configuration, do not use either the **MembersToExclude** or **MembersToInclude** property.</span></span> <span data-ttu-id="27d45-131">Tím dojde k chybě.</span><span class="sxs-lookup"><span data-stu-id="27d45-131">Doing so will generate an error.</span></span>|
| <span data-ttu-id="27d45-132">MembersToInclude</span><span class="sxs-lookup"><span data-stu-id="27d45-132">MembersToInclude</span></span>| <span data-ttu-id="27d45-133">Tuto vlastnost použijte k přidání členů do existující členství ve skupině.</span><span class="sxs-lookup"><span data-stu-id="27d45-133">Use this property to add members to the existing membership of the group.</span></span> <span data-ttu-id="27d45-134">Hodnota této vlastnosti je pole řetězců formuláře *domény*\\*uživatelské jméno*.</span><span class="sxs-lookup"><span data-stu-id="27d45-134">The value of this property is an array of strings of the form *Domain*\\*UserName*.</span></span> <span data-ttu-id="27d45-135">Pokud byste tuto vlastnost nastavit v konfiguraci, nepoužívejte **členy** vlastnost.</span><span class="sxs-lookup"><span data-stu-id="27d45-135">If you set this property in a configuration, do not use the **Members** property.</span></span> <span data-ttu-id="27d45-136">Tím dojde k chybě.</span><span class="sxs-lookup"><span data-stu-id="27d45-136">Doing so will generate an error.</span></span>|
| <span data-ttu-id="27d45-137">DependsOn</span><span class="sxs-lookup"><span data-stu-id="27d45-137">DependsOn</span></span> | <span data-ttu-id="27d45-138">Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="27d45-138">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="27d45-139">Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba __ResourceName__ a jejím typem je __ResourceType__, syntaxe pro použití této vlastnosti je "DependsOn ="[ ResourceName ResourceType]"".</span><span class="sxs-lookup"><span data-stu-id="27d45-139">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is \`DependsOn = "[ResourceType]ResourceName"\`\`.</span></span>|

## <a name="example-1-ensuring-groups-are-present"></a><span data-ttu-id="27d45-140">Příklad 1: Zajistit, že skupiny jsou k dispozici</span><span class="sxs-lookup"><span data-stu-id="27d45-140">Example 1: Ensuring Groups are present</span></span>

<span data-ttu-id="27d45-141">Následující příklad ukazuje, jak zajistit, aby byly k dispozici dvě skupiny s názvem "myGroup" a "myOtherGroup".</span><span class="sxs-lookup"><span data-stu-id="27d45-141">The following example shows how to ensure that two groups called "myGroup" and "myOtherGroup" are present.</span></span>

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

> [!NOTE]
> <span data-ttu-id="27d45-142">Tento příklad používá pro jednoduchost přihlašovací údaje jako prostý text.</span><span class="sxs-lookup"><span data-stu-id="27d45-142">This example uses plaintext credentials for simplicity.</span></span> <span data-ttu-id="27d45-143">Informace o tom, jak šifrování přihlašovacích údajů v konfiguračním souboru MOF najdete v tématu [zabezpečení souboru MOF](../../../pull-server/secureMOF.md).</span><span class="sxs-lookup"><span data-stu-id="27d45-143">For information about how to encrypt credentials in the configuration MOF file, see [Securing the MOF File](../../../pull-server/secureMOF.md).</span></span>
