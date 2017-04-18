---
title: Si sono verificati errori durante la compilazione di XML schema nel progetto | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- bc36810
- vbc36810
dev_langs:
- VB
helpviewer_keywords:
- BC36810
ms.assetid: 9323b5d2-ba14-4e49-91f1-9ad647162144
caps.latest.revision: 11
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- cs-cz
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- pl-pl
- pt-br
- ru-ru
- tr-tr
- zh-cn
- zh-tw
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: cf04e85da98db53d1c78269169571936f708cd21
ms.lasthandoff: 03/13/2017

---
# <a name="errors-occurred-while-compiling-the-xml-schemas-in-the-project"></a>Errori durante la compilazione di XML schema nel progetto
Si sono verificati errori durante la compilazione di XML schema nel progetto. Per questo motivo, IntelliSense XML non è disponibile.  
  
 Si verifica un errore in uno schema XML Schema Definition (XSD) incluso nel progetto. Questo errore si verifica quando si aggiunge un file XSD dello schema XSD che è in conflitto con lo schema XSD esistente impostato per il progetto.  
  
 **ID errore:** BC36810  
  
## <a name="to-correct-this-error"></a>Per correggere l'errore  
  
-   Fare doppio clic su avviso nella **elenco errori** finestra. Visual Basic verrà visualizzata la posizione nel file XSD che rappresenta l'origine dell'avviso. Correggere l'errore nello schema XSD.  
  
-   Verificare che tutti gli elementi file XSD dello schema (XSD) sono inclusi nel progetto. Potrebbe essere necessario fare clic su **Mostra tutti i file** sul **progetto** menu per visualizzare il file con estensione xsd file **Esplora**. Fare doppio clic su un file XSD e quindi fare clic su **Includi nel progetto** per includere il file nel progetto.  
  
-   Se si utilizza il XML guidata Schema, questo errore può verificarsi se si dedurre schemi più volte la stessa origine. In questo caso, è possibile rimuovere i file di schema XSD esistenti dal progetto, aggiungere un nuovo file XML al modello di elemento di Schema e fornire quindi il codice XML guidata Schema con tutte le origini XML applicabili per il progetto.  
  
-   Se nello schema XSD viene identificato alcun errore, il compilatore XML non dispone di informazioni sufficienti per fornire un messaggio di errore dettagliato. È possibile ottenere informazioni più dettagliate sull'errore se si assicura che gli spazi dei nomi XML per i file XSD incluso nel progetto corrispondano gli spazi dei nomi XML identificati per lo Schema XML, impostare in Visual Studio.  
  
## <a name="see-also"></a>Vedere anche  
 [Finestra Elenco errori](https://docs.microsoft.com/visualstudio/ide/reference/error-list-window)   
 [IntelliSense XML in Visual Basic](../../../visual-basic/programming-guide/language-features/xml/xml-intellisense.md)   
 [XML](../../../visual-basic/programming-guide/language-features/xml/index.md)
