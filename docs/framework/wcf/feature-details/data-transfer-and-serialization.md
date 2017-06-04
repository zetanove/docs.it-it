---
title: "Trasferimento dati e serializzazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "serializzazione di dati [WCF]"
  - "trasferimento dei dati [WCF]"
ms.assetid: 0f03c635-f3e7-4c5c-9463-3cb0135e221e
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Trasferimento dati e serializzazione
In un sistema collegato, per eseguire qualsiasi attività, servizi e client dipendono dallo scambio di dati.Gli sviluppatori di un servizio o di un client devono comprendere inoltre come [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] gestisce i dati e la serializzazione dei dati per creare applicazioni efficienti e facili da gestire.  
  
## In questa sezione  
 [Specifica del trasferimento di dati nei contratti di servizio](../../../../docs/framework/wcf/feature-details/specifying-data-transfer-in-service-contracts.md)  
 Descrive i concetti di base del trasferimento dati nei servizi.  
  
 [Uso di contratti dati](../../../../docs/framework/wcf/feature-details/using-data-contracts.md)  
 Descrive i contratti dati, come crearli e utilizzarli.  
  
 [Serializzatore dei contratti dati](../../../../docs/framework/wcf/feature-details/data-contract-serializer.md)  
 Descrive come eseguire la serializzazione di dati con la classe <xref:System.Runtime.Serialization.DataContractSerializer> o qualsiasi estensione della classe <xref:System.Runtime.Serialization.XmlObjectSerializer>.  
  
 [Utilizzo della classe XmlSerializer](../../../../docs/framework/wcf/feature-details/using-the-xmlserializer-class.md)  
 Descrive come e perché utilizzare la classe <xref:System.Xml.Serialization.XmlSerializer>, un'alternativa alla classe <xref:System.Runtime.Serialization.DataContractSerializer>.  
  
 [Utilizzo dei contratti di messaggio](../../../../docs/framework/wcf/feature-details/using-message-contracts.md)  
 Descrive in che modo i contratti di messaggio consentono il controllo accurato di messaggi SOAP.  
  
 [Utilizzo della classe Message](../../../../docs/framework/wcf/feature-details/using-the-message-class.md)  
 Descrive come utilizzare le funzionalità di una classe Message.  
  
 [Filtri](../../../../docs/framework/wcf/feature-details/filtering.md)  
 Descrive il filtraggio, che consente la pre\-elaborazione di un messaggio basata su vari criteri.  
  
 [Dati di grandi dimensioni e flussi](../../../../docs/framework/wcf/feature-details/large-data-and-streaming.md)  
 Descrive come inviare un grande blocco di dati, ad esempio un file binario.  
  
 [Considerazioni sulla protezione per i dati](../../../../docs/framework/wcf/feature-details/security-considerations-for-data.md)  
 Descrive gli elementi da prendere in considerazione quando si programma il trasferimento dei dati e la serializzazione.  
  
 [Panoramica dell'architettura di trasferimento dei dati](../../../../docs/framework/wcf/feature-details/data-transfer-architectural-overview.md)  
 Descrive il principio generale del trasferimento dei dati in [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
## Riferimenti  
 <xref:System.ServiceModel>  
  
 <xref:System.Runtime.Serialization.DataContractSerializer>  
  
 <xref:System.Xml.Serialization.XmlSerializer>  
  
 <xref:System.Runtime.Serialization>  
  
 <xref:System.Xml.Serialization>  
  
## Sezioni correlate  
 [Estensione di codificatori e serializzatori](../../../../docs/framework/wcf/extending/extending-encoders-and-serializers.md)  
  
## Vedere anche  
 [Procedure consigliate: controllo delle versioni del contratto dati](../../../../docs/framework/wcf/best-practices-data-contract-versioning.md)   
 [Controllo delle versioni del servizio](../../../../docs/framework/wcf/service-versioning.md)