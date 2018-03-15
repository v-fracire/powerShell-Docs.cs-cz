---
ms.date: 2017-06-12
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "V nástroji Návrhář prostředků"
ms.openlocfilehash: c39b48f67d3874ee3cd2f2704aeb7390fa186fe4
ms.sourcegitcommit: 99227f62dcf827354770eb2c3e95c5cf6a3118b4
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 03/15/2018
---
# <a name="using-the-resource-designer-tool"></a>V nástroji Návrhář prostředků

> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

Nástroj Návrhář prostředků je sada rutin, které jsou zveřejněné **xDscResourceDesigner** modul, který usnadnění vytváření prostředků požadovaného stavu aplikace Windows PowerShell (DSC). Rutiny v tento prostředek pomoci vytvořit schéma MOF, modulu skriptu a strukturu adresáře pro nový prostředek. Další informace o prostředcích DSC najdete v tématu [sestavení vlastní Windows PowerShell požadovaného stavu konfigurace prostředků](authoringResource.md).
V tomto tématu vytvoříme prostředek DSC, která spravuje uživatelů služby Active Directory.
Použití [instalace modulu](https://technet.microsoft.com/library/dn807162.aspx) k instalaci **xDscResourceDesigner** modulu.

>**Poznámka:**: **instalace modulu** je součástí **PowerShellGet** modul, který je součástí prostředí PowerShell 5.0. Si můžete stáhnout **PowerShellGet** modul pro prostředí PowerShell 3.0 a 4.0 na [Preview moduly Powershellu PackageManagement](https://www.microsoft.com/en-us/download/details.aspx?id=49186).

## <a name="creating-resource-properties"></a>Vytvoření vlastností prostředku
První věc, kterou je potřeba udělat je, vyberte vlastnosti, které se zveřejňují prostředku. V tomto příkladu jsme bude definovat uživatele služby Active Directory s následujícími vlastnostmi.
 
Název parametru popis
* **Uživatelské jméno**: klíčové vlastnosti, která jednoznačně identifikuje uživatele.
* **Ujistěte se,**: Určuje, zda uživatelský účet, musí být přítomen nebo chybí. Tento parametr bude obsahovat pouze dvě možné hodnoty.
* **DomainCredential**: heslo domény pro uživatele.
* **Heslo**: požadované heslo pro uživatele pro povolení konfiguraci, kterou chcete změnit heslo uživatele v případě potřeby.

Pokud chcete vytvořit vlastnosti, používáme **New-xDscResourceProperty** rutiny. Následující příkazy prostředí PowerShell vytvořit pomocí vlastností popsaných výše.

```powershell
$UserName = New-xDscResourceProperty –Name UserName -Type String -Attribute Key
$Ensure = New-xDscResourceProperty –Name Ensure -Type String -Attribute Write –ValidateSet “Present”, “Absent”
$DomainCredential = New-xDscResourceProperty –Name DomainCredential-Type PSCredential -Attribute Write
$Password = New-xDscResourceProperty –Name Password -Type PSCredential -Attribute Write
```

## <a name="create-the-resource"></a>Vytvořit prostředek

Teď, když byly vytvořeny vlastnosti prostředku, jsme volání **New-xDscResource** vytvořte prostředek. **New-xDscResource** rutiny přebírá seznam vlastností, jako parametry. Také trvá cestu, kde by se měl vytvořit modul, název nového prostředku a název modulu, ve kterém se nachází. Následující příkaz prostředí PowerShell vytvoří prostředek.

```powershell
New-xDscResource –Name Demo_ADUser –Property $UserName, $Ensure, $DomainCredential, $Password –Path ‘C:\Program Files\WindowsPowerShell\Modules’ –ModuleName Demo_DSCModule
```

**New-xDscResource** rutina vytvoří schéma MOF, skript kostru prostředků, strukturu požadované adresáře pro nový prostředek a manifestu pro modul, který zveřejňuje nový prostředek.

Schéma soubor MOF, který je na **C:\Program Files\WindowsPowerShell\Modules\Demo_DSCModule\DSCResources\Demo_ADUser\Demo_ADUser.schema.mof**, a jeho obsah následujícím způsobem.

```
[ClassVersion("1.0.0.0"), FriendlyName("Demo_ADUser")]
class Demo_ADUser : OMI_BaseResource
{
  [Key] string UserName;
  [Write, ValueMap{"Present","Absent"}, Values{"Present","Absent"}] string Ensure;
  [Write, EmbeddedInstance("MSFT_Credential")] String DomainCredential;
  [Write, EmbeddedInstance("MSFT_Credential")] String Password;
};
```

Je skript prostředků v **C:\Program Files\WindowsPowerShell\Modules\Demo_DSCModule\DSCResources\Demo_ADUser\Demo_ADUser.psm1**. Neobsahuje skutečné logiku pro provádění prostředku, který je nutné přidat sami. Obsah kostru skriptu jsou následujícím způsobem.

```powershell
function Get-TargetResource
{
  [CmdletBinding()]
  [OutputType([System.Collections.Hashtable])]
  param
  (
    [parameter(Mandatory = $true)]
    [System.String]
    $UserName
  )

  #Write-Verbose "Use this cmdlet to deliver information about command processing."

  #Write-Debug "Use this cmdlet to write debug information while troubleshooting."


  <#
  $returnValue = @{
  UserName = [System.String]
  Ensure = [System.String]
  DomainAdminCredential = [System.Management.Automation.PSCredential]
  Password = [System.Management.Automation.PSCredential]
  }

  $returnValue
  #>
}


function Set-TargetResource
{
  [CmdletBinding()]
  param
  (
    [parameter(Mandatory = $true)]
    [System.String]
    $UserName,

    [ValidateSet("Present","Absent")]
    [System.String]
    $Ensure,

    [System.Management.Automation.PSCredential]
    $DomainAdminCredential,

    [System.Management.Automation.PSCredential]
    $Password
  )

  #Write-Verbose "Use this cmdlet to deliver information about command processing."

  #Write-Debug "Use this cmdlet to write debug information while troubleshooting."

  #Include this line if the resource requires a system reboot.
  #$global:DSCMachineStatus = 1


}


function Test-TargetResource
{
  [CmdletBinding()]
  [OutputType([System.Boolean])]
  param
  (
    [parameter(Mandatory = $true)]
    [System.String]
    $UserName,

    [ValidateSet("Present","Absent")]
    [System.String]
    $Ensure,

    [System.Management.Automation.PSCredential]
    $DomainAdminCredential,

    [System.Management.Automation.PSCredential]
    $Password
  )

  #Write-Verbose "Use this cmdlet to deliver information about command processing."

  #Write-Debug "Use this cmdlet to write debug information while troubleshooting."


  <#
  $result = [System.Boolean]

  $result
  #>
}


Export-ModuleMember -Function *-TargetResource
```

## <a name="updating-the-resource"></a>Aktualizuje prostředek

Pokud potřebujete přidat nebo upravit seznam parametrů prostředku, můžete zavolat **aktualizace xDscResource** rutiny. Rutina aktualizuje prostředek nový seznam parametrů. Pokud jste již přidali logiku ve vašem skriptu prostředků, je ponechán beze změny.

Například předpokládejme, že chcete zahrnout poslední protokolu v čase pro uživatele v našem prostředku. Místo psaní znovu zcela prostředek, můžete volat **New-xDscResourceProperty** k vytvoření nové vlastnosti a pak zavolají **aktualizace xDscResource** a přidejte do vaší nové vlastnosti seznam vlastností.

```powershell
$lastLogon = New-xDscResourceProperty –Name LastLogon –Type Hashtable –Attribute Write –Description “For mapping users to their last log on time”
Update-xDscResource –Name ‘Demo_ADUser’ –Property $UserName, $Ensure, $DomainCredential, $Password, $lastLogon -Force
```

## <a name="testing-a-resource-schema"></a>Testování schéma prostředků

Nástroj Návrhář prostředků zpřístupní jeden další rutiny, která můžete použít k testování platnosti schématu MOF, který jste napsali ručně. Volání **Test xDscSchema** předávání cestu schéma MOF prostředků jako parametr rutiny. Rutina výstup všechny chyby ve schématu.

### <a name="see-also"></a>Viz také

#### <a name="concepts"></a>Koncepty
[Sestavení vlastní Windows PowerShell Desired State Configuration prostředky](authoringResource.md)

#### <a name="other-resources"></a>Další prostředky
[xDscResourceDesigner modulu](https://powershellgallery.com/packages/xDscResourceDesigner)