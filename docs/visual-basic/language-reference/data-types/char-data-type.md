---
title: "Char Data Type (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.Char"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "literal type characters, C"
  - "Char data type"
  - "C literal type character"
  - "data types [Visual Basic], assigning"
  - "Char data type, character literals"
ms.assetid: cd7547a9-7855-4e8e-b216-35d74a362657
caps.latest.revision: 17
caps.handback.revision: 17
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Char Data Type (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Contiene punti di codice senza segno a 16 bit \(2 byte\) in un intervallo compreso tra 0 e 65535.  Ogni *punto di codice*o codice carattere rappresenta un solo carattere Unicode.  
  
## Note  
 Per contenere un solo carattere senza overhead di `String`, è possibile utilizzare il tipo di dati `Char`.  In alcuni casi, è possibile utilizzare `Char()`, una matrice di elementi `Char`, per contenere più caratteri.  
  
 Il valore predefinito di `Char` è il carattere con un punto di codice pari a 0.  
  
## Caratteri Unicode  
 I primi 128 punti di codice \(0\-127\) di Unicode corrispondono alle lettere e ai simboli di una tastiera americana standard.  tastiera.  Questi primi 128 punti di codice corrispondono a quelli definiti dal set di caratteri ASCII.  I successivi 128 punti di codice \(da 128 a 255\) sono caratteri speciali, quali lettere di alfabeti internazionali, accenti, simboli di valuta e frazioni.  I rimamenti punti di codice \(256\-65535\) vengono utilizzati per un'ampia gamma di simboli, inclusi caratteri testuali universali, segni diacritici e simboli matematici e tecnici.  
  
 È possibile utilizzare metodi quali <xref:System.Char.IsDigit%2A> e <xref:System.Char.IsPunctuation%2A> su una variabile `Char` per determinarne la classificazione Unicode.  
  
## Conversioni di tipi  
 In Visual Basic non viene effettuata direttamente la conversione tra il tipo `Char` e i tipi numerici.  È possibile utilizzare la funzione <xref:Microsoft.VisualBasic.Strings.Asc%2A> o <xref:Microsoft.VisualBasic.Strings.AscW%2A> per convertire un valore `Char` in un `Integer` che rappresenti il relativo punto di codice.  È possibile utilizzare la funzione <xref:Microsoft.VisualBasic.Strings.Chr%2A> o <xref:Microsoft.VisualBasic.Strings.ChrW%2A> per convertire un valore `Integer` in un `Char` con tale punto di codice.  
  
 Se è attivata l'opzione di controllo dei tipi \([Option Strict Statement](../../../visual-basic/language-reference/statements/option-strict-statement.md)\), è necessario aggiungere il carattere di tipo letterale a una stringa letterale a carattere singolo per identificarla come tipo di dati `Char`.  Questa condizione è illustrata nell'esempio che segue.  
  
```  
Option Strict On  
Dim charVar As Char  
' The following statement attempts to convert a String literal to Char.  
' Because Option Strict is On, it generates a compiler error.  
charVar = "Z"  
' The following statement succeeds because it specifies a Char literal.  
charVar = "Z"C  
```  
  
## Suggerimenti per la programmazione  
  
-   **Numeri negativi.** `Char` è un tipo senza segno e non può rappresentare un valore negativo.  In ogni caso, si consiglia di non utilizzare `Char` per includere valori numerici.  
  
-   **Considerazioni sull'interoperabilità.** Se si prevede l'interazione con componenti non scritti per .NET Framework, ad esempio oggetti COM o di automazione, tenere presente che in altri ambienti i tipi di carattere presentano un'ampiezza di dati diversa \(8 bit\).  Se si passa un argomento a 8 bit a un componente di questo tipo, nel nuovo codice Visual Basic è necessario eseguirne la dichiarazione come `Byte` anziché come `Char`.  
  
-   **Conversione verso un tipo di dati più grande.** Il tipo di dati `Char` viene convertito verso il tipo più grande `String`.  In altri termini, è possibile convertire `Char` in `String` senza che si verifichi un errore <xref:System.OverflowException?displayProperty=fullName>.  
  
-   **Caratteri tipo.** Aggiungendo il carattere di tipo letterale `C` a un valore letterale stringa a carattere singolo, se ne determina la conversione nel tipo di dati `Char`.  Il tipo `Char` non dispone di caratteri di tipo identificatore.  
  
-   **Tipo Framework.** Il tipo corrispondente in .NET Framework è la struttura <xref:System.Char?displayProperty=fullName>.  
  
## Vedere anche  
 <xref:System.Char?displayProperty=fullName>   
 <xref:Microsoft.VisualBasic.Strings.Asc%2A>   
 <xref:Microsoft.VisualBasic.Strings.AscW%2A>   
 <xref:Microsoft.VisualBasic.Strings.Chr%2A>   
 <xref:Microsoft.VisualBasic.Strings.ChrW%2A>   
 [Data Types](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [String Data Type](../../../visual-basic/language-reference/data-types/string-data-type.md)   
 [Type Conversion Functions](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [Riepilogo della conversione](../../../visual-basic/language-reference/keywords/conversion-summary.md)   
 [How to: Call a Windows Function that Takes Unsigned Types](../../../visual-basic/programming-guide/com-interop/how-to-call-a-windows-function-that-takes-unsigned-types.md)   
 [Efficient Use of Data Types](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)