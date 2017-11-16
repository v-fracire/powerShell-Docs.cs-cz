---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Vytvoření nového objektu .NET a COM – objekty"
ms.assetid: 2057b113-efeb-465e-8b44-da2f20dbf603
ms.openlocfilehash: 534e1a9a759d67cfc62ce658a7abddf02f767212
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/03/2017
---
# <a name="creating-net-and-com-objects-new-object"></a><span data-ttu-id="be1c9-103">Vytváření rozhraní .NET a objekty modelu COM (nový objekt)</span><span class="sxs-lookup"><span data-stu-id="be1c9-103">Creating .NET and COM Objects (New-Object)</span></span>
<span data-ttu-id="be1c9-104">Existují softwarové komponenty pomocí rozhraní .NET Framework a COM, které vám umožní provádět mnoho úloh správy systému.</span><span class="sxs-lookup"><span data-stu-id="be1c9-104">There are software components with .NET Framework and COM interfaces that enable you to perform many system administration tasks.</span></span> <span data-ttu-id="be1c9-105">Prostředí Windows PowerShell umožňuje použít tyto součásti, takže můžete nejsou omezeny na úlohy, které lze provést pomocí rutin.</span><span class="sxs-lookup"><span data-stu-id="be1c9-105">Windows PowerShell lets you use these components, so you are not limited to the tasks that can be performed by using cmdlets.</span></span> <span data-ttu-id="be1c9-106">Mnoho rutin v původní verze prostředí Windows PowerShell nefungují na vzdálených počítačích.</span><span class="sxs-lookup"><span data-stu-id="be1c9-106">Many of the cmdlets in the initial release of Windows PowerShell do not work against remote computers.</span></span> <span data-ttu-id="be1c9-107">Popisuje, jak získat obejít toto omezení při správě protokolů událostí pomocí rozhraní .NET Framework **System.Diagnostics.EventLog** třídy přímo z prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="be1c9-107">We will demonstrate how to get around this limitation when managing event logs by using the .NET Framework **System.Diagnostics.EventLog** class directly from Windows PowerShell.</span></span>

### <a name="using-new-object-for-event-log-access"></a><span data-ttu-id="be1c9-108">Použití nový objekt pro přístup k protokolu událostí</span><span class="sxs-lookup"><span data-stu-id="be1c9-108">Using New-Object for Event Log Access</span></span>
<span data-ttu-id="be1c9-109">Knihovna tříd rozhraní .NET Framework zahrnuje třídy s názvem **System.Diagnostics.EventLog** který lze použít ke správě protokolů událostí.</span><span class="sxs-lookup"><span data-stu-id="be1c9-109">The .NET Framework Class Library includes a class named **System.Diagnostics.EventLog** that can be used to manage event logs.</span></span> <span data-ttu-id="be1c9-110">Můžete vytvořit novou instanci třídy rozhraní .NET Framework pomocí **New-Object** rutiny s **TypeName** parametr.</span><span class="sxs-lookup"><span data-stu-id="be1c9-110">You can create a new instance of a .NET Framework class by using the **New-Object** cmdlet with the **TypeName** parameter.</span></span> <span data-ttu-id="be1c9-111">Například následující příkaz vytvoří odkaz na protokol událostí:</span><span class="sxs-lookup"><span data-stu-id="be1c9-111">For example, the following command creates an event log reference:</span></span>

```
PS> New-Object -TypeName System.Diagnostics.EventLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
```

<span data-ttu-id="be1c9-112">I když příkaz vytvořil instanci třídy protokolu událostí, instance neobsahuje žádná data.</span><span class="sxs-lookup"><span data-stu-id="be1c9-112">Although the command has created an instance of the EventLog class, the instance does not include any data.</span></span> <span data-ttu-id="be1c9-113">Je to způsobeno jsme nezadali určitý protokol událostí.</span><span class="sxs-lookup"><span data-stu-id="be1c9-113">That is because we did not specify a particular event log.</span></span> <span data-ttu-id="be1c9-114">Jak získáte skutečné protokolu událostí</span><span class="sxs-lookup"><span data-stu-id="be1c9-114">How do you get a real event log?</span></span>

