---
title: "Conversions Between Strings and Other Types (Visual Basic) | Microsoft Docs"
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
  - "data type conversion, string"
  - "conversions, type"
  - "string conversion"
  - "conversions, data type"
  - "type conversion, string"
  - "regional options"
ms.assetid: c3a99596-f09a-44a5-81dd-1b89a094f1df
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# Conversions Between Strings and Other Types (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

È possibile convertire un valore numerico, `Boolean` o di data\/ora in un tipo `String`.  È inoltre possibile effettuare una conversione nella direzione inversa, da un valore stringa a un valore numerico, `Boolean` o `Date`, purché il contenuto della stringa possa essere interpretato come un valore valido del tipo di dati di destinazione.  In caso contrario, verrà generato un errore runtime.  
  
 Le conversioni relative a tutte queste assegnazioni, in entrambe le direzioni, sono conversioni di restrizione.  Si consiglia di utilizzare le parole chiave per la conversione dei tipi \(`CBool`, `CByte`, `CDate`, `CDbl`, `CDec`, `CInt`, `CLng`, `CSByte`, `CShort`, `CSng`, `CStr`, `CUInt`, `CULng`, `CUShort` e `CType`\).  Le funzioni <xref:Microsoft.VisualBasic.Strings.Format%2A> e <xref:Microsoft.VisualBasic.Conversion.Val%2A> offrono ulteriore controllo sulle conversioni tra stringhe e numeri.  
  
 Una volta definita una classe o una struttura, è possibile definire gli operatori di conversione dei tipi fra `String` e il tipo di classe o struttura.  Per ulteriori informazioni, vedere [How to: Define a Conversion Operator](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md).  
  
## Conversione di numeri in stringhe  
 È possibile utilizzare la funzione `Format` per convertire un numero in una stringa formattata che può includere non solo le cifre richieste, ma anche simboli di formattazione, quali un segno di valuta \(ad esempio `$`\), separatori delle migliaia o *simboli di raggruppamento delle cifre* \(ad esempio `,`\) e un separatore decimale \(ad esempio `.`\).   La funzione `Format` utilizza automaticamente i simboli appropriati in base alle **Impostazioni internazionali** definite nel **Pannello di controllo** di Windows.  
  
 L'operatore di concatenazione \(`&`\) consente di convertire un numero in una stringa in modo implicito, come illustrato nell'esempio che segue.  
  
```  
' The following statement converts count to a String value.  
Str = "The total count is " & count  
```  
  
## Conversione di stringhe in numeri  
 Per convertire esplicitamente le cifre di una stringa in un numero, è possibile utilizzare la funzione `Val`.  `Val` legge la stringa fino al rilevamento di un carattere diverso da una cifra, uno spazio, un segno di tabulazione, un avanzamento di riga o un punto.  Le sequenze "&O" e "&H" alterano la base del sistema numerico e terminano la scansione.  Finché non termina la lettura, `Val` converte tutti i caratteri appropriati in valori numerici.  L'istruzione che segue, ad esempio, restituisce il valore `141.825`.  
  
 `Val("   14   1.825 miles")`  
  
 Quando [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] converte una stringa in valore numerico, utilizza le **Impostazioni internazionali** specificate nel **Pannello di controllo** di Windows per interpretare il separatore delle migliaia, il separatore decimale e il simbolo di valuta.  Questo significa che una conversione può avere esito positivo con un'impostazione ma non con un'altra.  Ad esempio `"$14.20"` è accettabile con le impostazioni locali inglesi \(Stati Uniti d'America\) ma non con quelle francesi.  
  
## Vedere anche  
 [Type Conversions in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [Widening and Narrowing Conversions](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)   
 [Implicit and Explicit Conversions](../../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)   
 [How to: Convert an Object to Another Type in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/how-to-convert-an-object-to-another-type.md)   
 [Array Conversions](../../../../visual-basic/programming-guide/language-features/data-types/array-conversions.md)   
 [Data Types](../../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Type Conversion Functions](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [Introduzione alle applicazioni internazionali basate su .NET Framework](/visual-studio/ide/introduction-to-international-applications-based-on-the-dotnet-framework)