---
title: "&lt;codificaMessaggiTesto&gt; | Microsoft Docs"
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
ms.assetid: e6d834d0-356e-45eb-b530-bbefbb9ec3f0
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# &lt;codificaMessaggiTesto&gt;
Specifica le impostazioni di codifica e controllo di versione dei messaggi XML basati sul testo.  
  
## Sintassi  
  
```  
  
<textMessageEncoding maxReadPoolSize="Integer"  
   maxWritePoolSize="Integer"  
   messageVersion="Soap11Addressing10/Soap12Addressing10"  
      writeEncoding=”UnicodeFffeTextEncoding/Utf16TextEncoding/Utf8TextEncoding" />  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|maxReadPoolSize|Numero intero che specifica il numero di messaggi che possono essere letti contemporaneamente senza allocare nuovi reader.  Dimensioni maggiori del pool rendono il sistema più tollerante ai picchi di attività al costo di un working set superiore.  Il valore predefinito è 64.|  
|maxWritePoolSize|Numero intero che specifica il numero di messaggi che possono essere inviati contemporaneamente senza allocare nuovi writer.  Dimensioni maggiori del pool rendono il sistema più tollerante ai picchi di attività al costo di un working set superiore.  Il valore predefinito è 16.|  
|messageVersion|Specifica la versione SOAP dei messaggi inviati usando l'associazione.  I valori validi sono:<br /><br /> -   Soap11Addressing10<br />-   Soap12Addressing10<br /><br /> L'impostazione predefinita è Soap12Addressing10.  L'attributo è di tipo <xref:System.ServiceModel.Channels.MessageVersion>.|  
|writeEncoding|Specifica la codifica del set di caratteri da usare per l'emissione dei messaggi dell'associazione.  I valori validi sono:<br /><br /> -   UnicodeFffeTextEncoding: codifica Unicode BigEndian<br />-   Utf16TextEncoding: codifica Unicode<br />-   Utf8TextEncoding: codifica a 8 bit.<br /><br /> L'impostazione predefinita è Utf8TextEncoding.  L'attributo è di tipo <xref:System.Text.Encoding>.|  
  
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
  
 La codifica di testo rappresentata dall'elemento `textMessageEncoding` è la più interoperativa, ma la meno efficiente per i messaggi XML.  Il codificatore di testo crea messaggi in transito basati su testo.  I messaggi prodotti da questo codificatore sono adatti per l'interoperabilità basata su WS\-\*.  In genere il servizio Web o il client di tale servizio è in grado di comprendere codice XML in formato testo.  Tuttavia, la trasmissione di grandi blocchi di dati binari come testo è il metodo meno efficiente per la codifica di messaggi XML.  
  
## Esempio  
  
```  
<textMessageEncoding maxReadPoolSize="211"  
    maxWritePoolSize="2132"  
    messageVersion="Soap12Addressing10"  
    textEncoding=”utf-8” />  
```  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.TextMessageEncodingElement>   
 <xref:System.ServiceModel.Channels.CustomBinding>   
 <xref:System.ServiceModel.Channels.MessageEncodingBindingElement>   
 <xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement>   
 [Scelta di un codificatore di messaggi](../../../../../docs/framework/wcf/feature-details/choosing-a-message-encoder.md)   
 [Codifica dei messaggi](../../../../../docs/framework/configure-apps/file-schema/wcf/message-encoding.md)   
 [Associazioni](../../../../../docs/framework/wcf/bindings.md)   
 [Estensione delle associazioni](../../../../../docs/framework/wcf/extending/extending-bindings.md)   
 [Associazioni personalizzate](../../../../../docs/framework/wcf/extending/custom-bindings.md)   
 [\<customBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)