#### <a name="using-constructors-with-new-object"></a><span data-ttu-id="be1c9-115">Použití konstruktorů s nový objekt</span><span class="sxs-lookup"><span data-stu-id="be1c9-115">Using Constructors with New-Object</span></span>
<span data-ttu-id="be1c9-116">Odkázat na určitém protokolu událostí, budete muset zadat název protokolu.</span><span class="sxs-lookup"><span data-stu-id="be1c9-116">To refer to a specific event log, you need to specify the name of the log.</span></span> <span data-ttu-id="be1c9-117">**Nový objekt** má **ArgumentList** parametr.</span><span class="sxs-lookup"><span data-stu-id="be1c9-117">**New-Object** has an **ArgumentList** parameter.</span></span> <span data-ttu-id="be1c9-118">Argumenty, které můžete předat jako hodnoty tohoto parametru jsou používány speciální spuštění metodu objektu.</span><span class="sxs-lookup"><span data-stu-id="be1c9-118">The arguments you pass as values to this parameter are used by a special startup method of the object.</span></span> <span data-ttu-id="be1c9-119">Volání metody *konstruktor* protože se používá k vytvoření objektu.</span><span class="sxs-lookup"><span data-stu-id="be1c9-119">The method is called a *constructor* because it is used to construct the object.</span></span> <span data-ttu-id="be1c9-120">Například k získání odkazu do aplikačního protokolu, můžete zadat řetězec "Žádost" jako argument:</span><span class="sxs-lookup"><span data-stu-id="be1c9-120">For example, to get a reference to the Application log, you specify the string 'Application' as an argument:</span></span>

```
PS> New-Object -TypeName System.Diagnostics.EventLog -ArgumentList Application

Max(K) Retain OverflowAction        Entries Name
------ ------ --------------        ------- ----
16,384      7 OverwriteOlder          2,160 Application
```

> [!NOTE]
> <span data-ttu-id="be1c9-121">Vzhledem k tomu, že většina základní třídy rozhraní .NET Framework jsou obsaženy v oboru názvů systému, prostředí Windows PowerShell se automaticky pokusí vyhledat třídy, které zadáte v oboru názvů systému, pokud nemůže najít shodu pro typename, které zadáte.</span><span class="sxs-lookup"><span data-stu-id="be1c9-121">Since most of the .NET Framework core classes are contained in the System namespace, Windows PowerShell will automatically attempt to find classes you specify in the System namespace if it cannot find a match for the typename you specify.</span></span> <span data-ttu-id="be1c9-122">To znamená, že je možné zadat Diagnostics.EventLog místo System.Diagnostics.EventLog.</span><span class="sxs-lookup"><span data-stu-id="be1c9-122">This means that you can specify Diagnostics.EventLog instead of System.Diagnostics.EventLog.</span></span>

#### <a name="storing-objects-in-variables"></a><span data-ttu-id="be1c9-123">Ukládání objektů v proměnné</span><span class="sxs-lookup"><span data-stu-id="be1c9-123">Storing Objects in Variables</span></span>
<span data-ttu-id="be1c9-124">Můžete chtít uložit odkaz na objekt, abyste je mohli používat v aktuálním prostředí.</span><span class="sxs-lookup"><span data-stu-id="be1c9-124">You might want to store a reference to an object, so you can use it in the current shell.</span></span> <span data-ttu-id="be1c9-125">I když prostředí Windows PowerShell můžete dělat spoustu práce s kanály, lessening potřebu proměnné, někdy ukládání odkazů na objekty v proměnné je pohodlnější k manipulaci s těchto objektů.</span><span class="sxs-lookup"><span data-stu-id="be1c9-125">Although Windows PowerShell lets you do a lot of work with pipelines, lessening the need for variables, sometimes storing references to objects in variables makes it more convenient to manipulate those objects.</span></span>

<span data-ttu-id="be1c9-126">Prostředí Windows PowerShell umožňuje vytvářet proměnné, které jsou v podstatě s názvem objekty.</span><span class="sxs-lookup"><span data-stu-id="be1c9-126">Windows PowerShell lets you create variables that are essentially named objects.</span></span> <span data-ttu-id="be1c9-127">Výstup z jakékoli platný příkaz prostředí Windows PowerShell můžete uložené v proměnné.</span><span class="sxs-lookup"><span data-stu-id="be1c9-127">The output from any valid Windows PowerShell command can be stored in a variable.</span></span> <span data-ttu-id="be1c9-128">Názvy proměnných vždy začínat $.</span><span class="sxs-lookup"><span data-stu-id="be1c9-128">Variable names always begin with $.</span></span> <span data-ttu-id="be1c9-129">Pokud chcete uložit do proměnné s názvem $AppLog protokolu odkaz na aplikaci, zadejte název proměnné následuje symbol rovná a pak zadejte příkaz sloužící k vytvoření objektu Application protokolu:</span><span class="sxs-lookup"><span data-stu-id="be1c9-129">If you want to store the Application log reference in a variable named $AppLog, type the name of the variable, followed by an equal sign and then type the command used to create the Application log object:</span></span>

```
PS> $AppLog = New-Object -TypeName System.Diagnostics.EventLog -ArgumentList Application
```

