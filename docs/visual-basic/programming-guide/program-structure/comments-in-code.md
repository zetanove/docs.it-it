---
title: I commenti nel codice (Visual Basic) | Documenti di Microsoft
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
dev_langs:
- VB
helpviewer_keywords:
- Uncomment button
- REM statement
- comments, in code
- comments, Visual Basic code
- Comment button
- buttons, Uncomment
- buttons, Comment
- code comments, Visual Basic
- Visual Basic code, comments
- comments
- code comments
ms.assetid: 90136fba-22eb-49f9-ba81-63db629b4a47
caps.latest.revision: 17
author: stevehoag
ms.author: shoag
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
ms.openlocfilehash: 9663d83903ba2f9dcf93ecb5c293ac479e7dc175
ms.lasthandoff: 03/13/2017

---
# <a name="comments-in-code-visual-basic"></a>Commenti nel codice (Visual Basic)
Negli esempi di codice viene spesso utilizzato il simbolo di commento (`'`). Questo simbolo indica il [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] compilatore di ignorare il testo seguente, o *commento*. I commenti sono brevi annotazioni descrittive che vengono aggiunte al codice per agevolarne la lettura.  
  
 È buona norma di programmazione iniziare tutte le routine con un breve commento che ne descriva le caratteristiche funzionali, ovvero le operazioni che vengono compiute. Ciò può rivelarsi a proprio vantaggio e di chi esaminerà il codice. È opportuno separare le informazioni dettagliate relative alle modalità di implementazione dai commenti che descrivono le caratteristiche funzionali. Quando si includono informazioni dettagliate sulle modalità di implementazione, è importante che queste vengano aggiornate contestualmente all'aggiornamento della funzione.  
  
 I commenti possono seguire un'istruzione sulla stessa riga oppure occupare una riga intera. Nell'esempio di codice seguente vengono illustrate entrambe le opzioni.  
  
 [!code-vb[VbVbcnConventions&#16;](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/comments-in-code_1.vb)]  
  
 Se il commento richiede più di una riga, utilizzare il simbolo di commento su ogni riga, così come viene illustrato nell'esempio seguente:  
  
 [!code-vb[VbVbcnConventions n.&17;](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/comments-in-code_2.vb)]  
  
## <a name="commenting-guidelines"></a>Indicazioni sui commenti  
 Nella tabella riportata di seguito vengono fornite indicazioni generali sui tipi di commenti che possono precedere una sezione del codice. Si tratta di semplici suggerimenti; [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] non impone alcuna regola per l'aggiunta di commenti. Scrivere il testo che si ritiene più adatto alle proprie esigenze e a quelle di chi leggerà il codice.  
  
|||  
|---|---|  
|Tipo di commento|Descrizione del commento|  
|Scopo|Descrive le operazioni eseguite dalla routine, non la modalità di esecuzione|  
|Presupposti|Elenca tutte le variabili esterne, i controlli, i file aperti o gli altri elementi a cui accede la routine|  
|Effetti|Elenca tutte le variabili esterne, i controlli o i file interessati, nonché l'effetto su di essi (solo se non è ovvio)|  
|Input|Specifica lo scopo dell'argomento|  
|Valore restituito|Spiega i valori restituiti dalla routine|  
  
 È importante tenere presente i seguenti punti:  
  
-   Le dichiarazioni di variabili importanti devono essere precedute da un commento in cui viene descritto l'utilizzo della variabile dichiarata.  
  
-   I nomi di variabili, controlli e routine devono essere descrittivi in modo da rendere necessaria l'aggiunta di commenti solo per la descrizione di implementazioni complesse.  
  
-   Non è possibile inserire sulla stessa riga una sequenza di continuazione di riga seguita da un commento.  
  
 È possibile aggiungere o rimuovere i simboli di commento per un blocco di codice, selezionare uno o più righe di codice e scegliere il **commento** (![VisualBasicWinAppCodeEditorCommentButton](../../../visual-basic/programming-guide/program-structure/media/vacommentbutton.gif "vaCommentButton")) e **Rimuovi commento** (![VisualStudioWinAppProjectUncommentButton](../../../visual-basic/programming-guide/program-structure/media/vauncommentbutton.gif "vaUncommentButton")) pulsanti di **modificare** barra degli strumenti.  
  
> [!NOTE]
>  Per aggiungere commenti al codice è possibile anche inserire la parola chiave `REM` prima del testo. Tuttavia, il `'` simbolo e il **commento**/**Rimuovi commento** pulsanti sono più facili da utilizzare e richiedono meno spazio e memoria.  
  
## <a name="see-also"></a>Vedere anche  
 [La documentazione del codice con commenti XML](http://msdn.microsoft.com/magazine/dd722812.aspx)   
 [Procedura: creare documentazione XML](../../../visual-basic/programming-guide/program-structure/how-to-create-xml-documentation.md)   
 [Tag di commento XML](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)   
 [Struttura del programma e convenzioni del codice](../../../visual-basic/programming-guide/program-structure/program-structure-and-code-conventions.md)   
 [Istruzione REM](../../../visual-basic/language-reference/statements/rem-statement.md)
