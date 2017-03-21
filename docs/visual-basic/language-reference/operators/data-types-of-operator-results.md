---
title: Tipi di dati dei risultati degli operatori (Visual Basic) | Documenti di Microsoft
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
- data types [Visual Basic], operator result data types
- result data types
- operator result data types
- operators [Visual Basic], data types
- data types [Visual Basic], ranges
- operators [Visual Basic], result data types
ms.assetid: 9d524533-e1a1-4aa8-b1b8-622068173d06
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
ms.openlocfilehash: 577be6330cb76da436470c383841a717dd6e3200
ms.lasthandoff: 03/13/2017

---
# <a name="data-types-of-operator-results-visual-basic"></a>Tipi di dati dei risultati degli operatori (Visual Basic)
[!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]Determina il tipo di dati del risultato di un'operazione in base ai tipi di dati degli operandi. In alcuni casi potrebbe trattarsi di un tipo di dati con un intervallo maggiore rispetto a quello degli operandi.  
  
## <a name="data-type-ranges"></a>Intervalli dei tipi di dati  
 Gli intervalli dei tipi di dati rilevanti, in ordine dal più piccolo al più grande, sono i seguenti:  
  
-   [Booleano](../../../visual-basic/language-reference/data-types/boolean-data-type.md) , due valori possibili  
  
-   [SByte](../../../visual-basic/language-reference/data-types/sbyte-data-type.md), [Byte](../../../visual-basic/language-reference/data-types/byte-data-type.md) -256 valori integrali possibili  
  
-   [Breve](../../../visual-basic/language-reference/data-types/short-data-type.md), [UShort](../../../visual-basic/language-reference/data-types/ushort-data-type.md) , pari a 65.536 (6,5... E + 4) valori integrali possibili  
  
-   [Intero](../../../visual-basic/language-reference/data-types/integer-data-type.md), [UInteger](../../../visual-basic/language-reference/data-types/uinteger-data-type.md) -4.294.967.296 (4,2... E + 9) valori integrali possibili  
  
-   [Long](../../../visual-basic/language-reference/data-types/long-data-type.md), [ULong](../../../visual-basic/language-reference/data-types/ulong-data-type.md) -18.446.744.073.709.551.615 (1,8... E + 19) valori integrali possibili  
  
-   [Decimale](../../../visual-basic/language-reference/data-types/decimal-data-type.md) -1,5... E + 29 valori integrali possibili massimi intervallo 7,9... E + 28 (valore assoluto)  
  
-   [Singolo](../../../visual-basic/language-reference/data-types/single-data-type.md) : intervallo massimo 3.4... E + 38 (valore assoluto)  
  
-   [Double](../../../visual-basic/language-reference/data-types/double-data-type.md) : intervallo massimo 1.7... E + 308 (valore assoluto)  
  
 Per ulteriori informazioni su [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] tipi di dati, vedere [tipi di dati](../../../visual-basic/language-reference/data-types/data-type-summary.md).  
  
 Se un operando restituisce [nulla](../../../visual-basic/language-reference/nothing.md), [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] gli operatori aritmetici considerano come zero.  
  
## <a name="decimal-arithmetic"></a>Operazioni aritmetiche decimali  
 Si noti che il [decimale](../../../visual-basic/language-reference/data-types/decimal-data-type.md) tipo di dati non è né a virgola mobile né integer.  
  
 Se degli operandi di un `+`, `–`, `*`, `/`, o `Mod` operazione `Decimal` e l'altro non lo è `Single` o `Double`, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] amplia l'altro operando a `Decimal`. L'operazione viene eseguita in `Decimal`, e il tipo di dati del risultato è `Decimal`.  
  
## <a name="floating-point-arithmetic"></a>Aritmetica a virgola mobile  
 [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]esegue la maggior parte delle operazioni aritmetiche a virgola mobile in [Double](../../../visual-basic/language-reference/data-types/double-data-type.md), tipo di dati più efficiente per tali operazioni. Tuttavia, se uno degli operandi è [singolo](../../../visual-basic/language-reference/data-types/single-data-type.md) e l'altro non lo è `Double`, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] esegue l'operazione in `Single`. Il risultato è tale tipo di dati viene ampliato ogni operando in base alle esigenze per il tipo di dati appropriato prima dell'operazione.  
  
