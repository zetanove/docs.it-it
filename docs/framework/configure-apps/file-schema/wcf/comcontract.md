---
title: "&lt;contrattoCom&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3f8e1c0c-cfdf-4c79-ac65-c64e9323a51c
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# &lt;contrattoCom&gt;
Specifica un contratto del servizio COM\+ Integration.  
  
## Sintassi  
  
```  
  
<comContracts>  
  <comContract  
      contract="string"  
      namespace="string"  
      name="string"  
      requireSession="Boolean">  
      <exposedMethods>  
         <exposedMethod name="string" />  
      </exposedMethods>  
      <userDefinedTypes>  
         <userDefinedType name="string"  
            typeLibID="string"  
            typeLibVersion="string"  
            typeDefID="string">  
         </userDefinedType>  
      </userDefinedTypes>  
      <persistableTypes>  
         <persistableType id="string"  
            name="string">  
         </persistableType>  
      </persistableTypes>  
  </comContract>  
</comContracts>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|contratto|Stringa che contiene il tipo di contratto.|  
|name|Stringa che contiene il nome del contratto.|  
|namespace|Stringa che contiene lo spazio dei nomi del contratto.|  
|requiresSession|Valore booleano che specifica se il contratto può essere usato solo nelle associazioni con sessione.  All'avvio del servizio, il runtime di integrazione verifica che questa impostazione sia coerente con il tipo di associazione da usare.  Viene generata un'eccezione se una o più delle associazioni per il contratto sono in conflitto tra loro.  Se questa proprietà è `false` e viene usato un canale unidirezionale in presenza di parametri \[out\], viene generata un'eccezione.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|persistableTypes|Tutti i tipi persistenti.|  
|userDefinedTypes|Raccolta di tipi definiti dall'utente che deve essere inclusa nel contratto di servizio.|  
|exposedMethods|Raccolta di metodi COM\+ che vengono esposti quando l'interfaccia in un componente COM\+ viene esposta come servizio Web.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|comContracts|Contiene una raccolta di elementi `comContract`.|  
  
## Note  
 I contratti di servizio COM\+ Integration sono limitati attualmente allo spazio dei nomi "http:\/\/tempuri.org" e il nome del contratto è derivato dall'interfaccia COM di supporto.  È tuttavia possibile specificare alternative usando la sezione `comContracts` e anche l'elemento `comContract` nel file di configurazione.  Ad esempio, è possibile usare la configurazione seguente per specificare lo spazio dei nomi, il nome del contratto, i tipi definiti dall'utente da includere e altre impostazioni per un contratto di servizio.  
  
```  
<comContracts>  
  <comContract  
      contract="{5163B1E7-F0CF-4B6A-9A02-4AB654F34284}"  
      namespace="http://tempuri.org/5163B1E7-F0CF-4B6A-9A02-4AB654F34284"  
      name="_Broker"  
      requireSession="true">  
      <exposedMethods>  
         <exposedMethod name="BuyStock" />  
         <exposedMethod name="SellStock" />  
         <exposedMethod name="ExecuteTransaction" />  
      </exposedMethods>  
  </comContract>  
</comContracts>  
```  
  
 Quando il servizio viene inizializzato, gli spazi dei nomi specificati e i nomi del contratto vengono applicati alle descrizioni del servizio generate.  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.ComContractElementCollection>   
 <xref:System.ServiceModel.Configuration.ComContractElementCollection>   
 <xref:System.ServiceModel.Configuration.ComContractElement>   
 [\<comContracts\>](../../../../../docs/framework/configure-apps/file-schema/wcf/comcontracts.md)   
 [Integrazione con applicazioni COM\+](../../../../../docs/framework/wcf/feature-details/integrating-with-com-plus-applications.md)   
 [Procedura: configurare le impostazioni del servizio COM\+](../../../../../docs/framework/wcf/feature-details/how-to-configure-com-service-settings.md)