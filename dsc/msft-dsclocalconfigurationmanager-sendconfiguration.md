---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Metoda SendConfiguration MSFT_DSCLocalConfigurationManager třídy"
ms.openlocfilehash: 72c59b5aad293fa561146e5ad6822f27f40f321f
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="sendconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="10ccc-103">Metoda SendConfiguration MSFT_DSCLocalConfigurationManager třídy</span><span class="sxs-lookup"><span data-stu-id="10ccc-103">SendConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="10ccc-104">Odešle spravovaný uzel dokumentu konfigurace a uloží ji jako nevyřízenou změnu.</span><span class="sxs-lookup"><span data-stu-id="10ccc-104">Sends the configuration document to the managed node and saves it as a pending change.</span></span>

<a name="syntax"></a><span data-ttu-id="10ccc-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="10ccc-105">Syntax</span></span>
------

```mof
uint32 SendConfiguration(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

<a name="parameters"></a><span data-ttu-id="10ccc-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="10ccc-106">Parameters</span></span>
----------

<span data-ttu-id="10ccc-107">*ConfigurationData* \[v\]</span><span class="sxs-lookup"><span data-stu-id="10ccc-107">*ConfigurationData* \[in\]</span></span>  
<span data-ttu-id="10ccc-108">Data prostředí pro konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="10ccc-108">The environment data for the configuration.</span></span>

<span data-ttu-id="10ccc-109">*Vynutit* \[v\]</span><span class="sxs-lookup"><span data-stu-id="10ccc-109">*force* \[in\]</span></span>  
<span data-ttu-id="10ccc-110">**Hodnota TRUE,** vynutit konfiguraci zastavit.</span><span class="sxs-lookup"><span data-stu-id="10ccc-110">**true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="10ccc-111">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="10ccc-111">Return value</span></span>
------------

<span data-ttu-id="10ccc-112">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="10ccc-112">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="10ccc-113">Poznámky</span><span class="sxs-lookup"><span data-stu-id="10ccc-113">Remarks</span></span>

<span data-ttu-id="10ccc-114">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="10ccc-114">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="10ccc-115">Požadavky</span><span class="sxs-lookup"><span data-stu-id="10ccc-115">Requirements</span></span>
------------
><span data-ttu-id="10ccc-116">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="10ccc-116">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="10ccc-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="10ccc-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="10ccc-118">Viz taky</span><span class="sxs-lookup"><span data-stu-id="10ccc-118">See also</span></span>


[<span data-ttu-id="10ccc-119">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="10ccc-119">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