<span data-ttu-id="be1c9-130">Pokud zadejte $AppLog můžete zjistit, že obsahuje protokolu aplikace:</span><span class="sxs-lookup"><span data-stu-id="be1c9-130">If you then type $AppLog, you can see that it contains the Application log:</span></span>

```
PS> $AppLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
  16,384      7 OverwriteOlder          2,160 Application
```

#### <a name="accessing-a-remote-event-log-with-new-object"></a><span data-ttu-id="be1c9-131">Přístup k vzdáleného protokolu událostí s nový objekt</span><span class="sxs-lookup"><span data-stu-id="be1c9-131">Accessing a Remote Event Log with New-Object</span></span>
<span data-ttu-id="be1c9-132">Funkce použité v předchozí části cílit na místní počítač; **Get-EventLog** rutiny můžete udělat.</span><span class="sxs-lookup"><span data-stu-id="be1c9-132">The commands used in the preceding section target the local computer; the **Get-EventLog** cmdlet can do that.</span></span> <span data-ttu-id="be1c9-133">Chcete-li získat přístup k protokolu aplikace ve vzdáleném počítači, je nutné zadat název protokolu a název počítače (i IP adresu) jako argumenty.</span><span class="sxs-lookup"><span data-stu-id="be1c9-133">To access the Application log on a remote computer, you must supply both the log name and a computer name (or IP address) as arguments.</span></span>

```
PS> $RemoteAppLog = New-Object -TypeName System.Diagnostics.EventLog Application,192.168.1.81
PS> $RemoteAppLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
     512      7 OverwriteOlder            262 Application
```

<span data-ttu-id="be1c9-134">Teď, když máme odkaz na protokol událostí uložené v proměnné $RemoteAppLog, můžete nám jaké úlohy provádět na něm?</span><span class="sxs-lookup"><span data-stu-id="be1c9-134">Now that we have a reference to an event log stored in the $RemoteAppLog variable, what tasks can we perform on it?</span></span>

#### <a name="clearing-an-event-log-with-object-methods"></a><span data-ttu-id="be1c9-135">Vymazání protokolu událostí pomocí metod objektu</span><span class="sxs-lookup"><span data-stu-id="be1c9-135">Clearing an Event Log with Object Methods</span></span>
<span data-ttu-id="be1c9-136">Objekty mají často metody, které lze volat pro provádění úloh.</span><span class="sxs-lookup"><span data-stu-id="be1c9-136">Objects often have methods that can be called to perform tasks.</span></span> <span data-ttu-id="be1c9-137">Můžete použít **Get-člen** zobrazíte metody přidružená k objektu.</span><span class="sxs-lookup"><span data-stu-id="be1c9-137">You can use **Get-Member** to display the methods associated with an object.</span></span> <span data-ttu-id="be1c9-138">Následující příkaz a vybrané výstupní zobrazit některé metody třídy protokolu událostí:</span><span class="sxs-lookup"><span data-stu-id="be1c9-138">The following command and selected output show some the methods of the EventLog class:</span></span>

```
PS> $RemoteAppLog | Get-Member -MemberType Method

   TypeName: System.Diagnostics.EventLog

Name                      MemberType Definition
----                      ---------- ----------
...
Clear                     Method     System.Void Clear()
Close                     Method     System.Void Close()
...
GetType                   Method     System.Type GetType()
...
ModifyOverflowPolicy      Method     System.Void ModifyOverflowPolicy(Overfl...
RegisterDisplayName       Method     System.Void RegisterDisplayName(String ...
...
ToString                  Method     System.String ToString()
WriteEntry                Method     System.Void WriteEntry(String message),...
WriteEvent                Method     System.Void WriteEvent(EventInstance in...
```

<span data-ttu-id="be1c9-139">**Funkce Clear()** metoda slouží k vymazání protokolu událostí.</span><span class="sxs-lookup"><span data-stu-id="be1c9-139">The **Clear()** method can be used to clear the event log.</span></span> <span data-ttu-id="be1c9-140">Při volání metody, je nutné provést název metody v závorkách, i v případě, že metoda nevyžaduje argumenty.</span><span class="sxs-lookup"><span data-stu-id="be1c9-140">When calling a method, you must always follow the method name by parentheses, even if the method does not require arguments.</span></span> <span data-ttu-id="be1c9-141">Díky tomu prostředí Windows PowerShell rozlišit mezi metoda a potenciální vlastnost se stejným názvem.</span><span class="sxs-lookup"><span data-stu-id="be1c9-141">This lets Windows PowerShell distinguish between the method and a potential property with the same name.</span></span> <span data-ttu-id="be1c9-142">Zadejte následující příkaz pro volání **zrušte** metoda:</span><span class="sxs-lookup"><span data-stu-id="be1c9-142">Type the following to call the **Clear** method:</span></span>

