---
ms.date: 2017-06-05
keywords: "rutiny prostředí PowerShell"
title: "Objekt kanálu"
ms.assetid: 523d8ae4-d743-47a4-b79a-806130ca688a
ms.openlocfilehash: 3fa41cc744cf3ab66fc5ef186ead8eb919429a76
ms.sourcegitcommit: 74255f0b5f386a072458af058a15240140acb294
ms.translationtype: MT
ms.contentlocale: cs-CZ
ms.lasthandoff: 08/03/2017
---
# <a name="object-pipeline"></a>Objekt kanálu
Kanály fungovat stejně jako řadu připojené segmenty kanálu. Položky přesunutí podél kanálu předávání jednotlivých segmentů. Pokud chcete vytvořit kanál v prostředí Windows PowerShell, připojíte příkazy spolu s operátor kanálu "|". Výstup každé příkazu se používá jako vstup dalšího příkazu.

Kanály jsou pravděpodobně nejvíc hodí v situaci koncept používat rozhraní příkazového řádku. Použít správně, kanály nejen snížit náročnost při zadávání komplexní příkazy, ale také usnadňují najdete v části tok práce v příkazech. Související užitečné charakteristika kanálů je, protože funguje na každou položku samostatně, nemáte změnit podle toho, jestli se mají nula, jednu nebo mnoho položek v kanálu. Kromě toho každý příkaz v kanálu (označovaný jako element kanálu) obvykle předává její výstup do dalšího příkazu v kanálu položku po položce. To obvykle snižuje zatížení prostředků komplexní příkazů a umožňuje okamžitě získávání výstupu.

V této kapitole jsme se popisují, jak se liší od kanálů nejoblíbenější nutný zřetězením příkazů Windows Powershellu a pak ukazují některé základní nástroje, které můžete použít k usnadnění výstup kanál ovládacího prvku a také k najdete v článku Jak funguje kanálu.

