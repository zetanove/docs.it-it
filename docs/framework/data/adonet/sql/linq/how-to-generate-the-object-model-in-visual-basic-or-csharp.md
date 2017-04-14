---
title: "Procedura: generare il modello a oggetti in Visual Basic o C# | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a0c73b33-5650-420c-b9dc-f49310c201ee
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Procedura: generare il modello a oggetti in Visual Basic o C# #
In [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] viene eseguito il mapping di un modello a oggetti nel linguaggio di programmazione in uso a un database relazionale.  Per generare automaticamente un modello [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)] o C\# dai metadati di un database esistente sono disponibili due strumenti.  
  
-   Se si usa [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)], è possibile usare [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)] per generare un modello a oggetti.  In [!INCLUDE[vs_ordesigner_short](../../../../../../includes/vs-ordesigner-short-md.md)] è disponibile un'interfaccia utente avanzata che consente di generare un modello a oggetti [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  
  
-   Lo strumento della riga di comando SQLMetal.  Per altre informazioni, vedere [SqlMetal.exe \(strumento per la generazione del codice\)](../../../../../../docs/framework/tools/sqlmetal-exe-code-generation-tool.md).  
  
    > [!NOTE]
    >  Se non si dispone di un database esistente e si desidera crearne uno da un modello a oggetti, è possibile creare il modello a oggetti usando l'editor di codice e <xref:System.Data.Linq.DataContext.CreateDatabase%2A>.  Per altre informazioni, vedere [Procedura: creare dinamicamente un database](../../../../../../docs/framework/data/adonet/sql/linq/how-to-dynamically-create-a-database.md).  
  
 Nella documentazione per [!INCLUDE[vs_ordesigner_short](../../../../../../includes/vs-ordesigner-short-md.md)] vengono forniti esempi su come generare un modello a oggetti [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)] o C\# usando [!INCLUDE[vs_ordesigner_short](../../../../../../includes/vs-ordesigner-short-md.md)].  Le informazioni seguenti forniscono esempi relativi all'uso dello strumento della riga di comando SQLMetal.  Per altre informazioni, vedere [SqlMetal.exe \(strumento per la generazione del codice\)](../../../../../../docs/framework/tools/sqlmetal-exe-code-generation-tool.md).  
  
## Esempio  
 Usando la riga di comando SQLMetal riportata nell'esempio è possibile produrre codice [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)] come modello a oggetti basato su attributi del database di esempio Northwind.  Viene eseguito il rendering anche di stored procedure e funzioni.  
  
```  
sqlmetal /code:northwind.vb /language:vb "c:\northwnd.mdf" /sprocs /functions  
```  
  
## Esempio  
 Usando la riga di comando SQLMetal riportata nell'esempio è possibile produrre codice C\# come modello a oggetti basato su attributi del database di esempio Northwind.  Viene eseguito il rendering anche di stored procedure e funzioni, mentre i nomi delle tabelle vengono pluralizzati automaticamente.  
  
```  
sqlmetal /code:northwind.cs /language:csharp "c:\northwnd.mdf" /sprocs /functions /pluralize  
```  
  
## Vedere anche  
 [Guida per programmatori](../../../../../../docs/framework/data/adonet/sql/linq/programming-guide.md)   
 [Il modello a oggetti LINQ to SQL](../../../../../../docs/framework/data/adonet/sql/linq/the-linq-to-sql-object-model.md)   
 [Apprendimento tramite le procedure dettagliate](../../../../../../docs/framework/data/adonet/sql/linq/learning-by-walkthroughs.md)   
 [Procedura: personalizzare le classi di entità mediante l'editor di codice](../../../../../../docs/framework/data/adonet/sql/linq/how-to-customize-entity-classes-by-using-the-code-editor.md)   
 [Mapping basato su attributi](../../../../../../docs/framework/data/adonet/sql/linq/attribute-based-mapping.md)   
 [SqlMetal.exe \(strumento per la generazione del codice\)](../../../../../../docs/framework/tools/sqlmetal-exe-code-generation-tool.md)   
 [Mapping esterno](../../../../../../docs/framework/data/adonet/sql/linq/external-mapping.md)   
 [Download dei database di esempio](../../../../../../docs/framework/data/adonet/sql/linq/downloading-sample-databases.md)   
 [Creazione del modello a oggetti](../../../../../../docs/framework/data/adonet/sql/linq/creating-the-object-model.md)