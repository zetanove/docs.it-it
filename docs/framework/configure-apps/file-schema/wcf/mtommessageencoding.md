---
title: "&lt;codificaMessaggiMtom&gt; | Microsoft Docs"
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
ms.assetid: 7865d171-cd1e-430a-8421-39cc13541d1b
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# &lt;codificaMessaggiMtom&gt;
Specifica le impostazioni di codifica e controllo di versione dei messaggi SOAP basati sul meccanismo Message Transmission Optimization Mechanism \(MTOM\).  
  
## Sintassi  
  
```  
  
<mtomMessageEncoding   
   maxBufferSize="Integer"  
      maxReadPoolSize="Integer"  
   maxWritePoolSize="Integer"  
   messageVersion="Soap11Addressing1/Soap12Addressing10"  
      writeEncoding=”UnicodeFffeTextEncoding/Utf16TextEncoding/Utf8TextEncoding" />  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|maxBufferSize|Numero intero che specifica la dimensione massima del buffer che è possibile usare.|  
|maxReadPoolSize|Numero intero che specifica il numero di messaggi che possono essere letti contemporaneamente senza allocare nuovi reader.  Dimensioni maggiori del pool rendono il sistema più tollerante ai picchi di attività al costo di un working set superiore.  Il valore predefinito è 64.|  
|maxWritePoolSize|Numero intero che specifica il numero di messaggi che possono essere inviati contemporaneamente senza allocare nuovi writer.  Dimensioni maggiori del pool rendono il sistema più tollerante ai picchi di attività al costo di un working set superiore.  Il valore predefinito è 16.|  
|messageVersion|Specifica la versione SOAP dei messaggi inviati usando l'associazione.  I valori validi sono:<br /><br /> -   Soap11Addressing1<br />-   Soap12Addressing10<br /><br /> L'impostazione predefinita è Soap12Addressing10.  L'attributo è di tipo <xref:System.ServiceModel.Channels.MessageVersion>.|  
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
  
 L'elemento `MtomMessageEncoding` specifica la codifica dei caratteri, la versione dei messaggi e altre impostazioni usate per i messaggi che usano la codifica MTOM \(Message Transmission Optimization Mechanism\).  MTOM è una tecnologia efficiente per la trasmissione di dati binari nei messaggi di WCF.  Il codificatore MTOM cerca di creare un equilibrio tra efficienza e interoperabilità.  La codifica MTOM trasmette la maggior parte del codice XML in formato testo, ma ottimizza grandi blocchi di dati binari trasmettendoli senza introdurre modifiche e senza convertirli nel formato codificato Base64.  
  
## Esempio  
  
```  
<mtomMessageEncoding maxReadPoolSize="211"  
    maxWritePoolSize="2132"  
    messageVersion=”Soap11Addressing10”  
    textEncoding=”utf-8” />  
```  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.MtomMessageEncodingElement>   
 <xref:System.ServiceModel.Channels.CustomBinding>   
 <xref:System.ServiceModel.Channels.MessageEncodingBindingElement>   
 <xref:System.ServiceModel.Channels.MtomMessageEncodingBindingElement>   
 [Codifica dei messaggi](../../../../../docs/framework/configure-apps/file-schema/wcf/message-encoding.md)   
 [Scelta di un codificatore di messaggi](../../../../../docs/framework/wcf/feature-details/choosing-a-message-encoder.md)   
 [Associazioni](../../../../../docs/framework/wcf/bindings.md)   
 [Estensione delle associazioni](../../../../../docs/framework/wcf/extending/extending-bindings.md)   
 [Associazioni personalizzate](../../../../../docs/framework/wcf/extending/custom-bindings.md)   
 [\<customBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)