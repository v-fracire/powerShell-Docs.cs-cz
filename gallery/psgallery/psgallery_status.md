---
ms.date: 2017-06-12
contributor: JKeithB
ms.topic: conceptual
keywords: "Galerie prostředí powershell, rutiny, psgallery"
title: psgallery_status
ms.openlocfilehash: af6111d3c511273571bd978c6d0e7447726c2917
ms.sourcegitcommit: f069ff0689006fece768f178c10e3e3eeaee09f0
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 10/13/2017
---
<a name="powershell-gallery-status"></a>Stav Galerie prostředí PowerShell
=========================
## <a name="10102017---powershell-gallery-unavailable-for-2-hours-101017"></a>10/10/2017 - Galerie prostředí PowerShell, které jsou k dispozici další 2 hodiny 10/10/17

__Souhrn dopad__: galerii prostředí PowerShell došlo období velmi vysokou latencí, což vede k nepřerušované připojení problémy, počínaje přibližně 17: 00 (PDT) 10/10/17. Při řešení problému, převedl webu do stavu offline 2 hodin od přibližně 22: 00 (PDT). Webu byla obnovena krátce před půlnoc 10/10/2017. 
 
__Příčina__: hlavní příčinu vysoké latenci je stále probíhá prozkoumat.

__Řešení__: webové služby musí být převedeny do režimu offline a obnovit Chcete-li primární problém vyřešit. 

__Další kroky__: příčinu původní problém zkoumán.

## <a name="06012017---deploy-to-azure-automation-currently-unavailable"></a>01/06/2017 - nasazení do služby Azure Automation, které jsou nyní k dispozici

__Souhrn dopad__: nasazení položek závislosti pro Azure Automation z Galerie prostředí PowerShell je nyní k dispozici.  Import položek z Galerie Powershellu z uvnitř Azure Automation je stále k dispozici.  
 
__Hlavní příčinu__: položky, které mají závislosti na jiných a byla předtím nasadili do Azure Automation, nebude nasazen do Azure Automation. Technici určili problém s způsob generování šablon ARM pro položky s závislosti pro nasazení do Azure Automation funkce.

__Řešení__: technici pracují k vyřešení problému.  Aktuální řešení pro uživatele je importovat položky z Galerie Powershellu z uvnitř Azure Automation. 

__Další kroky__: technici vydá opravu za chvíli.  Do té doby použijte prosím doporučená řešení. 


## <a name="04112017---users-unable-to-log-in-with-azure-active-directory-aad-accounts"></a>04/11/2017 - uživatele nelze se přihlásit účty Azure Active Directory (AAD)

__Souhrn dopad__: někteří uživatelé nemohli k přihlášení do Galerie prostředí PowerShell pomocí účty Azure AD. 
 
__Hlavní příčinu__: během aktualizace bezpečněji spolupracovat s AAD, nebyla provedena změna nastavení. Testování provádí ověření změny nejsou zahrnuty některé typy účtů AAD, aby nasazení pokračovalo.

__Řešení__: technici identifikovat chybějící nastavení a byl problém odstraněn. 

__Další kroky__: jsme se změnou našich testech zahrnout širší sadě typy účtů AAD.

## <a name="03272017---resolved-unable-to-see-individual-module-and-script-pages"></a>VYŘEŠIT 03/27/2017 -: nelze zobrazit jednotlivé stránky modulu a skriptu

__Souhrn dopad__: přímé odkazy na jednotlivé modulu a skript stránky https://www.powershellgallery.com bylo přerušeno. To se ohlásil přes všechny oblasti. To negativní vliv na některé z rutiny PowerShellGet ie., nainstalujte modul, skript aktualizace, publikování-Module skriptu instalace, aktualizace-Module publikování-Scirpt dál fungovat.

__Příčina__: technici označený příčinu problému přináší až sociálních médií tlačítka jako je Facebook na stránku.  

__Řešení__: technici opraven problém zakázání informace o počtu Facebook.

__Další kroky__: jsme otevřít interní sledování problém opravit naše využití rozhraní API sítě Facebook.

## <a name="12152016---unable-to-send-emails-via-powershellgallery-website"></a>12/15/2016 - nelze odeslat e-mailů prostřednictvím PowerShellGallery webu

__Souhrn dopad__: až 12, 13/2016 15 12. 2016, nebyly přijaty žádné zprávy odeslané přes kontaktujte vlastníky, Spravovat vlastníky, obraťte se na podporu nebo oznámení zneužití správci Galerie prostředí PowerShell.  
__Příčina__: technici označený příčinu chyby ověřování se serverem SMTP.  
__Řešení__: technici byli schopni vyřešit problém s ověřováním a obnovte připojení k serveru SMTP.  
__Další kroky__: Pokud jste použili kontaktujte vlastníky, Spravovat vlastníky, obraťte se na podporu nebo oznámení zneužití odkazy k odesílání e-mailu cgadmin@microsoft.com během této doby a jsme neodpověděli, zkuste to prosím znovu. Omlouváme se za nepříjemnosti.  



