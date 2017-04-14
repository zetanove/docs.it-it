---
title: "Elemento &lt;endpoint&gt; | Microsoft Docs"
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
ms.assetid: 2fc8fedc-78d0-4e87-8142-fbfd26c15a4e
caps.latest.revision: 23
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 23
---
# Elemento &lt;endpoint&gt;
Specifica le proprietà di associazione, contratto e indirizzo di endpoint del servizio usato per esporre servizi.  
  
## Sintassi  
  
```  
  
<endpoint address="String"  
   behaviorConfiguration="String"  
   binding="String"  
   bindingConfiguration="String"  
   bindingName="String"  
   bindingNamespace="String"  
   contract="String"  
   endpointConfiguration=”String”  
   isSystemEndpoint=”Boolean”  
   kind=”String”  
   listenUriMode="Explicit/Unique"  
   listenUri="Uri"  
</endpoint>  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|address|Stringa che contiene l'indirizzo dell'endpoint.  L'indirizzo può essere specificato come indirizzo assoluto o relativo.  Se viene fornito un indirizzo relativo, l'host deve fornire un indirizzo di base appropriato per lo schema di trasporto usato nell'associazione.  Se non viene configurato un indirizzo, si presuppone che l'indirizzo di base valga come indirizzo per quell'endpoint.<br /><br /> Il valore predefinito è una stringa vuota.|  
|behaviorConfiguration|Stringa che contiene il nome del comportamento da usare nell'endpoint.|  
|associazione|Attributo stringa obbligatorio che specifica il tipo di associazione da usare.  Il tipo deve avere una sezione di configurazione registrata perché sia possibile farvi riferimento.  Il tipo viene registrato dal nome di sezione, anziché dal nome del tipo di associazione.|  
|bindingConfiguration|Stringa che specifica il nome dell'associazione da usare quando viene creata l'istanza dell'endpoint.  Il nome dell'associazione deve essere nell'ambito del punto in cui l'endpoint viene definito.  Il valore predefinito è una stringa vuota.<br /><br /> Questo attributo viene usato in combinazione con `binding` per fare riferimento a una configurazione di associazione specifica nel file di configurazione.  Impostare questo attributo se si sta tentando di usare un'associazione personalizzata.  In caso contrario, può venire generata un'eccezione.|  
|bindingName|Stringa che specifica il nome completo e univoco dell'associazione per l'esportazione delle definizioni tramite WSDL.  Il valore predefinito è una stringa vuota.|  
|bindingNamespace|Stringa che specifica il nome completo e univoco dello spazio dei nomi dell'associazione per l'esportazione delle definizioni tramite WSDL.  Il valore predefinito è una stringa vuota.|  
|contratto|Stringa che indica quale contratto viene esposto da questo endpoint.  L'assembly deve implementare il tipo di contratto.  Se un'implementazione del servizio implementa un tipo di contratto singolo, questa proprietà può essere omessa.  Il valore predefinito è una stringa vuota.|  
|endpointConfiguration|Stringa che specifica il nome dell'endpoint standard impostato dall'attributo `kind` che fa riferimento alle informazioni di configurazione aggiuntive di questo endpoint standard.  Lo stesso nome deve essere definito nella sezione `<standardEndpoints>`.|  
|isSystemEndpoint|Valore booleano che specifica se un endpoint è un endpoint di infrastruttura.|  
|kind|Stringa che specifica il tipo di endpoint standard applicato.  Il tipo deve essere registrato nella sezione `<extensions>` o in machine.config.  Se non specificato, viene creato un endpoint del servizio comune.|  
|listenUriMode|Specifica il modo in cui il trasporto considera l'elemento `ListenUri` fornito sul quale è in ascolto il servizio.  I valori validi sono:<br /><br /> -   Explicit<br />-   Univoco<br /><br /> Il valore predefinito è Explicit.|  
|listenUri|Stringa che specifica l'URI sul quale è in ascolto l'endpoint del servizio.  Il valore predefinito è una stringa vuota.|  
|name|Attributo facoltativo.  Stringa che specifica il nome dell'endpoint del servizio.  Il valore predefinito è costituito dalla concatenazione del nome dell'associazione e del nome della descrizione del contratto.  È possibile che i servizi siano dotati di più endpoint, quindi l'attributo `name` dell'endpoint si differenzia dal nome del servizio.|  
  
### Elementi figlio  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<intestazioni\>](../../../../../docs/framework/configure-apps/file-schema/wcf/headers.md)|Raccolte di intestazioni di indirizzo.|  
|[\<identità\>](../../../../../docs/framework/configure-apps/file-schema/wcf/identity.md)|Identità che consente l'autenticazione di un endpoint da altri endpoint con i quali vengono scambiati messaggi.|  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<service\>](../../../../../docs/framework/configure-apps/file-schema/wcf/service.md)|Sezione di configurazione che definisce un elenco di endpoint ai quali può connettersi un client.|  
  
## Esempio  
 Di seguito è riportato un esempio di configurazione dell'endpoint di un servizio.  
  
```  
<endpoint   
    address="/HelloWorld/"  
    bindingConfiguration="usingDefaults"  
    bindingName="MyBinding"  
    binding="customBinding"  
    contract="HelloWorld">  
    <Headers>  
       <Region xmlns="http://tempuri.org/">EastCoast</Region>  
       <Member xmlns="http://tempuri.org/">Gold</Member>  
    </Headers>  
</endpoint>  
```  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.ServiceEndpointElement>   
 <xref:System.ServiceModel.EndpointAddress>   
 <xref:System.ServiceModel.Description.ServiceEndpoint>   
 [Endpoint: indirizzi, associazioni e contratti](../../../../../docs/framework/wcf/feature-details/endpoints-addresses-bindings-and-contracts.md)   
 [Procedura: creare un endpoint di servizio nella configurazione](../../../../../docs/framework/wcf/feature-details/how-to-create-a-service-endpoint-in-configuration.md)