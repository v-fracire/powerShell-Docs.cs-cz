---
ms.date: 06/05/2017
keywords: rutiny prostředí PowerShell
title: Vytváření objektů .NET a COM nový objekt
ms.assetid: 2057b113-efeb-465e-8b44-da2f20dbf603
ms.openlocfilehash: 1ffd8d4afa419ec0c24321e44aa4a2f41a9bee44
ms.sourcegitcommit: 00ff76d7d9414fe585c04740b739b9cf14d711e1
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/14/2018
ms.locfileid: "53404109"
---
# <a name="creating-net-and-com-objects-new-object"></a><span data-ttu-id="3830d-103">Vytváření objektů .NET a COM (New-Object)</span><span class="sxs-lookup"><span data-stu-id="3830d-103">Creating .NET and COM Objects (New-Object)</span></span>

<span data-ttu-id="3830d-104">Existují softwarové komponenty pomocí rozhraní .NET Framework a modelu COM, které vám umožní provádět mnoho úkolů správy systému.</span><span class="sxs-lookup"><span data-stu-id="3830d-104">There are software components with .NET Framework and COM interfaces that enable you to perform many system administration tasks.</span></span> <span data-ttu-id="3830d-105">Prostředí Windows PowerShell vám umožní používat tyto komponenty, takže nejste omezeni na úlohy, které lze provádět pomocí rutin.</span><span class="sxs-lookup"><span data-stu-id="3830d-105">Windows PowerShell lets you use these components, so you are not limited to the tasks that can be performed by using cmdlets.</span></span> <span data-ttu-id="3830d-106">Mnoho rutin v počáteční verzi Windows Powershellu nebudou fungovat na vzdálených počítačích.</span><span class="sxs-lookup"><span data-stu-id="3830d-106">Many of the cmdlets in the initial release of Windows PowerShell do not work against remote computers.</span></span> <span data-ttu-id="3830d-107">Můžeme vám ukáže, jak získat vyhnout uvedeným potížím při správě protokolů událostí s použitím rozhraní .NET Framework **System.Diagnostics.EventLog** třídy přímo z prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3830d-107">We will demonstrate how to get around this limitation when managing event logs by using the .NET Framework **System.Diagnostics.EventLog** class directly from Windows PowerShell.</span></span>

### <a name="using-new-object-for-event-log-access"></a><span data-ttu-id="3830d-108">Pomocí nového objektu pro přístup k protokolu událostí</span><span class="sxs-lookup"><span data-stu-id="3830d-108">Using New-Object for Event Log Access</span></span>

<span data-ttu-id="3830d-109">Knihovny tříd rozhraní .NET Framework obsahuje třídu s názvem **System.Diagnostics.EventLog** , který lze použít ke správě protokolů událostí.</span><span class="sxs-lookup"><span data-stu-id="3830d-109">The .NET Framework Class Library includes a class named **System.Diagnostics.EventLog** that can be used to manage event logs.</span></span> <span data-ttu-id="3830d-110">Můžete vytvořit novou instanci třídy rozhraní .NET Framework pomocí **New-Object** rutinu s **TypeName** parametru.</span><span class="sxs-lookup"><span data-stu-id="3830d-110">You can create a new instance of a .NET Framework class by using the **New-Object** cmdlet with the **TypeName** parameter.</span></span> <span data-ttu-id="3830d-111">Například následující příkaz vytvoří odkaz na protokol událostí:</span><span class="sxs-lookup"><span data-stu-id="3830d-111">For example, the following command creates an event log reference:</span></span>

```
PS> New-Object -TypeName System.Diagnostics.EventLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
```

<span data-ttu-id="3830d-112">I když příkaz vytvořil instanci třídy protokolu událostí, instance neobsahuje žádná data.</span><span class="sxs-lookup"><span data-stu-id="3830d-112">Although the command has created an instance of the EventLog class, the instance does not include any data.</span></span> <span data-ttu-id="3830d-113">Důvodem je, jsme nezadali určitý protokol událostí.</span><span class="sxs-lookup"><span data-stu-id="3830d-113">That is because we did not specify a particular event log.</span></span> <span data-ttu-id="3830d-114">Jak můžete získat skutečný protokolu událostí?</span><span class="sxs-lookup"><span data-stu-id="3830d-114">How do you get a real event log?</span></span>

#### <a name="using-constructors-with-new-object"></a><span data-ttu-id="3830d-115">Použití konstruktorů s New-Object</span><span class="sxs-lookup"><span data-stu-id="3830d-115">Using Constructors with New-Object</span></span>

