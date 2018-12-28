---
ms.date: 06/12/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Pomocí nástroje Návrhář prostředků
ms.openlocfilehash: 3fd2f06cf46602ee30dd34f8e7bd77d3c92b808f
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403722"
---
# <a name="using-the-resource-designer-tool"></a>Pomocí nástroje Návrhář prostředků

> Platí pro: Prostředí Windows PowerShell 4.0, prostředí Windows PowerShell 5.0

Nástroj Návrhář prostředků je sada rutin, které jsou vystavené **xDscResourceDesigner** modul, který usnadnit vytváření prostředků Windows PowerShell Desired State Configuration (DSC). Rutiny v tomto prostředku pomoci vytvořit schéma MOF, modul skriptu a strukturu adresářů pro nový prostředek. Další informace o prostředcích DSC najdete v tématu [vytvářet vlastní Windows PowerShell Desired State Configuration prostředky](authoringResource.md).
V tomto tématu vytvoříme prostředek DSC, který slouží ke správě uživatelů služby Active Directory.
Použití [Install-Module](/powershell/module/PowershellGet/Install-Module) rutinu instalace **xDscResourceDesigner** modulu.

>**Poznámka:**: **Install-Module** je součástí **PowerShellGet** modulu, která je obsažena v Powershellu 5.0. Můžete stáhnout **PowerShellGet** modulu pro PowerShell 3.0 a 4.0 na [Preview moduly Powershellu PackageManagement](https://www.microsoft.com/en-us/download/details.aspx?id=49186).

## <a name="creating-resource-properties"></a>Vytvoření vlastností prostředku
První věc, kterou budeme muset udělat se při rozhodování o vlastnosti, které odhalují prostředku. V tomto příkladu jsme budou definovat uživatele služby Active Directory s následujícími vlastnostmi.

Název parametru popis
* **Uživatelské jméno**: Klíčová vlastnost, která jednoznačně identifikuje uživatele.
* **Zajištění**: Určuje, zda by měl být uživatelský účet k dispozici nebo chybí. Tento parametr budou mít pouze dva možné hodnoty.
* **DomainCredential**: Heslo domény pro daného uživatele.
* **Heslo**: Požadované heslo pro uživatele povolit konfiguraci, kterou chcete změnit heslo uživatele v případě potřeby.

K vytvoření vlastnosti, použijeme **New-xDscResourceProperty** rutiny. Následující příkazy prostředí PowerShell vytvoří vlastností popsaných výše.

```powershell
$UserName = New-xDscResourceProperty –Name UserName -Type String -Attribute Key
$Ensure = New-xDscResourceProperty –Name Ensure -Type String -Attribute Write –ValidateSet “Present”, “Absent”
$DomainCredential = New-xDscResourceProperty –Name DomainCredential -Type PSCredential -Attribute Write
$Password = New-xDscResourceProperty –Name Password -Type PSCredential -Attribute Write
```

## <a name="create-the-resource"></a>Vytvoření prostředku

Teď, když byly vytvořeny vlastnosti prostředku, budeme volat **New-xDscResource** rutina pro vytvoření prostředku. **New-xDscResource** rutiny přebírá seznam vlastností, které jako parametry. Přijímá také cestu, kde by měl být vytvořen modulu, název nového prostředku a název modulu, ve kterém je obsažená. Následující příkaz Powershellu vytvoří prostředek.

```powershell
New-xDscResource –Name Demo_ADUser –Property $UserName, $Ensure, $DomainCredential, $Password –Path ‘C:\Program Files\WindowsPowerShell\Modules’ –ModuleName Demo_DSCModule
```

**New-xDscResource** rutina vytvoří schéma MOF, skript kostru prostředků, vyžaduje adresářovou strukturu pro nový prostředek a manifest pro modul, který zpřístupňuje nový prostředek.

Je v schématu soubor MOF **C:\Program Files\WindowsPowerShell\Modules\Demo_DSCModule\DSCResources\Demo_ADUser\Demo_ADUser.schema.mof**, a jeho obsah následujícím způsobem.

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

Skript prostředků je na **C:\Program Files\WindowsPowerShell\Modules\Demo_DSCModule\DSCResources\Demo_ADUser\Demo_ADUser.psm1**. Nezahrnuje skutečné logiku pro implementaci prostředku, který je nutné přidat sami. Obsah kostru skriptu jsou následující.

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

## <a name="updating-the-resource"></a>Aktualizuje se prostředek

Pokud potřebujete přidat nebo upravit seznam parametrů prostředku, můžete volat **aktualizace xDscResource** rutiny. Rutina aktualizace prostředku se nový seznam parametrů. Pokud jste už přidali logiky ve vašem skriptu prostředků, je ponechán beze změny.

Předpokládejme například, že chcete poslední protokolu zahrnout v čase pro uživatele v naší prostředku. Místo psaní znovu zcela prostředek, můžete volat **New-xDscResourceProperty** vytvořit novou vlastnost a poté zavolejte **aktualizace xDscResource** a přidat nové vlastnosti do seznam vlastností.

```powershell
$lastLogon = New-xDscResourceProperty –Name LastLogon –Type Hashtable –Attribute Write –Description “For mapping users to their last log on time”
Update-xDscResource –Name ‘Demo_ADUser’ –Property $UserName, $Ensure, $DomainCredential, $Password, $lastLogon -Force
```

## <a name="testing-a-resource-schema"></a>Testování schématu zdroje

Nástroj Návrhář prostředků zpřístupňuje jeden další rutiny, které můžete použít k testování platnosti schématu MOF, který jste napsali ručně. Volání **testovací xDscSchema** předáním cesty prostředku schématu MOF jako parametr rutiny. Rutina vydá všechny chyby ve schématu.

### <a name="see-also"></a>Viz také

#### <a name="concepts"></a>Koncepty
[Vlastní Windows PowerShell Desired State Configuration prostředky sestavení](authoringResource.md)

#### <a name="other-resources"></a>Další prostředky
[xDscResourceDesigner modulu](https://www.powershellgallery.com/packages/xDscResourceDesigner/1.12.0.0)
