---
description: ''
ms.topic: article
ms.prod: powershell
keywords: rutiny prostředí PowerShell
ms.date: 12/12/2016
title: Přidat pswaauthorizationrule
ms.technology: powershell
schema: 2.0.0
ms.openlocfilehash: 07ddd4df6a776f3ef6763242f8682747b9b97061
ms.sourcegitcommit: cf195b090b3223fa4917206dfec7f0b603873cdf
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 04/09/2018
---
# <a name="add-pswaauthorizationrule"></a>Add-PswaAuthorizationRule

## <a name="synopsis"></a>STRUČNÝ OBSAH

Přidá nové autorizační pravidlo je sada pravidel autorizace pro Windows PowerShell® Web Access.

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

**Add-PswaAuthorizationRule** rutiny přidá nové autorizační pravidlo je sada pravidel autorizace pro Windows PowerShell® Web Access.

Zadejte uživatele, počítače a prostředí Windows PowerShell koncové body pro toto pravidlo. Můžete zadat uživatele a počítače podle jednotlivých uživatelských účtů a názvy počítačů, nebo zadáním skupiny.

Pro počítač, který je připojený k doméně služby Active Directory použije rutinu identifikátor zabezpečení (SID) počítače k vytvoření pravidla.
To umožňuje použít krátký název, plně kvalifikovaný název domény (FQDN) nebo IP adresu pro **název počítače** pole na stránce přihlášení.

Pro počítač, který není připojený k doméně služby Active Directory rutina vytvoří pravidlo s použitím názvu počítače poskytnutý správcem. K úspěšnému připojení k tomuto počítači, koncový uživatel musí poskytnout název počítače úplně stejně jako v pravidle.

Pokud existuje víc počítačů se stejným názvem v síti, může krátký název vyřešit více než jeden počítač. To může vést k nejednoznačnosti při navazování připojení. Například, pokud pravidlo existuje pro počítače pracovní skupiny s názvem "*Server1*" a nový počítač s názvem *server1.contoso.com* je připojený k síti, úspěšné ověření pomocí autorizačních pravidel a Windows PowerShell Web Access pokusí navázat připojení k počítači s názvem "*Server1*". Není zaručeno, že připojení k počítači konkrétní pracovní skupině; Pokus může být provedeny v pracovní skupině nebo doméně počítač s názvem "*Server1*". Aby se snížilo nejednoznačnosti, se doporučuje použít plně kvalifikovaný název domény pro cílového počítače vždy, když je možné vytvořit autorizační pravidlo.

Autorizační pravidla vyhodnotit primární přihlašovací pověření uživatelů Windows PowerShell Web Access, není alternativní přihlašovací údaje (druhou sadu pověření v nalezen **volitelná nastavení připojení** části přihlašovací stránka). Příklad tohoto najdete příklad 6.

## <a name="parameters"></a>Parameters

### <a name="-computergroupnameltstringgt"></a>-ComputerGroupName&lt;String&gt;

Určuje název skupiny počítačů ve službě Active Directory Domain Services (AD DS) nebo místní skupiny, ke kterým toto pravidlo udělí přístup.

|||
|-|-|
| Aliasy                              | žádný                                 |
| Povinné?                            | Hodnota TRUE                                 |
| Pozice?                            | S názvem                                |
| Výchozí hodnota                        | žádný                                 |
| Přijmout kanálový vstup?               | True (ByPropertyName)                |
| Přijímat zástupné znaky?          | false                                |

### <a name="-computernameltstringgt"></a>-ComputerName&lt;String&gt;

Určuje název počítače, na kterou toto pravidlo udělí přístup.

|||
|-|-|
| Aliasy                              | žádný                                 |
| Povinné?                            | Hodnota TRUE                                 |
| Pozice?                            | S názvem                                |
| Výchozí hodnota                        | žádný                                 |
| Přijmout kanálový vstup?               | True (ByPropertyName)                |
| Přijímat zástupné znaky?          | false                                |

### <a name="-configurationnameltstringgt"></a>-ConfigurationName&lt;řetězec&gt;

Určuje název konfigurace relace prostředí Windows PowerShell, také známé jako prostředí runspace, do které toto pravidlo udělí přístup.

|||
|-|-|
| Aliasy                              | žádný                                 |
| Povinné?                            | Hodnota TRUE                                 |
| Pozice?                            | S názvem                                |
| Výchozí hodnota                        | žádný                                 |
| Přijmout kanálový vstup?               | True (ByPropertyName)                |
| Přijímat zástupné znaky?          | false                                |

