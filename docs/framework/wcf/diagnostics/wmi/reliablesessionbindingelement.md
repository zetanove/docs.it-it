---
title: "ReliableSessionBindingElement | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: effda125-b8d3-4de6-8c0e-f59f5ea8f6eb
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# ReliableSessionBindingElement
ReliableSessionBindingElement  
  
## Sintassi  
  
```  
class ReliableSessionBindingElement : BindingElement  
{  
  datetime AcknowledgementInterval;  
  boolean FlowControlEnabled;  
  datetime InactivityTimeout;  
  sint32 MaxPendingChannels;  
  sint32 MaxRetryCount;  
  sint32 MaxTransferWindowSize;  
  boolean Ordered;  
  integer ReliableMessagingVersion;  
};  
```  
  
## Metodi  
 La classe ReliableSessionBindingElement non definisce metodi.  
  
## Proprietà  
 La classe ReliableSessionBindingElement ha le proprietà seguenti:  
  
### AcknowledgementInterval  
 Tipo di dati: DateTime  
  
 Tipo di accesso: sola lettura  
  
 Intervallo di tempo che una destinazione attende prima di inviare un acknowledgment all'origine del messaggio sui canali affidabili creati dalla factory.  
  
### FlowControlEnabled  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura  
  
 Valore booleano che specifica se è attivato il controllo di flusso.  
  
### InactivityTimeout  
 Tipo di dati: DateTime  
  
 Tipo di accesso: sola lettura  
  
 Specifica il limite massimo di tempo per cui il canale consente all'altra parte della comunicazione di non inviare messaggi prima di generare un errore per il canale.  
  
### MaxPendingChannels  
 Tipo di dati: sint32  
  
 Tipo di accesso: sola lettura  
  
 Numero massimo di canali che possono attendere nel listener prima di essere accettati.  
  
### MaxRetryCount  
 Tipo di dati: sint32  
  
 Tipo di accesso: sola lettura  
  
 Numero massimo di tentativi di ritrasmissione di un messaggio per cui un canale affidabile non ha ricevuto un acknowledgment, tramite una chiamata a `Send` sul canale sottostante.  
  
### MaxTransferWindowSize  
 Tipo di dati: sint32  
  
 Tipo di accesso: sola lettura  
  
 Dimensione massima della finestra di trasferimento per la sessione affidabile.  
  
### Ordered  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura  
  
 Valore booleano che specifica se è garantito l'arrivo dei messaggi nell'ordine in cui sono stati inviati.  
  
### ReliableMessagingVersion  
 Tipo di dati: numero intero  
  
 Tipo di accesso: sola lettura  
  
 Numero intero che specifica la versione del protocollo WS\-ReliableMessaging usata nella sessione affidabile.  
  
## Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-------------------------------------|  
|Spazio dei nomi|Definito in root\\ServiceModel|  
  
## Vedere anche  
 <xref:System.ServiceModel.Channels.ReliableSessionBindingElement>