```
PS> $RemoteAppLog.Clear()
```

<span data-ttu-id="be1c9-143">Zadejte následující příkaz k zobrazení v protokolu.</span><span class="sxs-lookup"><span data-stu-id="be1c9-143">Type the following to display the log.</span></span> <span data-ttu-id="be1c9-144">Zobrazí se, že protokol událostí byl vymazán a má teď 0 položek místo 262:</span><span class="sxs-lookup"><span data-stu-id="be1c9-144">You will see that the event log was cleared, and now has 0 entries instead of 262:</span></span>

```
PS> $RemoteAppLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
     512      7 OverwriteOlder              0 Application
```

### <a name="creating-com-objects-with-new-object"></a><span data-ttu-id="be1c9-145">Vytváření objektů modelu COM pomocí nového objektu</span><span class="sxs-lookup"><span data-stu-id="be1c9-145">Creating COM Objects with New-Object</span></span>
<span data-ttu-id="be1c9-146">Můžete použít **New-Object** pro práci s komponenty modelu COM (Component Object).</span><span class="sxs-lookup"><span data-stu-id="be1c9-146">You can use **New-Object** to work with Component Object Model (COM) components.</span></span> <span data-ttu-id="be1c9-147">Součásti v rozsahu od různých knihoven zahrnuté do ActiveX aplikace, jako je například Internet Explorer, které jsou nainstalované na většina systémů s skriptu hostitele prostředí WSH (Windows).</span><span class="sxs-lookup"><span data-stu-id="be1c9-147">Components range from the various libraries included with Windows Script Host (WSH) to ActiveX applications such as Internet Explorer that are installed on most systems.</span></span>

<span data-ttu-id="be1c9-148">**Nový objekt** používá rozhraní .NET Framework Runtime-– obálky s možností vytvořit objekty modelu COM, takže má stejná omezení, které nepodporuje rozhraní .NET Framework při volání COM – objekty.</span><span class="sxs-lookup"><span data-stu-id="be1c9-148">**New-Object** uses .NET Framework Runtime-Callable Wrappers to create COM objects, so it has the same limitations that .NET Framework does when calling COM objects.</span></span> <span data-ttu-id="be1c9-149">Vytvoření objektu COM, budete muset zadat **ComObject** parametr s programový identifikátor nebo *ProgId* třídy COM, kterou chcete použít.</span><span class="sxs-lookup"><span data-stu-id="be1c9-149">To create a COM object, you need to specify the **ComObject** parameter with the Programmatic Identifier or *ProgId* of the COM class you want to use.</span></span> <span data-ttu-id="be1c9-150">Úplné informace o omezení použití COM a určit, jaké ProgID jsou k dispozici v systému je nad rámec této uživatelské příručce, ale dobře známé objekty z prostředích, jako je prostředí WSH dá v prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="be1c9-150">A complete discussion of the limitations of COM use and determining what ProgIds are available on a system is beyond the scope of this user's guide, but most well-known objects from environments such as WSH can be used within Windows PowerShell.</span></span>

<span data-ttu-id="be1c9-151">Můžete vytvořit objekty WSH zadáním těchto ProgID: **WScript.Shell**, **WScript.Network**, **Scripting.Dictionary**, a  **Scripting.FileSystemObject**.</span><span class="sxs-lookup"><span data-stu-id="be1c9-151">You can create the WSH objects by specifying these progids: **WScript.Shell**, **WScript.Network**, **Scripting.Dictionary**, and **Scripting.FileSystemObject**.</span></span> <span data-ttu-id="be1c9-152">Následující příkazy vytvořit tyto objekty:</span><span class="sxs-lookup"><span data-stu-id="be1c9-152">The following commands create these objects:</span></span>

```
New-Object -ComObject WScript.Shell
New-Object -ComObject WScript.Network
New-Object -ComObject Scripting.Dictionary
New-Object -ComObject Scripting.FileSystemObject
```

<span data-ttu-id="be1c9-153">Přestože většinu funkcí těchto tříd je k dispozici jiným způsobem v prostředí Windows PowerShell, jsou stále lépe pomocí WSH třídy několik úloh, jako je například vytváření zástupce.</span><span class="sxs-lookup"><span data-stu-id="be1c9-153">Although most of the functionality of these classes is made available in other ways in Windows PowerShell, a few tasks such as shortcut creation are still easier to do using the WSH classes.</span></span>

