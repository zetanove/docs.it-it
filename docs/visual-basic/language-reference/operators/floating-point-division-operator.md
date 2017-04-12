---
title: / Operatore (Visual Basic) | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb./
dev_langs:
- VB
helpviewer_keywords:
- division operator, floating point
- floating-point numbers, division operator
- slash (/) operator
- zero, division by zero
- operators [Visual Basic], arithmetic
- arithmetic operators, division
- division, by zero
- operators [Visual Basic], division
- division operator, syntax
- / operator [Visual Basic]
- math operators
ms.assetid: 335e97f2-c434-439e-9064-76973a051101
caps.latest.revision: 18
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
ms.openlocfilehash: 71b4f64f6deeb334412c87131ccd9480620f284f
ms.lasthandoff: 03/13/2017

---
# <a name="-operator-visual-basic"></a>Operatore / (Visual Basic)
Divide due numeri e restituisce un risultato a virgola mobile.  
  
## <a name="syntax"></a>Sintassi  
  
```  
  
expression1 / expression2  
```  
  
## <a name="parts"></a>Parti  
 `expression1`  
 Obbligatorio. Qualsiasi espressione numerica.  
  
 `expression2`  
 Obbligatorio. Qualsiasi espressione numerica.  
  
## <a name="supported-types"></a>Tipi supportati  
 Tutti i tipi numerici, inclusi i tipi a virgola mobile e senza segno e `Decimal`.  
  
## <a name="result"></a>Risultato  
 Il risultato è il quoziente completo di `expression1` diviso `expression2`, incluso l'eventuale resto.  
  
 Il [\ (operatore) (Visual Basic)](../../../visual-basic/language-reference/operators/integer-division-operator.md) restituisce il quoziente intero, ossia senza resto.  
  
## <a name="remarks"></a>Note  
 Il tipo di dati del risultato dipende dai tipi degli operandi. Nella tabella seguente viene illustrato come il tipo di dati del risultato è determinato.  
  
|Tipi di dati degli operandi|Tipi di dati|  
|------------------------|----------------------|  
|Entrambe le espressioni sono tipi di dati integrali ([SByte](../../../visual-basic/language-reference/data-types/sbyte-data-type.md), [Byte](../../../visual-basic/language-reference/data-types/byte-data-type.md), [breve](../../../visual-basic/language-reference/data-types/short-data-type.md), [UShort](../../../visual-basic/language-reference/data-types/ushort-data-type.md), [intero](../../../visual-basic/language-reference/data-types/integer-data-type.md), [UInteger](../../../visual-basic/language-reference/data-types/uinteger-data-type.md), [lungo](../../../visual-basic/language-reference/data-types/long-data-type.md), [ULong](../../../visual-basic/language-reference/data-types/ulong-data-type.md))|`Double`|  
|Un'espressione è un [singolo](../../../visual-basic/language-reference/data-types/single-data-type.md) tipo di dati e l'altro non è un [Double](../../../visual-basic/language-reference/data-types/double-data-type.md)|`Single`|  
|Un'espressione è un [decimale](../../../visual-basic/language-reference/data-types/decimal-data-type.md) tipo di dati e l'altro non è un [singolo](../../../visual-basic/language-reference/data-types/single-data-type.md) o [Double](../../../visual-basic/language-reference/data-types/double-data-type.md)|`Decimal`|  
|Delle espressioni è un [Double](../../../visual-basic/language-reference/data-types/double-data-type.md) tipo di dati|`Double`|  
  
 Prima di eseguita la divisione, le espressioni numeriche integrali vengono estesi a `Double`. Se si assegna il risultato a un tipo di dati integrali, Visual Basic tenta di convertire il risultato da `Double` a tale tipo. Ciò può generare un'eccezione se il risultato non rientra in tale tipo. In particolare, vedere "Ha tentato di divisione per Zero" in questa pagina della Guida in linea.  
  
 Se `expression1` o `expression2` restituisce [nulla](../../../visual-basic/language-reference/nothing.md), viene considerato pari a zero.  
  
## <a name="attempted-division-by-zero"></a>Tentativo di divisione per Zero  
 Se `expression2` restituisce zero, il `/` operatore si comporta in modo diverso per i tipi di dati diversi operando. La tabella seguente illustra i possibili comportamenti.  
  
|Tipi di dati degli operandi|Comportamento se `expression2` è zero|  
|------------------------|---------------------------------------|  
|A virgola mobile (`Single` o `Double`)|Restituisce l'infinito (<xref:System.Double.PositiveInfinity> o <xref:System.Double.NegativeInfinity>), o <xref:System.Double.NaN>(non un numero) se `expression1` è zero</xref:System.Double.NaN> </xref:System.Double.NegativeInfinity> </xref:System.Double.PositiveInfinity>|  
|`Decimal`|Genera un'eccezione<xref:System.DivideByZeroException></xref:System.DivideByZeroException>|  
|Integrale (con o senza segno)|Tentativo di conversione al tipo integrale genera <xref:System.OverflowException>perché non possono accettare tipi integrali <xref:System.Double.PositiveInfinity>, <xref:System.Double.NegativeInfinity>, o <xref:System.Double.NaN></xref:System.Double.NaN> </xref:System.Double.NegativeInfinity> </xref:System.Double.PositiveInfinity> </xref:System.OverflowException>|  
  
> [!NOTE]
>  Il `/` operatore può essere *overload*, il che significa che una classe o struttura possibile ridefinire il comportamento quando un operando specifica il tipo di classe o struttura. Se il codice utilizza l'operatore su una classe o struttura, assicurarsi di comprendere il comportamento ridefinito. Per ulteriori informazioni, vedere [routine di operatore](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).  
  
## <a name="example"></a>Esempio  
 Questo esempio viene utilizzato il `/` operatore per eseguire una divisione a virgola mobile. Il risultato è il quoziente di due operandi.  
  
 [!code-vb[VbVbalrOperators&#16;](../../../visual-basic/language-reference/operators/codesnippet/VisualBasic/floating-point-division-operator_1.vb)]  
  
 Le espressioni nell'esempio precedente restituiscono valori di 2,5 e 3,333333. Si noti che il risultato è sempre a virgola mobile (`Double`), anche se entrambi gli operandi sono costanti integer.  
  
## <a name="see-also"></a>Vedere anche  
 [Operatore / = (Visual Basic)](../../../visual-basic/language-reference/operators/floating-point-division-assignment-operator.md)   
 [\ Operatore (Visual Basic)](../../../visual-basic/language-reference/operators/integer-division-operator.md)   
 [Tipi di dati dei risultati degli operatori](../../../visual-basic/language-reference/operators/data-types-of-operator-results.md)   
 [Aritmetici (operatori)](../../../visual-basic/language-reference/operators/arithmetic-operators.md)   
 [Precedenza tra operatori in Visual Basic](../../../visual-basic/language-reference/operators/operator-precedence.md)   
 [Elencata degli operatori per funzionalità](../../../visual-basic/language-reference/operators/operators-listed-by-functionality.md)   
 [Operatori aritmetici in Visual Basic](../../../visual-basic/programming-guide/language-features/operators-and-expressions/arithmetic-operators.md)

