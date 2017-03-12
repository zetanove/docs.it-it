---
title: "Static (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.Static"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "static modifier"
  - "Static keyword"
ms.assetid: 19013910-4658-47b6-a22e-1744b527979e
caps.latest.revision: 22
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 22
---
# Static (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Specifica che una o più variabili locali dichiarate restano valide e conservano i valori più recenti dopo il termine della routine nella quale vengono dichiarate.  
  
## Note  
 Di norma, l'esistenza di una variabile locale in una routine termina insieme alla routine stessa.  Una variabile statica resta valida e conserva il valore più recente.  Alla successiva chiamata della routine da parte del codice, la variabile non viene reinizializzata e contiene ancora il valore più recente a essa assegnato.  Una variabile statica continua a esistere per la durata della classe o del modulo in cui è definita.  
  
## Regole  
  
-   **Contesto della dichiarazione.** È possibile utilizzare `Static` solo per variabili locali.  In altri termini, il contesto della dichiarazione per una variabile `Static` deve essere una routine o un blocco in una routine e non può essere un file di origine, uno spazio dei nomi, una classe, una struttura o un modulo.  
  
     Non è possibile utilizzare `Static` all'interno di una routine di struttura.  
  
-   Non è possibile dedurre i tipi di dati delle variabili locali `Static`.  Per ulteriori informazioni, vedere [Local Type Inference](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md).  
  
-   **Modificatori combinati.** Non è possibile specificare `Static` insieme a `ReadOnly`, `Shadows` o `Shared` nella stessa dichiarazione.  
  
## Comportamento  
 Quando si dichiara una variabile statica in una routine di `Shared` , una sola copia della variabile statica è disponibile per l'intera applicazione.  Chiama una routine di `Shared` utilizzando il nome della classe, non una variabile che punti a un'istanza della classe.  
  
 Quando si dichiara una variabile statica in una routine che non è `Shared`, una sola copia della variabile è disponibile per ogni istanza della classe.  Chiama una routine non condivisa tramite una variabile che punta a un'istanza specifica della classe.  
  
## Esempio  
 Nell'esempio seguente viene illustrato l'utilizzo di `Static`.  
  
 [!code-vb[VbVbalrKeywords#5](../../../visual-basic/language-reference/codesnippet/visualbasic/static_1.vb)]  
  
 La variabile `Static` `totalSales` viene inizializzata su 0 una sola volta.  Ogni volta che si accede a `updateSales`, in `totalSales` è presente il valore calcolato più recente.  
  
 È possibile utilizzare il modificatore `Static` nel seguente contesto:  
  
 [Dim Statement](../../../visual-basic/language-reference/statements/dim-statement.md)  
  
## Vedere anche  
 [Shadows](../../../visual-basic/language-reference/modifiers/shadows.md)   
 [Shared](../../../visual-basic/language-reference/modifiers/shared.md)   
 [Lifetime in Visual Basic](../../../visual-basic/programming-guide/language-features/declared-elements/lifetime.md)   
 [Dichiarazione di variabili](../../../visual-basic/programming-guide/language-features/variables/variable-declaration.md)   
 [Structures](../../../visual-basic/programming-guide/language-features/data-types/structures.md)   
 [Local Type Inference](../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [Objects and Classes](../../../visual-basic/programming-guide/language-features/objects-and-classes/index.md)