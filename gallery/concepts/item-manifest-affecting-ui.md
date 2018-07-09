---
ms.date: 06/09/2017
schema: 2.0.0
keywords: prostředí PowerShell
title: Manifestu hodnoty položek, které mají vliv uživatelské rozhraní Galerie prostředí PowerShell
ms.openlocfilehash: fd5e48f8cc36795742ae597fc7715f7377605b6f
ms.sourcegitcommit: 8b076ebde7ef971d7465bab834a3c2a32471ef6f
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 07/06/2018
ms.locfileid: "37893473"
---
# <a name="item-manifest-values-that-impact-the-powershell-gallery-ui"></a>Manifestu hodnoty položek, které mají vliv uživatelské rozhraní Galerie prostředí PowerShell

Toto téma poskytuje vydavatelům se souhrnnými informacemi o tom, jak upravit manifest pro jejich publikací Galerie prostředí PowerShell tak, aby funkce rutiny Správce balíčků PowerShellGet a uživatelské rozhraní Galerie prostředí PowerShell bude mít vliv.
Tento obsah je uspořádaný podle změnu umístění, od verze v části System center a v navigační oblasti na levé straně. Je v těle pokrývající značky, který identifikuje důležité značky, stejně jako některé z více běžně používá značky.
Existují dvě témata, které poskytují manifestu příklady:

- Moduly, naleznete v tématu [aktualizace manifestu modulu](/powershell/module/powershellget/Update-ModuleManifest)
- U skriptů, najdete v článku [vytvoření souboru skriptu s metadaty](/powershell/module/powershellget/New-ScriptFileInfo)

## <a name="powershell-gallery-feature-elements-controlled-by-the-manifest"></a>Řídí Manifest elementy funkce Galerie prostředí PowerShell

Následující tabulka ukazuje prvky na stránce Galerie prostředí PowerShell položka uživatelského rozhraní, které jsou řízené vydavatele.
Každá položka signalizuje, pokud mohou být řízena v manifestu modulu nebo skriptu.

