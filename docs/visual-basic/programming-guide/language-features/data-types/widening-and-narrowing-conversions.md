---
title: Ampliamento e restrizione conversioni (Visual Basic) | Documenti di Microsoft
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
- widening conversions
- narrowing conversions
- conversions, type
- data types [Visual Basic], changing
- variables [Visual Basic], changing data type
- conversions, exceptions during conversion
- type conversion, exceptions during conversion
- conversions, data type
- conversions, narrowing
- type conversion, narrowing
- data type conversion, widening
- data type conversion, narrowing
- changing data types
- type conversion, widening
- data type conversion, exceptions during conversion
- conversions, widening
ms.assetid: 058c3152-6c28-4268-af44-2209e774f0bd
caps.latest.revision: 27
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
ms.openlocfilehash: 88c5db6e7e82a88ae8015b581e5a795ec389d003
ms.lasthandoff: 03/13/2017

---
# <a name="widening-and-narrowing-conversions-visual-basic"></a>Conversioni di ampliamento e restrizione (Visual Basic)
Una considerazione importante con una conversione del tipo è se il risultato della conversione è compreso nell'intervallo del tipo di dati di destinazione.  
  
 Oggetto *conversione di ampliamento* modifica un valore in un tipo di dati che consente di eseguire tutti i valori possibili dei dati originali.  Conversioni di ampliamento mantiene il valore di origine, ma possono modificarne la rappresentazione. Ciò si verifica se si converte da un tipo integrale a `Decimal`, o da `Char` a `String`.  
  
 Una *conversione verso un tipo di dati più piccolo* imposta un valore su un tipo di dati che potrebbe non contenere alcuni dei possibili valori. Ad esempio, un valore frazionario viene arrotondato quando viene convertito in un tipo integrale e un tipo numerico convertito in `Boolean` viene ridotto a `True` o `False`.  
  
## <a name="widening-conversions"></a>Conversioni verso un tipo di dati più grande  
 Nella tabella seguente mostra le conversioni di ampliamento standard.  
  
|Tipo di dati|Si amplia in tipi di dati <sup>1</sup>|  
|---|---|  
|[SByte](../../../../visual-basic/language-reference/data-types/sbyte-data-type.md)|`SByte`, `Short`, `Integer`, `Long`, `Decimal`, `Single`, `Double`|  
|[Byte](../../../../visual-basic/language-reference/data-types/byte-data-type.md)|`Byte`, `Short`, `UShort`, `Integer`, `UInteger`, `Long`, `ULong`, `Decimal`, `Single`, `Double`|  
|[Breve](../../../../visual-basic/language-reference/data-types/short-data-type.md)|`Short`, `Integer`, `Long`, `Decimal`, `Single`, `Double`|  
|[UShort](../../../../visual-basic/language-reference/data-types/ushort-data-type.md)|`UShort`, `Integer`, `UInteger`, `Long`, `ULong`, `Decimal`, `Single`, `Double`|  
|[Valore integer](../../../../visual-basic/language-reference/data-types/integer-data-type.md)|`Integer`, `Long`, `Decimal`, `Single`, `Double`<sup>2</sup>|  
|[UInteger](../../../../visual-basic/language-reference/data-types/uinteger-data-type.md)|`UInteger`, `Long`, `ULong`, `Decimal`, `Single`, `Double`<sup>2</sup>|  
|[Long](../../../../visual-basic/language-reference/data-types/long-data-type.md)|`Long`, `Decimal`, `Single`, `Double`<sup>2</sup>|  
|[ULong](../../../../visual-basic/language-reference/data-types/ulong-data-type.md)|`ULong`, `Decimal`, `Single`, `Double`<sup>2</sup>|  
|[Decimal](../../../../visual-basic/language-reference/data-types/decimal-data-type.md)|`Decimal`, `Single`, `Double`<sup>2</sup>|  
|[Single](../../../../visual-basic/language-reference/data-types/single-data-type.md)|`Single`, `Double`|  
|[Double](../../../../visual-basic/language-reference/data-types/double-data-type.md)|`Double`|  
|Qualsiasi tipo enumerato ([Enum](../../../../visual-basic/language-reference/statements/enum-statement.md))|Il tipo integrale sottostante e qualsiasi tipo a cui può ampliarsi nel tipo sottostante.|  
|[Char](../../../../visual-basic/language-reference/data-types/char-data-type.md)|`Char`, `String`|  
|Matrice `Char`|`Char`matrice,`String`|  
|Qualsiasi tipo|[Oggetto](../../../../visual-basic/language-reference/data-types/object-data-type.md)|  
|Qualsiasi tipo derivato|Qualsiasi tipo da cui deriva base <sup>3</sup>.|  
|Qualsiasi tipo|Qualsiasi interfaccia implementata.|  
|[Nothing](../../../../visual-basic/language-reference/nothing.md)|Qualsiasi tipo di dati o un tipo di oggetto.|  
  
 <sup>1</sup> per definizione, ogni tipo di dati viene ampliato a se stesso.  
  
 <sup>2</sup> le conversioni da `Integer`, `UInteger`, `Long`, `ULong`, o `Decimal` a `Single` o `Double` possono comportare una perdita di precisione, ma mai in ordine di grandezza. In questo senso non comportano la perdita di informazioni.  
  
 <sup>3</sup> potrebbe sembrare sorprendente che una conversione da un tipo derivato a uno dei tipi di base è una conversione di ampliamento. Il motivo è che il tipo derivato contiene tutti i membri del tipo di base, pertanto viene qualificato come un'istanza del tipo di base. Nella direzione opposta, il tipo di base non contiene tutti i nuovi membri definiti dal tipo derivato.  
  
 Le conversioni di ampliamento hanno sempre esito positivo in fase di esecuzione e non comportano perdita di dati. È sempre possibile eseguirle in modo implicito, se il [istruzione Option Strict](../../../../visual-basic/language-reference/statements/option-strict-statement.md) imposta il tipo di opzione per il controllo `On` o `Off`.  
  