### <a name="creating-a-desktop-shortcut-with-wscriptshell"></a><span data-ttu-id="be1c9-154">Vytvoření zástupce na ploše s WScript.Shell</span><span class="sxs-lookup"><span data-stu-id="be1c9-154">Creating a Desktop Shortcut with WScript.Shell</span></span>
<span data-ttu-id="be1c9-155">Jednu úlohu, která lze rychle provést pomocí objektu COM je vytvoření zástupce.</span><span class="sxs-lookup"><span data-stu-id="be1c9-155">One task that can be performed quickly with a COM object is creating a shortcut.</span></span> <span data-ttu-id="be1c9-156">Předpokládejme, že chcete vytvořit zástupce na ploše odkazující na domovskou složku pro prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="be1c9-156">Suppose you want to create a shortcut on your desktop that links to the home folder for Windows PowerShell.</span></span> <span data-ttu-id="be1c9-157">Je nutné nejprve vytvořit odkaz na **WScript.Shell**, který jsme budou ukládat do proměnné s názvem **$WshShell**:</span><span class="sxs-lookup"><span data-stu-id="be1c9-157">You first need to create a reference to **WScript.Shell**, which we will store in a variable named **$WshShell**:</span></span>

```
$WshShell = New-Object -ComObject WScript.Shell
```

<span data-ttu-id="be1c9-158">Get-člen funguje s objekty modelu COM, abyste jej mohli prozkoumat členy objektu zadáním:</span><span class="sxs-lookup"><span data-stu-id="be1c9-158">Get-Member works with COM objects, so you can explore the members of the object by typing:</span></span>

```
PS> $WshShell | Get-Member

   TypeName: System.__ComObject#{41904400-be18-11d3-a28b-00104bd35090}

Name                     MemberType            Definition
----                     ----------            ----------
AppActivate              Method                bool AppActivate (Variant, Va...
CreateShortcut           Method                IDispatch CreateShortcut (str...
...
```

<span data-ttu-id="be1c9-159">**Get-člen** má volitelný **InputObject** parametr, můžete místo zřetězení k zadání **Get-člen**.</span><span class="sxs-lookup"><span data-stu-id="be1c9-159">**Get-Member** has an optional **InputObject** parameter you can use instead of piping to provide input to **Get-Member**.</span></span> <span data-ttu-id="be1c9-160">Které byste získali stejný výstup jako v příkladu nahoře, pokud místo toho použít příkaz **člen Get - InputObject $WshShell**.</span><span class="sxs-lookup"><span data-stu-id="be1c9-160">You would get the same output as shown above if you instead used the command **Get-Member -InputObject $WshShell**.</span></span> <span data-ttu-id="be1c9-161">Pokud používáte **InputObject**, ho pracuje s její argument jako jednu položku.</span><span class="sxs-lookup"><span data-stu-id="be1c9-161">If you use **InputObject**, it treats its argument as a single item.</span></span> <span data-ttu-id="be1c9-162">To znamená, že pokud máte několik objektů do proměnné, **Get-člen** pracuje s nimi jako pole objektů.</span><span class="sxs-lookup"><span data-stu-id="be1c9-162">This means that if you have several objects in a variable, **Get-Member** treats them as an array of objects.</span></span> <span data-ttu-id="be1c9-163">Příklad:</span><span class="sxs-lookup"><span data-stu-id="be1c9-163">For example:</span></span>


```
PS> $a = 1,2,"three"
PS> Get-Member -InputObject $a
TypeName: System.Object[]
Name               MemberType    Definition
----               ----------    ----------
Count              AliasProperty Count = Length
...
```

<span data-ttu-id="be1c9-164">**WScript.Shell CreateShortcut** metoda přijímá jeden argument, cesta k souboru zástupce vytvořit.</span><span class="sxs-lookup"><span data-stu-id="be1c9-164">The **WScript.Shell CreateShortcut** method accepts a single argument, the path to the shortcut file to create.</span></span> <span data-ttu-id="be1c9-165">Jsme může zadejte úplnou cestu k pracovní ploše, ale je jednodušší způsob.</span><span class="sxs-lookup"><span data-stu-id="be1c9-165">We could type in the full path to the desktop, but there is an easier way.</span></span> <span data-ttu-id="be1c9-166">Na ploše je obvykle reprezentována složku s názvem plochy uvnitř domovskou složku aktuálního uživatele.</span><span class="sxs-lookup"><span data-stu-id="be1c9-166">The desktop is normally represented by a folder named Desktop inside the home folder of the current user.</span></span> <span data-ttu-id="be1c9-167">Prostředí Windows PowerShell obsahuje proměnnou **$Home** obsahující cestu k této složce.</span><span class="sxs-lookup"><span data-stu-id="be1c9-167">Windows PowerShell has a variable **$Home** that contains the path to this folder.</span></span> <span data-ttu-id="be1c9-168">Jsme můžete zadat cestu ke složce domácí pomocí této proměnné a poté přidejte název plochy složky a názvu zástupce vytvořit zadáním:</span><span class="sxs-lookup"><span data-stu-id="be1c9-168">We can specify the path to the home folder by using this variable, and then add the name of the Desktop folder and the name for the shortcut to create by typing:</span></span>