### <a name="-credentialltpscredentialgt"></a>-Credential&lt;PSCredential&gt;

Určuje **PSCredential** objekt pro uživatelský účet, který chcete použít ke změně Windows PowerShell Web Access autorizačních pravidel. Pokud tento parametr nepřidáte, rutina používá účet aktuálně přihlášeného uživatele. Chcete-li získat **PSCredential** objekt, který je potřeba přidat autorizační pravidla vzdáleně, spusťte [Get-Credential](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.security/Get-Credential) rutiny.

|||
|-|-|
| Aliasy                              | žádný                                 |
| Povinné?                            | false                                |
| Pozice?                            | S názvem                                |
| Výchozí hodnota                        | žádný                                 |
| Přijmout kanálový vstup?               | false                                |
| Přijímat zástupné znaky?          | false                                |

### <a name="-force"></a>-Force

Vynutí spuštění příkazu, aniž by požádal uživatele o potvrzení. \
Kromě toho je také vyzve k potvrzení při zadání názvu počítače jednoduchý nebo krátké (například název, který není platný název domény nebo není plně kvalifikovaná). Potvrzení je požadována z bezpečnostních důvodů, takže pokud chcete přidat počítač, pouze pokud je počítač v pracovní skupině můžete použít jednoduchý název.

|||
|-|-|
| Aliasy                              | žádný                                 |
| Povinné?                            | false                                |
| Pozice?                            | S názvem                                |
| Výchozí hodnota                        | žádný                                 |
| Přijmout kanálový vstup?               | false                                |
| Přijímat zástupné znaky?          | false                                |

### <a name="-rulenameltstringgt"></a>-RuleName&lt;String&gt;

Určuje popisný název pro toto pravidlo.

|||
|-|-|
| Aliasy                              | žádný                                 |
| Povinné?                            | false                                |
| Pozice?                            | S názvem                                |
| Výchozí hodnota                        | žádný                                 |
| Přijmout kanálový vstup?               | True (ByPropertyName)                |
| Přijímat zástupné znaky?          | false                                |

### <a name="-usergroupnameltstringgt"></a>-UserGroupName&lt;String\[\]&gt;

Určuje název jednoho nebo víc skupin uživatelů ve službě AD DS nebo místních skupin, ke kterým toto pravidlo udělí přístup.

|||
|-|-|
| Aliasy                              | žádný                                 |
| Povinné?                            | Hodnota TRUE                                 |
| Pozice?                            | S názvem                                |
| Výchozí hodnota                        | žádný                                 |
| Přijmout kanálový vstup?               | True (ByPropertyName)                |
| Přijímat zástupné znaky?          | false                                |

### <a name="-usernameltstringgt"></a>-UserName&lt;String\[\]&gt;

Určuje jeden nebo více uživatelů, na které toto pravidlo udělí přístup. Uživatelské jméno může být místní uživatelský účet v počítači brány nebo uživatele ve službě AD DS.
Formát je `domain\user` nebo `computer\user`.

|||
|-|-|
| Aliasy                              | žádný                                 |
| Povinné?                            | Hodnota TRUE                                 |
| Pozice?                            | 1                                    |
| Výchozí hodnota                        | žádný                                 |
| Přijmout kanálový vstup?               | Hodnotu true (ByValue, ByPropertyName)       |
| Přijímat zástupné znaky?          | false                                |

### <a name="ltcommonparametersgt"></a>&lt;CommonParameters&gt;

Tato rutina podporuje běžné parametry:-Verbose,-Debug, - ErrorAction, - ErrorVariable,-OutBuffer a - OutVariable.
Další informace najdete v tématu [about_CommonParameters](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/about/about_commonparameters).

## <a name="inputs"></a>VSTUPY

### <a name="string"></a>Řetězec

Tato rutina akceptuje jako vstupní řetězec nebo pole řetězců.

### <a name="string"></a>Řetězec\[\]

Tato rutina akceptuje jako vstupní řetězec nebo pole řetězců.

## <a name="outputs"></a>Výstupy

### <a name="microsoftmanagementpowershellwebaccesspswaauthorizationrule"></a>Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule

Tato rutina vrací objektu pravidla autorizace.

## <a name="examples"></a>PŘÍKLADY

### <a name="example-1"></a>PŘÍKLAD 1

