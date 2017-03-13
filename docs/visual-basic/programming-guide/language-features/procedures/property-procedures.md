---
title: "Routine Property (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Set (istruzione), routine Property"
  - "Visual Basic (codice), routine"
  - "valori restituiti, routine Property"
  - "sintassi, routine Property"
  - "routine, Property"
  - "Visual Basic (codice), proprietà"
  - "routine, chiamata"
  - "proprietà [Visual Basic], personalizzate"
  - "Property (routine)"
  - "Get (istruzione), routine Property"
ms.assetid: 46a98379-e1a2-45dd-a48c-b51213f5ab07
caps.latest.revision: 22
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 22
---
# Routine Property (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Una routine della proprietà è una serie di istruzioni di [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] che gestiscono una proprietà personalizzata di un modulo, una classe o una struttura.  Le routine Property sono anche note come *funzioni di accesso alle proprietà*.  
  
 In [!INCLUDE[vbprvb](../../../../csharp/programming-guide/concepts/linq/includes/vbprvb-md.md)] sono disponibili le seguenti routine della proprietà:  
  
-   Una routine `Get` restituisce il valore di una proprietà  e viene chiamata quando si accede alla proprietà in un'espressione.  
  
-   Una routine `Set` imposta una proprietà su un valore, compreso un riferimento a un oggetto.  Viene chiamata quando si assegna un valore alla proprietà.  
  
 Le routine della proprietà vengono generalmente definite in coppie, mediante le istruzioni `Get` e `Set`, tuttavia è possibile definire una routine singolarmente, se la proprietà è in sola lettura \([Get Statement](../../../../visual-basic/language-reference/statements/get-statement.md)\) o in sola scrittura \([Set Statement](../../../../visual-basic/language-reference/statements/set-statement.md)\).  
  
 È possibile omettere le routine `Get` e `Set` in caso di utilizzo di una proprietà implementata automaticamente.  Per ulteriori informazioni, vedere [Auto\-Implemented Properties](../../../../visual-basic/programming-guide/language-features/procedures/auto-implemented-properties.md).  
  
 È possibile definire le proprietà in classi, strutture e moduli.  Le proprietà sono `Public` per impostazione predefinita, il che significa che è possibile chiamarle da un punto qualsiasi dell'applicazione che può accedere al contenitore della proprietà.  
  
 Per un confronto tra proprietà e variabili, vedere [Differences Between Properties and Variables in Visual Basic](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-properties-and-variables.md).  
  
## Sintassi di dichiarazione  
 Una proprietà viene definita da un blocco di codice racchiuso tra le istruzioni [Property Statement](../../../../visual-basic/language-reference/statements/property-statement.md) e `End Property`.  All'interno del blocco ciascuna routine della proprietà viene visualizzata come un blocco interno racchiuso tra un'istruzione di dichiarazione \(`Get` o `Set`\) e la dichiarazione `End` corrispondente.  
  
 La sintassi per dichiarare una proprietà e le relative routine è la seguente:  
  
```  
[Default] [Modifiers] Property PropertyName[(ParameterList)] [As DataType]  
    [AccessLevel] Get  
        ' Statements of the Get procedure.  
        ' The following statement returns an expression as the property's value.  
        Return Expression  
    End Get  
    [AccessLevel] Set[(ByVal NewValue As DataType)]  
        ' Statements of the Set procedure.  
        ' The following statement assigns newvalue as the property's value.  
        LValue = NewValue  
    End Set  
End Property  
- or -  
[Default] [Modifiers] Property PropertyName [(ParameterList)] [As DataType]  
```  
  
 I `Modifiers` possono specificare il livello di accesso e informazioni su overload, override, condivisione e shadowing, nonché indicare se la proprietà è in sola lettura o scrittura.  `AccessLevel` la routine di `Set` o di `Get` può essere qualsiasi livello più restrittivo rispetto al livello di accesso specificato per la proprietà stessa.  Per ulteriori informazioni, vedere [Property Statement](../../../../visual-basic/language-reference/statements/property-statement.md).  
  
### Tipo di dati  
 Il tipo di dati e il livello di accesso principale di una proprietà sono definiti nell'istruzione `Property`, non nelle routine della proprietà.  Una proprietà può avere un solo tipo di dati.  Non è possibile, ad esempio, definire una proprietà per memorizzare un valore `Decimal` ma recuperare un valore `Double`.  
  