```
$lnk = $WshShell.CreateShortcut("$Home\Desktop\PSHome.lnk")
```

<span data-ttu-id="be1c9-169">Použijete-li objekt, který vypadá jako název proměnné uvnitř dvojitých uvozovek, pokusí se prostředí Windows PowerShell nahraďte odpovídající hodnotu.</span><span class="sxs-lookup"><span data-stu-id="be1c9-169">When you use something that looks like a variable name inside double-quotes, Windows PowerShell tries to substitute a matching value.</span></span> <span data-ttu-id="be1c9-170">Pokud použijete jeden uvozovky, není pokusí nahraďte hodnotu proměnné prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="be1c9-170">If you use single-quotes, Windows PowerShell does not try to substitute the variable value.</span></span> <span data-ttu-id="be1c9-171">Zkuste například zadáním následujících příkazů:</span><span class="sxs-lookup"><span data-stu-id="be1c9-171">For example, try typing the following commands:</span></span>

```
PS> "$Home\Desktop\PSHome.lnk"
C:\Documents and Settings\aka\Desktop\PSHome.lnk
PS> '$Home\Desktop\PSHome.lnk'
$Home\Desktop\PSHome.lnk
```

<span data-ttu-id="be1c9-172">Nyní je k dispozici proměnné s názvem **$lnk** obsahující odkaz na nový zástupce.</span><span class="sxs-lookup"><span data-stu-id="be1c9-172">We now have a variable named **$lnk** that contains a new shortcut reference.</span></span> <span data-ttu-id="be1c9-173">Pokud chcete zobrazit členy, můžete zřetězit ho do **Get-člen**.</span><span class="sxs-lookup"><span data-stu-id="be1c9-173">If you want to see its members, you can pipe it to **Get-Member**.</span></span> <span data-ttu-id="be1c9-174">Následující výstup zobrazuje členy, že je potřeba pro dokončení vytváření naše zástupce:</span><span class="sxs-lookup"><span data-stu-id="be1c9-174">The output below shows the members we need to use to finish creating our shortcut:</span></span>

```
PS> $lnk | Get-Member
TypeName: System.__ComObject#{f935dc23-1cf0-11d0-adb9-00c04fd58a0b}
Name             MemberType   Definition
----             ----------   ----------
...
Save             Method       void Save ()
...
TargetPath       Property     string TargetPath () {get} {set}
```

<span data-ttu-id="be1c9-175">Je potřeba zadat **TargetPath –**, což je složka aplikace pro prostředí Windows PowerShell a potom uložte zástupce **$lnk** voláním **Uložit** metoda.</span><span class="sxs-lookup"><span data-stu-id="be1c9-175">We need to specify the **TargetPath**, which is the application folder for Windows PowerShell, and then save the shortcut **$lnk** by calling the **Save** method.</span></span> <span data-ttu-id="be1c9-176">Cesta ke složce aplikace prostředí Windows PowerShell je uložené v proměnné **$PSHome**, takže jsme lze provést zadáním:</span><span class="sxs-lookup"><span data-stu-id="be1c9-176">The Windows PowerShell application folder path is stored in the variable **$PSHome**, so we can do this by typing:</span></span>

```
$lnk.TargetPath = $PSHome
$lnk.Save()
```

### <a name="using-internet-explorer-from-windows-powershell"></a><span data-ttu-id="be1c9-177">Použijte Internet Explorer z prostředí Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="be1c9-177">Using Internet Explorer from Windows PowerShell</span></span>
<span data-ttu-id="be1c9-178">Mnoho aplikací (včetně aplikace Microsoft Office řadu aplikací a prohlížeče Internet Explorer) je možné automatizovat pomocí modelu COM.</span><span class="sxs-lookup"><span data-stu-id="be1c9-178">Many applications (including the Microsoft Office family of applications and Internet Explorer) can be automated by using COM.</span></span> <span data-ttu-id="be1c9-179">Internet Explorer ukazuje některé typické techniky a problémy při práci s aplikace založené na modelu COM.</span><span class="sxs-lookup"><span data-stu-id="be1c9-179">Internet Explorer illustrates some of the typical techniques and issues involved in working with COM-based applications.</span></span>

