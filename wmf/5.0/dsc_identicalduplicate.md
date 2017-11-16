---
ms.date: 2017-06-12
author: JKeithB
ms.topic: reference
keywords: "WMF, prostředí powershell, instalační program"
ms.openlocfilehash: d3a625d05eaf4e7448b4abf90499f6a94e2f7718
ms.sourcegitcommit: 75f70c7df01eea5e7a2c16f9a3ab1dd437a1f8fd
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 06/12/2017
---
# <a name="allowing-for-identical-duplicate-resources-in-a-configuration"></a>Povolení pro identické duplicitní prostředky v konfiguraci

DSC nemá povolit nebo zpracování konfliktní definice prostředků v rámci konfigurace. Namísto pokusu o vyřešení konfliktu, jednoduše dojde k chybě. Jako opakované použití konfigurace se změní na více využité prostřednictvím složené prostředků, dojde častěji konflikty atd. Když jsou identické konfliktní definice prostředků, DSC by měl být inteligentní a povolit to. V této verzi se podporujeme s více instancí prostředků, které mají stejné definice:

```powershell
Configuration IIS_FrontEnd
{
    WindowsFeature FE_IIS         #Identical resource
    {
        Ensure = 'Present'
        Name = 'Web-Server'
    }

    WindowsFeature FTP
    {
        Ensure = 'Present'
        Name = 'Web-FTP-Server'
    }
}

Configuration IIS_Worker
{
    WindowsFeature Worker_IIS      #Identical resource
    {
        Ensure = 'Present'
        Name = 'Web-Server'
    }

    WindowsFeature ASP
    {
        Ensure = 'Present'
        Name = 'Web-ASP-Net45'
    }
}

Configuration WebApplication
{
    IIS_Frontend Web {}

    IIS_Worker ASP {}
}
```

V předchozích verzích výsledkem bude, že je nainstalovaná kompilace se nezdařila z důvodu konfliktu mezi WindowsFeature FE_IIS a instancí WindowsFeature Worker_IIS pokusu zkontrolujte roli webovým serverem. Všimněte si, že *všechny* vlastnosti, které jsou právě konfigurovány jsou identické v těchto dvou konfiguracích. Vzhledem k tomu *všechny* vlastností v tyto dva prostředky jsou identické, výsledkem bude nyní úspěšné kompilace. 

Pokud jsou jakékoli vlastnosti rozdíly mezi dva prostředky, se nebude se zvažovat identické a nebude kompilace:

```powershell
Configuration IIS_FrontEnd
{
    WindowsFeature FE_IIS
    {
        Ensure = 'Present'     # Ensure is Present here
        Name = 'Web-Server'
    }

    WindowsFeature FTP
    {
        Ensure = 'Present'
        Name = 'Web-FTP-Server'
    }
}

Configuration IIS_Worker
{
    WindowsFeature Worker_IIS
    {
        Ensure = 'Absent'      # Ensure property is Absent instead of Present
        Name = 'Web-Server'
    }

    WindowsFeature ASP
    {
        Ensure = 'Present'
        Name = 'Web-ASP-Net45'
    }
}

Configuration WebApplication
{
    IIS_Frontend Web {}

    IIS_Worker ASP {}
}
```

Tato velmi podobné konfigurace selže, protože WindowsFeature FE_IIS a prostředky WindowsFeature Worker_IIS již nejsou identické a proto dojít ke konfliktu.

