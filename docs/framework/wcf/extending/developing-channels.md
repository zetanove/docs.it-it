---
title: "Sviluppo di canali | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0513af9f-a0c2-457b-9a50-5b6bfee48513
caps.latest.revision: 17
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 17
---
# Sviluppo di canali
Per sviluppare un protocollo o un canale di trasporto che possa essere utilizzato con il livello dell'applicazione [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] sono necessari vari passaggi.In questo argomento vengono illustrati tali passaggi con rimandi agli argomenti specifici per ulteriori informazioni.Per comprendere il modello dei canali e i vari tipi menzionati in questo argomento, vedere [Panoramica sul modello dei canali](../../../../docs/framework/wcf/extending/channel-model-overview.md).Per un esempio di un canale di trasporto completo, vedere [Trasporto UDP](../../../../docs/framework/wcf/samples/transport-udp.md).  
  
## Elenco delle attività di sviluppo di un canale  
 I passaggi per creare un canale definito dall'utente sono i seguenti.Per tutti i canali è necessario:  
  
1.  Definire quale modello di scambio dei messaggi del canale \(<xref:System.ServiceModel.Channels.IOutputChannel>, <xref:System.ServiceModel.Channels.IInputChannel>, <xref:System.ServiceModel.Channels.IDuplexChannel>, <xref:System.ServiceModel.Channels.IRequestChannel> o <xref:System.ServiceModel.Channels.IReplyChannel>\) verrà supportato dalle interfacce <xref:System.ServiceModel.Channels.IChannelFactory> e <xref:System.ServiceModel.Channels.IChannelListener> e se supporterà le variazioni con sessione di tali interfacce.Per informazioni dettagliate, vedere [Scelta di un modello di scambio dei messaggi](../../../../docs/framework/wcf/extending/choosing-a-message-exchange-pattern.md).  
  
2.  Creare una channel factory e un listener di canale \(<xref:System.ServiceModel.Channels.IChannelFactory> e <xref:System.ServiceModel.Channels.IChannelListener>\) che supportano il modello di scambio dei messaggi.Per informazioni dettagliate sullo sviluppo di channel factory, vedere [Client: channel factory e canali](../../../../docs/framework/wcf/extending/client-channel-factories-and-channels.md).Per informazioni dettagliate sullo sviluppo di listener di canale, vedere [Servizio: listener del canale e canali](../../../../docs/framework/wcf/extending/service-channel-listeners-and-channels.md).  
  
3.  Garantire che eventuali eccezioni specifiche della rete vengano normalizzate in <xref:System.TimeoutException?displayProperty=fullName> o nella classe derivata appropriata di <xref:System.ServiceModel.CommunicationException>.Per informazioni dettagliate, vedere [Gestione di eccezioni ed errori](../../../../docs/framework/wcf/extending/handling-exceptions-and-faults.md).  
  
4.  Per abilitare l'utilizzo dal livello dell'applicazione, aggiungere una classe <xref:System.ServiceModel.Channels.BindingElement> che aggiunge il canale personalizzato a un stack di canali.Per ulteriori informazioni, vedere [Creazione di una classe BindingElement](../../../../docs/framework/wcf/extending/creating-a-bindingelement.md).  
  
 Per abilitare un supporto più completo a livello dell'applicazione, sono necessari i passaggi aggiuntivi seguenti:  
  
1.  Aggiungere una sezione di estensione degli elementi di associazione per esporre il nuovo elemento di associazione al sistema di configurazione.Per ulteriori informazioni, vedere [Supporto di configurazione e metadati](../../../../docs/framework/wcf/extending/configuration-and-metadata-support.md).  
  
2.  Aggiungere le estensioni dei metadati per comunicare le funzionalità agli altri endpoint.Per ulteriori informazioni, vedere [Supporto di configurazione e metadati](../../../../docs/framework/wcf/extending/configuration-and-metadata-support.md).  
  
3.  Aggiungere un'associazione che preconfigura uno stack di elementi di associazione secondo un profilo ben definito.Per ulteriori informazioni, vedere [Creazione di associazioni definite dall'utente](../../../../docs/framework/wcf/extending/creating-user-defined-bindings.md).  
  
4.  Aggiungere una sezione dell'associazione e un elemento di configurazione dell'associazione per esporre l'associazione al sistema di configurazione.Per ulteriori informazioni, vedere [Supporto di configurazione e metadati](../../../../docs/framework/wcf/extending/configuration-and-metadata-support.md).  
  
## Vedere anche  
 [Estensione delle associazioni](../../../../docs/framework/wcf/extending/extending-bindings.md)