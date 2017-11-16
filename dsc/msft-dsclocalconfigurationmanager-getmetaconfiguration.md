---
ms.date: 2017-06-12
author: eslesar
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Metoda GetMetaConfiguration MSFT_DSCLocalConfigurationManager třídy"
ms.openlocfilehash: 4f209014e9fde5841a9bce743f5364e6677d1e41
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="getmetaconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="9c67e-103">Metoda GetMetaConfiguration MSFT_DSCLocalConfigurationManager třídy</span><span class="sxs-lookup"><span data-stu-id="9c67e-103">GetMetaConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="9c67e-104">Získá místní nastavení nástroje Configuration Manager, která slouží k řízení konfigurace agenta.</span><span class="sxs-lookup"><span data-stu-id="9c67e-104">Gets the local Configuration Manager settings that are used to control the Configuration Agent.</span></span>

<a name="syntax"></a><span data-ttu-id="9c67e-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="9c67e-105">Syntax</span></span>
------

```mof
uint32 GetMetaConfiguration(
  [out] MSFT_DSCMetaConfiguration MetaConfiguration
);
```

<a name="parameters"></a><span data-ttu-id="9c67e-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="9c67e-106">Parameters</span></span>
----------

<span data-ttu-id="9c67e-107">*Metakonfiguraci* \[out\]</span><span class="sxs-lookup"><span data-stu-id="9c67e-107">*MetaConfiguration* \[out\]</span></span>  
<span data-ttu-id="9c67e-108">Při návratu, obsahuje vložené instance **MSFT_DSCMetaConfiguration** třídu, která definuje nastavení.</span><span class="sxs-lookup"><span data-stu-id="9c67e-108">On return, contains an embedded instance of the **MSFT_DSCMetaConfiguration** class that defines the settings.</span></span>

## <a name="return-value"></a><span data-ttu-id="9c67e-109">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="9c67e-109">Return value</span></span>
------------

<span data-ttu-id="9c67e-110">Vrátí nula v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="9c67e-110">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="9c67e-111">Poznámky</span><span class="sxs-lookup"><span data-stu-id="9c67e-111">Remarks</span></span>

<span data-ttu-id="9c67e-112">Jde o statickou metodu.</span><span class="sxs-lookup"><span data-stu-id="9c67e-112">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="9c67e-113">Požadavky</span><span class="sxs-lookup"><span data-stu-id="9c67e-113">Requirements</span></span>
------------
><span data-ttu-id="9c67e-114">**MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="9c67e-114">**MOF:** DscCore.mof</span></span>

><span data-ttu-id="9c67e-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="9c67e-115">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>


## <a name="see-also"></a><span data-ttu-id="9c67e-116">Viz taky</span><span class="sxs-lookup"><span data-stu-id="9c67e-116">See also</span></span>


[<span data-ttu-id="9c67e-117">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="9c67e-117">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)


 

 



