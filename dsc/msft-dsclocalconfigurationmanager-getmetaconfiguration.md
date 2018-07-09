---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Metoda GetMetaConfiguration třídy MSFT_DSCLocalConfigurationManager
ms.openlocfilehash: e14237ef68b95d68e2f14071aa1fa6ba0717f39f
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37892837"
---
# <a name="getmetaconfiguration-method-of-the-msftdsclocalconfigurationmanager-class"></a><span data-ttu-id="4a7bd-103">Metoda GetMetaConfiguration třídy MSFT_DSCLocalConfigurationManager</span><span class="sxs-lookup"><span data-stu-id="4a7bd-103">GetMetaConfiguration method of the MSFT_DSCLocalConfigurationManager class</span></span>

<span data-ttu-id="4a7bd-104">Získá místní nastavení nástroje Configuration Manager, které se používají k řízení konfigurace agenta.</span><span class="sxs-lookup"><span data-stu-id="4a7bd-104">Gets the local Configuration Manager settings that are used to control the Configuration Agent.</span></span>

## <a name="syntax"></a><span data-ttu-id="4a7bd-105">Syntaxe</span><span class="sxs-lookup"><span data-stu-id="4a7bd-105">Syntax</span></span>

```mof
uint32 GetMetaConfiguration(
  [out] MSFT_DSCMetaConfiguration MetaConfiguration
);
```

## <a name="parameters"></a><span data-ttu-id="4a7bd-106">Parameters</span><span class="sxs-lookup"><span data-stu-id="4a7bd-106">Parameters</span></span>

<span data-ttu-id="4a7bd-107">*MetaConfiguration* \[si\] na vrátit, obsahuje vložený instance **MSFT_DSCMetaConfiguration** třídu, která definuje nastavení.</span><span class="sxs-lookup"><span data-stu-id="4a7bd-107">*MetaConfiguration* \[out\] On return, contains an embedded instance of the **MSFT_DSCMetaConfiguration** class that defines the settings.</span></span>

## <a name="return-value"></a><span data-ttu-id="4a7bd-108">Návratová hodnota</span><span class="sxs-lookup"><span data-stu-id="4a7bd-108">Return value</span></span>

<span data-ttu-id="4a7bd-109">Vrátí nulu v případě úspěchu; v opačném případě vrátí kód chyby.</span><span class="sxs-lookup"><span data-stu-id="4a7bd-109">Returns zero on success; otherwise returns an error code.</span></span>

## <a name="remarks"></a><span data-ttu-id="4a7bd-110">Poznámky</span><span class="sxs-lookup"><span data-stu-id="4a7bd-110">Remarks</span></span>

<span data-ttu-id="4a7bd-111">Toto je statické metody.</span><span class="sxs-lookup"><span data-stu-id="4a7bd-111">This is a static method.</span></span>

## <a name="requirements"></a><span data-ttu-id="4a7bd-112">Požadavky</span><span class="sxs-lookup"><span data-stu-id="4a7bd-112">Requirements</span></span>

<span data-ttu-id="4a7bd-113">**Soubor MOF:** DscCore.mof</span><span class="sxs-lookup"><span data-stu-id="4a7bd-113">**MOF:** DscCore.mof</span></span>

<span data-ttu-id="4a7bd-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span><span class="sxs-lookup"><span data-stu-id="4a7bd-114">**Namespace**: Root\Microsoft\Windows\DesiredStateConfiguration</span></span>

## <a name="see-also"></a><span data-ttu-id="4a7bd-115">Viz taky</span><span class="sxs-lookup"><span data-stu-id="4a7bd-115">See also</span></span>

[<span data-ttu-id="4a7bd-116">**MSFT_DSCLocalConfigurationManager**</span><span class="sxs-lookup"><span data-stu-id="4a7bd-116">**MSFT_DSCLocalConfigurationManager**</span></span>](msft-dsclocalconfigurationmanager.md)