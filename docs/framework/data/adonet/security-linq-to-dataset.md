---
title: "Sicurezza (LINQ to DataSet) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6116b2b8-75f4-4d8b-aea6-c13e55cda50b
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Sicurezza (LINQ to DataSet)
In questo argomento vengono illustrati i problemi di sicurezza riscontrati in [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)].  
  
## Passaggio di una query a un componente non attendibile  
 È possibile formulare una query [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] in un punto di un'applicazione e eseguirla in un punto diverso.  Nel punto in cui viene formulata, la query può fare riferimento a qualsiasi elemento visibile, ovvero membri private della classe cui appartiene il metodo chiamante oppure simboli che rappresentano variabili\/argomenti locali.  In fase di esecuzione la query sarà effettivamente in grado di accedere ai membri cui è stato fatto riferimento durante la formulazione anche se tali membri non sono visibili al codice di chiamata.  Il codice che esegue la query non dispone di visibilità arbitraria aggiunta, in quanto non è in grado di scegliere gli elementi cui accedere.  Può infatti accedere esclusivamente agli elementi accessibili alla query e solo tramite la query stessa.  
  
 Se pertanto un riferimento a una query viene passato a un'altra porzione di codice, il componente che riceve la query viene ritenuto attendibile e può accedere a tutti i membri public e private cui fa riferimento la query.  In generale, è preferibile non passare query [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] a componenti non attendibili, a meno che la query non sia stata costruita con particolare attenzione al fine di evitare l'esposizione di informazioni che devono rimanere riservate.  
  
## Input esterno  
 Le applicazioni accettano spesso input esterno, ad esempio da un utente o da un altro agente esterno, ed eseguono azioni sulla base di tale input.  Nel caso di [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)], l'applicazione può costruire una query in un determinato modo, sulla base di input esterno, oppure usare input esterno nella query. Nelle query [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] i parametri vengono accettati in qualsiasi punto in cui vengono accettati i valori letterali.  Gli sviluppatori di applicazioni devono usare query con parametri, anziché inserire valori letterali direttamente nella query tramite un agente esterno.  
  
 Eventuale input derivato in modo diretto o indiretto dall'utente o da un agente esterno può includere contenuto che sfrutta la sintassi del linguaggio di destinazione per eseguire azioni non autorizzate.  Tale fenomeno è noto come attacco SQL injection, il cui nome deriva da uno schema di attacco in cui il linguaggio di destinazione è Transact\-SQL.  L'input utente inserito direttamente nella query viene usato per rimuovere una tabella di database, determinare un attacco di tipo Denial of Service o alterare in altro modo la natura dell'operazione da eseguire.  Sebbene sia possibile comporre query in [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)], per questa operazione viene usata l'API del modello a oggetti. Le query [!INCLUDE[linq_dataset](../../../../includes/linq-dataset-md.md)] non vengono composte usando funzionalità di modifica o concatenazione di stringhe, come avviene in Transact\-SQL, e non sono soggette ad attacchi SQL injection in senso tradizionale.  
  
## Vedere anche  
 [Guida per programmatori](../../../../docs/framework/data/adonet/programming-guide-linq-to-dataset.md)