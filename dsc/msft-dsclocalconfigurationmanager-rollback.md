---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Metoda vrácení zpět MSFT_DSCLocalConfigurationManager třídy"
ms.openlocfilehash: a219703389405c0dd457d0b2e0b1c54b9c28f559
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="rollback-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="30268-103">Metoda vrácení zpět MSFT_DSCLocalConfigurationManager třídy</span><span class="sxs-lookup"><span data-stu-id="30268-103">RollBack method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="30268-104">Vrátí konfiguraci zpět na předchozí verzi.</span><span class="sxs-lookup"><span data-stu-id="30268-104">Rolls back the configuration to a previous version.</span></span>

<a name="syntax"></a><span data-ttu-id="30268-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="30268-105">Syntax</span></span>
------

```mof
uint32 RollBack(
  [in] uint8 configurationNumber
);
```

<a name="parameters"></a><span data-ttu-id="30268-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="30268-106">Parameters</span></span>
----------

<span data-ttu-id="30268-107">*configurationNumber* \[v\]</span><span class="sxs-lookup"><span data-stu-id="30268-107">*configurationNumber* \[in\]</span></span>  
<span data-ttu-id="30268-108">Určuje požadovanou konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="30268-108">Specifies the requested configuration.</span></span> 

## <a name="return-value"></a><span data-ttu-id="30268-109">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="30268-109">Return value</span></span>
------------

<span data-ttu-id="30268-110">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="30268-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="30268-111">Poznámky</span><span class="sxs-lookup"><span data-stu-id="30268-111">Remarks</span></span>

<span data-ttu-id="30268-112">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="30268-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="30268-113">Požadavky</span><span class="sxs-lookup"><span data-stu-id="30268-113">Requirements</span></span>
------------
><span data-ttu-id="30268-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="30268-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="30268-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="30268-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="30268-116">Viz taky</span><span class="sxs-lookup"><span data-stu-id="30268-116">See also</span></span>


[<span data-ttu-id="30268-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="30268-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



