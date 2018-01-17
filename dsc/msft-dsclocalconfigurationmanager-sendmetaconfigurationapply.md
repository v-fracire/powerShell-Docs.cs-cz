---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Metoda SendMetaConfigurationApply MSFT_DSCLocalConfigurationManager třídy"
ms.openlocfilehash: 350555220757b1939b1de34ab423e963635eb53c
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="sendmetaconfigurationapply-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="b54de-103">Metoda SendMetaConfigurationApply MSFT_DSCLocalConfigurationManager třídy</span><span class="sxs-lookup"><span data-stu-id="b54de-103">SendMetaConfigurationApply method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="b54de-104">Nastaví správce místní konfigurace nastavení, která slouží k řízení konfigurace agenta.</span><span class="sxs-lookup"><span data-stu-id="b54de-104">Sets the Local Configuration Manager settings that are used to control the Configuration Agent.</span></span>

<a name="syntax"></a><span data-ttu-id="b54de-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="b54de-105">Syntax</span></span>
------

```mof
uint32 SendMetaConfigurationApply(
  [in] uint8   ConfigurationData[],
  [in] boolean force
);
```

<a name="parameters"></a><span data-ttu-id="b54de-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="b54de-106">Parameters</span></span>
----------

<span data-ttu-id="b54de-107">*ConfigurationData* \[v\]</span><span class="sxs-lookup"><span data-stu-id="b54de-107">*ConfigurationData* \[in\]</span></span>  
<span data-ttu-id="b54de-108">Data prostředí pro konfiguraci.</span><span class="sxs-lookup"><span data-stu-id="b54de-108">The environment data for the configuration.</span></span>

<span data-ttu-id="b54de-109">*Vynutit* \[v\]</span><span class="sxs-lookup"><span data-stu-id="b54de-109">*force* \[in\]</span></span>  
<span data-ttu-id="b54de-110">**Hodnota TRUE,** vynutit konfiguraci zastavit.</span><span class="sxs-lookup"><span data-stu-id="b54de-110">**true** to force the configuration to stop.</span></span>

## <a name="return-value"></a><span data-ttu-id="b54de-111">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="b54de-111">Return value</span></span>
------------

<span data-ttu-id="b54de-112">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="b54de-112">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="b54de-113">Poznámky</span><span class="sxs-lookup"><span data-stu-id="b54de-113">Remarks</span></span>

<span data-ttu-id="b54de-114">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="b54de-114">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="b54de-115">Požadavky</span><span class="sxs-lookup"><span data-stu-id="b54de-115">Requirements</span></span>
------------
><span data-ttu-id="b54de-116">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="b54de-116">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="b54de-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="b54de-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="b54de-118">Viz taky</span><span class="sxs-lookup"><span data-stu-id="b54de-118">See also</span></span>


[<span data-ttu-id="b54de-119">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="b54de-119">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



