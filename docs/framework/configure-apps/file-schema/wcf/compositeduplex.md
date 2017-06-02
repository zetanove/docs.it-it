---
title: "&lt; compositeDuplex &gt; | Microsoft Docs"
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
ms.assetid: 725004d1-ce88-4405-a220-78e89844f81f
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# &lt; compositeDuplex &gt;
Definisce l'elemento di associazione usato quando il client deve esporre un endpoint affinché il servizio restituisca messaggi al client.  
  
## Sintassi  
  
```  
  
<compositeDuplex clientBaseAddress="URI" />  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|clientBaseAddress|URI che imposta l'indirizzo del canale di supporto in modalità duplex.  Il servizio usa questo indirizzo per creare un contatto e stabilire una connessione con il client.<br /><br /> Se questo attributo non è impostato, viene generato un indirizzo predefinito “`full qualified name+default port\TemporaryIndigoAddress\guid`”.  Il valore predefinito è `null`.|  
  
### Elementi figlio  
 None  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<associazione\>](../../../../../docs/framework/misc/binding.md)|Definisce tutte le funzionalità di associazione dell'associazione personalizzata.|  
  
## Note  
 Questo elemento di configurazione viene usato con trasporti che non consentono comunicazioni duplex a livello nativo, ad esempio, HTTP.  TCP, al contrario, consente comunicazioni duplex a livello nativo e non richiede l'uso di questo elemento di associazione affinché il servizio invii messaggi a un client.  
  
 Il client deve esporre un indirizzo affinché il servizio crei un contatto e stabilisca una connessione.  Questo indirizzo client è fornito dall'attributo `clientBaseAddress`.  Si noti che Windows Communication Foundation \(WCF\) genera automaticamente un ClientBaseAddress se l'utente non ne imposta uno in modo esplicito.  
  
## Esempio  
  
```  
<compositeDuplex clientBaseAddress="http://www.contoso.com" />  
```  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.CompositeDuplexElement>   
 <xref:System.ServiceModel.Channels.CompositeDuplexBindingElement>   
 <xref:System.ServiceModel.Channels.CustomBinding>   
 [Associazioni](../../../../../docs/framework/wcf/bindings.md)   
 [Estensione delle associazioni](../../../../../docs/framework/wcf/extending/extending-bindings.md)   
 [Associazioni personalizzate](../../../../../docs/framework/wcf/extending/custom-bindings.md)   
 [\<customBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)