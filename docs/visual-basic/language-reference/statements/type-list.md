---
title: "Type List (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "12/08/2016"
ms.prod: "visual-studio-dev14"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "StructureConstraint"
  - "vb.StructureConstraint"
  - "ClassConstraint"
  - "vb.ClassConstraint"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "class constraint"
  - "constraints, Visual Basic generic types"
  - "generic parameters"
  - "generics [Visual Basic], constraints"
  - "generics [Visual Basic], type list"
  - "structure constraint"
  - "constraints, in type parameters"
  - "generics [Visual Basic], generic types"
  - "parameters, type"
  - "constraints, Structure keyword"
  - "type parameters, constraints"
  - "types [Visual Basic], generic"
  - "parameters, generic"
  - "generics [Visual Basic], type parameters"
  - "type parameters"
  - "constraints, Class keyword"
ms.assetid: 56db947a-2ae8-40f2-a70a-960764e9d0db
caps.latest.revision: 33
caps.handback.revision: 33
author: "stevehoag"
ms.author: "shoag"
manager: "wpickett"
---
# Type List (Visual Basic)
[!INCLUDE[vs2017banner](../../../csharp/includes/vs2017banner.md)]

Specifica i *parametri di tipo* per un elemento di programmazione *generico*.  Nel caso di più parametri, è possibile separarli mediante virgole.  Di seguito è riportata la sintassi di un parametro di tipo.  
  
## Sintassi  
  
```  
  
[genericmodifier] typename [ As constraintlist ]  
```  
  
## Parti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`genericmodifier`|Parametro facoltativo.  Può essere utilizzato solo in interfacce e delegati generici.  È possibile dichiarare una covariante del tipo utilizzando la parola chiave [Out](../../../visual-basic/language-reference/modifiers/out-generic-modifier.md) oppure una controvariante utilizzando la parola chiave [In](../../../visual-basic/language-reference/modifiers/in-generic-modifier.md).  Vedere [Covarianza e controvarianza](../Topic/Covariance%20and%20Contravariance%20\(C%23%20and%20Visual%20Basic\).md).|  
|`typename`|Obbligatorio.  Nome del parametro di tipo.  Si tratta di un segnaposto da sostituire con un tipo definito specificato dall'argomento di tipo corrispondente.|  
|`constraintlist`|Parametro facoltativo.  Elenco di requisiti che vincolano il tipo di dati che è possibile specificare per `typename`.  In presenza di più vincoli è possibile racchiuderli tra parentesi graffe \(`{ }`\) e separarli con virgole.  L'elenco dei vincoli deve essere introdotto dalla parola chiave [As](../../../visual-basic/language-reference/statements/as-clause.md).  `As` viene utilizzata una sola volta all'inizio dell'elenco.|  
  
## Note  
 Ogni elemento di programmazione generico deve accettare almeno un parametro di tipo.  Tale parametro è un segnaposto per uno specifico tipo, ossia un *elemento costruito*, specificato dal codice client al momento della creazione di un'istanza del tipo generico.  È possibile definire una classe, una struttura, un'interfaccia, una routine o un delegato generico.  
  
 Per ulteriori informazioni sul momento in cui definire un tipo generico, vedere [Tipi generici in Visual Basic](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md).  Per ulteriori informazioni sui nomi dei parametri di tipo, vedere [Declared Element Names](../../../visual-basic/programming-guide/language-features/declared-elements/declared-element-names.md).  
  
## Regole  
  
-   **Parentesi.** Se si specifica un elenco di parametri di tipo, è necessario racchiuderlo tra parentesi e farlo precedere dalla parola chiave [Of](../../../visual-basic/language-reference/statements/of-clause.md).  `Of` viene utilizzata una sola volta all'inizio dell'elenco.  
  
