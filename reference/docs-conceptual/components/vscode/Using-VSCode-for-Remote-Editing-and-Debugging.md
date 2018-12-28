---
title: Pro vzdálené úpravy a ladění pomocí Visual Studio Code
description: Pro vzdálené úpravy a ladění pomocí Visual Studio Code
ms.date: 08/06/2018
ms.openlocfilehash: bab1a629a7e9dafd5957cf93025abb18b8a4f326
ms.sourcegitcommit: 548547b2d5fc73e726bb9fec6175d452a351d975
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 12/20/2018
ms.locfileid: "53655503"
---
# <a name="using-visual-studio-code-for-remote-editing-and-debugging"></a>Pro vzdálené úpravy a ladění pomocí Visual Studio Code

Pro ty, které byly znáte ISE, si pravděpodobně pamatujete, aby bylo možné spustit `psedit file.ps1` z integrovaná Konzola pro otevření souborů – místních nebo vzdálených - pravým tlačítkem myši v prostředí ISE.

Jak ukázalo se, tato funkce je také k dispozici v rozšíření prostředí PowerShell pro VSCode. Tato příručka obsahuje pokyny k tomu.

## <a name="prerequisites"></a>Předpoklady

Tato příručka předpokládá, že máte:

- vzdálený prostředek (ex: virtuální počítač, kontejner), abyste měli přístup k
- Powershellu spouštěné na ně a hostitelského počítače
- VSCode a rozšíření prostředí PowerShell pro VSCode

Tato funkce funguje v prostředí Windows PowerShell a PowerShell Core.

Tato funkce funguje i při připojování ke vzdálenému počítači prostřednictvím služby WinRM, přímou službu PowerShell nebo SSH. Pokud chcete použít SSH, ale používají Windows, podívejte se [Win32 verzi SSH](https://github.com/PowerShell/Win32-OpenSSH)!

## <a name="lets-go"></a>Jdeme

V této části můžu zabývat vzdálené úpravy a ladění z mé MacBook Pro do virtuálního počítače s Ubuntu v Azure. Můžu možná nepoužívají Windows, ale **je stejný jako proces**.

### <a name="local-file-editing-with-open-editorfile"></a>Úpravy s Open-EditorFile místního souboru

Díky rozšíření prostředí PowerShell pro VSCode spuštění a integrovaná konzola Powershellu otevřít, můžeme zadat `Open-EditorFile foo.ps1` nebo `psedit foo.ps1` otevřít místní foo.ps1 souboru přímo v editoru.

![Otevřít EditorFile foo.ps1 funguje místně](https://user-images.githubusercontent.com/2644648/34895897-7c2c46ac-f79c-11e7-9410-a252aff52f13.png)

>[!NOTE]
> foo.ps1 už musí existovat.

Tady můžeme:

přidat zarážky do mřížky ![přidání zarážky na ovládací prvek](https://user-images.githubusercontent.com/2644648/34895893-7bdc38e2-f79c-11e7-8026-8ad53f9a1bad.png)

a stisknutím klávesy F5, chcete-li ladit skript prostředí PowerShell.
![ladění místní skript prostředí PowerShell](https://user-images.githubusercontent.com/2644648/34895894-7bedb874-f79c-11e7-9180-7e0dc2d02af8.png)

Při ladění, můžete pracovat s konzolou pro ladění, podívejte se na proměnné v oboru na levé straně a všechny ostatní standardní nástroje pro ladění.

### <a name="remote-file-editing-with-open-editorfile"></a>Vzdálený soubor s Open-EditorFile úpravy

Teď Pojďme na vzdálený soubor, úpravy a ladění. Postup je téměř stejný, stačí jednou z věcí, musíme nejprve – zadání naše relace prostředí PowerShell ke vzdálenému serveru.

K tomu je pro rutinu. Je volána `Enter-PSSession`.

Je watered dolů vysvětlení rutiny:

- `Enter-PSSession -ComputerName foo` Spustí relaci prostřednictvím služby WinRM
- `Enter-PSSession -ContainerId foo` a `Enter-PSSession -VmId foo` spuštění relace přes přímou službu PowerShell
- `Enter-PSSession -HostName foo` Spustí relaci pomocí protokolu SSH

Další informace o `Enter-PSSession`, podívejte se na webu docs [tady](https://docs.microsoft.com/en-us/powershell/module/microsoft.powershell.core/enter-pssession?view=powershell-6).

Můžu používat SSH pro vzdálenou komunikaci od teď předvedu ze systému macOS virtuálního počítače s Ubuntu v Azure.

Nejprve v konzole integrovaného spustíme naše Enter-PSSession. Budete vědět, že jste v relaci, protože `[something]` , zobrazí se nalevo od vaší řádku.

![Volání Enter-PSSession](https://user-images.githubusercontent.com/2644648/34895896-7c18e0bc-f79c-11e7-9b36-6f4bd0e9b0db.png)

Tady můžeme udělat přesný postup jako v případě, že jsme dříve upravovali místní skript.

1. Spustit `Open-EditorFile test.ps1` nebo `psedit test.ps1` otevřete vzdáleného `test.ps1` souboru ![Open-EditorFile test.ps1 souboru](https://user-images.githubusercontent.com/2644648/34895898-7c3e6a12-f79c-11e7-8bdf-549b591ecbcb.png)
2. Upravit soubor nebo nastavit zarážky ![Upravit a nastavit zarážky](https://user-images.githubusercontent.com/2644648/34895892-7bb68246-f79c-11e7-8c0a-c2121773afbb.png)
3. Spustit ladění (F5) vzdáleného souboru

![ladění vzdáleného souboru](https://user-images.githubusercontent.com/2644648/34895895-7c040782-f79c-11e7-93ea-47724fa5c10d.png)

To je všechno je to! Doufáme, že tento průvodce pomáhá vymazat nahoru jakékoliv otázky týkající se vzdáleného ladění a úpravy Powershellu ve VSCode.

Pokud máte jakékoli problémy, neváhejte hlásit problémy [v úložišti Githubu](http://github.com/powershell/vscode-powershell).
