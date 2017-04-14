---
title: "Procedura: proiettare i risultati delle query (WCF Data Services) | Microsoft Docs"
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
  - "proiezione [WCF Data Service]"
  - "proiezioni di query [WCF Data Services]"
  - "WCF Data Services, proiezione"
  - "WCF Data Services, esecuzione di query"
ms.assetid: 474ac625-8770-43ba-8320-d3315ea9530f
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Procedura: proiettare i risultati delle query (WCF Data Services)
La proiezione fornisce un meccanismo per ridurre la quantità di dati restituiti da una query specificando che solo determinate proprietà di un'entità vengano restituite nella risposta.  È possibile eseguire proiezioni sui risultati di una query [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] usando l'opzione di query `$select` o la clausola [select](../Topic/select%20clause%20\(C%23%20Reference\).md) \([Select](../Topic/Select%20Clause%20\(Visual%20Basic\).md) in Visual Basic\) in una query LINQ.  Per altre informazioni, vedere [Esecuzione di query sul servizio dati](../../../../docs/framework/data/wcf/querying-the-data-service-wcf-data-services.md).  
  
 Nell'esempio riportato in questo argomento vengono usati il servizio dati Northwind di esempio e le classi del servizio dati client generate automaticamente.  Questo servizio e le classi di dati client vengono creati al completamento della [Guida rapida di WCF Data Services](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md).  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrata una query LINQ che proietta le entità Customers in un nuovo tipo CustomerAddress contenente solo le proprietà specifiche dell'indirizzo e la proprietà Identity.  Questa classe `CustomerAddress` viene definita nel client e attribuita in modo da essere riconosciuta come tipo di entità dalla libreria client.  
  
 [!code-csharp[Astoria Northwind Client#SelectCustomerAddress](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#selectcustomeraddress)]
 [!code-vb[Astoria Northwind Client#SelectCustomerAddress](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#selectcustomeraddress)]  
  
## Esempio  
 Nell'esempio riportato di seguito viene illustrata una query LINQ che proietta le entità Customers restituite in un nuovo tipo CustomerAddressNonEntity contenente solo le proprietà specifiche dell'indirizzo e nessuna proprietà Identity.  Questa classe `CustomerAddressNonEntity` è definita nel client e non viene attribuita come tipo di entità.  
  
 [!code-csharp[Astoria Northwind Client#SelectCustomerAddressNonEntity](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/source.cs#selectcustomeraddressnonentity)]
 [!code-vb[Astoria Northwind Client#SelectCustomerAddressNonEntity](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/source.vb#selectcustomeraddressnonentity)]  
  
## Esempio  
 Nell'esempio riportato di seguito vengono illustrate le definizioni dei tipi `CustomerAddress` `CustomerAddressNonEntity` usati negli esempi precedenti.  
  
 [!code-csharp[Astoria Northwind Client#CustomerAddressDefinition](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/customeraddress.cs#customeraddressdefinition)]
 [!code-vb[Astoria Northwind Client#CustomerAddressDefinition](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/customeraddress.vb#customeraddressdefinition)]