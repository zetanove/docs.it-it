---
title: "String Data Type (Visual Basic) | Microsoft Docs"
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
  - "vb.String"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "strings [Visual Basic], character"
  - "strings [Visual Basic], fixed-length"
  - "string keyword [Visual Basic]"
  - "fixed-length strings, string data type"
  - "literals, string"
  - "text [Visual Basic], String data type"
  - "$ identifier type character"
  - "String data type"
  - "fixed-length strings"
  - "string literals"
  - "data types [Visual Basic], assigning"
  - "" String literals"
  - "identifier type characters, $"
ms.assetid: 15ac03f5-cabd-42cc-a754-1df3893c25d9
caps.latest.revision: 19
caps.handback.revision: 19
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# String Data Type (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Contiene sequenze di punti di codici senza segno a 16 bit \(2 byte\) in un intervallo compreso tra 0 e 65535.  Ogni *punto di codice*o codice carattere rappresenta un solo carattere Unicode.  Una stringa può contenere da 0 a circa 2 miliardi \(2 ^ 31\) di caratteri Unicode.  
  
## Note  
 Utilizzare il tipo di dati `String` per contenere più caratteri senza overhead nella gestione di `Char()`, una matrice di elementi `Char`.  
  
 Il valore predefinito di `String` è `Nothing`, un riferimento null.  Si noti che questo valore non corrisponde alla stringa vuota \(valore `""`\).  
  
## Caratteri Unicode  
 I primi 128 punti di codice \(0\-127\) di Unicode corrispondono alle lettere e ai simboli di una tastiera americana standard.  tastiera.  Questi primi 128 punti di codice corrispondono a quelli definiti dal set di caratteri ASCII.  I successivi 128 punti di codice \(da 128 a 255\) sono caratteri speciali, quali lettere di alfabeti internazionali, accenti, simboli di valuta e frazioni.  Unicode utilizza gli elementi di codice rimanenti \(256\-65535\) per un'ampia varietà di simboli,  inclusi i caratteri testuali, segni diacritici e simboli matematici e tecnici utilizzati a livello mondiale.  
  
 È possibile utilizzare metodi quali <xref:System.Char.IsDigit%2A> e <xref:System.Char.IsPunctuation%2A> su un singolo carattere di una variabile di tipo `String` per determinarne la classificazione Unicode.  
  
## Requisiti di formato  
 È necessario racchiudere un valore letterale `String` tra virgolette \(`" "`\).  Se è necessario includere le virgolette come carattere nella stringa, utilizzare due virgolette contigue \(`""`\).  Questa condizione è illustrata nell'esempio che segue.  
  
```  
Dim j As String = "Joe said ""Hello"" to me."  
Dim h As String = "Hello"  
' The following messages all display the same thing:  
' "Joe said "Hello" to me."  
MsgBox(j)  
MsgBox("Joe said " & """" & h & """" & " to me.")  
MsgBox("Joe said """ & h & """ to me.")  
```  
  
 Le virgolette contigue che rappresentano le virgolette nella stringa sono indipendenti da quelle che indicano l'inizio e la fine del valore letterale `String`.  
  
## Modifica delle stringhe  
 Dopo aver assegnato una stringa a una variabile di tipo `String`, tale stringa diventa *non modificabile*, ossia non è possibile modificarne la lunghezza né il contenuto.  Quando si apportano modifiche una stringa, viene creata una nuova stringa e la precedente viene abbandonata.  La variabile `String` fa quindi riferimento alla nuova stringa.  
  
 Per modificare il contenuto di una variabile `String`, è possibile utilizzare una serie di funzioni di stringa.  Nell'esempio seguente viene illustrata la funzione <xref:Microsoft.VisualBasic.Strings.Left%2A>.  
  
```  
Dim S As String = "Database"  
' The following statement sets S to a new string containing "Data".  
S = Microsoft.VisualBasic.Left(S, 4)  
```  
  
 Una stringa creata da un altro componente può essere completata con spazi iniziali o finali.  Se si riceve una stringa di questo tipo, è possibile rimuovere gli spazi utilizzando le funzioni <xref:Microsoft.VisualBasic.Strings.Trim%2A>, <xref:Microsoft.VisualBasic.Strings.LTrim%2A> e <xref:Microsoft.VisualBasic.Strings.RTrim%2A>.  
  
 Per ulteriori informazioni sulla modifica delle stringhe, vedere [Strings](../../../visual-basic/programming-guide/language-features/strings/index.md).  
  
## Suggerimenti per la programmazione  
  
-   **Numeri negativi.** Tenere presente che i caratteri inclusi in `String` sono senza segno e non possono rappresentare valori negativi.  In ogni caso, si consiglia di non utilizzare `String` per includere valori numerici.  
  
-   **Considerazioni sull'interoperabilità.** Se si prevede l'interazione con componenti non scritti per .NET Framework, ad esempio oggetti COM o di automazione, tenere presente che in altri ambienti i caratteri di stringa hanno un'ampiezza di dati diversa \(8 bit\).  Se si passa un argomento stringa di caratteri a 8 bit a un componente di questo tipo, nel nuovo codice Visual Basic è necessario eseguirne la dichiarazione come `Byte()`, una matrice di elementi `Byte`, anziché come `String`.  
  
-   **Caratteri tipo.** Aggiungendo il carattere di tipo identificatore `$` a qualsiasi identificatore, se ne determina la conversione al tipo di dati `String`.  `String` non ha alcun carattere di tipo letterale.  Il compilatore considera tuttavia i valori letterali racchiusi tra virgolette \(`" "`\) come valori di tipo `String`.  
  
-   **Tipo Framework.** Il tipo corrispondente in .NET Framework è la classe <xref:System.String?displayProperty=fullName>.  
  
## Vedere anche  
 <xref:System.String?displayProperty=fullName>   
 [Data Types](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Char Data Type](../../../visual-basic/language-reference/data-types/char-data-type.md)   
 [Type Conversion Functions](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [Riepilogo della conversione](../../../visual-basic/language-reference/keywords/conversion-summary.md)   
 [How to: Call a Windows Function that Takes Unsigned Types](../../../visual-basic/programming-guide/com-interop/how-to-call-a-windows-function-that-takes-unsigned-types.md)   
 [Efficient Use of Data Types](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)