<span data-ttu-id="3830d-116">K odkazování na určitém protokolu událostí, musíte zadat název protokolu.</span><span class="sxs-lookup"><span data-stu-id="3830d-116">To refer to a specific event log, you need to specify the name of the log.</span></span> <span data-ttu-id="3830d-117">**Nový objekt** má **Seznam_argumentů** parametru.</span><span class="sxs-lookup"><span data-stu-id="3830d-117">**New-Object** has an **ArgumentList** parameter.</span></span> <span data-ttu-id="3830d-118">Argumenty, které můžete předat jako hodnoty pro tento parametr používá speciální po spuštění metody objektu.</span><span class="sxs-lookup"><span data-stu-id="3830d-118">The arguments you pass as values to this parameter are used by a special startup method of the object.</span></span> <span data-ttu-id="3830d-119">Metoda je volána *konstruktor* vzhledem k tomu, že se používá ke konstrukci objektu.</span><span class="sxs-lookup"><span data-stu-id="3830d-119">The method is called a *constructor* because it is used to construct the object.</span></span> <span data-ttu-id="3830d-120">Třeba získat odkaz na aplikaci protokolu, zadejte řetězec "Aplikace" jako argument:</span><span class="sxs-lookup"><span data-stu-id="3830d-120">For example, to get a reference to the Application log, you specify the string 'Application' as an argument:</span></span>

```
PS> New-Object -TypeName System.Diagnostics.EventLog -ArgumentList Application

Max(K) Retain OverflowAction        Entries Name
------ ------ --------------        ------- ----
16,384      7 OverwriteOlder          2,160 Application
```

> [!NOTE]
> <span data-ttu-id="3830d-121">Protože většina základních tříd rozhraní .NET Framework jsou obsaženy v oboru názvů System, prostředí Windows PowerShell se automaticky pokusí vyhledat třídy, které zadáte v oboru názvů System, pokud nemůže najít shoda pro název typu, který zadáte.</span><span class="sxs-lookup"><span data-stu-id="3830d-121">Since most of the .NET Framework core classes are contained in the System namespace, Windows PowerShell will automatically attempt to find classes you specify in the System namespace if it cannot find a match for the typename you specify.</span></span> <span data-ttu-id="3830d-122">To znamená, že je možné zadat Diagnostics.EventLog místo System.Diagnostics.EventLog.</span><span class="sxs-lookup"><span data-stu-id="3830d-122">This means that you can specify Diagnostics.EventLog instead of System.Diagnostics.EventLog.</span></span>

#### <a name="storing-objects-in-variables"></a><span data-ttu-id="3830d-123">Ukládání objektů v proměnných</span><span class="sxs-lookup"><span data-stu-id="3830d-123">Storing Objects in Variables</span></span>

<span data-ttu-id="3830d-124">Může být vhodné k uložení odkazu na objekt, takže ho můžete použít v aktuálním prostředí.</span><span class="sxs-lookup"><span data-stu-id="3830d-124">You might want to store a reference to an object, so you can use it in the current shell.</span></span> <span data-ttu-id="3830d-125">I když se prostředí Windows PowerShell umožňuje provádět spoustu práce s kanály, lessening potřebu proměnné, někdy ukládání odkazů na objekty v proměnné umožňuje efektivněji pracovat s těmito objekty.</span><span class="sxs-lookup"><span data-stu-id="3830d-125">Although Windows PowerShell lets you do a lot of work with pipelines, lessening the need for variables, sometimes storing references to objects in variables makes it more convenient to manipulate those objects.</span></span>

<span data-ttu-id="3830d-126">Prostředí Windows PowerShell umožňuje vytvářet proměnné, které jsou v podstatě pojmenované objekty.</span><span class="sxs-lookup"><span data-stu-id="3830d-126">Windows PowerShell lets you create variables that are essentially named objects.</span></span> <span data-ttu-id="3830d-127">Výstup z jakékoli platný příkaz prostředí Windows PowerShell lze uložit do proměnné.</span><span class="sxs-lookup"><span data-stu-id="3830d-127">The output from any valid Windows PowerShell command can be stored in a variable.</span></span> <span data-ttu-id="3830d-128">Proměnné názvy vždy začínají znakem $.</span><span class="sxs-lookup"><span data-stu-id="3830d-128">Variable names always begin with $.</span></span> <span data-ttu-id="3830d-129">Pokud chcete uložit do proměnné s názvem $AppLog referenční informace k protokolům aplikace, zadejte název proměnné, za nímž následuje znaménko rovná se a zadejte příkaz použít k vytvoření objektu protokolu aplikace:</span><span class="sxs-lookup"><span data-stu-id="3830d-129">If you want to store the Application log reference in a variable named $AppLog, type the name of the variable, followed by an equal sign and then type the command used to create the Application log object:</span></span>

