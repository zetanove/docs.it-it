---
title: "TcpTransportBindingElement | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 33bbc1e5-44e4-4ee3-b7b5-801dc78956e4
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# TcpTransportBindingElement
TcpTransportBindingElement  
  
## Sintassi  
  
```  
class TcpTransportBindingElement : ConnectionOrientedTransportBindingElement  
{  
  TcpConnectionPoolSettings ConnectionPoolSettings;  
  sint32 ListenBacklog;  
  boolean PortSharingEnabled;  
  boolean TeredoEnabled;  
};  
```  
  
## Metodi  
 La classe TcpTransportBindingElement non definisce metodi.  
  
## Proprietà  
 La classe TcpTransportBindingElement dispone delle proprietà seguenti:  
  
### ConnectionPoolSettings  
 Tipo di dati: TcpConnectionPoolSettings  
  
 Tipo di accesso: in sola lettura.  
  
 Impostazioni del pool di connessioni.  
  
### ListenBacklog  
 Tipo di dati: sint32  
  
 Tipo di accesso: sola lettura.  
  
 Numero massimo di richieste di connessioni in coda che possono essere in sospeso.  
  
### PortSharingEnabled  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura.  
  
 Valore booleano che specifica se è attivata la condivisione delle porte TCP per la connessione.  
  
### TeredoEnabled  
 Tipo di dati: booleano  
  
 Tipo di accesso: sola lettura.  
  
 Valore booleano che specifica se Teredo \(una tecnologia per l'indirizzamento dei client dietro a firewall\) è attivata.  
  
## Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-------------------------------------|  
|Spazio dei nomi|Definito in root\\ServiceModel|  
  
## Vedere anche  
 <xref:System.ServiceModel.Channels.TcpTransportBindingElement>