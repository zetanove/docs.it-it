---
title: "API Web ASP.NET e WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 08ceded3-fd9a-4467-9715-c4cbd9c7228e
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# API Web ASP.NET e WCF
WCF è il modello di programmazione unificato di Microsoft per la compilazione di applicazioni orientate ai servizi.Consente agli sviluppatori di compilare soluzioni transazionali protette e affidabili in grado di integrarsi a piattaforme diverse e interagire con investimenti esistenti.[API Web ASP.NET](http://www.asp.net/web-api) è un framework che consente di compilare servizi HTTP che soddisfano una vasta gamma di client, inclusi i browser e i dispositivi mobili.API Web ASP.NET è la piattaforma ideale per compilare applicazioni RESTful in .NET Framework.In questo argomento vengono indicate alcune linee guida utili per decidere la tecnologia che soddisfa meglio le proprie esigenze.  
  
## Scelta della tecnologia da utilizzare  
 Nella tabella seguente vengono descritte le principali funzionalità di ogni tecnologia.  
  
|WCF|API Web ASP.NET|  
|---------|---------------------|  
|Abilita i servizi di compilazione che supportano più protocolli di trasporto \(HTTP, TCP, UDP e trasporti personalizzati\) e consentono il passaggio da un protocollo all'altro.|Solo HTTP.Modello di programmazione di prima classe per HTTP. Più appropriato per l'accesso da vari browser, dispositivi mobili e così via, è un modello di ampia portata.|  
|Abilita i servizi di compilazione che supportano più codifiche \(testo, MTOM e binario\) dello stesso tipo di messaggio e consente il passaggio da una codifica all'altra.|Abilita le API Web che supportano un'ampia varietà di tipi di contenuti multimediali, ad esempio XML, JSON e così via.|  
|Supporta i servizi di compilazione con gli standard WS\-\* come la messaggistica affidabile, le transazioni, la sicurezza dei messaggi.|Utilizza il protocollo di base e i formati quali HTTP, WebSockets, SSL, JQuery, JSON e XML.Non è disponibile alcun supporto per i protocolli di livello superiore, ad esempio la messaggistica affidabile o le transazioni.|  
|Supporta i modelli di scambio dei messaggi richiesta\-risposta, unidirezionale e duplex.|HTTP è richiesta\-risposta ma i modelli aggiuntivi possono essere supportati tramite l'integrazione [SignalR](https://github.com/SignalR/SignalR) e WebSockets.|  
|I servizi SOAP WCF possono essere descritti in WSDL per permettere agli strumenti automatizzati di generare i proxy client anche per i servizi con schemi complessi.|Esistono diversi modi per descrivere un'API Web, dalla pagina della Guida HTML generata automaticamente che descrive frammenti ai metadati strutturati per API integrate OData.|  
|Viene fornito con .NET Framework.|Viene fornito con .NET Framework ma è open\-source ed è anche disponibile fuori banda come download indipendente.|  
  
 Utilizzare WCF per creare i servizi Web efficaci e sicuri accessibili da una varietà di trasporti.Utilizzare l'API Web ASP.NET per creare i servizi basati su HTTP accessibili da un'ampia varietà di client.Utilizzare l'API Web ASP.NET se si stanno creando e progettando nuovi servizi in stile REST.Sebbene WCF fornisca supporto per scrivere servizi in stile REST, il supporto per REST nell'API Web ASP.NET è più completo e tutti i futuri miglioramenti della funzionalità REST verranno introdotti nell'API Web ASP.NET.Se si dispone di un servizio WCF e si desidera esporre endpoint REST aggiuntivi, utilizzare WCF e <xref:System.ServiceModel.WebHttpBinding>.  
  
## Vedere anche  
 [Informazioni su Windows Communication Foundation](../../../docs/framework/wcf/whats-wcf.md)   
 [Concetti fondamentali di Windows Communication Foundation](../../../docs/framework/wcf/fundamental-concepts.md)   
 [WCF and ASP.NET Web API](../../../docs/framework/wcf/wcf-and-aspnet-web-api.md)