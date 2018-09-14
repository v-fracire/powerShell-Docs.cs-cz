---
ms.topic: reference
keywords: rutiny prostředí PowerShell
ms.date: 12/12/2016
title: Add-PswaAuthorizationRule
schema: 2.0.0
ms.openlocfilehash: fe2b71dcfa870ba3f92484ae3fd3c45b3107a1bc
ms.sourcegitcommit: e46b868f56f359909ff7c8230b1d1770935cce0e
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 09/13/2018
ms.locfileid: "45523073"
---
# <a name="add-pswaauthorizationrule"></a>Add-PswaAuthorizationRule

## <a name="synopsis"></a>SOUHRN

Přidá nové autorizační pravidlo sada pravidel autorizace pro Windows PowerShell Web Accessu.

## <a name="syntax"></a>Syntaxe

### <a name="usergroupnamecomputergroupname"></a>UserGroupNameComputerGroupName

```
Add-PswaAuthorizationRule -ComputerGroupName <String> -ConfigurationName <String> -UserGroupName <String[]> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

### <a name="usergroupnamecomputername"></a>UserGroupNameComputerName

```
Add-PswaAuthorizationRule -ComputerName <String> -ConfigurationName <String> -UserGroupName <String[]> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

### <a name="usernamecomputergroupname"></a>UserNameComputerGroupName

