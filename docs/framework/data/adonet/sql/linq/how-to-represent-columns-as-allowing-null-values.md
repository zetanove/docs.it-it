---
title: "Procedura: rappresentare le colonne in modo che accettino valori Null | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: ebb71a37-1f4c-4fa7-b2d2-d903f13c4af1
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Procedura: rappresentare le colonne in modo che accettino valori Null
Usare la proprietà <xref:System.Data.Linq.Mapping.ColumnAttribute.CanBeNull%2A> di [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] sull'attributo <xref:System.Data.Linq.Mapping.ColumnAttribute> per specificare che la colonna del database associata può contenere valori null.  
  
 Per esempi di codice, vedere <xref:System.Data.Linq.Mapping.ColumnAttribute.CanBeNull%2A>.  
  
### Per definire una colonna in modo che accetti valori null  
  
1.  Aggiungere la proprietà <xref:System.Data.Linq.Mapping.ColumnAttribute.CanBeNull%2A> all'attributo <xref:System.Data.Linq.Mapping.ColumnAttribute>.  
  
2.  Impostare il valore della proprietà <xref:System.Data.Linq.Mapping.ColumnAttribute.CanBeNull%2A> su `true`.  
  
## Vedere anche  
 [Il modello a oggetti LINQ to SQL](../../../../../../docs/framework/data/adonet/sql/linq/the-linq-to-sql-object-model.md)   
 [Procedura: personalizzare le classi di entità mediante l'editor di codice](../../../../../../docs/framework/data/adonet/sql/linq/how-to-customize-entity-classes-by-using-the-code-editor.md)