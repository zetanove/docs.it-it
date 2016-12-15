---
title: "Sub Procedures (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/15/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Sub procedures, about Sub procedures"
  - "statement blocks"
  - "Sub procedures, calling"
  - "procedures, calling"
  - "Sub procedures, syntax"
  - "Sub procedures"
  - "procedures, Sub"
  - "syntax, Sub procedures"
ms.assetid: 6a0a4958-ed0a-4d3d-8d31-0772c82bda58
caps.latest.revision: 21
caps.handback.revision: 21
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Sub Procedures (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Una routine `Sub` è costituita da una serie di istruzioni [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] racchiuse tra le istruzioni `Sub` ed `End Sub`.  La routine `Sub` esegue un'attività e quindi restituisce il controllo al codice chiamante, senza tuttavia restituire a quest'ultimo un valore.  
  
 Ogni volta che la routine viene chiamata, le relative istruzioni vengono eseguite a partire dalla prima istruzione eseguibile dopo l'istruzione `Sub` e fino alla prima istruzione `End Sub`, `Exit Sub` o `Return` rilevata.  
  
 È possibile definire una routine `Sub` in moduli, classi e strutture.  Per impostazione predefinita, la routine è `Public` ed è pertanto possibile chiamarla da qualsiasi punto dell'applicazione che disponga dell'accesso al modulo, alla classe o alla struttura nella quale è stata definita.  Il termine *metodo* descrive una procedura `Sub` o `Function` alla quale si accede al di fuori del relativo modulo, classe o struttura che la definisce.  Per ulteriori informazioni, vedere [Procedures](../../../../visual-basic/programming-guide/language-features/procedures/index.md).  
  
 Una routine `Sub` può accettare argomenti, ad esempio costanti, variabili o espressioni, passati dal codice chiamante.  
  
## Sintassi di dichiarazione  
 La sintassi per dichiarare una routine `Sub` è la seguente:  
  
 `[` *modificatori* `] Sub`  *subname* `[(` *parameterlist* `)]`  
  
 `' Statements of the Sub procedure.`  
  
 `End Sub`  
  
 Nei `modifiers` è possibile specificare il livello di accesso e le informazioni sull'overload, l'override, la condivisione e lo shadowing.  Per ulteriori informazioni, vedere [Sub Statement](../../../../visual-basic/language-reference/statements/sub-statement.md).  
  
## Dichiarazione dei parametri  
 Ogni parametro di routine viene dichiarato in modo simile a una variabile, specificandone il nome e il tipo di dati.  È possibile specificare anche il meccanismo di passaggio e se il parametro è facoltativo oppure una matrice di parametri.  
  
 La sintassi per ciascun parametro dell'elenco dei parametri è la seguente:  
  
 `[Optional] [ByVal | ByRef] [ParamArray]`  *parametername*  `As`  *datatype*  
  
 Se il parametro è facoltativo, è necessario specificare nella dichiarazione anche un valore predefinito.  La sintassi per la specifica di un valore predefinito è la seguente:  
  
 `Optional [ByVal | ByRef]`   *parametername*  `As`  *tipo di dati*  `=`  *defaultvalue*  
  
### Parametri come variabili locali  
 Quando il controllo passa alla routine, ogni parametro viene considerato come variabile locale.  Questo significa che la relativa durata è identica a quella della routine e l'ambito è l'intera routine.  
  
## Sintassi di chiamata  
 Una routine `Sub` viene chiamata in modo esplicito tramite un'istruzione di chiamata autonoma.  Non è possibile chiamarla utilizzandone il nome in un'espressione.  È necessario specificare valori per tutti gli argomenti non facoltativi e racchiudere l'elenco degli argomenti tra parentesi.  Se non viene specificato alcun argomento, è anche possibile omettere le parentesi.  L'utilizzo della parola chiave `Call` è facoltativo ma non consigliato.  
  
 La sintassi di una chiamata a una routine `Sub` è la seguente:  
  
 `[Call]`  *subname* `[(`*argumentlist*`)]`  
  
 È possibile chiamare il metodo `Sub` dall'esterno della classe da cui è definito.  In primo luogo è necessario utilizzare la parola chiave `New` per creare un'istanza della classe o chiamare un metodo che restituisce un'istanza della classe.  Per ulteriori informazioni, vedere [New Operator](../../../../visual-basic/language-reference/operators/new-operator.md).  In seguito è possibile utilizzare la sintassi seguente per chiamare il metodo `Sub` sull'oggetto dell'istanza:  
  
 *Oggetto*.*nomemetodo*`[(`*elencoargomenti*`)]`  
  
### Illustrazione della dichiarazione e della chiamata  
 La routine `Sub` riportata di seguito indica all'utente del computer quale attività l'applicazione sta per eseguire e visualizza un timestamp.  Anziché duplicare questo codice all'inizio di ogni attività, l'applicazione chiama semplicemente `tellOperator` da posizioni diverse.  Ogni chiamata passa una stringa nell'argomento  `task` , che identifica l'attività che sta per essere avviata.  
  
 [!code-vb[VbVbcnProcedures#2](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/VisualBasic/sub-procedures_1.vb)]  
  
 Nell'esempio riportato di seguito viene illustrata una tipica chiamata a `tellOperator`.  
  
 [!code-vb[VbVbcnProcedures#3](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/VisualBasic/sub-procedures_2.vb)]  
  
## Vedere anche  
 [Procedures](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Routine Function](../../../../visual-basic/programming-guide/language-features/procedures/function-procedures.md)   
 [Routine Property](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [Operator Procedures](../../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)   
 [Procedure Parameters and Arguments](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Sub Statement](../../../../visual-basic/language-reference/statements/sub-statement.md)   
 [How to: Call a Procedure that Does Not Return a Value](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-a-procedure-that-does-not-return-a-value.md)   
 [How to: Call an Event Handler in Visual Basic](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-an-event-handler.md)