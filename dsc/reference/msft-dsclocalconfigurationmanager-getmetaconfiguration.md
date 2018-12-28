---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Metoda GetMetaConfiguration třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: e14237ef68b95d68e2f14071aa1fa6ba0717f39f
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403833"
---
# <a name="getmetaconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="663f8-103">Metoda GetMetaConfiguration třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="663f8-103">GetMetaConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="663f8-104">Získá místní nastavení nástroje Configuration Manager, které se používají k řízení konfigurace agenta.</span><span class="sxs-lookup"><span data-stu-id="663f8-104">Gets the local Configuration Manager settings that are used to control the Configuration Agent.</span></span>

## <a name="syntax"></a><span data-ttu-id="663f8-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="663f8-105">Syntax</span></span>

```mof
uint32 GetMetaConfiguration(
  [out] MSFT_DSCMetaConfiguration MetaConfiguration
);
```

## <a name="parameters"></a><span data-ttu-id="663f8-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="663f8-106">Parameters</span></span>

<span data-ttu-id="663f8-107">*MetaConfiguration* \[si\] na vrátit, obsahuje vložený instance **MSFT_DSCMetaConfiguration** třídu, která definuje nastavení.</span><span class="sxs-lookup"><span data-stu-id="663f8-107">*MetaConfiguration* \[out\] On return, contains an embedded instance of the **MSFT_DSCMetaConfiguration** class that defines the settings.</span></span>

## <a name="return-value"></a><span data-ttu-id="663f8-108">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="663f8-108">Return value</span></span>

<span data-ttu-id="663f8-109">Vrátí nulu v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="663f8-109">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="663f8-110">Poznámky</span><span class="sxs-lookup"><span data-stu-id="663f8-110">Remarks</span></span>

<span data-ttu-id="663f8-111">Toto je statické metody.</span><span class="sxs-lookup"><span data-stu-id="663f8-111">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="663f8-112">Požadavky</span><span class="sxs-lookup"><span data-stu-id="663f8-112">Requirements</span></span>

<span data-ttu-id="663f8-113">**SOUBOR MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="663f8-113">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="663f8-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="663f8-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="663f8-115">Viz taky</span><span class="sxs-lookup"><span data-stu-id="663f8-115">See also</span></span>

[<span data-ttu-id="663f8-116">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="663f8-116">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)