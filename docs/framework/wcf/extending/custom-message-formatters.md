---
title: "Formattatori dei messaggi personalizzati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c07435f3-5214-4791-8961-2c2b61306d71
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# Formattatori dei messaggi personalizzati
Il contenuto di un messaggio è spesso nel formato XML, che in genere non è un formato pratico per un'applicazione.  Le applicazioni modificano gli oggetti, ottenendo e impostando le relative proprietà.  [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] usa il *contratto dati* per convertire un oggetto <xref:System.ServiceModel.Channels.Message> in un oggetto facilmente gestibile da un'applicazione.  Questi processi sono definiti serializzazione e deserializzazione.  Questi stessi termini vengono usati per descrivere la serializzazione e la deserializzazione eseguita dal livello del trasporto verso e dal formato di trasmissione del messaggio, che sono processi non correlati.  
  
 È possibile usare un formattatore dei messaggi personalizzato se è necessario implementare una conversione specializzata tra messaggi e oggetti che non può essere eseguita mediante un contratto dati.  Per questo scopo, modificare o estendere il comportamento di esecuzione di un'operazione del contratto specifica su un client o un servizio.  
  
## Formattatori dei messaggi personalizzati sul client  
 L'interfaccia <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter> definisce i metodi usati per controllare la conversione dei messaggi in oggetti e degli oggetti in messaggi per le applicazioni client.  
  
 È necessario implementare questa interfaccia.  Eseguire innanzitutto l'override del metodo <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter.DeserializeReply%2A> per deserializzare un messaggio.  Questo metodo viene chiamato dopo la ricezione di un messaggio in ingresso, ma prima che il messaggio venga inviato all'operazione client.  
  
 Eseguire quindi l'override del metodo <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter.SerializeRequest%2A> per serializzare un oggetto.  Questo metodo viene chiamato prima di inviare un messaggio in uscita.  
  
 Per inserire il formattatore personalizzato nell'applicazione del servizio, assegnare l'oggetto <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter> alla proprietà <xref:System.ServiceModel.Dispatcher.ClientOperation.Formatter%2A> usando un comportamento dell'operazione.  Per altre informazioni sui comportamenti, vedere [Configurazione ed estensione del runtime con i comportamenti](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md).  
  
## Formattatori dei messaggi personalizzati sul servizio  
 L'interfaccia <xref:System.ServiceModel.Dispatcher.IDispatchMessageFormatter> definisce i metodi che convertono un oggetto <xref:System.ServiceModel.Channels.Message> in parametri per un'operazione e da parametri in un oggetto <xref:System.ServiceModel.Channels.Message> in un'applicazione di servizio.  
  
 È necessario implementare questa interfaccia.  Eseguire innanzitutto l'override del metodo <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter.DeserializeReply%2A> per deserializzare un messaggio.  Questo metodo viene chiamato dopo la ricezione di un messaggio in ingresso, ma prima che il messaggio venga inviato all'operazione client.  
  
 Eseguire quindi l'override del metodo <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter.SerializeRequest%2A> per serializzare un oggetto.  Questo metodo viene chiamato prima di inviare un messaggio in uscita.  
  
 Per inserire il formattatore personalizzato nell'applicazione del servizio, assegnare l'oggetto <xref:System.ServiceModel.Dispatcher.IDispatchMessageFormatter> alla proprietà <xref:System.ServiceModel.Dispatcher.DispatchOperation.Formatter%2A> usando un comportamento dell'operazione.  Per altre informazioni sui comportamenti, vedere [Configurazione ed estensione del runtime con i comportamenti](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md).  
  
## Vedere anche  
 <xref:System.ServiceModel.Dispatcher.IClientMessageFormatter>   
 <xref:System.ServiceModel.Dispatcher.IDispatchMessageFormatter>   
 [Configurazione ed estensione del runtime con i comportamenti](../../../../docs/framework/wcf/extending/configuring-and-extending-the-runtime-with-behaviors.md)