### <a name="-and--operators"></a>/ e ^ operatori  
 Il `/` è definito solo per il [decimale](../../../visual-basic/language-reference/data-types/decimal-data-type.md), [singolo](../../../visual-basic/language-reference/data-types/single-data-type.md), e [Double](../../../visual-basic/language-reference/data-types/double-data-type.md) tipi di dati. [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]Converte ogni operando in base alle esigenze per il tipo di dati appropriato prima dell'operazione e il risultato è il tipo di dati.  
  
 Nella tabella seguente viene illustrato il risultato tipi di dati per il `/` operatore. Si noti che questa tabella è simmetrica. per una determinata combinazione di tipi di dati di operando, il tipo di dati del risultato è lo stesso indipendentemente dall'ordine degli operandi.  
  
||||||  
|---|---|---|---|---|  
||`Decimal`|`Single`|`Double`|Qualsiasi tipo integer|  
|`Decimal`|Decimal|Single|Double|Decimal|  
|`Single`|Single|Single|Double|Single|  
|`Double`|Double|Double|Double|Double|  
|Qualsiasi tipo integer|Decimal|Single|Double|Double|  
  
 Il `^` è definito solo per il `Double` tipo di dati. [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]Converte ogni operando in base alle esigenze per `Double` prima dell'operazione e il risultato di tipo di dati è sempre `Double`.  
  
## <a name="integer-arithmetic"></a>Operazioni aritmetiche su valori integer  
 Il tipo di dati del risultato di un'operazione integer dipende da tipi di dati degli operandi. In generale, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] vengono utilizzati i criteri seguenti per determinare il tipo di dati del risultato:  
  
-   Se entrambi gli operandi dell'operatore binario con lo stesso tipo di dati, il risultato è il tipo di dati. Un'eccezione è `Boolean`, che è obbligato a `Short`.  
  
-   Se fa parte di un operando senza segno con segno, il risultato è un tipo con segno con almeno un più ampio un intervallo come degli operandi.  
  
-   In caso contrario, il risultato è in genere il più elevato tra due tipi di dati degli operandi.  
  
 Notare che il tipo di dati del risultato potrebbe non essere lo stesso tipo di dati degli operandi.  
  
> [!NOTE]
>  Il tipo di dati del risultato non è sempre sufficientemente grande da contenere tutti i possibili valori risultanti dall'operazione. Un <xref:System.OverflowException>eccezione può verificarsi se il valore è troppo grande per il tipo di dati del risultato.</xref:System.OverflowException>  
  
### <a name="unary--and--operators"></a>Unario + e -operatori  
 Nella tabella seguente viene illustrato il risultato tipi di dati per i due operatori unari, `+` e `–`.  
  
|||||||||||  
|---|---|---|---|---|---|---|---|---|---|  
||`Boolean`|`SByte`|`Byte`|`Short`|`UShort`|`Integer`|`UInteger`|`Long`|`ULong`|  
|Unario`+`|Short|SByte|Byte|Short|UShort|Integer|UInteger|Long|ULong|  
|Unario`–`|Short|SByte|Short|Short|Integer|Integer|Long|Long|Decimal|  
  
### <a name="-and--operators"></a><\<e >> operatori  
 Nella tabella seguente viene illustrato il risultato tipi di dati per i due operatori di spostamento di bit, `<<` e `>>`. [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]ogni operatore di spostamento di bit viene considerato come un operatore unario sul relativo operando di sinistra (lo schema di bit da spostare).  
  
|||||||||||  
|---|---|---|---|---|---|---|---|---|---|  
||`Boolean`|`SByte`|`Byte`|`Short`|`UShort`|`Integer`|`UInteger`|`Long`|`ULong`|  
|`<<`, `>>`|Short|SByte|Byte|Short|UShort|Integer|UInteger|Long|ULong|  
  
 Se l'operando sinistro è `Decimal`, `Single`, `Double`, o `String`, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] tenta di convertirlo in `Long` prima dell'operazione e il risultato è di tipo di dati `Long`. L'operando di destra (il numero di posizioni di bit da spostare) deve essere `Integer` o un tipo convertibile in `Integer`.  
  
### <a name="binary----and-mod-operators"></a>Binario +, -, * e gli operatori Mod  
 Nella tabella seguente viene illustrato il risultato tipi di dati per il file binario `+` e `–` operatori e `*` e `Mod` operatori. Si noti che questa tabella è simmetrica. per una determinata combinazione di tipi di dati di operando, il tipo di dati del risultato è lo stesso indipendentemente dall'ordine degli operandi.  
  