## <a name="narrowing-conversions"></a>Conversioni verso un tipo di dati più piccolo  
 Di seguito sono elencate le conversioni di restrizione standard:  
  
-   Le direzioni inverse delle conversioni di ampliamento nella precedente tabella (ad eccezione del fatto che ogni tipo viene ampliato a se stesso)  
  
-   Le conversioni in entrambe le direzioni tra [booleano](../../../../visual-basic/language-reference/data-types/boolean-data-type.md) e qualsiasi tipo numerico  
  
-   Conversioni da qualsiasi tipo numerico a qualsiasi tipo enumerato (`Enum`)  
  
-   Le conversioni in entrambe le direzioni tra [stringa](../../../../visual-basic/language-reference/data-types/string-data-type.md) e qualsiasi tipo numerico, `Boolean`, o [Data](../../../../visual-basic/language-reference/data-types/date-data-type.md)  
  
-   Le conversioni da un tipo di dati o un oggetto tipo di un tipo derivato da esso  
  
 Le conversioni non sempre esito positivo in fase di esecuzione e non completato o perdita di dati. Si verifica un errore se il tipo di dati di destinazione non può ricevere il valore da convertire. Ad esempio, una conversione numerica può comportare un overflow. Il compilatore non consente di eseguire le conversioni in modo implicito a meno che il [istruzione Option Strict](../../../../visual-basic/language-reference/statements/option-strict-statement.md) imposta il tipo di opzione per il controllo `Off`.  
  
> [!NOTE]
>  Viene eliminato l'errore di conversione di restrizione per le conversioni da elementi di un `For Each…Next` insieme alla variabile di controllo del ciclo. Per ulteriori informazioni ed esempi, vedere la sezione "Conversioni di restrizione" [For Each... Istruzione successiva](../../../../visual-basic/language-reference/statements/for-each-next-statement.md).  
  
### <a name="when-to-use-narrowing-conversions"></a>Quando utilizzare le conversioni di restrizione  
 Si utilizza una conversione di narrowing quando si conosce che il valore di origine è convertibile nel tipo di dati di destinazione senza perdita di dati o di errore. Ad esempio, se si dispone di un `String` di conoscere contiene "True" o "False", è possibile utilizzare il `CBool` (parola chiave) per convertirlo in `Boolean`.  
  
## <a name="exceptions-during-conversion"></a>Eccezioni durante la conversione  
 Poiché le conversioni di ampliamento sempre esito positivo, non generano eccezioni. Le conversioni, quando non riescono, generano di solito le eccezioni seguenti:  
  
-   <xref:System.InvalidCastException>: se è definita alcuna conversione tra i due tipi</xref:System.InvalidCastException>  
  
-   <xref:System.OverflowException>-(solo tipi integrali) se il valore convertito è troppo grande per il tipo di destinazione</xref:System.OverflowException>  
  
 Se una classe o struttura definisce un [funzione CType](../../../../visual-basic/language-reference/functions/ctype-function.md) come un operatore di conversione da o verso tale classe o struttura, che `CType` possibile generare qualsiasi eccezione ritenuta appropriata. Inoltre, che `CType` potrebbe chiamare [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] funzioni o [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] metodi, che a sua volta potrebbero generare una varietà di eccezioni.  
  
## <a name="changes-during-reference-type-conversions"></a>Modifiche apportate durante le conversioni di tipo riferimento  
 Una conversione da un *tipo di riferimento* copia solo il puntatore al valore. Il valore stesso non viene copiato né modificato in alcun modo. L'unico elemento che è possibile modificare è il tipo di dati della variabile che contiene il puntatore. Nell'esempio seguente, il tipo di dati viene convertito dalla classe derivata a classe base, ma l'oggetto che entrambe le variabili a questo puntano rimane invariato.  
  
```  
' Assume class cSquare inherits from class cShape.  
Dim shape As cShape  
Dim square As cSquare = New cSquare  
' The following statement performs a widening  
' conversion from a derived class to its base class.  
shape = square  
```  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di dati](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [Conversioni di tipi in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [Conversioni implicite ed esplicite](../../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)   
 [Conversioni fra stringhe e altri tipi](../../../../visual-basic/programming-guide/language-features/data-types/conversions-between-strings-and-other-types.md)   
 [Procedura: convertire un oggetto in un altro tipo in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/how-to-convert-an-object-to-another-type.md)   
 [Conversioni di matrici](../../../../visual-basic/programming-guide/language-features/data-types/array-conversions.md)   
 [Tipi di dati](../../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Funzioni di conversione del tipo](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)
