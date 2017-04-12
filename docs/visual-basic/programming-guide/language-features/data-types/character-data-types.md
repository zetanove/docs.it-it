---
title: Tipi di dati (Visual Basic) carattere | Documenti di Microsoft
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
- data types [Visual Basic], character
- String data type, character data types
- character data types [Visual Basic]
- Char data type, character data types
- data types [Visual Basic], choosing
ms.assetid: 902479ef-1679-47fc-9911-0c1c5008226c
caps.latest.revision: 23
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
ms.openlocfilehash: 7ce600fe188c94593e4c07e37883ca11f90d9ae5
ms.lasthandoff: 03/13/2017

---
# <a name="character-data-types-visual-basic"></a>Dati di tipo carattere (Visual Basic)
[!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]fornisce *tipi di dati carattere* per la gestione dei caratteri stampabili e visualizzabili. Sebbene entrambi gestiscano i caratteri Unicode, `Char` contiene un singolo carattere mentre `String` contiene un numero indefinito di caratteri.  
  
 Per una tabella che visualizza un confronto side-by-side di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] tipi di dati, vedere [tipi di dati](../../../../visual-basic/language-reference/data-types/data-type-summary.md).  
  
## <a name="char-type"></a>Char (tipo)  
 Il `Char` tipo di dati è un singolo carattere di Unicode a due byte (16 bit). Se una variabile memorizza sempre esattamente un carattere, dichiararla come `Char`. Ad esempio:  
  
 [!code-vb[VbVbalrCharTypes n.&1;](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/character-data-types_1.vb)]  
  
 Ogni valore possibile in un `Char` o `String` variabile è un *punto di codice*, o codice di carattere, nel set di caratteri Unicode. I caratteri Unicode includono set di caratteri ASCII di base diverse altre lettere dell'alfabeto, accenti, simboli di valuta, le frazioni di secondo, i segni diacritici e simboli matematici e tecnici.  
  
> [!NOTE]
>  Set di caratteri Unicode riserva i punti di codice D800 a DFFF (da 55296 a 55551 in formato decimale) per *coppie di surrogati*, che richiedono due valori a 16 bit per rappresentare un singolo punto di codice. Oggetto `Char` variabile non può contenere una coppia di surrogati e un `String` utilizza due posizioni per mantenere tale coppia.  
  
 Per ulteriori informazioni, vedere [tipo di dati Char](../../../../visual-basic/language-reference/data-types/char-data-type.md).  
  
## <a name="string-type"></a>Tipo di stringa  
 Il `String` tipo di dati è una sequenza di zero o più caratteri Unicode a due byte (16 bit). Se una variabile può contenere un numero indefinito di caratteri, dichiararla come `String`. Ad esempio:  
  
 [!code-vb[VbVbalrCharTypes n.&2;](../../../../visual-basic/programming-guide/language-features/data-types/codesnippet/VisualBasic/character-data-types_2.vb)]  
  
 Per ulteriori informazioni, vedere [tipo di dati stringa](../../../../visual-basic/language-reference/data-types/string-data-type.md).  
  
## <a name="see-also"></a>Vedere anche  
 [Tipi di dati elementari](../../../../visual-basic/programming-guide/language-features/data-types/elementary-data-types.md)   
 [Tipi di dati compositi](../../../../visual-basic/programming-guide/language-features/data-types/composite-data-types.md)   
 [Tipi generici in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [Tipi di valore e tipi di riferimento](../../../../visual-basic/programming-guide/language-features/data-types/value-types-and-reference-types.md)   
 [Conversioni di tipi in Visual Basic](../../../../visual-basic/programming-guide/language-features/data-types/type-conversions.md)   
 [Risoluzione dei tipi di dati](../../../../visual-basic/programming-guide/language-features/data-types/troubleshooting-data-types.md)   
 [Caratteri tipo](../../../../visual-basic/programming-guide/language-features/data-types/type-characters.md)