```
PS> $AppLog = New-Object -TypeName System.Diagnostics.EventLog -ArgumentList Application
```

<span data-ttu-id="3830d-130">Zadejte $AppLog uvidíte, že obsahuje protokolu aplikace:</span><span class="sxs-lookup"><span data-stu-id="3830d-130">If you then type $AppLog, you can see that it contains the Application log:</span></span>

```
PS> $AppLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
  16,384      7 OverwriteOlder          2,160 Application
```

#### <a name="accessing-a-remote-event-log-with-new-object"></a><span data-ttu-id="3830d-131">Přístup k vzdálené protokolu událostí s New-Object</span><span class="sxs-lookup"><span data-stu-id="3830d-131">Accessing a Remote Event Log with New-Object</span></span>

<span data-ttu-id="3830d-132">Příkazy v předchozí části cílit na místní počítač; **Get-EventLog** rutiny, které můžete provést.</span><span class="sxs-lookup"><span data-stu-id="3830d-132">The commands used in the preceding section target the local computer; the **Get-EventLog** cmdlet can do that.</span></span> <span data-ttu-id="3830d-133">Pro přístup k protokolu aplikací ve vzdáleném počítači, musíte zadat jak název protokolu a název počítače (nebo IP adresu) jako argumenty.</span><span class="sxs-lookup"><span data-stu-id="3830d-133">To access the Application log on a remote computer, you must supply both the log name and a computer name (or IP address) as arguments.</span></span>

```
PS> $RemoteAppLog = New-Object -TypeName System.Diagnostics.EventLog Application,192.168.1.81
PS> $RemoteAppLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
     512      7 OverwriteOlder            262 Application
```

<span data-ttu-id="3830d-134">Když teď máme odkaz na protokol událostí, který je uložen v proměnné $RemoteAppLog, jaké úkoly jsme provádět v něm?</span><span class="sxs-lookup"><span data-stu-id="3830d-134">Now that we have a reference to an event log stored in the $RemoteAppLog variable, what tasks can we perform on it?</span></span>

#### <a name="clearing-an-event-log-with-object-methods"></a><span data-ttu-id="3830d-135">Vymazání protokolu událostí s objektových metod</span><span class="sxs-lookup"><span data-stu-id="3830d-135">Clearing an Event Log with Object Methods</span></span>

<span data-ttu-id="3830d-136">Objekty často mají metody, které lze volat pro provádění úloh.</span><span class="sxs-lookup"><span data-stu-id="3830d-136">Objects often have methods that can be called to perform tasks.</span></span> <span data-ttu-id="3830d-137">Můžete použít **Get-Member** zobrazíte metody přidružené k objektu.</span><span class="sxs-lookup"><span data-stu-id="3830d-137">You can use **Get-Member** to display the methods associated with an object.</span></span> <span data-ttu-id="3830d-138">Následující příkaz a vybrané výstupní představují některé metody třídy událostí:</span><span class="sxs-lookup"><span data-stu-id="3830d-138">The following command and selected output show some the methods of the EventLog class:</span></span>

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

<span data-ttu-id="3830d-139">**Clear()** metodu je možné vymazat protokol událostí.</span><span class="sxs-lookup"><span data-stu-id="3830d-139">The **Clear()** method can be used to clear the event log.</span></span> <span data-ttu-id="3830d-140">Při volání metody, je nutné provést název metody v závorkách, i v případě, že metoda nevyžaduje argumenty.</span><span class="sxs-lookup"><span data-stu-id="3830d-140">When calling a method, you must always follow the method name by parentheses, even if the method does not require arguments.</span></span> <span data-ttu-id="3830d-141">Díky tomu prostředí Windows PowerShell rozlišovat mezi metodu a potenciální vlastnost se stejným názvem.</span><span class="sxs-lookup"><span data-stu-id="3830d-141">This lets Windows PowerShell distinguish between the method and a potential property with the same name.</span></span> <span data-ttu-id="3830d-142">Zadejte následující příkaz pro volání **vymazat** metody:</span><span class="sxs-lookup"><span data-stu-id="3830d-142">Type the following to call the **Clear** method:</span></span>

