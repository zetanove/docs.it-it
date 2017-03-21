---
title: 'Procedura: interrompere e combinare istruzioni nel codice (Visual Basic) | Documenti di Microsoft'
ms.custom: 
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb._
dev_langs:
- VB
helpviewer_keywords:
- colons (:)
- line continuation
- _ line-continuation character
- ': line separator character'
- Visual Basic code, line breaks in
- Visual Basic code, line breaks
- Visual Basic code, line continuation
- long lines of code
- line terminator
- line-continuation sequence
- underscores, in code
- statements [Visual Basic], line continuation in
- line breaks, in code
- line-continuation character
- Visual Basic code, line continuation in
- statements [Visual Basic], line breaks in
ms.assetid: dea01dad-a8ac-484a-bb3a-8c45a1b1eccc
caps.latest.revision: 21
author: stevehoag
ms.author: shoag
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: 840036a91f430f72e0258b8be466770f2855a58f
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-break-and-combine-statements-in-code-visual-basic"></a>Procedura: Interrompere e combinare istruzioni nel codice (Visual Basic)
Quando si scrive codice, è possibile creare in alcuni casi istruzioni molto lunghe che richiedono lo scorrimento orizzontale nell'Editor di codice. Anche se ciò non influiscono sulla modalità di esecuzione del codice, rende difficile a te o ad altri utenti di leggere il codice visualizzato sul monitor. In questi casi, è opportuno suddividere una lunga istruzione in più righe.  
  
### <a name="to-break-a-single-statement-into-multiple-lines"></a>Per suddividere una singola istruzione in più righe  
  
-   Utilizzare il carattere di continuazione di riga, ovvero un carattere di sottolineatura (`_`), nel punto in cui si desidera inserire l'interruzione di riga. Il carattere di continuazione di riga deve essere preceduto da uno spazio e seguito da un terminatore di riga (ritorno a capo).  
  
    > [!NOTE]
    >  In alcuni casi, se si omette il carattere di continuazione di riga, il compilatore Visual Basic in modo implicito continuerà l'istruzione nella riga successiva del codice. Per un elenco di elementi della sintassi per il quale è possibile omettere il carattere di continuazione di riga, vedere "Continuazione di riga implicita" in [istruzioni](../../../visual-basic/programming-guide/language-features/statements.md).  
  
     Nell'esempio seguente, l'istruzione viene suddivisa in quattro righe con caratteri di continuazione di riga che terminano tutte tranne l'ultima riga.  
  
     [!code-vb[VbVbcnConventions&#20;](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/how-to-break-and-combine-statements-in-code_1.vb)]  
  
     Utilizzo di questa sequenza semplifica il codice leggere, sia online e quando stampata.  
  
     Il carattere di continuazione di riga deve essere l'ultimo carattere su una riga. È possibile seguire con altri elementi nella stessa riga.  
  
     Esistono alcune limitazioni riguardo in cui è possibile utilizzare il carattere di continuazione di riga; ad esempio, è possibile utilizzare all'interno di un nome dell'argomento. È possibile interrompere un elenco di argomenti con il carattere di continuazione di riga, ma i singoli nomi degli argomenti devono rimanere invariati.  
  
     È possibile continuare un commento con un carattere di continuazione di riga. Il compilatore non esamina i caratteri in un commento per un significato speciale. Per commenti su più righe, ripetere il simbolo di commento (`'`) in ogni riga.  
  
 Sebbene il metodo consigliato consiste nell'inserire ogni istruzione su una riga separata [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] consente inoltre di inserire più istruzioni sulla stessa riga.  
  
### <a name="to-place-multiple-statements-on-the-same-line"></a>Per inserire più istruzioni sulla stessa riga  
  
-   Separare le istruzioni con due punti (`:`), come nell'esempio seguente.  
  
     [!code-vb[VbVbcnConventions&#10;](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/how-to-break-and-combine-statements-in-code_2.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 [Struttura del programma e convenzioni del codice](../../../visual-basic/programming-guide/program-structure/program-structure-and-code-conventions.md)   
 [Istruzioni](../../../visual-basic/programming-guide/language-features/statements.md)
