---
title: "Intercettori (WCF Data Services) | Microsoft Docs"
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
ms.assetid: e33ae8dc-8069-41d0-99a0-75ff28db7050
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# Intercettori (WCF Data Services)
[!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] consente a un'applicazione di intercettare messaggi di richiesta in modo che sia possibile aggiungere la logica personalizzata a un'operazione.  È possibile usare questa logica personalizzata per convalidare i dati nei messaggi in arrivo.  È inoltre possibile usarla per limitare ulteriormente l'ambito di una richiesta di query, inserendo ad esempio criteri di autorizzazione personalizzati per le singole richieste.  
  
 L'intercettazione viene eseguita specificando metodi attribuiti in modo specifico nel servizio dati.  Questi metodi vengono chiamati da [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] al momento appropriato durante l'elaborazione del messaggio.  Gli intercettori vengono definiti per le singole entità e, a differenza delle operazioni del servizio, i metodi dell'intercettore non accettano parametri dalla richiesta.  I metodi dell'intercettore di query, chiamati durante l'elaborazione di una richiesta GET HTTP, devono restituire un'espressione lambda che determina se un'istanza del set di entità dell'intercettore deve essere restituita nei risultati della query.  Questa espressione viene usata dal servizio dati per definire ulteriormente l'operazione richiesta.  Di seguito viene riportato un esempio di definizione di un intercettore di query.  
  
 [!code-csharp[Astoria Northwind Service#QueryInterceptorDef](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind service/cs/northwind2.svc.cs#queryinterceptordef)]
 [!code-vb[Astoria Northwind Service#QueryInterceptorDef](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind service/vb/northwind2.svc.vb#queryinterceptordef)]  
  
 Per altre informazioni, vedere [Procedura: intercettare messaggi del servizio dati](../../../../docs/framework/data/wcf/how-to-intercept-data-service-messages-wcf-data-services.md).  
  
 Gli intercettori di modifiche, chiamati durante l'elaborazione di operazioni non di query, devono restituire `void` \(`Nothing` in Visual Basic\).  I metodi dell'intercettore di modifiche devono accettare i due parametri seguenti:  
  
1.  Un parametro di un tipo compatibile con il tipo di entità del set di entità.  Quando il servizio dati richiama l'intercettore di modifiche, il valore di questo parametro riflette le informazioni sull'entità inviate dalla richiesta.  
  
2.  Un parametro di tipo <xref:System.Data.Services.UpdateOperations>.  Quando il servizio dati richiama l'intercettore di modifiche, il valore di questo parametro riflette l'operazione tentata dalla richiesta.  
  
 Di seguito viene riportato un esempio di definizione di un intercettore di modifiche.  
  
 [!code-csharp[Astoria Northwind Service#ChangeInterceptorDef](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind service/cs/northwind2.svc.cs#changeinterceptordef)]
 [!code-vb[Astoria Northwind Service#ChangeInterceptorDef](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind service/vb/northwind2.svc.vb#changeinterceptordef)]  
  
 Per altre informazioni, vedere [Procedura: intercettare messaggi del servizio dati](../../../../docs/framework/data/wcf/how-to-intercept-data-service-messages-wcf-data-services.md).  
  
 Gli attributi che seguono sono supportati per l'intercettazione.  
  
 **\[QueryInterceptor\(** *EntitySetName* **\)\]**  
 Metodi a cui è applicato l'attributo <xref:System.Data.Services.QueryInterceptorAttribute> vengono chiamati quando una richiesta GET HTTP viene ricevuta per la risorsa del set di entità di destinazione.  Questi metodi devono restituire sempre un'espressione lambda nel formato `Expression<Func<T,bool>>`.  
  
 **\[ChangeInterceptor\(** *EntitySetName* **\)\]**  
 Metodi a cui è applicato l'attributo <xref:System.Data.Services.ChangeInterceptorAttribute> vengono chiamati quando una richiesta HTTP diversa da GET viene ricevuta per la risorsa del set di entità di destinazione.  Questi metodi devono restituire sempre `void` \(`Nothing` in Visual Basic\).  
  
 Per altre informazioni, vedere [Procedura: intercettare messaggi del servizio dati](../../../../docs/framework/data/wcf/how-to-intercept-data-service-messages-wcf-data-services.md).  
  
## Vedere anche  
 [Operazioni del servizio](../../../../docs/framework/data/wcf/service-operations-wcf-data-services.md)