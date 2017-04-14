---
title: "&lt;add&gt; di &lt;protocolMapping&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 08e62249-1641-41d1-91b1-66d7b46244e4
caps.latest.revision: 2
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 2
---
# &lt;add&gt; di &lt;protocolMapping&gt;
Rappresenta un mapping del protocollo predefinito tra lo schema di un protocollo di trasporto \(ad esempio http, net.tcp, net.pipe e così via\) e l'associazione di [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)].  Durante la creazione di endpoint predefiniti in fase di esecuzione, [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] analizza i mapping configurati e determina l'associazione da usare per un particolare indirizzo di base.  
  
## Sintassi  
  
```vb  
  
<protocolMapping>  
    <add binding="String”  
         bindingConfiguration="String”  
         scheme="http/net.msmq/net.pipe/net.tcp"/>  
</protocolMapping>  
  
```  
  
```csharp  
  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|associazione|Stringa che specifica il tipo di associazione da usare per un endpoint durante la creazione dell'endpoint predefinito.|  
|bindingConfiguration|Stringa che specifica il nome della sezione di configurazione dell'associazione alla quale fare riferimento.|  
|scheme|Schema del protocollo di trasporto da usare per l'endpoint predefinito.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<protocolMapping\>](../../../../../docs/framework/configure-apps/file-schema/wcf/protocolmapping.md)|Rappresenta una sezione di configurazione per la definizione dei mapping di protocolli predefiniti tra gli schemi dei protocolli di trasporto \(ad esempio http, net.tcp, net.pipe e così via\) e le associazioni di [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)].|  
  
## Esempio  
 Nell'esempio di configurazione seguente viene illustrato il mapping del protocollo predefinito nel file machine.config.  È possibile eseguire l'override di questo mapping predefinito al livello di computer modificando il file machine.config.  In alternativa, se si desidera eseguirne l'override solo nell'ambito di un'applicazione, è possibile eseguire l'override di questa sezione all'interno del file di configurazione dell'applicazione e modificare il mapping per i singoli schemi di protocollo.  
  
```  
  
<protocolMapping>  
        <add scheme="http" binding="basicHttpBinding"/>  
        <add scheme="net.tcp" binding="netTcpBinding"/>  
        <add scheme="net.pipe" binding="netNamedPipeBinding"/>  
        <add scheme="net.msmq" binding="netMsmqBinding"/>  
</protocolMapping>  
  
```  
  
## Vedere anche  
 [System.ServiceModel.Configuration.ProtocolMappingSection](assetId:///System.ServiceModel.Configuration.ProtocolMappingSection?qualifyHint=False&amp;autoUpgrade=True)   
 [System.ServiceModel.Configuration.ProtocolMappingElement](assetId:///System.ServiceModel.Configuration.ProtocolMappingElement?qualifyHint=False&amp;autoUpgrade=True)