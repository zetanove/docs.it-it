---
title: "contenitore di entit&#224; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 16e80405-2c75-42fc-b0e4-b1df53b1c584
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# contenitore di entit&#224;
Un *contenitore di entità* è un raggruppamento logico di [set di entità](../../../../docs/framework/data/adonet/entity-set.md), [set di associazioni](../../../../docs/framework/data/adonet/association-set.md) e [importazioni di funzioni](../../../../docs/framework/data/adonet/model-declared-function.md).  
  
 Le affermazioni seguenti relative a un contenitore di entità definito in un modello concettuale devono essere vere:  
  
-   In ogni modello concettuale deve essere definito almeno un contenitore di entità.  
  
-   Il contenitore di entità deve disporre di un nome univoco all'interno di ogni modello concettuale.  
  
 Un contenitore di entità può definire set di entità o set di associazioni che usano i tipi o le associazioni di entità definite in uno o più spazi dei nomi.  Per altre informazioni, vedere [Entity Data Model: spazi dei nomi](../../../../docs/framework/data/adonet/entity-data-model-namespaces.md).  
  
## Esempio  
 Nel diagramma seguente viene illustrato un modello concettuale con tre tipi di entità: `Book`, `Publisher` e `Author`.  Per altre informazioni, vedere l'esempio successivo.  
  
 ![Modello di esempio](../../../../docs/framework/data/adonet/media/examplemodel.gif "ExampleModel")  
  
 Anche se nel diagramma non sono contenute informazioni sul contenitore di entità, il modello concettuale deve definire un contenitore di entità.  [ADO.NET Entity Framework](../../../../docs/framework/data/adonet/ef/index.md) usa un linguaggio specifico di dominio detto [CSDL](../../../../docs/framework/data/adonet/ef/language-reference/csdl-specification.md) \(Conceptual Schema Definition Language\) per definire i modelli concettuali.  Il linguaggio CSDL seguente definisce un contenitore di entità per il modello concettuale illustrato nel diagramma precedente.  Si noti che il nome del contenitore di entità è definito in un attributo XML.  
  
 [!code-xml[EDM_Example_Model#EntityContainerExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#entitycontainerexample)]  
  
## Vedere anche  
 [Concetti chiave di Entity Data Model](../../../../docs/framework/data/adonet/entity-data-model-key-concepts.md)   
 [Entity Data Model](../../../../docs/framework/data/adonet/entity-data-model.md)