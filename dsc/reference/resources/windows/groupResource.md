---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Prostředek DSC skupiny
ms.openlocfilehash: 9894150f6f749fc23efd4ce2b155b18788557d1d
ms.sourcegitcommit: e04292a9c10de9a8391d529b7f7aa3753b362dbe
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/04/2019
ms.locfileid: "54048123"
---
# <a name="dsc-group-resource"></a><span data-ttu-id="2c1ae-103">Prostředek DSC skupiny</span><span class="sxs-lookup"><span data-stu-id="2c1ae-103">DSC Group Resource</span></span>

> <span data-ttu-id="2c1ae-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="2c1ae-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>

<span data-ttu-id="2c1ae-105">Skupiny prostředků ve Windows Powershellu Desired State Configuration (DSC) poskytuje mechanismus ke správě místních skupin na cílový uzel.</span><span class="sxs-lookup"><span data-stu-id="2c1ae-105">The Group resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage local groups on the target node.</span></span>

## <a name="syntax"></a><span data-ttu-id="2c1ae-106">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="2c1ae-106">Syntax</span></span>

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

## <a name="properties"></a><span data-ttu-id="2c1ae-107">Properties</span><span class="sxs-lookup"><span data-stu-id="2c1ae-107">Properties</span></span>

|  <span data-ttu-id="2c1ae-108">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="2c1ae-108">Property</span></span>  |  <span data-ttu-id="2c1ae-109">Popis</span><span class="sxs-lookup"><span data-stu-id="2c1ae-109">Description</span></span>   |
|---|---|
| <span data-ttu-id="2c1ae-110">Název skupiny</span><span class="sxs-lookup"><span data-stu-id="2c1ae-110">GroupName</span></span>| <span data-ttu-id="2c1ae-111">Název skupiny, pro které chcete zajistit určitý stav.</span><span class="sxs-lookup"><span data-stu-id="2c1ae-111">The name of the group for which you want to ensure a specific state.</span></span>|
| <span data-ttu-id="2c1ae-112">Přihlašovací údaje</span><span class="sxs-lookup"><span data-stu-id="2c1ae-112">Credential</span></span>| <span data-ttu-id="2c1ae-113">Na pověření potřebná pro přístup ke vzdáleným prostředkům.</span><span class="sxs-lookup"><span data-stu-id="2c1ae-113">The credentials required to access remote resources.</span></span> <span data-ttu-id="2c1ae-114">**Poznámka:**: Tento účet musí mít příslušná oprávnění služby Active Directory přidat všechny jiné než místní účty do skupiny; v opačném případě dojde k chybě při konfiguraci spuštění na cílovém uzlu.</span><span class="sxs-lookup"><span data-stu-id="2c1ae-114">**Note**: This account must have the appropriate Active Directory permissions to add all non-local accounts to the group; otherwise, an error occurs when the configuration is executed on the target node.</span></span>
| <span data-ttu-id="2c1ae-115">Popis</span><span class="sxs-lookup"><span data-stu-id="2c1ae-115">Description</span></span>| <span data-ttu-id="2c1ae-116">Popis skupiny.</span><span class="sxs-lookup"><span data-stu-id="2c1ae-116">The description of the group.</span></span>|
| <span data-ttu-id="2c1ae-117">Zkontrolujte</span><span class="sxs-lookup"><span data-stu-id="2c1ae-117">Ensure</span></span>| <span data-ttu-id="2c1ae-118">Určuje, zda skupina existuje.</span><span class="sxs-lookup"><span data-stu-id="2c1ae-118">Indicates if the group exists.</span></span> <span data-ttu-id="2c1ae-119">Nastavte tuto vlastnost na "Chybí" Ujistěte se, že skupina neexistuje.</span><span class="sxs-lookup"><span data-stu-id="2c1ae-119">Set this property to "Absent" to ensure that the group does not exist.</span></span> <span data-ttu-id="2c1ae-120">Nastavení "Prezentovat" (výchozí hodnota) zajišťuje, že tato skupina existuje.</span><span class="sxs-lookup"><span data-stu-id="2c1ae-120">Setting it to "Present" (the default value) ensures that the group exists.</span></span>|
| <span data-ttu-id="2c1ae-121">Členové</span><span class="sxs-lookup"><span data-stu-id="2c1ae-121">Members</span></span>| <span data-ttu-id="2c1ae-122">Tuto vlastnost použijte k nahrazení aktuální členství ve skupině se zadanými členy.</span><span class="sxs-lookup"><span data-stu-id="2c1ae-122">Use this property to replace the current group membership with the specified members.</span></span> <span data-ttu-id="2c1ae-123">Hodnota této vlastnosti je pole řetězců formuláře *domény*\\*uživatelské jméno*.</span><span class="sxs-lookup"><span data-stu-id="2c1ae-123">The value of this property is an array of strings of the form *Domain*\\*UserName*.</span></span> <span data-ttu-id="2c1ae-124">Pokud byste tuto vlastnost nastavit v konfiguraci, nepoužívejte buď **MembersToExclude** nebo **MembersToInclude** vlastnost.</span><span class="sxs-lookup"><span data-stu-id="2c1ae-124">If you set this property in a configuration, do not use either the **MembersToExclude** or **MembersToInclude** property.</span></span> <span data-ttu-id="2c1ae-125">Tím dojde k chybě.</span><span class="sxs-lookup"><span data-stu-id="2c1ae-125">Doing so generates an error.</span></span>|
| <span data-ttu-id="2c1ae-126">MembersToExclude</span><span class="sxs-lookup"><span data-stu-id="2c1ae-126">MembersToExclude</span></span>| <span data-ttu-id="2c1ae-127">Tuto vlastnost použijte k odebrání členů z existující členství ve skupině.</span><span class="sxs-lookup"><span data-stu-id="2c1ae-127">Use this property to remove members from the existing membership of the group.</span></span> <span data-ttu-id="2c1ae-128">Hodnota této vlastnosti je pole řetězců formuláře *domény*\\*uživatelské jméno*.</span><span class="sxs-lookup"><span data-stu-id="2c1ae-128">The value of this property is an array of strings of the form *Domain*\\*UserName*.</span></span> <span data-ttu-id="2c1ae-129">Pokud byste tuto vlastnost nastavit v konfiguraci, nepoužívejte **členy** vlastnost.</span><span class="sxs-lookup"><span data-stu-id="2c1ae-129">If you set this property in a configuration, do not use the **Members** property.</span></span> <span data-ttu-id="2c1ae-130">Tím dojde k chybě.</span><span class="sxs-lookup"><span data-stu-id="2c1ae-130">Doing so generates an error.</span></span>|
| <span data-ttu-id="2c1ae-131">MembersToInclude</span><span class="sxs-lookup"><span data-stu-id="2c1ae-131">MembersToInclude</span></span>| <span data-ttu-id="2c1ae-132">Tuto vlastnost použijte k přidání členů do existující členství ve skupině.</span><span class="sxs-lookup"><span data-stu-id="2c1ae-132">Use this property to add members to the existing membership of the group.</span></span> <span data-ttu-id="2c1ae-133">Hodnota této vlastnosti je pole řetězců formuláře *domény*\\*uživatelské jméno*.</span><span class="sxs-lookup"><span data-stu-id="2c1ae-133">The value of this property is an array of strings of the form *Domain*\\*UserName*.</span></span> <span data-ttu-id="2c1ae-134">Pokud byste tuto vlastnost nastavit v konfiguraci, nepoužívejte **členy** vlastnost.</span><span class="sxs-lookup"><span data-stu-id="2c1ae-134">If you set this property in a configuration, do not use the **Members** property.</span></span> <span data-ttu-id="2c1ae-135">Tím dojde k chybě.</span><span class="sxs-lookup"><span data-stu-id="2c1ae-135">Doing so will generate an error.</span></span>|
| <span data-ttu-id="2c1ae-136">DependsOn</span><span class="sxs-lookup"><span data-stu-id="2c1ae-136">DependsOn</span></span> | <span data-ttu-id="2c1ae-137">Udává, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="2c1ae-137">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="2c1ae-138">Pokud blok, který chcete spustit skript ID prostředku konfigurace nejprve je třeba __ResourceName__ a jejím typem je __ResourceType__, syntaxe pro použití této vlastnosti je "DependsOn ="[ ResourceName ResourceType]"".</span><span class="sxs-lookup"><span data-stu-id="2c1ae-138">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is \`DependsOn = "[ResourceType]ResourceName"\`\`.</span></span>|

## <a name="example-1"></a><span data-ttu-id="2c1ae-139">Příklad 1</span><span class="sxs-lookup"><span data-stu-id="2c1ae-139">Example 1</span></span>

<span data-ttu-id="2c1ae-140">Následující příklad ukazuje, jak zajistit, že skupinu s názvem "TestGroup" chybí.</span><span class="sxs-lookup"><span data-stu-id="2c1ae-140">The following example shows how to ensure that a group called "TestGroup" is absent.</span></span>

```powershell
Group GroupExample
{
    # This removes TestGroup, if present
    # To create a new group, set Ensure to "Present“
    Ensure = "Absent"
    GroupName = "TestGroup"
}
```

## <a name="example-2"></a><span data-ttu-id="2c1ae-141">Příklad 2</span><span class="sxs-lookup"><span data-stu-id="2c1ae-141">Example 2</span></span>

<span data-ttu-id="2c1ae-142">Následující příklad ukazuje, jak přidat uživatele služby Active Directory do místní skupiny administrators v rámci testovacího prostředí s více počítači sestavení, pokud už používáte objekt PSCredential pro účet místního správce.</span><span class="sxs-lookup"><span data-stu-id="2c1ae-142">The following example shows how to add an Active Directory User to the local administrators group as part of a Multi-Machine Lab build where you are already using a PSCredential for the Local Adminstrator account.</span></span>
<span data-ttu-id="2c1ae-143">Jak to se také používá pro účet správce domény (po povýšení domény), následně je potřeba převést tento existující PSCredential doméně popisným přihlašovací údaje.</span><span class="sxs-lookup"><span data-stu-id="2c1ae-143">As this is also used for the Domain Admin Account (after Domain promotion), we then need to convert this existing PSCredential to a Domain Friendly credential.</span></span>
<span data-ttu-id="2c1ae-144">Pak můžeme přidat uživatele domény do místní skupiny Administrators na členský server.</span><span class="sxs-lookup"><span data-stu-id="2c1ae-144">Then we can add a Domain User to the Local Administrators Group on the Member server.</span></span>

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

Group AddADUserToLocalAdminGroup {
    GroupName='Administrators'
    Ensure= 'Present'
    MembersToInclude= "$domain\$($Node.AdminAccount)"
    Credential = $dCredential
    PsDscRunAsCredential = $DCredential
}
```

## <a name="example-3"></a><span data-ttu-id="2c1ae-145">Příklad 3</span><span class="sxs-lookup"><span data-stu-id="2c1ae-145">Example 3</span></span>

<span data-ttu-id="2c1ae-146">Následující příklad ukazuje, jak zajistit místní skupina, TigerTeamAdmins, na serveru TigerTeamSource.Contoso.Com neobsahuje konkrétní doménový účet, Contoso\JerryG.</span><span class="sxs-lookup"><span data-stu-id="2c1ae-146">The following example shows how to ensure a local group, TigerTeamAdmins, on the server TigerTeamSource.Contoso.Com does not contain a particular domain account, Contoso\JerryG.</span></span>

```powershell
Configuration SecureTigerTeamSrouce {
  Import-DscResource -ModuleName 'PSDesiredStateConfiguration'

  Node TigerTeamSource.Contoso.Com {
    Group TigerTeamAdmins {
       GroupName        = 'TigerTeamAdmins'
       Ensure           = 'Present'
       MembersToExclude = "Contoso\JerryG"
    }
  }
}
```