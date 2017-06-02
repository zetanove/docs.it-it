---
title: "Elemento &lt;httpWebRequest&gt; (Impostazioni di rete) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#configuration/system.net/settings/httpWebRequest"
  - "http://schemas.microsoft.com/.NetConfiguration/v2.0#httpWebRequest"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "<httpWebRequest> (elemento)"
  - "httpWebRequest (elemento)"
ms.assetid: 52acd9d2-5bdc-4dc4-9c2a-f0a476ccbb31
caps.latest.revision: 18
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 18
---
# Elemento &lt;httpWebRequest&gt; (Impostazioni di rete)
Personalizza i parametri delle richieste Web.  
  
## Sintassi  
  
```  
  
      <httpWebRequest  
  maximumResponseHeadersLength="size"  
  maximumErrorResponseLength="size"  
  maximumUnauthorizedUploadLength="size"  
  useUnsafeHeaderParsing="true|false"  
/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|**Attributo**|**Descrizione**|  
|-------------------|---------------------|  
|`maximumResponseHeadersLength`|Specifica la lunghezza massima, in kilobyte, di un'intestazione di risposta.  Il valore predefinito è 64.  Il valore \-1 indica che non verrà imposto alcun limite di dimensione sulle intestazioni di risposta.|  
|`maximumErrorResponseLength`|Specifica la lunghezza massima, in kilobyte, di una risposta di errore.  Il valore predefinito è 64.  Il valore \-1 indica che non verrà imposto alcun limite di dimensione sulle risposte di errore.|  
|`maximumUnauthorizedUploadLength`|Specifica la lunghezza massima, in byte, di un caricamento eseguito in risposta a un codice di errore non autorizzato.  Il valore predefinito è \-1.  Un valore di \-1 indica che non verrà imposto alcun limite di dimensione all'upload.|  
|`useUnsafeHeaderParsing`|Specifica se l'analisi delle intestazioni non protette è attivata.  Il valore predefinito è `false`.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|**Elemento**|**Descrizione**|  
|------------------|---------------------|  
|[impostazioni](../../../../../docs/framework/configure-apps/file-schema/network/settings-element-network-settings.md)|Configura opzioni di rete di base per lo spazio dei nomi <xref:System.Net>.|  
  
## Note  
 Per impostazione predefinita, .NET Framework applica in maniera rigida la specifica RFC 2616 per l'analisi URI.  Alcune risposte del server possono includere caratteri di controllo in campi non consentiti, che causeranno la generazione di un'eccezione <xref:System.Net.WebException> da parte del metodo <xref:System.Net.HttpWebRequest.GetResponse?displayProperty=fullName>.  Se l'attributo **useUnsafeHeaderParsing** è impostato su **true**, il metodo <xref:System.Net.HttpWebRequest.GetResponse?displayProperty=fullName> non genererà alcuna eccezione. L'applicazione sarà, tuttavia, vulnerabile a diverse forme di attacchi durante l'analisi URI.  La soluzione migliore consiste nel modificare le impostazioni del server in modo che la risposta non includa caratteri di controllo.  
  
## File di configurazione  
 L'elemento può essere utilizzato nel file di configurazione dell'applicazione o nel file di configurazione del computer \(Machine.config\).  
  
## Esempio  
 Nell'esempio di codice riportato di seguito viene illustrato come specificare una lunghezza di intestazione massima maggiore del normale.  
  
```  
<configuration>  
  <system.net>  
    <settings>  
      <httpWebRequest  
        maximumResponseHeadersLength="128"  
      />  
    </settings>  
  </system.net>  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.Net.HttpWebRequest.MaximumResponseHeadersLength%2A>   
 [Schema delle impostazioni di rete](../../../../../docs/framework/configure-apps/file-schema/network/index.md)