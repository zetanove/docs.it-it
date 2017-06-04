---
title: "&lt;tipoDefinitoDaUtente&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0f70ec06-8249-4f0c-9f49-b4df59985fb8
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# &lt;tipoDefinitoDaUtente&gt;
Rappresenta un tipo definito dall'utente \(UDT\) che deve essere incluso nel contratto di servizio.  
  
## Sintassi  
  
```  
  
<comContracts>  
  <comContract>  
      <userDefinedTypes>  
         <userDefinedType name="string"  
            typeLibID="string"  
            typeLibVersion="string"  
            typeDefID="string">  
         </userDefinedType>  
      </userDefinedTypes>  
  </comContract>  
</comContracts>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|`name`|Attributo facoltativo contenente una stringa che fornisce il nome tipo leggibile.  Non viene usato dal runtime, ma aiuta un reader a distinguere i tipi.|  
|`TypeDefID`|Stringa GUID che identifica il tipo specifico definito dall'utente all'interno della libreria dei tipi registrati.|  
|`TypeLibID`|Stringa GUID che identifica la libreria dei tipi registrata che definisce il tipo.|  
|`TypeLibVersion`|Stringa che identifica la versione della libreria dei tipi che definisce il tipo.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|`userDefinedTypes`|Raccolta di elementi `userDefinedType`.|  
  
## Note  
 Il runtime di integrazione COM\+ crea servizi controllando la libreria dei tipi.  Quando un componente COM\+ contiene metodi che passano una VARIANT, il sistema non può determinare i tipi effettivi da passare prima della fase di esecuzione.  Quando si tenta pertanto di passare un tipo definito dall'utente \(UDT\) all'interno di una VARIANT, l'operazione non riesce perché non è un tipo noto per la serializzazione.  
  
 Per aggirare questo problema, è possibile aggiungere tipi definiti dall'utente al file di configurazione in modo che possano essere inclusi come tipi noti nel contratto di servizio appropriato.  A tale scopo, è necessario identificare in modo univoco i tipi definiti dall'utente e i contratti, ovvero le interfacce COM originali che li usano.  
  
 L'esempio seguente illustra come aggiungere alla sezione \<`userDefinedTypes`\> del file di configurazione due tipi specifici definiti dall'utente per questo scopo.  
  
```  
<comContracts>  
  <comContract  
      contract="{5163B1E7-F0CF-4B6A-9A02-4AB654F34284}"  
      namespace="http://tempuri.org/5163B1E7-F0CF-4B6A-9A02-4AB654F34284"  
      name="_Broker"  
      requireSession="true">  
      <userDefinedTypes>  
         <userDefinedType name="CustomerType"  
            typeLibID="{91DC728C-4F1A-45de-A9B6-B538E209CEA6}"  
            typeLibVersion="1.0"  
            typeDefID="{D129765C-F211-434e-825A-9A63198C41F2}">  
         </userDefinedType>  
         <userDefinedType name="AddressType"  
            typeLibID="{91DC728C-4F1A-45de-A9B6-B538E209CEA6}"  
            typeLibVersion="1.0"  
            typeDefID="{4616AE0D-687A-43B7-BC63-141AE3DFD099}">  
         </userDefinedType>  
      </userDefinedTypes>  
      <exposedMethods>  
         <exposedMethod name="BuyStock" />  
         <exposedMethod name="SellStock" />  
         <exposedMethod name="ExecuteTransaction" />  
      </exposedMethods>  
  </comContract>  
</comContracts>  
```  
  
 Quando il servizio viene inizializzato, il runtime di integrazione ricerca i tipi specificati e li aggiunge alla raccolta dei tipi noti per i contratti specificati.  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.ComContractElement.UserDefinedTypes%2A>   
 <xref:System.ServiceModel.Configuration.ComUdtElementCollection>   
 <xref:System.ServiceModel.Configuration.ComUdtElement>   
 [\<comContracts\>](../../../../../docs/framework/configure-apps/file-schema/wcf/comcontracts.md)   
 [Integrazione con applicazioni COM\+](../../../../../docs/framework/wcf/feature-details/integrating-with-com-plus-applications.md)   
 [Procedura: configurare le impostazioni del servizio COM\+](../../../../../docs/framework/wcf/feature-details/how-to-configure-com-service-settings.md)