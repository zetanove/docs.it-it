---
title: "Confronto tra i servizi Web ASP.NET e WCF basato sullo scopo e gli standard usati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d3890278-fa9b-4902-91ea-8da73b7143cc
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Confronto tra i servizi Web ASP.NET e WCF basato sullo scopo e gli standard usati
I servizi Web ASP.NET sono stati sviluppati per creare applicazioni che inviano e ricevono messaggi usando SOAP \(Simple Object Access Protocol\) su HTTP.  La struttura dei messaggi può essere definita usando un XML Schema e viene fornito un strumento per facilitare la serializzazione dei messaggi provenienti e destinati a oggetti .NET Framework.  La tecnologia può generare automaticamente metadati per descrivere i servizi Web nel linguaggio di descrizione dei servizi Web \(WSDL, Web Services Description Language\) e viene fornito un secondo strumento per generare client per i servizi Web da WSDL.  
  
 [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] è stato progettato per consentire alle applicazioni .NET Framework di scambiare messaggi con altre entità software.  Per impostazione predefinita viene usato SOAP, ma i messaggi possono avere qualsiasi formato ed essere trasmessi mediante qualsiasi protocollo di trasporto.  La struttura dei messaggi può essere definita usando un XML Schema e sono disponibili diverse opzioni per la serializzazione dei messaggi provenienti e destinati a oggetti .NET Framework.  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] può generare automaticamente metadati per descrivere applicazioni compilate usando la tecnologia in WSDL e fornisce anche uno strumento per la generazione di client per tali applicazioni da WSDL.  
  
 Gli standard supportati dai servizi Web ASP.NET sono documentati nella pagina sui [servizi Web XML creati tramite ASP.NET](http://go.microsoft.com/fwlink/?LinkId=94872).  Un elenco più completo degli standard supportati da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] è disponibile in [Protocolli di servizi Web supportati da associazioni di interoperabilità fornite dal sistema](../../../../docs/framework/wcf/feature-details/web-services-protocols-supported-by-system-provided-interoperability-bindings.md).  
  
## Vedere anche  
 [Confronto tra servizi Web ASP.NET e WCF basato sullo sviluppo](../../../../docs/framework/wcf/feature-details/comparing-aspnet-web-services-to-wcf-based-on-development.md)