---
title: "Procedura: generare codice personalizzato tramite la modifica di un file DBML | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 50ad597a-8598-42d3-82dd-fc7d702ebc37
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Procedura: generare codice personalizzato tramite la modifica di un file DBML
È possibile generare codice sorgente [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)] o C\# da un file di metadati DBML \(Database Markup Language\).  Questo approccio consente di personalizzare il file DBML predefinito prima di generare il codice di mapping dell'applicazione.  Si tratta di una funzionalità avanzata.  
  
 Di seguito sono elencati i passaggi di questo processo.  
  
1.  Generare un file con estensione dbml.  
  
2.  Usare un editor per modificare il file con estensione dbml,  che dovrà essere convalidato in base al file di definizione dello schema \(con estensione xsd\) per i file dbml di [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)].  Per altre informazioni, vedere [Generazione di codice in LINQ to SQL](../../../../../../docs/framework/data/adonet/sql/linq/code-generation-in-linq-to-sql.md).  
  
3.  Generare il codice sorgente [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)] o C\#.  
  
 Negli esempi seguenti viene usato lo strumento della riga di comando SQLMetal.  Per altre informazioni, vedere [SqlMetal.exe \(strumento per la generazione del codice\)](../../../../../../docs/framework/tools/sqlmetal-exe-code-generation-tool.md).  
  
## Esempio  
 Nel codice seguente viene generato un file con estensione dbml dal database di esempio Northwind.  Come origine per i metadati del database è possibile usare il nome del database o il nome del file con estensione mdf.  
  
```  
sqlmetal /server:myserver /database:northwind /dbml:mymeta.dbml  
sqlmetal /dbml:mymeta.dbml mydbfile.mdf  
```  
  
## Esempio  
 Nel codice seguente viene generato file di codice sorgente [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)] o C\# da un file con estensione dbml.  
  
```  
sqlmetal /namespace:nwind /code:nwind.vb /language:vb DBMLFile.dbml  
sqlmetal /namespace:nwind /code:nwind.cs /language:csharp DBMLFile.dbml  
```  
  
## Vedere anche  
 [Generazione di codice in LINQ to SQL](../../../../../../docs/framework/data/adonet/sql/linq/code-generation-in-linq-to-sql.md)   
 [SqlMetal.exe \(strumento per la generazione del codice\)](../../../../../../docs/framework/tools/sqlmetal-exe-code-generation-tool.md)   
 [Creazione del modello a oggetti](../../../../../../docs/framework/data/adonet/sql/linq/creating-the-object-model.md)