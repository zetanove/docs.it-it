---
title: "Considerations in Overloading Procedures (Visual Basic) | Microsoft Docs"
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
  - "signatures, ParamArray arguments"
  - "ParamArray keyword, parameter arrays"
  - "ParamArray keyword, arguments and signatures"
  - "function overloading, implicit overloads for ParamArray"
  - "ParamArray keyword, signatures"
  - "Visual Basic code, procedures"
  - "arguments [Visual Basic], parameter arrays"
  - "procedures, overloading"
  - "parameters, lists"
  - "function overloading, typeless programming"
  - "typeless programming"
  - "function overloading, restrictions"
  - "arguments [Visual Basic], optional"
  - "optional arguments, overloading"
  - "signatures, procedure"
  - "parameter lists"
  - "parameter arrays, overloading arguments"
  - "Visual Basic code, parameter lists"
  - "procedure overloading, considerations"
  - "Option Explicit statement"
  - "restrictions, overloading procedures"
  - "procedures, parameter lists"
ms.assetid: a2001248-10d0-42c5-b0ce-eeedc987319f
caps.latest.revision: 26
caps.handback.revision: 26
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Considerations in Overloading Procedures (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Quando si esegue l'overload di una routine, è necessario utilizzare una *firma* diversa per ciascuna versione di overload.  Questo in genere significa che per ogni versione deve essere specificato un elenco di parametri distinto.  Per ulteriori informazioni, vedere "Firma diversa" in [Procedure Overloading](../../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md).  
  
 È possibile eseguire l'overload di una routine `Function` con una routine `Sub` e viceversa, purché le firme siano diverse.  Non è consentito che l'unica differenza tra due overload sia la presenza o meno di un valore restituito.  
  
 È possibile eseguire l'overload di una proprietà in base alla stessa procedura utilizzata per una routine e con le stesse limitazioni.  Non è invece possibile eseguire l'overload di una routine con una proprietà o viceversa.  
  
## Alternative alle versioni di overload  
 In alcuni casi esistono alternative alle versioni di overload, specialmente quando la presenza di argomenti è facoltativa o il relativo numero è variabile.  
  
 Si tenga presente che gli argomenti facoltativi non sono necessariamente supportati da tutti i linguaggi e che le matrici di parametri sono disponibili solo in [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)].  Le versioni di overload offrono il massimo livello di flessibilità per la scrittura di routine destinate con ogni probabilità a essere chiamate da codice creato in uno dei numerosi linguaggi.  
  
### Overload e argomenti facoltativi  
 Se il codice chiamante può facoltativamente specificare oppure omettere uno o più argomenti, è possibile definire più versioni di overload o utilizzare parametri facoltativi.  
  
#### Utilizzo di versioni di overload  
 Di seguito sono riportati i casi in cui è opportuno prendere in considerazione la definizione di una serie di versioni di overload.  
  
-   La logica presente nel codice della routine varia in modo considerevole a seconda che nel codice chiamante sia specificato o meno un argomento facoltativo.  
  
-   Il codice della routine non può verificare in modo affidabile se il codice chiamante ha fornito un argomento facoltativo.  Questa situazione si verifica, ad esempio, se non è possibile prevedere alcun valore predefinito che possa essere fornito dal codice chiamante.  
  
#### Utilizzo di parametri facoltativi  
 Di seguito sono illustrati i casi in cui è possibile utilizzare uno o più parametri facoltativi.  
  
-   L'unica azione obbligatoria quando nel codice chiamante non è specificato un argomento facoltativo consiste nell'impostare il parametro su un valore predefinito.  In tal caso, per semplificare il codice della routine è possibile definire un'unica versione con uno o più parametri `Optional`.  
  
 Per ulteriori informazioni, vedere [Optional Parameters](../../../../visual-basic/programming-guide/language-features/procedures/optional-parameters.md).  
  
### Overload e ParamArray  
 Se il codice chiamante può passare un numero variabile di argomenti, è possibile definire più versioni di overload o utilizzare una matrice di parametri.  
  
#### Utilizzo di versioni di overload  
 Di seguito sono riportati i casi in cui è opportuno prendere in considerazione la definizione di una serie di versioni di overload.  
  
-   Si è certi che il codice chiamante passa sempre un numero ridotto di valori alla matrice di parametri.  
  
-   La logica presente nel codice della routine varia in modo considerevole in base al numero di valori passati dal codice chiamante.  
  
-   Il codice chiamante può passare valori di diversi tipi di dati.  
  
#### Utilizzo di una matrice di parametri  
 Di seguito sono riportati i casi in cui si consiglia l'utilizzo di un parametro `ParamArray`.  
  
-   Non è possibile prevedere il numero di valori che il codice chiamante può passare alla matrice di parametri e potrebbe trattarsi di un numero di valori elevato.  
  
