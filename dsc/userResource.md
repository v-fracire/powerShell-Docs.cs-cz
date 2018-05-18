---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Prostředek DSC uživatele
ms.openlocfilehash: f2660933aec43967e3f4082a983ef328a5b93851
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
---
#<a name="dsc-user-resource"></a><span data-ttu-id="a41d5-103">Prostředek DSC uživatele #</span><span class="sxs-lookup"><span data-stu-id="a41d5-103">DSC User Resource#</span></span>


><span data-ttu-id="a41d5-104">Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0</span><span class="sxs-lookup"><span data-stu-id="a41d5-104">Applies To: Windows PowerShell 4.0, Windows PowerShell 5.0</span></span>


<span data-ttu-id="a41d5-105">__Uživatele__ prostředek v systému Windows PowerShell požadovaného stavu konfigurace (DSC) poskytuje mechanismus ke správě místní uživatelské účty na cílovém uzlu.</span><span class="sxs-lookup"><span data-stu-id="a41d5-105">The __User__ resource in Windows PowerShell Desired State Configuration (DSC) provides a mechanism to manage local user accounts on the target node.</span></span>


##<a name="syntax"></a><span data-ttu-id="a41d5-106">Syntaxe ##</span><span class="sxs-lookup"><span data-stu-id="a41d5-106">Syntax##</span></span>

```
User [string] #ResourceName
{
    UserName = [string]
    [ Description = [string] ]
    [ Disabled = [bool] ]
    [ Ensure = [string] { Absent | Present }  ]
    [ FullName = [string] ]
    [ Password = [PSCredential] ]
    [ PasswordChangeNotAllowed = [bool] ]
    [ PasswordChangeRequired = [bool] ]
    [ PasswordNeverExpires = [bool] ]
    [ DependsOn = [string[]] ]
}
```

