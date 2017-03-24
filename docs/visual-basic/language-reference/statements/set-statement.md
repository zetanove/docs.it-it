---
title: "Set Statement (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Set"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "property procedures, Set statements"
  - "Set statement"
  - "Set statement, syntax"
  - "write-only properties"
  - "properties [Visual Basic], write-only"
ms.assetid: 9ecc27b4-df84-420d-9075-db25455fb3cd
caps.latest.revision: 16
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 16
---
# Set Statement (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Consente di dichiarare una routine della proprietà `Set` utilizzata per assegnare un valore a una proprietà.  
  
## Sintassi  
  
```  
[ <attributelist> ] [ accessmodifier ] Set (ByVal value [ As datatype ])  
    [ statements ]  
End Set  
```  
  
## Parti  
 `attributelist`  
 Parametro facoltativo.  Vedere [Elenco degli attributi](../../../visual-basic/language-reference/statements/attribute-list.md).  
  
 `accessmodifier`  
 Facoltativo per al massimo una delle istruzioni `Get` e `Set` in questa proprietà e può essere  ad esempio uno dei seguenti:  
  
-   [Protected](../../../visual-basic/language-reference/modifiers/protected.md)  
  
-   [Friend](../../../visual-basic/language-reference/modifiers/friend.md)  
  
-   [Private](../../../visual-basic/language-reference/modifiers/private.md)  
  
-   `Protected Friend`  
  
 Vedere [Access Levels in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md).  
  
 `value`  
 Obbligatorio.  Parametro contenente il nuovo valore della proprietà.  
  
 `datatype`  
 Obbligatoria se `Option Strict` è `On`.  Tipo di dati del parametro `value`.  È necessario che sia uguale al tipo di dati della proprietà nella quale viene dichiarata l'istruzione `Set`.  
  
 `statements`  
 Parametro facoltativo.  Una o più istruzioni che vengono eseguite quando viene chiamata la routine della proprietà `Set`.  
  
 `End Set`  
 Obbligatorio.  Consente di terminare la definizione della routine della proprietà `Set`.  
  
## Note  
 Ogni proprietà deve avere una routine della proprietà `Set` a meno che la proprietà stessa non sia contrassegnata come `ReadOnly`.  La routine `Set` viene utilizzata per impostare il valore della proprietà.  
  
 Quando un'istruzione di assegnazione fornisce un valore da memorizzare nella proprietà, in Visual Basic viene automaticamente chiamata la routine `Set` della proprietà.  
  
 In Visual Basic un parametro viene passato alla routine `Set` durante le assegnazioni di proprietà.  Se non si fornisce un parametro per `Set`, un parametro implicito denominato `value` verrà utilizzato dall'ambiente di sviluppo integrato.  Il parametro contiene il valore da assegnare alla proprietà.  In genere tale valore viene memorizzato in una variabile locale privata e viene restituito ogni volta che viene chiamata la routine `Get`.  
  
 All'interno del corpo della dichiarazione di proprietà possono essere contenute solo le routine `Get` e `Set` della proprietà fra le istruzioni [Property Statement](../../../visual-basic/language-reference/statements/property-statement.md) e `End Property`.  Non è possibile memorizzare altro all'infuori di queste routine.  In particolare, non è possibile memorizzare il valore corrente della proprietà.  Questo valore va memorizzarlo al di fuori della proprietà. Se lo si inserisce all'interno di una delle routine infatti, l'altra non potrà accedervi.  In genere questo valore viene memorizzato in una variabile [Private](../../../visual-basic/language-reference/modifiers/private.md) dichiarata allo stesso livello della proprietà.  È necessario definire una routine `Set` all'interno della proprietà a cui viene applicata.  
  
 Per impostazione predefinita, la routine `Set` utilizza il livello di accesso della proprietà che la contiene a meno che non si utilizzi `accessmodifier` nell'istruzione `Set`.  
  
## Regole  
  
-   **Livelli di accesso misto.** Se si definisce una proprietà di lettura\/scrittura, è eventualmente possibile specificare un livello di accesso diverso per la routine `Get` o `Set`, ma non per entrambe.  Il livello di accesso della routine deve essere più restrittivo rispetto a quello della proprietà.  Ad esempio, se la proprietà è dichiarata `Friend`, è possibile dichiarare la procedura `Set` come `Private`, ma non come `Public`.  
  
     Se si definisce una proprietà `WriteOnly`, la routine `Set` rappresenta l'intera proprietà.  Non è possibile dichiarare un livello di accesso diverso per `Set`, poiché in tal caso verrebbero impostati due livelli di accesso per la proprietà.  
  
## Comportamento  
  
-   **Chiusura di una routine della proprietà.** Quando la routine `Set` torna al codice chiamante, l'esecuzione continua seguendo l'istruzione che ha fornito il valore da archiviare.  
  
     Le routine della proprietà `Set` possono essere chiuse tramite [Return Statement](../../../visual-basic/language-reference/statements/return-statement.md) o [Exit Statement](../../../visual-basic/language-reference/statements/exit-statement.md).  
  
     Le istruzioni `Exit Property` e `Return` consentono di uscire immediatamente da una routine di proprietà.  Qualsiasi numero delle istruzioni `Exit Property` e `Return` può essere visualizzato in un punto qualsiasi della procedura ed è possibile mescolare le istruzioni `Exit Property` e `Return`.  
  
## Esempio  
 Nell'esempio seguente l'istruzione `Set` viene utilizzata per impostare il valore di una proprietà.  
  
 [!code-vb[VbVbalrStatements#55](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/set-statement_1.vb)]  
  
## Vedere anche  
 [Get Statement](../../../visual-basic/language-reference/statements/get-statement.md)   
 [Property Statement](../../../visual-basic/language-reference/statements/property-statement.md)   
 [Sub Statement](../../../visual-basic/language-reference/statements/sub-statement.md)   
 [Routine Property](../../../visual-basic/programming-guide/language-features/procedures/property-procedures.md)