|||||||||||  
|---|---|---|---|---|---|---|---|---|---|  
||`Boolean`|`SByte`|`Byte`|`Short`|`UShort`|`Integer`|`UInteger`|`Long`|`ULong`|  
|`Boolean`|Short|SByte|Short|Short|Integer|Integer|Long|Long|Decimal|  
|`SByte`|SByte|SByte|Short|Short|Integer|Integer|Long|Long|Decimal|  
|`Byte`|Short|Short|Byte|Short|UShort|Integer|UInteger|Long|ULong|  
|`Short`|Short|Short|Short|Short|Integer|Integer|Long|Long|Decimal|  
|`UShort`|Integer|Integer|UShort|Integer|UShort|Integer|UInteger|Long|ULong|  
|`Integer`|Integer|Integer|Integer|Integer|Integer|Integer|Long|Long|Decimal|  
|`UInteger`|Long|Long|UInteger|Long|UInteger|Long|UInteger|Long|ULong|  
|`Long`|Long|Long|Long|Long|Long|Long|Long|Long|Decimal|  
|`ULong`|Decimal|Decimal|ULong|Decimal|ULong|Decimal|ULong|Decimal|ULong|  
  
### <a name="-operator"></a>Operatore \  
 Nella tabella seguente viene illustrato il risultato tipi di dati per il `\` operatore. Si noti che questa tabella è simmetrica. per una determinata combinazione di tipi di dati di operando, il tipo di dati del risultato è lo stesso indipendentemente dall'ordine degli operandi.  
  
|||||||||||  
|---|---|---|---|---|---|---|---|---|---|  
||`Boolean`|`SByte`|`Byte`|`Short`|`UShort`|`Integer`|`UInteger`|`Long`|`ULong`|  
|`Boolean`|Short|SByte|Short|Short|Integer|Integer|Long|Long|Long|  
|`SByte`|SByte|SByte|Short|Short|Integer|Integer|Long|Long|Long|  
|`Byte`|Short|Short|Byte|Short|UShort|Integer|UInteger|Long|ULong|  
|`Short`|Short|Short|Short|Short|Integer|Integer|Long|Long|Long|  
|`UShort`|Integer|Integer|UShort|Integer|UShort|Integer|UInteger|Long|ULong|  
|`Integer`|Integer|Integer|Integer|Integer|Integer|Integer|Long|Long|Long|  
|`UInteger`|Long|Long|UInteger|Long|UInteger|Long|UInteger|Long|ULong|  
|`Long`|Long|Long|Long|Long|Long|Long|Long|Long|Long|  
|`ULong`|Long|Long|ULong|Long|ULong|Long|ULong|Long|ULong|  
  
 Se degli operandi di `\` operatore [decimale](../../../visual-basic/language-reference/data-types/decimal-data-type.md), [singolo](../../../visual-basic/language-reference/data-types/single-data-type.md), o [Double](../../../visual-basic/language-reference/data-types/double-data-type.md), [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] tenta di convertirlo in [lungo](../../../visual-basic/language-reference/data-types/long-data-type.md) prima dell'operazione e il risultato è di tipo di dati `Long`.  
  
## <a name="relational-and-bitwise-comparisons"></a>Confronti relazionali e bit per bit  
 Il tipo di dati del risultato di un'operazione relazionale (`=`, `<>`, `<`, `>`, `<=`, `>=`) è sempre `Boolean` [tipo di dati Boolean](../../../visual-basic/language-reference/data-types/boolean-data-type.md). Lo stesso vale per le operazioni logiche (`And`, `AndAlso`, `Not`, `Or`, `OrElse`, `Xor`) su `Boolean` operandi.  
  
 Il tipo di dati del risultato di un'operazione logica OR bit per bit dipende da tipi di dati degli operandi. Si noti che `AndAlso` e `OrElse` sono definiti solo per `Boolean`, e [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] converte ogni operando in base alle esigenze per `Boolean` prima di eseguire l'operazione.  
  
### <a name="-----and--operators"></a>=, <>, \<, >, \<=, and >= Operators  
 Se entrambi gli operandi sono `Boolean`, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] considera `True` essere minore di `False`. Se un tipo numerico viene confrontato con un `String`, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] tenta di convertire il `String` per `Double` prima dell'operazione. Oggetto `Char` o `Date` operando può essere confrontato solo con un altro operando dello stesso tipo di dati. Il tipo di dati del risultato è sempre `Boolean`.  
  
### <a name="bitwise-not-operator"></a>Bit per bit Not (operatore)  
 Nella tabella seguente viene illustrato il risultato tipi di dati per il bit per bit `Not` operatore.  
  
|||||||||||  
|---|---|---|---|---|---|---|---|---|---|  
||`Boolean`|`SByte`|`Byte`|`Short`|`UShort`|`Integer`|`UInteger`|`Long`|`ULong`|  
|`Not`|Booleano|SByte|Byte|Short|UShort|Integer|UInteger|Long|ULong|  
  
 Se l'operando è `Decimal`, `Single`, `Double`, o `String`, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] tenta di convertirlo in `Long` prima dell'operazione e il risultato è di tipo di dati `Long`.  
  
### <a name="bitwise-and-or-and-xor-operators"></a>Bit per bit e, o e gli operatori Xor  
 Nella tabella seguente viene illustrato il risultato tipi di dati per il bit per bit `And`, `Or`, e `Xor` operatori. Si noti che questa tabella è simmetrica. per una determinata combinazione di tipi di dati di operando, il tipo di dati del risultato è lo stesso indipendentemente dall'ordine degli operandi.  
  
|||||||||||  
|---|---|---|---|---|---|---|---|---|---|  
||`Boolean`|`SByte`|`Byte`|`Short`|`UShort`|`Integer`|`UInteger`|`Long`|`ULong`|  
|`Boolean`|Booleano|SByte|Short|Short|Integer|Integer|Long|Long|Long|  
|`SByte`|SByte|SByte|Short|Short|Integer|Integer|Long|Long|Long|  
|`Byte`|Short|Short|Byte|Short|UShort|Integer|UInteger|Long|ULong|  
|`Short`|Short|Short|Short|Short|Integer|Integer|Long|Long|Long|  
|`UShort`|Integer|Integer|UShort|Integer|UShort|Integer|UInteger|Long|ULong|  
|`Integer`|Integer|Integer|Integer|Integer|Integer|Integer|Long|Long|Long|  
|`UInteger`|Long|Long|UInteger|Long|UInteger|Long|UInteger|Long|ULong|  
|`Long`|Long|Long|Long|Long|Long|Long|Long|Long|Long|  
|`ULong`|Long|Long|ULong|Long|ULong|Long|ULong|Long|ULong|  
  
 Se un operando è `Decimal`, `Single`, `Double`, o `String`, [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] tenta di convertirlo in `Long` prima dell'operazione e i dati del risultato è lo stesso come se l'operando è già `Long`.  
  
## <a name="miscellaneous-operators"></a>Operatori vari  
 Il `&` è definito solo per la concatenazione di `String` operandi. [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]Converte ogni operando in base alle esigenze per `String` prima dell'operazione e il risultato di tipo di dati è sempre `String`. Per quanto riguarda la `&` operatore, tutte le conversioni in `String` sono considerate di ampliamento, anche se `Option Strict` è `On`.  
  
 Il `Is` e `IsNot` operatori richiedono entrambi gli operandi di un tipo di riferimento. The `TypeOf`... `Is` espressione richiede il primo operando di un tipo di riferimento e il secondo operando per corrispondere al nome di un tipo di dati. In tutti questi casi, i dati del risultato è `Boolean`.  
  
 Il `Like` è definito solo per i criteri di ricerca di `String` operandi. [!INCLUDE[vbprvb](../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]tenta di convertire ogni operando in base alle esigenze per `String` prima dell'operazione. Il tipo di dati del risultato è sempre `Boolean`.  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di dati](../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Operatori ed espressioni](../../../visual-basic/programming-guide/language-features/operators-and-expressions/index.md)   
 [Operatori aritmetici in Visual Basic](../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)   
 [Operatori di confronto in Visual Basic](../../../visual-basic/programming-guide/language-features/operators-and-expressions/comparison-operators.md)   
 [Operatori](../../../visual-basic/language-reference/operators/index.md)   
 [Precedenza tra operatori in Visual Basic](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [Elencata degli operatori per funzionalità](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [Aritmetici (operatori)](../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [Operatori di confronto](../../../visual-basic/language-reference/operators/comparison-operators.md)   
 [Istruzione Option Strict](../../../visual-basic/language-reference/statements/option-strict-statement.md)
