---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Metoda StopConfiguration MSFT_DSCLocalConfigurationManager třídy"
ms.openlocfilehash: f0b550615b20f07f99c8ed7009805c45794bfe22
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="stopconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="ef22e-103">Metoda StopConfiguration MSFT_DSCLocalConfigurationManager třídy</span><span class="sxs-lookup"><span data-stu-id="ef22e-103">StopConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="ef22e-104">Zastaví změny konfigurace, která je v průběhu.</span><span class="sxs-lookup"><span data-stu-id="ef22e-104">Stops the configuration change that is in progress.</span></span>

<a name="syntax"></a><span data-ttu-id="ef22e-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="ef22e-105">Syntax</span></span>
------

```mof
uint32 StopConfiguration(
  [in] boolean force
);
```

<a name="parameters"></a><span data-ttu-id="ef22e-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="ef22e-106">Parameters</span></span>
----------

<span data-ttu-id="ef22e-107">*Vynutit* \[v\]</span><span class="sxs-lookup"><span data-stu-id="ef22e-107">*force* \[in\]</span></span>  
<span data-ttu-id="ef22e-108">**Hodnota TRUE,** vynutit konfiguraci zastavit.</span><span class="sxs-lookup"><span data-stu-id="ef22e-108">**true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="ef22e-109">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="ef22e-109">Return value</span></span>
------------

<span data-ttu-id="ef22e-110">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="ef22e-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="ef22e-111">Poznámky</span><span class="sxs-lookup"><span data-stu-id="ef22e-111">Remarks</span></span>

<span data-ttu-id="ef22e-112">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="ef22e-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="ef22e-113">Požadavky</span><span class="sxs-lookup"><span data-stu-id="ef22e-113">Requirements</span></span>
------------
><span data-ttu-id="ef22e-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="ef22e-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="ef22e-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="ef22e-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="ef22e-116">Viz taky</span><span class="sxs-lookup"><span data-stu-id="ef22e-116">See also</span></span>


[<span data-ttu-id="ef22e-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="ef22e-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



