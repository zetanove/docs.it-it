---
title: "Procedura: eseguire una stored procedure con parametri utilizzando EntityCommand | Microsoft Docs"
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
ms.assetid: 4f5639bf-bb7f-4982-bb1d-c7caa4348888
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Procedura: eseguire una stored procedure con parametri utilizzando EntityCommand
In questo argomento viene mostrato come eseguire una stored procedure con parametri usando la classe <xref:System.Data.EntityClient.EntityCommand>.  
  
### Per eseguire il codice in questo esempio  
  
1.  Aggiungere [School Model](http://msdn.microsoft.com/it-it/859a9587-81ea-4a45-9bc0-f8d330e1adac) al progetto e configurare il progetto per l'uso di [!INCLUDE[adonet_ef](../../../../../includes/adonet-ef-md.md)].  Per altre informazioni, vedere [How to: Use the Entity Data Model Wizard](http://msdn.microsoft.com/it-it/dadb058a-c5d9-4c5c-8b01-28044112231d).  
  
2.  Nella tabella codici per l'applicazione aggiungere le istruzioni `using` seguenti \(`Imports` in Visual Basic\):  
  
     [!code-csharp[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#namespaces)]
     [!code-vb[DP EntityServices Concepts#Namespaces](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#namespaces)]  
  
3.  Importare la stored procedure `GetStudentGrades` e specificare entità `CourseGrade` come tipo restituito.  Per informazioni sull'importazione di una stored procedure, vedere [How to: Import a Stored Procedure](http://msdn.microsoft.com/it-it/24e68bf4-bd6d-428d-bc35-92d7b8e3736d).  
  
## Esempio  
 Nel codice seguente viene eseguita la stored procedure `GetStudentGrades`, dove `StudentId` è un parametro obbligatorio.  I risultati vengono quindi letti da <xref:System.Data.EntityClient.EntityDataReader>.  
  
 [!code-csharp[DP EntityServices Concepts#StoredProcWithEntityCommand](../../../../../samples/snippets/csharp/VS_Snippets_Data/dp entityservices concepts/cs/source.cs#storedprocwithentitycommand)]
 [!code-vb[DP EntityServices Concepts#StoredProcWithEntityCommand](../../../../../samples/snippets/visualbasic/VS_Snippets_Data/dp entityservices concepts/vb/source.vb#storedprocwithentitycommand)]  
  
## Vedere anche  
 [Provider EntityClient per Entity Framework](../../../../../docs/framework/data/adonet/ef/entityclient-provider-for-the-entity-framework.md)