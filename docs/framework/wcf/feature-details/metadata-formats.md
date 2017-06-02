---
title: "Formati dei metadati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: baad1e68-28fc-4a6a-8a43-75e47e7fa871
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Formati dei metadati
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] supporta i formati di metadati riportati nella tabella seguente.  
  
## Specifiche e utilizzo dei metadati  
  
|Protocollo|Specifica e utilizzo|  
|----------------|--------------------------|  
|WSDL 1.1|[Web Services Description Language \(WSDL\) 1.1](http://go.microsoft.com/fwlink/?LinkId=94859)<br /><br /> [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] usa Web Services Description Language \(WSDL\) per descrivere i servizi.|  
|XML Schema|[XML Schema Part 2: Datatypes Second Edition](http://go.microsoft.com/fwlink/?LinkId=94861) e [XML Schema Part 1: Structures Second Edition](http://go.microsoft.com/fwlink/?LinkId=94862)<br /><br /> [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] usa l'XML Schema per descrivere tipi di dati usati nei messaggi.|  
|WS Policy|[Web Services Policy 1.2 \- Framework \(WS\-Policy\)](http://go.microsoft.com/fwlink/?LinkId=94864)<br /><br /> [Web Services Policy 1.5 \- Framework](http://go.microsoft.com/fwlink/?LinkId=94865)<br /><br /> [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] usa la specifica WS\-Policy 1.2 o 1.5 insieme ad asserzioni specifiche del dominio per descrivere le funzionalità e i requisiti del servizio.|  
|WS Policy Attachments|[Web Services Policy 1.2 \- Attachment \(WS\-PolicyAttachment\)](http://go.microsoft.com/fwlink/?LinkId=94866)<br /><br /> [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] implementa WS\-PolicyAttachments per allegare espressioni di criteri a vari ambiti in WSDL.|  
|WS Metadata Exchange|[Web Services Metadata Exchange \(WS\-MetadataExchange\) versione 1.1](http://go.microsoft.com/fwlink/?LinkId=94868)<br /><br /> [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] implementa WS\-MetadataExchange per recuperare XML Schema, WSDL e WS\-Policy.|  
|WS Addressing Binding per WSDL|[Web Services Addressing 1.0 \- WSDL Binding](http://go.microsoft.com/fwlink/?LinkId=94869)<br /><br /> [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] implementa WS\-Addressing Binding per WSDL per collegare informazioni di indirizzamento in WSDL.|  
  
## Vedere anche  
 [Protocolli di servizi Web supportati da associazioni di interoperabilità fornite dal sistema](../../../../docs/framework/wcf/feature-details/web-services-protocols-supported-by-system-provided-interoperability-bindings.md)   
 [WSDL e criteri](../../../../docs/framework/wcf/feature-details/wsdl-and-policy.md)