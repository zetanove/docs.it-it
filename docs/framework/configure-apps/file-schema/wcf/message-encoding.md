---
title: "Codifica dei messaggi | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
ms.assetid: f30ee941-aca9-4c67-82a5-421568496f07
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Codifica dei messaggi
La codifica è il processo di trasformazione di un insieme di caratteri Unicode in una sequenza di byte.  La decodifica è il processo inverso.  Windows Communication Foundation \(WCF\) include tre tipi di codifica per i messaggi SOAP, ovvero testo, binaria e MTOM \(Message Transmission Optimization Mechanism\).  
  
 La sezione di configurazione `binaryMessageEncoding` specifica la codifica dei caratteri e la versione dei messaggi usate per messaggi XML basati su un sistema binario.  Il codificatore di messaggi binario codifica messaggi di Windows Communication Foundation \(WCF\) in transito in formato binario.  Se da un lato questa codifica comporta una trasmissione molto veloce dei messaggi, dall'altro si perde l'interoperabilità basata sugli standard WS \- \*.  
  
 La sezione di configurazione `mtomMessageEncoding` specifica la codifica dei caratteri e il controllo di versione del messaggio usati per un messaggio che usa una codifica Message Transmission Optimization Mechanism \(MTOM\).  MTOM è una tecnologia efficiente per la trasmissione di dati binari nei messaggi di Windows Communication Foundation \(WCF\).  Il codificatore MTOM cerca un equilibrio tra efficienza e interoperabilità.  La codifica MTOM trasmette la maggior parte del codice XML in formato testo, ma ottimizza grandi blocchi di dati binari trasmettendoli senza introdurre modifiche e senza convertirli in formato testo.  
  
 La sezione di configurazione `textMessageEncoding` specifica un codificatore di testo usato per creare messaggi in transito basati su testo.  I messaggi prodotti da questo codificatore sono adatti per l'interoperabilità basata su WS\-\*.  In genere il servizio Web o il client di tale servizio è in grado di comprendere codice XML in formato testo.  Tuttavia, la trasmissione di grandi blocchi di dati binari come testo è il metodo meno efficiente per la codifica di messaggi XML.  
  
## Vedere anche  
 <xref:System.ServiceModel.Channels.CustomBinding>   
 <xref:System.ServiceModel.Channels.MessageEncodingBindingElement>   
 [Associazioni](../../../../../docs/framework/wcf/bindings.md)   
 [Estensione delle associazioni](../../../../../docs/framework/wcf/extending/extending-bindings.md)   
 [Associazioni personalizzate](../../../../../docs/framework/wcf/extending/custom-bindings.md)   
 [\<customBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)   
 [Scelta di un codificatore di messaggi](../../../../../docs/framework/wcf/feature-details/choosing-a-message-encoder.md)