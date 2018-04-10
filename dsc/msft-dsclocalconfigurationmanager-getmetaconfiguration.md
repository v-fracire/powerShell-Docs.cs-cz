---
ms.date: 06/12/2017
ms.topic: conceptual
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Metoda GetMetaConfiguration třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: ddc016402239bcdea060a717fbac9ab7ea42698c
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="getmetaconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="27738-103">Metoda GetMetaConfiguration třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="27738-103">GetMetaConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="27738-104">Získá místní nastavení nástroje Configuration Manager, která slouží k řízení konfigurace agenta.</span><span class="sxs-lookup"><span data-stu-id="27738-104">Gets the local Configuration Manager settings that are used to control the Configuration Agent.</span></span>

<a name="syntax"></a><span data-ttu-id="27738-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="27738-105">Syntax</span></span>
------

```mof
uint32 GetMetaConfiguration(
  [out] MSFT_DSCMetaConfiguration MetaConfiguration
);
```

<a name="parameters"></a><span data-ttu-id="27738-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="27738-106">Parameters</span></span>
----------

<span data-ttu-id="27738-107">*Metakonfiguraci* \[out\] na vrátí, obsahuje vložené instance **MSFT_DSCMetaConfiguration** třídu, která definuje nastavení.</span><span class="sxs-lookup"><span data-stu-id="27738-107">*MetaConfiguration* \[out\] On return, contains an embedded instance of the **MSFT_DSCMetaConfiguration** class that defines the settings.</span></span>

## <a name="return-value"></a><span data-ttu-id="27738-108">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="27738-108">Return value</span></span>
------------

<span data-ttu-id="27738-109">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="27738-109">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="27738-110">Poznámky</span><span class="sxs-lookup"><span data-stu-id="27738-110">Remarks</span></span>

<span data-ttu-id="27738-111">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="27738-111">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="27738-112">Požadavky</span><span class="sxs-lookup"><span data-stu-id="27738-112">Requirements</span></span>
------------
><span data-ttu-id="27738-113">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="27738-113">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="27738-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="27738-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="27738-115">Viz taky</span><span class="sxs-lookup"><span data-stu-id="27738-115">See also</span></span>


[<span data-ttu-id="27738-116">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="27738-116">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)