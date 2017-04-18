---
title: 'Procedura: passare argomenti a una routine (Visual Basic) | Documenti di Microsoft'
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
- arguments [Visual Basic], passing to procedures
- procedures, arguments
- procedures, parameters
- procedure arguments
- Visual Basic code, procedures
- procedure parameters
- procedures, calling
- argument passing, procedures
ms.assetid: 08723588-3890-4ddc-8249-79e049e0f241
caps.latest.revision: 14
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
ms.openlocfilehash: ddccd476b2347368d0435f637edf3882db306f45
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-pass-arguments-to-a-procedure-visual-basic"></a>Procedura: passare argomenti a una routine (Visual Basic)
Quando si chiama una routine, seguendo il nome della routine con un elenco di argomenti racchiuso tra parentesi. Viene fornito un argomento corrispondente a ogni parametro obbligatorio definisce la procedura e, facoltativamente, è possibile specificare argomenti per il `Optional` parametri. Se non si fornisce un `Optional` parametro nella chiamata, è necessario includere una virgola per contrassegnarne la posizione nell'elenco di argomenti, se viene fornito alcun argomento successivo.  
  
 Se si intende passare un argomento di un tipo di dati diverso da quello del parametro corrispondente, ad esempio `Byte` a `String`, è possibile impostare l'opzione di verifica del tipo ([istruzione Option Strict](../../../../visual-basic/language-reference/statements/option-strict-statement.md)) a `Off`. Se `Option Strict` è `On`, è necessario utilizzare parole chiave di conversione esplicita o le conversioni di ampliamento. Per ulteriori informazioni, vedere [conversioni di ampliamento e restrizione](../../../../visual-basic/programming-guide/language-features/data-types/widening-and-narrowing-conversions.md) e [funzioni di conversione del tipo](../../../../visual-basic/language-reference/functions/type-conversion-functions.md).  
  
 Per ulteriori informazioni, vedere [procedura parametri e argomenti](./procedure-parameters-and-arguments.md).  
  
### <a name="to-pass-one-or-more-arguments-to-a-procedure"></a>Per passare uno o più argomenti a una routine  
  
1.  Nell'istruzione di chiamata, aggiungere il nome tra parentesi.  
  
2.  All'interno delle parentesi, inserire un elenco di argomenti. Includere un argomento per ogni parametro obbligatorio definito dalla routine e gli argomenti, separarli con virgole.  
  
3.  Assicurarsi che ogni argomento è un'espressione valida che restituisce un tipo di dati convertibile nel tipo di procedura definisce per il parametro corrispondente.  
  
4.  Se un parametro viene definito come [facoltativo](../../../../visual-basic/language-reference/modifiers/optional.md), è possibile includerlo nell'elenco di argomenti oppure ometterlo. Se viene omesso, la routine utilizza il valore predefinito definito per tale parametro.  
  
5.  Se si omette un argomento per un `Optional` parametro ed è presente un altro parametro dopo di esso nell'elenco dei parametri, è possibile contrassegnare la posizione dell'argomento viene omesso da un'altra virgola nell'elenco di argomenti.  
  
     Nell'esempio seguente viene chiamato il [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] <xref:Microsoft.VisualBasic.Interaction.MsgBox%2A>funzione.</xref:Microsoft.VisualBasic.Interaction.MsgBox%2A>  
  
     [!code-vb[VbVbcnProcedures&#34;](./codesnippet/VisualBasic/how-to-pass-arguments-to-a-procedure_1.vb)]  
  
     Nell'esempio precedente fornisce il primo argomento obbligatorio, ovvero la stringa di messaggio da visualizzare. Viene omesso un argomento per il secondo parametro facoltativo che specifica i pulsanti da visualizzare nella finestra di messaggio. Poiché la chiamata non fornisce alcun valore, `MsgBox` utilizza il valore predefinito, `MsgBoxStyle.OKOnly`, che consente di visualizzare solo un **OK** pulsante.  
  
     La seconda virgola nell'elenco degli argomenti contrassegna la posizione del secondo argomento omesso e l'ultima stringa viene passata al terzo parametro facoltativo di `MsgBox`, ovvero il testo da visualizzare nella barra del titolo.  
  
## <a name="see-also"></a>Vedere anche  
 [Sub (routine)](./sub-procedures.md)   
 [Routine di funzione](./function-procedures.md)   
 [Proprietà (routine)](./property-procedures.md)   
 [Routine di operatore](./operator-procedures.md)   
 [Procedura: definire un parametro per una routine](./how-to-define-a-parameter-for-a-procedure.md)   
 [Passaggio di argomenti per valore e per riferimento](./passing-arguments-by-value-and-by-reference.md)   
 [Routine ricorsive](./recursive-procedures.md)   
 [Overload di routine](./procedure-overloading.md)   
 [Oggetti e classi](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)   
 [Programmazione orientata ad oggetti](http://msdn.microsoft.com/library/1cf6e655-3f30-45f1-9a5d-4a88ca24a1c2)
