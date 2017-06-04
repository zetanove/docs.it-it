---
title: "TcpConnectionPoolSettings | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 19acfba3-c057-4dbc-bac7-8674d7844d83
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# TcpConnectionPoolSettings
TcpConnectionPoolSettings  
  
## Sintassi  
  
```  
class TcpConnectionPoolSettings  
{  
  string GroupName;  
  datetime IdleTimeout;  
  datetime LeaseTimeout;  
  sint32 MaxOutboundConnectionsPerEndpoint;  
};  
```  
  
## Metodi  
 La classe TcpConnectionPoolSettings non definisce metodi.  
  
## Proprietà  
 La classe TcpConnectionPoolSettings dispone delle proprietà seguenti:  
  
### GroupName  
 Tipo di dati: stringa  
  
 Tipo di accesso: in sola lettura.  
  
 Nome del gruppo del pool di connessioni utilizzato dall'elemento di associazione.  
  
### IdleTimeout  
 Tipo di dati: data e ora  
  
 Tipo di accesso: sola lettura.  
  
 Periodo massimo di inattività della connessione prima che venga interrotta.  
  
### LeaseTimeout  
 Tipo di dati: DateTime  
  
 Tipo di accesso: sola lettura.  
  
 Limite massimo di tempo per il completamento dell'operazione di lease prima del timeout.  
  
### MaxOutboundConnectionsPerEndpoint  
 Tipo di dati: sint32  
  
 Tipo di accesso: sola lettura.  
  
 Numero massimo di connessioni in uscita per ogni endpoint.  
  
## Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-------------------------------------|  
|Spazio dei nomi|Definito in root\\ServiceModel|  
  
## Vedere anche  
 <xref:System.ServiceModel.Channels.TcpConnectionPoolSettings>