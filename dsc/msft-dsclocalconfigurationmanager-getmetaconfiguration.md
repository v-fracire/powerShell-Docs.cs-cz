---
ms.date: 06/12/2017
keywords: DSC prostředí powershell, konfiguraci, instalační program
title: Metoda GetMetaConfiguration třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: ebf2b65f152c622ccf42e12545b0048a0b96d963
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
---
# <a name="getmetaconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="a888d-103">Metoda GetMetaConfiguration třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="a888d-103">GetMetaConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="a888d-104">Získá místní nastavení nástroje Configuration Manager, která slouží k řízení konfigurace agenta.</span><span class="sxs-lookup"><span data-stu-id="a888d-104">Gets the local Configuration Manager settings that are used to control the Configuration Agent.</span></span>

<a name="syntax"></a><span data-ttu-id="a888d-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="a888d-105">Syntax</span></span>
------

```mof
uint32 GetMetaConfiguration(
  [out] MSFT_DSCMetaConfiguration MetaConfiguration
);
```

<a name="parameters"></a><span data-ttu-id="a888d-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="a888d-106">Parameters</span></span>
----------

<span data-ttu-id="a888d-107">*Metakonfiguraci* \[out\] na vrátí, obsahuje vložené instance **MSFT_DSCMetaConfiguration** třídu, která definuje nastavení.</span><span class="sxs-lookup"><span data-stu-id="a888d-107">*MetaConfiguration* \[out\] On return, contains an embedded instance of the **MSFT_DSCMetaConfiguration** class that defines the settings.</span></span>

## <a name="return-value"></a><span data-ttu-id="a888d-108">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="a888d-108">Return value</span></span>
------------

<span data-ttu-id="a888d-109">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="a888d-109">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="a888d-110">Poznámky</span><span class="sxs-lookup"><span data-stu-id="a888d-110">Remarks</span></span>

<span data-ttu-id="a888d-111">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="a888d-111">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="a888d-112">Požadavky</span><span class="sxs-lookup"><span data-stu-id="a888d-112">Requirements</span></span>
------------
><span data-ttu-id="a888d-113">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="a888d-113">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="a888d-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="a888d-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="a888d-115">Viz taky</span><span class="sxs-lookup"><span data-stu-id="a888d-115">See also</span></span>


[<span data-ttu-id="a888d-116">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="a888d-116">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)