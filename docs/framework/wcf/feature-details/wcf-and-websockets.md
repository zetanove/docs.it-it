---
title: "WCF e WebSocket | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1e53b49e-022c-49c7-8984-4b21b53c05b3
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# WCF e WebSocket
Con .NET Framework 4.5 è stato introdotto il supporto per WebSocket in Windows Communication Foundation.Si tratta di una tecnologia efficiente e basata su standard che consente la comunicazione bidirezionale sulle porte 80 e 443 HTTP standard.L'utilizzo delle porte HTTP standard consente la comunicazione WebSocket attraverso il Web mediante intermediari.Sono state aggiunte due nuove associazioni standard per supportare la comunicazione tramite un trasporto WebSocket,<xref:System.ServiceModel.NetHttpBinding> e <xref:System.ServiceModel.NetHttpsBinding>.Le impostazioni specifiche per WebSocket possono essere configurate nell'elemento <xref:> System.ServiceModel.Channels.HttpTransportBinding?qualifyHint=False&autoUpgrade=True accedendo alla proprietà <xref:System.ServiceModel.Channels.HttpTransportBindingElement.WebSocketSettings%2A>.  
  
## In questa sezione  
 [Uso di NetHttpBinding](../../../../docs/framework/wcf/feature-details/using-the-nethttpbinding.md)  
 Viene illustrato l'oggetto <xref:System.ServiceModel.NetHttpBinding> e la relativa configurazione.  
  
 [Procedura: creare un servizio WCF che comunica tramite WebSockets](../../../../docs/framework/wcf/feature-details/how-to-create-a-wcf-service-that-communicates-over-websockets.md)  
 Viene descritto come creare un servizio WCF che comunica tramite WebSockets.  
  
## Riferimenti  
  
## Sezioni correlate