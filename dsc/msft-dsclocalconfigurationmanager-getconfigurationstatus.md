---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Metoda GetConfigurationStatus MSFT_DSCLocalConfigurationManager třídy"
ms.openlocfilehash: e02ed81a7b8436323bc68aaa2587a445e6a5adf9
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="getconfigurationstatus-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="0b77a-103">Metoda GetConfigurationStatus MSFT_DSCLocalConfigurationManager třídy</span><span class="sxs-lookup"><span data-stu-id="0b77a-103">GetConfigurationStatus method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="0b77a-104">Načtení historie stav konfigurace.</span><span class="sxs-lookup"><span data-stu-id="0b77a-104">Get the configuration status history.</span></span>

<a name="syntax"></a><span data-ttu-id="0b77a-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="0b77a-105">Syntax</span></span>
------

```mof
uint32 GetConfigurationStatus(
  [in]  boolean                     All,
  [out] MSFT_DSCConfigurationStatus configurationStatus[]
);
```

<a name="parameters"></a><span data-ttu-id="0b77a-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="0b77a-106">Parameters</span></span>
----------

<span data-ttu-id="0b77a-107">*Všechny* \[v\]</span><span class="sxs-lookup"><span data-stu-id="0b77a-107">*All* \[in\]</span></span>  
<span data-ttu-id="0b77a-108">**Hodnota TRUE,** Pokud tato metoda by měla vrátit informace o všech konfigurace běží na počítači, včetně konfigurace aplikace a kontrolu konzistence.</span><span class="sxs-lookup"><span data-stu-id="0b77a-108">**true** if this method should return information about all the configuration runs on the machine, including the configuration application and the consistency check.</span></span>

<span data-ttu-id="0b77a-109">*configurationStatus* \[out\]</span><span class="sxs-lookup"><span data-stu-id="0b77a-109">*configurationStatus* \[out\]</span></span>  
<span data-ttu-id="0b77a-110">Při návratu, obsahuje vložené instance **MSFT_DSCConfigurationStatus** třídu, která definuje nastavení.</span><span class="sxs-lookup"><span data-stu-id="0b77a-110">On return, contains an embedded instance of the **MSFT_DSCConfigurationStatus** class that defines the settings.</span></span>

## <a name="return-value"></a><span data-ttu-id="0b77a-111">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="0b77a-111">Return value</span></span>
------------

<span data-ttu-id="0b77a-112">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="0b77a-112">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="0b77a-113">Poznámky</span><span class="sxs-lookup"><span data-stu-id="0b77a-113">Remarks</span></span>

<span data-ttu-id="0b77a-114">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="0b77a-114">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="0b77a-115">Požadavky</span><span class="sxs-lookup"><span data-stu-id="0b77a-115">Requirements</span></span>
------------
><span data-ttu-id="0b77a-116">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="0b77a-116">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="0b77a-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="0b77a-117">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="0b77a-118">Viz taky</span><span class="sxs-lookup"><span data-stu-id="0b77a-118">See also</span></span>


[<span data-ttu-id="0b77a-119">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="0b77a-119">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