<span data-ttu-id="be1c9-180">Vytvoření instance aplikace Internet Explorer tak, že zadáte v Internet Exploreru ProgId, **InternetExplorer.Application**:</span><span class="sxs-lookup"><span data-stu-id="be1c9-180">You create an Internet Explorer instance by specifying the Internet Explorer ProgId, **InternetExplorer.Application**:</span></span>

```
$ie = New-Object -ComObject InternetExplorer.Application
```

<span data-ttu-id="be1c9-181">Tento příkaz spustí aplikaci Internet Explorer, ale není zviditelnit.</span><span class="sxs-lookup"><span data-stu-id="be1c9-181">This command starts Internet Explorer, but does not make it visible.</span></span> <span data-ttu-id="be1c9-182">Pokud zadáte Get-Process, uvidíte, že proces s názvem iexplore běží.</span><span class="sxs-lookup"><span data-stu-id="be1c9-182">If you type Get-Process, you can see that a process named iexplore is running.</span></span> <span data-ttu-id="be1c9-183">Ve skutečnosti Pokud ukončení prostředí Windows PowerShell, proces bude nadále spouštět.</span><span class="sxs-lookup"><span data-stu-id="be1c9-183">In fact, if you exit Windows PowerShell, the process will continue to run.</span></span> <span data-ttu-id="be1c9-184">Musíte restartovat počítač nebo použít nástroj podobně jako u Správce úloh ukončit proces iexplore.</span><span class="sxs-lookup"><span data-stu-id="be1c9-184">You must reboot the computer or use a tool like Task Manager to end the iexplore process.</span></span>

> [!NOTE]
> <span data-ttu-id="be1c9-185">Objekty COM, které začínají jako samostatné procesy, označovaného jako *spustitelné soubory ActiveX*, může nebo nemusí být zobrazeny okno uživatelského rozhraní při jejich spuštění.</span><span class="sxs-lookup"><span data-stu-id="be1c9-185">COM objects that start as separate processes, commonly called *ActiveX executables*, may or may not display a user interface window when they start up.</span></span> <span data-ttu-id="be1c9-186">Pokud vytvoření okna, ale není zviditelnit, jako třeba Internet Explorer, budou obecně fokus na ploše systému Windows a je nutné provést okna viditelné pracovat s ním.</span><span class="sxs-lookup"><span data-stu-id="be1c9-186">If they create a window but do not make it visible, like Internet Explorer, the focus will generally move to the Windows desktop and you must make the window visible to interact with it.</span></span>

<span data-ttu-id="be1c9-187">Zadáním **$ie | Get-člen**, můžete zobrazit vlastnosti a metody pro Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="be1c9-187">By typing **$ie | Get-Member**, you can view properties and methods for Internet Explorer.</span></span> <span data-ttu-id="be1c9-188">Pokud chcete zobrazit okno aplikace Internet Explorer, nastavte vlastnost Visible na $true zadáním:</span><span class="sxs-lookup"><span data-stu-id="be1c9-188">To see the Internet Explorer window, set the Visible property to $true by typing:</span></span>

```
$ie.Visible = $true
```

<span data-ttu-id="be1c9-189">Potom můžete přejít na konkrétní webovou adresu pomocí metody přejděte:</span><span class="sxs-lookup"><span data-stu-id="be1c9-189">You can then navigate to a specific Web address by using the Navigate method:</span></span>

```
$ie.Navigate("http://www.microsoft.com/technet/scriptcenter/default.mspx")
```

<span data-ttu-id="be1c9-190">Pomocí ostatním členům objektový model aplikace Internet Explorer, je možné načíst textový obsah z webové stránky.</span><span class="sxs-lookup"><span data-stu-id="be1c9-190">Using other members of the Internet Explorer object model, it is possible to retrieve text content from the Web page.</span></span> <span data-ttu-id="be1c9-191">Následující příkaz zobrazí text ve formátu HTML v těle aktuální webové stránky:</span><span class="sxs-lookup"><span data-stu-id="be1c9-191">The following command will display the HTML text in the body of the current Web page:</span></span>

```
$ie.Document.Body.InnerText
```

<span data-ttu-id="be1c9-192">Zavřete Internet Explorer z prostředí PowerShell, volejte příslušnou metodu Quit():</span><span class="sxs-lookup"><span data-stu-id="be1c9-192">To close Internet Explorer from within PowerShell, call its Quit() method:</span></span>

```
$ie.Quit()
```