Tento příklad uděluje přístup k této konfiguraci relace *Pswakoncovybod*, omezuje prostředí runspace *srv2* pro uživatele v *SMAdmins* skupiny. \
**Poznámka:**: název počítače musí být platný plně kvalifikovaný název domény (FQDN). Správci definují konfiguraci relace s omezeným přístupem nebo prostředí runspace, což je omezeným rozsahem rutin a úloh, které koncoví uživatelé můžou běžet. Definování omezeném prostředí runspace může zabránit uživatelům v přístupu k jiným počítačům, které nejsou v povolené prostředí runspace Windows PowerShell®, což zajišťuje bezpečnější připojení. Další informace o konfiguracích relace najdete v tématu [about_Session_Configurations](https://msdn.microsoft.com/powershell/reference/5.1/microsoft.powershell.core/about/about_session_configurations) nebo [instalace a použití Windows PowerShell Web Access](../install-and-use-windows-powershell-web-access.md).

```PowerShell
Add-PswaAuthorizationRule -ComputerName srv2.contoso.com -UserGroupName contoso\SMAdmins -ConfigurationName PSWAEndpoint
```

### <a name="example-2"></a>PŘÍKLAD 2

Tento příklad uděluje přístup k výchozí konfiguraci relace prostředí Windows PowerShell, `Microsoft.PowerShell`na *srv2* pro uživatele v seznamu Uživatelé s názvem contoso\\uživatel1, contoso\\uživatel2 a contoso\\UŽIVATEL3. Tato rutina vytvoří tři pravidla (1 na osobu).

```PowerShell
Add-PswaAuthorizationRule –UserName contoso\user1, contoso\user2, contoso\user3 –ComputerName srv2.contoso.com -ConfigurationName Microsoft.PowerShell
```

### <a name="example-3"></a>PŘÍKLAD 3

Tento příklad ukazuje, jak vstupní hodnoty názvu uživatele prostřednictvím kanálu.

```
"contoso\user1","contoso\user2" | Add-pswaAuthorizationRule –ComputerName srv2.contoso.com –ConfigurationName Microsoft.PowerShell
```

### <a name="example-4"></a>PŘÍKLAD 4

Tento příklad ukazuje, jak všechny parametry trvat hodnoty z kanálu podle názvu vlastnosti.

````PowerShell
$o = New-Object -TypeName PSObject |
    Add-Member -Type NoteProperty -Name "UserName" -Value "contoso\user1" -PassThru |
    Add-Member -Type NoteProperty -Name "ComputerName" -Value "srv2.contoso.com" -PassThru |
    Add-Member -Type NoteProperty -Name "ConfigurationName" -Value "Microsoft.PowerShell" –PassThru

$o | Add-PswaAuthorizationRule -UserName contoso\user1 -ConfigurationName Microsoft.PowerShell
````

### <a name="example-5"></a>PŘÍKLAD 5

Tento příklad přidá pravidlo povolující místního uživatele s názvem *PswaServer\\Janlocal* přístup k serveru s názvem *srv1.contoso.com*.

Tento příklad ukazuje scénář, kde brána je v pracovní skupině a cílový počítač je v doméně. Autorizační pravidlo platí pro místní uživatele na bráně. Na Windows PowerShell Web Access přihlašovací stránku k ověření úspěšně, musí uživatel zadat druhou sadu pověření v **volitelná nastavení připojení** oblasti. Server brány použije další sadu pověření k ověření uživatele v cílovém počítači, serveru s názvem *srv1.contoso.com*.

````
Add-PswaAuthorizationRule –UserName PswaServer\ChrisLocal –ComputerName srv1.contoso.com –ConfigurationName Microsoft.PowerShell
````

### <a name="example-6"></a>PŘÍKLAD 6

Tento příklad umožňuje všem uživatelům přístup k všechny koncové body na všech počítačích.
To v podstatě vypne autorizačních pravidel. \
**Poznámka:**: použití `*` zástupný znak se nedoporučuje pro nasazení citlivé na zabezpečení a by měla pouze být považovány za pro testovací prostředí nebo použitým v nasazeních, kde můžete zmírnit zabezpečení.

````PowerShell
Add-PswaAuthorizationRule –UserName * -ComputerName * -ConfigurationName *
````

## <a name="see-also"></a>Viz také

- [Get-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592891(v=wps.630).aspx)
- [Remove-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592893(v=wps.630).aspx)
- [Test-PswaAuthorizationRule](https://technet.microsoft.com/en-us/library/jj592892(v=wps.630).aspx)
- [Rutiny Install-PswaWebApplication](https://technet.microsoft.com/en-us/library/jj592894(v=wps.630).aspx)
- [Přidat člena](http://go.microsoft.com/fwlink/p/?LinkId=113280)
- [New-Object](http://go.microsoft.com/fwlink/p/?LinkId=113355)
- [Get-Credential](http://go.microsoft.com/fwlink/?LinkID=293936)