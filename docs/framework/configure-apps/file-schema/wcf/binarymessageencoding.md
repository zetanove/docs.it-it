---
title: "&lt;codificaMessaggiBinaria&gt; | Microsoft Docs"
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
ms.assetid: e4ae3cd4-6b67-4ce1-af4b-9400e0a38dba
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# &lt;codificaMessaggiBinaria&gt;
Definisce un codificatore di messaggi binario che codifica messaggi di Windows Communication Foundation \(WCF\) in transito in formato binario.  
  
## Sintassi  
  
```  
  
<binaryMessageEncoding   
      maxReadPoolSize="Integer"  
   maxSessionSize="Integer"   
   maxWritePoolSize="Integer"  
   messageVersion="Soap11Addressing10/Soap12Addressing10” />  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|maxReadPoolSize|Numero intero che definisce il numero di messaggi che possono essere letti contemporaneamente senza allocare nuovi lettori.  Dimensioni maggiori del pool rendono il sistema più tollerante ai picchi di attività al costo di un working set superiore.  Il valore predefinito è 64.|  
|maxSessionSize|Numero intero positivo che imposta la dimensione, in byte, del buffer usato per la codifica.  Un buffer più grande aumenta la velocità di codifica a spese della dimensione del working set.  Il valore predefinito è 2048.|  
|maxWritePoolSize|Numero intero che definisce il numero di messaggi che possono essere inviati contemporaneamente senza allocare nuovi writer.  Dimensioni maggiori del pool rendono il sistema più tollerante ai picchi di attività al costo di un working set superiore.  Il valore predefinito è 16.|  
|messageVersion|Specifica le versioni del messaggio SOAP e WS\-Addressing usate o previste.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<quoteReader\>](../Topic/%3CreaderQuotas%3E.md)|Definisce i vincoli sulla complessità dei messaggi SOAP che possono essere elaborati dagli endpoint configurati con questa associazione.  L'elemento è di tipo <xref:System.ServiceModel.Configuration.XmlDictionaryReaderQuotasElement>.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<associazione\>](../../../../../docs/framework/misc/binding.md)|Definisce tutte le funzionalità di associazione dell'associazione personalizzata.|  
  
## Note  
 La codifica è il processo di trasformazione di un messaggio in una sequenza di byte.  La decodifica è il processo inverso.  Windows Communication Foundation \(WCF\) include tre tipi di codifica per i messaggi SOAP, ovvero testo, binaria e MTOM \(Message Transmission Optimization Mechanism\).  
  
 L'elemento `binaryMessageEncoding` specifica il formato binario .NET per XML e dispone delle opzioni che consentono di specificare la codifica dei caratteri e le versioni SOAP e WS\-Addressing da usare.  Il codificatore di messaggi binario codifica messaggi di Windows Communication Foundation \(WCF\) in transito in formato binario.  Se da un lato questa codifica comporta una trasmissione molto veloce dei messaggi, dall'altro si perde l'interoperabilità basata sugli standard WS \- \*.  
  
## Esempio  
  
```  
<binaryMessageEncoding maxReadPoolSize="211"  
   maxWritePoolSize="2132"  
   maxSessionSize="3141" />  
```  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.BinaryMessageEncodingElement>   
 <xref:System.ServiceModel.Channels.CustomBinding>   
 <xref:System.ServiceModel.Channels.MessageEncodingBindingElement>   
 <xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement>   
 [Codifica dei messaggi](../../../../../docs/framework/configure-apps/file-schema/wcf/message-encoding.md)   
 [Scelta di un codificatore di messaggi](../../../../../docs/framework/wcf/feature-details/choosing-a-message-encoder.md)   
 [Associazioni](../../../../../docs/framework/wcf/bindings.md)   
 [Estensione delle associazioni](../../../../../docs/framework/wcf/extending/extending-bindings.md)   
 [Associazioni personalizzate](../../../../../docs/framework/wcf/extending/custom-bindings.md)   
 [\<customBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)