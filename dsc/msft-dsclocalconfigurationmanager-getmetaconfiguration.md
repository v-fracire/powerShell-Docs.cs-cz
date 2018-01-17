---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Metoda GetMetaConfiguration MSFT_DSCLocalConfigurationManager třídy"
ms.openlocfilehash: 695be4ee6490567295fda0cc44635870362d24b8
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="getmetaconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="79ad9-103">Metoda GetMetaConfiguration MSFT_DSCLocalConfigurationManager třídy</span><span class="sxs-lookup"><span data-stu-id="79ad9-103">GetMetaConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="79ad9-104">Získá místní nastavení nástroje Configuration Manager, která slouží k řízení konfigurace agenta.</span><span class="sxs-lookup"><span data-stu-id="79ad9-104">Gets the local Configuration Manager settings that are used to control the Configuration Agent.</span></span>

<a name="syntax"></a><span data-ttu-id="79ad9-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="79ad9-105">Syntax</span></span>
------

```mof
uint32 GetMetaConfiguration(
  [out] MSFT_DSCMetaConfiguration MetaConfiguration
);
```

<a name="parameters"></a><span data-ttu-id="79ad9-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="79ad9-106">Parameters</span></span>
----------

<span data-ttu-id="79ad9-107">*Metakonfiguraci* \[out\]</span><span class="sxs-lookup"><span data-stu-id="79ad9-107">*MetaConfiguration* \[out\]</span></span>  
<span data-ttu-id="79ad9-108">Při návratu, obsahuje vložené instance **MSFT_DSCMetaConfiguration** třídu, která definuje nastavení.</span><span class="sxs-lookup"><span data-stu-id="79ad9-108">On return, contains an embedded instance of the **MSFT_DSCMetaConfiguration** class that defines the settings.</span></span>

## <a name="return-value"></a><span data-ttu-id="79ad9-109">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="79ad9-109">Return value</span></span>
------------

<span data-ttu-id="79ad9-110">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="79ad9-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="79ad9-111">Poznámky</span><span class="sxs-lookup"><span data-stu-id="79ad9-111">Remarks</span></span>

<span data-ttu-id="79ad9-112">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="79ad9-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="79ad9-113">Požadavky</span><span class="sxs-lookup"><span data-stu-id="79ad9-113">Requirements</span></span>
------------
><span data-ttu-id="79ad9-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="79ad9-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="79ad9-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="79ad9-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="79ad9-116">Viz taky</span><span class="sxs-lookup"><span data-stu-id="79ad9-116">See also</span></span>


[<span data-ttu-id="79ad9-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="79ad9-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



