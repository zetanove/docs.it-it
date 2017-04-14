---
title: "Associazioni WS-MetadataExchange | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 10f8de5d-b81d-4ea7-b37e-7f2c00c39714
caps.latest.revision: 4
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 4
---
# Associazioni WS-MetadataExchange
In questo argomento vengono illustrate le modalità di costruzione delle associazioni predefinite per lo scambio di metadati per i vari trasporti.  
  
## Associazioni predefinite  
  
|Nome associazione predefinita|Modalità di costruzione dell'associazione|  
|-----------------------------------|-----------------------------------------------|  
|MexHttpBinding|Una classe <xref:System.ServiceModel.WSHttpBinding> con protezione a livello di trasporto attivata.|  
|MexHttpsBinding|Una classe <xref:System.ServiceModel.WSHttpBinding> che supporta la protezione a livello di trasporto.|  
|MexNamedPipeBinding|Una classe <xref:System.ServiceModel.Channels.CustomBinding> con un elemento <xref:System.ServiceModel.Channels.NamedPipeTransportBindingElement> che utilizza valori predefiniti.|  
|MexTcpBinding|Una classe <xref:System.ServiceModel.Channels.CustomBinding> con un elemento <xref:System.ServiceModel.Channels.TcpTransportBindingElement> che utilizza valori predefiniti.|