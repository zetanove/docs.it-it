---
title: "Trasporti in Windows Communication Foundation | Microsoft Docs"
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
  - "trasporti [WCF]"
  - "WCF, trasporti"
  - "Windows Communication Foundation, trasporti"
ms.assetid: 005c894b-af70-48aa-a1c1-c99338083c27
caps.latest.revision: 18
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 18
---
# Trasporti in Windows Communication Foundation
Il livello di trasporto è al livello più basso dello stack dei canali.I trasporti principali utilizzati in [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] sono HTTP, Https, TCP e named pipe.Negli argomenti di questa sezione vengono fornite informazioni sulla scelta fra questi trasporti, la configurazione del trasporto e l'impostazione delle proprietà di ottimizzazione.  
  
 In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] sono inclusi trasporti aggiuntivi.Per informazioni sul trasporto del sistema di accodamento messaggi \(detto anche MSMQ\), vedere [Code e sessioni affidabili](../../../../docs/framework/wcf/feature-details/queues-and-reliable-sessions.md).Per informazioni sul trasporto peer\-to\-peer, vedere [Rete peer\-to\-peer](../../../../docs/framework/wcf/feature-details/peer-to-peer-networking.md).  
  
## In questa sezione  
 [Scelta di un trasporto](../../../../docs/framework/wcf/feature-details/choosing-a-transport.md)  
 Descrive i tre trasporti principali con gli aspetti da considerare in fase di selezione.  
  
 [Scelta di un codificatore di messaggi](../../../../docs/framework/wcf/feature-details/choosing-a-message-encoder.md)  
 Descrive i fattori da considerare nella scelta di un elemento di associazione di codifica dei messaggi.  
  
 [Trasferimento dei messaggi di flusso](../../../../docs/framework/wcf/feature-details/streaming-message-transfer.md)  
 Descrive come configurare il livello del trasporto per l'esecuzione del flusso.  
  
 [Configurazione di HTTP e HTTPS](../../../../docs/framework/wcf/feature-details/configuring-http-and-https.md)  
 Descrive come configurare gli elementi di associazione del trasporto HTTP e HTTPS.  
  
 [Procedura: Sostituire la prenotazione URL WCF con una prenotazione limitata](../../../../docs/framework/wcf/feature-details/how-to-replace-the-wcf-url-reservation-with-a-restricted-reservation.md)  
 Descrive come utilizzare le prenotazioni limitate URL di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
 [Quote dei trasporti](../../../../docs/framework/wcf/feature-details/transport-quotas.md)  
 Vengono fornite considerazioni per l'impostazione delle quote disponibili nel livello di trasporto.  
  
 [Utilizzo di conversioni NAT e firewall](../../../../docs/framework/wcf/feature-details/working-with-nats-and-firewalls.md)  
 Descrive come configurare il livello di trasporto quando i messaggi vengono inviati o ricevuti attraverso un firewall o quando si utilizza la conversione degli indirizzi di rete \(NAT\).  
  
 [Condivisione delle porte Net.TCP](../../../../docs/framework/wcf/feature-details/net-tcp-port-sharing.md)  
 Descrive come utilizzare il componente di condivisione porte Net.TCP di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
## Riferimenti  
 <xref:System.ServiceModel.Channels.HttpTransportBindingElement>  
  
 <xref:System.ServiceModel.Channels.HttpsTransportBindingElement>  
  
 <xref:System.ServiceModel.Channels.TcpTransportBindingElement>  
  
 <xref:System.ServiceModel.Channels.NamedPipeTransportBindingElement>  
  
## Sezioni correlate  
 [Associazioni](../../../../docs/framework/wcf/feature-details/bindings.md)  
  
 [Estensione delle associazioni](../../../../docs/framework/wcf/extending/extending-bindings.md)