---
title: "Procedura: test del proxy di individuazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d96e3fa2-3c42-4e5d-8244-2694081bdc32
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Procedura: test del proxy di individuazione
Di seguito viene illustrato il quarto di quattro argomenti che indica come implementare un proxy di individuazione.  Nell'argomento precedente, [Procedura: implementare un'applicazione client che utilizza il proxy di individuazione per cercare un servizio](../../../../docs/framework/wcf/feature-details/client-app-discovery-proxy-to-find-a-service.md), è stata implementata un'applicazione client di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] che usa il proxy di individuazione per cercare un servizio e chiamarlo.  In questo argomento viene descritto come verificare che il proxy di individuazione, il servizio e l'applicazione client funzionino come previsto.  
  
### Eseguire il proxy di individuazione  
  
1.  Aprire un prompt dei comandi come amministratore.  
  
2.  È possibile che venga visualizzata una finestra di dialogo con il testo seguente: Windows Firewall ha bloccato alcune funzionalità del programma.  Se viene visualizzato questo messaggio, fare clic sul pulsante **Sblocca**.  
  
3.  All'interno del prompt dei comandi eseguire il proxy di individuazione \(DiscoveryProxy.exe\).  
  
4.  Nell'applicazione viene visualizzato il testo seguente: `Proxy started. Hit Enter to exit`.  
  
### Eseguire il servizio individuabile  
  
1.  Aprire un prompt dei comandi come amministratore.  
  
2.  Al prompt dei comandi eseguire il servizio individuabile Service.exe.  
  
3.  In DiscoveryProxy.exe viene visualizzato il testo seguente: `******* Adding the following service: ** [Service Contract Name] ** [Service Endpoint Addr] 3.******* Done *******` .  
  
### Eseguire l'applicazione client  
  
1.  Aprire un prompt dei comandi.  
  
2.  Al prompt dei comandi eseguire l'applicazione client.exe.  
  
3.  Dopo alcuni secondi nell'applicazione client viene visualizzato il testo seguente: Connessione a \[Endpoint\-servizio\] in corso.  
  
4.  In Service.exe viene quindi visualizzato il testo seguente: Greeting request received, I will respond.  
  
5.  In Client.exe viene quindi visualizzato il testo seguente: Hello Client\!  
  
### Chiudere le applicazioni  
  
1.  Chiudere l'applicazione client.  
  
2.  Chiudere il servizio.  Il proxy di individuazione visualizza il testo seguente: `******* Removing the following service: ** [Service Contract Name] ** [Service Endpoint Addr] 2.3.******* Done *******`.  
  
3.  Chiudere il proxy di individuazione  
  
## Vedere anche  
 [Panoramica di WCF Discovery](../../../../docs/framework/wcf/feature-details/wcf-discovery-overview.md)   
 [Procedura: implementare un proxy di individuazione](../../../../docs/framework/wcf/feature-details/how-to-implement-a-discovery-proxy.md)   
 [Procedura: implementare un servizio individuabile che esegue la registrazione al proxy di individuazione](../../../../docs/framework/wcf/feature-details/discoverable-service-that-registers-with-the-discovery-proxy.md)   
 [Procedura: implementare un'applicazione client che utilizza il proxy di individuazione per cercare un servizio](../../../../docs/framework/wcf/feature-details/client-app-discovery-proxy-to-find-a-service.md)