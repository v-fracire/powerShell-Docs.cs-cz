---
ms.topic: reference
keywords: rutiny prostředí PowerShell
ms.date: 12/12/2016
title: Test-PswaAuthorizationRule
ms.openlocfilehash: 08248e65be229f9d0f4d606d6c0d039d86ced054
ms.sourcegitcommit: 54534635eedacf531d8d6344019dc16a50b8b441
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 05/16/2018
---
# <a name="test-pswaauthorizationrule"></a>Test-PswaAuthorizationRule

## <a name="synopsis"></a>STRUČNÝ OBSAH

Ověřuje, zda pravidla pro zadaného uživatele, počítače nebo koncový bod neexistuje.

## <a name="syntax"></a>SYNTAXE

### <a name="computername"></a>ComputerName
```
Test-PswaAuthorizationRule [-UserName] <String> [-ComputerName] <String> [[-ConfigurationName] <String> ] [-Credential <PSCredential> ] [-Rule <PswaAuthorizationRule[]> ] [ <CommonParameters>]
```

### <a name="connectionuri"></a>ConnectionUri
```
Test-PswaAuthorizationRule [-UserName] <String> [-ConnectionUri] <Uri> [[-ConfigurationName] <String> ] [-Credential <PSCredential> ] [-Rule <PswaAuthorizationRule[]> ] [ <CommonParameters>]
```

## <a name="description"></a>POPIS

**Test-PswaAuthorizationRule** rutiny ověřuje, zda pravidla pro zadaného uživatele, počítače nebo koncový bod neexistuje.
Tuto rutinu můžete použít také otestovat autorizační pravidla, chcete-li ověřit, že je autorizovaný konkrétní uživatele, počítače nebo koncový bod žádost o přístup.
Ve výchozím nastavení vyhodnotí tato rutina všechna pravidla v souboru autorizace.
Můžete však zadat podmnožinu pravidla k testování.

Tato rutina vám pomůže vyřešit potíže s počet selhání ověření.

Parametry pro tuto rutinu odpovídají pole na stránku pro přihlášení k Windows PowerShell® Web Access.

## <a name="parameters"></a>PARAMETRY

### <a name="-computername-ltstringgt"></a>-ComputerName &lt;řetězec&gt;

Určuje název počítače, které chcete otestovat.

|||
|-|-|
| Aliasy                              | žádný                                 |
| Povinné?                            | Hodnota TRUE                                 |
| Pozice?                            | 2                                    |
| Výchozí hodnota                        | žádný                                 |
| Přijmout kanálový vstup?               | false                                |
| Přijímat zástupné znaky?          | false                                |

### <a name="-configurationname-ltstringgt"></a>-ConfigurationName &lt;řetězec&gt;

Určuje název konfigurace relace prostředí Windows PowerShell, také známé jako koncový bod nebo prostředí runspace k testování.

|||
|-|-|
| Aliasy                              | žádný                                 |
| Povinné?                            | false                                |
| Pozice?                            | 3                                    |
| Výchozí hodnota                        | žádný                                 |
| Přijmout kanálový vstup?               | false                                |
| Přijímat zástupné znaky?          | false                                |

### <a name="-connectionuri-lturigt"></a>-ConnectionUri &lt;identifikátor Uri&gt;

Určuje identifikátor URI k testování připojení.

|||
|-|-|
| Aliasy                              | žádný                                 |
| Povinné?                            | Hodnota TRUE                                 |
| Pozice?                            | 2                                    |
| Výchozí hodnota                        | žádný                                 |
| Přijmout kanálový vstup?               | false                                |
| Přijímat zástupné znaky?          | false                                |

### <a name="-credential-ltpscredentialgt"></a>-Credential &lt;PSCredential&gt;

Určuje **PSCredential** objekt pro uživatelský účet, který chcete použít pro testování Windows PowerShell Web Access autorizačních pravidel. Pokud tento parametr nepřidáte, rutina používá účet aktuálně přihlášeného uživatele. Chcete-li získat **PSCredential** objekt, který je potřeba otestovat autorizační pravidla vzdáleně, spusťte [Get-Credential](http://go.microsoft.com/fwlink/?LinkID=293936) rutiny.

|||
|-|-|
| Aliasy                              | žádný                                 |
| Povinné?                            | false                                |
| Pozice?                            | S názvem                                |
| Výchozí hodnota                        | žádný                                 |
| Přijmout kanálový vstup?               | false                                |
| Přijímat zástupné znaky?          | false                                |

### <a name="-rule-ltpswaauthorizationrulegt"></a>-Pravidla &lt;PswaAuthorizationRule\[\]&gt;

Určuje podmnožinu pravidla k testování. Pokud není tento parametr zadán, tato rutina testuje proti všechna autorizační pravidla.

|||
|-|-|
| Aliasy                              | žádný                                 |
| Povinné?                            | false                                |
| Pozice?                            | S názvem                                |
| Výchozí hodnota                        | žádný                                 |
| Přijmout kanálový vstup?               | Hodnotu true (ByValue)                       |
| Přijímat zástupné znaky?          | false                                |

### <a name="-username-ltstringgt"></a>-UserName &lt;řetězec&gt;

Určuje jméno uživatele, který chcete otestovat.

|||
|-|-|
| Aliasy                              | žádný                                 |
| Povinné?                            | Hodnota TRUE                                 |
| Pozice?                            | 1                                    |
| Výchozí hodnota                        | žádný                                 |
| Přijmout kanálový vstup?               | false                                |
| Přijímat zástupné znaky?          | false                                |

### <a name="ltcommonparametersgt"></a>&lt;CommonParameters&gt;

Tato rutina podporuje běžné parametry:-Verbose,-Debug, - ErrorAction, - ErrorVariable,-OutBuffer a - OutVariable.
Další informace najdete v tématu [about_CommonParameters](http://go.microsoft.com/fwlink/p/?LinkID=113216).

## <a name="inputs"></a>VSTUPY

### <a name="microsoftmanagementpowershellwebaccesspswaauthorizationrule"></a>Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule\[\]

Tato rutina akceptuje jako vstupní pole objektů PswaAuthorizationRule.

## <a name="outputs"></a>VÝSTUPY

### <a name="microsoftmanagementpowershellwebaccesspswaauthorizationrule"></a>Microsoft.Management.PowerShellWebAccess.PswaAuthorizationRule\[\]

Tato rutina vytvoří pole objektů PswaAuthorizationRule jako výstup.

## <a name="examples"></a>PŘÍKLADY

### <a name="example-1"></a>PŘÍKLAD 1

Tento příklad testuje všechna autorizační pravidla, aby bylo možné zobrazit všechna pravidla, které uživateli *contoso\\mhanson* pro připojení k počítači *srv2* a použijte k tomu relaci prostředí Windows PowerShell Konfigurace s názvem *testování*.

```
Test-PswaAuthorizationRule -ComputerName srv2.contoso.com -UserName contoso\mhanson -ConfigurationName test
```

### <a name="example-2"></a>PŘÍKLAD 2

Tento příklad testy všechna autorizační pravidla ke kontrole které autorizační pravidla platí pro uživatele *contoso\\mhanson*.

```
Test-PswaAuthorizationRule -UserName contoso\mhanson -ComputerName *
```

## <a name="related-topics"></a>Příbuzná témata

- [Add-PswaAuthorizationRule](add-pswaauthorizationrule.md)
- [Get-PswaAuthorizationRule](get-pswaauthorizationrule.md)
- [Rutiny Install-PswaWebApplication](install-pswawebapplication.md)
- [Remove-PswaAuthorizationRule](remove-pswaauthorizationrule.md)