-   **Vincoli.** Un elenco di *vincoli* definiti su un parametro di tipo può includere qualsiasi combinazione dei seguenti elementi:  
  
    -   Un numero qualsiasi di interfacce.  Il tipo specificato deve implementare ogni interfaccia dell'elenco.  
  
    -   Al massimo una classe.  Il tipo specificato deve ereditare da tale classe.  
  
    -   Parola chiave `New`.  Il tipo specificato deve esporre un costruttore senza parametri a cui possa accedere il tipo generico.  Questa caratteristica risulta utile se si vincola un parametro di tipo tramite una o più interfacce.  Un tipo che implementa interfacce non espone necessariamente un costruttore. A seconda del livello di accesso del costruttore, è pertanto possibile che il codice all'interno del tipo generico non sia in grado di accedere a tale costruttore.  
  
    -   La parola chiave `Class` o `Structure`.  La parola chiave `Class` vincola un parametro di tipo generico forzandolo a richiedere che qualsiasi argomento di tipo passato sia un tipo di riferimento, ad esempio una stringa, una matrice, un delegato o un oggetto creato da una classe.  La parola chiave `Structure` vincola un parametro di tipo generico forzandolo a richiedere che qualsiasi argomento di tipo passato sia un tipo di valore, ad esempio una struttura, un'enumerazione o un tipo di dati elementare.  Non è possibile includere `Class` e `Structure` nella stessa parte `constraintlist`.  
  
     Il tipo specificato deve soddisfare tutti i requisiti inclusi in `constraintlist`.  
  
     I vincoli definiti su ciascun parametro di tipo sono indipendenti da quelli definiti sugli altri parametri di tipo.  
  
## Comportamento  
  
-   **Sostituzione in fase di compilazione.** Quando si crea un tipo costruito da un elemento di programmazione generico, viene specificato un tipo definito per ciascun parametro di tipo.  Il compilatore Visual Basic sostituisce il tipo specificato per ogni ricorrenza di `typename` all'interno dell'elemento generico.  
  
-   **Assenza di vincoli.** Se non si specifica alcun vincolo su un parametro di tipo, il codice è limitato alle operazioni e ai membri supportati dal [Object Data Type](../../../visual-basic/language-reference/data-types/object-data-type.md) per tale parametro.  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrata la definizione di base di una classe dizionario generica, che comprende una funzione di base per l'aggiunta di una nuova voce al dizionario.  
  
 [!code-vb[VbVbalrStatements#3](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/type-list_1.vb)]  
  
## Esempio  
 Poiché `dictionary` è generico, il codice che lo utilizza può creare a partire da tale elemento una vasta gamma di oggetti, ciascuno con le stesse funzionalità ma con effetto su tipi di dati diversi.  Nell'esempio riportato di seguito viene illustrata una riga di codice che crea un oggetto `dictionary` con voci `String` e chiavi `Integer`.  
  
 [!code-vb[VbVbalrStatements#4](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/type-list_2.vb)]  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrata la definizione di base equivalente generata dall'esempio precedente.  
  
 [!code-vb[VbVbalrStatements#5](../../../visual-basic/language-reference/error-messages/codesnippet/VisualBasic/type-list_3.vb)]  
  
## Vedere anche  
 [Of](../../../visual-basic/language-reference/statements/of-clause.md)   
 [New Operator](../../../visual-basic/language-reference/operators/new-operator.md)   
 [Access Levels in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/access-levels.md)   
 [Object Data Type](../../../visual-basic/language-reference/data-types/object-data-type.md)   
 [Function Statement](../../../visual-basic/language-reference/statements/function-statement.md)   
 [Structure Statement](../../../visual-basic/language-reference/statements/structure-statement.md)   
 [Sub Statement](../../../visual-basic/language-reference/statements/sub-statement.md)   
 [Procedura: utilizzare una classe generica](../../../visual-basic/programming-guide/language-features/data-types/how-to-use-a-generic-class.md)   
 [Covarianza e controvarianza](../Topic/Covariance%20and%20Contravariance%20\(C%23%20and%20Visual%20Basic\).md)   
 [In](../../../visual-basic/language-reference/modifiers/in-generic-modifier.md)   
 [Out](../../../visual-basic/language-reference/modifiers/out-generic-modifier.md)