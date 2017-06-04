---
title: "ConnectionOrientedTransportBindingElement | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c1308313-f0e2-49e6-977d-6b4ce9ad35d1
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# ConnectionOrientedTransportBindingElement
ConnectionOrientedTransportBindingElement  
  
## Sintassi  
  
```  
class ConnectionOrientedTransportBindingElement : TransportBindingElement  
{  
  datetime ChannelInitializationTimeout;  
  sint32 ConnectionBufferSize;  
  string HostNameComparisonMode;  
  sint32 MaxBufferSize;  
  datetime MaxOutputDelay;  
  sint32 MaxPendingAccepts;  
  sint32 MaxPendingConnections;  
  string TransferMode;  
};  
```  
  
## Metodi  
 La classe ConnectionOrientedTransportBindingElement non definisce metodi.  
  
## Proprietà  
 La classe ConnectionOrientedTransportBindingElement dispone delle proprietà seguenti:  
  
### ChannelInitializationTimeout  
 Tipo di dati: DateTime  
  
 Tipo di accesso: sola lettura  
  
 TimeSpan che specifica l'intervallo di tempo per il completamento dell'inizializzazione del canale prima del timeout.  
  
### ConnectionBufferSize  
 Tipo di dati: sint32  
  
 Tipo di accesso: sola lettura  
  
 Dimensione del buffer usata per trasmettere un blocco del messaggio serializzato in transito dal client o servizio.  
  
### HostnameComparisonMode  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura  
  
 Valore che indica se viene usato il nome host per raggiungere il servizio in caso di corrispondenza dell'URI.  
  
### MaxBufferSize  
 Tipo di dati: sint32  
  
 Tipo di accesso: sola lettura  
  
 Dimensione massima del buffer da usare.  
  
### MaxOutputDelay  
 Tipo di dati: DateTime  
  
 Tipo di accesso: sola lettura  
  
 Intervallo di tempo massimo per cui un blocco di un messaggio o un messaggio intero può rimanere memorizzato nel buffer prima dell'invio.  
  
### MaxPendingAccepts  
 Tipo di dati: sint32  
  
 Tipo di accesso: sola lettura  
  
 Numero massimo di thread asincroni in sospeso disponibili per l'elaborazione delle connessioni in ingresso del servizio.  
  
### MaxPendingConnections  
 Tipo di dati: sint32  
  
 Tipo di accesso: sola lettura  
  
 Numero massimo di connessioni in sospeso.  
  
### TransferMode  
 Tipo di dati: stringa  
  
 Tipo di accesso: sola lettura  
  
 Valore che specifica se i messaggi vengono memorizzati nel buffer o trasmessi con il trasporto orientato alla connessione.  
  
## Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-------------------------------------|  
|Spazio dei nomi|Definito in root\\ServiceModel|  
  
## Vedere anche  
 <xref:System.ServiceModel.Channels.ConnectionOrientedTransportBindingElement>