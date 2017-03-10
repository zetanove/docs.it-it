---
title: "How to: Declare and Call a Default Property in Visual Basic | Microsoft Docs"
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
  - "defaults, properties"
  - "properties [Visual Basic], default"
  - "procedures, defining"
  - "default properties, in Visual Basic"
  - "Visual Basic code, procedures"
  - "Visual Basic code, properties"
  - "default properties"
ms.assetid: 68b4026e-09ef-4613-808e-f6287494ff63
caps.latest.revision: 23
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 23
---
# How to: Declare and Call a Default Property in Visual Basic
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Una *proprietà predefinita* è una proprietà di una classe o di una struttura alla quale il codice può accedere senza specificarla.  Quando il codice chiamante fa riferimento a una classe o a una struttura ma non a una proprietà e il contesto consente l'accesso a una proprietà, in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] l'accesso viene risolto nella proprietà predefinita di tale classe o struttura, se disponibile.  
  
 Una classe o una struttura può includere al massimo una proprietà predefinita.  È tuttavia possibile eseguire l'overload di una proprietà predefinita e disporre di più versioni di tale proprietà.  
  
 Per ulteriori informazioni, vedere [Default](../../../../visual-basic/language-reference/modifiers/default.md).  
  
### Per dichiarare una proprietà predefinita  
  
1.  Dichiarare la proprietà secondo la normale procedura.  Non specificare la parola chiave `Shared` o `Private`.  
  
2.  Includere la parola chiave `Default` nella dichiarazione della proprietà.  
  
3.  Specificare almeno un parametro per la proprietà.  Non è possibile specificare una proprietà predefinita se non accetta almeno un argomento.  
  
     [!code-vb[VbVbcnProcedures#17](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/how-to-declare-and-call-_1.vb)]  
  
### Per chiamare una proprietà predefinita  
  
1.  Dichiarare una variabile del tipo struttura o classe che la contiene.  
  
     [!code-vb[VbVbcnProcedures#16](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/how-to-declare-and-call-_2.vb)]  
  
2.  Utilizzare il nome di variabile da solo in un'espressione in cui in genere viene incluso il nome della proprietà.  
  
     [!code-vb[VbVbcnProcedures#21](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/how-to-declare-and-call-_3.vb)]  
  
3.  Dopo il nome della variabile inserire un elenco di argomenti tra parentesi.  Una proprietà predefinita deve accettare almeno un argomento.  
  
     [!code-vb[VbVbcnProcedures#20](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/how-to-declare-and-call-_4.vb)]  
  
4.  Per recuperare il valore della proprietà predefinita, utilizzare il nome della variabile, con un elenco di argomenti, in un'espressione o dopo il segno di uguale \(`=`\) in un'istruzione di assegnazione.  
  
     [!code-vb[VbVbcnProcedures#15](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/how-to-declare-and-call-_5.vb)]  
  
5.  Per impostare il valore della proprietà predefinita, utilizzare il nome della variabile, con un elenco di argomenti, a sinistra dell'istruzione di assegnazione.  
  
     [!code-vb[VbVbcnProcedures#14](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/how-to-declare-and-call-_6.vb)]  
  
6.  È sempre possibile specificare il nome della proprietà predefinita con il nome della variabile, come quando si accede a qualsiasi altra proprietà.  
  
     [!code-vb[VbVbcnProcedures#19](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/how-to-declare-and-call-_7.vb)]  
  
## Esempio  
 Nell'esempio riportato di seguito viene dichiarata una proprietà predefinita in una classe.  
  
 [!code-vb[VbVbcnProcedures#12](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/how-to-declare-and-call-_8.vb)]  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrato come chiamare la proprietà predefinita `myProperty` nella classe `class1`.  I valori vengono archiviati dalle tre istruzioni di assegnazione in `myProperty` e vengono letti dalla chiamata a <xref:Microsoft.VisualBasic.Interaction.MsgBox%2A>.  
  
 [!code-vb[VbVbcnProcedures#13](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/visualbasic/how-to-declare-and-call-_9.vb)]  
  
 L'utilizzo più comune di una proprietà predefinita è rappresentato dalla proprietà <xref:Microsoft.VisualBasic.Collection.Item%2A> in diverse classi di raccolte.  
  
## Programmazione efficiente  
 L'utilizzo di proprietà predefinite può consentire una lieve riduzione del numero di caratteri del codice sorgente, ma può rendere più difficile la lettura di tale codice.  Se il codice chiamante non viene comunemente utilizzato con una specifica classe o struttura, quando fa riferimento al nome di quest'ultima non è in grado di determinare se il riferimento accede alla classe o alla struttura oppure a una proprietà predefinita.  Questa situazione può generare errori del compilatore o errori meno evidenti della logica di runtime.  
  
 È possibile ridurre in qualche misura il rischio di errori generati dalla proprietà predefinita utilizzando sempre l'[Option Strict Statement](../../../../visual-basic/language-reference/statements/option-strict-statement.md) per impostare il controllo dei tipi del compilatore su `On`.  
  
 Se si intende utilizzare una classe o una struttura predefinita nel codice, è necessario stabilire se include una proprietà predefinita e, in caso affermativo, identificarne il nome.  
  
 A causa degli svantaggi elencati, si consiglia di evitare di specificare proprietà predefinite.  Per migliorare la leggibilità del codice, si consiglia inoltre di fare sempre riferimento in modo esplicito a tutte le proprietà, incluse quelle predefinite.  
  
## Vedere anche  
 [Routine Property](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [Procedure Parameters and Arguments](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Property Statement](../../../../visual-basic/language-reference/statements/property-statement.md)   
 [Default](../../../../visual-basic/language-reference/modifiers/default.md)   
 [Differences Between Properties and Variables in Visual Basic](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-properties-and-variables.md)   
 [How to: Create a Property](../../../../visual-basic/programming-guide/language-features/procedures/how-to-create-a-property.md)   
 [How to: Declare a Property with Mixed Access Levels](../../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-a-property-with-mixed-access-levels.md)   
 [How to: Call a Property Procedure](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-a-property-procedure.md)   
 [How to: Put a Value in a Property](../../../../visual-basic/programming-guide/language-features/procedures/how-to-put-a-value-in-a-property.md)   
 [How to: Get a Value from a Property](../../../../visual-basic/programming-guide/language-features/procedures/how-to-get-a-value-from-a-property.md)