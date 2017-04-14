---
title: "Procedura: definire la stringa di connessione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "ESQL"
  - "jsharp"
ms.assetid: 6027335d-4e26-420d-9151-6523289b1989
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Procedura: definire la stringa di connessione
In questo argomento viene illustrato come definire la stringa di connessione usata per la connessione a un modello concettuale.  Questo argomento è basato sul modello concettuale [Sales di AdventureWorks](http://msdn.microsoft.com/it-it/f16cd988-673f-4376-b034-129ca93c7832).  Il modello Sales di AdventureWorks viene usato in tutti gli argomenti correlati ad attività inclusi nella documentazione di [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)].  In questo argomento si presuppone che [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] sia già stato configurato e che il modello Sales di AdventureWorks sia già stato definito.  Per altre informazioni, vedere [How to: Manually Define the Model and Mapping Files](http://msdn.microsoft.com/it-it/d4fd6864-f2a1-48f0-aa32-1e318775a99a).  Le procedure di questo argomento sono incluse anche in [How to: Manually Configure an Entity Framework Project](http://msdn.microsoft.com/it-it/73f6ae1d-b3b2-4577-aebd-ad5a75954e9e).  
  
> [!NOTE]
>  Se si usa la Procedura guidata [!INCLUDE[adonet_edm](../../../../../includes/adonet-edm-md.md)] in un progetto [!INCLUDE[vsprvs](../../../../../includes/vsprvs-md.md)], viene automaticamente generato un file con estensione edmx e il progetto viene configurato per l'uso di [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)].  Per altre informazioni, vedere [How to: Use the Entity Data Model Wizard](http://msdn.microsoft.com/it-it/dadb058a-c5d9-4c5c-8b01-28044112231d).  
  
### Per definire la stringa di connessione Entity Framework  
  
-   Aprire il file di configurazione dell'applicazione \(app.config\) del progetto e aggiungere la stringa di connessione seguente.  
  
  
  
     Se il progetto non dispone di un file di configurazione dell'applicazione, è possibile aggiungerne uno scegliendo **Aggiungi nuovo elemento** dal menu **Progetto**, selezionando la categoria **Generale**, selezionando **File di configurazione dell'applicazione** e quindi facendo clic su **Aggiungi**.  
  
## Vedere anche  
 [Quickstart](http://msdn.microsoft.com/it-it/0bc534be-789f-4819-b9f6-76e51d961675)   
 [How to: Create a New .edmx File](http://msdn.microsoft.com/it-it/beb8189e-e51c-4051-839c-9902c224abf2)   
 [ADO.NET Entity Data Model  Tools](http://msdn.microsoft.com/it-it/91076853-0881-421b-837a-f582f36be527)