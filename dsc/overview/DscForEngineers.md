---
ms.date: 10/13/2017
keywords: DSC, powershell, konfigurace, instalační program
title: Přehled platformy Desired State Configuration pro techniky
ms.openlocfilehash: 0e599c2218cd2df29dbd0529006be5e1ef17ce5f
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53403864"
---
# <a name="desired-state-configuration-overview-for-engineers"></a>Přehled platformy Desired State Configuration pro techniky

Tento dokument je určený pro vývojáře provozní týmy a týmy pochopíte výhody z prostředí PowerShell Desired State Configuration (DSC).
Pro vyšší úroveň zobrazení hodnoty DSC poskytuje, najdete [Desired State Configuration přehled pro pracovníky s rozhodovací pravomocí](decisionMaker.md)

## <a name="benefits-of-desired-state-configuration"></a>Výhody Desired State Configuration

DSC neexistuje:

- Zjednodušte skriptování ve Windows
- Zvýšení rychlosti iterace

Pojem "průběžné nasazování" je stále důležitější.
Průběžné nasazování znamená možnost nasazení často, potenciálně mnohokrát za den.
Účelem těchto nasazeních není nějakou opravu, ale něco publikovaly rychle získat.
Získávání nových funkcí prostřednictvím vývoje do operace bezproblémovému a spolehlivě, jako je to možné, můžete snížit dobu realizace nové obchodní logiky.

Přesunout na cloud computingu implikuje nasazení řešení, které využívá model "deklarativní" šablony, kde je koncový stav prostředí deklarované jako text a publikují do modulu nasazení.
Tento postup nasazení umožňuje rychlé změny ve velkém měřítku, s odolnost proti selhání hrozeb vzhledem k tomu, že v okamžiku nasazení můžete konzistentně opakovat zajistit koncového stavu.
Vytvoření nástrojů a služeb, které podporují tento styl operace, ať už automation je odpovědí na tyto změny.

DSC je platforma, která poskytuje deklarativní a nasazení (opakovatelné) idempotentní, konfigurace a přizpůsobení.
Platforma DSC umožňuje součástí vašeho datového centra zajistit správnou konfiguraci, která zabraňuje chybám a zabraňuje chybám při nasazování nákladné.
DSC podle konfigurace DSC se zpracuje jako část kódu aplikace, umožňuje průběžné nasazování.
Konfigurace DSC se musí aktualizovat jako součást aplikace zajišťující, že znalosti potřebné k nasazení aplikace je vždy aktuální a připravená k použití.

## <a name="i-have-powershell-why-do-i-need-desired-state-configuration"></a>"Mám prostředí PowerShell, proč je nutné Desired State Configuration?"

Záměr samostatné konfigurace DSC nebo "co chci provést", spuštění nebo "jak chci udělat."
To znamená, že logika zpracování je obsažen v prostředcích.
Uživatelé nebudou mít k určení, jak implementovat nebo nasadit funkci, když prostředek DSC této funkce je k dispozici.
To mu umožní se zaměřují na strukturu jejich nasazení.

Jako příklad skripty prostředí PowerShell by měl vypadat takto:
```powershell
# Create a share in Windows Server 8
New-SmbShare -Name MyShare -Path C:\Demo\Temp -FullAccess Alice -ReadAccess Bob
```
Tento skript je jednoduché, srozumitelné a jednoduché.
Ale pokud se pokusíte vložení tohoto skriptu do produkčního prostředí, budete spouštět na několik problémů.
Co se stane, když spuštění dvakrát za sebou skriptu?
Co se stane, pokud Bob dříve měli úplný přístup ke sdílené složce?

Jako kompenzaci za tyto problémy, bude vypadat blíž ke něco jako "real" verze skriptu:
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

Tento skript je složitější, s spoustu logiky a zpracování chyb.
Skript je složitější, protože jsou již uvedením, co chcete Hotovo, ale *jak na to*.

DSC umožňuje určit, co chcete Hotovo a logiku je abstrahovaný okamžitě.

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
          ReadAccess  = "Bob"
          FullAccess  = "Alice"
          Description = "This is an updated description for this share"
      }
   }
}
#Run the function to compile the configuration
Sample_Share
#Pass the configuration to the nodes we defined and configure them
Start-DscConfiguration Sample_Share
```

Tento skript je čistě naformátovaný a je jednoduché ke čtení.
Jsou stále k dispozici v logické cesty a zpracování chyb [prostředků](../resources/resources.md) implementaci, ale neviditelné autorovi skriptu.

## <a name="separating-environment-from-structure"></a>Oddělení prostředí ze struktury

Běžným vzorem v DevOps je, aby více prostředí pro nasazení.
Například může být "dev" prostředí umožňuje rychle prototypu nový kód.
Kódu z prostředí "dev" přejde do prostředí "test", kde jiní lidé ověřte nové funkce.
Nakonec kód přejde do stavu "produkční" nebo produkčním prostředí živého webu.

Konfigurace DSC podle tohoto kanálu dev-test-prod prostřednictvím [konfigurační data](../configurations/configData.md).
To dále abstrahuje rozdíl mezi struktura konfiguraci z uzlů, které se spravují.
Můžete například definovat konfiguraci, která vyžaduje SQL server, server služby IIS a server střední vrstvy.
Bez ohledu na to, jaké uzly zobrazí různé části této konfigurace tyto tři prvky bude k dispozici vždy.
Konfigurační data můžete použít tak, aby odkazoval všechny tři prvky na stejném počítači pro vývoj prostředí, samostatné tři prvky do tří různých počítačů pro testovací prostředí a nakonec na všech provozních serverech pro produkční prostředí.
Pokud chcete nasadit do různých prostředí, můžete vyvolat **Start-DscConfiguration** správnou konfiguraci dat pro prostředí, kterou chcete cílit.

## <a name="see-also"></a>Viz také

[Konfigurace](../configurations/configurations.md)

[Konfigurační Data](../configurations/configData.md)

[Prostředky](../resources/resources.md)
