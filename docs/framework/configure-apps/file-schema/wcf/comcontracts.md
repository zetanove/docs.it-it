---
title: "&lt;comContracts&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 42e74148-223d-4888-a8ed-1d928527eb09
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# &lt;comContracts&gt;
La sezione di configurazione `comContracts` contiene elementi che consentono di specificare varie proprietà di un contratto di servizio COM\+ Integration.  
  
## Specifica di spazio dei nomi e contratto  
 I contratti di servizio COM\+ Integration sono limitati attualmente allo spazio dei nomi "http:\/\/tempuri.org" e il nome del contratto è derivato dall'interfaccia COM di supporto.  È tuttavia possibile specificare alternative usando la sezione `comContracts` nel file di configurazione.  
  
 Ad esempio, è possibile usare la configurazione seguente per specificare lo spazio dei nomi e il nome del contratto di servizio, oltre a un'opzione per imporre l'uso di associazioni con sessione.  
  
```  
<comContracts>  
  <comContract  
      contract="{5163B1E7-F0CF-4B6A-9A02-4AB654F34284}"  
      namespace="http://tempuri.org/5163B1E7-F0CF-4B6A-9A02-4AB654F34284"  
      name="_Broker"  
      requireSession="true">  
  </comContract>  
</comContracts>  
```  
  
 Quando il servizio viene inizializzato, gli spazi dei nomi specificati e i nomi del contratto vengono applicati alle descrizioni del servizio generate.  
  
 Quando questa sezione è vuota, l'inizializzazione del servizio applica uno spazio dei nomi e un nome del contratto predefiniti presi dall'ID dell'interfaccia COM di supporto.  
  
 In aggiunta, è possibile usare l'elemento [\<exposedMethod\>](../../../../../docs/framework/configure-apps/file-schema/wcf/exposedmethod.md) per specificare metodi COM\+ che vengono esposti quando l'interfaccia in un componente COM\+ viene esposta come servizio Web.  È anche possibile usare [\<persistableTypes\>](../../../../../docs/framework/configure-apps/file-schema/wcf/persistabletypes.md) per specificare i tipi persistenti usati nell'integrazione.  Infine, è possibile usare l'elemento [\<tipoDefinitoDaUtente\>](../../../../../docs/framework/configure-apps/file-schema/wcf/userdefinedtype.md) per includere tipi definiti dall'utente da includere nel contratto del servizio.  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.ComContractElementCollection>   
 <xref:System.ServiceModel.Configuration.ComContractElement>   
 [\<exposedMethod\>](../../../../../docs/framework/configure-apps/file-schema/wcf/exposedmethod.md)   
 [\<persistableTypes\>](../../../../../docs/framework/configure-apps/file-schema/wcf/persistabletypes.md)   
 [\<tipoDefinitoDaUtente\>](../../../../../docs/framework/configure-apps/file-schema/wcf/userdefinedtype.md)   
 [\<contrattoCom\>](../../../../../docs/framework/configure-apps/file-schema/wcf/comcontract.md)   
 [Integrazione con applicazioni COM\+](../../../../../docs/framework/wcf/feature-details/integrating-with-com-plus-applications.md)   
 [Procedura: configurare le impostazioni del servizio COM\+](../../../../../docs/framework/wcf/feature-details/how-to-configure-com-service-settings.md)