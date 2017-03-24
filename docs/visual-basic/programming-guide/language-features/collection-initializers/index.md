---
title: "Collection Initializers (Visual Basic) | Microsoft Docs"
ms.custom: ""
ms.date: "2015-07-20"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "devlang-visual-basic"
ms.topic: "article"
f1_keywords: 
  - "vb.CollectionInitializer"
dev_langs: 
  - "VB"
helpviewer_keywords: 
  - "collection initializers [Visual Basic]"
ms.assetid: a9290329-77b0-4fdf-ae75-8fc17287f469
caps.latest.revision: 23
author: "stevehoag"
ms.author: "shoag"
caps.handback.revision: 23
---
# Collection Initializers (Visual Basic)
[!INCLUDE[vs2017banner](../../../../visual-basic/developing-apps/includes/vs2017banner.md)]

Gli *inizializzatori di raccolta* forniscono una sintassi abbreviata che consente di creare una raccolta e di popolarla con un set iniziale di valori.  Gli inizializzatori di raccolta sono utili quando si crea una raccolta da un set di valori noti, ad esempio, un elenco di opzioni di menu o di categorie, un set iniziale di valori numerici, un elenco statico di stringhe quali nomi di giorno o di mese o località geografiche quale un elenco di stati utilizzato per la convalida.  
  
 Per ulteriori informazioni sugli insiemi, vedere [Raccolte](../Topic/Collections%20\(C%23%20and%20Visual%20Basic\).md).  
  
 Si identifica un inizializzatore di raccolta utilizzando la parola chiave `From` seguita da parentesi \(`{}`\).  È simile alla sintassi del valore letterale della matrice descritta in [Matrici](../../../../visual-basic/programming-guide/language-features/arrays/index.md).  Negli esempi riportati di seguito vengono illustrate diverse modalità di utilizzo degli inizializzatori di raccolta per creare le raccolte.  
  
 [!code-vb[VbVbalrCollectionInitializers#1](../../../../visual-basic/programming-guide/language-features/arrays/codesnippet/VisualBasic/index_1.vb)]  
  
> [!NOTE]
>  Anche in C\# sono disponibili inizializzatori di raccolta.  Gli inizializzatori di raccolta di C\# forniscono la stessa funzionalità di quelli di Visual Basic.  Per ulteriori informazioni sugli inizializzatori di raccolta di C\#, vedere [Inizializzatori di oggetto e di raccolta](../../../../csharp/programming-guide/classes-and-structs/object-and-collection-initializers.md).  
  
## Sintassi  
 Un inizializzatore di raccolta è costituito da un elenco di valori delimitati da virgole racchiusi tra parentesi \(`{}`\), preceduti dalla parola chiave `From`, come mostrato nel codice seguente.  
  
 [!code-vb[VbVbalrCollectionInitializers#2](../../../../visual-basic/programming-guide/language-features/arrays/codesnippet/VisualBasic/index_2.vb)]  
  
 Quando si crea una raccolta, quale un oggetto <xref:System.Collections.Generic.List%601> o <xref:System.Collections.Generic.Dictionary%602>, è necessario specificare il tipo di raccolta prima dell'inizializzatore di raccolta, come illustrato nel codice seguente.  
  
 [!code-vb[VbVbalrCollectionInitializers#13](../../../../visual-basic/programming-guide/language-features/arrays/codesnippet/VisualBasic/index_3.vb)]  
  
> [!NOTE]
>  Non è possibile utilizzare sia un inizializzatore di raccolta che un inizializzatore di oggetto per inizializzare lo stesso oggetto Collection.  È possibile utilizzare gli inizializzatori di oggetto per inizializzare gli oggetti in un inizializzatore di raccolta.  
  
## Creazione di una raccolta tramite un inizializzatore di raccolta  
 Quando si crea una raccolta utilizzando un inizializzatore di raccolta, ogni valore specificato nell'inizializzatore di raccolta viene passato al metodo `Add` appropriato della raccolta.  Se, ad esempio, si crea un oggetto <xref:System.Collections.Generic.List%601> utilizzando un inizializzatore di raccolta, ogni valore di stringa nell'inizializzatore di raccolta viene passato al metodo <xref:System.Collections.Generic.List%601.Add%2A>.  Se si desidera creare una raccolta utilizzando un inizializzatore di raccolta, il tipo specificato deve essere il tipo di raccolta valido.  Tra gli esempi di tipi di raccolta validi sono incluse le classi che implementano l'interfaccia <xref:System.Collections.Generic.IEnumerable%601> o ereditano la classe <xref:System.Collections.CollectionBase>.  Il tipo specificato deve inoltre esporre un metodo `Add` che soddisfa i criteri seguenti.  
  
-   Il metodo `Add` deve essere disponibile dall'ambito nel quale viene chiamato l'inizializzatore di raccolta.  Il metodo `Add` non deve essere pubblico se si utilizza l'inizializzatore di raccolta in uno scenario dove è possibile accedere a metodi non pubblici della raccolta.  
  
-   Il metodo `Add` deve essere un membro di istanza o un membro `Shared` della classe di raccolte oppure un metodo di estensione.  
  
-   Deve esistere un metodo `Add` corrispondente, in base alle regole di risoluzione dell'overload, ai tipi specificati nell'inizializzatore di raccolta.  
  
 Nell'esempio di codice seguente, ad esempio, viene illustrato come creare una raccolta `List(Of Customer)` utilizzando un inizializzatore di raccolta.  Quando viene eseguito il codice, ogni oggetto `Customer` viene passato al metodo `Add(Customer)` dell'elenco generico.  
  
 [!code-vb[VbVbalrCollectionInitializers#9](../../../../visual-basic/programming-guide/language-features/arrays/codesnippet/VisualBasic/index_4.vb)]  
  
 Nell'esempio di codice seguente viene illustrato il codice equivalente che non utilizza un inizializzatore di raccolta.  
  
 [!code-vb[VbVbalrCollectionInitializers#10](../../../../visual-basic/programming-guide/language-features/arrays/codesnippet/VisualBasic/index_5.vb)]  
  
 Se la raccolta dispone di un metodo `Add` con parametri corrispondenti al costruttore per l'oggetto `Customer`, è possibile annidare valori del parametro per il metodo `Add` all'interno di inizializzatori di raccolta, come illustrato nella sezione successiva.  Se la raccolta non dispone di tale metodo `Add`, è possibile crearne uno come metodo di estensione.  Per un esempio di creazione di un metodo `Add` come metodo di estensione per una raccolta, vedere [How to: Create an Add Extension Method Used by a Collection Initializer](../../../../visual-basic/programming-guide/language-features/collection-initializers/how-to-create-an-add-extension-method-used-by-a-collection-initializer.md).  Per un esempio di creazione di una raccolta personalizzata che può essere utilizzata con un inizializzatore di raccolta, vedere [How to: Create a Collection Used by a Collection Initializer](../../../../visual-basic/programming-guide/language-features/collection-initializers/how-to-create-a-collection-used-by-a-collection-initializer.md).  
  
## Annidamento di inizializzatori di raccolta  
 È possibile annidare valori all'interno di un inizializzatore di raccolta per identificare un overload specifico di un metodo `Add` per la raccolta creata.  I valori passati al metodo `Add` devono essere separati da virgole e racchiusi tra parentesi \(`{}`\), come in un valore letterale di matrice o in un inizializzatore di raccolta.  
  
 Quando si crea una raccolta utilizzando valori annidati, ogni elemento dell'elenco di valori annidati viene passato come argomento al metodo `Add` che corrisponde ai tipi di elemento.  Nell'esempio di codice seguente, ad esempio, viene creato un oggetto <xref:System.Collections.Generic.Dictionary%602> in cui le chiavi sono di tipo `Integer` e i valori sono di tipo `String`.  Ognuno degli elenchi di valori annidati corrisponde al metodo <xref:System.Collections.Generic.Dictionary%602.Add%2A> per l'oggetto `Dictionary`.  
  
 [!code-vb[VbVbalrCollectionInitializers#5](../../../../visual-basic/programming-guide/language-features/arrays/codesnippet/VisualBasic/index_6.vb)]  
  
 Di seguito viene fornito il codice equivalente all'esempio di codice precedente.  
  
 [!code-vb[VbVbalrCollectionInitializers#6](../../../../visual-basic/programming-guide/language-features/arrays/codesnippet/VisualBasic/index_7.vb)]  
  
 Solo gli elenchi di valori annidati dal primo livello di annidamento vengono inviati al metodo `Add` per il tipo di raccolta.  I livelli più profondi di annidamento vengono considerati valori letterali di matrice e gli elenchi di valori annidati non corrispondono al metodo `Add` di alcuna raccolta.  
  
## Argomenti correlati  
  
|||  
|-|-|  
|Titolo|Descrizione|  
|[How to: Create an Add Extension Method Used by a Collection Initializer](../../../../visual-basic/programming-guide/language-features/collection-initializers/how-to-create-an-add-extension-method-used-by-a-collection-initializer.md)|Viene illustrato come creare un metodo di estensione denominato `Add` che può essere utilizzato per popolare una raccolta con i valori da un inizializzatore di raccolta.|  
|[How to: Create a Collection Used by a Collection Initializer](../../../../visual-basic/programming-guide/language-features/collection-initializers/how-to-create-a-collection-used-by-a-collection-initializer.md)|Viene illustrato come attivare l'utilizzo di un inizializzatore di raccolta includendo `Add` metodo in una classe di raccolte che implementa  `IEnumerable`.|  
  
## Vedere anche  
 [Raccolte](../Topic/Collections%20\(C%23%20and%20Visual%20Basic\).md)   
 [Matrici](../../../../visual-basic/programming-guide/language-features/arrays/index.md)   
 [Object Initializers: Named and Anonymous Types](../../../../visual-basic/programming-guide/language-features/objects-and-classes/object-initializers-named-and-anonymous-types.md)   
 [New Operator](../../../../visual-basic/language-reference/operators/new-operator.md)   
 [Auto\-Implemented Properties](../../../../visual-basic/programming-guide/language-features/procedures/auto-implemented-properties.md)   
 [How to: Initialize an Array Variable in Visual Basic](../../../../visual-basic/programming-guide/language-features/arrays/how-to-initialize-an-array-variable.md)   
 [Local Type Inference](../../../../visual-basic/programming-guide/language-features/variables/local-type-inference.md)   
 [Anonymous Types](../../../../visual-basic/programming-guide/language-features/objects-and-classes/anonymous-types.md)   
 [Introduction to LINQ in Visual Basic](../../../../visual-basic/programming-guide/language-features/linq/introduction-to-linq.md)   
 [How to: Create a List of Items](../../../../visual-basic/programming-guide/concepts/linq/how-to-create-a-list-of-items.md)