```
PS> $RemoteAppLog.Clear()
```

<span data-ttu-id="3830d-143">Zadejte následující příkaz pro zobrazení protokolu.</span><span class="sxs-lookup"><span data-stu-id="3830d-143">Type the following to display the log.</span></span> <span data-ttu-id="3830d-144">Uvidíte, že byl vymazán. v protokolu událostí a teď má 0 položek místo 262:</span><span class="sxs-lookup"><span data-stu-id="3830d-144">You will see that the event log was cleared, and now has 0 entries instead of 262:</span></span>

```
PS> $RemoteAppLog

  Max(K) Retain OverflowAction        Entries Name
  ------ ------ --------------        ------- ----
     512      7 OverwriteOlder              0 Application
```

### <a name="creating-com-objects-with-new-object"></a><span data-ttu-id="3830d-145">Vytváření objektů COM pomocí New-Object</span><span class="sxs-lookup"><span data-stu-id="3830d-145">Creating COM Objects with New-Object</span></span>
<span data-ttu-id="3830d-146">Můžete použít **New-Object** pro práci s komponenty modelu COM (Component Object).</span><span class="sxs-lookup"><span data-stu-id="3830d-146">You can use **New-Object** to work with Component Object Model (COM) components.</span></span> <span data-ttu-id="3830d-147">Součásti v rozsahu od různé knihovny zahrnuté do ActiveX aplikací, jako je například Internet Explorer, které jsou nainstalovány ve většině systémů Windows Script Host (WSH).</span><span class="sxs-lookup"><span data-stu-id="3830d-147">Components range from the various libraries included with Windows Script Host (WSH) to ActiveX applications such as Internet Explorer that are installed on most systems.</span></span>

<span data-ttu-id="3830d-148">**Nový objekt** používá rozhraní .NET Framework Runtime – obálky s možností k vytváření objektů modelu COM, tak má stejné omezení, které rozhraní .NET Framework při volání metody COM objekty.</span><span class="sxs-lookup"><span data-stu-id="3830d-148">**New-Object** uses .NET Framework Runtime-Callable Wrappers to create COM objects, so it has the same limitations that .NET Framework does when calling COM objects.</span></span> <span data-ttu-id="3830d-149">Chcete-li vytvořit objekt modelu COM, je třeba zadat **ComObject** parametr s programový identifikátor nebo *ProgId* třídy modelu COM, kterou chcete použít.</span><span class="sxs-lookup"><span data-stu-id="3830d-149">To create a COM object, you need to specify the **ComObject** parameter with the Programmatic Identifier or *ProgId* of the COM class you want to use.</span></span> <span data-ttu-id="3830d-150">Úplné informace o omezení použití modelu COM a určení, jaké jsou k dispozici v systému ProgID je nad rámec tohoto průvodce, ale dobře známým objektům z prostředí, jako je prostředí WSH lze použít v prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3830d-150">A complete discussion of the limitations of COM use and determining what ProgIds are available on a system is beyond the scope of this user's guide, but most well-known objects from environments such as WSH can be used within Windows PowerShell.</span></span>

<span data-ttu-id="3830d-151">Můžete vytvořit prostředí WSH objekty tak, že zadáte tyto ProgID: **WScript.Shell**, **WScript.Network**, **Scripting.Dictionary**, a **Scripting.FileSystemObject**.</span><span class="sxs-lookup"><span data-stu-id="3830d-151">You can create the WSH objects by specifying these progids: **WScript.Shell**, **WScript.Network**, **Scripting.Dictionary**, and **Scripting.FileSystemObject**.</span></span> <span data-ttu-id="3830d-152">Následující příkazy vytvoří tyto objekty:</span><span class="sxs-lookup"><span data-stu-id="3830d-152">The following commands create these objects:</span></span>

```powershell
New-Object -ComObject WScript.Shell
New-Object -ComObject WScript.Network
New-Object -ComObject Scripting.Dictionary
New-Object -ComObject Scripting.FileSystemObject
```

<span data-ttu-id="3830d-153">Přestože většinu funkcí těchto tříd je k dispozici jiným způsobem v prostředí Windows PowerShell, jsou stále snazší používání tříd prostředí WSH několik úloh, jako je například vytváření zástupce.</span><span class="sxs-lookup"><span data-stu-id="3830d-153">Although most of the functionality of these classes is made available in other ways in Windows PowerShell, a few tasks such as shortcut creation are still easier to do using the WSH classes.</span></span>

