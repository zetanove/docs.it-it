---
title: "NamedPipeConnectionPoolSettings | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 079bccb8-54b5-4436-a43d-5567763f72ce
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# NamedPipeConnectionPoolSettings
NamedPipeConnectionPoolSettings  
  
## Sintassi  
  
```  
class NamedPipeConnectionPoolSettings  
{  
  string GroupName;  
  datetime IdleTimeout;  
  sint32 MaxOutboundConnectionsPerEndpoint;  
};  
```  
  
## Metodi  
 La classe NamedPipeConnectionPoolSettings non definisce metodi.  
  
## Proprietà  
 La classe NamedPipeConnectionPoolSettings dispone delle proprietà seguenti:  
  
### GroupName  
 Tipo di dati: stringa  
  
 Tipo di accesso: in sola lettura.  
  
 Nome del gruppo del pool di connessioni utilizzato dall'elemento di associazione.  
  
### IdleTimeout  
 Tipo di dati: data e ora  
  
 Tipo di accesso: sola lettura.  
  
 Periodo massimo di inattività della connessione prima che venga interrotta.  
  
### MaxOutboundConnectionsPerEndpoint  
 Tipo di dati: sint32  
  
 Tipo di accesso: sola lettura.  
  
 Numero massimo di connessioni in uscita per ogni endpoint sul client.  
  
## Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-------------------------------------|  
|Spazio dei nomi|Definito in root\\ServiceModel|  
  
## Vedere anche  
 <xref:System.ServiceModel.Channels.NamedPipeConnectionPoolSettings>