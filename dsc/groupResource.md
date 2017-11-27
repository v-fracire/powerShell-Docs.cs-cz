---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Prostředek DSC skupiny"
ms.openlocfilehash: 6fb6c5f9593687d7204ff31fddd9bca978ed2707
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="dsc-group-resource"></a><span data-ttu-id="86c37-103">Prostředek DSC skupiny</span><span class="sxs-lookup"><span data-stu-id="86c37-103">DSC Group Resource</span></span>

> <span data-ttu-id="86c37-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="86c37-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="86c37-105">Skupiny prostředků v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus ke správě místních skupin na cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="86c37-105">The Group resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage local groups on the target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="86c37-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="86c37-106">Syntax</span></span>
```
Group [string] #ResourceName
{
    GroupName          = [string]
    [ Credential       = [PSCredential] ]
    [ Description      = [string[]] ]
    [ Ensure           = [string] { Absent | Present }  ]
    [ Members          = [string[]] ]
    [ MembersToExclude = [string[]] ]
    [ MembersToInclude = [string[]] ]
    [ DependsOn        = [string[]] ]
}
```

## <a name="properties"></a><span data-ttu-id="86c37-107">Properties</span><span class="sxs-lookup"><span data-stu-id="86c37-107">Properties</span></span>

|  <span data-ttu-id="86c37-108">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="86c37-108">Property</span></span>  |  <span data-ttu-id="86c37-109">Popis</span><span class="sxs-lookup"><span data-stu-id="86c37-109">Description</span></span>   | 
|---|---| 
| <span data-ttu-id="86c37-110">Název skupiny</span><span class="sxs-lookup"><span data-stu-id="86c37-110">GroupName</span></span>| <span data-ttu-id="86c37-111">Název skupiny, pro které chcete zajistit určitý stav.</span><span class="sxs-lookup"><span data-stu-id="86c37-111">The name of the group for which you want to ensure a specific state.</span></span>| 
| <span data-ttu-id="86c37-112">přihlašovací údaje</span><span class="sxs-lookup"><span data-stu-id="86c37-112">Credential</span></span>| <span data-ttu-id="86c37-113">Přihlašovací údaje potřebné pro přístup k vzdálené prostředky.</span><span class="sxs-lookup"><span data-stu-id="86c37-113">The credentials required to access remote resources.</span></span> <span data-ttu-id="86c37-114">**Poznámka:**: Tento účet musí mít příslušná oprávnění služby Active Directory přidat všechny jiné než místní účty do skupiny; jinak, pokud dojde k chybě konfigurace se spustí na cílovém uzlu.</span><span class="sxs-lookup"><span data-stu-id="86c37-114">**Note**: This account must have the appropriate Active Directory permissions to add all non-local accounts to the group; otherwise, an error occurs when the configuration is executed on the target node.</span></span>  
| <span data-ttu-id="86c37-115">Popis</span><span class="sxs-lookup"><span data-stu-id="86c37-115">Description</span></span>| <span data-ttu-id="86c37-116">Popis skupiny.</span><span class="sxs-lookup"><span data-stu-id="86c37-116">The description of the group.</span></span>| 
| <span data-ttu-id="86c37-117">Ujistěte se</span><span class="sxs-lookup"><span data-stu-id="86c37-117">Ensure</span></span>| <span data-ttu-id="86c37-118">Označuje, pokud existuje daná skupina.</span><span class="sxs-lookup"><span data-stu-id="86c37-118">Indicates if the group exists.</span></span> <span data-ttu-id="86c37-119">Nastavením této vlastnosti "Chybí" zajistit, že skupina neexistuje.</span><span class="sxs-lookup"><span data-stu-id="86c37-119">Set this property to "Absent" to ensure that the group does not exist.</span></span> <span data-ttu-id="86c37-120">Nastavení jej do "K dispozici" (výchozí hodnota) zajišťuje, zda existuje daná skupina.</span><span class="sxs-lookup"><span data-stu-id="86c37-120">Setting it to "Present" (the default value) ensures that the group exists.</span></span>| 
| <span data-ttu-id="86c37-121">Členové</span><span class="sxs-lookup"><span data-stu-id="86c37-121">Members</span></span>| <span data-ttu-id="86c37-122">Pomocí této vlastnosti můžete nahradit členství v aktuální skupině zadaný členy.</span><span class="sxs-lookup"><span data-stu-id="86c37-122">Use this property to replace the current group membership with the specified members.</span></span> <span data-ttu-id="86c37-123">Hodnota této vlastnosti je pole řetězce ve formátu *domény*\\*uživatelské jméno*.</span><span class="sxs-lookup"><span data-stu-id="86c37-123">The value of this property is an array of strings of the form *Domain*\\*UserName*.</span></span> <span data-ttu-id="86c37-124">Pokud tuto vlastnost nastavit v konfiguraci, nepoužívejte buď **MembersToExclude** nebo **MembersToInclude** vlastnost.</span><span class="sxs-lookup"><span data-stu-id="86c37-124">If you set this property in a configuration, do not use either the **MembersToExclude** or **MembersToInclude** property.</span></span> <span data-ttu-id="86c37-125">Tím dojde k chybě.</span><span class="sxs-lookup"><span data-stu-id="86c37-125">Doing so generates an error.</span></span>| 
| <span data-ttu-id="86c37-126">MembersToExclude</span><span class="sxs-lookup"><span data-stu-id="86c37-126">MembersToExclude</span></span>| <span data-ttu-id="86c37-127">Pomocí této vlastnosti se odebrat členy ze stávajícího členství skupiny.</span><span class="sxs-lookup"><span data-stu-id="86c37-127">Use this property to remove members from the existing membership of the group.</span></span> <span data-ttu-id="86c37-128">Hodnota této vlastnosti je pole řetězce ve formátu *domény*\\*uživatelské jméno*.</span><span class="sxs-lookup"><span data-stu-id="86c37-128">The value of this property is an array of strings of the form *Domain*\\*UserName*.</span></span> <span data-ttu-id="86c37-129">Pokud tuto vlastnost nastavit v konfiguraci, nepoužívejte **členy** vlastnost.</span><span class="sxs-lookup"><span data-stu-id="86c37-129">If you set this property in a configuration, do not use the **Members** property.</span></span> <span data-ttu-id="86c37-130">Tím dojde k chybě.</span><span class="sxs-lookup"><span data-stu-id="86c37-130">Doing so generates an error.</span></span>| 
| <span data-ttu-id="86c37-131">MembersToInclude</span><span class="sxs-lookup"><span data-stu-id="86c37-131">MembersToInclude</span></span>| <span data-ttu-id="86c37-132">Postup přidání členů do stávajícího členství skupiny pomocí této vlastnosti.</span><span class="sxs-lookup"><span data-stu-id="86c37-132">Use this property to add members to the existing membership of the group.</span></span> <span data-ttu-id="86c37-133">Hodnota této vlastnosti je pole řetězce ve formátu *domény*\\*uživatelské jméno*.</span><span class="sxs-lookup"><span data-stu-id="86c37-133">The value of this property is an array of strings of the form *Domain*\\*UserName*.</span></span> <span data-ttu-id="86c37-134">Pokud tuto vlastnost nastavit v konfiguraci, nepoužívejte **členy** vlastnost.</span><span class="sxs-lookup"><span data-stu-id="86c37-134">If you set this property in a configuration, do not use the **Members** property.</span></span> <span data-ttu-id="86c37-135">Tím dojde k chybě.</span><span class="sxs-lookup"><span data-stu-id="86c37-135">Doing so will generate an error.</span></span>| 
| <span data-ttu-id="86c37-136">dependsOn</span><span class="sxs-lookup"><span data-stu-id="86c37-136">DependsOn</span></span> | <span data-ttu-id="86c37-137">Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="86c37-137">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="86c37-138">Pokud ID konfigurace prostředků skriptu blok, který chcete spustit nejprve je třeba __ResourceName__ a její typ je __ResourceType__, syntaxe pro používání této vlastnosti je ' DependsOn = "[Typ prostředku] ResourceName"".</span><span class="sxs-lookup"><span data-stu-id="86c37-138">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`\`.</span></span>| 