### <a name="creating-a-desktop-shortcut-with-wscriptshell"></a><span data-ttu-id="3830d-154">Vytvoření zástupce na ploše pomocí WScript.Shell</span><span class="sxs-lookup"><span data-stu-id="3830d-154">Creating a Desktop Shortcut with WScript.Shell</span></span>

<span data-ttu-id="3830d-155">Jeden úkol, který můžete rychle provést pomocí objektu COM je vytvoření zástupce.</span><span class="sxs-lookup"><span data-stu-id="3830d-155">One task that can be performed quickly with a COM object is creating a shortcut.</span></span> <span data-ttu-id="3830d-156">Předpokládejme, že chcete vytvořit zástupce na ploše, který odkazuje na domovskou složku pro prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3830d-156">Suppose you want to create a shortcut on your desktop that links to the home folder for Windows PowerShell.</span></span> <span data-ttu-id="3830d-157">Nejprve musíte vytvořit odkaz na **WScript.Shell**, kterém jsme se uloží do proměnné s názvem **$WshShell**:</span><span class="sxs-lookup"><span data-stu-id="3830d-157">You first need to create a reference to **WScript.Shell**, which we will store in a variable named **$WshShell**:</span></span>

```powershell
$WshShell = New-Object -ComObject WScript.Shell
```

<span data-ttu-id="3830d-158">Get-Member funguje s objekty COM, abyste mohli zkoumat členy objektu tak, že zadáte:</span><span class="sxs-lookup"><span data-stu-id="3830d-158">Get-Member works with COM objects, so you can explore the members of the object by typing:</span></span>

```
PS> $WshShell | Get-Member

   TypeName: System.__ComObject#{41904400-be18-11d3-a28b-00104bd35090}

Name                     MemberType            Definition
----                     ----------            ----------
AppActivate              Method                bool AppActivate (Variant, Va...
CreateShortcut           Method                IDispatch CreateShortcut (str...
...
```

<span data-ttu-id="3830d-159">**Get-Member** má volitelnou **InputObject** parametr, můžete místo zřetězení příkazů k zadání **Get-Member**.</span><span class="sxs-lookup"><span data-stu-id="3830d-159">**Get-Member** has an optional **InputObject** parameter you can use instead of piping to provide input to **Get-Member**.</span></span> <span data-ttu-id="3830d-160">Byste získali stejný výstup, jak je znázorněno výše, pokud jste místo toho použili příkaz **Get-Member - InputObject $WshShell**.</span><span class="sxs-lookup"><span data-stu-id="3830d-160">You would get the same output as shown above if you instead used the command **Get-Member -InputObject $WshShell**.</span></span> <span data-ttu-id="3830d-161">Pokud používáte **InputObject**, zpracovává svůj argument jako jednu položku.</span><span class="sxs-lookup"><span data-stu-id="3830d-161">If you use **InputObject**, it treats its argument as a single item.</span></span> <span data-ttu-id="3830d-162">To znamená, že pokud máte několik objektů v proměnné, **Get-Member** je zpracovává jako pole objektů.</span><span class="sxs-lookup"><span data-stu-id="3830d-162">This means that if you have several objects in a variable, **Get-Member** treats them as an array of objects.</span></span> <span data-ttu-id="3830d-163">Příklad:</span><span class="sxs-lookup"><span data-stu-id="3830d-163">For example:</span></span>

```
PS> $a = 1,2,"three"
PS> Get-Member -InputObject $a
TypeName: System.Object[]
Name               MemberType    Definition
----               ----------    ----------
Count              AliasProperty Count = Length
...
```

<span data-ttu-id="3830d-164">**WScript.Shell CreateShortcut** metoda přijímá jeden argument, cesta k souboru zástupce k vytvoření.</span><span class="sxs-lookup"><span data-stu-id="3830d-164">The **WScript.Shell CreateShortcut** method accepts a single argument, the path to the shortcut file to create.</span></span> <span data-ttu-id="3830d-165">Jsme mohli zadejte úplnou cestu k pracovní ploše, ale je snadnější.</span><span class="sxs-lookup"><span data-stu-id="3830d-165">We could type in the full path to the desktop, but there is an easier way.</span></span> <span data-ttu-id="3830d-166">Ploše obvykle představuje složku s názvem Desktopu uvnitř domovskou složku aktuálního uživatele.</span><span class="sxs-lookup"><span data-stu-id="3830d-166">The desktop is normally represented by a folder named Desktop inside the home folder of the current user.</span></span> <span data-ttu-id="3830d-167">Prostředí Windows PowerShell obsahuje proměnnou s **$Home** , který obsahuje cestu k této složce.</span><span class="sxs-lookup"><span data-stu-id="3830d-167">Windows PowerShell has a variable **$Home** that contains the path to this folder.</span></span> <span data-ttu-id="3830d-168">Můžeme zadat cestu k domovské složky pomocí této proměnné a pak přidejte název složky Desktop a název zástupce vytvořit zadáním:</span><span class="sxs-lookup"><span data-stu-id="3830d-168">We can specify the path to the home folder by using this variable, and then add the name of the Desktop folder and the name for the shortcut to create by typing:</span></span>

