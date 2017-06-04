---
title: "&lt;sicurezzaFlussoWindows&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 926bea29-90c7-4a26-9cf0-fb4aa44f6f70
caps.latest.revision: 10
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 10
---
# &lt;sicurezzaFlussoWindows&gt;
Specificare le impostazioni per la sicurezza del flusso di Windows dell'associazione personalizzata.  
  
## Sintassi  
  
```  
  
<windowsStreamSecurity protectionLevel="None/Sign/EncryptAndSign"/>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|protectionLevel|Definisce la sicurezza a livello di messaggio.  La firma dei messaggi riduce il rischio di manomissione da parte di terzi durante il trasferimento.  La crittografia fornisce riservatezza a livello di dati durante il trasporto.  Di seguito vengono elencati i valori validi:<br /><br /> -   None: nessuna protezione.<br />-   Sign: i messaggi sono firmati.<br />-   EncryptAndSign: i messaggi vengono firmati e crittografati.<br /><br /> L'impostazione predefinita è EncryptAndSign.<br /><br /> L'attributo è di tipo <xref:System.Net.Security.ProtectionLevel>.|  
  
### Elementi figlio  
 None  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<associazione\>](../../../../../docs/framework/misc/binding.md)|Definisce tutte le funzionalità di associazione dell'associazione personalizzata.|  
  
## Note  
 I trasporti che usano un protocollo orientato al flusso, ad esempio TCP e named pipe, supportano aggiornamenti del trasporto basati sul flusso.  In particolare, WCF fornisce aggiornamenti della sicurezza.  La configurazione di questa sicurezza del trasporto viene incapsulata da questo elemento di configurazione e da [\<sslStreamSecurity\>](../../../../../docs/framework/configure-apps/file-schema/wcf/sslstreamsecurity.md), che è possibile configurare e aggiungere a un'associazione personalizzata.  
  
## Vedere anche  
 <xref:System.ServiceModel.Channels.CustomBinding>   
 <xref:System.ServiceModel.Configuration.WindowsStreamSecurityElement>   
 <xref:System.ServiceModel.Channels.WindowsStreamSecurityBindingElement>   
 [Associazioni](../../../../../docs/framework/wcf/bindings.md)   
 [Estensione delle associazioni](../../../../../docs/framework/wcf/extending/extending-bindings.md)   
 [Associazioni personalizzate](../../../../../docs/framework/wcf/extending/custom-bindings.md)   
 [\<customBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)