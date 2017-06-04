---
title: "Procedura: intercettare messaggi del servizio dati (WCF Data Services) | Microsoft Docs"
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
  - "intercettori di query [WCF Data Services]"
  - "WCF Data Services, personalizzazione"
ms.assetid: 24b9df1b-b54b-4795-a033-edf333675de6
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# Procedura: intercettare messaggi del servizio dati (WCF Data Services)
Con [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] è possibile intercettare i messaggi di richiesta per l'aggiunta di logica personalizzata a un'operazione.  Per intercettare un messaggio, si usano metodi attribuiti in modo speciale nel servizio dati.  Per altre informazioni, vedere [Intercettori](../../../../docs/framework/data/wcf/interceptors-wcf-data-services.md).  
  
 Nell'esempio riportato in questo argomento viene usato il servizio dati Northwind di esempio.  Questo servizio viene creato al completamento della [Guida rapida di WCF Data Services](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md).  
  
### Per definire un intercettore di query per il set di entità Orders  
  
1.  Nel progetto del servizio dati Northwind aprire il file Northwind.svc.  
  
2.  Nella tabella codici per la classe `Northwind` aggiungere l'istruzione `using` riportata di seguito \(`Imports` in Visual Basic\).  
  
     [!code-csharp[Astoria Northwind Service#UsingLinqExpressions](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind service/cs/northwind2.svc.cs#usinglinqexpressions)]
     [!code-vb[Astoria Northwind Service#UsingLinqExpressions](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind service/vb/northwind2.svc.vb#usinglinqexpressions)]  
  
3.  Nella classe `Northwind` definire un metodo dell'operazione del servizio denominato `OnQueryOrders` nel modo seguente:  
  
     [!code-csharp[Astoria Northwind Service#QueryInterceptorDef](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind service/cs/northwind2.svc.cs#queryinterceptordef)]
     [!code-vb[Astoria Northwind Service#QueryInterceptorDef](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind service/vb/northwind2.svc.vb#queryinterceptordef)]  
  
### Per definire un intercettore di modifiche per il set di entità Products  
  
1.  Nel progetto del servizio dati Northwind aprire il file Northwind.svc.  
  
2.  Nella classe `Northwind` definire un metodo dell'operazione del servizio denominato `OnChangeProducts` nel modo seguente:  
  
     [!code-csharp[Astoria Northwind Service#ChangeInterceptorDef](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind service/cs/northwind2.svc.cs#changeinterceptordef)]
     [!code-vb[Astoria Northwind Service#ChangeInterceptorDef](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind service/vb/northwind2.svc.vb#changeinterceptordef)]  
  
## Esempio  
 In questo esempio viene definito un metodo intercettore di query per il set di entità `Orders` che restituisce un'espressione lambda.  Questa espressione contiene un delegato che filtra gli `Orders` richiesti in base ai `Customers` correlati che presentano un nome di contatto specifico.  Il nome viene a sua volta determinato in base all'utente che lo richiede.  In questo esempio si presuppone che il servizio dati sia ospitato all'interno di un'applicazione Web ASP.NET che usa WCF e che l'autenticazione è abilitata.  La classe <xref:System.Web.HttpContext> viene usata per recuperare il principio della richiesta corrente.  
  
 [!code-csharp[Astoria Northwind Service#QueryInterceptor](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind service/cs/northwind2.svc.cs#queryinterceptor)]
 [!code-vb[Astoria Northwind Service#QueryInterceptor](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind service/vb/northwind2.svc.vb#queryinterceptor)]  
  
## Esempio  
 In questo esempio viene definito un metodo intercettore di modifiche per il set di entità `Products`.  Questo metodo convalida l'input per il servizio per un'operazione <xref:System.Data.Services.UpdateOperations> o <xref:System.Data.Services.UpdateOperations> e genera un'eccezione quando una modifica viene apportata a un prodotto non più disponibile.  Blocca inoltre l'eliminazione di prodotti come operazione non supportata.  
  
 [!code-csharp[Astoria Northwind Service#ChangeInterceptor](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind service/cs/northwind2.svc.cs#changeinterceptor)]
 [!code-vb[Astoria Northwind Service#ChangeInterceptor](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind service/vb/northwind2.svc.vb#changeinterceptor)]  
  
## Vedere anche  
 [Procedura: definire un'operazione del servizio](../../../../docs/framework/data/wcf/how-to-define-a-service-operation-wcf-data-services.md)   
 [Definizione di WCF Data Services](../../../../docs/framework/data/wcf/defining-wcf-data-services.md)