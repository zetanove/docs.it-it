---
title: "Configurazione della traccia del flusso di messaggi | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 15571ca2-bee2-47fb-ba10-fcbc09152ad0
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Configurazione della traccia del flusso di messaggi
Se la traccia delle attività di [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)] è abilitata, gli ID di attività end\-to\-end vengono assegnati alle attività logiche in tutto lo stack [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)].  In [!INCLUDE[netfx_current_short](../../../../../includes/netfx-current-short-md.md)] è ora disponibile una versione con prestazioni superiori di questa funzionalità utilizzabile con Event Tracing for Windows \(ETW\) denominata traccia del flusso di messaggi.  Se abilitati, gli ID di attività end\-to\-end vengono raccolti dai messaggi in ingresso o assegnati a tali messaggi se vuoti e vengono propagati in tutti gli eventi di traccia generati successivamente alla decodifica del messaggio da parte del canale.  I clienti possono utilizzare questa funzionalità per ricostruire flussi di messaggi con i log di traccia dai vari servizi dopo la decodifica.  
  
 La traccia può essere abilitata in seguito al rilevamento di un problema con l'applicazione, quindi disabilitata una volta che il problema viene risolto.  
  
## Abilitazione della traccia  
 È possibile abilitare la traccia del flusso di messaggi impostando l'elemento di configurazione `messageFlowTracing` di .NET Framework 4 su `true`, come mostrato nell'esempio seguente.  
  
```  
<system.servicemodel>  
  <diagnostics>  
    <endToEndTracing propagateActivity="true" messageFlowTracing="true" />  
  </diagnostics>  
</system.servicemodel>  
  
```  
  
> [!NOTE]
>  Poiché l'elemento di configurazione `endToEndTracing` si trova in un file Web.config, non può essere configurato dinamicamente in modo analogo a ETW.  Affinché l'elemento di configurazione `endToEndTracing` venga applicato, è necessario riciclare l'applicazione.  
  
 Le attività sono correlate dall'interscambio di un identificatore denominato ID attività.  Questo identificatore è un GUID e viene generato dalla classe System.Diagnostics.CorrelationManager.  Se si modifica System.Diagnostics.Trace.CorrelationManager.ActivityID, assicurarsi che il valore venga impostato sul valore originale quando il controllo dell'esecuzione viene trasferito di nuovo al codice WCF.  Inoltre, se si utilizza un modello di programmazione WCF asincrono, assicurarsi che System.Diagnostics.Trace.CorrelationManager.ActivityID venga trasferito tra i thread.  
  
## Traccia del flusso di messaggi e servizi REST  
 La traccia del flusso di messaggi consente di tracciare una richiesta end\-to\-end.  Con i servizi basati su SOAP un ID attività viene inviato n un'intestazione di messaggio SOAP.  Le richieste REST non contengono questa intestazione, per cui viene invece utilizzata un'intestazione di evento HTTP speciale.  Nel frammento di codice seguente viene illustrato come recuperare il valore dell'ID attività a livello di codice:  
  
```vb  
  
Object output = null;                    
if (OperationContext.Current.IncomingMessageProperties.TryGetValue(HttpRequestMessageProperty.Name, out output))  
{  
   HttpRequestMessageProperty httpHeaders = output as HttpRequestMessageProperty;       
   // Retrieve the Activity Id from the HTTP header    string e2eId = httpHeaders.Headers["E2EActivity"];  
   // ...  
}  
  
```  
  
 È possibile aggiungere l'intestazione a livello di codice utilizzando codice seguente:  
  
```csharp  
  
HttpContent content = new StreamContent(contentStream);  
Guid correlation = Guid.NewGuid();  
content.Headers.Add("E2EActivity", Convert.ToBase64String(correlation.ToByteArray()));  
  
```