| Prvek uživatelského rozhraní | Popis | Modul | Skript |
| --- | --- | --- | --- |
| **Název** | Toto je název položky, která je publikována do Galerie  | Ne | Ne |
| **Verze** | Zobrazí verze je verze řetězce v metadatech a předběžná Pokud je zadán. Primární část verze v manifestu modulu je verze modulu. Pro skript je identifikovaný jako. VERZE. Pokud je zadaný řetězec předběžnou verzi, bude připojeno k ModuleVersion pro moduly, nebo zadaná jako součást. VERZE pro skripty. Je dokumentace ke službě pro zadání předběžné verze řetězce v [moduly](/powershell/gallery/concepts/module-prerelease-support)a v [skriptů](/powershell/gallery/concepts/script-prerelease-support) | Ano | Ano |
| **Popis** | Toto je popis v manifestu modulu a v souboru manifestu skriptu je. POPIS | Ano | Ano |
| **Vyžadování přijetí licence** | Modul může vyžadovat, aby uživatel přijměte licenci, úpravou manifestu modulu s RequireLicenseAcceptance = $true, zadávání LicenseURI a poskytnutí souboru license.txt v kořenové složce modulu. Další informace najdete v [vyžadovat přijetí licence](/powershell/gallery/how-to/working-with-items/items-that-require-license-acceptance) tématu. | Ano | Ne |
| **Poznámky k verzi** | Pro moduly tyto informace přenesou z ReleaseNotes části PSData\PrivateData. V manifestech skriptu, je. RELEASENOTES element. | Ano | Ano |
| **Vlastníci** | Vlastníci jsou seznam uživatelů v galerii prostředí PowerShell, který může aktualizovat položku. Manifest položky není součástí seznamu vlastníků. Další dokumentace popisuje jak [Správa vlastníků položek](/powershell/gallery/how-to/publishing-items/managing-item-owners). | Ne | Ne |
| **Autor** | To je součástí manifestu modulu jako autor a v manifestu jako skript. AUTOR. Autor pole se často používá k určení společnost nebo organizace, které jsou přidružené položce. | Ano | Ano |
| **Copyright** | Toto je pole Copyright v manifestu modulu a. COPYRIGHT v manifestu skriptu. | Ano | Ano |
| **FileList** | Seznam souborů pochází z balíčku, když se publikuje v galerii prostředí PowerShell. Není může ovládat informace o manifestu. Poznámka: k dispozici je další souboru .nuspec soubor s každou položku v galerii prostředí PowerShell, který není k dispozici po instalaci položky v systému. Toto je manifest balíčku Nuget pro položku a mohou být ignorovány. | Ne | Ne |
| **Značky** | Pro moduly zahrnují PSData\PrivateData značky. Pro skripty je označené části. ZNAČKY. Všimněte si, že značky nemůžou obsahovat mezery, i když se nachází v uvozovkách. Značky mají další požadavky a významy, které jsou popsány dále v tomto tématu v části Podrobnosti o značce. | Ano | Ano |
| **Rutiny** | To je k dispozici v manifestu modulu pomocí CmdletsToExport. Všimněte si, že osvědčeným postupem je explicitně seznam položek, spíš než zástupný znak "*", jak, která zlepší výkon modulu zatížení pro uživatele. | Ano | Ne |
| **Funkce** | To je k dispozici v manifestu modulu pomocí FunctionsToExport. Všimněte si, že osvědčeným postupem je explicitně seznam položek, spíš než zástupný znak "*", jak, která zlepší výkon modulu zatížení pro uživatele. | Ano | Ne |
| **Prostředky DSC** | Pro moduly, které se použije na prostředí PowerShell verze 5.0 a vyšším to je součástí manifestu pomocí DscResourcesToExport. Pokud je modul pro použití v prostředí PowerShell 4, DSCResourcesToExport se nemá používat není podporované klíč manifestu. (DSC nebyla k dispozici před Powershellu 4.) | Ano | Ne |
| **Pracovní postupy** | Pracovní postupy jsou publikované v galerii prostředí PowerShell jako skripty a identifikovány jako pracovní postupy (viz [Connect-AzureVM](https://www.powershellgallery.com/packages/Connect-AzureVM/1.0/Content/Connect-AzureVM.ps1) příklad) v kódu. To není řízen manifest. | Ne | Ne |
| **Funkce rolí** | To se zobrazí, když modul publikována do Galerie prostředí PowerShell obsahuje jeden nebo více rolí možnost (.psrc) soubory, které jsou používány JEA. Naleznete v dokumentaci JEA podrobnější [funkce rolí](https://docs.microsoft.com/en-us/powershell/jea/role-capabilities). | Ano | Ne |
| **Edice Powershellu** | To je určeno v manifestu skriptu nebo modulu. Pro moduly, které se používá v Powershellu 5.0 a starších se to je řízen pomocí značek. Pro stolní počítače použijte značku PSEdition_Desktop a jádro, použijte značku PSEdition_Core. Pro moduly, které se použijí jenom v prostředí PowerShell 5.1 a vyšší verzí existuje hlavní manifestu CompatiblePSEditions klíč. Další podrobnosti najdete v tématu funkci PS Edition v [dokumentaci Powershellu Get](/powershell/gallery/concepts/module-psedition-support). | Ano | Ano |
| **Závislosti** | Závislosti jsou moduly v galerii prostředí PowerShell, které jsou deklarovány v modulu jako RequiredModules nebo v manifestu skript jako #Requires – modul (název). | Ano | Ano |
| **Minimální verze prostředí Powershell** | Můžete zadat v manifestu modulu jako verze prostředí PowerShell | Ano | Ne |
| **Historie verzí** | Historie verzí odráží aktualizace provedené v modulu v galerii prostředí PowerShell. Pokud verze položky, skrytá pomocí funkce odstranění se nebude zobrazovat v historii verzí s výjimkou pro vlastníky položky. | Ne | Ne |
| **Web projektu** | Web projektu se poskytuje pro moduly v části Privatedata\PSData manifestu modulu zadáním ProjectURI. V manifestu skriptu je řídit určením. PROJECTURI. | Ano | Ano |
| **Licence** | Licence je k dispozici odkaz pro moduly v části Privatedata\PSData manifestu modulu zadáním LicenseURI. V manifestu skriptu je řídit určením. LICENSEURI. Je důležité si uvědomit, že pokud není k dispozici licenci prostřednictvím LicenseURI nebo v rámci modulu, pak podmínky použití pro galerii prostředí PowerShell zadejte podmínky použití pro položku. Přečíst podmínky použití pro podrobnosti. | Ano | Ano |

## <a name="editing-item-details"></a>Úpravy podrobností položky

Na stránce Galerie prostředí PowerShell upravit položka umožňuje vydavatelům změnit několik polí zobrazených pro některou položku, konkrétně:

- Title
- Popis
- Souhrn
- Adresa URL ikony
- Adresa URL domovské stránky projektu
- Autoři
- Copyright
- Značky
- Poznámky k verzi
- Vyžadují licenci

Tento přístup není doporučen obecně, s výjimkou při potřebný k opravě, co se zobrazí pro starší verzi modulu.
Uživatelé, kteří získají modulu se zobrazí, že metadata se neshoduje s co se zobrazí v galerii prostředí PowerShell, který vyvolává otázky o položce.
Výsledkem bude často dotazy, přejděte na vlastníky položky pro potvrzení změny.
Důrazně doporučujeme, aby pokaždé, když se používá tento přístup, nová verze položky by se měly zveřejňovat stejnými změnami.

## <a name="tag-details"></a>Podrobnosti o značce

Značky jsou jednoduché řetězce příjemci použijte k vyhledání položek.
Značky jsou nejužitečnější, pokud jsou používány konzistentně napříč mnoha položky související s ke stejnému tématu. Použití více charakterů stejného slovo (například databáze a databáze, nebo testování a testování) obvykle poskytuje málo výhodné.
Značky jsou řetězce jednoslovnou velkých a malých písmen a nesmí obsahovat prázdné hodnoty. Pokud frázi, které si myslíte, že bude hledat uživatele, přidejte ho do popis položky a bude nalezen ve výsledcích hledání. Pokud se pokoušíte, aby se zlepšila čitelnost pomocí malých a velkých písmen Pascal, spojovník, podtržítkem nebo pomlčkou. Buďte opatrní vytváření značky dlouhý, komplexní a neobvyklé, jako jsou často překlep.

Značky, které jsou důležité si uvědomit, jako galerie prostředí PowerShell a Správce balíčků PowerShellGet rutiny s nimi zacházet jedinečným způsobem. PSEdition_Desktop PSEdition_Core jsou konkrétní příklady a jsou popsané výše.

Jak bylo uvedeno výše, značky poskytují větší hodnotu, pokud jsou určené a používá konzistentně napříč mnoho položek.
Jako vydavatel pokusu o nalezení Nejlepší značky používat je nejjednodušší způsob hledání v galerii prostředí PowerShell pro značky, které uvažujete.
V ideálním případě bude existovat mnoho položek vrácených a popisy pro položky zarovná s vaším používáním této klíčové slovo.

Pro referenci Zde jsou některé běžně používané značky k 12/14/2017.
V některých případech jsou podobné, ale možná méně ideální možností uvedených vedle značky.
Je osvědčeným postupem použít značku upřednostňované jako, který bude mít za následek méně rušivé a lepší výsledky hledání pro zákazníky.

| **Upřednostňované značky** | **Náhradní řešení a poznámky** |
| --- | --- |
| **Azure** |  |
| **DSC** | DesiredStateConfiguration je méně vhodné, je příliš dlouhý |
| **Správce prostředků** | Slouží k popisu skupiny procesory ARM a neměl by se používat pro Azure Resource Manageru | **DSCResourceKit** |  |
| **SQL** |  |
| **AWS** |  |
| **DSCResource** |  |
| **Automatizace** |  |
| **REST** |  |
| **Active Directory** | AD se aktuálně nepoužívá samostatně  |
| **SQLServer** |  |
| **DBA** |  |
| **Zabezpečení** | Obrana je méně přesné |
| **Databáze** | Je méně vhodné databáze (množné číslo) |
| **DevOps** |  |
| **Windows** |  |
| **Sestavení** |  |
| **Nasazení** | Nasazení se používá méně často |
| **Cloud** |  |
| **GIT** |  |
| **Test** | Testování je méně vhodné |
| **VersionControl** | Verze je méně přesné, i když se často používá  |
| **Protokolování** | Upřednostňované použití protokolování jako akci |
| **Protokol** | Upřednostňované použití protokolu jako objekt |
| **Zálohování** |  |
| **IaaS** |  |
| **Linux** |  |
| **SLUŽBA IIS** |  |
| **AzureAutomation** |  |
| **Úložiště** |  |
| **GitHub** |  |
| **JSON** |  |
| **Exchange** |  |
| **Sítě** | Sítě je podobné, méně často používají |
| **SharePoint** |  |
| **Vytváření sestav** | Vytváření sestav je akce, sestava je to |
| **Sestavy** | To je sestava |
| **WinRM** |  |
| **Monitorování** |  |
| **VSTS** |  |
| **Excel** |  |
| **Google** |  |
| **Barva** |  |
| **DNS** |  |
| **Office365** | Hláskování Office je vhodnější. O365 je méně často používány, i když je kratší | **Gitlab** |  |
| **Pester** |  |
| **AzureAD** |  |
| **HTML** |  |
| **Hyper-V** | Hyper-v je méně častý jako značku |
| **Konfigurace** |  |
| **ChatOps** |  |
| **PackageManagement** |  |
| **WMI** |  |
| **Brány firewall** |  |
| **Docker** |  |
| **Appveyor** |  |
| **AzureRm** | Používá hlavně pro moduly AzureRM |
| **PSČ** |  |
| **MSI** |  |
| **Mac** |  |
| **PoshBot** |  |