---
title: "Widening and Narrowing Conversions (Visual Basic) | Microsoft Docs"
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
  - "widening conversions"
  - "narrowing conversions"
  - "conversions, type"
  - "data types [Visual Basic], changing"
  - "variables [Visual Basic], changing data type"
  - "conversions, exceptions during conversion"
  - "type conversion, exceptions during conversion"
  - "conversions, data type"
  - "conversions, narrowing"
  - "type conversion, narrowing"
  - "data type conversion, widening"
  - "data type conversion, narrowing"
  - "changing data types"
  - "type conversion, widening"
  - "data type conversion, exceptions during conversion"
  - "conversions, widening"
ms.assetid: 058c3152-6c28-4268-af44-2209e774f0bd
caps.latest.revision: 27
caps.handback.revision: 27
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Widening and Narrowing Conversions (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Un aspetto importante da considerare durante una conversione di tipo è se il risultato della conversione è compreso o meno nell'intervallo del tipo di dati di destinazione.  
  
 In *conversione di ampliamento* modifica di un valore a un tipo di dati che può consentire tutti i valori possibili dei dati originali.  Le conversioni verso un tipo di dati più grande preservano il valore di origine ma possono modificarne la rappresentazione.  Ciò si verifica se si esegue la conversione da un tipo integrale a `Decimal`, o da  `Char` in  `String`.  
  
 Una *conversione di restrizione* esegue il passaggio di un valore a un tipo di dati che potrebbe non essere in grado di contenere alcuni dei valori possibili.  Ad esempio, un valore frazionario viene arrotondato quando viene convertito in un tipo integrale e un tipo numerico convertito in `Boolean` viene ridotto peruna o l'altra  `True` o  `False`.  
  
## Conversioni di ampliamento  
 Nella tabella che segue sono illustrate le conversioni di ampliamento standard.  
  
|||  
|-|-|  
|Tipo di dati|Tipi di dati risultanti dalla conversione a un tipo di dati più grande <sup>1</sup>|  
|[SByte](../../../../visual-basic/language-reference/data-types/sbyte-data-type.md)|`SByte`, `Short`, `Integer`, `Long`, `Decimal`, `Single`, `Double`|  
|[Byte](../../../../visual-basic/language-reference/data-types/byte-data-type.md)|`Byte`, `Short`, `UShort`, `Integer`, `UInteger`, `Long`, `ULong`, `Decimal`, `Single`, `Double`|  
|[Short](../../../../visual-basic/language-reference/data-types/short-data-type.md)|`Short`, `Integer`, `Long`, `Decimal`, `Single`, `Double`|  
|[UShort](../../../../visual-basic/language-reference/data-types/ushort-data-type.md)|`UShort`, `Integer`, `UInteger`, `Long`, `ULong`, `Decimal`, `Single`, `Double`|  
|[Integer](../../../../visual-basic/language-reference/data-types/integer-data-type.md)|`Integer`, `Long`, `Decimal`, `Single`, `Double`<sup>2</sup>|  
|[UInteger](../../../../visual-basic/language-reference/data-types/uinteger-data-type.md)|`UInteger`, `Long`, `ULong`, `Decimal`, `Single`, `Double` <sup>2</sup>|  
|[Long](../../../../visual-basic/language-reference/data-types/long-data-type.md)|`Long`, `Decimal`, `Single`, `Double` <sup>2</sup>|  
|[ULong](../../../../visual-basic/language-reference/data-types/ulong-data-type.md)|`ULong`, `Decimal`, `Single`, `Double` <sup>2</sup>|  
|[Decimal](../../../../visual-basic/language-reference/data-types/decimal-data-type.md)|`Decimal`, `Single`, `Double` <sup>2</sup>|  
|[Single](../../../../visual-basic/language-reference/data-types/single-data-type.md)|`Single`, `Double`|  
|[Double](../../../../visual-basic/language-reference/data-types/double-data-type.md)|`Double`|  
|Qualsiasi tipo enumerato \([Enum](../../../../visual-basic/language-reference/statements/enum-statement.md)\)|Il tipo integrale sottostante e qualsiasi tipo che viene convertito il tipo sottostante.|  
|[Char](../../../../visual-basic/language-reference/data-types/char-data-type.md)|`Char`, `String`|  
|Matrice `Char`|Matrice `Char`, `String`|  
|Qualsiasi tipo|[Object](../../../../visual-basic/language-reference/data-types/object-data-type.md)|  
|Qualsiasi tipo derivato|qualsiasi tipo di base da cui è derivato <sup>3</sup>.|  
|Qualsiasi tipo|qualsiasi interfaccia che implementa.|  
|[Nothing](../../../../visual-basic/language-reference/nothing.md)|qualsiasi tipo di dati o tipo di oggetto.|  
  
 <sup>1</sup> Per definizione, ogni tipo di dati viene ampliato in se stesso.  
  
 <sup>2</sup> Le conversioni da `Integer`, `UInteger`, `Long`, `ULong` o `Decimal` a `Single` o `Double` possono comportare una perdita nella precisione, ma non una riduzione dell'ordine di grandezza.  In questo senso non sono soggette a perdita di informazioni.  
  
 <sup>3</sup> Può apparire sorprendente che una conversione da un tipo derivato a uno dei relativi tipi di base sia una conversione di ampliamento.  Il motivo è che il tipo derivato contiene tutti i membri del tipo di base, pertanto viene qualificato come un'istanza del tipo di base.  Viceversa, il tipo di base non contiene nuovi membri definiti dal tipo derivato.  
  
 Le conversioni di ampliamento vengono sempre eseguite correttamente in fase di esecuzione e non comportano mai una perdita di dati.  È sempre possibile eseguirle in modo implicito, indipendentemente dal fatto che l'[Option Strict Statement](../../../../visual-basic/language-reference/statements/option-strict-statement.md) imposti l'opzione di controllo dei tipi su `On` o su `Off`.  
  
## Conversioni di restrizione  
 Di seguito sono elencate le conversioni di restrizione standard:  
  
-   Le direzioni inverse delle conversioni di ampliamento elencate nella tabella precedente \(tranne quella che prevede che ogni tipo viene ampliato in se stesso\)  
  
-   Le conversioni, in entrambe le direzioni, tra valori [Boolean](../../../../visual-basic/language-reference/data-types/boolean-data-type.md) e un qualsiasi tipo numerico  
  
-   Le conversioni da un qualsiasi tipo numerico in un qualsiasi tipo enumerato \(`Enum`\)  
  
-   Le conversioni, in entrambe le direzioni, tra valori [String](../../../../visual-basic/language-reference/data-types/string-data-type.md) e un qualsiasi tipo numerico, `Boolean` o [Date](../../../../visual-basic/language-reference/data-types/date-data-type.md)  
  
-   Le conversioni da un tipo di dati o tipo di oggetto a un tipo da esso derivato  
  
 Le conversioni di restrizione non vengono sempre eseguite correttamente in fase di esecuzione e possono causare una perdita di dati.  Viene generato un errore se il tipo di dati di destinazione non è in grado di ricevere il valore convertito.  Una conversione numerica ad esempio può comportare un overflow.  Il compilatore non consente di eseguire conversioni di restrizione in modo implicito, a meno che l'[Option Strict Statement](../../../../visual-basic/language-reference/statements/option-strict-statement.md) non imposti l'opzione di controllo dei tipi su `Off`.  
  
> [!NOTE]
>  L'errore di conversione verso un tipo di dati più piccolo viene eliminato per le conversioni dagli elementi di una raccolta `For Each…Next` alla variabile di controllo del ciclo.  Per ulteriori informazioni ed esempi, vedere la sezione "Conversioni verso tipi di dati più piccoli" di [Istruzione For Each...Next](../../../../visual-basic/language-reference/statements/for-each-next-statement.md).  
  
### Quando utilizzare le conversioni di restrizione  
 Si consiglia di utilizzare una conversione di restrizione quando si è certi che il valore di origine può essere convertito nel tipo di dati di destinazione senza errori o perdita di dati.  Ad esempio, se si dispone di un oggetto `String` stabilito contiene o “true„ o “False„, è possibile utilizzare  `CBool` parola chiave per convertirla a  `Boolean`.  
  
## Eccezioni durante la conversione  
 Dal momento che hanno sempre esito positivo, le conversioni di ampliamento non generano eccezioni.  Quando non riescono, le conversioni di restrizione generano di solito le seguenti eccezioni:  
  
-   <xref:System.InvalidCastException>: se non è definita alcuna conversione tra i due tipi  
  
-   <xref:System.OverflowException>: \(solo tipi integrali\) se il valore convertito è troppo grande per il tipo di destinazione  
  
 Se una classe o una struttura definisce una [Funzione CType](../../../../visual-basic/language-reference/functions/ctype-function.md) da utilizzare come operatore di conversione rispetto a tale classe o struttura, la funzione `CType` può generare qualsiasi eccezione ritenuta appropriata.  Inoltre, l'oggetto `CType` potrebbe chiamare funzioni di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] o metodi di [!INCLUDE[dnprdnshort](../../../../csharp/getting-started/includes/dnprdnshort_md.md)] che a loro volta potrebbero generare diverse eccezioni.  
  
## Modifiche durante conversioni di tipi riferimento  
 Una conversione da un *tipo di riferimento* copia solo il puntatore al valore.  Il valore in sé non viene in alcun modo copiato né modificato.  L'unica differenza può essere rappresentata dal tipo di dati della variabile contenente il puntatore.  Nell'esempio che segue il tipo di dati viene convertito dalla classe derivata nella relativa classe di base, ma l'oggetto al quale ora puntano entrambe le variabili è invariato.  
  
```  
' Assume class cSquare inherits from class cShape.  
Dim shape As cShape  
Dim square As cSquare = New cSquare  
' The following statement performs a widening  
' conversion from a derived class to its base class.  
shape = square  
```  
  
## Vedere anche  
 [Riepilogo dei tipi di dati](../../../../visual-basic/programming-guide/language-features/data-types/index.md)   
 [Type Conversions in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [Implicit and Explicit Conversions](../../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md)   
 [Conversions Between Strings and Other Types](../../../../visual-basic/programming-guide/language-features/data-types/conversions-between-strings-and-other-types.md)   
 [How to: Convert an Object to Another Type in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/how-to-convert-an-object-to-another-type.md)   
 [Array Conversions](../../../../visual-basic/programming-guide/language-features/data-types/array-conversions.md)   
 [Data Types](../../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Type Conversion Functions](../../../../visual-basic/language-reference/functions/type-conversion-functions.md)