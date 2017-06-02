---
title: "Procedura: creare un&#39;applicazione Windows Presentation Framework asincrona (WCF Data Services) | Microsoft Docs"
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
  - "WCF Data Services, operazioni asincrone"
ms.assetid: 834614df-1427-4839-b0be-90f68e5afffd
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# Procedura: creare un&#39;applicazione Windows Presentation Framework asincrona (WCF Data Services)
Con [!INCLUDE[ssAstoria](../../../../includes/ssastoria-md.md)] è possibile associare i dati ottenuti da un servizio dati a elementi dell'interfaccia utente di un'applicazione Windows Presentation Framework \(WPF\).  Per altre informazioni, vedere [Associazione di dati a controlli](../../../../docs/framework/data/wcf/binding-data-to-controls-wcf-data-services.md). È inoltre possibile eseguire operazioni sul servizio dati in modo asincrono, consentendo all'applicazione di continuare a rispondere mentre è in attesa di una risposta a una richiesta del servizio dati.  Per accedere al servizio dati in modo asincrono, è necessario disporre di applicazioni per Silverlight.  Per altre informazioni, vedere [Operazioni asincrone](../../../../docs/framework/data/wcf/asynchronous-operations-wcf-data-services.md).  
  
 In questo argomento viene illustrato come accedere in modo asincrono a un servizio dati e associare i risultati agli elementi di un'applicazione WPF.  Negli esempi riportati in questo argomento vengono usati il servizio dati Northwind di esempio e le classi del servizio dati client generate automaticamente.  Questo servizio e le classi di dati client vengono creati al completamento della [Guida rapida di WCF Data Services](../../../../docs/framework/data/wcf/quickstart-wcf-data-services.md).  
  
## Esempio  
 Tramite il codice XAML seguente viene definita la finestra dell'applicazione WPF.  
  
 [!code-xml[Astoria Northwind Client#WpfDataBindingAsyncXaml](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/customerordersasync.xaml#wpfdatabindingasyncxaml)]  
  
## Esempio  
 La pagina code\-behind seguente per il file XAML esegue una query asincrona usando il servizio dati e associa i risultati agli elementi nella finestra WPF.  
  
 [!code-csharp[Astoria Northwind Client#WpfDataBindingAsync](../../../../samples/snippets/csharp/VS_Snippets_Misc/astoria northwind client/cs/customerordersasync.xaml.cs#wpfdatabindingasync)]
 [!code-vb[Astoria Northwind Client#WpfDataBindingAsync](../../../../samples/snippets/visualbasic/VS_Snippets_Misc/astoria northwind client/vb/customerordersasync.xaml.vb#wpfdatabindingasync)]  
  
## Vedere anche  
 [Libreria client WCF Data Services](../../../../docs/framework/data/wcf/wcf-data-services-client-library.md)