```powershell
$lnk = $WshShell.CreateShortcut("$Home\Desktop\PSHome.lnk")
```

<span data-ttu-id="3830d-169">Pokud používáte něco, co vypadá jako název proměnné v uvozovkách, prostředí Windows PowerShell se pokusí nahradit odpovídající hodnotu.</span><span class="sxs-lookup"><span data-stu-id="3830d-169">When you use something that looks like a variable name inside double-quotes, Windows PowerShell tries to substitute a matching value.</span></span> <span data-ttu-id="3830d-170">Pokud používáte nabídek jedním, nepokusí se k nahrazení hodnoty proměnné prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3830d-170">If you use single-quotes, Windows PowerShell does not try to substitute the variable value.</span></span> <span data-ttu-id="3830d-171">Zkuste například zadat následující příkazy:</span><span class="sxs-lookup"><span data-stu-id="3830d-171">For example, try typing the following commands:</span></span>

```
PS> "$Home\Desktop\PSHome.lnk"
C:\Documents and Settings\aka\Desktop\PSHome.lnk
PS> '$Home\Desktop\PSHome.lnk'
$Home\Desktop\PSHome.lnk
```

<span data-ttu-id="3830d-172">Teď máme proměnnou s názvem **$lnk** , který obsahuje nový odkaz na místní.</span><span class="sxs-lookup"><span data-stu-id="3830d-172">We now have a variable named **$lnk** that contains a new shortcut reference.</span></span> <span data-ttu-id="3830d-173">Pokud chcete zobrazit jejích členů, můžete zřetězit ho do **Get-Member**.</span><span class="sxs-lookup"><span data-stu-id="3830d-173">If you want to see its members, you can pipe it to **Get-Member**.</span></span> <span data-ttu-id="3830d-174">Následující výstup zobrazí členy, že musíme použít k dokončení vytvoření náš zástupce:</span><span class="sxs-lookup"><span data-stu-id="3830d-174">The output below shows the members we need to use to finish creating our shortcut:</span></span>

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

<span data-ttu-id="3830d-175">Budeme muset zadat **TargetPath**, což je složka aplikace pro Windows PowerShell a uložit místní **$lnk** voláním **Uložit** metody.</span><span class="sxs-lookup"><span data-stu-id="3830d-175">We need to specify the **TargetPath**, which is the application folder for Windows PowerShell, and then save the shortcut **$lnk** by calling the **Save** method.</span></span> <span data-ttu-id="3830d-176">Cesta ke složce aplikace prostředí Windows PowerShell je uložen v proměnné **$PSHome**, takže můžeme to udělat tak, že zadáte:</span><span class="sxs-lookup"><span data-stu-id="3830d-176">The Windows PowerShell application folder path is stored in the variable **$PSHome**, so we can do this by typing:</span></span>

```powershell
$lnk.TargetPath = $PSHome
$lnk.Save()
```

### <a name="using-internet-explorer-from-windows-powershell"></a><span data-ttu-id="3830d-177">Pomocí aplikace Internet Explorer z prostředí Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="3830d-177">Using Internet Explorer from Windows PowerShell</span></span>

<span data-ttu-id="3830d-178">Mnoho aplikací (včetně Microsoft Office řady aplikací a prohlížeče Internet Explorer) je možné automatizovat pomocí modelu COM.</span><span class="sxs-lookup"><span data-stu-id="3830d-178">Many applications (including the Microsoft Office family of applications and Internet Explorer) can be automated by using COM.</span></span> <span data-ttu-id="3830d-179">Aplikace Internet Explorer ukazuje některé typické technik a problémy při práci s aplikací založených na modelu COM.</span><span class="sxs-lookup"><span data-stu-id="3830d-179">Internet Explorer illustrates some of the typical techniques and issues involved in working with COM-based applications.</span></span>

