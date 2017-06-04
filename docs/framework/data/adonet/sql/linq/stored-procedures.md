---
title: "Stored procedure | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4d23dd7a-a85f-44ff-a717-af7d0950c0fc
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Stored procedure
In [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] vengono usati metodi nel modello a oggetti per rappresentare stored procedure nel database.  Per definire metodi come stored procedure, applicare l'attributo <xref:System.Data.Linq.Mapping.FunctionAttribute> quindi, dove richiesto, l'attributo <xref:System.Data.Linq.Mapping.ParameterAttribute>.  Per altre informazioni, vedere [Il modello a oggetti LINQ to SQL](../../../../../../docs/framework/data/adonet/sql/linq/the-linq-to-sql-object-model.md).  
  
 Gli sviluppatori che usano [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] ricorrono in genere a [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)] per eseguire il mapping delle stored procedure. Negli argomenti elencati in questa sezione viene illustrato come formare e chiamare questi metodi nell'applicazione quando si scrive codice personalizzato.  
  
## In questa sezione  
 [Procedura: restituire rowset](../../../../../../docs/framework/data/adonet/sql/linq/how-to-return-rowsets.md)  
 Viene descritto come restituire righe di dati e viene illustrato come usare un parametro di input.  
  
 [Procedura: utilizzare le stored procedure che accettano parametri](../../../../../../docs/framework/data/adonet/sql/linq/how-to-use-stored-procedures-that-take-parameters.md)  
 Viene descritto come usare parametri di input e output.  
  
 [Procedura: utilizzare stored procedure mappate per forme di risultati multipli](../../../../../../docs/framework/data/adonet/sql/linq/how-to-use-stored-procedures-mapped-for-multiple-result-shapes.md)  
 Viene descritto come ottenere la restituzione di più forme nella stessa stored procedure.  
  
 [Procedura: utilizzare stored procedure mappate per forme di risultati sequenziali](../../../../../../docs/framework/data/adonet/sql/linq/how-to-use-stored-procedures-mapped-for-sequential-result-shapes.md)  
 Viene descritto come ottenere più forme dove la sequenza restituita è nota.  
  
 [Personalizzazione delle operazioni tramite l'utilizzo di stored procedure](../../../../../../docs/framework/data/adonet/sql/linq/customizing-operations-by-using-stored-procedures.md)  
 Viene descritto come usare stored procedure per implementare operazioni di inserimento, aggiornamento ed eliminazione.  
  
 [Personalizzazione delle operazioni tramite l'utilizzo esclusivo di stored procedure](../../../../../../docs/framework/data/adonet/sql/linq/customizing-operations-by-using-stored-procedures-exclusively.md)  
 Viene descritto come usare unicamente stored procedure per implementare operazioni di inserimento, aggiornamento ed eliminazione.  
  
## Sezioni correlate  
 [Guida per programmatori](../../../../../../docs/framework/data/adonet/sql/linq/programming-guide.md)  
 Fornisce informazioni sulla creazione e sull'uso del modello a oggetti di [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  
  
 [Procedura dettagliata: utilizzo delle sole stored procedure \(Visual Basic\)](../../../../../../docs/framework/data/adonet/sql/linq/walkthrough-using-only-stored-procedures-visual-basic.md)  
 Sono incluse procedure che illustrano come usare stored procedure in Visual Basic.  
  
 [Procedura dettagliata: utilizzo delle sole stored procedure \(C\#\)](../../../../../../docs/framework/data/adonet/sql/linq/walkthrough-using-only-stored-procedures-csharp.md)  
 Sono incluse procedure che illustrano come usare stored procedure in C\#.