---
title: "&lt;limitazioneServizio&gt; | Microsoft Docs"
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
ms.assetid: a337d064-1e64-4209-b4a9-db7fdb7e3eaf
caps.latest.revision: 22
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 22
---
# &lt;limitazioneServizio&gt;
Specifica il meccanismo della limitazione di un servizio Windows Communication Foundation \(WCF\).  
  
## Sintassi  
  
```  
  
<serviceThrottling maxConcurrentCalls="Integer"  
    maxConcurrentInstances="Integer"  
    maxConcurrentSessions="Integer" />  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|maxConcurrentCalls|Numero intero positivo che limita il numero di messaggi attualmente elaborati in un oggetto <xref:System.ServiceModel.ServiceHost>.  Le chiamate in eccesso vengono messe in coda.  L'impostazione di questo valore su 0 è equivalente alla relativa impostazione su Int32.MaxValue.  L'impostazione predefinita è 16 \* il numero dei processori.|  
|maxConcurrentInstances|Numero intero positivo che limita il numero di oggetti <xref:System.ServiceModel.InstanceContext> eseguiti contemporaneamente in un oggetto <xref:System.ServiceModel.ServiceHost>.  Le richieste di creare istanze aggiuntive vengono messe in coda e completate quando diventa disponibile uno slot sotto il limite.  L'impostazione predefinita è la somma di maxConcurrentSessions più MaxConcurrentCalls|  
|maxConcurrentSessions|Numero intero positivo che limita il numero di sessioni che possono essere accettate da un oggetto <xref:System.ServiceModel.ServiceHost>.<br /><br /> Il servizio accetterà le connessioni oltre il limite, ma sono attivi solo i canali sotto il limite \(i messaggi vengono letti dal canale\).  L'impostazione di questo valore su 0 è equivalente alla relativa impostazione su Int32.MaxValue.  L'impostazione predefinita è 100 \* il numero dei processori.|  
  
### Elementi figlio  
 Nessuno.  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<comportamento\>](../../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-endpointbehaviors.md)|Specifica un elemento di comportamento.|  
  
## Note  
 I controlli di limitazione pongono dei limiti sul numero di chiamate, istanze o sessioni simultanee per impedire l'uso eccessivo di risorse.  
  
 Viene scritta una traccia ogni volta che viene raggiunto il valore di attributi.  La prima traccia viene scritta come un avviso.  
  
## Esempio  
 Nell'esempio di configurazione seguente viene specificato che il servizio limita il numero massimo di chiamate simultanee a 2 e il numero massimo di istanze simultanee a 10.  Per un esempio dettagliato relativo all'esecuzione dell'esempio, vedere [Limitazione](../../../../../docs/framework/wcf/samples/throttling.md).  
  
```  
<behaviors>   
  <serviceBehaviors>   
    <behavior name="CalculatorServiceBehavior">   
      <serviceDebug includeExceptionDetailInFaults="False" />   
      <serviceMetadata httpGetEnabled="True"/>   
      <!-- Specify throttling behavior -->  
      <serviceThrottling maxConcurrentCalls="2"   
           maxConcurrentInstances="10"/>   
    </behavior>  
  </serviceBehaviors>  
</behaviors>  
```  
  
## Vedere anche  
 <xref:System.ServiceModel.Description.ServiceThrottlingBehavior>   
 <xref:System.ServiceModel.Configuration.ServiceThrottlingElement>   
 [Uso di ServiceThrottlingBehavior per controllare le prestazioni dei servizi WCF](../../../../../docs/framework/wcf/feature-details/using-servicethrottlingbehavior-to-control-wcf-service-performance.md)