---
title: Istruzione Mid | Documenti di Microsoft
ms.date: 2015-07-20
ms.prod: .net
ms.reviewer: 
ms.suite: 
ms.technology:
- devlang-visual-basic
ms.topic: article
f1_keywords:
- vb.MidB
- vb.Mid
dev_langs:
- VB
helpviewer_keywords:
- substrings, Mid statement
- strings [Visual Basic], substrings
- Mid statement
- strings [Visual Basic], replacing
ms.assetid: 2b82d7a8-9646-4cb0-bec5-80abc98297bf
caps.latest.revision: 20
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
translationtype: Machine Translation
ms.sourcegitcommit: a06bd2a17f1d6c7308fa6337c866c1ca2e7281c0
ms.openlocfilehash: e385d6838daa16d45903c6b270fc47ad88797845
ms.lasthandoff: 03/13/2017

---
# <a name="mid-statement"></a>Istruzione Mid
Sostituisce un numero specificato di caratteri in un `String` variabili con i caratteri da un'altra stringa.  
  
## <a name="syntax"></a>Sintassi  
  
```  
Mid( _  
   ByRef Target As String, _  
   ByVal Start As Integer, _  
   Optional ByVal Length As Integer _  
) = StringExpression  
```  
  
## <a name="parts"></a>Parti  
 `Target`  
 Obbligatorio. Nome di `String` variabile da modificare.  
  
 `Start`  
 Obbligatorio. `Integer`espressione. Posizione del carattere in `Target` dove inizia la sostituzione di testo. `Start`utilizza un indice in base uno.  
  
 `Length`  
 Facoltativo. `Integer`espressione. Numero di caratteri da sostituire. Se omesso, tutti i `String` viene utilizzato.  
  
 `StringExpression`  
 Obbligatorio. `String`espressione che sostituisce una parte di `Target`.  
  
## <a name="exceptions"></a>Eccezioni  
  
|Tipo di eccezione|Condizione|  
|--------------------|---------------|  
|<xref:System.ArgumentException></xref:System.ArgumentException>|`Start`<= 0="" or=""></=>`Length`< 0.></ 0.>|  
  
## <a name="remarks"></a>Note  
 Il numero di caratteri sostituiti è sempre minore o uguale al numero di caratteri in `Target`.  
  
 Visual Basic è un <xref:Microsoft.VisualBasic.Strings.Mid%2A>(funzione) e un `Mid` istruzione.</xref:Microsoft.VisualBasic.Strings.Mid%2A> Questi elementi entrambi operano su un numero specificato di caratteri in una stringa, ma il `Mid` funzione restituisce i caratteri, mentre il `Mid` istruzione sostituisce i caratteri. Per ulteriori informazioni, vedere <xref:Microsoft.VisualBasic.Strings.Mid%2A>.</xref:Microsoft.VisualBasic.Strings.Mid%2A>  
  
> [!NOTE]
>  Il `MidB` istruzione delle versioni precedenti di Visual Basic sostituisce una sottostringa in byte, anziché in caratteri. Viene utilizzato principalmente per la conversione di stringhe nelle applicazioni di double byte character set (DBCS). Tutte le stringhe di Visual Basic sono in formato Unicode, e `MidB` non è più supportata.  
  
## <a name="example"></a>Esempio  
 Questo esempio viene utilizzato il `Mid` istruzione per sostituire un numero specificato di caratteri in una variabile di stringa con caratteri da un'altra stringa.  
  
 [!code-vb[VbVbalrStrings n.&5;](../../../visual-basic/language-reference/functions/codesnippet/VisualBasic/mid-statement_1.vb)]  
  
## <a name="requirements"></a>Requisiti  
 **Namespace:** [Microsoft. VisualBasic](../../../visual-basic/language-reference/runtime-library-members.md)  
  
 **Modulo:**`Strings`  
  
 **Assembly:**[!INCLUDE[vbprvbruntime](../../../visual-basic/language-reference/objects/includes/vbprvbruntime_md.md)]  
  
## <a name="see-also"></a>Vedere anche  
 <xref:Microsoft.VisualBasic.Strings.Mid%2A></xref:Microsoft.VisualBasic.Strings.Mid%2A>   
 [Stringhe](../../../visual-basic/programming-guide/language-features/strings/index.md)   
 [Introduzione alle stringhe in Visual Basic](../../../visual-basic/programming-guide/language-features/strings/introduction-to-strings.md)
