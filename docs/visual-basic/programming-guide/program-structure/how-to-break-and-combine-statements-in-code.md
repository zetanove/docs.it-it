---
title: "Procedura: Interrompere e combinare istruzioni nel codice (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb._"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "due punti (:)"
  - "continuazioni di riga"
  - "_ (carattere di continuazione di riga)"
  - ": (carattere separatore di riga)"
  - "Visual Basic (codice), interruzioni di riga in"
  - "Visual Basic (codice), interruzioni di riga"
  - "Visual Basic (codice), continuazione di riga"
  - "righe di codice lunghe"
  - "terminazione di riga"
  - "sequenza di continuazione di riga"
  - "sottolineature, nel codice"
  - "istruzioni [Visual Basic], continuazione di riga"
  - "interruzioni di riga, nel codice"
  - "carattere di continuazione di riga"
  - "Visual Basic (codice), continuazione di riga in"
  - "istruzioni [Visual Basic], interruzioni di riga"
ms.assetid: dea01dad-a8ac-484a-bb3a-8c45a1b1eccc
caps.latest.revision: 21
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 21
---
# Procedura: Interrompere e combinare istruzioni nel codice (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Durante la scrittura del codice, vengono talvolta create istruzioni molto lunghe che richiedono uno scorrimento orizzontale nell'editor di codice.  Sebbene non influiscono sulla modalità del codice, può rendere difficoltosa la lettura del codice sullo schermo.  In questi casi, è opportuno suddividere una lunga istruzione su più righe.  
  
### Per suddividere un'istruzione in più righe  
  
-   Utilizzare il carattere di continuazione di riga, ossia un segno di sottolineatura \(`_`\), nel punto in cui si desidera inserire l'interruzione della riga.  La sottolineatura deve essere immediatamente preceduto da uno spazio e immediatamente essere seguita da un carattere di terminazione di riga \(ritorno a capo\).  
  
    > [!NOTE]
    >  In alcuni casi, se si omette il carattere di continuazione di riga, il compilatore Visual Basic continua in modo implicito l'istruzione sulla riga di codice successiva.  Per un elenco di elementi della sintassi per cui è possibile omettere il carattere di continuazione di riga, vedere "continuazione di riga implicita" in [Statements](../../../visual-basic/programming-guide/language-features/statements.md).  
  
     Nell'esempio che segue l'istruzione viene suddivisa in quattro righe con caratteri di continuazione di riga alla fine di tutte le righe tranne l'ultima.  
  
     [!code-vb[VbVbcnConventions#20](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/how-to-break-and-combine-statements-in-code_1.vb)]  
  
     L'utilizzo di questa sequenza semplifica la lettura del codice, sia online che in versione stampata.  
  
     Il carattere di continuazione di riga deve essere l'ultimo carattere in una riga.  Non può essere seguita da altro.  
  
     Esistono alcune limitazioni riguardo il punto è possibile utilizzare il carattere di continuazione di riga, ad esempio, non è possibile utilizzarlo in corso un nome dell'argomento.  È possibile interrompere un elenco di argomenti con il carattere di continuazione di riga, a condizione che i singoli nomi degli argomenti rimangano inalterati.  
  
     Non è possibile continuare un commento utilizzando un carattere di continuazione di riga.  Il compilatore non esamina i caratteri in un commento per il significato speciale.  Per un commento a più righe, inserire il simbolo di commento \(`'`\) in ogni riga.  
  
 Sebbene posizionare ogni istruzione su una riga separata è il metodo consigliato, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] consente anche a più istruzioni sulla stessa riga.  
  
### Per inserire più istruzioni sulla stessa riga  
  
-   Separare le istruzioni con due punti \(`:`\), come nell'esempio seguente:  
  
     [!code-vb[VbVbcnConventions#10](../../../visual-basic/programming-guide/language-features/codesnippet/VisualBasic/how-to-break-and-combine-statements-in-code_2.vb)]  
  
## Vedere anche  
 [Struttura del programma e convenzioni di scrittura del codice](../../../visual-basic/programming-guide/program-structure/program-structure-and-code-conventions.md)   
 [Statements](../../../visual-basic/programming-guide/language-features/statements.md)