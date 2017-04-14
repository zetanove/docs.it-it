---
title: "Procedura: determinare il numero di entit&#224; restituite da una query (WCF Data Services) | Microsoft Docs"
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
  - "WCF Data Services, conteggio righe"
ms.assetid: 03d41a82-df95-40ac-8439-a6c327d37ba8
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# Procedura: determinare il numero di entit&#224; restituite da una query (WCF Data Services)
Con [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] è possibile determinare il numero di entità specificate nel set di entità dall'URI di una query.  Il conteggio può essere incluso insieme al risultato della query o come valore integer.  Per altre informazioni, vedere [Esecuzione di query sul servizio dati](../../../../docs/framework/data/wcf/querying-the-data-service-wcf-data-services.md).  
  
 Nell'esempio riportato in questo argomento vengono usati il servizio dati Northwind di esempio e le classi del servizio dati client generate automaticamente.  Questo servizio e le classi di dati client vengono creati al completamento della [Guida rapida di WCF Data Services](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md).  
  
## Esempio  
 In questo esempio viene eseguita una query dopo avere chiamato il metodo <xref:System.Data.Services.Client.DataServiceQuery%601.IncludeTotalCount%2A>.  La proprietà <xref:System.Data.Services.Client.QueryOperationResponse%601.TotalCount%2A> restituisce il numero di entità nel set di entità `Customers`.  
  
 [!code-csharp[Astoria Northwind Client#CountAllCustomers](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#countallcustomers)]
 [!code-vb[Astoria Northwind Client#CountAllCustomers](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#countallcustomers)]  
  
## Esempio  
 In questo esempio viene chiamato il metodo <xref:System.Linq.Enumerable.Count%2A> per restituire solo un valore integer che corrisponde al numero di entità nel set di entità `Customers`.  
  
 [!code-csharp[Astoria Northwind Client#CountAllCustomersValueOnly](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#countallcustomersvalueonly)]
 [!code-vb[Astoria Northwind Client#CountAllCustomersValueOnly](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#countallcustomersvalueonly)]  
  
## Vedere anche  
 [Esecuzione di query sul servizio dati](../../../../docs/framework/data/wcf/querying-the-data-service-wcf-data-services.md)