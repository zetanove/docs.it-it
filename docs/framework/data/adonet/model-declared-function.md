---
title: "funzione dichiarata dal modello | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: aba87f13-5685-4f6b-ad14-918e8a7d5c2a
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# funzione dichiarata dal modello
Una *funzione dichiarata dal modello* è una funzione dichiarata in un modello concettuale, ma non definita in tale modello concettuale.  La funzione può essere definita nell'ambiente host o di archiviazione.  È possibile, ad esempio, eseguire il mapping di una funzione dichiarata dal modello a una funzione definita in un database, esponendo in tal modo la funzionalità lato server nel modello concettuale.  
  
 La dichiarazione di una funzione dichiarata dal modello contiene le informazioni seguenti:  
  
-   Nome della funzione.  \(obbligatorio\).  
  
-   Il tipo del valore restituito  \(facoltativo\)  
  
    > [!NOTE]
    >  Se non viene specificato alcun valore restituito, il tipo restituito sarà void.  
  
-   Informazioni sul parametro, inclusi il nome e il tipo del parametro  \(facoltativo\)  
  
## Esempio  
 [ADO.NET Entity Framework](../../../../docs/framework/data/adonet/ef/index.md) usa un linguaggio specifico di dominio detto [CSDL](../../../../docs/framework/data/adonet/ef/language-reference/csdl-specification.md) \(Conceptual Schema Definition Language\) per definire i modelli concettuali.  In CSDL, un'implementazione di una funzione dichiarata dal modello è un'[importazione di funzioni](http://msdn.microsoft.com/it-it/125704ae-56c7-4233-80b7-389a10f3a65d).  Il seguente linguaggio CSDL definisce un contenitore di entità con una definizione di importazione di funzioni.  Si noti che il tipo restituito per la funzione è void perché non è specificato alcun tipo restituito.  
  
 [!code-xml[EDM_Example_Model#FunctionImport](../../../../samples/snippets/xml/VS_Snippets_Data/edm_example_model/xml/books4.edmx#functionimport)]  
  
## Vedere anche  
 [Concetti chiave di Entity Data Model](../../../../docs/framework/data/adonet/entity-data-model-key-concepts.md)   
 [Entity Data Model](../../../../docs/framework/data/adonet/entity-data-model.md)