## <a name="example-1"></a><span data-ttu-id="86c37-139">Příklad 1</span><span class="sxs-lookup"><span data-stu-id="86c37-139">Example 1</span></span>

<span data-ttu-id="86c37-140">Následující příklad ukazuje, jak zajistit, že skupinu s názvem "TestGroup" chybí.</span><span class="sxs-lookup"><span data-stu-id="86c37-140">The following example shows how to ensure that a group called "TestGroup" is absent.</span></span> 

```powershell
Group GroupExample
{
    # This removes TestGroup, if present
    # To create a new group, set Ensure to "Present“
    Ensure = "Absent"
    GroupName = "TestGroup"
}
```
## <a name="example-2"></a><span data-ttu-id="86c37-141">Příklad 2</span><span class="sxs-lookup"><span data-stu-id="86c37-141">Example 2</span></span>
<span data-ttu-id="86c37-142">Následující příklad ukazuje, jak přidat uživatele služby Active Directory do místní skupiny administrators v rámci prostředí s více počítači sestavení, které už používáte přihlašovací údaje pro účet místního správce.</span><span class="sxs-lookup"><span data-stu-id="86c37-142">The following example shows how to add an Active Directory User to the local administrators group as part of a Multi-Machine Lab build where you are already using a PSCredential for the Local Adminstrator account.</span></span> <span data-ttu-id="86c37-143">Jako také používá se pro účet správce domény (po povýšení domény) potřebujeme pak převést tento existující přihlašovací údaje do domény popisný přihlašovací údaje uživatele domény přidat do místní skupiny Administrators na členském serveru, nám umožňují.</span><span class="sxs-lookup"><span data-stu-id="86c37-143">As this is also used for the Domain Admin Account (after Domain promotion) we then need to convert this existing PSCredential to a Domain Friendly credential to enable us to add a Domain User to the Local Administrators Group on the Member server.</span></span>

