---
title: "&lt;oneWay&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 00e67e0e-77c0-4695-9138-c0997b0e5f3c
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# &lt;oneWay&gt;
Abilita il routing dei pacchetti e l'uso di metodi unidirezionali per un'associazione personalizzata.  
  
## Sintassi  
  
```  
  
<oneWay packetRoutable="Boolean">  
        <channelPoolSettings  
           idleTimeout"TimeSpan"  
          leaseTimeout"TimeSpan"  
          maxOutboundConnectionsPerEndpopint=”Integer” />  
```  
  
```  
  
</oneWay>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`packetRoutable`|Valore booleano che specifica se è attivato il routing dei pacchetti.  Il valore predefinito è `false`.|  
|`MaxAcceptedChannels`|Numero intero che specifica il numero massimo di canali che possono essere accettati.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<impostazioniPoolCanali\>](../../../../../docs/framework/configure-apps/file-schema/wcf/channelpoolsettings.md)|Oggetto <xref:System.ServiceModel.Configuration.ChannelPoolSettingsElement> che contiene le proprietà del pool di canali per il canale corrente.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<associazione\>](../../../../../docs/framework/misc/binding.md)|Definisce tutte le funzionalità di associazione dell'associazione personalizzata.|  
  
## Note  
 Per abilitare il routing dei pacchetti, è necessario un livello di conversione unidirezionale, fornito da questo elemento.  Un utente può creare un'associazione personalizzata che sovrapponga questa associazione su un trasporto in grado di riconoscere la sessione o un trasporto Request\/Reply affinché supporti il routing dei pacchetti.  Questa elemento può essere inoltre usato quando si desidera esporre metodi unidirezionali in modo più nativo.  Su questo livello possono essere applicate più trasformazioni, ad esempio duplex composito e messaggistica attendibile.  
  
## Vedere anche  
 <xref:System.ServiceModel.Channels.OneWayBindingElement>   
 <xref:System.ServiceModel.Configuration.OneWayElement>   
 <xref:System.ServiceModel.Channels.CustomBinding>   
 [Associazioni](../../../../../docs/framework/wcf/bindings.md)   
 [Estensione delle associazioni](../../../../../docs/framework/wcf/extending/extending-bindings.md)   
 [Associazioni personalizzate](../../../../../docs/framework/wcf/extending/custom-bindings.md)   
 [\<customBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)