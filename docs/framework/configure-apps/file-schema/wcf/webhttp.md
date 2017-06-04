---
title: "&lt;webHttp&gt; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1f9d0754-d41e-44ce-a298-e51cb3096c64
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# &lt;webHttp&gt;
Questo elemento specifica il comportamento <xref:System.ServiceModel.Description.WebHttpBehavior> in un endpoint tramite la configurazione.  Questo comportamento, quando viene usato insieme all'associazione standard [\<webHttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/webhttpbinding.md), consente di usare il modello di programmazione Web per un servizio [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)].  
  
## Sintassi  
  
```  
  
<webHttp />  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|automaticFormatSelectionEnabled|Quando questa proprietà è impostata su `true`, l'infrastruttura di WCF determina il formato migliore da usare.  La selezione automatica del formato è disabilitata per impostazione predefinita per la compatibilità con le versioni precedenti.  La selezione automatica del formato automatica può essere abilitata a livello di codice o tramite la configurazione.|  
|defaultBodyStyle|Specifica lo stile predefinito del corpo dei messaggi restituiti.  [!INCLUDE[crdefault](../../../../../includes/crdefault-md.md)] <xref:System.ServiceModel.Web.WebMessageBodyStyle> e [Formattazione di HTTP Web WCF](../../../../../docs/framework/wcf/feature-details/wcf-web-http-formatting.md).|  
|defaultOutgoingResponseFormat|Specifica il formato del messaggio di risposta in uscita predefinito per i messaggi.  [!INCLUDE[crdefault](../../../../../includes/crdefault-md.md)]Per altre informazioni, vedere [Formattazione di HTTP Web WCF](../../../../../docs/framework/wcf/feature-details/wcf-web-http-formatting.md).|  
|faultExceptionEnabled|Ottiene o imposta il flag che specifica se viene generata un'eccezione FaultException quando si verifica un errore del server interno \(codice di stato HTTP: 500\).|  
|helpEnabled|Ottiene o imposta un valore che determina se la pagina della Guida è abilitata.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<comportamento\>](../../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md)|Specifica l'insieme di comportamenti dell'endpoint.|  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.WebHttpElement>   
 <xref:System.ServiceModel.Description.WebHttpBehavior>   
 [Integrazione AJAX e supporto JSON](../../../../../docs/framework/wcf/feature-details/ajax-integration-and-json-support.md)   
 [\<webHttpBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/webhttpbinding.md)