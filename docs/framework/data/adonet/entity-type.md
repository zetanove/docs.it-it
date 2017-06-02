---
title: "tipo di entit&#224; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a6dee9ab-9e4a-48f2-a169-3f79cc15821c
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# tipo di entit&#224;
Il *tipo di entità* è il blocco predefinito fondamentale per la descrizione della struttura di dati con Entity Data Model \(EDM\).  In un modello concettuale, un tipo di entità rappresenta la struttura di concetti di livello superiore, quale ad esempio clienti o ordini.  Un tipo di entità è un modello per le istanze del tipo di entità.  Ogni modello contiene le informazioni seguenti:  
  
-   Un nome univoco.  Obbligatorio.  
  
-   Una [chiave di entità](../../../../docs/framework/data/adonet/entity-key.md) che è definita da una o più proprietà  Obbligatorio.  
  
-   Dati sotto forma di [proprietà](../../../../docs/framework/data/adonet/property.md) \(Facoltative\)  
  
-   [Proprietà di navigazione](../../../../docs/framework/data/adonet/navigation-property.md) che consentono di navigare da un'[entità finale](../../../../docs/framework/data/adonet/association-end.md) di un'[associazione](../../../../docs/framework/data/adonet/association-type.md) all'altra  \(facoltativo\)  
  
 In un'applicazione, un'istanza di un tipo di entità rappresenta un oggetto specifico, quale ad esempio un cliente o un ordine specifico.  Ogni istanza di un tipo di entità deve avere una [chiave di entità](../../../../docs/framework/data/adonet/entity-key.md) univoca all'interno di un [set di entità](../../../../docs/framework/data/adonet/entity-set.md).  
  
 Due istanze di tipi di entità sono considerate uguali solo se sono dello stesso tipo e se i valori delle rispettive chiavi di entità sono uguali.  
  
## Esempio  
 Nel diagramma seguente viene illustrato un modello concettuale con tre tipi di entità: `Book`, `Publisher` e `Author`:  
  
 ![Modello di esempio](../../../../docs/framework/data/adonet/media/examplemodel.gif "ExampleModel")  
  
 Si noti che le proprietà di ogni tipo di entità che costituiscono la chiave di entità vengono indicate con "\(Key\)".  
  
 [ADO.NET Entity Framework](../../../../docs/framework/data/adonet/ef/index.md) usa un linguaggio specifico di dominio detto [CSDL](../../../../docs/framework/data/adonet/ef/language-reference/csdl-specification.md) \(Conceptual Schema Definition Language\) per definire i modelli concettuali.  Il linguaggio CSDL seguente definisce il tipo di entità `Book` illustrato nel diagramma precedente:  
  
 [!code-xml[EDM_Example_Model#EntityExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#entityexample)]  
  
## Vedere anche  
 [Concetti chiave di Entity Data Model](../../../../docs/framework/data/adonet/entity-data-model-key-concepts.md)   
 [Entity Data Model](../../../../docs/framework/data/adonet/entity-data-model.md)   
 [facet](../../../../docs/framework/data/adonet/facet.md)