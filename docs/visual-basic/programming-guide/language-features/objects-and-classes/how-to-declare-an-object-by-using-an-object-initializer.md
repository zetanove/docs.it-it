---
title: "How to: Declare an Object by Using an Object Initializer (Visual Basic) | Microsoft Docs"
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
  - "declaring objects using object initializer"
  - "object initializers [Visual Basic]"
  - "initializers [Visual Basic]"
  - "Video How tos, Visual Basic"
ms.assetid: 0f53a553-efd6-466d-80bf-6b679e5cd174
caps.latest.revision: 20
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 20
---
# How to: Declare an Object by Using an Object Initializer (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Gli inizializzatori di oggetto consentono di dichiarare e creare un'istanza di un'istanza di una classe in una sola istruzione.  Inoltre è possibile inizializzare contemporaneamente uno o più membri dell'istanza senza richiamare un costruttore con parametri.  
  
 Quando si utilizza un inizializzatore di oggetto per creare un'istanza di un tipo denominato, viene chiamato il costruttore predefinito per la classe, seguito dall'inizializzazione dei membri designati nell'ordine specificato.  
  
 Nella procedura riportata di seguito viene illustrato come creare un'istanza di una classe `Student` in tre modi diversi.  Ad esempio, la classe ha un nome, un cognome e le proprietà dell'anno della classe.  Ognuna delle tre dichiarazioni crea una nuova istanza di `Student`, con proprietà `First` impostata su "Michael", proprietà `Last` impostata su "Tucker" e tutti gli altri membri impostati sui valori predefiniti.  Il risultato di ogni dichiarazione nella routine è equivalente all'esempio seguente, che non utilizza un inizializzatore di oggetto.  
  
 [!code-vb[VbVbalrObjectInit#20](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/how-to-declare-an-object-by-using-an-object-initializer_1.vb)]  
  
 Per l'implementazione della classe `Student`, vedere [How to: Create a List of Items](../../../../visual-basic/programming-guide/concepts/linq/how-to-create-a-list-of-items.md).  È possibile copiare il codice da quell'argomento per configurare la classe e creare un elenco di oggetti `Student` da utilizzare.  
  
### Per creare un oggetto di una classe denominata utilizzando un inizializzatore di oggetto  
  
1.  Iniziare la dichiarazione come se si intendesse utilizzare un costruttore.  
  
     `Dim student1 As New Student`  
  
2.  Digitare la parola chiave `With`, seguita da un elenco di inizializzazione tra parentesi graffe.  
  
     `Dim student1 As New Student With { <initialization list> }`  
  
3.  Nell'elenco di inizializzazione, includere ogni proprietà che si desidera inizializzare e assegnarle un valore iniziale.  Il nome della proprietà è preceduto da un punto.  
  
     [!code-vb[VbVbalrObjectInit#21](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/how-to-declare-an-object-by-using-an-object-initializer_2.vb)]  
  
     È possibile inizializzare uno o più membri della classe:  
  
4.  In alternativa, è possibile dichiarare una nuova istanza della classe e quindi assegnarle un valore.  Dichiarare innanzitutto un'istanza di `Student`:  
  
     `Dim student2 As Student`  
  
5.  Iniziare la creazione di un'istanza di `Student` nel modo normale.  
  
     `Dim student2 As Student = New Student`  
  
6.  Digitare `With` e quindi un inizializzatore di oggetto per inizializzare uno o più membri della nuova istanza.  
  
     [!code-vb[VbVbalrObjectInit#22](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/how-to-declare-an-object-by-using-an-object-initializer_3.vb)]  
  
7.  È possibile semplificare la definizione nel precedente passaggio omettendo `As Student`.  Se si procede in questa modo, il compilatore determina che `student3` è un'istanza di `Student` utilizzando l'inferenza del tipo di variabile locale.  
  
     [!code-vb[VbVbalrObjectInit#23](../../../../visual-basic/programming-guide/language-features/objects-and-classes/codesnippet/VisualBasic/how-to-declare-an-object-by-using-an-object-initializer_4.vb)]  
  
     Per ulteriori informazioni, vedere [Local Type Inference](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md).  
  
## Vedere anche  
 [Local Type Inference](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [How to: Create a List of Items](../../../../visual-basic/programming-guide/concepts/linq/how-to-create-a-list-of-items.md)   
 [Object Initializers: Named and Anonymous Types](../../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)   
 [Anonymous Types](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)