<span data-ttu-id="3830d-180">Vytvořit instanci aplikace Internet Explorer tak, že zadáte Internet Explorer ProgId, **InternetExplorer.Application**:</span><span class="sxs-lookup"><span data-stu-id="3830d-180">You create an Internet Explorer instance by specifying the Internet Explorer ProgId, **InternetExplorer.Application**:</span></span>

```powershell
$ie = New-Object -ComObject InternetExplorer.Application
```

<span data-ttu-id="3830d-181">Tento příkaz spustí aplikaci Internet Explorer, ale není viditelný.</span><span class="sxs-lookup"><span data-stu-id="3830d-181">This command starts Internet Explorer, but does not make it visible.</span></span> <span data-ttu-id="3830d-182">Pokud zadáte Get-Process, uvidíte, že proces s názvem iexplore běží.</span><span class="sxs-lookup"><span data-stu-id="3830d-182">If you type Get-Process, you can see that a process named iexplore is running.</span></span> <span data-ttu-id="3830d-183">Ve skutečnosti Pokud ukončení prostředí Windows PowerShell procesu nadále spuštěn.</span><span class="sxs-lookup"><span data-stu-id="3830d-183">In fact, if you exit Windows PowerShell, the process will continue to run.</span></span> <span data-ttu-id="3830d-184">Musíte restartovat počítač nebo použijte nástroj Správce úloh, jako je ukončit proces iexplore.</span><span class="sxs-lookup"><span data-stu-id="3830d-184">You must reboot the computer or use a tool like Task Manager to end the iexplore process.</span></span>

> [!NOTE]
> <span data-ttu-id="3830d-185">Objekty COM, které začínají jako samostatné procesy říká *spustitelné soubory ActiveX*, může nebo nemusí být zobrazeny okno uživatelského rozhraní při jejich spuštění.</span><span class="sxs-lookup"><span data-stu-id="3830d-185">COM objects that start as separate processes, commonly called *ActiveX executables*, may or may not display a user interface window when they start up.</span></span> <span data-ttu-id="3830d-186">Je-li vytvořit časové období, ale není viditelný, jako třeba Internet Explorer, budou obecně fokus na plochu Windows a je nutné provést v okně viditelné s ní pracovat.</span><span class="sxs-lookup"><span data-stu-id="3830d-186">If they create a window but do not make it visible, like Internet Explorer, the focus will generally move to the Windows desktop and you must make the window visible to interact with it.</span></span>

<span data-ttu-id="3830d-187">Zadáním **$ie | Get-Member**, můžete zobrazit vlastnosti a metody pro aplikaci Internet Explorer.</span><span class="sxs-lookup"><span data-stu-id="3830d-187">By typing **$ie | Get-Member**, you can view properties and methods for Internet Explorer.</span></span> <span data-ttu-id="3830d-188">Pokud chcete zobrazit v okně aplikace Internet Explorer, nastavení vlastnosti Visible na $true zadáním:</span><span class="sxs-lookup"><span data-stu-id="3830d-188">To see the Internet Explorer window, set the Visible property to $true by typing:</span></span>

```powershell
$ie.Visible = $true
```

<span data-ttu-id="3830d-189">Pak můžete přejít na konkrétní webovou adresu pomocí metody navigace:</span><span class="sxs-lookup"><span data-stu-id="3830d-189">You can then navigate to a specific Web address by using the Navigate method:</span></span>

```powershell
$ie.Navigate("http://www.microsoft.com/technet/scriptcenter/default.mspx")
```

<span data-ttu-id="3830d-190">Pomocí dalších členů objektový model aplikace Internet Explorer, je možné načíst textový obsah z webové stránky.</span><span class="sxs-lookup"><span data-stu-id="3830d-190">Using other members of the Internet Explorer object model, it is possible to retrieve text content from the Web page.</span></span> <span data-ttu-id="3830d-191">Následující příkaz zobrazí text ve formátu HTML v těle aktuální webové stránky:</span><span class="sxs-lookup"><span data-stu-id="3830d-191">The following command will display the HTML text in the body of the current Web page:</span></span>

```powershell
$ie.Document.Body.InnerText
```

<span data-ttu-id="3830d-192">Zavřete aplikaci Internet Explorer z v rámci prostředí PowerShell, volání metody Quit():</span><span class="sxs-lookup"><span data-stu-id="3830d-192">To close Internet Explorer from within PowerShell, call its Quit() method:</span></span>

```powershell
$ie.Quit()
```

