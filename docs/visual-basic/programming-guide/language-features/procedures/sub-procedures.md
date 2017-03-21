---
title: Sub (routine) (Visual Basic) | Documenti di Microsoft
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
- Sub procedures, about Sub procedures
- statement blocks
- Sub procedures, calling
- procedures, calling
- Sub procedures, syntax
- Sub procedures
- procedures, Sub
- syntax, Sub procedures
ms.assetid: 6a0a4958-ed0a-4d3d-8d31-0772c82bda58
caps.latest.revision: 21
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
ms.openlocfilehash: d224fa3338ca707070ee431380578a8fdde47e07
ms.lasthandoff: 03/13/2017

---
# <a name="sub-procedures-visual-basic"></a>Routine Sub (Visual Basic)
Oggetto `Sub` routine è una serie di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] racchiuso tra istruzioni il `Sub` e `End Sub` istruzioni. Il `Sub` routine esegue un'attività e quindi restituisce il controllo al codice chiamante, ma non restituisce un valore al codice chiamante.  
  
 Ogni volta che viene chiamata la routine, le relative istruzioni vengono eseguite a partire dalla prima istruzione eseguibile dopo il `Sub` istruzione e terminando con il primo `End Sub`, `Exit Sub`, o `Return` istruzione rilevata.  
  
 È possibile definire un `Sub` procedura in moduli, classi e strutture. Per impostazione predefinita è `Public`, ovvero è possibile chiamarla da qualsiasi punto dell'applicazione che ha accesso al modulo, classe o struttura in cui è stata definita. Il termine *metodo*, viene descritto un `Sub` o `Function` procedure accessibili dall'esterno la definizione di modulo, classe o struttura. Per ulteriori informazioni, vedere [procedure](./index.md).  
  
 Oggetto `Sub` procedure può accettare argomenti, ad esempio costanti, variabili o espressioni, che vengono passate al metodo dal codice chiamante.  
  
## <a name="declaration-syntax"></a>Sintassi di dichiarazione  
 La sintassi per dichiarare un `Sub` è la seguente procedura:  
  
 `[`*modifiers* `] Sub`*subname* `[(` *parameterlist*  `)]`  
  
 `' Statements of the Sub procedure.`  
  
 `End Sub`  
  
 Il `modifiers` possibile specificare il livello di accesso e informazioni su overload, override, condivisione e shadowing. Per ulteriori informazioni, vedere [Sub (istruzione)](../../../../visual-basic/language-reference/statements/sub-statement.md).  
  
## <a name="parameter-declaration"></a>Dichiarazione di parametro  
 Dichiarare ogni parametro di routine in modo analogo a come si dichiara una variabile, che specifica il tipo di dati e nome di parametro. È inoltre possibile specificare il meccanismo di passaggio e se il parametro è facoltativo o una matrice di parametri.  
  
 La sintassi per ogni parametro nell'elenco dei parametri è come segue:  
  
 `[Optional] [ByVal | ByRef] [ParamArray]`  *ParameterName*`As`*tipo di dati    *  
  
 Se il parametro è facoltativo, è necessario fornire anche un valore predefinito come parte della relativa dichiarazione. La sintassi per specificare un valore predefinito è come segue:  
  
 `Optional [ByVal | ByRef]`  *ParameterName*`As`*datatype*`=`*defaultvalue        *  
  
### <a name="parameters-as-local-variables"></a>Parametri come variabili locali  
 Quando il controllo passa alla routine, ogni parametro viene trattato come una variabile locale. Ciò significa che la sua durata è uguale a quello della procedura e il relativo ambito è l'intera procedura.  
  
## <a name="calling-syntax"></a>Sintassi di chiamata  
 Richiamare un `Sub` procedura in modo esplicito tramite un'istruzione di chiamata autonoma. È possibile effettuare la chiamata utilizzando il relativo nome in un'espressione. È necessario fornire valori per tutti gli argomenti che non sono facoltativi e racchiudere l'elenco di argomenti racchiuso tra parentesi. Se viene fornito alcun argomento, è possibile omettere le parentesi. L'utilizzo di `Call` (parola chiave) è facoltativo ma non consigliato.  
  
 La sintassi per una chiamata a un `Sub` è la seguente procedura:  
  
 `[Call]`  *subname* `[(` *argumentlist*`)]`  
  
 È possibile chiamare un `Sub` metodo dall'esterno della classe che lo definisce. In primo luogo, è necessario utilizzare il `New` (parola chiave) per creare un'istanza della classe o chiamare un metodo che restituisce un'istanza della classe. Per ulteriori informazioni, vedere [nuovo operatore](../../../../visual-basic/language-reference/operators/new-operator.md). Quindi, è possibile utilizzare la sintassi seguente per chiamare il `Sub` metodo sull'oggetto dell'istanza:  
  
 *Object*.* MethodName*`[(`*argumentlist*`)]`  
  
### <a name="illustration-of-declaration-and-call"></a>Illustrazione di dichiarazione e chiamata  
 Nell'esempio `Sub` procedure viene illustrato l'operatore computer quale attività l'applicazione sta per eseguire e visualizza un timestamp. Anziché ripetere questo codice all'inizio di ogni attività, l'applicazione chiama semplicemente `tellOperator` da diverse posizioni. Ogni chiamata passa una stringa di `task` argomento che identifica l'attività in corso l'avvio.  
  
 [!code-vb[VbVbcnProcedures n.&2;](./codesnippet/VisualBasic/sub-procedures_1.vb)]  
  
 Nell'esempio seguente viene illustrata una tipica chiamata a `tellOperator`.  
  
 [!code-vb[VbVbcnProcedures n.&3;](./codesnippet/VisualBasic/sub-procedures_2.vb)]  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure](./index.md)   
 [Routine di funzione](./function-procedures.md)   
 [Proprietà (routine)](./property-procedures.md)   
 [Routine di operatore](./operator-procedures.md)   
 [Gli argomenti e parametri di routine](./procedure-parameters-and-arguments.md)   
 [Sub (istruzione)](../../../../visual-basic/language-reference/statements/sub-statement.md)   
 [Procedura: chiamare una routine che non restituisce un valore](./how-to-call-a-procedure-that-does-not-return-a-value.md)   
 [Procedura: chiamare un gestore eventi in Visual Basic](./how-to-call-an-event-handler.md)
