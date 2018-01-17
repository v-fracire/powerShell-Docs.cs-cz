---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Metoda StopConfiguration MSFT_DSCLocalConfigurationManager třídy"
ms.openlocfilehash: 66d00cb40750e91e4b369a2e8cebb449697406d9
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="stopconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="10a84-103">Metoda StopConfiguration MSFT_DSCLocalConfigurationManager třídy</span><span class="sxs-lookup"><span data-stu-id="10a84-103">StopConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="10a84-104">Zastaví změny konfigurace, která je v průběhu.</span><span class="sxs-lookup"><span data-stu-id="10a84-104">Stops the configuration change that is in progress.</span></span>

<a name="syntax"></a><span data-ttu-id="10a84-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="10a84-105">Syntax</span></span>
------

```mof
uint32 StopConfiguration(
  [in] boolean force
);
```

<a name="parameters"></a><span data-ttu-id="10a84-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="10a84-106">Parameters</span></span>
----------

<span data-ttu-id="10a84-107">*Vynutit* \[v\]</span><span class="sxs-lookup"><span data-stu-id="10a84-107">*force* \[in\]</span></span>  
<span data-ttu-id="10a84-108">**Hodnota TRUE,** vynutit konfiguraci zastavit.</span><span class="sxs-lookup"><span data-stu-id="10a84-108">**true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="10a84-109">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="10a84-109">Return value</span></span>
------------

<span data-ttu-id="10a84-110">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="10a84-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="10a84-111">Poznámky</span><span class="sxs-lookup"><span data-stu-id="10a84-111">Remarks</span></span>

<span data-ttu-id="10a84-112">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="10a84-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="10a84-113">Požadavky</span><span class="sxs-lookup"><span data-stu-id="10a84-113">Requirements</span></span>
------------
><span data-ttu-id="10a84-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="10a84-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="10a84-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="10a84-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="10a84-116">Viz taky</span><span class="sxs-lookup"><span data-stu-id="10a84-116">See also</span></span>


[<span data-ttu-id="10a84-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="10a84-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



