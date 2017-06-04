---
title: "Procedura: eseguire una query Entity SQL con parametri utilizzando EntityCommand | Microsoft Docs"
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
ms.assetid: e93fea43-7e03-4d7d-9fee-2517b8b88cba
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Procedura: eseguire una query Entity SQL con parametri utilizzando EntityCommand
In questo argomento viene mostrato un esempio di esecuzione di una query [!INCLUDE[esql](../../../../../includes/esql-md.md)] con parametri tramite l'uso di un oggetto <xref:System.Data.EntityClient.EntityCommand>.  
  
### Per eseguire il codice in questo esempio  
  
1.  Aggiungere [AdventureWorks Sales Model](http://msdn.microsoft.com/it-it/f16cd988-673f-4376-b034-129ca93c7832) al progetto e configurare il progetto per l'uso di [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)].  Per altre informazioni, vedere [How to: Use the Entity Data Model Wizard](http://msdn.microsoft.com/it-it/dadb058a-c5d9-4c5c-8b01-28044112231d).  
  
2.  Nella tabella codici per l'applicazione aggiungere le istruzioni `using` seguenti \(`Imports` in Visual Basic\):  
  
     [!code-csharp[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#namespaces)]
     [!code-vb[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#namespaces)]  
  
## Esempio  
 Nell'esempio seguente viene illustrato come costruire una stringa di query con due parametri.  Viene quindi creato un oggetto <xref:System.Data.EntityClient.EntityCommand>, vengono aggiunti due parametri alla raccolta <xref:System.Data.EntityClient.EntityParameter> di <xref:System.Data.EntityClient.EntityCommand> e viene scorsa la raccolta di elementi `Contact`.  
  
 [!code-csharp[DP EntityServices Concepts#ParameterizedQueryWithEntityCommand](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#parameterizedquerywithentitycommand)]
 [!code-vb[DP EntityServices Concepts#ParameterizedQueryWithEntityCommand](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#parameterizedquerywithentitycommand)]  
  
## Vedere anche  
 [How to: Execute a Parameterized Query](http://msdn.microsoft.com/it-it/42048f03-c65c-4d98-b50a-3e7d537a63e8)   
 [Linguaggio Entity SQL](../../../../../docs/framework/data/adonet/ef/language-reference/entity-sql-language.md)