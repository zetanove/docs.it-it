---
title: Tipo di dati (Visual Basic) stringa | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.String
dev_langs:
- VB
helpviewer_keywords:
- strings [Visual Basic], character
- strings [Visual Basic], fixed-length
- string keyword [Visual Basic]
- fixed-length strings, string data type
- literals, string
- text [Visual Basic], String data type
- $ identifier type character
- String data type
- fixed-length strings
- string literals
- data types [Visual Basic], assigning
- String literals
- identifier type characters, $
ms.assetid: 15ac03f5-cabd-42cc-a754-1df3893c25d9
caps.latest.revision: 19
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
ms.openlocfilehash: 9221a89a1fb46609b4b8550968e3a2bbe874772c
ms.lasthandoff: 03/13/2017

---
# <a name="string-data-type-visual-basic"></a>Tipo di dati String (Visual Basic)
Contiene le sequenze di punti di codice di (2 byte) senza segno a 16 bit quell'intervallo compreso tra 0 e 65535. Ogni *punto di codice*, o codice carattere, rappresenta un singolo carattere Unicode. Una stringa può contenere da 0 a circa 2 miliardi (2 ^ 31) i caratteri Unicode.  
  
## <a name="remarks"></a>Note  
 Utilizzare il `String` tipo di dati per contenere più caratteri senza overhead nella gestione di `Char()`, una matrice di `Char` elementi.  
  
 Il valore predefinito di `String` è `Nothing` (un riferimento null). Si noti che questo non corrisponde alla stringa vuota (valore `""`).  
  
## <a name="unicode-characters"></a>Caratteri Unicode  
 I primo 128 punti di codice (da 0 a 127) di Unicode corrispondono alle lettere e simboli di tastiera standard. Questi primi punti di 128 codice sono gli stessi di quelli definisce il set di caratteri ASCII. I secondo 128 punti di codice (128-255) rappresentano caratteri speciali, ad esempio lettere dell'alfabeto latino, accenti, simboli di valuta e le frazioni di secondo. Unicode utilizza i punti di codice rimanenti (256-65535) per un'ampia gamma di simboli. Sono inclusi caratteri testuali in tutto il mondo, i segni diacritici e simboli matematici e tecnici.  
  
 È possibile utilizzare i metodi, ad esempio <xref:System.Char.IsDigit%2A>e <xref:System.Char.IsPunctuation%2A>su un singolo carattere in un `String` variabile per determinarne la classificazione Unicode.</xref:System.Char.IsPunctuation%2A> </xref:System.Char.IsDigit%2A>  
  
## <a name="format-requirements"></a>Requisiti di formato  
 È necessario racchiudere un `String` letterale racchiusa tra virgolette (`" "`). Se è necessario includere una virgoletta come uno dei caratteri nella stringa, utilizzare due virgolette contigue (`""`). Questa condizione è illustrata nell'esempio seguente.  
  
```  
Dim j As String = "Joe said ""Hello"" to me."  
Dim h As String = "Hello"  
' The following messages all display the same thing:  
' "Joe said "Hello" to me."  
MsgBox(j)  
MsgBox("Joe said " & """" & h & """" & " to me.")  
MsgBox("Joe said """ & h & """ to me.")  
```  
  
 Si noti che le virgolette contigue che rappresentano le virgolette nella stringa sono indipendenti dalle virgolette che iniziano e terminano le `String` letterale.  
  
## <a name="string-manipulations"></a>Manipolazioni di stringhe  
 Dopo aver assegnato una stringa a un `String` è variabile, tale stringa *non modificabile*, ovvero è possibile modificare la lunghezza o il contenuto. Quando si modifica una stringa in alcun modo, Visual Basic crea una nuova stringa e la precedente viene abbandonata. Il `String` variabile fa quindi riferimento alla nuova stringa.  
  
 È possibile modificare il contenuto di un `String` variabile utilizzando un'ampia gamma di funzioni di stringa. Nell'esempio seguente viene illustrata la <xref:Microsoft.VisualBasic.Strings.Left%2A>funzione</xref:Microsoft.VisualBasic.Strings.Left%2A>  
  
```  
Dim S As String = "Database"  
' The following statement sets S to a new string containing "Data".  
S = Microsoft.VisualBasic.Left(S, 4)  
```  
  
 Una stringa creata da un altro componente può essere completata con spazi iniziali o finali. Se si riceve una stringa di questo tipo, è possibile utilizzare il <xref:Microsoft.VisualBasic.Strings.Trim%2A>, <xref:Microsoft.VisualBasic.Strings.LTrim%2A>, e <xref:Microsoft.VisualBasic.Strings.RTrim%2A>funzioni per rimuovere gli spazi.</xref:Microsoft.VisualBasic.Strings.RTrim%2A> </xref:Microsoft.VisualBasic.Strings.LTrim%2A> </xref:Microsoft.VisualBasic.Strings.Trim%2A>  
  
 Per ulteriori informazioni sulle stringhe, vedere [stringhe](../../../visual-basic/programming-guide/language-features/strings/index.md).  
  
## <a name="programming-tips"></a>Suggerimenti per la programmazione  
  
-   **Numeri negativi.** Tenere presente che i caratteri inclusi in `String` non sono firmati e non può rappresentare valori negativi. In ogni caso, è consigliabile non utilizzare `String` per includere valori numerici.  
  
-   **Considerazioni sull'interoperabilità.** Se si prevede l'interazione con componenti non scritti per .NET Framework, ad esempio oggetti COM o di automazione, tenere presente che i caratteri di stringa hanno un'ampiezza dei dati diversa (8 bit) in altri ambienti. Se si passa un argomento di stringa di caratteri a 8 bit a tale componente, dichiararla come `Byte()`, una matrice di `Byte` elementi, anziché `String` nel nuovo codice Visual Basic.  
  
-   **Caratteri tipo.** Aggiungendo il carattere di tipo identificatore `$` a qualsiasi identificatore e ne impone il `String` tipo di dati. `String`non include alcun carattere tipo effettivo. Tuttavia, il compilatore considera i valori letterali racchiusi tra virgolette (`" "`) come `String`.  
  
-   **Tipo di Framework.** Il tipo corrispondente in .NET Framework è la <xref:System.String?displayProperty=fullName>classe.</xref:System.String?displayProperty=fullName>  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.String?displayProperty=fullName></xref:System.String?displayProperty=fullName>   
 [Tipi di dati](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Tipo di dati Char](../../../visual-basic/language-reference/data-types/char-data-type.md)   
 [Funzioni di conversione del tipo](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [Riepilogo della conversione](../../../visual-basic/language-reference/keywords/conversion-summary.md)   
 [Procedura: chiamare una funzione Windows che accetta tipi senza segno](../../../visual-basic/programming-guide/com-interop/how-to-call-a-windows-function-that-takes-unsigned-types.md)   
 [Uso efficiente dei tipi di dati](../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)

