---
title: "Condivisione delle porte Net.TCP | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "attivazione porte [WCF]"
  - "condivisione delle porte [WCF]"
ms.assetid: f13692ee-a179-4439-ae72-50db9534eded
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# Condivisione delle porte Net.TCP
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] fornisce un nuovo protocollo di rete basato su TCP \(net.tcp:\/\/\) per la comunicazione ad alte prestazioni.  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] introduce inoltre un nuovo componente di sistema, il Servizio condivisione porte Net.Tcp, che consente la condivisione delle porte net.tcp tra più processi utente.  
  
## Informazioni generali e motivazione  
 Quando il protocollo TCP\/IP è stato introdotto per la prima volta, solo pochi protocolli di applicazione lo utilizzavano.  TCP\/IP usa numeri di porta per differenziare le applicazioni, assegnando un numero di porta univoco a 16 bit a ogni protocollo di applicazione.  Ad esempio, il traffico HTTP è oggi standardizzato sull'utilizzo del TCP sulla porta 80, l'SMTP usa il TCP sulla porta 25 e l'FTP usa il TCP sulle porte 20 e 21.  Per altre applicazioni che usano il TCP come trasporto è possibile scegliere un altro numero di porta disponibile, per convenzione o attraverso la standardizzazione formale.  
  
 L'utilizzo di numeri di porta per fare distinzioni tra le applicazioni comporta problemi di sicurezza.  I firewall sono generalmente configurati per bloccare il traffico TCP su tutte le porte, a parte alcuni punti di ingresso conosciuti, pertanto la distribuzione di un'applicazione che usa una porta non standard è spesso complicata, se non impossibile, a causa della presenza di firewall aziendali e personali.  Le applicazioni che possono comunicare su porte note standard, già consentite, riducono la superficie d'attacco esterna.  Molte applicazioni di rete usano il protocollo HTTP, poiché la maggior parte dei firewall è configurata, per impostazione predefinita, per consentire il traffico sulla porta TCP 80.  
  
 Il modello HTTP.SYS, in cui il traffico per molte applicazioni HTTP diverse viene reso multiplex su una sola porta TCP, è diventato lo standard sulla piattaforma Windows.  Questo offre un punto di controllo comune per gli amministratori dei firewall, consentendo al contempo agli sviluppatori di applicazioni di ridurre al minimo i costi di distribuzione associati alla creazione di nuove applicazioni che possono fare uso della rete.  
  
 La possibilità di condividere porte tra più applicazioni HTTP caratterizza da molto tempo Internet Information Services \(IIS\).  Tuttavia, è solo con l'introduzione di HTTP.SYS \(il listener del protocollo HTTP in modalità kernel\) con [!INCLUDE[iis601](../../../../includes/iis601-md.md)] che questa infrastruttura è stata completamente generalizzata.  In effetti, HTTP.SYS consente a processi utente arbitrari di condividere le porte TCP dedicate al traffico HTTP.  Questa capacità consente a molte applicazioni HTTP di coesistere sullo stesso computer fisico in processi isolati, distinti e nel contempo condividere l'infrastruttura di rete richiesta per inviare e ricevere il traffico su TCP sulla porta 80.  Il Servizio di condivisione porte Net.TCP consente alle applicazioni net.tcp di condividere lo stesso tipo di porta.  
  
## Architettura di condivisione delle porte  
 L'architettura di condivisione delle porte in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] ha tre componenti principali:  
  
-   Un processo di lavoro: qualsiasi processo che comunica su net.tcp:\/\/ usando porte condivise.  
  
-   Il trasporto TCP [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)]: implementa il protocollo net.tcp:\/\/.  
  
-   Il Servizio di condivisione porte Net.TCP: consente a molti processi di lavoro di condividere la stessa porta TCP.  
  
 Il Servizio di condivisione porte Net.TCP è un servizio Windows in modalità utente che accetta connessioni net.tcp:\/\/ per conto dei processi di lavoro che stabiliscono connessioni tramite esso.  Quando arriva una connessione socket, il servizio di condivisione delle porte esamina il flusso di messaggi in ingresso per ottenerne l'indirizzo di destinazione.  In base a questo indirizzo, il servizio di condivisione delle porte può instradare il flusso di dati all'applicazione che in definitiva lo elaborerà.  
  
 Quando viene aperto un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] che usa la condivisione delle porte net.tcp:\/\/, l'infrastruttura di trasporto TCP [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non apre direttamente un socket TCP nel processo dell'applicazione.  Registra, invece, l'URI \(Uniform Resource Identifier\) dell'indirizzo di base del servizio presso il Servizio di condivisione porte Net.TCP e attende che quest'ultimo ascolti i messaggi per suo conto.  Il servizio di condivisione delle porte invia i messaggi indirizzati al servizio dell'applicazione non appena arrivano.  
  
## Installazione della condivisione delle porte  
 Il Servizio di condivisione porte Net.TCP è disponibile in tutti i sistemi operativi che supportano [!INCLUDE[vstecwinfx](../../../../includes/vstecwinfx-md.md)], ma non viene attivato per impostazione predefinita.  Per motivi di sicurezza, gli amministratori devono attivare manualmente il Servizio di condivisione porte Net.TCP al primo utilizzo.  Il Servizio di condivisione porte Net.TCP espone opzioni di configurazione che consentono di modificare diverse caratteristiche dei socket di rete appartenenti al servizio stesso.  [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Procedura: attivare il servizio di condivisione delle porte Net.TCP](../../../../docs/framework/wcf/feature-details/how-to-enable-the-net-tcp-port-sharing-service.md).  
  
## Utilizzo della condivisione delle porte Net.tcp in un'applicazione  
 Il modo più semplice per usare la condivisione delle porte net.tcp:\/\/ nell'applicazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] consiste nell'esporre un servizio mediante <xref:System.ServiceModel.NetTcpBinding> e nell'attivare il Servizio di condivisione porte Net.TCP mediante la proprietà <xref:System.ServiceModel.NetTcpBinding.PortSharingEnabled%2A>.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] come effettuare questa operazione, vedere [Procedura: configurare un servizio WCF per l'utilizzo della condivisione delle porte](../../../../docs/framework/wcf/feature-details/how-to-configure-a-wcf-service-to-use-port-sharing.md).  
  
## Implicazioni di sicurezza della condivisione delle porte  
 Sebbene il Servizio di condivisione porte Net.TCP preveda un livello di elaborazione tra le applicazioni e la rete, le applicazioni che usano la condivisione delle porte dovrebbero comunque essere protette come se fossero direttamente in ascolto sulla rete.  In particolare, le applicazioni che usano la condivisione delle porte dovrebbero valutare i privilegi del processo con cui vengono eseguite.  Considerare l'ipotesi di eseguire l'applicazione usando l'account predefinito Servizio di rete, che viene eseguito con il set minimo di privilegi del processo necessari per la comunicazione di rete.  
  
## Vedere anche  
 [Configurazione del servizio di condivisione delle porte Net.TCP](../../../../docs/framework/wcf/feature-details/configuring-the-net-tcp-port-sharing-service.md)   
 [Hosting](../../../../docs/framework/wcf/feature-details/hosting.md)   
 [Procedura: configurare un servizio WCF per l'utilizzo della condivisione delle porte](../../../../docs/framework/wcf/feature-details/how-to-configure-a-wcf-service-to-use-port-sharing.md)   
 [Procedura: attivare il servizio di condivisione delle porte Net.TCP](../../../../docs/framework/wcf/feature-details/how-to-enable-the-net-tcp-port-sharing-service.md)