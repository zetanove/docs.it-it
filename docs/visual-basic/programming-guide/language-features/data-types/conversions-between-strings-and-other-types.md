---
title: Conversioni fra stringhe e altri tipi (Visual Basic) | Documenti di Microsoft
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
- data type conversion, string
- conversions, type
- string conversion
- conversions, data type
- type conversion, string
- regional options
ms.assetid: c3a99596-f09a-44a5-81dd-1b89a094f1df
caps.latest.revision: 16
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
ms.openlocfilehash: 2d0a5fc7327ecd6339b5021e1b4cb87cc54bd2bc
ms.lasthandoff: 03/13/2017

---
# <a name="conversions-between-strings-and-other-types-visual-basic"></a>Conversioni fra stringhe e altri tipi (Visual Basic)
È possibile convertire un valore numerico, `Boolean`, o valore di data/ora un `String`. È inoltre possibile convertire nella direzione inversa, ovvero da un valore stringa e numerici, `Boolean`, o `Date` , purché il contenuto della stringa può essere interpretato come un valore valido del tipo di dati di destinazione. In caso contrario, si verifica un errore di run-time.  
  
 Le conversioni per tutte queste assegnazioni, in entrambe le direzioni, sono conversioni di restrizione. You should use the type conversion keywords (`CBool`, `CByte`, `CDate`, `CDbl`, `CDec`, `CInt`, `CLng`, `CSByte`, `CShort`, `CSng`, `CStr`, `CUInt`, `CULng`, `CUShort`, and `CType`). Il <xref:Microsoft.VisualBasic.Strings.Format%2A>e <xref:Microsoft.VisualBasic.Conversion.Val%2A>funzioni forniscono un maggiore controllo sulle conversioni fra stringhe e numeri.</xref:Microsoft.VisualBasic.Conversion.Val%2A> </xref:Microsoft.VisualBasic.Strings.Format%2A>  
  
 Se è stato definito una classe o struttura, è possibile definire operatori di conversione di tipo tra `String` e il tipo di classe o struttura. Per ulteriori informazioni, vedere [procedura: definire un operatore di conversione](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md).  
  
## <a name="conversion-of-numbers-to-strings"></a>Conversione di numeri in stringhe  
 È possibile utilizzare il `Format` funzione per convertire un numero in una stringa formattata, che può includere non solo le cifre appropriate ma anche simboli, ad esempio un simbolo di valuta di formattazione (ad esempio `$`), migliaia separatori o *i simboli di raggruppamento delle cifre* (come `,`) e un separatore decimale (come `.`). `Format`utilizza automaticamente i simboli appropriati in base al **opzioni internazionali** impostazioni specificate nelle finestre **Pannello di controllo**.  
  
 Si noti che il concatenamento (`&`) (operatore) può convertire un numero in una stringa in modo implicito, come illustrato nell'esempio seguente.  
  
```  
' The following statement converts count to a String value.  
Str = "The total count is " & count  
```  
  
## <a name="conversion-of-strings-to-numbers"></a>Conversione di stringhe in numeri  
 È possibile utilizzare il `Val` funzione per convertire esplicitamente le cifre in una stringa in un numero. `Val`legge la stringa fino a quando non viene rilevato un carattere diverso da una cifra, spazio, scheda, avanzamento riga o periodo. Le sequenze "/ O" e "/ H" alterano la base del sistema di numerazione e terminare l'analisi. Fino a quando termina la lettura, `Val` converte tutti i caratteri appropriati in un valore numerico. Ad esempio, l'istruzione seguente restituisce il valore `141.825`.  
  
 `Val("   14   1.825 miles")`  
  
 Quando [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] converte una stringa in un valore numerico, utilizza il **opzioni internazionali** impostazioni specificate nelle finestre **Pannello di controllo** per interpretare le migliaia separatore, il separatore decimale e il simbolo di valuta. Ciò significa che una conversione potrebbe avere esito positivo con un'impostazione ma non su un altro. Ad esempio, `"$14.20"` accettabile nelle impostazioni locali inglese (Stati Uniti) ma non in qualsiasi lingua francese.  
  
## <a name="see-also"></a>Vedere anche  
 [Conversioni di tipi in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [Ampliamento e restrizione conversioni](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md)   
 [Conversioni implicite ed esplicite](../../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)   
 [Procedura: convertire un oggetto in un altro tipo in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/how-to-convert-an-object-to-another-type.md)   
 [Conversioni di matrici](../../../../visual-basic/programming-guide/language-features/data-types/array-conversions.md)   
 [Tipi di dati](../../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Funzioni di conversione del tipo](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [Introduzione alle applicazioni internazionali basate su .NET Framework](https://docs.microsoft.com/visualstudio/ide/introduction-to-international-applications-based-on-the-dotnet-framework)