<span data-ttu-id="be1c9-193">Tato akce vynutí ho zavřete.</span><span class="sxs-lookup"><span data-stu-id="be1c9-193">This will force it to close.</span></span> <span data-ttu-id="be1c9-194">Ie proměnné $ už neobsahuje platný odkaz, i když stále se zdá, že se objekt COM.</span><span class="sxs-lookup"><span data-stu-id="be1c9-194">The $ie variable no longer contains a valid reference even though it still appears to be a COM object.</span></span> <span data-ttu-id="be1c9-195">Pokud se pokusíte použít, obdržíte chybu automatizace:</span><span class="sxs-lookup"><span data-stu-id="be1c9-195">If you attempt to use it, you will get an automation error:</span></span>

```
PS> $ie | Get-Member
Get-Member : Exception retrieving the string representation for property "Appli
cation" : "The object invoked has disconnected from its clients. (Exception fro
m HRESULT: 0x80010108 (RPC_E_DISCONNECTED))"
At line:1 char:16
+ $ie | Get-Member <<<<
```

<span data-ttu-id="be1c9-196">Můžete buď odstranit zbývající odkazovat pomocí příkazu jako $ie = $null nebo úplně odebrat proměnnou zadáním:</span><span class="sxs-lookup"><span data-stu-id="be1c9-196">You can either remove the remaining reference with a command like $ie = $null, or completely remove the variable by typing:</span></span>

```
Remove-Variable ie
```

> [!NOTE]
> <span data-ttu-id="be1c9-197">Neexistuje žádné běžný standard pro jestli spustitelné soubory ActiveX ukončit nebo pokračovat v běhu při odebrání odkaz na jednu.</span><span class="sxs-lookup"><span data-stu-id="be1c9-197">There is no common standard for whether ActiveX executables exit or continue to run when you remove a reference to one.</span></span> <span data-ttu-id="be1c9-198">V závislosti na případech, například zda je aplikace viditelné, jestli je v něm spuštěný upravený dokument a i jestli prostředí Windows PowerShell je stále spuštěná aplikace může nebo nemusí ukončit.</span><span class="sxs-lookup"><span data-stu-id="be1c9-198">Depending on circumstances such as whether the application is visible, whether an edited document is running in it, and even whether Windows PowerShell is still running, the application may or may not exit.</span></span> <span data-ttu-id="be1c9-199">Z tohoto důvodu byste měli otestovat chování při ukončení pro každý ActiveX spustitelného souboru, že kterou chcete použít v prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="be1c9-199">For this reason, you should test termination behavior for each ActiveX executable you want to use in Windows PowerShell.</span></span>

### <a name="getting-warnings-about-net-framework-wrapped-com-objects"></a><span data-ttu-id="be1c9-200">Získávání upozornění o rozhraní .NET Framework zabalené COM – objekty</span><span class="sxs-lookup"><span data-stu-id="be1c9-200">Getting Warnings About .NET Framework-Wrapped COM Objects</span></span>
<span data-ttu-id="be1c9-201">V některých případech může mít objekt COM přidružené rozhraní .NET Framework *obálka volatelná za běhu* nebo RCW a tím se použije **New-Object**.</span><span class="sxs-lookup"><span data-stu-id="be1c9-201">In some cases, a COM object might have an associated .NET Framework *Runtime-Callable Wrapper* or RCW, and this will be used by **New-Object**.</span></span> <span data-ttu-id="be1c9-202">Vzhledem k tomu, že chování RCW se může lišit od chování normální objektu COM **New-Object** má **Strict** parametru informují o RCW přístup.</span><span class="sxs-lookup"><span data-stu-id="be1c9-202">Since the behavior of the RCW may be different from the behavior of the normal COM object, **New-Object** has a **Strict** parameter to warn you about RCW access.</span></span> <span data-ttu-id="be1c9-203">Pokud zadáte **Strict** parametr a potom vytvoříte objekt modelu COM, který se používá RCW, zobrazí zprávu s upozorněním:</span><span class="sxs-lookup"><span data-stu-id="be1c9-203">If you specify the **Strict** parameter and then create a COM object that uses an RCW, you get a warning message:</span></span>

```
PS> $xl = New-Object -ComObject Excel.Application -Strict
New-Object : The object written to the pipeline is an instance of the type "Mic
rosoft.Office.Interop.Excel.ApplicationClass" from the component's primary inte
rop assembly. If this type exposes different members than the IDispatch members
, scripts written to work with this object might not work if the primary intero
p assembly is not installed.
At line:1 char:17
+ $xl = New-Object  <<<< -ComObject Excel.Application -Strict
```

<span data-ttu-id="be1c9-204">I když je objekt stále vytvořen, budete upozorněni, že se nejedná o standardní objektu COM.</span><span class="sxs-lookup"><span data-stu-id="be1c9-204">Although the object is still created, you are warned that it is not a standard COM object.</span></span>

