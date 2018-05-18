---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: 01d4989711c22db20431876c52740afb350caad0
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
---
# <a name="generate-powershell-cmdlets-based-on-odata-endpoint"></a><span data-ttu-id="87181-102">Generování powershellových rutin na základě koncového bodu OData</span><span class="sxs-lookup"><span data-stu-id="87181-102">Generate PowerShell Cmdlets based on OData Endpoint</span></span>
<a name="generate-windows-powershell-cmdlets-based-on-an-odata-endpoint"></a><span data-ttu-id="87181-103">Generovat rutiny prostředí Windows PowerShell, které jsou založené na koncový bod OData</span><span class="sxs-lookup"><span data-stu-id="87181-103">Generate Windows PowerShell cmdlets based on an OData endpoint</span></span>
--------------------------------------------------------------

<span data-ttu-id="87181-104">**Export-ODataEndpointProxy** je rutina, která generuje sadu rutin prostředí Windows PowerShell podle funkce vystavené dané koncový bod OData.</span><span class="sxs-lookup"><span data-stu-id="87181-104">**Export-ODataEndpointProxy** is a cmdlet that generates a set of Windows PowerShell cmdlets based on the functionality exposed by a given OData endpoint.</span></span>

<span data-ttu-id="87181-105">Následující příklad ukazuje, jak použít tuto novou rutinu:</span><span class="sxs-lookup"><span data-stu-id="87181-105">The following example shows how to use this new cmdlet:</span></span>

<span data-ttu-id="87181-106">\# Základní použití malá ODataEndpointProxy exportu</span><span class="sxs-lookup"><span data-stu-id="87181-106">\# Basic use case of Export-ODataEndpointProxy</span></span>

```powershell
Export-ODataEndpointProxy -Uri 'http://services.odata.org/v3/(S(snyobsk1hhutkb2yulwldgf1))/odata/odata.svc' -OutputModule C:\Users\user\Generated.psd1

ipmo 'C:\Users\user\Generated.psd1'
# Cmdlets are created based on the following heuristics
# New-<EntityType> -<Key> [-<Other Attributes>]
#
# Get-<EntityType> [-<Key> -Top –Skip –Filter -OrderBy]
# # If there is a complex key, the keys will actually be -<Key1> -<Key2>…
# # Note this rule applies to any other instances of the key
#
# Set-<EntityType> -<Key> [-<Other Attributes>]
#
# Remove-<EntityType> -<Key>
#
# Invoke-<EntityType><Action> [-<Key> -<Other Parameters>]
#
#
# Cmdlets from associations (Note: Get and Remove get additional parameter sets)
# Get-<EntityType> -<AssociatedEntity>
# New-<EntityType> -<AssociatedEntity> -<Key>
# Remove-<EntityType> -<AssociatedEntity> -<Key>
#
#
# Note: Every cmdlet has the –ConnectionURI parameter for explicitly setting the URI of the endpoint. This normally uses the same address that you gave the Export-ODataEndpointProxy cmdlet, but can be overridden in this fashion for the sake of similar endpoints.
#
```

<span data-ttu-id="87181-107">Stále existují částí případů použití klíče v vývoj pro tuto funkci, včetně, mimo jiné:</span><span class="sxs-lookup"><span data-stu-id="87181-107">There are still parts of key use cases in development for this functionality, including, but not limited to:</span></span>
-   <span data-ttu-id="87181-108">Přidružení</span><span class="sxs-lookup"><span data-stu-id="87181-108">Associations</span></span>
-   <span data-ttu-id="87181-109">Předávání datové proudy</span><span class="sxs-lookup"><span data-stu-id="87181-109">Passing streams</span></span>

<a name="generate-windows-powershell-cmdlets-based-on-an-odata-endpoint-with-odatautils"></a><span data-ttu-id="87181-110">Generovat založené na koncový bod OData s ODataUtils rutiny prostředí Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="87181-110">Generate Windows PowerShell cmdlets based on an OData endpoint with ODataUtils</span></span>
------------------------------------------------------------------------------
<span data-ttu-id="87181-111">Modul ODataUtils umožňuje generování rutin prostředí Windows PowerShell z koncové body REST, které podporují OData.</span><span class="sxs-lookup"><span data-stu-id="87181-111">The ODataUtils module allows generation of Windows PowerShell cmdlets from REST endpoints that support OData.</span></span> <span data-ttu-id="87181-112">V modulu Microsoft.PowerShell.ODataUtils Windows PowerShell jsou následující Přírůstkové vylepšení.</span><span class="sxs-lookup"><span data-stu-id="87181-112">The following incremental enhancements are in the Microsoft.PowerShell.ODataUtils Windows PowerShell module.</span></span>
-   <span data-ttu-id="87181-113">Další informace o kanálu z koncového bodu na straně serveru na straně klienta.</span><span class="sxs-lookup"><span data-stu-id="87181-113">Channel additional information from server-side endpoint to client side.</span></span>
-   <span data-ttu-id="87181-114">Podporu stránkování straně klienta</span><span class="sxs-lookup"><span data-stu-id="87181-114">Client-side paging support</span></span>
-   <span data-ttu-id="87181-115">Filtrování na straně serveru pomocí parametru-výběru</span><span class="sxs-lookup"><span data-stu-id="87181-115">Server-side filtering by using the -Select parameter</span></span>
-   <span data-ttu-id="87181-116">Podpora pro webové žádosti hlavičky</span><span class="sxs-lookup"><span data-stu-id="87181-116">Support for web request headers</span></span>