```powershell
@{
    AllNodes = @(
        @{
            NodeName = '*';
            DomainName = 'SubTest.contoso.com';
         }
     @{
            NodeName = 'Box2';
            AdminAccount = 'Admin-Dave_Alexanderson'   
      }    
    )
}
                  
$domain = $node.DomainName.split('.')[0]
$DCredential = New-Object -TypeName System.Management.Automation.PSCredential -ArgumentList ("$domain\$($credential.Username)", $Credential.Password)

Group AddADUserToLocalAdminGroup
        {
            GroupName='Administrators'   
            Ensure= 'Present'             
            MembersToInclude= "$domain\$($Node.AdminAccount)"
            Credential = $dCredential    
            PsDscRunAsCredential = $DCredential
        }
```

## <a name="example-3"></a><span data-ttu-id="86c37-144">Příklad 3</span><span class="sxs-lookup"><span data-stu-id="86c37-144">Example 3</span></span>
<span data-ttu-id="86c37-145">Následující příklad ukazuje, jak ověřit místní skupina, TigerTeamAdmins, na serveru TigerTeamSource.Contoso.Com neobsahuje účet konkrétní domény, Contoso\JerryG.</span><span class="sxs-lookup"><span data-stu-id="86c37-145">The following example shows how to ensure a local group, TigerTeamAdmins, on the server TigerTeamSource.Contoso.Com does not contain a particular domain account, Contoso\JerryG.</span></span>  

```powershell

Configuration SecureTigerTeamSrouce 
{
  Import-DscResource -ModuleName 'PSDesiredStateConfiguration'
  
  Node TigerTeamSource.Contoso.Com {
  Group TigerTeamAdmins
    {
       GroupName        = 'TigerTeamAdmins'   
       Ensure           = 'Absent'             
       MembersToInclude = "Contoso\JerryG"
    }
  }
}
```
