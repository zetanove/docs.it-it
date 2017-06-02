---
title: "Procedura: eseguire la migrazione del codice per client di servizi Web ASP.NET a Windows Communication Foundation | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2e0a22a7-e1d5-4718-8997-4319a7cd9027
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Procedura: eseguire la migrazione del codice per client di servizi Web ASP.NET a Windows Communication Foundation
Nella procedura seguente vengono descritti i passaggi generali da eseguire per la migrazione del codice per client di servizi Web ASP.NET a [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
## Procedura  
  
#### Per eseguire la migrazione del codice per client di servizi Web ASP.NET a WCF  
  
1.  Assicurarsi che esista un set completo di test per il client.  
  
2.  Utilizzare Visual Studio 2005 per aggiornare l'applicazione client a .NET 2.0.Eseguire il set di test.  
  
3.  Rimuovere il codice del client ASP.NET dal progetto client.Tale codice è presente nei moduli generati tramite lo strumento WSDL.exe.  
  
4.  Generare il codice del client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizzando [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md).Aggiungere il codice al progetto client ed eseguire il merge del risultato della configurazione nel file di configurazione esistente del client.  
  
5.  Compilare l'applicazione.Correggere gli errori di compilazione sostituendo i riferimenti ai tipi di client ASP.NET precedenti con i nuovi tipi di client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
6.  Eseguire il set di test.  
  
## Vedere anche  
 [Procedura: eseguire la migrazione del codice di un servizio Web ASP.NET a Windows Communication Foundation](../../../../docs/framework/wcf/feature-details/migrate-asp-net-web-service-to-wcf.md)