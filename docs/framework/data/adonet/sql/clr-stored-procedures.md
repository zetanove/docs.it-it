---
title: "Stored procedure CLR | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fd7eea9b-218a-4988-8c9a-8abcc6031c66
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Stored procedure CLR
Le stored procedure sono routine che non possono essere usate in espressioni scalari.  Possono restituire risultati in formato schematico e messaggi al client, eseguire chiamate di istruzioni DDL \(Data Definition Language\) e DML \(Data Manipulation Language\) nonché restituire parametri di output.  
  
> [!NOTE]
>  In Microsoft Visual Basic i parametri di output non sono supportati come in Microsoft Visual C\#.  È necessario specificare che il parametro deve essere passato tramite un riferimento e applicare l'attributo \<Out\(\)\> per rappresentare un parametro di output, come nel seguente codice:  
  
```  
Public Shared Sub ExecuteToClient( <Out()> ByRef number As Integer)  
```  
  
 Per informazioni più dettagliate, vedere la versione della documentazione online di SQL Server corrispondente alla versione di SQL Server in uso.  
  
 **Documentazione online di SQL Server**  
  
1.  [Stored procedure CLR](http://go.microsoft.com/fwlink/?LinkId=115400)  
  
## Vedere anche  
 [Creating SQL Server 2005 Objects In Managed Code](http://msdn.microsoft.com/it-it/5358a825-e19b-49aa-8214-674ce5fed1da)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)