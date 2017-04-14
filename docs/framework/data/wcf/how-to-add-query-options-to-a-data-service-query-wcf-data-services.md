---
title: "Procedura: aggiungere opzioni di query a una query del servizio dati (WCF Data Services) | Microsoft Docs"
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
  - "esecuzione di query sul servizio dati [WCF Data Services]"
  - "WCF Data Services, accesso ai dati"
  - "WCF Data Services, esecuzione di query"
ms.assetid: e4258526-557e-4e96-91e1-2175400c7c8f
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# Procedura: aggiungere opzioni di query a una query del servizio dati (WCF Data Services)
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] consente di eseguire query su un servizio dati da un'applicazione client basata su .NET Framework usando le classi del servizio dati client generate. Il modo più semplice per conseguire questo risultato consiste nel creare un'espressione di query LINQ \(Language Integrated Query\) con le opzioni query desiderate.  È inoltre possibile chiamare una serie di metodi di query LINQ per creare una query equivalente.  È infine possibile usare il metodo <xref:System.Data.Services.Client.DataServiceQuery%601.AddQueryOption%2A> per aggiungere opzioni query a una query.  In ciascuno di questi casi l'URI generato dal client include il set di entità richiesto con le opzioni query selezionate applicate.  Per altre informazioni, vedere [Esecuzione di query sul servizio dati](../../../../docs/framework/data/wcf/querying-the-data-service-wcf-data-services.md).  
  
 Nell'esempio riportato in questo argomento vengono usati il servizio dati Northwind di esempio e le classi del servizio dati client generate automaticamente.  Questo servizio e le classi di dati client vengono creati al completamento della [Guida rapida di WCF Data Services](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md).  
  
## Esempio  
 Nell'esempio seguente viene illustrato come creare un'espressione di query LINQ che restituisce solo gli ordini con un costo di spedizione maggiore di 30 dollari e ordina i risultati in senso decrescente in base alla data di spedizione.  
  
 [!code-csharp[Astoria Northwind Client#AddQueryOptionsLinq](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#addqueryoptionslinq)]
 [!code-vb[Astoria Northwind Client#AddQueryOptionsLinq](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#addqueryoptionslinq)]  
  
## Esempio  
 Nell'esempio seguente viene illustrato come creare una query LINQ equivalente alla query precedente tramite i metodi di query LINQ.  
  
 [!code-csharp[Astoria Northwind Client#AddQueryOptionsLinqExpression](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#addqueryoptionslinqexpression)]
 [!code-vb[Astoria Northwind Client#AddQueryOptionsLinqExpression](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#addqueryoptionslinqexpression)]  
  
## Esempio  
 Nell'esempio seguente viene illustrato come usare il metodo <xref:System.Data.Services.Client.DataServiceQuery%601.AddQueryOption%2A> per creare un oggetto <xref:System.Data.Services.Client.DataServiceQuery%601> equivalente agli esempi precedenti.  
  
 [!code-csharp[Astoria Northwind Client#AddQueryOptions](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#addqueryoptions)]
 [!code-vb[Astoria Northwind Client#AddQueryOptions](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#addqueryoptions)]  
  
## Esempio  
 Nell'esempio seguente viene illustrato come usare l'opzione query `$orderby` per filtrare e ordinare gli oggetti Orders restituiti in base alla proprietà Freight.  
  
 [!code-csharp[Astoria Northwind Client#OrderWithFilter](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#orderwithfilter)]
 [!code-vb[Astoria Northwind Client#OrderWithFilter](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#orderwithfilter)]  
  
## Vedere anche  
 [Esecuzione di query sul servizio dati](../../../../docs/framework/data/wcf/querying-the-data-service-wcf-data-services.md)   
 [Procedura: proiettare i risultati delle query](../../../../docs/framework/data/wcf/how-to-project-query-results-wcf-data-services.md)