---
title: "With...End With Statement (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.With"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "With keyword"
  - "loop structures, and With...End With statements"
  - "execution, on object"
  - "instructions, repeating"
  - "With...End With statements"
  - "With statement"
  - "With statement, nesting"
  - "objects [Visual Basic], accessing"
  - "With block"
  - "End keyword, With...End With statements"
ms.assetid: 340d5fbb-4f43-48ec-a024-80843c137817
caps.latest.revision: 34
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 34
---
# With...End With Statement (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Esegue una serie di istruzioni che fanno riferimento più volte a un singolo oggetto o struttura in modo da poter utilizzare una sintassi semplificata per le istruzioni quando si accede ai membri dell'oggetto o della struttura.  Quando si utilizza una struttura, è possibile leggere solo i valori dei membri o i metodi invoke e ottenere un errore se si tenta di assegnare valori ai membri di una struttura utilizzata in un'istruzione `With...End With`.  
  
## Sintassi  
  
```  
With objectExpression  
    [ statements ]  
End With  
```  
  
## Parti  
  
|||  
|-|-|  
|Termine|Definizione|  
|`objectExpression`|Obbligatorio.  Espressione che restituisce un oggetto.  L'espressione può essere arbitrariamente complessa ed essere valutata solo una volta.  Può restituire qualsiasi tipo di dati, compresi i tipi di base.|  
|`statements`|Facoltativa.  Una o più istruzioni tra `With` e `End With` che possono fare riferimento ai membri di un oggetto che verrà prodotto dalla valutazione di `objectExpression`.|  
|`End With`|Obbligatorio.  Termina la definizione del blocco `With`.|  
  
## Note  
 Utilizzando `With...End With`, è possibile eseguire una serie di istruzioni in un oggetto specificato senza specificare il nome dell'oggetto più volte.  All'interno di un blocco di istruzioni `With`, è possibile specificare un membro dell'oggetto che inizia con un punto, come se l'oggetto dell'istruzione `With` lo precedesse.  
  
 Per modificare più proprietà in un singolo oggetto, ad esempio, è possibile inserire le istruzioni di assegnazione delle proprietà all'interno del blocco `With...End With`, facendo riferimento all'oggetto una sola volta anziché una volta per assegnazione di proprietà.  
  
 Se il codice accede allo stesso oggetto in più istruzioni, utilizzando l'istruzione di `With` si ottengono i vantaggi seguenti:  
  
-   Non è necessario valutare più volte un'espressione complessa o assegnare il risultato a una variabile temporanea per fare riferimento ai membri più volte.  
  
-   È possibile rendere il codice più leggibile eliminando le espressioni di qualificazione ripetitive.  
  
 Il tipo di dati `objectExpression` può essere qualsiasi tipo di classe o struttura o anche un tipo elementare di Visual Basic come `Integer`.  Se `objectExpression` restituisce qualcosa di diverso da un oggetto, è possibile leggere solo i valori dei membri o i metodi invoke e ottenere un errore se si tenta di assegnare valori ai membri di una struttura utilizzata in un'istruzione `With...End With`.  Si tratta dello stesso errore che si otterrebbe se viene richiamato un metodo che restituisce una struttura e immediatamente si accede e si assegna un valore a un membro del risultato della funzione, come `GetAPoint().x = 1`.  Il problema in entrambi i casi è che la struttura esiste solo nello stack di chiamate e in nessun caso un membro di una struttura modificata in tali situazioni può scrivere in una posizione in modo che altro codice del programma può osservare la modifica.  
  
 `objectExpression` viene valutato una volta, all'ingresso nel blocco.  Non è possibile riassegnare `objectExpression` dall'interno del blocco `With`.  
  
 Dal blocco `With`, è possibile accedere ai metodi e alle proprietà del solo oggetto specificato senza qualifica.  Metodi e proprietà di altri oggetti possono essere utilizzati ma è necessario qualificarli con i relativi nomi di oggetto.  
  
 È possibile inserire un'istruzione `With...End With` in un'altra.  Le istruzioni `With...End With` annidate possono creare confusione se gli oggetti a cui si fa riferimento non sono chiari dal contesto.  È necessario fornire un riferimento completo a un oggetto che si trova in un blocco `With` esterno quando si fa riferimento all'oggetto dal un blocco `With` interno.  
  
 Non è consentita la diramazione in un'istruzione `With` dall'esterno del blocco.  
  
 A meno che il blocco non contenga un ciclo, le istruzioni vengono eseguite una sola volta.  È possibile annidare tipi diversi di strutture di controllo.  Per ulteriori informazioni, vedere [Nested Control Structures](../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md).  
  
> [!NOTE]
>  È possibile utilizzare la parola chiave `With` anche negli inizializzatori di oggetto.  Per ulteriori informazioni ed esempi, vedere [Object Initializers: Named and Anonymous Types](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md) e [Anonymous Types](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md).  
>   
>  Se si utilizza un blocco `With` solo per inizializzare le proprietà o i campi di un oggetto di cui è stata appena creata un'istanza, è possibile utilizzare un inizializzatore di oggetto.  
  
## Esempio  
 Nell'esempio riportato di seguito, ogni blocco `With` esegue una serie di istruzioni su un singolo oggetto.  
  
 [!code-vb[VbVbalrWithStatement#2](../../../visual-basic/language-reference/statements/codesnippet/visualbasic/vbwpfapp/mainwindow.xaml.vb#2)]  
  
## Esempio  
 Nell'esempio seguente vengono annidate le istruzioni `With…End With`.  Nell'istruzione `With` annidata, la sintassi fa riferimento all'oggetto interno.  
  
 [!code-vb[VbVbalrWithStatement#1](../../../visual-basic/language-reference/statements/codesnippet/visualbasic/vbwpfapp/mainwindow.xaml.vb#1)]  
  
## Vedere anche  
 <xref:System.Collections.Generic.List%601>   
 [Nested Control Structures](../../../visual-basic/programming-guide/language-features/control-flow/nested-control-structures.md)   
 [Object Initializers: Named and Anonymous Types](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)   
 [Anonymous Types](../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)