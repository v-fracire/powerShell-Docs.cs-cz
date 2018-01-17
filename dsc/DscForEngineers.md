---
ms.date: 2017-10-13
ms.topic: conceptual
keywords: "DSC prostředí powershell, konfiguraci, instalační program"
title: "Přehled stavu konfigurace požadovaných pro rozhodují"
ms.openlocfilehash: ae545ead0718def44d5a17708d254b872691e1d3
ms.sourcegitcommit: a444406120e5af4e746cbbc0558fe89a7e78aef6
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 01/17/2018
---
# <a name="desired-state-configuration-overview-for-engineers"></a>Přehled stavu konfigurace požadovaných pro technici

Tento dokument je určený pro vývojáře a operace týmy pochopit výhody z prostředí PowerShell požadovaného stavu konfigurace (DSC).
Pro vyšší úroveň zobrazení hodnoty DSC poskytuje, najdete v tématu [potřeby přehled stavu konfigurace pro rozhodují](decisionMaker.md)

## <a name="benefits-of-desired-state-configuration"></a>Výhody Desired State Configuration

DSC existuje:

- Snížení složitosti skriptování v systému Windows
- Zvýšení rychlosti iterace

Koncept "průběžné nasazování" se stává stále důležitější.
Průběžné nasazování znamená schopnost nasadit často, potenciálně mnohokrát za den.
Účelem tato nasazení není něco opravit, ale něco publikovaly rychle získat.
Získáním nové funkce prostřednictvím vývoj do operace pro bezproblémové a spolehlivě jako možné snížit čas na hodnotu nové obchodní logiky.

Přesuňte směrem cloud computing znamená nasazení řešení, které využívá model "deklarativní" šablony, kde je deklarován jako text prostředí end stavu a je publikována ve službě modul nasazení.
Tento postup nasazení umožňuje rychlé změnu ve velkém měřítku, s odolnost proti selhání riziko, protože kdykoli nasazení lze konzistentně opakovat zaručit stavu pro koncové.
Vytvoření nástrojů a služeb, které podporují tento styl operací prostřednictvím automatizace je odpovědí na tyto změny.

DSC je platforma, která poskytuje deklarativní a idempotent (repeatable) nasazení, konfiguraci a shoda.
Platforma DSC umožňuje ujistěte, že součástí vašeho datového centra mají správnou konfiguraci, která zabraňuje chyby a brání selhání nákladná nasazení.
DSC podle konfigurace DSC považuje jako součást kódu aplikace, umožňuje průběžné nasazování.
Konfigurace DSC je třeba aktualizovat v rámci aplikace, zajistíte, že znalosti potřebné k nasazení aplikace je vždy aktuální a připravené k použití.

## <a name="i-have-powershell-why-do-i-need-desired-state-configuration"></a>"Mám prostředí PowerShell, proč je důležité konfigurace požadovaného stavu?"

Záměr samostatné konfigurace DSC, nebo "co chcete udělat", provedení, nebo "jak chcete provést."
To znamená, že logiku spouštění je obsažena v prostředky.
Uživatelé nemusí vědět, jak implementovat nebo nasazení funkce, pokud prostředek DSC této funkce je k dispozici.
To umožňuje uživatelům zaměřit se na strukturu jejich nasazení.

Jako příklad skriptů prostředí PowerShell by měl vypadat takto:
```powershell
# Create a share in Windows Server 8
New-SmbShare -Name MyShare -Path C:\Demo\Temp -FullAccess Alice -ReadAccess Bob
```
Tento skript je jednoduché, srozumitelné a přehledné.
Ale pokud se pokusíte vložení skriptu do produkčního prostředí, budete spouštět do několika problémy.
Co se stane, když, skript je spuštěn v řádku dvakrát?
Co se stane, když Bob dříve mají plný přístup ke sdílené složce?

Pro kompenzaci tyto problémy, bude vypadat blíže něco podobného jako "Skutečná" verze skriptu:
```powershell
# But actually creating a share in an idempotent way would be

$shareExists = $false
$smbShare = Get-SmbShare -Name $Name -ErrorAction SilentlyContinue
if($smbShare -ne $null)
{
    Write-Verbose -Message "Share with name $Name exists"
    $shareExists = $true
}

if ($shareExists -eq $false)
{
    Write-Verbose "Creating share $Name to ensure it is Present"
    New-SmbShare @psboundparameters
}
else
{
    # Need to call either Set-SmbShare or *ShareAccess cmdlets
    if ($psboundparameters.ContainsKey("ChangeAccess"))
    {
       #...etc, etc, etc
    }
}
```

Tento skript je složitější s dostatkem logiku a zpracování chyb.
Skript je složitější, protože se už oznamující, co chcete done, ale *jak to udělat*.

DSC umožňuje určit, co chcete done a logiku je abstrahované rychle.

```powershell
# A configuration is a special kind of PowerShell function
Configuration Sample_Share
{
   Import-DscResource -Module xSmbShare
   # Nodes are the endpoint we wish to configure
   # A Configuration block can have zero or more Node blocks
   Node $NodeName
   {
      # Next, specify one or more resource blocks
      # Resources are simply PowerShell modules that
      # implement the logic of "how" to execute a task
      xSmbShare MySMBShare
      {
          Ensure      = "Present"
          Name        = "MyShare"
          Path        = "C:\Demo\Temp"
          ReadAccess  = "Alice"
          FullAccess  = "Bob"
          Description = "This is an updated description for this share"
      }
   }
}
#Run the function to compile the configuration
Sample_Share
#Pass the configuration to the nodes we defined and configure them
Start-DscConfiguration Sample_Share
```

Tento skript je řádně formátovaný a přehledné ke čtení.
Se stále nachází na logické cesty a zpracování chyb [prostředků](resources.md) implementace, ale neviditelné autorovi skriptu.

## <a name="separating-environment-from-structure"></a>Oddělení prostředí z struktura

Běžné vzoru v DevOps je mít několik prostředí pro nasazení.
Například může být prostředí "dev" umožňuje rychle prototypu nový kód.
Kód z prostředí "dev" přejde do prostředí s "test", které jiní lidé ověřte nové funkce.
Nakonec kód přejde do stavu "produkčního" nebo živý web produkčního prostředí.

Konfigurace DSC zohlednit tento kanál dev-test produkčnímu prostřednictvím [konfigurační data](configData.md).
Tato další abstrahuje rozdíl mezi strukturu konfigurace z uzlů, které jsou spravovány.
Můžete například definovat konfigurace, která vyžaduje SQL server, server se službou IIS a server střední vrstvy.
Bez ohledu na to, jaké uzly zobrazí různé části této konfigurace bude mít tyto tři prvky vždy existuje.
Konfigurační data můžete použít tak, aby odkazoval na stejném počítači pro vývoj prostředí, samostatné tři prvky do tří různých počítačů pro testovací prostředí, všechny tři prvky a v neposlední řadě směrem všech provozních serverů pro produkčnímu prostředí.
Nasadit do různých prostředích, můžete vyvolat **Start-DscConfiguration** s daty správnou konfiguraci pro prostředí, který chcete cílit.

## <a name="see-also"></a>Viz také

[Konfigurace](configurations.md)

[Konfigurační Data](configData.md)

[Prostředky](resources.md)
