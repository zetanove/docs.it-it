---
title: "tipo di associazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 26c409f6-06e8-4441-ac78-1b1076a3c005
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# tipo di associazione
Un *tipo di associazione* \(detto anche associazione\) è il blocco predefinito fondamentale per la descrizione delle relazioni in Entity Data Model \(EDM\).  In un modello concettuale, un'associazione rappresenta una relazione tra due [tipi di entità](../../../../docs/framework/data/adonet/entity-type.md) \(ad esempio, `Customer` e `Order`\).  In un'applicazione, un'istanza di un'associazione rappresenta un'associazione specifica \(ad esempio, un'associazione tra un'istanza di `Customer` e una di `Order`\).  Le istanze dell'associazione sono raggruppate logicamente in un [set di associazioni](../../../../docs/framework/data/adonet/association-set.md).  
  
 Una definizione di associazione contiene le informazioni seguenti:  
  
-   Un nome univoco.  \(obbligatorio\).  
  
-   Due [entità finali dell'associazione](../../../../docs/framework/data/adonet/association-end.md), uno per ogni tipo di entità nella relazione  \(obbligatorio\).  
  
    > [!NOTE]
    >  Un'associazione non può rappresentare una relazione tra più di due tipi di entità.  Un'associazione può tuttavia definire una relazione interna specificando lo stesso tipo di entità per ognuna delle entità finali dell'associazione.  
  
-   Un [vincolo di integrità referenziale](../../../../docs/framework/data/adonet/referential-integrity-constraint.md) \(facoltativo\)  
  
 Ogni entità finale dell'associazione deve specificare una [molteplicità di entità finale dell'associazione](../../../../docs/framework/data/adonet/association-end-multiplicity.md) che indica il numero di istanze del tipo di entità che possono trovarsi in un'entità finale dell'associazione.  Una molteplicità di entità finale dell'associazione può disporre di un valore pari a uno \(1\), zero o uno \(0..1\) o molti \(\*\).  Le istanze del tipo di entità in corrispondenza di un'entità finale di un'associazione sono accessibili attraverso [proprietà di navigazione](../../../../docs/framework/data/adonet/navigation-property.md) o chiavi esterne se sono esposte in un tipo di entità.  Per altre informazioni, vedere [Entity Data Model \- Chiavi esterne](../../../../docs/framework/data/adonet/foreign-key-property.md).  
  
## Esempio  
 Nel diagramma seguente viene illustrato un modello concettuale con due associazioni: `PublishedBy` e `WrittenBy`.  Le entità finali dell'associazione per l'associazione `PublishedBy` sono i tipi di entità `Book` e `Publisher`.  La molteplicità dell'entità finale `Publisher` è uno \(1\) e la molteplicità dell'entità finale `Book` è molti \(\*\), a indicare che un editore pubblica molti libri e un libro viene pubblicato da un solo editore.  
  
 ![Modello di esempio](../../../../docs/framework/data/adonet/media/examplemodel.gif "ExampleModel")  
  
 [ADO.NET Entity Framework](../../../../docs/framework/data/adonet/ef/index.md) usa un linguaggio specifico di dominio detto [CSDL](../../../../docs/framework/data/adonet/ef/language-reference/csdl-specification.md) \(Conceptual Schema Definition Language\) per definire i modelli concettuali.  Il linguaggio CSDL seguente definisce l'associazione `PublishedBy` illustrata nel diagramma precedente:  
  
 [!code-xml[EDM_Example_Model#AssociationExample](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books.edmx#associationexample)]  
  
## Vedere anche  
 [Concetti chiave di Entity Data Model](../../../../docs/framework/data/adonet/entity-data-model-key-concepts.md)   
 [Entity Data Model](../../../../docs/framework/data/adonet/entity-data-model.md)