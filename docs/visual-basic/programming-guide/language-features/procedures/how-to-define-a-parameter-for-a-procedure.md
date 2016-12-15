---
title: "How to: Define a Parameter for a Procedure (Visual Basic) | Microsoft Docs"
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
  - "procedure parameters, defining data types for"
  - "procedures, parameters"
  - "procedures, defining"
  - "Visual Basic code, procedures"
  - "procedure parameters, defining"
ms.assetid: 7962808d-407e-4e84-984e-43e9857c53c9
caps.latest.revision: 15
caps.handback.revision: 15
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# How to: Define a Parameter for a Procedure (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Un *parametro* consente al codice chiamante di passare un valore alla routine quando ne esegue la chiamata.  La dichiarazione di ciascun parametro per una routine avviene come la dichiarazione di una variabile, specificandone il nome e il tipo di dati.  È inoltre possibile specificare il meccanismo di passaggio e se il parametro è facoltativo.  
  
 Per ulteriori informazioni, vedere [Procedure Parameters and Arguments](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md).  
  
### Per definire un parametro di routine  
  
1.  Nella dichiarazione di routine aggiungere il nome di parametro all'elenco di parametri della routine, separandolo dagli altri parametri mediante virgole.  
  
2.  Scegliere il tipo di dati del parametro.  
  
3.  Inserire una clausola `As` dopo il nome del parametro per specificare il tipo di dati.  
  
4.  Scegliere il meccanismo di passaggio desiderato per il parametro.  Generalmente i parametri vengono passati per valore, a meno che non si desideri modificarne il valore nel codice chiamante mediante la routine.  
  
5.  Inserire [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md) o [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md) prima del nome di parametro per specificare il meccanismo di passaggio.  Per ulteriori informazioni, vedere [Differences Between Passing an Argument By Value and By Reference](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-passing-an-argument-by-value-and-by-reference.md).  
  
6.  Se il parametro è facoltativo, inserire [Optional](../../../../visual-basic/language-reference/modifiers/optional.md) prima del meccanismo di passaggio e specificare un segno di uguale \(`=`\) e un valore predefinito dopo il tipo di dati del parametro.  
  
     Nell'esempio di codice seguente viene definita la struttura di una routine `Sub` con tre parametri.  I primi due sono obbligatori mentre il terzo è facoltativo.  Nell'elenco di parametri le dichiarazioni di parametro sono separate da virgole.  
  
     [!code-vb[VbVbcnProcedures#33](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/VisualBasic/how-to-define-a-parameter-for-a-procedure_1.vb)]  
  
     Il primo parametro accetta un oggetto `customer` e `updateCustomer` può aggiornare direttamente la variabile passata a `c` in quanto l'argomento viene passato [ByRef](../../../../visual-basic/language-reference/modifiers/byref.md).  La routine non può modificare i valori degli ultimi due argomenti in quanto vengono passati [ByVal](../../../../visual-basic/language-reference/modifiers/byval.md).  
  
     Se il codice chiamante non fornisce alcun valore per il parametro `level` , viene automaticamente impostato il valore predefinito 0.  
  
     Se l'opzione di controllo dei tipi \([Option Strict Statement](../../../../visual-basic/language-reference/statements/option-strict-statement.md)\) è `Off`, la clausola `As` è facoltativa quando si definisce un parametro.  Se, tuttavia, un parametro utilizza una clausola `As`, dovranno utilizzarla tutti i parametri.  Se l'opzione di controllo dei tipi è `On`, la clausola `As` è obbligatoria per ogni definizione di parametro.  
  
     La specifica dei tipi di dati per tutti gli elementi di programmazione è nota come *tipizzazione forte*.  Quando si imposta `Option Strict On`, viene applicata la tipizzazione forte,  che è particolarmente consigliata per i seguenti motivi:  
  
    -   Attiva il supporto IntelliSense per le variabili e i parametri,  consentendo la visualizzazione delle relative proprietà e di altri membri mentre si digita il codice.  
  
    -   Consente al compilatore di eseguire la verifica dei tipi.  In questo modo è possibile rilevare le istruzioni destinate ad avere esito negativo in fase di esecuzione a causa di errori quale l'overflow.  Vengono inoltre rilevate le chiamate a metodi su oggetti che non li supportano.  
  
    -   Comporta un'esecuzione più veloce del codice.  Ciò è possibile anche perché se non si specifica un tipo di dati per un elemento di programmazione, il compilatore di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] assegna automaticamente il tipo `Object`.  Con il codice compilato potrebbe essere necessario eseguire più conversioni tra `Object` e altri tipi di dati, con un conseguente calo delle prestazioni.  
  
## Vedere anche  
 [Procedures](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Sub Procedures](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md)   
 [Routine Function](../../../../visual-basic/programming-guide/language-features/procedures/function-procedures.md)   
 [How to: Pass Arguments to a Procedure](../../../../visual-basic/programming-guide/language-features/procedures/how-to-pass-arguments-to-a-procedure.md)   
 [Passing Arguments by Value and by Reference](../../../../visual-basic/programming-guide/language-features/procedures/passing-arguments-by-value-and-by-reference.md)   
 [Recursive Procedures](../../../../visual-basic/programming-guide/language-features/procedures/recursive-procedures.md)   
 [Procedure Overloading](../../../../visual-basic/programming-guide/language-features/procedures/procedure-overloading.md)   
 [Objects and Classes](../../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)   
 [Programmazione orientata ad oggetti](../Topic/Object-Oriented%20Programming%20\(C%23%20and%20Visual%20Basic\).md)