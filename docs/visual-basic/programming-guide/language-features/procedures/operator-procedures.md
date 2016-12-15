---
title: "Operator Procedures (Visual Basic) | Microsoft Docs"
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
  - "Visual Basic code, procedures"
  - "procedures, operator"
  - "Visual Basic code, operators"
  - "syntax, Operator procedures"
  - "operators [Visual Basic], overloading"
  - "overloaded operators"
  - "operator overloading"
  - "operator procedures"
ms.assetid: 8c513d38-246b-4fb7-8b75-29e1364e555b
caps.latest.revision: 17
caps.handback.revision: 17
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Operator Procedures (Visual Basic)
[!INCLUDE[vs2017banner](../../../../csharp/includes/vs2017banner.md)]

Una routine di operatore è costituita da una serie di istruzioni [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] che definiscono il comportamento di un operatore standard, ad esempio `*`, `<>` o `And`, su una classe o una struttura definita.  Tale routine viene definita anche *overload dell'operatore*.  
  
## Definizione delle routine di operatore  
 Dopo aver definito una classe o una struttura, è possibile dichiarare le variabili dello stesso tipo di tale classe o struttura.  Tali variabili devono talvolta partecipare a un'operazione come parte di un'espressione,  ossia come operandi di un operatore.  
  
 In [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb_md.md)] gli operatori vengono definiti solo sui tipi di dati più importanti.  È possibile definire il comportamento di un operatore quando il tipo di uno o di entrambi gli operandi corrisponde a quello della classe o della struttura.  
  
 Per ulteriori informazioni, vedere [Operator Statement](../../../../visual-basic/language-reference/statements/operator-statement.md).  
  
## Tipi delle routine di operatore  
 Una routine di operatore può essere di uno dei seguenti tipi:  
  
-   Una definizione di un operatore unario in cui l'argomento è del tipo della classe o della struttura.  
  
-   Una definizione di un operatore binario in cui almeno uno degli argomenti è del tipo della classe o della struttura.  
  
-   Una definizione di un operatore di conversione in cui l'argomento è del tipo della classe o della struttura.  
  
-   Una definizione di un operatore di conversione che restituisce il tipo della classe o della struttura.  
  
 Gli operatori di conversione sono sempre unari e `CType` viene sempre utilizzato come operatore da definire.  
  
## Sintassi di dichiarazione  
 La sintassi per dichiarare una routine di operatore è la seguente:  
  
 `Public Shared`   `[Widening | Narrowing]`   `Operator`   ``  *simbolooperatore*  `(` *operando1*  `[,`  *operando2* `]) As`  *tipodati*  
  
 `' Statements of the operator procedure.`  
  
 `End Operator`  
  
 Le parole chiave `Widening` o `Narrowing` vengono utilizzate solo su un operatore di conversione dei tipi.  Il simbolo dell'operatore è sempre la [Funzione CType](../../../../visual-basic/language-reference/functions/ctype-function.md) per un operatore di conversione dei tipi.  
  
 Per definire un operatore binario è necessario dichiarare due operandi, mentre per definire un operatore unario è necessario dichiarare un operando, incluso un operatore di conversione dei tipi.  Tutti gli operandi devono essere dichiarati `ByVal`.  
  
 La dichiarazione di ciascun operando viene eseguita in modo identico alla dichiarazione dei parametri per le [Sub Procedures](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md).  
  
### Tipo di dati  
 Poiché la definizione di un operatore viene eseguita su una classe o una struttura già definita, almeno uno degli operandi deve essere del tipo di dati di tale classe o struttura.  Per un operatore di conversione dei tipi, l'operando o il tipo restituito deve essere del tipo di dati della classe o della struttura.  
  
 Per informazioni dettagliate, vedere [Operator Statement](../../../../visual-basic/language-reference/statements/operator-statement.md).  
  
## Sintassi di chiamata  
 Per richiamare una routine di operatore in modo implicito, è necessario utilizzare il simbolo dell'operatore in un'espressione.  Gli operandi vengono forniti con le stesse modalità utilizzate per gli operatori predefiniti.  
  
 La sintassi per una chiamata implicita a una routine di operatore è la seguente:  
  
 `Dim testStruct As`  *nomestruttura*  
  
 `Dim testNewStruct As`  *nomestruttura*  `= testStruct`  *simbolooperatore*  `10`  
  
### Illustrazione della dichiarazione e della chiamata  
 Nella struttura riportata di seguito un valore integer con segno a 128 bit viene memorizzato come parte costitutiva più e meno significativa.  L'operatore `+` viene definito per aggiungere due valori `veryLong` e generare un valore `veryLong` risultante.  
  
 [!code-vb[VbVbcnProcedures#23](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/VisualBasic/operator-procedures_1.vb)]  
  
 Nell'esempio riportato di seguito viene illustrata una chiamata tipica all'operatore `+` definito su `veryLong`.  
  
 [!code-vb[VbVbcnProcedures#24](../../../../visual-basic/programming-guide/language-features/procedures/codesnippet/VisualBasic/operator-procedures_2.vb)]  
  
 Per ulteriori informazioni ed esempi, vedere [Operator Overloading in Visual Basic 2005](http://go.microsoft.com/fwlink/?LinkId=101703) \(informazioni in lingua inglese\).  
  
## Vedere anche  
 [Procedures](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Sub Procedures](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md)   
 [Routine Function](../../../../visual-basic/programming-guide/language-features/procedures/function-procedures.md)   
 [Routine Property](../../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)   
 [Procedure Parameters and Arguments](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Operator Statement](../../../../visual-basic/language-reference/statements/operator-statement.md)   
 [How to: Define an Operator](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-an-operator.md)   
 [How to: Define a Conversion Operator](../../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)   
 [How to: Call an Operator Procedure](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-an-operator-procedure.md)   
 [How to: Use a Class that Defines Operators](../../../../visual-basic/programming-guide/language-features/procedures/how-to-use-a-class-that-defines-operators.md)