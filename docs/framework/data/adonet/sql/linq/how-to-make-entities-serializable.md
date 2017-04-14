---
title: "Procedura: creare entit&#224; serializzabili | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: a6c5bf6e-064a-4f77-b74c-76b3a5dec309
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Procedura: creare entit&#224; serializzabili
Quando si genera il codice, è possibile rendere serializzabili le entità.  Le classi di entità vengono decorate con l'attributo <xref:System.Runtime.Serialization.DataContractAttribute> e le colonne con l'attributo <xref:System.Runtime.Serialization.DataMemberAttribute>.  
  
 Gli sviluppatori che usano [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] possono adoperare [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)] a questo scopo.  
  
 Se si usa lo strumento della riga di comando SQLMetal, usare l'opzione **\/serialization** con l'argomento `unidirectional`.  Per altre informazioni, vedere [SqlMetal.exe \(strumento per la generazione del codice\)](../../../../../../docs/framework/tools/sqlmetal-exe-code-generation-tool.md).  
  
## Esempio  
 Le righe di comando SQLMetal seguenti consentono di produrre file con entità serializzabili.  
  
```  
sqlmetal /code:nwserializable.vb /language:vb "c:\northwnd.mdf" /sprocs /functions /pluralize /serialization:unidirectional  
```  
  
```  
sqlmetal /code:nwserializable.cs /language:csharp "c:\northwnd.mdf" /sprocs /functions /pluralize /serialization:unidirectional  
```  
  
## Vedere anche  
 [Serializzazione](../../../../../../docs/framework/data/adonet/sql/linq/serialization.md)   
 [Creazione del modello a oggetti](../../../../../../docs/framework/data/adonet/sql/linq/creating-the-object-model.md)