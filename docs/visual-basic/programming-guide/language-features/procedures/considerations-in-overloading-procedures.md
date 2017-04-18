---
title: Considerazioni sull&quot;overload di routine (Visual Basic) | Documenti di Microsoft
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
- signatures, ParamArray arguments
- ParamArray keyword, parameter arrays
- ParamArray keyword, arguments and signatures
- function overloading, implicit overloads for ParamArray
- ParamArray keyword, signatures
- Visual Basic code, procedures
- arguments [Visual Basic], parameter arrays
- procedures, overloading
- parameters, lists
- function overloading, typeless programming
- typeless programming
- function overloading, restrictions
- arguments [Visual Basic], optional
- optional arguments, overloading
- signatures, procedure
- parameter lists
- parameter arrays, overloading arguments
- Visual Basic code, parameter lists
- procedure overloading, considerations
- Option Explicit statement
- restrictions, overloading procedures
- procedures, parameter lists
ms.assetid: a2001248-10d0-42c5-b0ce-eeedc987319f
caps.latest.revision: 26
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
ms.openlocfilehash: aa20cf367fba157f88afd861a4799540dcdecde1
ms.lasthandoff: 03/13/2017

---
# <a name="considerations-in-overloading-procedures-visual-basic"></a>Considerazioni sull'overload di routine (Visual Basic)
Quando si esegue l'overload di una procedura, è necessario utilizzare un diverso *firma* per ogni versione di overload. In genere significa che ogni versione è necessario specificare un elenco di parametri diversi. Per ulteriori informazioni, vedere "Firma diversa" in [overload di routine](./procedure-overloading.md).  
  
 È possibile eseguire l'overload un `Function` procedura con un `Sub` procedure e viceversa, purché siano firme diverse. Due overload non possono differire solo in quanto uno ha un valore restituito e l'altro non lo consente.  
  
 È possibile eseguire l'overload una proprietà allo stesso modo, si esegue l'overload di una routine e con le stesse restrizioni. Tuttavia, è possibile eseguire l'overload di una procedura con una proprietà o viceversa.  
  
## <a name="alternatives-to-overloaded-versions"></a>Alternative alle versioni di overload  
 È talvolta necessario alternative alle versioni di overload, in particolare quando la presenza di argomenti è facoltativa o il relativo numero è variabile.  
  
 Tenere presente che gli argomenti facoltativi non sono necessariamente supportati da tutti i linguaggi e le matrici di parametri sono limitate a [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)]. Se si sta scrivendo una routine che possa essere chiamato dal codice scritto in uno qualsiasi dei numerosi linguaggi, overload versioni offerta la massima flessibilità.  
  
### <a name="overloads-and-optional-arguments"></a>Argomenti facoltativi e overload  
 Quando il codice chiamante può facoltativamente specificare o omettere uno o più argomenti, è possibile definire più versioni di overload o utilizzare parametri facoltativi.  
  
#### <a name="when-to-use-overloaded-versions"></a>Quando utilizzare le versioni di overload  
 È possibile definire una serie di versioni di overload nei casi seguenti:  
  
-   La logica nel codice della routine è notevolmente diversa a seconda se il codice chiamante fornisce un argomento facoltativo o non.  
  
-   Il codice della routine non può verificare in modo affidabile se il codice chiamante ha fornito un argomento facoltativo. Ciò avviene, ad esempio, se non è possibile prevedere alcun valore predefinito che il codice chiamante potrebbe non essere previsto di fornire.  
  
#### <a name="when-to-use-optional-parameters"></a>Quando utilizzare parametri facoltativi  
 È possibile scegliere uno o più parametri facoltativi nei casi seguenti:  
  
-   L'azione richiesta solo quando il codice chiamante non fornisce un argomento facoltativo consiste nell'impostare il parametro su un valore predefinito. In tal caso, il codice della routine può essere meno complesso se si definisce una singola versione con uno o più `Optional` parametri.  
  
 Per ulteriori informazioni, vedere [parametri facoltativi](./optional-parameters.md).  
  
### <a name="overloads-and-paramarrays"></a>Overload e ParamArray  
 Quando il codice chiamante può passare un numero variabile di argomenti, è possibile definire più versioni di overload o utilizzare una matrice di parametri.  
  
#### <a name="when-to-use-overloaded-versions"></a>Quando utilizzare le versioni di overload  
 È possibile definire una serie di versioni di overload nei casi seguenti:  
  
-   Sai che il codice chiamante passa sempre un numero ridotto di valori alla matrice di parametri.  
  
-   La logica nel codice della routine è notevolmente diversa a seconda del numero di valori passa al codice chiamante.  
  
-   Il codice chiamante può passare valori di tipi di dati diversi.  
  
#### <a name="when-to-use-a-parameter-array"></a>Quando utilizzare una matrice di parametri  
 Consigliabile un `ParamArray` parametro nei casi seguenti:  
  
