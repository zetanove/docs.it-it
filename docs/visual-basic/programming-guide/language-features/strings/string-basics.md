---
title: "String Basics in Visual Basic | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "strings [Visual Basic], Like operator"
  - "strings [Visual Basic], Visual Basic"
  - "strings [Visual Basic], regular expressions"
ms.assetid: 5674418d-f00d-4f72-9f98-d15897793350
caps.latest.revision: 14
caps.handback.revision: 14
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# String Basics in Visual Basic
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Il tipo di dati `String` rappresenta una serie di caratteri, ognuno dei quali, a sua volta, rappresenta un'istanza del tipo di dati `Char`.  Questo argomento illustra i concetti di base relativi alle stringhe in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  
  
## Variabili di tipo String  
 È possibile assegnare a un'istanza di una stringa un valore letterale che rappresenta una serie di caratteri.  Ad esempio:  
  
 [!code-vb[VbVbalrStrings#63](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-basics_1.vb)]  
  
 Una variabile `String` può accettare anche qualsiasi espressione che restituisca una stringa.  Di seguito sono riportati alcuni esempi.  
  
 [!code-vb[VbVbalrStrings#64](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-basics_2.vb)]  
  
 Qualsiasi valore letterale assegnato a una variabile `String` deve essere racchiuso tra virgolette \(""\).  Questo implica che all'interno di una stringa le virgolette non possono essere rappresentate dal segno di virgolette.  Il codice seguente, ad esempio, causa un errore di compilazione:  
  
 [!code-vb[VbVbalrStrings#65](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-basics_3.vb)]  
  
 L'errore è determinato dal fatto che durante la compilazione la stringa viene considerata terminata dopo il secondo segno di virgolette e il resto della stringa è interpretato come codice.  Per risolvere il problema, [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] interpreta due segni di virgolette presenti in un valore letterale stringa come un singolo segno di virgolette nella stringa.  L'esempio seguente illustra il modo corretto per inserire le virgolette in una stringa:  
  
 [!code-vb[VbVbalrStrings#66](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-basics_4.vb)]  
  
 Nell'esempio precedente, la coppia di virgolette che precede la parola `Look` diventa un segno di virgolette nella stringa.  Le tre serie di virgolette alla fine della riga rappresentano le virgolette appartenenti alla stringa seguite dal carattere di terminazione della stringa.  
  
 I valori letterali stringa possono contenere più righe:  
  
```vb  
Dim x = "hello  
world"  
  
```  
  
 La stringa risultante contiene le sequenze di nuove righe usate nel valore letterale stringa \(vbcr, vbcrlf e così via\).  Non è più necessario usare la soluzione alternativa precedente:  
  
```vb  
Dim x = <xml><![CDATA[Hello  
World]]></xml>.Value  
  
```  
  
## Caratteri nelle stringhe  
 Una stringa può essere considerata una serie di valori `Char`. Il tipo `String` è dotato di funzioni predefinite che consentono di eseguire numerose manipolazioni della stringa, simili a quelle consentite dalle matrici.  Come tutte le matrici in [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)], queste sono matrici in base zero.  Per fare riferimento a un carattere specifico di una stringa è possibile usare la proprietà `Chars`, che consente di accedere a un carattere in base alla sua posizione all'interno della stringa.  Ad esempio:  
  
 [!code-vb[VbVbalrStrings#67](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-basics_5.vb)]  
  
 Nell'esempio precedente, la proprietà `Chars` della stringa restituisce il quarto carattere della stringa, ovvero `D`, e lo assegna a `myChar`.  È anche possibile ottenere la lunghezza di una particolare stringa mediante la proprietà `Length`.  Se è necessario eseguire su una stringa più manipolazioni analoghe a quelle consentite nelle matrici, è possibile convertire la stringa in una matrice di istanze di `Char` usando la funzione `ToCharArray` della stringa.  Ad esempio:  
  
 [!code-vb[VbVbalrStrings#68](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-basics_6.vb)]  
  
 La variabile `myArray` ora contiene una matrice di istanze di `Char`, ognuna delle quali rappresenta un carattere di `myString`.  
  
## Immutabilità delle stringhe  
 Una stringa è *immutabile*, il suo valore, cioè, non può essere modificato dopo che è stata creata.  Questo non impedisce tuttavia di assegnare più valori a una variabile di tipo String.  Si consideri l'esempio seguente:  
  
 [!code-vb[VbVbalrStrings#69](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/string-basics_7.vb)]  
  
 In questo esempio, dopo aver creato una variabile stringa, le viene assegnato un valore che successivamente viene modificato.  
  
 Più precisamente, nella prima riga viene creata un'istanza di tipo `String` cui viene assegnato il valore `This string is immutable`.  Nella seconda riga dell'esempio viene creata una nuova istanza a cui viene assegnato il valore `Or is it?`. Il riferimento alla prima istanza viene quindi ignorato e con la variabile stringa viene archiviato il riferimento alla nuova istanza.  
  
 A differenza di altri tipi di dati intrinseci, `String` è un tipo riferimento.  Quando una variabile di tipo riferimento viene passata come argomento di una funzione o di una subroutine, invece del valore effettivo della stringa viene passato un riferimento all'indirizzo di memoria in cui sono archiviati i dati  Nell'esempio precedente, quindi, il nome della variabile rimane lo stesso, ma punta a un'istanza nuova e diversa della classe `String`, che contiene il nuovo valore.  
  
## Vedere anche  
 [Introduction to Strings in Visual Basic](../../../../visual-basic/programming-guide/language-features/strings/introduction-to-strings.md)   
 [String Data Type](../../../../visual-basic/language-reference/data-types/string-data-type.md)   
 [Char Data Type](../../../../visual-basic/language-reference/data-types/char-data-type.md)   
 [Operazioni di base su stringhe](../Topic/Basic%20String%20Operations%20in%20the%20.NET%20Framework.md)