### Livello di accesso  
 È possibile, tuttavia, definire un livello di accesso principale per una proprietà e restringere ulteriormente il livello di accesso in una delle rispettive routine.  È possibile, ad esempio, definire una proprietà `Public`, quindi definire una routine `Private Set`.  La routine `Get` rimane `Public`.  È possibile modificare il livello di accesso in una sola delle routine della proprietà e renderlo solo più restrittivo rispetto al livello di accesso principale.  Per ulteriori informazioni, vedere [How to: Declare a Property with Mixed Access Levels](../../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-a-property-with-mixed-access-levels.md).  
  
## Dichiarazione dei parametri  
 Ciascun parametro viene dichiarato mediante la stessa procedura utilizzata per [Sub Procedures](../../../../visual-basic/programming-guide/language-features/procedures/sub-procedures.md), a eccezione del fatto che è necessario che il meccanismo di passaggio sia `ByVal`.  
  
 La sintassi per ciascun parametro dell'elenco dei parametri è la seguente:  
  
 `[Optional] ByVal [ParamArray] parametername As datatype`  
  
 Se il parametro è facoltativo, è necessario specificare nella dichiarazione anche un valore predefinito.  La sintassi per la specifica di un valore predefinito è la seguente:  
  
 `Optional ByVal parametername As datatype = defaultvalue`  
  
## Valore proprietà  
 In una routine `Get` il valore restituito viene fornito all'espressione chiamante come valore della proprietà.  
  
 In una routine `Set` il nuovo valore della proprietà viene passato al parametro dell'istruzione `Set`.  Se si dichiara esplicitamente un parametro, è necessario dichiararlo con lo stesso tipo di dati della proprietà.  Se nessun parametro viene dichiarato, viene utilizzato il parametro implicito `Value` per rappresentare il nuovo valore da assegnare alla proprietà.  
  
## Sintassi di chiamata  
 Si richiama implicitamente una routine della proprietà facendo riferimento alla proprietà.  Il nome della proprietà viene utilizzato come se utilizzasse il nome di una variabile. L'unica differenza consiste nel fatto che è necessario fornire valori per tutti gli argomenti non facoltativi e racchiudere tra parentesi l'elenco degli argomenti.  Se non viene specificato alcun argomento, è anche possibile omettere le parentesi.  
  
 La sintassi per una chiamata implicita a una routine `Set` è la seguente:  
  
 `propertyname[(argumentlist)] = expression`  
  
 La sintassi per una chiamata implicita a una routine `Get` è la seguente:  
  
 `lvalue = propertyname[(argumentlist)]`  
  
 `Do While (propertyname[(argumentlist)] > expression)`  
  
### Illustrazione della dichiarazione e della chiamata  
 La proprietà riportata di seguito memorizza un nome completo come due nomi costitutivi, ovvero il nome e il cognome.  Quando il codice chiamante legge  `fullName`, la routine `Get` combina i due nomi costitutivi e restituisce il nome completo.  Quando il codice chiamante assegna un nuovo nome completo, la routine `Set` tenta di scomporlo in due parti costitutive.  Se non viene rilevato alcuno spazio, viene memorizzato tutto come nome.  
  
 [!code-vb[VbVbcnProcedures#8](./codesnippet/VisualBasic/property-procedures_1.vb)]  
  
 Nell'esempio riportato di seguito vengono illustrate le chiamate tipiche alle routine delle proprietà di `fullName`.  
  
 [!code-vb[VbVbcnProcedures#9](./codesnippet/VisualBasic/property-procedures_2.vb)]  
  
## Vedere anche  
 [Procedures](../../../../visual-basic/programming-guide/language-features/procedures/index.md)   
 [Routine Function](../../../../visual-basic/programming-guide/language-features/procedures/function-procedures.md)   
 [Operator Procedures](../../../../visual-basic/programming-guide/language-features/procedures/operator-procedures.md)   
 [Procedure Parameters and Arguments](../../../../visual-basic/programming-guide/language-features/procedures/procedure-parameters-and-arguments.md)   
 [Differences Between Properties and Variables in Visual Basic](../../../../visual-basic/programming-guide/language-features/procedures/differences-between-properties-and-variables.md)   
 [How to: Create a Property](../../../../visual-basic/programming-guide/language-features/procedures/how-to-create-a-property.md)   
 [How to: Call a Property Procedure](../../../../visual-basic/programming-guide/language-features/procedures/how-to-call-a-property-procedure.md)   
 [How to: Declare and Call a Default Property in Visual Basic](../../../../visual-basic/programming-guide/language-features/procedures/how-to-declare-and-call-a-default-property.md)   
 [How to: Put a Value in a Property](../../../../visual-basic/programming-guide/language-features/procedures/how-to-put-a-value-in-a-property.md)   
 [How to: Get a Value from a Property](../../../../visual-basic/programming-guide/language-features/procedures/how-to-get-a-value-from-a-property.md)