<span data-ttu-id="87181-117">Rutiny služby proxy generované rutinu Export-ODataEndPointProxy poskytují další informace (není uvedeno v $metadata používá při generování proxy server na straně klienta) ze serveru koncový bod OData straně v datovém proudu informace (nového systému Windows Funkce prostředí PowerShell 5.0).</span><span class="sxs-lookup"><span data-stu-id="87181-117">The proxy cmdlets generated by the Export-ODataEndPointProxy cmdlet provide additional information (not mentioned in the $metadata used during the client-side proxy generation) from the server side OData endpoint on the Information stream (a new Windows PowerShell 5.0 feature).</span></span> <span data-ttu-id="87181-118">Tady je příklad toho, jak získat tyto informace.</span><span class="sxs-lookup"><span data-stu-id="87181-118">Here is an example of how to get that information.</span></span>
```powershell
Import-Module Microsoft.PowerShell.ODataUtils -Force
$generatedProxyModuleDir = Join-Path -Path $env:SystemDrive -ChildPath 'ODataDemoProxy'
$uri = "http://services.odata.org/V3/(S(fhleiief23wrm5a5nhf542q5))/OData/OData.svc/"
Export-ODataEndpointProxy -Uri $uri -OutputModule $generatedProxyModuleDir -Force -AllowUnSecureConnection -Verbose -AllowClobber
Import-Module $generatedProxyModuleDir -Force

# In the below command, we are retrieving top 1 product.
# By specifying -IncludeTotalResponseCount parameter,
# we are getting the total count of all the Product records
# available on the server side. This information
# is surfaced on the client side through the Information stream.
$product = Get-Product -Top 1 -AllowUnsecureConnection -AllowAdditionalData -IncludeTotalResponseCount -InformationVariable infoStream
# The Information stream contains the additional
# information sent from the server side.
$additionalInfo = $infoStream.GetEnumerator() | % MessageData
# 'Odata.Count' indicates the total product records
# available on the server side Odata endpoint.
$additionalInfo['odata.count']
```

<span data-ttu-id="87181-119">Záznamy můžete získat z na straně serveru v dávkách s využitím podpory stránkování straně klienta.</span><span class="sxs-lookup"><span data-stu-id="87181-119">You can get the records from the server side in batches by using client-side paging support.</span></span> <span data-ttu-id="87181-120">To je užitečné v případě velkého množství dat musí získat ze serveru přes síť.</span><span class="sxs-lookup"><span data-stu-id="87181-120">This is useful when you must get a large amount of data from the server over the network.</span></span>
```powershell
$skipCount = 0
$batchSize = 3
# Client-Side Paging Support: The records from the server side
# are retrieved in batches of $batchSize
while($skipCount -le $additionalInfo['odata.count'])
{
Get-Product -AllowUnsecureConnection -AllowAdditionalData -Top $batchSize -Skip $skipCount
$skipCount += $batchSize
}
```

<span data-ttu-id="87181-121">Rutiny vygenerovaný proxy server podporují – vyberte parametr, který můžete získat pouze vlastnosti záznamu, které klient musí použít jako filtr.</span><span class="sxs-lookup"><span data-stu-id="87181-121">The generated proxy cmdlets support the –Select parameter which you can use as a filter to receive only the record properties that the client needs.</span></span> <span data-ttu-id="87181-122">Tím se snižuje množství dat, která se přenáší přes síť, protože filtrování proběhne na straně serveru.</span><span class="sxs-lookup"><span data-stu-id="87181-122">This reduces the amount of data that is transferred over the network, because the filtering occurs on the server side.</span></span>
```powershell
# In the below example only the Name property of the
# Product record is retrieved from the server side.
Get-Product -Top 2 -AllowUnsecureConnection -AllowAdditionalData -Select Name
```

<span data-ttu-id="87181-123">Rutina Export-ODataEndpointProxy a rutiny služby proxy generované, teď podporují parametr hlavičky (zadejte hodnoty jako zatřiďovací tabulku), který můžete použít k kanálu žádné další informace, které je očekávaný koncový bod OData na straně serveru.</span><span class="sxs-lookup"><span data-stu-id="87181-123">The Export-ODataEndpointProxy cmdlet, and the proxy cmdlets generated by it, now support the Headers parameter (supply values as a hash table), which you can use to channel any additional information that is expected by the server-side OData endpoint.</span></span> <span data-ttu-id="87181-124">V následujícím příkladu můžete kanálu klíč předplatného prostřednictvím hlavičky pro služby, které se očekává klíč předplatného pro ověřování.</span><span class="sxs-lookup"><span data-stu-id="87181-124">In the following example, you can channel a Subscription key through Headers for services that are expecting a Subscription key for authentication.</span></span>
```powershell
# As an example, in the below command 'XXXX' is the authentication used by the
# Export-ODataEndpointProxy cmdlet to interact with the server-side
# OData endpoint accessed through $endPointUri.

Export-ODataEndpointProxy -Uri $endPointUri -OutputModule $generatedProxyModuleDir -Force -AllowUnSecureConnection -Verbose -Headers @{'subscription-key'='XXXX'}
```
