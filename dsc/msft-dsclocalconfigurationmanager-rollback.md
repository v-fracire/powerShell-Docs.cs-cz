---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Metoda vrácení zpět MSFT_DSCLocalConfigurationManager třídy"
ms.openlocfilehash: b8597e3eb7872d9894863fb02d927c9f475da44c
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="rollback-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="eb4f7-103">Metoda vrácení zpět MSFT_DSCLocalConfigurationManager třídy</span><span class="sxs-lookup"><span data-stu-id="eb4f7-103">RollBack method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="eb4f7-104">Vrátí konfiguraci zpět na předchozí verzi.</span><span class="sxs-lookup"><span data-stu-id="eb4f7-104">Rolls back the configuration to a previous version.</span></span>

<a name="syntax"></a><span data-ttu-id="eb4f7-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="eb4f7-105">Syntax</span></span>
------

```mof
uint32 RollBack(
  [in] uint8 configurationNumber
);
```

<a name="parameters"></a><span data-ttu-id="eb4f7-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="eb4f7-106">Parameters</span></span>
----------

<span data-ttu-id="eb4f7-107">*configurationNumber* \[v\]</span><span class="sxs-lookup"><span data-stu-id="eb4f7-107">*configurationNumber* \[in\]</span></span>  
<span data-ttu-id="eb4f7-108">Určuje požadovanou konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="eb4f7-108">Specifies the requested configuration.</span></span> 

## <a name="return-value"></a><span data-ttu-id="eb4f7-109">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="eb4f7-109">Return value</span></span>
------------

<span data-ttu-id="eb4f7-110">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="eb4f7-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="eb4f7-111">Poznámky</span><span class="sxs-lookup"><span data-stu-id="eb4f7-111">Remarks</span></span>

<span data-ttu-id="eb4f7-112">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="eb4f7-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="eb4f7-113">Požadavky</span><span class="sxs-lookup"><span data-stu-id="eb4f7-113">Requirements</span></span>
------------
><span data-ttu-id="eb4f7-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="eb4f7-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="eb4f7-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="eb4f7-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="eb4f7-116">Viz taky</span><span class="sxs-lookup"><span data-stu-id="eb4f7-116">See also</span></span>


[<span data-ttu-id="eb4f7-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="eb4f7-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



