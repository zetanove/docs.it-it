---
title: 'Procedura: definire un parametro per una routine (Visual Basic) | Documenti di Microsoft'
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
- procedure parameters, defining data types for
- procedures, parameters
- procedures, defining
- Visual Basic code, procedures
- procedure parameters, defining
ms.assetid: 7962808d-407e-4e84-984e-43e9857c53c9
caps.latest.revision: 15
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
ms.openlocfilehash: 9fb9ad244499039c1768ff97f071168e0a0842e4
ms.lasthandoff: 03/13/2017

---
# <a name="how-to-define-a-parameter-for-a-procedure-visual-basic"></a>Procedura: definire un parametro per una routine (Visual Basic)
Oggetto *parametro* consente di passare un valore alla routine quando si chiama il codice chiamante. Dichiarare ogni parametro per una procedura simile a quello si dichiara una variabile, specificando il nome e tipo di dati. Specificare inoltre il meccanismo di passaggio e se il parametro è facoltativo.  
  
 Per ulteriori informazioni, vedere [procedura parametri e argomenti](./procedure-parameters-and-arguments.md).  
  
### <a name="to-define-a-procedure-parameter"></a>Per definire un parametro di routine  
  
1.  Nella dichiarazione di routine, aggiungere il nome del parametro all'elenco di parametri della stored procedure, separandolo dalle altri parametri da una virgola.  
  
2.  Decidere il tipo di dati del parametro.  
  
3.  Seguire il nome del parametro con un `As` clausola per specificare il tipo di dati.  
  
4.  Decidere il meccanismo di passaggio desiderato per il parametro. In genere passato un parametro per valore, a meno che non si desidera essere in grado di modificare il valore del codice chiamante alla routine.  
  
5.  Anteporre il nome del parametro [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md) o [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md) per specificare il meccanismo di passaggio. Per ulteriori informazioni, vedere [le differenze tra il passaggio di un argomento per valore e per riferimento](./differences-between-passing-an-argument-by-value-and-by-reference.md).  
  
6.  Se il parametro è facoltativo, anteporre il meccanismo di passaggio [facoltativo](../../../../visual-basic/language-reference/modifiers/optional.md) e seguire il tipo di dati di parametro con un segno di uguale (`=`) e un valore predefinito.  
  
     Nell'esempio seguente viene definita la struttura di un `Sub` routine con tre parametri. I primi due sono necessari e il terzo è facoltativo. Le dichiarazioni dei parametri sono separati nell'elenco di parametri da virgole.  
  
     [!code-vb[VbVbcnProcedures n.&33;](./codesnippet/VisualBasic/how-to-define-a-parameter-for-a-procedure_1.vb)]  
  
     Il primo parametro accetta un `customer` oggetto, e `updateCustomer` può aggiornare direttamente la variabile passata a `c` perché viene passato l'argomento [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md). La procedura non può modificare i valori degli ultimi due argomenti in quanto vengono passati [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md).  
  
     Se il codice chiamante non fornisce un valore per il `level` parametro [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] imposta il valore predefinito pari a 0.  
  
     Se il controllo dei tipi ([istruzione Option Strict](../../../../visual-basic/language-reference/statements/option-strict-statement.md)) è `Off`, `As` clausola è facoltativa quando si definisce un parametro. Tuttavia, se un qualsiasi parametro utilizza un `As` clausola, tutti gli elementi da utilizzare. Se il tipo di opzione di verifica dei `On`, `As` clausola è obbligatoria per ogni definizione di parametro.  
  
     Specifica di tipi di dati per tutti gli elementi di programmazione è noto come *la tipizzazione forte*. Quando si imposta `Option Strict On`, [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] attiva la tipizzazione forte. Questa opzione è fortemente consigliata per i motivi seguenti:  
  
    -   Consente il supporto IntelliSense per le variabili e parametri. Ciò consente di visualizzare le relative proprietà e gli altri membri durante la digitazione del codice.  
  
    -   Consente al compilatore di eseguire il controllo dei tipi. In questo modo può avere esito negativo in fase di esecuzione a causa di errori, ad esempio overflow istruzione catch. Inoltre, intercetta le chiamate ai metodi su oggetti che non li supportano.  
  
    -   Comporta un'esecuzione più rapida del codice. Una ragione è che se non si specifica un tipo di dati per un elemento di programmazione, il [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] compilatore assegna automaticamente il `Object` tipo. Il codice compilato potrebbe essere necessario convertire avanti e indietro tra `Object` e altri tipi di dati, riducendo le prestazioni.  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure](./index.md)   
 [Sub (routine)](./sub-procedures.md)   
 [Routine di funzione](./function-procedures.md)   
 [Procedura: passare argomenti a una routine](./how-to-pass-arguments-to-a-procedure.md)   
 [Passaggio di argomenti per valore e per riferimento](./passing-arguments-by-value-and-by-reference.md)   
 [Routine ricorsive](./recursive-procedures.md)   
 [Overload di routine](./procedure-overloading.md)   
 [Oggetti e classi](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)   
 [Programmazione orientata ad oggetti](http://msdn.microsoft.com/library/1cf6e655-3f30-45f1-9a5d-4a88ca24a1c2)
