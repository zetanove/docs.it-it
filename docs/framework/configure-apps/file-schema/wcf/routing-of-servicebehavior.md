---
title: "&lt;routing&gt; di &lt;serviceBehavior&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: d8f9c844-4629-4a45-9599-856dc8f01794
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# &lt;routing&gt; di &lt;serviceBehavior&gt;
Fornisce l'accesso in fase di esecuzione al servizio di routing per consentire la modifica dinamica della configurazione di routing.  
  
## Sintassi  
  
```  
  
<behaviors>  
  <serviceBehaviors>  
    <behavior name=String">  
      <routing filterTable=”String”  
         routeOnHeadersOnly="Boolean"  
         SoapProcessingEnabled=”Boolean” />  
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|filterTable|Stringa che specifica il nome della tabella di routing contenente i filtri per la valutazione da parte del servizio di routing.  Questo valore deve corrispondere all'attributo `name` di un elemento [\<filterTable\>](../../../../../docs/framework/configure-apps/file-schema/wcf/filtertable.md) nella sezione [\<filterTables\>](../../../../../docs/framework/configure-apps/file-schema/wcf/filtertables.md).|  
|routeOnHeaderOnly|Valore booleano che specifica se il filtro esaminerà il corpo del messaggio e l'intestazione oppure solo l'intestazione.  Il valore predefinito è `true`.|  
|soapProcessingEnabled|Valore booleano che specifica se è necessario che si verifichi l'elaborazione SOAP.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<comportamento\>](../../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md)|Specifica un elemento di comportamento.|  
  
## Note  
 Quando viene aggiunto alla configurazione del comportamento del servizio, questo elemento di configurazione abilita il routing del servizio.  È possibile specificare la tabella di routing effettiva per l'uso da parte del servizio in questo elemento.  
  
 L'utilizzo di questa sezione di configurazione consente di modificare le impostazioni di routing non appena cambia il modello di distribuzione.  In fase di runtime è possibile registrare l'estensione di routing personalizzata con le nuove impostazioni del routing e il servizio di routing inizierà a usare le informazioni di configurazione aggiornate per i nuovi messaggi e sessioni, mentre per i messaggi e le sessioni in corso continueranno a essere usate le regole implementate al momento dell'avvio. In questo modo è possibile eseguire la riconfigurazione indipendente dalla sessione e senza riciclo del servizio di routing in fase di runtime.  
  
## Vedere anche  
 <xref:System.ServiceModel.Routing.RoutingExtenstion>   
 <xref:System.ServiceModel.Routing.Configuration.RoutingExtenstionElement>