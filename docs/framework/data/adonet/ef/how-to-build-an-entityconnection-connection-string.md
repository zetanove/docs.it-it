---
title: "Procedura: compilare una stringa di connessione EntityConnection | Microsoft Docs"
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
ms.assetid: 5bd1a748-3df7-4d0a-a607-14f25e3175e9
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Procedura: compilare una stringa di connessione EntityConnection
In questo argomento viene fornito un esempio di come compilare un oggetto <xref:System.Data.EntityClient.EntityConnection>.  
  
### Per eseguire il codice in questo esempio  
  
1.  Aggiungere [AdventureWorks Sales Model](http://msdn.microsoft.com/it-it/f16cd988-673f-4376-b034-129ca93c7832) al progetto e configurare il progetto per l'uso di [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)].  Per altre informazioni, vedere [How to: Use the Entity Data Model Wizard](http://msdn.microsoft.com/it-it/dadb058a-c5d9-4c5c-8b01-28044112231d).  
  
2.  Nella tabella codici per l'applicazione aggiungere le istruzioni `using` seguenti \(`Imports` in Visual Basic\):  
  
     [!code-csharp[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#namespaces)]
     [!code-vb[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#namespaces)]  
  
## Esempio  
 Nell'esempio seguente viene inizializzato l'oggetto <xref:System.Data.SqlClient.SqlConnectionStringBuilder?displayProperty=fullName> per il provider sottostante, quindi viene inizializzato l'oggetto <xref:System.Data.EntityClient.EntityConnectionStringBuilder?displayProperty=fullName>, che viene passato al costruttore di <xref:System.Data.EntityClient.EntityConnection>.  
  
 [!code-csharp[DP EntityServices Concepts#BuildingConnectionStringWithEntityCommand](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#buildingconnectionstringwithentitycommand)]
 [!code-vb[DP EntityServices Concepts#BuildingConnectionStringWithEntityCommand](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#buildingconnectionstringwithentitycommand)]  
  
## Vedere anche  
 [How to: Use EntityConnection with an Object Context](http://msdn.microsoft.com/it-it/2140fe7b-b88b-47c8-a749-d7f142eb1080)   
 [Provider EntityClient per Entity Framework](../../../../../docs/framework/data/adonet/ef/entityclient-provider-for-the-entity-framework.md)