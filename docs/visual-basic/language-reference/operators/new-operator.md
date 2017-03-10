---
title: "New Operator (Visual Basic) | Microsoft Docs"
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.new"
  - "vb.NewConstraint"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "constraints, Visual Basic generic types"
  - "generics [Visual Basic], constraints"
  - "constraints, New keyword"
  - "New constraint"
  - "New keyword"
ms.assetid: d7d566d7-fe0e-4336-91f7-641a542de4d0
caps.latest.revision: 23
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 23
---
# New Operator (Visual Basic)
[!INCLUDE[vs2017banner](../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Introduce una clausola `New` per creare una nuova istanza di oggetto, specifica un vincolo di costruttore su un parametro di tipo o identifica una routine `Sub` come costruttore di classe.  
  
## Note  
 In un'istruzione di assegnazione o per la dichiarazione una clausola `New` deve specificare una classe definita da cui sia possibile creare l'istanza.  In altre parole, la classe deve esporre uno o più costruttori a cui il codice chiamante possa accedere.  
  
 È possibile utilizzare una clausola `New` in un'istruzione di assegnazione o per la dichiarazione.  Quando l'istruzione viene eseguita, viene chiamato il costruttore appropriato della classe specificata e vengono passati gli argomenti forniti.  Nell'esempio seguente viene illustrato questo comportamento tramite la creazione di istanze di una classe `Customer` con due costruttori, uno che non accetta parametri e uno che accetta un parametro stringa.  
  
 [!code-vb[VbVbalrKeywords#11](../../../visual-basic/language-reference/codesnippet/visualbasic/new-operator_1.vb)]  
  
 Poiché le matrici sono classi, `New` consente di creare una nuova istanza di matrice, come illustrato negli esempi seguenti.  
  
 [!code-vb[VbVbalrKeywords#12](../../../visual-basic/language-reference/codesnippet/visualbasic/new-operator_2.vb)]  
  
 In Common Language Runtime viene generato un errore <xref:System.OutOfMemoryException> se la memoria è insufficiente per creare la nuova istanza.  
  
> [!NOTE]
>  La parola chiave `New` viene inoltre utilizzata negli elenchi di parametri di tipo per specificare che il tipo fornito deve esporre un costruttore senza parametri accessibile.  Per ulteriori informazioni su vincoli e parametri di tipo, vedere [Type List](../../../visual-basic/language-reference/statements/type-list.md).  
  
 Per creare una routine del costruttore per una classe, impostare il nome di una routine `Sub` sulla parola chiave `New`.  Per ulteriori informazioni, vedere [Object Lifetime: How Objects Are Created and Destroyed](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-lifetime-how-objects-are-created-and-destroyed.md).  
  
 È possibile utilizzare la parola chiave `New` nei seguenti contesti:  
  
 [Dim Statement](../../../visual-basic/language-reference/statements/dim-statement.md)  
  
 [Of](../../../visual-basic/language-reference/statements/of-clause.md)  
  
 [Sub Statement](../../../visual-basic/language-reference/statements/sub-statement.md)  
  
## Vedere anche  
 <xref:System.OutOfMemoryException>   
 [Parole chiave](../../../visual-basic/language-reference/keywords/index.md)   
 [Type List](../../../visual-basic/language-reference/statements/type-list.md)   
 [Tipi generici in Visual Basic](../../../visual-basic/programming-guide/language-features/data-types/generic-types.md)   
 [Object Lifetime: How Objects Are Created and Destroyed](../../../visual-basic/programming-guide/language-features/objects-and-classes/object-lifetime-how-objects-are-created-and-destroyed.md)