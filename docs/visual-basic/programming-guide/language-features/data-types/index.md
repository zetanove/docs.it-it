---
title: Tipi di dati in Visual Basic | Microsoft Docs
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
- data types [Visual Basic], declaring
- typing
- data types [Visual Basic]
- Visual Basic code, data types
- data types [Visual Basic], improving speed with
ms.assetid: 5e1b9aaf-c7ca-4b29-9b22-0e82ed8e85e2
caps.latest.revision: 28
author: dotnet-bot
ms.author: dotnetcontent
translation.priority.ht:
- de-de
- es-es
- fr-fr
- it-it
- ja-jp
- ko-kr
- ru-ru
- zh-cn
- zh-tw
translation.priority.mt:
- cs-cz
- pl-pl
- pt-br
- tr-tr
translationtype: Human Translation
ms.sourcegitcommit: c86e1bfacbe06d10915bd476a5c6f528fcebe70d
ms.openlocfilehash: 2642145e496469eb8bcb382408fda2147f48b0d5
ms.lasthandoff: 04/30/2017

---
# <a name="data-types-in-visual-basic"></a>Tipi di dati in Visual Basic
Il *tipo di dati* di un elemento di programmazione indica la tipologia di dati che può contenere e la modalità di archiviazione di tali dati. I tipi di dati si applicano a tutti i valori che possono essere archiviati nella memoria del computer o partecipano alla valutazione di un'espressione. Ogni variabile, valore letterale, costante, enumerazione, proprietà, parametro di routine, argomento di routine e valore restituito di routine ha un tipo di dati.  
  
## <a name="declared-data-types"></a>Tipi di dati dichiarati  
 Un elemento di programmazione viene definito con un'istruzione di dichiarazione e il relativo tipo di dati viene specificato con la clausola `As`. La tabella seguente mostra le istruzioni usate per dichiarare i vari elementi.  
  
|Elemento di programmazione|Dichiarazione del tipo di dati|  
|-------------------------|---------------------------|  
|Variabile|In un'[istruzione Dim](../../../../visual-basic/language-reference/statements/dim-statement.md)<br /><br /> `Dim`   `amount As Double`<br /><br /> `Static`   `yourName As String`<br /><br /> `Public`   `billsPaid As Decimal = 0`|  
|Literal|Con un carattere di tipo letterale. Vedere "Caratteri di tipo letterale" in [Caratteri tipo](../../../../visual-basic/programming-guide/language-features/data-types/type-characters.md)<br /><br /> `Dim searchChar As Char = "."`  `C`|  
|Costante|In un'[istruzione Const](../../../../visual-basic/language-reference/statements/const-statement.md)<br /><br /> `Const`   `modulus As Single = 4.17825F`|  
|Enumerazione|In un'[istruzione Enum](../../../../visual-basic/language-reference/statements/enum-statement.md)<br /><br /> `Public`   `Enum`   `colors`|  
|Proprietà|In un'[istruzione Property](../../../../visual-basic/language-reference/statements/property-statement.md)<br /><br /> `Property`   `region() As String`|  
|Parametro di routine|In un'[istruzione Sub](../../../../visual-basic/language-reference/statements/sub-statement.md), un'[istruzione Function](../../../../visual-basic/language-reference/statements/function-statement.md) o un'[istruzione Operator](../../../../visual-basic/language-reference/statements/operator-statement.md)<br /><br /> `Sub addSale(ByVal`   `amount`   `As Double)`|  
|Argomento di routine|Nel codice chiamante; ogni argomento è un elemento di programmazione già dichiarato o un'espressione che contiene elementi dichiarati<br /><br /> `subString = Left(`  `inputString`  `,`   `5`  `)`|  
|Valore restituito di routine|In un'[istruzione Function](../../../../visual-basic/language-reference/statements/function-statement.md) o un'[istruzione Operator](../../../../visual-basic/language-reference/statements/operator-statement.md)<br /><br /> `Function convert(ByVal b As Byte)`   `As String`|  
  
 Per un elenco dei tipi di dati di Visual Basic, vedere [Tipi di dati](../../../../visual-basic/language-reference/data-types/data-type-summary.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Caratteri tipo](../../../../visual-basic/programming-guide/language-features/data-types/type-characters.md)   
 [Tipi di dati elementari](../../../../visual-basic/programming-guide/language-features/data-types/elementary-data-types.md)   
 [Tipi di dati compositi](../../../../visual-basic/programming-guide/language-features/data-types/composite-data-types.md)   
 [Tipi generici in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [Tipi valore e tipi di riferimento](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)   
 [Conversioni di tipi in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [Strutture](../../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [Tuple](tuples.md)     
 [Risoluzione dei problemi relativi ai tipi di dati](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [Riepilogo dei tipi di dati](../../../../visual-basic/language-reference/data-types/data-type-summary.md)   
 [Uso efficiente dei tipi di dati](../../../../visual-basic/programming-guide/language-features/data-types/efficient-use-of-data-types.md)
