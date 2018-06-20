---
ms.date: 06/12/2017
keywords: wmf,powershell,setup
ms.openlocfilehash: 01d4989711c22db20431876c52740afb350caad0
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/17/2018
ms.locfileid: "34219544"
---
# <a name="generate-powershell-cmdlets-based-on-odata-endpoint"></a>Generování powershellových rutin na základě koncového bodu OData
<a name="generate-windows-powershell-cmdlets-based-on-an-odata-endpoint"></a>Generovat rutiny prostředí Windows PowerShell, které jsou založené na koncový bod OData
--------------------------------------------------------------

**Export-ODataEndpointProxy** je rutina, která generuje sadu rutin prostředí Windows PowerShell podle funkce vystavené dané koncový bod OData.

Následující příklad ukazuje, jak použít tuto novou rutinu:

\# Základní použití malá ODataEndpointProxy exportu

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

Stále existují částí případů použití klíče v vývoj pro tuto funkci, včetně, mimo jiné:
-   Přidružení
-   Předávání datové proudy

<a name="generate-windows-powershell-cmdlets-based-on-an-odata-endpoint-with-odatautils"></a>Generovat založené na koncový bod OData s ODataUtils rutiny prostředí Windows PowerShell
------------------------------------------------------------------------------
Modul ODataUtils umožňuje generování rutin prostředí Windows PowerShell z koncové body REST, které podporují OData. V modulu Microsoft.PowerShell.ODataUtils Windows PowerShell jsou následující Přírůstkové vylepšení.
-   Další informace o kanálu z koncového bodu na straně serveru na straně klienta.
-   Podporu stránkování straně klienta
-   Filtrování na straně serveru pomocí parametru-výběru
-   Podpora pro webové žádosti hlavičky

Rutiny služby proxy generované rutinu Export-ODataEndPointProxy poskytují další informace (není uvedeno v $metadata používá při generování proxy server na straně klienta) ze serveru koncový bod OData straně v datovém proudu informace (nového systému Windows Funkce prostředí PowerShell 5.0). Tady je příklad toho, jak získat tyto informace.
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

Záznamy můžete získat z na straně serveru v dávkách s využitím podpory stránkování straně klienta. To je užitečné v případě velkého množství dat musí získat ze serveru přes síť.
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

Rutiny vygenerovaný proxy server podporují – vyberte parametr, který můžete získat pouze vlastnosti záznamu, které klient musí použít jako filtr. Tím se snižuje množství dat, která se přenáší přes síť, protože filtrování proběhne na straně serveru.
```powershell
# In the below example only the Name property of the
# Product record is retrieved from the server side.
Get-Product -Top 2 -AllowUnsecureConnection -AllowAdditionalData -Select Name
```

Rutina Export-ODataEndpointProxy a rutiny služby proxy generované, teď podporují parametr hlavičky (zadejte hodnoty jako zatřiďovací tabulku), který můžete použít k kanálu žádné další informace, které je očekávaný koncový bod OData na straně serveru. V následujícím příkladu můžete kanálu klíč předplatného prostřednictvím hlavičky pro služby, které se očekává klíč předplatného pro ověřování.
```powershell
# As an example, in the below command 'XXXX' is the authentication used by the
# Export-ODataEndpointProxy cmdlet to interact with the server-side
# OData endpoint accessed through $endPointUri.

Export-ODataEndpointProxy -Uri $endPointUri -OutputModule $generatedProxyModuleDir -Force -AllowUnSecureConnection -Verbose -Headers @{'subscription-key'='XXXX'}
```
