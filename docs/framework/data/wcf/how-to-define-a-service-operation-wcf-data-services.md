---
title: "Procedura: definire un&#39;operazione del servizio (WCF Data Services) | Microsoft Docs"
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
  - "operazioni del servizio [WCF Data Services]"
  - "WCF Data Services, operazioni del servizio"
ms.assetid: dfcd3cb1-2f07-4d0b-b16a-6b056c4f45fa
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# Procedura: definire un&#39;operazione del servizio (WCF Data Services)
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] espone i metodi definiti nel server come operazioni del servizio.  Le operazioni del servizio consentono a un servizio dati di fornire l'accesso tramite un URI a un metodo definito nel server.  Per definire un'operazione del servizio, applicare l'attributo \[`WebGet]` or `[WebInvoke]` al metodo.  Per supportare gli operatori di query, l'operazione del servizio deve restituire un'istanza di <xref:System.Linq.IQueryable%601>.  L'accesso all'origine dati sottostante da parte delle operazioni del servizio può essere eseguito tramite la proprietà <xref:System.Data.Services.DataService%601.CurrentDataSource%2A> su <xref:System.Data.Services.DataService%601>. Per altre informazioni, vedere [Operazioni del servizio](../../../../docs/framework/data/wcf/service-operations-wcf-data-services.md).  
  
 Nell'esempio incluso in questo argomento viene definita un'operazione del servizio denominata `GetOrdersByCity` che restituisce un'istanza di <xref:System.Linq.IQueryable%601> filtrata relativa a `Orders` e agli oggetti `Order_Details` correlati.  Nell'esempio viene eseguito l'accesso all'istanza di <xref:System.Data.Objects.ObjectContext> che rappresenta l'origine dati per il servizio dati Northwind di esempio.  Questo servizio viene creato al completamento della [Guida rapida di WCF Data Services](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md).  
  
### Per definire un'operazione del servizio nel servizio dati Northwind  
  
1.  Nel progetto del servizio dati Northwind aprire il file Northwind.svc.  
  
2.  Nella classe `Northwind` definire un metodo dell'operazione del servizio denominato `GetOrdersByCity` nel modo seguente:  
  
     [!code-csharp[Astoria Northwind Service#ServiceOperationDef](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind service/cs/northwind2.svc.cs#serviceoperationdef)]
     [!code-vb[Astoria Northwind Service#ServiceOperationDef](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind service/vb/northwind2.svc.vb#serviceoperationdef)]  
  
3.  Nel metodo `InitializeService` della classe `Northwind` aggiungere il codice seguente per abilitare l'accesso all'operazione del servizio:  
  
     [!code-csharp[Astoria Northwind Service#ServiceOperationConfig](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind service/cs/northwind2.svc.cs#serviceoperationconfig)]
     [!code-vb[Astoria Northwind Service#ServiceOperationConfig](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind service/vb/northwind2.svc.vb#serviceoperationconfig)]  
  
### Per eseguire una query sull'operazione del servizio GetOrdersByCity  
  
-   In un browser immettere uno degli URI indicati di seguito per richiamare l'operazione del servizio definita nell'esempio seguente:  
  
    -   `http://localhost:12345/Northwind.svc/GetOrdersByCity?city='London'`  
  
    -   `http://localhost:12345/Northwind.svc/GetOrdersByCity?city='London'&$top=2`  
  
    -   `http://localhost:12345/Northwind.svc/GetOrdersByCity?city='London'&$expand=Order_Details&$orderby=RequiredDate desc`  
  
## Esempio  
 Nell'esempio seguente viene implementa un'operazione del servizio denominata `GetOrderByCity` nel servizio dati Northwind.  Questa operazione usa ADO.NET Entity Framework per restituire un set di oggetti `Orders` e di oggetti `Order_Details` correlati come istanza di <xref:System.Linq.IQueryable%601> in base al nome di città specificato.  
  
> [!NOTE]
>  Gli operatori di query sono supportati su questo endpoint dell'operazione del servizio in quanto il metodo restituisce un'istanza di <xref:System.Linq.IQueryable%601>.  
  
 [!code-csharp[Astoria Northwind Service#ServiceOperation](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind service/cs/northwind2.svc.cs#serviceoperation)]
 [!code-vb[Astoria Northwind Service#ServiceOperation](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind service/vb/northwind2.svc.vb#serviceoperation)]  
  
## Vedere anche  
 [Definizione di WCF Data Services](../../../../docs/framework/data/wcf/defining-wcf-data-services.md)