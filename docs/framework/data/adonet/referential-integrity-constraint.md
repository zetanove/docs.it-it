---
title: "vincolo di integrit&#224; referenziale | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3d3ba44b-4302-40d8-a7a9-62932e0395e5
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# vincolo di integrit&#224; referenziale
Un *vincolo di integrità referenziale* in Entity Data Model \(EDM\) è analogo a un vincolo di integrità referenziale in un database relazionale.  Nello stesso modo in cui una colonna \(o più colonne\) da una tabella di database può fare riferimento alla chiave primaria di un'altra tabella, una [proprietà](../../../../docs/framework/data/adonet/property.md) \(o più proprietà\) di un [tipo di entità](../../../../docs/framework/data/adonet/entity-type.md) può fare riferimento alla [chiave di entità](../../../../docs/framework/data/adonet/entity-key.md) di un altro tipo di entità.  Il tipo di entità al quale è fatto riferimento viene chiamato l'*entità finale principale* del vincolo.  Il tipo di entità che fa riferimento all'estremità principale viene chiamato l'*entità finale dipendente* del vincolo.  
  
 Un vincolo di integrità referenziale è definito come parte di un'[associazione](../../../../docs/framework/data/adonet/association-type.md) tra due tipi di entità.  La definizione per un vincolo di integrità referenziale specifica le informazioni seguenti:  
  
-   Entità finale principale del vincolo  \(un tipo di entità alla cui chiave di entità è fatto riferimento dall'entità finale dipendente\).  
  
-   Chiave di entità dell'entità finale principale.  
  
-   Entità finale dipendente del vincolo  \(un tipo di entità che dispone di una o più proprietà che fanno riferimento alla chiave di entità dell'entità finale principale\).  
  
-   La proprietà o le proprietà di riferimento dell'entità finale dipendente.  
  
 Lo scopo dei vincoli di integrità referenziali in EDM è di assicurare che esistano sempre associazioni valide.  Per altre informazioni, vedere [proprietà di chiave esterna](../../../../docs/framework/data/adonet/foreign-key-property.md).  
  
## Esempio  
 Nel diagramma seguente viene illustrato un modello concettuale con due associazioni: `WrittenBy` e `PublishedBy`.  Il tipo di entità `Book` dispone di una proprietà, `PublisherId`, che fa riferimento alla chiave di entità del tipo di entità `Publisher` quando si definisce un vincolo di integrità referenziale sull'associazione `PublishedBy`.  
  
 ![RefConstraintModel](../../../../docs/framework/data/adonet/media/refconstraintmodel.gif "RefConstraintModel")  
  
 [ADO.NET Entity Framework](../../../../docs/framework/data/adonet/ef/index.md) usa un linguaggio specifico di dominio detto [CSDL](../../../../docs/framework/data/adonet/ef/language-reference/csdl-specification.md) \(Conceptual Schema Definition Language\) per definire i modelli concettuali.  Nel seguente linguaggio CSDL viene definito un vincolo di integrità referenziale sull'associazione `PublishedBy` illustrata nel modello concettuale precedente.  
  
 [!code-xml[EDM_Example_Model#RefConstraint](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books4.edmx#refconstraint)]  
  
## Vedere anche  
 [Concetti chiave di Entity Data Model](../../../../docs/framework/data/adonet/entity-data-model-key-concepts.md)   
 [Entity Data Model](../../../../docs/framework/data/adonet/entity-data-model.md)