---
title: "Procedura: abilitare l&#39;accesso al servizio dati (WCF Data Services) | Microsoft Docs"
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
  - "WCF Data Services, configurazione"
ms.assetid: 3d830bcd-32b4-4f26-9287-d58a071452c6
caps.latest.revision: 3
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 3
---
# Procedura: abilitare l&#39;accesso al servizio dati (WCF Data Services)
In [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] è necessario concedere in modo esplicito l'accesso alle risorse esposte da un servizio dati.  In altre parole, dopo aver creato un nuovo servizio dati, è necessario fornire in modo esplicito l'accesso alle singole risorse come set di entità.  In questo argomento viene illustrato come abilitare l'accesso in lettura e in scrittura a cinque dei set di entità nel servizio dati Northwind creato al completamento della [guida rapida](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md). Poiché l'enumerazione <xref:System.Data.Services.EntitySetRights> viene definita tramite <xref:System.FlagsAttribute>, è possibile usare un operatore logico OR per specificare più autorizzazioni per un singolo set di entità.  
  
> [!NOTE]
>  I client che possono accedere all'applicazione ASP.NET saranno inoltre in grado di accedere alle risorse esposte dal servizio dati.  Per impedire l'accesso non autorizzato alle risorse in un servizio dati di produzione, è inoltre necessario proteggere l'applicazione stessa.  Per altre informazioni, vedere [NIB: ASP.NET Security](http://msdn.microsoft.com/it-it/04b37532-18d9-40b4-8e5f-ee09a70b311d).  
  
### Per abilitare l'accesso al servizio dati  
  
-   Nel codice per il servizio dati sostituire il codice segnaposto nella funzione `InitializeService` con il codice seguente:  
  
     [!code-csharp[Astoria Quickstart Service#AllReadConfig](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria quickstart service/cs/northwind.svc.cs#allreadconfig)]
     [!code-vb[Astoria Quickstart Service#AllReadConfig](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria quickstart service/vb/northwind.svc.vb#allreadconfig)]  
  
     In questo modo i client saranno in grado di accedere in lettura e scrittura ai set di entità `Orders` e `Order_Details` e solo in lettura ai set di entità `Customers`.  
  
## Vedere anche  
 [Procedura: sviluppare un servizio WCF in esecuzione in IIS](../../../../docs/framework/data/wcf/how-to-develop-a-wcf-data-service-running-on-iis.md)   
 [Configurazione del servizio dati](../../../../docs/framework/data/wcf/configuring-the-data-service-wcf-data-services.md)