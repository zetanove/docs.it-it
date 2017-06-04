---
title: "Procedura: impostare file di modello e di mapping come risorse incorporate | Microsoft Docs"
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
ms.assetid: 20dfae4d-e95a-4264-9540-f5ad23b462d3
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Procedura: impostare file di modello e di mapping come risorse incorporate
[!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)] consente di distribuire file di modello e di mapping come risorse incorporate di un'applicazione.  L'assembly con i file di mapping e di modello incorporati deve essere caricato nello stesso dominio applicazione della connessione dell'entità.  Per altre informazioni, vedere [Stringhe di connessione](../../../../../docs/framework/data/adonet/ef/connection-strings.md).  Gli strumenti [!INCLUDE[adonet_edm](../../../../../includes/adonet-edm-md.md)] incorporano i file di modello e di mapping per impostazione predefinita. Quando si definiscono manualmente i file di modello e di mapping, usare questa procedura per assicurarsi che i file vengano distribuiti come risorse incorporate insieme all'applicazione [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)].  
  
> [!NOTE]
>  Per gestire le risorse incorporate, è necessario ripetere la procedura ogni volta che si modificano i file di modello e di mapping.  
  
### Per incorporare i file di modello e di mapping  
  
1.  In **Esplora soluzioni** selezionare il file concettuale con estensione .csdl.  
  
2.  Nel riquadro **Proprietà** impostare **Operazione di compilazione** su **Risorsa incorporata**.  
  
3.  Ripetere i passaggi 1 e 2 per il file di archiviazione \(.ssdl\) e il file di mapping \(.msl\).  
  
4.  In **Esplora soluzioni** fare doppio clic sul file App.config, quindi modificare il parametro `Metadata` nell'attributo `connectionString` in base a uno dei formati seguenti:  
  
    -   `Metadata=` `res://<assemblyFullName>/<resourceName>;`  
  
    -   `Metadata=` `res://*/<resourceName>;`  
  
    -   `Metadata=res://*;`  
  
     Per altre informazioni, vedere [Stringhe di connessione](../../../../../docs/framework/data/adonet/ef/connection-strings.md).  
  
## Esempio  
 La stringa di connessione seguente fa riferimento ai file di modello e di mapping incorporati per il [modello Sales di AdventureWorks](http://msdn.microsoft.com/it-it/f16cd988-673f-4376-b034-129ca93c7832).  Questa stringa di connessione è archiviata nel file App.config del progetto.  
  
  
  
## Vedere anche  
 [Modellazione e mapping](../../../../../docs/framework/data/adonet/ef/modeling-and-mapping.md)   
 [Procedura: definire la stringa di connessione](../../../../../docs/framework/data/adonet/ef/how-to-define-the-connection-string.md)   
 [Procedura: compilare una stringa di connessione EntityConnection](../../../../../docs/framework/data/adonet/ef/how-to-build-an-entityconnection-connection-string.md)   
 [ADO.NET Entity Data Model  Tools](http://msdn.microsoft.com/it-it/91076853-0881-421b-837a-f582f36be527)