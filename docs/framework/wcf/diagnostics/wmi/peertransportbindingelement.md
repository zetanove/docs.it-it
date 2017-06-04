---
title: "PeerTransportBindingElement | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 40bf6be2-8087-4cb3-a66c-408d53eb9269
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# PeerTransportBindingElement
PeerTransportBindingElement  
  
## Sintassi  
  
```  
class PeerTransportBindingElement : TransportBindingElement  
{  
  string ListenIPAddress;  
  sint32 Port;  
  PeerSecuritySettings Security;  
};  
```  
  
## Metodi  
 La classe PeerTransportBindingElement non definisce metodi.  
  
## Proprietà  
 La classe PeerTransportBindingElement dispone delle proprietà seguenti:  
  
### ListenIPAddress  
 Tipo di dati: stringa  
  
 Tipo di accesso: in sola lettura  
  
 Indirizzo IP su cui il nodo del peer è in attesa di messaggi.  
  
### Porta  
 Tipo di dati: sint32  
  
 Tipo di accesso: sola lettura.  
  
 Porta di interfaccia di rete su cui l'associazione elabora messaggi del canale del peer.  
  
### Protezione  
 Tipo di dati: PeerSecuritySettings  
  
 Tipo di accesso: sola lettura.  
  
 Impostazioni di sicurezza del trasporto peer.  
  
## Requisiti  
  
|MOF|Dichiarato in Servicemodel.mof.|  
|---------|-------------------------------------|  
|Spazio dei nomi|Definito in root\\ServiceModel|  
  
## Vedere anche  
 <xref:System.ServiceModel.Channels.PeerTransportBindingElement>