## <a name="8102016---resolved-unable-to-send-emails-to-cgadminmicrosoftcom"></a>8/10/2016 - přeložit: nebylo možné odeslat e-mailůcgadmin@microsoft.com

__Souhrn dopad__: mezi 8/5/2016 a 8/10/2016 zákazníci nemohli odesílat e-mailů cgadmin@microsoft.com, nebo použijte funkci kontaktujte nás.  
__Příčina__: technici označený příčinu změna konfigurace e-mailového účtu.  
__Řešení__: technici práce na incidentu k vyřešení problému konfigurace.  
__Další kroky__: Pokud můžete použít odkaz kontaktujte nás nebo odeslat e-mailu cgadmin@microsoft.com během této doby a jsme neodpověděli, zkuste to prosím znovu. Děkujeme vám za trpělivost.



## <a name="7132016---download-items-failed"></a>13/7/2016 – stažení položky se nezdařilo

__Souhrn dopad__: mezi 7/11. dubna 2016 a 13 7. 2016 podmnožinu zákazníkům došlo problémy stahování položky z Galerie prostředí PowerShell. Tento problém pravděpodobně sám označované v následující chybovou zprávu vrácenou z instalace – modul nebo instalační skript a uložit modulu nebo Save-skriptu:

```powershell
PS C:\> Install-Module xStorage 
PackageManagement\Install-Package : Package 'xStorage' failed to be installed because: 
End of Central Directory record could not be found. At C:\Program 
Files\WindowsPowerShell\Modules\PowerShellGet\1.0.0.1\PSModule.psm1:1375 char:21 + ... 
$null = PackageManagement\Install-Package @PSBoundParameters + 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ + CategoryInfo : InvalidResult: 
(xStorage:String) [Install-Package], Exception + FullyQualifiedErrorId : Package '{0}' 
failed to be installed because: {1},Microsoft.PowerShell.PackageManagement.Cmdlets.InstallPackage 
```

__Předběžný hlavní příčinu__: technici zjistila problém s obsahu doručit síť (CDN) Azure, který byl nasazen do Galerie prostředí PowerShell na 7/11. dubna 2016.  
__Zmírnění dopadů__: technici zakázáno Azure CDN v galerii prostředí PowerShell.  
__Další kroky__: prozkoumat základní příčiny a vývoj řešení, aby se zabránilo budoucna.


## <a name="5192016---download-items-failed"></a>5/19. ledna 2016 - stažení položky se nezdařilo
__Souhrn dopad__: mezi 5/17/2016 a 5/19. ledna 2016, podmnožinu zákazníkům došlo problémy stahování položky z Galerie prostředí PowerShell. Tento problém pravděpodobně sám označované v následující chybovou zprávu vrácenou z instalace – modul nebo instalační skript a uložit modulu nebo Save-skriptu:

```powershell
VERBOSE: Hash for package 'AzureRM.OperationalInsights' does not match hash provided from the server.
VERBOSE: InstallPackageLocal' - name='AzureRM.OperationalInsights', version='1.0.8',
destination='C:\Users\jbritt\AppData\Local\Temp\2\1741355729'
WARNING: Package 'AzureRM.OperationalInsights' failed to be installed because: 
End of Central Directory record could not be found. 
WARNING: Dependent Package 'AzureRM.OperationalInsights' failed to install. 
WARNING: Package 'AzureRM' failed to install. 
VERBOSE: Module 'AzureRM.Network' was saved successfully. 
VERBOSE: Saving the dependency module 'AzureRM.NotificationHubs' with version '1.0.8' for the 
module 'AzureRM'. 
VERBOSE: Module 'AzureRM.NotificationHubs' was saved successfully. 
PackageManagement\Save-Package : Unable to save the module 'AzureRM'. At C:\Program 
Files\WindowsPowerShell\Modules\PowerShellGet\1.0.0.1\PSModule.psm1:1187 char:21 + 
$null = PackageManagement\Save-Package @PSBoundParameters + 
~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~~ + 
CategoryInfo : InvalidOperation: (Microsoft.Power...ets.SavePackage:SavePackage) 
[Save-Package], Exception + FullyQualifiedErrorId : ProviderFailToDownloadFile,
Microsoft.PowerShell.PackageManagement.Cmdlets.SavePackage 
```

__Předběžný hlavní příčinu__: technici identifikovat výpadku v rámci příslušného zprostředkovatele z obsahu doručit síť (CDN) Azure, který byl nasazen do Galerie prostředí PowerShell 5/17/2016.  
__Zmírnění dopadů__: technici zakázáno Azure CDN v galerii prostředí PowerShell.  
__Další kroky__: prozkoumat základní příčiny a vývoj řešení, aby se zabránilo budoucna.

