---
title: "Procedura: eseguire query in un batch (WCF Data Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-oob"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "WCF Data Services, richieste batch"
ms.assetid: 3b4db7df-bd33-43a1-8ea4-63a18e131f97
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# Procedura: eseguire query in un batch (WCF Data Services)
Tramite la libreria client di [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] è possibile eseguire più query sul servizio dati in un unico batch.  Per altre informazioni, vedere [Invio in batch di operazioni](../../../../docs/framework/data/wcf/batching-operations-wcf-data-services.md).  
  
 Nell'esempio riportato in questo argomento vengono usati il servizio dati Northwind di esempio e le classi del servizio dati client generate automaticamente.  Questo servizio e le classi di dati client vengono creati al completamento della [Guida rapida di WCF Data Services](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md).  
  
## Esempio  
 Nell'esempio seguente viene illustrato come chiamare il metodo <xref:Microsoft.SqlServer.ReportingServices.ReportingService.ExecuteBatch%2A> per eseguire una matrice di oggetti <xref:System.Data.Services.Client.DataServiceRequest%601> contenente query che restituiscono gli oggetti `Customers` e `Products` dal servizio dati Northwind.  La raccolta di oggetti <xref:System.Data.Services.Client.QueryOperationResponse%601> inclusa nell'oggetto <xref:System.Data.Services.Client.DataServiceResponse> restituito viene enumerata, allo stesso modo della raccolta di oggetti inclusa in ogni oggetto <xref:System.Data.Services.Client.QueryOperationResponse%601>.  
  
 [!code-csharp[Astoria Northwind Client#BatchQuery](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#batchquery)]
 [!code-vb[Astoria Northwind Client#BatchQuery](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#batchquery)]  
  
## Vedere anche  
 [Libreria client WCF Data Services](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md)