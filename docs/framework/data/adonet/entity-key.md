---
title: "chiave di entit&#224; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0d447a6d-fa7a-4db0-8e7a-fd45e385fca0
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# chiave di entit&#224;
Una *chiave di entità* è una [proprietà](../../../../docs/framework/data/adonet/property.md) o un set di proprietà di un [tipo di entità](../../../../docs/framework/data/adonet/entity-type.md) usate per determinare l'identità.  Le proprietà che costituiscono una chiave di entità vengono scelte in fase di progettazione.  I valori delle proprietà della chiave di entità devono identificare in modo univoco in fase di esecuzione un'istanza del tipo di entità all'interno di un [set di entità](../../../../docs/framework/data/adonet/entity-set.md).  Le proprietà che costituiscono una chiave di entità devono essere scelte per garantire univocità delle istanze in un set di entità.  
  
 Di seguito sono elencati i requisiti che consentono a un set di proprietà di essere una chiave di entità:  
  
-   Non possono esistere due chiavi di entità identiche all'interno di un set di entità,  vale a dire che, per due entità qualsiasi all'interno di un set di entità, i valori per tutte le proprietà che costituiscono una chiave non possono essere gli stessi.  Tuttavia, alcuni valori \(ma non tutti\) che costituiscono una chiave di entità possono essere gli stessi.  
  
-   Una chiave di entità deve essere costituita da un set di [proprietà di tipo primitivo](../../../../docs/framework/data/adonet/entity-data-model-primitive-data-types.md) non nullable e immutabili.  
  
-   Le proprietà che costituiscono una chiave di entità per un determinato tipo di entità non possono essere modificate.  Non è possibile consentire più di una possibile chiave di entità per un determinato tipo di entità. Le chiavi surrogate non sono supportate.  
  
-   Quando un'entità è coinvolta in una gerarchia di ereditarietà, l'entità radice deve contenere tutte le proprietà che costituiscono la chiave di entità e la chiave di entità deve essere definita sul tipo di entità radice.  Per altre informazioni, vedere [Entity Data Model: ereditarietà](../../../../docs/framework/data/adonet/entity-data-model-inheritance.md).  
  
## Esempio  
 Nel diagramma seguente viene illustrato un modello concettuale con tre tipi di entità: `Book`, `Publisher` e `Author`.  Le proprietà di ogni tipo di entità che costituiscono la chiave di entità vengono indicate con "\(Key\)".  Si noti che il tipo di entità `Author` dispone di una chiave di entità costituita da due proprietà, `Name` e `Address`.  
  
 ![Modello di esempio](../../../../docs/framework/data/adonet/media/examplemodel.gif "ExampleModel")  
  
 [ADO.NET Entity Framework](../../../../docs/framework/data/adonet/ef/index.md) usa un linguaggio specifico di dominio detto [CSDL](../../../../docs/framework/data/adonet/ef/language-reference/csdl-specification.md) \(Conceptual Schema Definition Language\) per definire i modelli concettuali.  Il linguaggio CSDL seguente definisce il tipo di entità `Book` illustrato nel diagramma precedente.  Si noti che la chiave di entità viene definita facendo riferimento alla proprietà `ISBN` del tipo di entità.  
  
 [!code-xml[EDM_Example_Model#EntityExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#entityexample)]  
  
 La proprietà `ISBN` è una valida scelta per la chiave di entità perché un codice ISBN \(International Standard Book Number\) identifica in modo univoco un libro.  
  
 Il linguaggio CSDL seguente definisce il tipo di entità `Author` illustrato nel diagramma precedente.  Si noti che la chiave di entità è costituita da due proprietà, `Name` e `Address`.  
  
 [!code-xml[EDM_Example_Model#CompositeKeyExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#compositekeyexample)]  
  
 L'utilizzo di `Name` e `Address` per la chiave di entità è una scelta ragionevole, perché è improbabile che due autori con lo stesso nome vivano allo stesso indirizzo.  Questa scelta per una chiave di entità non garantisce tuttavia in modo assoluto chiavi di entità univoche in un set di entità.  In questo caso, è consigliabile aggiungere una proprietà, ad esempio `AuthorId`, che consente di identificare in modo univoco un autore.  
  
## Vedere anche  
 [Concetti chiave di Entity Data Model](../../../../docs/framework/data/adonet/entity-data-model-key-concepts.md)   
 [Entity Data Model](../../../../docs/framework/data/adonet/entity-data-model.md)