---
title: "Comments in Code (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Uncomment button"
  - "REM statement"
  - "comments, in code"
  - "comments, Visual Basic code"
  - "Comment button"
  - "buttons, Uncomment"
  - "buttons, Comment"
  - "code comments, Visual Basic"
  - "Visual Basic code, comments"
  - "comments"
  - "code comments"
ms.assetid: 90136fba-22eb-49f9-ba81-63db629b4a47
caps.latest.revision: 17
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 17
---
# Comments in Code (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Negli esempi di codice viene spesso utilizzato il simbolo di commento \(`'`\).  Questo simbolo indica al compilatore [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] di ignorare il testo seguente, ovvero il *commento*.  I commenti sono brevi annotazioni descrittive che vengono aggiunte al codice per agevolarne la lettura.  
  
 È buona norma di programmazione iniziare tutte le routine con un breve commento che ne descriva le caratteristiche funzionali, ovvero le operazioni che vengono compiute.  Ciò può rivelarsi a proprio vantaggio e di chi esaminerà il codice.  È opportuno separare le informazioni dettagliate relative alle modalità di implementazione dai commenti che descrivono le caratteristiche funzionali.  Quando si includono informazioni dettagliate sulle modalità di implementazione, è importante che queste vengano aggiornate contestualmente all'aggiornamento della funzione.  
  
 I commenti possono seguire un'istruzione sulla stessa riga oppure occupare una riga intera.  Nell'esempio di codice seguente vengono illustrate entrambe le opzioni.  
  
 [!code-vb[VbVbcnConventions#16](../../../visual-basic/programming-guide/language-features/codesnippet/visualbasic/comments-in-code_1.vb)]  
  
 Se il commento richiede più di una riga, utilizzare il simbolo di commento su ogni riga, così come viene illustrato nell'esempio seguente:  
  
 [!code-vb[VbVbcnConventions#17](../../../visual-basic/programming-guide/language-features/codesnippet/visualbasic/comments-in-code_2.vb)]  
  
## Indicazioni sui commenti  
 Nella tabella riportata di seguito vengono fornite indicazioni generali sui tipi di commenti che possono precedere una sezione del codice.  Si tratta di semplici suggerimenti; [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] non impone alcuna regola per l'aggiunta di commenti.  Scrivere il testo che si ritiene più adatto alle proprie esigenze e a quelle di chi leggerà il codice.  
  
|||  
|-|-|  
|Tipo di commento|Descrizione del commento|  
|Scopo|Descrive le operazioni eseguite dalla routine, non la modalità di esecuzione|  
|Presupposti|Elenca tutte le variabili esterne, i controlli, i file aperti o gli altri elementi a cui accede la routine|  
|Effetti|Elenca tutte le variabili esterne, i controlli o i file interessati, nonché l'effetto su di essi \(solo se non è ovvio\)|  
|Input|Specifica lo scopo dell'argomento|  
|Valore restituito|Spiega i valori restituiti dalla routine|  
  
 È importante tenere presente i seguenti punti:  
  
-   Le dichiarazioni di variabili importanti devono essere precedute da un commento in cui viene descritto l'utilizzo della variabile dichiarata.  
  
-   I nomi di variabili, controlli e routine devono essere descrittivi in modo da rendere necessaria l'aggiunta di commenti solo per la descrizione di implementazioni complesse.  
  
-   Non è possibile inserire sulla stessa riga una sequenza di continuazione di riga seguita da un commento.  
  
 Per aggiungere o rimuovere i simboli di commento per un blocco di codice, selezionare una o più righe di codice e fare clic sui pulsanti **Commento** \(![VisualBasicWinAppCodeEditorCommentButton](../../../visual-basic/programming-guide/program-structure/media/vacommentbutton.png "vaCommentButton")\) e **Rimuovi commento** \(![VisualStudioWinAppProjectUncommentButton](../../../visual-basic/programming-guide/program-structure/media/vauncommentbutton.png "vaUncommentButton")\) sulla barra degli strumenti **Modifica**.  
  
> [!NOTE]
>  Per aggiungere commenti al codice è possibile anche inserire la parola chiave `REM` prima del testo.  Il simbolo `'` e i pulsanti **Commento**\/**Rimuovi commento** sono comunque più semplici da utilizzare e richiedono meno spazio e memoria.  
  
## Vedere anche  
 [Documentare il codice con commenti XML](http://msdn.microsoft.com/magazine/dd722812.aspx)   
 [How to: Create XML Documentation](../../../visual-basic/programming-guide/program-structure/how-to-create-xml-documentation.md)   
 [XML Comment Tags](../../../visual-basic/language-reference/xmldoc/recommended-xml-tags-for-documentation-comments.md)   
 [Struttura del programma e convenzioni di scrittura del codice](../../../visual-basic/programming-guide/program-structure/program-structure-and-code-conventions.md)   
 [REM Statement](../../../visual-basic/language-reference/statements/rem-statement.md)