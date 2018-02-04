# <a name="item-manifest-values-that-impact-the-powershell-gallery-ui"></a>Položka manifest hodnoty, které mají vliv rozhraní Galerie prostředí PowerShell

Toto téma obsahuje vydavatelů s souhrnné informace o tom, jak upravit manifest pro jejich publikace Galerie prostředí PowerShell tak, aby funkce PowerShellGet rutin a rozhraní Galerie prostředí PowerShell bude mít vliv. Tento obsah je seřazená podle změn umístění, od verze v části center a pak navigační oblast na levé straně. Je část Podrobnosti zahrnut značky, který identifikuje důležité značky, jakož i některé Čím více běžně používané značky. Existují dvě témata, která manifestu příklady: 

* Moduly, naleznete v části [aktualizace modulu Manifest](https://docs.microsoft.com/en-us/powershell/gallery/psget/module/psget_update-modulemanifest)
* Skripty, najdete v části [vytvoření souboru skriptu s metadaty](https://docs.microsoft.com/en-us/powershell/gallery/psget/script/psget_new-scriptfileinfo)

## <a name="powershell-gallery-feature-elements-controlled-by-the-manifest"></a>Řízené Manifest prvky funkce Galerie prostředí PowerShell

Následující tabulka uvádí prvky stránky položky galerie prostředí PowerShell uživatelského rozhraní, které jsou řízené vydavatele.
Každá položka označuje, jestli může být ovládaná v manifestu modulu nebo skriptu.

| Element uživatelského rozhraní | Popis | Modul | Skript | 
| --- | --- | --- | --- |
| **Název** | Toto je název položky, která je publikovaná do Galerie  | Ne | Ne |
| **Verze** | Zobrazí verze je řetězec verze ve metadata a předběžné verze pokud je zadán. Primární část verze v manifestu modulu je verze modulu. Pro skript je identifikovaný jako. VERZE. Pokud je zadaný řetězec předprodejní verze, bude připojeno k verze modulu pro moduly, nebo zadaný jako součást. VERZE pro skripty. Není k dispozici dokumentace pro zadání předprodejní řetězců v [moduly](https://docs.microsoft.com/en-us/powershell/gallery/psget/module/prereleasemodule)a v [skriptů](https://docs.microsoft.com/en-us/powershell/gallery/psget/script/prereleasescript) | Ano | Ano |
| **Popis** | Toto je popis v manifestu modulu a v souboru manifestu skriptu je. POPIS | Ano | Ano |
| **Vyžadovat přijetí licence** | Modul může vyžadovat, aby uživatel přijmout licenci, úpravou manifestu modulu s RequireLicenseAcceptance = $true, poskytnutím LicenseURI a poskytnutí souboru license.txt v kořenové složce modulu. Další informace jsou k dispozici v [vyžadovat přijetí licence](https://docs.microsoft.com/en-us/powershell/gallery/psgallery/psgallery_requires_license_acceptance) tématu. | Ano | Ne |
| **Poznámky k verzi** | Pro moduly tyto informace vykreslením z části ReleaseNotes pod PSData\PrivateData. V manifestech skriptu, je. RELEASENOTES element. | Ano | Ano |
| **Vlastníci** | Vlastníci jsou seznam uživatelů v galerii prostředí PowerShell, kdo může aktualizovat položku. Seznamu vlastníků není zahrnutý v manifestu položky. Další dokumentace popisuje postup [spravovat vlastníci položky](https://docs.microsoft.com/en-us/powershell/gallery/psgallery/managing-item-owners). | Ne | Ne |
| **Autor** | To je zahrnuta v manifestu modulu jako autor a v manifestu skriptu jako. AUTOR. Pole Author se často používá k určení společnosti nebo organizace, které jsou přidružené položce. | Ano | Ano |
| **Copyright** | Toto je pole Copyright v manifestu modulu a. COPYRIGHT v manifestu skriptu. | Ano | Ano |
| **FileList** | Seznam souborů je čerpají z balíčku, při publikování do Galerie prostředí PowerShell. Není ovladatelné podle manifestu informace. Poznámka: je soubor s příponou .nuspec další označené každou položku v galerii prostředí PowerShell, který není k dispozici po instalaci položka v systému. Toto je manifest balíčku Nuget pro položku a může být ignorován. | Ne | Ne |
| **Značky** | Pro moduly značky jsou zahrnuty v části PSData\PrivateData. U skriptů je v části označené. ZNAČKY. Všimněte si, že značky nesmí obsahovat mezery, i když se nachází v uvozovkách. Značky mají další požadavky a významy, které jsou popsány dále v tomto tématu v části Podrobnosti značky. | Ano | Ano |
| **Rutiny** | Toto jsou uvedené v manifestu modulu pomocí CmdletsToExport. Všimněte si, že osvědčeným postupem je výslovně uvádějí seznam položek, nikoli pomocí zástupného "*", jako který umožní zvýšení výkonu zatížení modulu pro uživatele. | Ano | Ne |
| **Funkce** | Toto jsou uvedené v manifestu modulu pomocí FunctionsToExport. Všimněte si, že osvědčeným postupem je výslovně uvádějí seznam položek, nikoli pomocí zástupného "*", jako který umožní zvýšení výkonu zatížení modulu pro uživatele. | Ano | Ne |
| **Prostředky DSC** | Pro moduly, které se použijí na prostředí PowerShell verze 5.0 a vyšší tím jsou uvedené v manifestu pomocí DscResourcesToExport. Pokud modul pro použití v prostředí PowerShell 4, DSCResourcesToExport nepoužívejte, protože se nejedná o podporovaný manifestu klíč. (DSC nebyl k dispozici před prostředí PowerShell 4.) | Ano | Ne |
| **Pracovní postupy** | Pracovní postupy jsou publikovány do Galerie prostředí PowerShell jako skripty a identifikovat jako pracovní postupy (viz [Connect-AzureVM](https://www.powershellgallery.com/packages/Connect-AzureVM/1.0/Content/Connect-AzureVM.ps1) příklad) v kódu. Ovládaná nejsou v manifestu. | Ne | Ne |
| **Funkce role** | To se objeví při obsahuje jeden nebo více rolí schopnosti (.psrc) soubory, které jsou používány JEA modul publikovaná do Galerie prostředí PowerShell. V dokumentaci JEA podrobnosti na [role možnosti](https://docs.microsoft.com/en-us/powershell/jea/role-capabilities). | Ano | Ne |
| **Verze prostředí PowerShell** | Toto nastavení je zadané ve skriptu nebo modul manifestu. Pro moduly, které jsou určeny k použití s PowerShell 5.0 a níže, to je řízena pomocí značek. Pro stolní počítače použijte značky PSEdition_Desktop a pro základní, použijte značky PSEdition_Core. Pro moduly, které se použijí jenom v prostředí PowerShell 5.1 a vyšší není v manifestu hlavní klíč CompatiblePSEditions. Další podrobnosti, projděte si funkci edice PS v [v prostředí PowerShell Get dokumentaci](https://docs.microsoft.com/en-us/powershell/gallery/psget/module/modulewithpseditionsupport). | Ano | Ano |
| **Závislosti** | Závislosti jsou moduly v galerii prostředí PowerShell, které jsou deklarované v modulu jako RequiredModules nebo v manifestu skriptu jako #Requires – modul (název). | Ano | Ano |
| **Minimální verze prostředí Powershell** | Můžete zadat v manifestu modulu jako verze prostředí PowerShell | Ano | Ne |
| **Historie verzí** | Historie verzí odráží aktualizace provedené na modul v galerii prostředí PowerShell. Pokud používáte funkci odstranění skrytý verzi položky, ho nebudou zobrazeny v historii verzí s výjimkou na vlastníky položky. | Ne | Ne |
| **Web projektu** | Web projektu zajišťuje pro moduly v části Privatedata\PSData manifestu modulu zadáním ProjectURI. V manifestu skriptu je řízena zadáním. PROJECTURI. | Ano | Ano |
| **License** | Licence je k dispozici odkaz pro moduly v části Privatedata\PSData manifestu modulu zadáním LicenseURI. V manifestu skriptu je řízena zadáním. LICENSEURI. Je důležité si uvědomit, že pokud není k dispozici licence prostřednictvím LicenseURI nebo v rámci modul, pak podmínky použití pro galerii prostředí PowerShell zadejte podmínky použití pro položku. Viz podmínky použití podrobnosti. | Ano | Ano |

## <a name="editing-item-details"></a>Podrobnosti o položkách úpravy

Položka stránce Upravit Galerie prostředí PowerShell umožňuje vydavatelů, chcete-li změnit několik polí zobrazit pro položky, konkrétně:

* Title
* Popis
* Souhrn
* Adresa URL ikony
* Adresa URL domovské stránky projektu
* Autoři
* Copyright
* Značky
* Poznámky k verzi
* Vyžadována licence

Tento přístup se nedoporučuje obecně, s výjimkou při potřeba opravit, co se zobrazuje pro starší verze modulu. Uživatelé, kteří získají modulu se zobrazí, že metadata neodpovídá, co se zobrazí v galerii prostředí PowerShell, který vyvolá pochybnostmi k položce. Výsledkem bude nejčastější dotazy ohledně chystáte vlastníci položky pro potvrzení změny. Důrazně doporučujeme, aby vždy, když tento postup se používá, novou verzi položky je nutné ji publikovat pomocí stejné změny. 

## <a name="tag-details"></a>Podrobnosti značky

Značky jsou jednoduché řetězce příjemci používá k nalezení položek. Značky jsou nejužitečnější, pokud se používají konzistentně napříč mnoha položky související s stejné téma. Pomocí více typů stejného word (například databáze a databáze, nebo testovací a testování) obvykle poskytuje málo výhodné. Značky jsou řetězce, jednoslovného výrazu velká a malá písmena a nesmí obsahovat prázdné znaky. Pokud je heslo, které předpokládáte, že bude hledat uživatele, který přidejte do popis položky a bude nalezen ve výsledcích hledání. Pokud se pokoušíte ke zlepšení čitelnosti pomocí Pascal velká a malá písmena, pomlčku, podtržítkem nebo pomlčkou. Buďte opatrní vytváření dlouhé, komplexní a neobvyklé značky, jako jsou často chybně. 

Jsou značky, které jsou důležité si uvědomit, jako galerie prostředí PowerShell a PowerShellGet rutiny pracovat s nimi jedinečné. PSEdition_Desktop PSEdition_Core jsou konkrétní příklady a jsou popsané výše. 

Jak jsme uvedli výše, značky poskytují maximální hodnotu, když jsou konkrétní a použít konzistentně napříč mnoho položek. Jako vydavatel pokusu o nalezení Nejlepší značky používat je snadnější přístup k vyhledání Galerie prostředí PowerShell pro značky, které je třeba zajistit. V ideálním případě bude mnoho položek vrátil a popisy položky zarovnané s vaším používáním této klíčové slovo. 

Pro referenci tady jsou některé z nejčastěji používaných značky od 12/14/2017. V některých případech jsou podobné, ale možná méně ideální možnosti uvedené vedle značky.
Je osvědčeným postupem použít jako upřednostňovaný značky, který bude mít za následek menší šumu a lepší výsledky hledání pro spotřebitele. 


| **Upřednostňované značky** | **Náhradní řešení a poznámky** |
| --- | --- |
| **Azure** |  |
| **DSC** | DesiredStateConfiguration je méně vhodné, je příliš dlouhá |
| **ResourceManager** | ARM se používá k popisu skupinu procesorů a neměl by se používat pro Azure Resource Manager | **DSCResourceKit** |  |
| **SQL** |  |
| **AWS** |  |
| **DSCResource** |  |
| **Automatizace** |  |
| **REST** |  |
| **ActiveDirectory** | AD není právě používána samostatně  |
| **SQLServer** |  |
| **DBA** |  |
| **Zabezpečení** | Obrana je méně přesné |
| **Databáze** | Databáze (množném čísle) je méně vhodné |
| **DevOps** |  |
| **Windows** |  |
| **Sestavení** |  |
| **Nasazení** | Nasazení se používá méně často |
| **Cloud** |  |
| **GIT** |  |
| **Test** | Testování je méně vhodné |
| **VersionControl** | I když používají častěji je méně přesné verze  |
| **Protokolování** | Upřednostňované použití protokolování jako akce |
| **Protokolu** | Upřednostňované použití protokolu jako věc |
| **Backup** |  |
| **IaaS** |  |
| **Linux** |  |
| **IIS** |  |
| **AzureAutomation** |  |
| **Úložiště** |  |
| **GitHub** |  |
| **JSON** |  |
| **Exchange** |  |
| **Network** | Sítě je podobný, méně často používají |
| **SharePoint** |  |
| **Vytváření sestav** | Vytváření sestav je akce, sestavy věcí |
| **Sestava** | Sestava je věcí |
| **WinRM** |  |
| **Monitorování** |  |
| **VSTS** |  |
| **Excel** |  |
| **Google** |  |
| **Barva** |  |
| **DNS** |  |
| **Office365** | Kontrola pravopisu out Office je vhodnější. O365 se méně často používá, i když je kratší | **Gitlab** |  |
| **Pester** |  |
| **AzureAD** |  |
| **HTML** |  |
| **Hyper-V** | Hyper-v je méně častých jako značku |
| **Konfigurace** |  |
| **ChatOps** |  |
| **PackageManagement** |  |
| **WMI** |  |
| **Firewall** |  |
| **Docker** |  |
| **Appveyor** |  |
| **AzureRm** | Používá se především pro moduly AzureRM |
| **Zip** |  |
| **MSI** |  |
| **Mac** |  |
| **PoshBot** |  |