## <a name="properties"></a><span data-ttu-id="a41d5-107">Properties</span><span class="sxs-lookup"><span data-stu-id="a41d5-107">Properties</span></span>
|  <span data-ttu-id="a41d5-108">Vlastnost</span><span class="sxs-lookup"><span data-stu-id="a41d5-108">Property</span></span>  |  <span data-ttu-id="a41d5-109">Popis</span><span class="sxs-lookup"><span data-stu-id="a41d5-109">Description</span></span>   |
|---|---|
| <span data-ttu-id="a41d5-110">UserName</span><span class="sxs-lookup"><span data-stu-id="a41d5-110">UserName</span></span>| <span data-ttu-id="a41d5-111">Určuje název účtu, pro které chcete zajistit určitý stav.</span><span class="sxs-lookup"><span data-stu-id="a41d5-111">Indicates the account name for which you want to ensure a specific state.</span></span>|
| <span data-ttu-id="a41d5-112">Popis</span><span class="sxs-lookup"><span data-stu-id="a41d5-112">Description</span></span>| <span data-ttu-id="a41d5-113">Určuje popis, který chcete použít pro uživatelský účet.</span><span class="sxs-lookup"><span data-stu-id="a41d5-113">Indicates the description you want to use for the user account.</span></span>|
| <span data-ttu-id="a41d5-114">Zakázáno</span><span class="sxs-lookup"><span data-stu-id="a41d5-114">Disabled</span></span>| <span data-ttu-id="a41d5-115">Určuje, zda je povolen účet.</span><span class="sxs-lookup"><span data-stu-id="a41d5-115">Indicates if the account is enabled.</span></span> <span data-ttu-id="a41d5-116">Tuto vlastnost nastavit na __$true__ zajistit, že tento účet je zakázané a nastavte ji na __$false__ zajistit, že je povolena.</span><span class="sxs-lookup"><span data-stu-id="a41d5-116">Set this property to __$true__ to ensure that this account is disabled, and set it to __$false__ to ensure that it is enabled.</span></span>|
| <span data-ttu-id="a41d5-117">Ujistěte se</span><span class="sxs-lookup"><span data-stu-id="a41d5-117">Ensure</span></span>| <span data-ttu-id="a41d5-118">Určuje, jestli účet existuje.</span><span class="sxs-lookup"><span data-stu-id="a41d5-118">Indicates if the account exists.</span></span> <span data-ttu-id="a41d5-119">Nastavením této vlastnosti "Přítomen" zajistit, že existuje účet a nastavte ji na "Chybí" zajistit, že účet neexistuje.</span><span class="sxs-lookup"><span data-stu-id="a41d5-119">Set this property to "Present" to ensure that the account exists, and set it to "Absent" to ensure that the account does not exist.</span></span>|
| <span data-ttu-id="a41d5-120">Úplný název</span><span class="sxs-lookup"><span data-stu-id="a41d5-120">FullName</span></span>| <span data-ttu-id="a41d5-121">Představuje řetězec s úplný název, který chcete použít pro uživatelský účet.</span><span class="sxs-lookup"><span data-stu-id="a41d5-121">Represents a string with the full name you want to use for the user account.</span></span>|
| <span data-ttu-id="a41d5-122">Heslo</span><span class="sxs-lookup"><span data-stu-id="a41d5-122">Password</span></span>| <span data-ttu-id="a41d5-123">Určuje heslo, které chcete použít pro tento účet.</span><span class="sxs-lookup"><span data-stu-id="a41d5-123">Indicates the password you want to use for this account.</span></span> |
| <span data-ttu-id="a41d5-124">PasswordChangeNotAllowed</span><span class="sxs-lookup"><span data-stu-id="a41d5-124">PasswordChangeNotAllowed</span></span>| <span data-ttu-id="a41d5-125">Určuje, pokud uživatel změnit heslo.</span><span class="sxs-lookup"><span data-stu-id="a41d5-125">Indicates if the user can change the password.</span></span> <span data-ttu-id="a41d5-126">Tuto vlastnost nastavit na __$true__ zajistit, že uživatel nemůže změnit heslo a nastavte ji na __$false__ umožňuje uživatelům změnit heslo.</span><span class="sxs-lookup"><span data-stu-id="a41d5-126">Set this property to __$true__ to ensure that the user cannot change the password, and set it to __$false__ to allow the user to change the password.</span></span> <span data-ttu-id="a41d5-127">Výchozí hodnota je __$false__.</span><span class="sxs-lookup"><span data-stu-id="a41d5-127">The default value is __$false__.</span></span>|
| <span data-ttu-id="a41d5-128">PasswordChangeRequired</span><span class="sxs-lookup"><span data-stu-id="a41d5-128">PasswordChangeRequired</span></span>| <span data-ttu-id="a41d5-129">Označuje, pokud uživatel musí změnit heslo při příštím přihlašování.</span><span class="sxs-lookup"><span data-stu-id="a41d5-129">Indicates if the user must change the password at the next sign in.</span></span> <span data-ttu-id="a41d5-130">Tuto vlastnost nastavit na __$true__ Pokud musí uživatel změnit heslo.</span><span class="sxs-lookup"><span data-stu-id="a41d5-130">Set this property to __$true__ if the user must change the password.</span></span> <span data-ttu-id="a41d5-131">Výchozí hodnota je __$true__.</span><span class="sxs-lookup"><span data-stu-id="a41d5-131">The default value is __$true__.</span></span>|
| <span data-ttu-id="a41d5-132">PasswordNeverExpires</span><span class="sxs-lookup"><span data-stu-id="a41d5-132">PasswordNeverExpires</span></span>| <span data-ttu-id="a41d5-133">Označuje, pokud vyprší platnost hesla.</span><span class="sxs-lookup"><span data-stu-id="a41d5-133">Indicates if the password will expire.</span></span> <span data-ttu-id="a41d5-134">K zajištění, že heslo pro tento účet nikdy nevyprší, nastavte tuto vlastnost __$true__a nastavte ji na __$false__ Pokud vyprší platnost hesla.</span><span class="sxs-lookup"><span data-stu-id="a41d5-134">To ensure that the password for this account will never expire, set this property to __$true__, and set it to __$false__ if the password will expire.</span></span> <span data-ttu-id="a41d5-135">Výchozí hodnota je __$false__.</span><span class="sxs-lookup"><span data-stu-id="a41d5-135">The default value is __$false__.</span></span>|
| <span data-ttu-id="a41d5-136">dependsOn</span><span class="sxs-lookup"><span data-stu-id="a41d5-136">DependsOn</span></span> | <span data-ttu-id="a41d5-137">Určuje, že konfigurace jiný prostředek musí spouštět předtím, než je tento prostředek nakonfigurován.</span><span class="sxs-lookup"><span data-stu-id="a41d5-137">Indicates that the configuration of another resource must run before this resource is configured.</span></span> <span data-ttu-id="a41d5-138">Pokud ID konfigurace prostředků skriptu blok, který chcete spustit nejprve je třeba __ResourceName__ a její typ je __ResourceType__, syntaxe pro používání této vlastnosti je `DependsOn = "[ResourceType]ResourceName"`.</span><span class="sxs-lookup"><span data-stu-id="a41d5-138">For example, if the ID of the resource configuration script block that you want to run first is __ResourceName__ and its type is __ResourceType__, the syntax for using this property is `DependsOn = "[ResourceType]ResourceName"`.</span></span>|

## <a name="example"></a><span data-ttu-id="a41d5-139">Příklad</span><span class="sxs-lookup"><span data-stu-id="a41d5-139">Example</span></span>

```powershell
User UserExample
{
    Ensure = "Present"  # To ensure the user account does not exist, set Ensure to "Absent"
    UserName = "SomeName"
    Password = $passwordCred # This needs to be a credential object
    DependsOn = "[Group]GroupExample" # Configures GroupExample first
}
```