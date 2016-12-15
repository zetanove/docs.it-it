---
title: "Get Statement | Microsoft Docs"
ms.custom: ""
ms.date: "12/05/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "vb.Get"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "Get statement, syntax"
  - "Get statement"
  - "properties [Visual Basic], read-only"
  - "read-only properties"
  - "Get keyword"
  - "property procedures, Get statements"
ms.assetid: 56b05cdc-bd64-4dfd-bb12-824eacec6f94
caps.latest.revision: 19
caps.handback.revision: 19
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Get Statement
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Consente di dichiarare una routine di proprietà `Get` utilizzata per recuperare il valore di una proprietà.  
  
## Sintassi  
  
```  
[ <attributelist> ] [ accessmodifier ] Get()  
    [ statements ]  
End Get  
```  
  
## Parti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`attributelist`|Parametro facoltativo.  Vedere [Elenco degli attributi](../../../visual-basic/language-reference/statements/attribute-list.md).|  
|`accessmodifier`|Facoltativo per al massimo una delle istruzioni `Get` e `Set` in questa proprietà e può essere  ad esempio uno dei seguenti:<br /><br /> -   [Protected](../../../visual-basic/language-reference/modifiers/protected.md)<br />-   [Friend](../../../visual-basic/language-reference/modifiers/friend.md)<br />-   [Private](../../../visual-basic/language-reference/modifiers/private.md)<br />-   `Protected Friend`<br /><br /> Vedere [Access Levels in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md).|  
|`statements`|Parametro facoltativo.  Una o più istruzioni eseguite quando viene chiamata la routine di proprietà `Get`.|  
|`End Get`|Obbligatorio.  Consente di terminare la definizione della routine di proprietà `Get`.|  
  
## Note  
 Per ogni proprietà deve esistere una routine di proprietà `Get` a meno che la proprietà non sia contrassegnata come `WriteOnly`.  La routine `Get` viene utilizzata per ottenere il valore corrente della proprietà.  
  
 In Visual Basic viene automaticamente chiamata la routine `Get` di una proprietà quando un'espressione richiede il valore della proprietà.  
  
 All'interno del corpo della dichiarazione di proprietà possono essere contenute solo le routine `Get` e `Set` della proprietà fra le istruzioni [Property Statement](../../../visual-basic/language-reference/statements/property-statement.md) e `End Property`.  Non è possibile memorizzare altro all'infuori di queste routine.  In particolare, non è possibile memorizzare il valore corrente della proprietà.  Questo valore va memorizzarlo al di fuori della proprietà. Se lo si inserisce all'interno di una delle routine infatti, l'altra non potrà accedervi.  In genere questo valore viene memorizzato in una variabile [Private](../../../visual-basic/language-reference/modifiers/private.md) dichiarata allo stesso livello della proprietà.  Una routine `Get` deve essere definita all'interno della proprietà a cui si riferisce.  
  
 La routine `Get` assume per impostazione predefinita il livello di accesso della proprietà che la contiene, a meno che non si utilizzi il parametro `accessmodifier` nell'istruzione `Get`.  
  
## Regole  
  
-   **Livelli di accesso misto.** Se si definisce una proprietà di lettura\/scrittura, è eventualmente possibile specificare un livello di accesso diverso per la routine `Get` o `Set`, ma non per entrambe.  Il livello di accesso della routine deve essere più restrittivo rispetto a quello della proprietà.  Se ad esempio la proprietà è dichiarata `Friend`, la routine `Get` può essere dichiarata `Private`, ma non `Public`.  
  
     Se si sta definendo una proprietà `ReadOnly`, la routine `Get` rappresenta l'intera proprietà.  Non è possibile dichiarare un livello di accesso diverso per `Get` in quanto altrimenti per la proprietà verrebbero specificati due livelli di accesso.  
  
-   **Tipo restituito.** L'[Property Statement](../../../visual-basic/language-reference/statements/property-statement.md) può dichiarare il tipo di dati del valore restituito.  La routine `Get` restituisce automaticamente quel tipo di dati.  È possibile specificare qualsiasi tipo di dati o il nome di un'enumerazione, struttura, classe o interfaccia.  
  
     Se nell'istruzione `Property` non è specificato `returntype`, la routine restituisce `Object`.  
  
## Comportamento  
  
-   **Chiusura di una routine.** Quando la routine `Get` torna al codice chiamante, l'esecuzione continua all'interno dell'istruzione che ha richiesto il valore della proprietà.  
  
     Le routine di proprietà `Get` possono restituire un valore utilizzando l'[Return Statement](../../../visual-basic/language-reference/statements/return-statement.md) oppure assegnando il valore restituito al nome della proprietà.  Per ulteriori informazioni, vedere "Valore restituito" in [Function Statement](../../../visual-basic/language-reference/statements/function-statement.md).  
  
     Le istruzioni `Exit Property` e `Return` consentono di uscire immediatamente da una routine di proprietà.  Qualsiasi numero delle istruzioni `Exit Property` e `Return` può essere visualizzato in un punto qualsiasi della procedura ed è possibile mescolare le istruzioni `Exit Property` e `Return`.  
  
-   **Valore restituito.** Per ottenere un valore da una routine `Get` è possibile assegnare il valore al nome della proprietà oppure includerlo in un'[Return Statement](../../../visual-basic/language-reference/statements/return-statement.md).  L'istruzione `Return` assegna il valore restituito della routine `Get` e contemporaneamente consente di uscire dalla routine.  
  
     Se si utilizza l'istruzione `Exit Property` senza assegnare un valore al nome della proprietà, la routine `Get` restituisce il valore predefinito per il tipo di dati della proprietà.  Per ulteriori informazioni, vedere "Valore restituito" in [Function Statement](../../../visual-basic/language-reference/statements/function-statement.md).  
  
     Nell'esempio seguente sono illustrati due metodi che consentono alla proprietà di sola lettura `quoteForTheDay` di restituire il valore contenuto nella variabile privata `quoteValue`.  
  
     [!code-vb[VbVbalrStatements#27](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/get-statement_1.vb)]  
  
     [!code-vb[VbVbalrStatements#28](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/get-statement_2.vb)]  
  
     [!code-vb[VbVbalrStatements#29](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/get-statement_3.vb)]  
  
## Esempio  
 Nell'esempio seguente l'istruzione `Get` viene utilizzata per restituire il valore di una proprietà.  
  
 [!code-vb[VbVbalrStatements#30](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/get-statement_4.vb)]  
  
## Vedere anche  
 [Set Statement](../../../visual-basic/language-reference/statements/set-statement.md)   
 [Property Statement](../../../visual-basic/language-reference/statements/property-statement.md)   
 [Exit Statement](../../../visual-basic/language-reference/statements/exit-statement.md)   
 [Objects and Classes](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)   
 [Walkthrough: Defining Classes](../../../visual-basic/programming-guide/language-features/objects-and-classes/walkthrough-defining-classes.md)