```
Add-PswaAuthorizationRule [-UserName] <String[]> -ComputerGroupName <String> -ConfigurationName <String> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

### <a name="usernamecomputername"></a>UserNameComputerName

```
Add-PswaAuthorizationRule [-UserName] <String[]> [-ComputerName] <String> [-ConfigurationName] <String> [-Credential <PSCredential> ] [-Force] [-RuleName <String> ] [ <CommonParameters>]
```

## <a name="description"></a>POPIS

**Add-PswaAuthorizationRule** rutina přidá nové autorizační pravidlo do sada pravidel autorizace pro Windows PowerShell(r) Web Access.

Musíte zadat uživatelů, počítačů a prostředí Windows PowerShell koncové body pro toto pravidlo. Můžete určit uživatele a počítače jednotlivých uživatelských účtů a názvy počítačů nebo zadáním skupiny.

Pro počítač, který je připojený k doméně služby Active Directory rutina k vytvoření pravidla používá identifikátor zabezpečení (SID) počítače. Díky tomu můžete použít krátký název, plně kvalifikovaný název domény (FQDN) nebo IP adresu pro **název_počítače** na přihlašovací stránku.

Pro počítač, který není připojený k doméně služby Active Directory rutina vytvoří pravidlo s použitím názvu počítače program od správce. K úspěšnému připojení k tomuto počítači, musí koncový uživatel poskytnutí názvu počítače, v naprosto stejném tvaru v pravidle.

Pokud existuje více počítačů se stejným názvem v síti, krátký název lze přeložit na více než jednom počítači. To může vést k nejednoznačnosti při navazování připojení. Například, pokud existuje pravidlo pro počítače pracovní skupiny s názvem "*Server1*" a nový počítač s názvem *"server1.contoso.com"* je připojen k síti a bude úspěšné ověření pomocí autorizačních pravidel a Windows PowerShell Web Accessu se pokusí navázat připojení k počítači s názvem "*Server1*". Není zaručeno, že se připojení k počítači pracovní skupiny zadaný; Tento pokus se může provést v pracovní skupině nebo doméně počítač s názvem "*Server1*". Ke snížení nejednoznačnost, doporučujeme použít plně kvalifikovaný název pro cílový počítač pokaždé, když je možné vytvořit autorizační pravidlo.

Autorizační pravidla vyhodnocení primární přihlašovací pověření uživatelů Windows PowerShell Web Accessu, ne alternativní přihlašovací údaje (součástí druhou sadu pověření **volitelná nastavení připojení** část přihlašovací stránka). Příkladem naleznete v příkladu 6.

## <a name="parameters"></a>Parameters

### <a name="-computergroupname-string"></a>-ComputerGroupName \<řetězec\>

Určuje název skupiny počítačů v Active Directory Domain Services (AD DS) nebo místních skupin, na které toto pravidlo udělí přístup.

|||
|-|-|
| Aliasy                     | žádný                  |
| Povinné?                   | Hodnota TRUE                  |
| Pozice?                   | s názvem                 |
| Výchozí hodnota               | žádný                  |
| Přijmout kanálový vstup?      | True (ByPropertyName) |
| Přijímat zástupné znaky? | false                 |

### <a name="-computername-string"></a>-ComputerName \<řetězec\>

Určuje název počítače, na které toto pravidlo udělí přístup.

|||
|-|-|
| Aliasy                     | žádný                  |
| Povinné?                   | Hodnota TRUE                  |
| Pozice?                   | s názvem                 |
| Výchozí hodnota               | žádný                  |
| Přijmout kanálový vstup?      | True (ByPropertyName) |
| Přijímat zástupné znaky? | false                 |

### <a name="-configurationname-string"></a>– Při ConfigurationName \<řetězec\>

Určuje název konfigurace relace prostředí Windows PowerShell, označované také jako prostředí runspace, do které toto pravidlo udělí přístup.

|||
|-|-|
| Aliasy                     | žádný                  |
| Povinné?                   | Hodnota TRUE                  |
| Pozice?                   | s názvem                 |
| Výchozí hodnota               | žádný                  |
| Přijmout kanálový vstup?      | True (ByPropertyName) |
| Přijímat zástupné znaky? | false                 |

### <a name="-credential--pscredential"></a>-Credential \<PSCredential\>

Určuje **PSCredential** objektu pro uživatelský účet, který chcete použít ke změně Windows PowerShell Web Accessu autorizačních pravidel. Pokud nemůžete přidat tento parametr, rutina používá účet aktuálně přihlášeného uživatele. Chcete-li získat **PSCredential** objektu, který je potřeba přidat autorizační pravidla vzdáleně, spusťte [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential) rutiny.

|||
|-|-|
| Aliasy                     | žádný  |
| Povinné?                   | false |
| Pozice?                   | s názvem |
| Výchozí hodnota               | žádný  |
| Přijmout kanálový vstup?      | false |
| Přijímat zástupné znaky? | false |

### <a name="-force"></a>-Force

Vynutí spuštění příkazu, aniž by požádal uživatele o potvrzení. Kromě toho se také zobrazí výzvu k potvrzení při zadání názvu počítače jednoduché nebo krátké (jako je například název, který není název domény nebo není plně kvalifikovaný). Potvrzení je požadována z důvodu zabezpečení tak, aby jednoduchý název slouží k přidání počítače pouze v případě, že je počítač v pracovní skupině.

|||
|-|-|
| Aliasy                              | žádný                                 |
| Povinné?                            | false                                |
| Pozice?                            | s názvem                                |
| Výchozí hodnota                        | žádný                                 |
| Přijmout kanálový vstup?               | false                                |
| Přijímat zástupné znaky?          | false                                |

### <a name="-rulename-string"></a>-RuleName \<řetězec\>

Určuje popisný název pro toto pravidlo.

|||
|-|-|
| Aliasy                              | žádný                                 |
| Povinné?                            | false                                |
| Pozice?                            | s názvem                                |
| Výchozí hodnota                        | žádný                                 |
| Přijmout kanálový vstup?               | True (ByPropertyName)                |
| Přijímat zástupné znaky?          | false                                |

### <a name="-usergroupname-string"></a>-UserGroupName \<řetězec\[\]\>

Určuje název jedné nebo víc skupin uživatelů ve službě AD DS nebo místních skupin, na které toto pravidlo udělí přístup.

|||
|-|-|
| Aliasy                              | žádný                                 |
| Povinné?                            | Hodnota TRUE                                 |
| Pozice?                            | s názvem                                |
| Výchozí hodnota                        | žádný                                 |
| Přijmout kanálový vstup?               | True (ByPropertyName)                |
| Přijímat zástupné znaky?          | false                                |

### <a name="-username-string"></a>-UserName \<řetězec\[\]\>

Určuje jeden nebo více uživatelů, na které toto pravidlo udělí přístup. Uživatelské jméno může být místní uživatelský účet na počítači brány nebo uživatel ve službě AD DS. Formát je `domain\user` nebo `computer\user`.

|||
|-|-|
| Aliasy                              | žádný                                 |
| Povinné?                            | Hodnota TRUE                                 |
| Pozice?                            | 1                                    |
| Výchozí hodnota                        | žádný                                 |
| Přijmout kanálový vstup?               | True (ByValue, ByPropertyName)       |
| Přijímat zástupné znaky?          | false                                |

###  <a name="commonparameters"></a>\<CommonParameters\>

Tato rutina podporuje běžné parametry:

-Verbose, -Debug, -ErrorAction, -ErrorVariable, -OutBuffer a -OutVariable.
Další informace najdete v tématu [about_CommonParameters](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/about/about_commonparameters).

## <a name="inputs"></a>VSTUPY

### <a name="string"></a>Řetězec

Tato rutina akceptuje jako vstupní řetězec nebo pole řetězců.

### <a name="string"></a>Řetězec\[\]

Tato rutina akceptuje jako vstupní řetězec nebo pole řetězců.

## <a name="outputs"></a>Výstupy

### <a name="microsoftmanagementpowershellwebaccesspswaauthorizationrule"></a>Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule

Tato rutina vrátí objektu pravidla autorizace.

## <a name="examples"></a>PŘÍKLADY

### <a name="example-1"></a>PŘÍKLAD 1

Tento příklad uděluje přístup ke konfiguraci relace _Pswakoncovybod_, omezuje prostředí runspace _srv2_ pro uživatele v _SMAdmins_ skupiny.

> [!NOTE]
> Název počítače musí být plně kvalifikovaný název domény (FQDN). Správci definují konfiguraci relace s omezeným přístupem nebo prostředí runspace, což je omezeným rozsahem rutin a úloh, které koncoví uživatelé můžou spouštět. Definování omezeném prostředí runspace můžete zabránit uživatelům v přístupu k jiným počítačům, které nejsou v povolených prostředí runspace Windows PowerShell(r), což zajišťuje bezpečnější připojení. Další informace o konfiguracích relace najdete v tématu [about_Session_Configurations](/powershell/module/microsoft.powershell.core/about/about_session_configurations) nebo [instalace a používání Windows PowerShell Web Accessu](../install-and-use-windows-powershell-web-access.md).

```powershell
Add-PswaAuthorizationRule -ComputerName srv2.contoso.com -UserGroupName contoso\SMAdmins -ConfigurationName PSWAEndpoint
```

### <a name="example-2"></a>PŘÍKLAD 2

Tento příklad uděluje přístup k výchozí konfiguraci relace prostředí Windows PowerShell `Microsoft.PowerShell`na *srv2* pro uživatele v uživatelů s názvem `contoso\user1`, `contoso\user2`, a `contoso\user3`. Tato rutina vytvoří tři pravidla (1 na osobu).

```powershell
Add-PswaAuthorizationRule -UserName contoso\user1, contoso\user2, contoso\user3 -ComputerName srv2.contoso.com -ConfigurationName Microsoft.PowerShell
```

### <a name="example-3"></a>PŘÍKLAD 3

Tento příklad ukazuje, jak vstupní hodnoty název uživatele prostřednictvím kanálu.

```powershell
"contoso\user1","contoso\user2" | Add-pswaAuthorizationRule -ComputerName srv2.contoso.com -ConfigurationName Microsoft.PowerShell
```

### <a name="example-4"></a>PŘÍKLAD 4:

Tento příklad ukazuje, jak všechny parametry v této hodnoty z kanálu název vlastnosti.

````powershell
$o = New-Object -TypeName PSObject |
    Add-Member -Type NoteProperty -Name "UserName" -Value "contoso\user1" -PassThru |
    Add-Member -Type NoteProperty -Name "ComputerName" -Value "srv2.contoso.com" -PassThru |
    Add-Member -Type NoteProperty -Name "ConfigurationName" -Value "Microsoft.PowerShell" -PassThru

$o | Add-PswaAuthorizationRule -UserName contoso\user1 -ConfigurationName Microsoft.PowerShell
````

### <a name="example-5"></a>PŘÍKLAD 5

V tomto příkladu přidá pravidla povolení místního uživatele s názvem `PswaServer\ChrisLocal` přístup k serveru s názvem **srv1.contoso.com**.

Tento příklad ukazuje scénář, ve kterém je brána v pracovní skupině a cílový počítač nachází v doméně. Autorizační pravidlo platí pro místní uživatele v bráně. Na Windows PowerShell Web Accessu přihlašovací stránku k ověření úspěšně, uživatel musí zadat druhou sadu pověření v **volitelná nastavení připojení** oblasti. Server brány použije další sadu pověření pro ověření uživatele v cílovém počítači, serveru s názvem *srv1.contoso.com*.

````powershell
Add-PswaAuthorizationRule -UserName PswaServer\ChrisLocal -ComputerName srv1.contoso.com -ConfigurationName Microsoft.PowerShell
````

### <a name="example-6"></a>PŘÍKLAD 6

Tento příklad umožňuje všem uživatelům přístup k všechny koncové body na všech počítačích. To v podstatě vypne autorizačních pravidel.

> [!NOTE]
> Použití `*` zástupný znak se doporučují pro nasazení zabezpečené a by měl pouze se považuje za pro testovací prostředí nebo použít v nasazeních, kde můžete zmírnit zabezpečení.

````powershell
Add-PswaAuthorizationRule -UserName * -ComputerName * -ConfigurationName *
````

## <a name="see-also"></a>Viz také

[Get-PswaAuthorizationRule](https://technet.microsoft.com/library/jj592891(v=wps.630).aspx)

[Remove-PswaAuthorizationRule](https://technet.microsoft.com/library/jj592893(v=wps.630).aspx)

[Test-PswaAuthorizationRule](https://technet.microsoft.com/library/jj592892(v=wps.630).aspx)

[Rutiny Install-PswaWebApplication](https://technet.microsoft.com/library/jj592894(v=wps.630).aspx)

[Přidat člena](http://go.microsoft.com/fwlink/p/?LinkId=113280)

[New-Object](http://go.microsoft.com/fwlink/p/?LinkId=113355)

[Get-Credential](http://go.microsoft.com/fwlink/?LinkID=293936)
