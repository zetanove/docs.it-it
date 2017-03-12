---
title: "Parameter List (Visual Basic) | Microsoft Docs"
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
  - "Visual Basic code, procedures"
  - "parameters, Visual Basic"
  - "parameters, lists"
  - "parameter lists"
  - "Visual Basic code, parameter lists"
  - "arguments [Visual Basic], Visual Basic"
  - "procedures, parameter lists"
ms.assetid: 5d737319-0c34-4df9-a23d-188fc840becd
caps.latest.revision: 19
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 19
---
# Parameter List (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Specifica i parametri previsti quando viene chiamata una routine.  Nel caso di più parametri, è possibile separarli mediante virgole.  Di seguito è riportata la sintassi per un parametro.  
  
## Sintassi  
  
```  
[ <attributelist> ] [ Optional ] [{ ByVal | ByRef }] [ ParamArray ]   
parametername[( )] [ As parametertype ] [ = defaultvalue ]  
```  
  
## Parti  
 `attributelist`  
 Parametro facoltativo.  Elenco di attributi applicabili al parametro.  È necessario racchiudere l'[Attribute List](../../../visual-basic/language-reference/statements/attribute-list.md) tra parentesi angolari \("`<`" e "`>`"\).  
  
 `Optional`  
 Parametro facoltativo.  Specifica che il parametro non è obbligatorio quando viene chiamata la routine.  
  
 `ByVal`  
 Parametro facoltativo.  Specifica che alla routine non è consentito sostituire o riassegnare l'elemento variabile sottostante all'argomento corrispondente nel codice chiamante.  
  
 `ByRef`  
 Parametro facoltativo.  Specifica che alla routine è consentito modificare la variabile sottostante nel codice chiamante, analogamente a quanto consentito al codice chiamante stesso.  
  
 `ParamArray`  
 Parametro facoltativo.  Specifica che l'ultimo parametro dell'elenco di parametri è una matrice facoltativa di elementi del tipo di dati specificato.  Ciò consente al codice chiamante di passare alla routine un numero arbitrario di argomenti.  
  
 `parametername`  
 Obbligatorio.  Nome della variabile locale che rappresenta il parametro.  
  
 `parametertype`  
 Obbligatoria se `Option Strict` è `On`.  Tipo di dati della variabile locale che rappresenta il parametro.  
  
 `defaultvalue`  
 Obbligatoria per i parametri `Optional`.  Qualsiasi costante o espressione costante che restituisce il tipo di dati del parametro.  Se il tipo è `Object` oppure una classe, un'interfaccia, una matrice o una struttura, il valore predefinito potrà essere solo `Nothing`.  
  
## Note  
 I parametri sono racchiusi tra parentesi e separati da una virgola.  Un parametro può essere dichiarato con qualsiasi tipo di dati.  Se non si specifica la parte `parametertype`, verrà utilizzato il valore predefinito `Object`.  
  
 Quando chiama la routine, il codice chiamante passa un *argomento* a ciascun parametro obbligatorio.  Per ulteriori informazioni, vedere [Differences Between Parameters and Arguments](../../../visual-basic/programming-guide/language-features/procedures/differences-between-parameters-and-arguments.md).  
  
 L'argomento passato dal codice chiamante a ciascun parametro costituisce un puntatore a un elemento sottostante nel codice chiamante.  Se tale elemento è *non variabile*, ovvero una costante, un valore letterale, un'enumerazione o un'espressione, nessun codice sarà in grado di modificarlo.  Se si tratta di un elemento *variabile*, ovvero una variabile, un campo, una proprietà, un elemento di matrice o un elemento di struttura dichiarato, il codice chiamante potrà modificarlo.  Per ulteriori informazioni, vedere [Differences Between Modifiable and Nonmodifiable Arguments](../../../visual-basic/programming-guide/language-features/procedures/differences-between-modifiable-and-nonmodifiable-arguments.md).  
  
 La routine potrà modificare anche un elemento variabile `ByRef` passato.  Per ulteriori informazioni, vedere [Differences Between Passing an Argument By Value and By Reference](../../../visual-basic/programming-guide/language-features/procedures/differences-between-passing-an-argument-by-value-and-by-reference.md).  
  
## Regole  
  
-   **Parentesi.** Quando si specifica un elenco di parametri, è necessario racchiuderlo tra parentesi.  Se non sono presenti parametri, l'utilizzo delle parentesi per racchiudere un elenco vuoto  rende comunque più leggibile il codice in quanto indica che l'elemento è una routine.  
  
-   **Parametri facoltativi.** Se si utilizza il modificatore `Optional` su un parametro, anche tutti i parametri successivi dell'elenco devono essere facoltativi e dichiarati utilizzando il modificatore `Optional`.  
  
     È necessario che in tutte le dichiarazioni di parametri facoltativi sia specificata la clausola `defaultvalue`.  
  
     Per ulteriori informazioni, vedere [Optional Parameters](../../../visual-basic/programming-guide/language-features/procedures/optional-parameters.md).  
  
-   **Matrici di parametri.** È necessario specificare `ByVal` per un parametro `ParamArray`.  
  
     Non è possibile utilizzare sia `Optional` che `ParamArray` nello stesso elenco di parametri.  
  
     Per ulteriori informazioni, vedere [Parameter Arrays](../../../visual-basic/programming-guide/language-features/procedures/parameter-arrays.md) .  
  
-   **Meccanismo di passaggio.** Il meccanismo predefinito per ciascun argomento è `ByVal`, che indica che la routine non può modificare l'elemento variabile sottostante.  Se l'elemento è un tipo di riferimento, la routine potrà tuttavia modificare il contenuto o i membri dell'oggetto sottostante, anche se non potrà sostituire o riassegnare l'oggetto stesso.  
  
-   **Nomi di parametri.** Se il tipo di dati del parametro è una matrice, inserire parentesi immediatamente dopo `parametername`.  Per ulteriori informazioni sui nomi dei parametri, vedere [Declared Element Names](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md).  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrata una routine `Function` che definisce due parametri.  
  
 [!code-vb[VbVbalrStatements#2](../../../visual-basic/language-reference/error-messages/codesnippet/visualbasic/parameter-list_1.vb)]  
  
## Vedere anche  
 <xref:System.Runtime.InteropServices.DllImportAttribute>   
 [Function Statement](../../../visual-basic/language-reference/statements/function-statement.md)   
 [Sub Statement](../../../visual-basic/language-reference/statements/sub-statement.md)   
 [Declare Statement](../../../visual-basic/language-reference/statements/declare-statement.md)   
 [Structure Statement](../../../visual-basic/language-reference/statements/structure-statement.md)   
 [Option Strict Statement](../../../visual-basic/language-reference/statements/option-strict-statement.md)   
 [Attributi](../Topic/Attributes%20\(C%23%20and%20Visual%20Basic\).md)   
 [Procedura: Interrompere e combinare istruzioni nel codice](../../../visual-basic/programming-guide/program-structure/how-to-break-and-combine-statements-in-code.md)