-   La logica della routine è indicata per scorrere tutti i valori passati dal codice chiamante, dal momento che esegue le stesse operazioni su ogni valore.  
  
 Per ulteriori informazioni, vedere [Parameter Arrays](../../../../visual-basic/programming-guide/language-features/procedures/parameter-arrays.md).  
  
## Overload impliciti per i parametri facoltativi  
 Una routine con un parametro [Optional](../../../../visual-basic/language-reference/modifiers/optional.md) equivale a due routine di overload, una con il parametro facoltativo e una senza.  Non è possibile eseguire l'overload di una routine di questo tipo con un elenco di parametri corrispondente a uno di quelli riportati di seguito.  Questa situazione viene illustrata nelle dichiarazioni seguenti.  
  
 [!code-vb[VbVbcnProcedures#58](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/VisualBasic/considerations-in-overloading-procedures_1.vb)]  
  
 [!code-vb[VbVbcnProcedures#60](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/VisualBasic/considerations-in-overloading-procedures_2.vb)]  
  
 [!code-vb[VbVbcnProcedures#61](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/VisualBasic/considerations-in-overloading-procedures_3.vb)]  
  
 Per una routine con più parametri facoltativi esiste un insieme di overload impliciti, che sono il risultato di una logica simile a quella dell'esempio precedente.  
  
## Overload impliciti per un parametro ParamArray  
 Il compilatore presuppone che una routine con un parametro [ParamArray](../../../../visual-basic/language-reference/modifiers/paramarray.md) disponga di un numero infinito di overload, che si differenziano l'uno dall'altro in base agli elementi passati dal codice chiamante alla matrice di parametri, come illustrato di seguito:  
  
-   Un overload quando il codice chiamante non fornisce un argomento al parametro `ParamArray`  
  
-   Un overload quando il codice chiamante fornisce una matrice unidimensionale del tipo di elemento `ParamArray`  
  
-   Per ogni Integer positivo, un overload quando il codice chiamante fornisce tale numero di argomenti, ciascuno del tipo di elemento `ParamArray`  
  
 Nelle dichiarazioni riportate di seguito vengono illustrati questi overload impliciti.  
  
 [!code-vb[VbVbcnProcedures#68](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/VisualBasic/considerations-in-overloading-procedures_4.vb)]  
  
 [!code-vb[VbVbcnProcedures#70](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/VisualBasic/considerations-in-overloading-procedures_5.vb)]  
  
 Non è possibile eseguire l'overload di una routine di questo tipo con un elenco di parametri che accetta una matrice unidimensionale per la matrice di parametri.  È invece possibile utilizzare le firme di altri overload impliciti.  Questa situazione viene illustrata nelle dichiarazioni seguenti.  
  
 [!code-vb[VbVbcnProcedures#71](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/VisualBasic/considerations-in-overloading-procedures_6.vb)]  
  
## Programmazione senza tipi come alternativa all'overload  
 Per consentire al codice chiamante ai tipi di dati diversi di passare a un parametro, un'alternativa consiste programmazione senza tipi.  È possibile impostare l'opzione di controllo dei tipi su `Off` con l'[Option Strict Statement](../../../../visual-basic/language-reference/statements/option-strict-statement.md) o con l'opzione del compilatore [\/optionstrict](../../../../visual-basic/reference/command-line-compiler/optionstrict.md).  Non è quindi necessario dichiarare il tipo di dati del parametro.  Rispetto all'overload, tuttavia, questo metodo presenta i seguenti svantaggi:  
  
-   La programmazione senza tipi produce un codice di esecuzione meno efficace.  
  
-   È necessario che la routine verifichi ogni tipo di dati del quale anticipa il passaggio.  
  
-   Il compilatore non può segnalare un errore se il codice chiamante passa un tipo di dati non supportato dalla routine.  
  
## Vedere anche  
 [Procedures](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Procedure Parameters and Arguments](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Troubleshooting Procedures](../../../../visual-basic/programming-guide/language-features/procedures/troubleshooting-procedures.md)   
 [How to: Define Multiple Versions of a Procedure](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-multiple-versions-of-a-procedure.md)   
 [How to: Call an Overloaded Procedure](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-an-overloaded-procedure.md)   
 [How to: Overload a Procedure that Takes Optional Parameters](../../../../visual-basic/programming-guide/language-features/procedures/how-to-overload-a-procedure-that-takes-optional-parameters.md)   
 [How to: Overload a Procedure that Takes an Indefinite Number of Parameters](../../../../visual-basic/programming-guide/language-features/procedures/how-to-overload-a-procedure-that-takes-an-indefinite-number-of-parameters.md)   
 [Overload Resolution](../../../../visual-basic/programming-guide/language-features/procedures/overload-resolution.md)   
 [Overloads](../../../../visual-basic/language-reference/modifiers/overloads.md)