-   Non si è in grado di stimare il numero di valori il codice chiamante può passare la matrice di parametri e potrebbe essere un numero elevato.  
  
-   La logica della stored procedure si presta per scorrere tutti i valori passati al codice chiamante, essenzialmente le stesse operazioni per ogni valore di esecuzione.  
  
 Per ulteriori informazioni, vedere [matrici di parametro](./parameter-arrays.md).  
  
## <a name="implicit-overloads-for-optional-parameters"></a>Overload impliciti per i parametri facoltativi  
 Una routine con un [facoltativo](../../../../visual-basic/language-reference/modifiers/optional.md) parametro equivale a due routine di overload, uno con il parametro facoltativo e l'altra senza. È possibile eseguire l'overload di una routine con un elenco di parametri corrispondente a uno di questi. Le seguenti dichiarazioni illustrare questo concetto.  
  
 [!code-vb[VbVbcnProcedures&#58;](./codesnippet/VisualBasic/considerations-in-overloading-procedures_1.vb)]  
  
 [!code-vb[60 VbVbcnProcedures](./codesnippet/VisualBasic/considerations-in-overloading-procedures_2.vb)]  
  
 [!code-vb[VbVbcnProcedures n.&61;](./codesnippet/VisualBasic/considerations-in-overloading-procedures_3.vb)]  
  
 Per una procedura con più di un parametro facoltativo, è un set di overload impliciti, una logica simile a quello dell'esempio precedente.  
  
## <a name="implicit-overloads-for-a-paramarray-parameter"></a>Overload impliciti per un parametro ParamArray  
 Il compilatore considera una routine con un [ParamArray](../../../../visual-basic/language-reference/modifiers/paramarray.md) parametro venga specificato un numero infinito di overload, che differiscono tra loro per ciò che il codice chiamante passa alla matrice di parametri, come indicato di seguito:  
  
-   Quando il codice chiamante non fornisce un argomento a un overload di`ParamArray`  
  
-   Quando il codice chiamante fornisce una matrice unidimensionale di un overload di `ParamArray` tipo di elemento  
  
-   Per ogni integer positivo, un overload quando il codice chiamante fornisce tale numero di argomenti, ognuno del `ParamArray` tipo di elemento  
  
 Le dichiarazioni seguenti illustrano questi overload impliciti.  
  
 [!code-vb[VbVbcnProcedures&#68;](./codesnippet/VisualBasic/considerations-in-overloading-procedures_4.vb)]  
  
 [!code-vb[VbVbcnProcedures&#70;](./codesnippet/VisualBasic/considerations-in-overloading-procedures_5.vb)]  
  
 Impossibile eseguire l'overload di una routine con un elenco di parametri che accetta una matrice unidimensionale per la matrice di parametri. Tuttavia, è possibile utilizzare le firme degli altri overload impliciti. Le seguenti dichiarazioni illustrare questo concetto.  
  
 [!code-vb[VbVbcnProcedures&#71;](./codesnippet/VisualBasic/considerations-in-overloading-procedures_6.vb)]  
  
## <a name="typeless-programming-as-an-alternative-to-overloading"></a>Programmazione senza tipi come alternativa all'overload  
 Se si desidera consentire al codice chiamante di passare diversi tipi di dati a un parametro, un approccio alternativo è costituito dalla programmazione. È possibile impostare il tipo di opzione per il controllo `Off` con il [istruzione Option Strict](../../../../visual-basic/language-reference/statements/option-strict-statement.md) o [/optionstrict](../../../../visual-basic/reference/command-line-compiler/optionstrict.md) l'opzione del compilatore. Quindi non è necessario dichiarare il tipo di dati del parametro. Tuttavia, questo approccio presenta i seguenti svantaggi rispetto all'overload:  
  
-   Programmazione senza tipi produce un codice di esecuzione meno efficiente.  
  
-   La procedura è necessario testare per ogni tipo di dati che anticipa il passaggio.  
  
-   Il compilatore non può segnalare un errore se il codice chiamante passa un tipo di dati che non supportano la procedura.  
  
## <a name="see-also"></a>Vedere anche  
 [Procedure](./index.md)   
 [Gli argomenti e parametri di routine](./procedure-parameters-and-arguments.md)   
 [Le procedure di risoluzione](./troubleshooting-procedures.md)   
 [Procedura: definire più versioni di una routine](./how-to-define-multiple-versions-of-a-procedure.md)   
 [Procedura: chiamare una routine di overload](./how-to-call-an-overloaded-procedure.md)   
 [Procedura: eseguire l'Overload di una routine che accetta parametri facoltativi](./how-to-overload-a-procedure-that-takes-optional-parameters.md)   
 [Procedura: eseguire l'Overload di una routine che accetta un numero indefinito di parametri](./how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters.md)   
 [Risoluzione dell'overload](./overload-resolution.md)   
 [Overload](../../../../visual-basic/language-reference/modifiers/overloads.md)
