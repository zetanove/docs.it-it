---
title: Tipi di metodi di manipolazione delle stringhe in Visual Basic | Documenti di Microsoft
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
- strings [Visual Basic], manipulating [Visual Basic]
- string manipulation
ms.assetid: 905055cd-7f50-48fb-9eed-b0995af1dc1f
caps.latest.revision: 12
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
ms.openlocfilehash: 349cfdb3e31225f6aeba90ac29aa1c66e37c7e11
ms.lasthandoff: 03/13/2017

---
# <a name="types-of-string-manipulation-methods-in-visual-basic"></a>Tipi di metodi per la gestione delle stringhe in Visual Basic
Esistono diversi modi per analizzare e modificare le stringhe. Alcuni metodi fanno parte del [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] language altri sono inerenti la `String` classe.  
  
## <a name="visual-basic-language-and-the-net-framework"></a>Linguaggio Visual Basic e .NET Framework  
 [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]metodi vengono utilizzati come funzioni intrinseche del linguaggio. Essi possono essere utilizzati senza qualifica nel codice. Nell'esempio seguente viene illustrato l'utilizzo tipico di un [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] comando di modifica di stringhe:  
  
 [!code-vb[VbVbalrStrings&#44;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/types-of-string-manipulation-methods_1.vb)]  
  
 In questo esempio, il `Mid` funzione esegue un'operazione diretta su `aString` e assegna il valore a `bString`.  
  
 Per un elenco di metodi di manipolazione di stringhe di Visual Basic, vedere [String Manipulation Summary](../../../../visual-basic/language-reference/keywords/string-manipulation-summary.md).  
  
### <a name="shared-methods-and-instance-methods"></a>Metodi condivisi e metodi di istanza  
 È inoltre possibile modificare le stringhe con i metodi della `String` classe. Esistono due tipi di metodi in `String`: *condivisa* metodi e *istanza* metodi.  
  
#### <a name="shared-methods"></a>Metodi condivisi  
 Un metodo condiviso è un metodo che deriva dalla `String` classe stessa e non richiede un'istanza di tale classe per funzionare. Questi metodi possono essere qualificati con il nome della classe (`String`) anziché con un'istanza di `String` (classe). Ad esempio:  
  
 [!code-vb[N. VbVbalrStrings&45;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/types-of-string-manipulation-methods_2.vb)]  
  
 Nell'esempio precedente, il <xref:System.String.Copy%2A?displayProperty=fullName>è un metodo statico, che agisce su un'espressione fornita e assegna il valore risulta a `bString`.</xref:System.String.Copy%2A?displayProperty=fullName>  
  
#### <a name="instance-methods"></a>Metodi di istanza  
 Metodi di istanza, invece, hanno origine da una particolare istanza di `String` e deve essere qualificato con il nome dell'istanza. Ad esempio:  
  
 [!code-vb[VbVbalrStrings n.&46;](../../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/types-of-string-manipulation-methods_3.vb)]  
  
 In questo esempio, il <xref:System.String.Substring%2A?displayProperty=fullName>è un metodo dell'istanza di `String` (vale a dire `aString`).</xref:System.String.Substring%2A?displayProperty=fullName> Esegue un'operazione su `aString` e assegna tale valore per `bString`.  
  
 Per ulteriori informazioni, vedere la documentazione per la <xref:System.String>classe.</xref:System.String>  
  
## <a name="see-also"></a>Vedere anche  
 [Introduzione alle stringhe in Visual Basic](../../../../visual-basic/programming-guide/language-features/strings/introduction-to-strings.md)
