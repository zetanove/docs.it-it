---
title: "Funzione CType (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.CType"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "(espressioni) risultati di conversione"
  - "conversioni esplicite di tipi di dati"
  - "CType (funzione)"
  - "conversioni, espressione"
ms.assetid: dd4b29e7-6fa1-428c-877e-69955420bb72
caps.latest.revision: 22
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 22
---
# Funzione CType (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Restituisce il risultato della conversione esplicita di un'espressione in un tipo di dati, una struttura, una classe, un'interfaccia o un oggetto specificato.  
  
## Sintassi  
  
```  
CType(expression, typename)  
```  
  
## Parti  
 `expression`  
 Qualsiasi espressione valida.  Se il valore di `expression` non rientra nell'intervallo consentito da `typename`, viene generata un'eccezione.  
  
 `typename`  
 Qualsiasi espressione valida in una clausola `As` di un'istruzione `Dim`, ovvero il nome di qualsiasi tipo di dati, oggetto, struttura, classe o interfaccia.  
  
## Note  
  
> [!TIP]
>  È anche possibile utilizzare le funzioni seguenti per eseguire una conversione del tipo:  
>   
>  -   Funzioni di conversione dei tipi come `CByte`, `CDbl`e `CInt` che eseguono una conversione in un tipo di dati specifico.  Per ulteriori informazioni, vedere [Type Conversion Functions](../../../visual-basic/language-reference/functions/type-conversion-functions.md).  
> -   [DirectCast Operator](../../../visual-basic/language-reference/operators/directcast-operator.md) o [TryCast Operator](../../../visual-basic/language-reference/operators/trycast-operator.md).  Questi operatori richiedono che un tipo erediti da o implementi l'altro tipo.  Possono fornire prestazioni migliori rispetto a `CType` nella conversione da e verso il tipo di dati `Object`.  
  
 La funzione `CType` viene compilata inline. Il codice di conversione fa quindi parte del codice con cui viene valutata l'espressione.  In alcuni casi, il codice viene eseguito più velocemente quanto non viene chiamata alcuna procedura per eseguire la conversione.  
  
 Se non è stata definita alcuna conversione da `expression` in `typename`, ad esempio da `Integer` in `Date`, in Visual Basic viene visualizzato un messaggio di errore in fase di compilazione.  
  
 Se un'operazione di conversione ha esito negativo in fase di esecuzione, viene generata l'eccezione appropriata.  Se una conversione verso un tipo di dati più piccolo ha esito negativo, il risultato più frequente è rappresentato da un'eccezione <xref:System.OverflowException>.  Se la conversione non è definita, viene generata un'eccezione <xref:System.InvalidCastException>.  Ad esempio, questa situazione può verificarsi se `expression` è di tipo `Object` e il relativo tipo di runtime non viene convertito in `typename`.  
  
 Se il tipo di dati di `expression` o di `typename` è una classe o una struttura specificata, è possibile definire `CType` su tale classe o struttura come operatore di conversione.  In questo modo, la funzione `CType` funge da *operatore di overload* In questo caso, è possibile controllare il comportamento delle conversioni da e nella classe o struttura, incluse le eccezioni che possono essere generate.  
  
## Overload  
 È possibile eseguire l'overload dell'operatore `CType` anche su una classe o una struttura definita all'esterno del codice.  Se il codice esegue una conversione da o in una classe o struttura di questo tipo, è importante comprendere il comportamento del relativo operatore `CType`.  Per ulteriori informazioni, vedere [Operator Procedures](../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md).  
  
## Conversione di oggetti dinamici  
 Le conversioni di tipi di oggetti dinamici sono eseguite dalle conversioni dinamiche definite dall'utente che utilizzano i metodi <xref:System.Dynamic.DynamicMetaObject.BindConvert%2A> o <xref:System.Dynamic.DynamicObject.TryConvert%2A>.  Se si utilizzano gli oggetti dinamici, utilizzare il metodo <xref:Microsoft.VisualBasic.Conversion.CTypeDynamic%2A> per convertire l'oggetto dinamico.  
  
## Esempio  
 Nell'esempio seguente la funzione `CType` viene utilizzata per convertire un'espressione nel tipo di dati `Single`.  
  
 [!code-vb[VbVbalrFunctions#24](../../../visual-basic/language-reference/functions/codesnippet/visualbasic/ctype-function_1.vb)]  
  
 Per ulteriori esempi, vedere [Implicit and Explicit Conversions](../../../visual-basic/programming-guide/language-features/data-types/implicit-and-explicit-conversions.md).  
  
## Vedere anche  
 <xref:System.OverflowException>   
 <xref:System.InvalidCastException>   
 [Type Conversion Functions](../../../visual-basic/language-reference/functions/type-conversion-functions.md)   
 [Conversion Functions](../../../visual-basic/language-reference/functions/conversion-functions.md)   
 [Operator Statement](../../../visual-basic/language-reference/statements/operator-statement.md)   
 [How to: Define a Conversion Operator](../../../visual-basic/programming-guide/language-features/procedures/how-to-define-a-conversion-operator.md)   
 [Conversione di tipi in .NET Framework](../Topic/Type%20Conversion%20in%20the%20.NET%20Framework.md)