<span data-ttu-id="3830d-193">Tato akce vynutí ho zavřete.</span><span class="sxs-lookup"><span data-stu-id="3830d-193">This will force it to close.</span></span> <span data-ttu-id="3830d-194">Přestože stále zdá být objekt modelu COM, ie proměnné $ už neobsahuje platný odkaz.</span><span class="sxs-lookup"><span data-stu-id="3830d-194">The $ie variable no longer contains a valid reference even though it still appears to be a COM object.</span></span> <span data-ttu-id="3830d-195">Při pokusu o jeho použití, obdržíte chybu služby automation:</span><span class="sxs-lookup"><span data-stu-id="3830d-195">If you attempt to use it, you will get an automation error:</span></span>

```
PS> $ie | Get-Member
Get-Member : Exception retrieving the string representation for property "Appli
cation" : "The object invoked has disconnected from its clients. (Exception fro
m HRESULT: 0x80010108 (RPC_E_DISCONNECTED))"
At line:1 char:16
+ $ie | Get-Member <<<<
```

<span data-ttu-id="3830d-196">Můžete buď odstranit zbývající odkazovat pomocí příkazu jako $, ie = $null nebo úplně odebrat proměnnou tak, že zadáte:</span><span class="sxs-lookup"><span data-stu-id="3830d-196">You can either remove the remaining reference with a command like $ie = $null, or completely remove the variable by typing:</span></span>

```powershell
Remove-Variable ie
```

> [!NOTE]
> <span data-ttu-id="3830d-197">Neexistuje žádné je běžný standard pro Určuje, zda spustitelné soubory ActiveX ukončit nebo pokračovat v běhu při odebrání odkazu na jeden.</span><span class="sxs-lookup"><span data-stu-id="3830d-197">There is no common standard for whether ActiveX executables exit or continue to run when you remove a reference to one.</span></span> <span data-ttu-id="3830d-198">V závislosti na okolnosti – třeba Určuje, zda je viditelný aplikaci, určuje, zda je spuštěna upravený dokument v něm a ještě Určuje, zda prostředí Windows PowerShell je stále spuštěna aplikace může nebo nemusí ukončete.</span><span class="sxs-lookup"><span data-stu-id="3830d-198">Depending on circumstances such as whether the application is visible, whether an edited document is running in it, and even whether Windows PowerShell is still running, the application may or may not exit.</span></span> <span data-ttu-id="3830d-199">Z tohoto důvodu byste měli otestovat chování pro každou ActiveX spustitelného souboru, že kterou chcete použít v prostředí Windows PowerShell.</span><span class="sxs-lookup"><span data-stu-id="3830d-199">For this reason, you should test termination behavior for each ActiveX executable you want to use in Windows PowerShell.</span></span>

### <a name="getting-warnings-about-net-framework-wrapped-com-objects"></a><span data-ttu-id="3830d-200">Získávání upozornění na objekty .NET Framework zabalené COM</span><span class="sxs-lookup"><span data-stu-id="3830d-200">Getting Warnings About .NET Framework-Wrapped COM Objects</span></span>

<span data-ttu-id="3830d-201">V některých případech může mít objekt modelu COM přidružené rozhraní .NET Framework *Runtime Callable Wrapper* nebo obálky RCW a tím se použije **New-Object**.</span><span class="sxs-lookup"><span data-stu-id="3830d-201">In some cases, a COM object might have an associated .NET Framework *Runtime-Callable Wrapper* or RCW, and this will be used by **New-Object**.</span></span> <span data-ttu-id="3830d-202">Protože chování Objekt RCW může lišit od chování normální objektu COM **New-Object** má **Strict** parametr upozornit RCW přístup.</span><span class="sxs-lookup"><span data-stu-id="3830d-202">Since the behavior of the RCW may be different from the behavior of the normal COM object, **New-Object** has a **Strict** parameter to warn you about RCW access.</span></span> <span data-ttu-id="3830d-203">Pokud zadáte **Strict** parametr a poté vytvoříte objekt modelu COM, který používá obálky RCW, dostanete zprávu s upozorněním:</span><span class="sxs-lookup"><span data-stu-id="3830d-203">If you specify the **Strict** parameter and then create a COM object that uses an RCW, you get a warning message:</span></span>

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

<span data-ttu-id="3830d-204">I když je objekt stále vytvořen, se zobrazí upozornění, že není standardní objekt modelu COM.</span><span class="sxs-lookup"><span data-stu-id="3830d-204">Although the object is still created, you are warned that it is not a standard COM object.</span></span>