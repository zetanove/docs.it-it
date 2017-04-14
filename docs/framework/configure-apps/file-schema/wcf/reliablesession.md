---
title: "&lt;sessioneAttendibile&gt; | Microsoft Docs"
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
ms.assetid: 129b4a59-37f0-4030-b664-03795d257d29
caps.latest.revision: 19
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 19
---
# &lt;sessioneAttendibile&gt;
Definisce l'impostazione per WS\-Reliable Messaging.  Quando questo elemento viene aggiunto a un'associazione personalizzata, il canale risultante può supportare assicurazioni di recapito una volta esatta.  
  
## Sintassi  
  
```  
  
<reliableSession acknowledgementInterval="TimeSpan"  
        flowControlEnabled="Boolean"   
    inactivityTimeout="TimeSpan"  
    maxPendingChannels="Integer"  
    maxRetryCount="Integer"   
        maxTransferWindowSize="Integer"  
    reliableMessagingVersion="Default/WSReliableMessagingFebruary2005/WSReliableMessaging11"  
    ordered="Boolean" />  
```  
  
## Attributi ed elementi  
 Nelle sezioni seguenti vengono descritti gli attributi, gli elementi figlio e gli elementi padre.  
  
### Attributi  
  
|Attributo|Descrizione|  
|---------------|-----------------|  
|acknowledgementInterval|<xref:System.TimeSpan> che contiene l'intervallo di attesa massimo del canale per l'invio di un riconoscimento dei messaggi ricevuti fino a quel punto.  Il valore predefinito è 00:00:02.|  
|flowControlEnabled|Valore booleano che indica se è attivato il controllo di flusso avanzato, un'implementazione specifica di Microsoft del controllo di flusso per WS\-Affidabile Messaging.  Il valore predefinito è `true`.|  
|inactivityTimeout|Valore <xref:System.TimeSpan> che specifica la durata massima durante la quale il canale consente all'altra parte della comunicazione di non inviare messaggi prima di generare un errore per il canale.  L'impostazione predefinita è 00:10:00.<br /><br /> L'attività in un canale viene definita come ricezione di messaggi di un'applicazione o di un'infrastruttura.  Questa proprietà controlla la durata massima in attività di una sessione inattiva.  Se il periodo di inattività è più lungo, la sessione viene interrotta dall'infrastruttura e viene generato un errore per il canale. **Note:**  Per tenere attiva la connessione non è necessario che l'applicazione invii periodicamente messaggi.|  
|maxPendingChannels|Numero intero che specifica il numero massimo di canali che possono attendere nel listener prima di essere accettati.  Questo valore deve essere compreso tra 1 e 16384 inclusi.  Il valore predefinito è 4.<br /><br /> I canali sono in sospeso quando attendono di essere accettati.  Una volta che tale limite viene raggiunto, non vengono creati canali.  Invece, questi vengono impostati in modalità sospesa finché questo numero non diminuisce, accettando i canali in sospeso.  Si tratta di un limite per\-factory.<br /><br /> Quando la soglia viene raggiunta e un'applicazione remota tenta di stabilire una nuova sessione affidabile, la richiesta è negata e l'operazione di apertura che ha inviato la richiesta produce un errore.  Questo limite non si applica al numero di canali in uscita in sospeso.|  
|maxRetryCount|Numero intero che specifica il numero massimo di tentativi di ritrasmissione di un messaggio per il quale un canale affidabile non ha ricevuto un riconoscimento, tramite una chiamata a Send sul canale sottostante.<br /><br /> Questo valore deve essere maggiore di zero.  Il valore predefinito è 8.<br /><br /> Il valore deve essere un intero maggiore di zero.  Se non viene ricevuto un riconoscimento dopo l'ultima ritrasmissione, il canale genera un errore.<br /><br /> Un messaggio è considerato trasferito se il recapito al destinatario è stato dato riconosciuto dal destinatario.<br /><br /> Se entro una certa quantità di tempo non è stato ricevuto un riconoscimento per un messaggio trasmesso, l'infrastruttura lo ritrasmette automaticamente.  L'infrastruttura tenta a reinviare il messaggio almeno per il numero di volte specificato da questa proprietà.  Se non viene ricevuto un riconoscimento dopo l'ultima ritrasmissione, il canale genera un errore.<br /><br /> L'infrastruttura usa un algoritmo di interruzione temporanea esponenziale per determinare quando ritrasmettere, in base a un tempo medio di andata e ritorno calcolato.  Il periodo parte inizialmente 1 secondo prima della ritrasmissione raddoppiando il ritardo con ogni tentativo, che si traduce approssimativamente in 8,5 minuti tra il primo tentativo della trasmissione e l'ultimo.  Il momento del primo tentativo di ritrasmissione viene regolato in base al tempo di andata e ritorno calcolato e l'adattamento temporale richiesto da tali tentativi varia di conseguenza.  Questo consente di adattare dinamicamente il tempo di ritrasmissione alle mutevoli condizioni della rete.|  
|maxTransferWindowSize|\[out\] Valore intero che specifica la dimensione massima del buffer.  I valori validi sono compresi tra 1 e 4096 inclusi.<br /><br /> Sul client, questo attributo definisce la dimensione massima del buffer usata da un canale affidabile per contenere i messaggi non riconosciuti dal ricevitore.  L'unità della quota è un messaggio.  Se il buffer è pieno, ulteriori operazioni SNED vengono bloccate.<br /><br /> Sul ricevitore, questo attributo definisce la dimensione massima del buffer usata dal canale per memorizzare i messaggi non ancora inviati all'applicazione.  Se il buffer è pieno, ulteriori messaggi vengono rilasciati silenziosamente dal ricevitore e richiedono la ritrasmissione da parte del client.|  
|ordered|Valore booleano che specifica se viene garantito l'arrivo dei messaggi nell'ordine in cui sono stati inviati.  Se l'impostazione è `false`, i messaggi possono arrivare in qualsiasi ordine.  Il valore predefinito è `true`.|  
|reliableMessagingVersion|Un valore valido da <xref:System.ServiceModel.ReliableMessagingVersion> che specifica la versione di WS\-ReliableMessaging da usare.|  
  
### Elementi figlio  
 None  
  
### Elementi padre  
  
|Elemento|Descrizione|  
|--------------|-----------------|  
|[\<associazione\>](../../../../../docs/framework/misc/binding.md)|Definisce tutte le funzionalità di associazione dell'associazione personalizzata.|  
  
## Note  
 Le sessioni affidabili forniscono funzionalità per la messaggistica affidabile e le sessioni.  La messaggistica affidabile ritenta la comunicazione in caso di errore e consente di specificare assicurazioni del recapito quali l'arrivo nell'ordine di invio dei messaggi.  Le sessioni gestiscono lo stato per i client tra le chiamate.  Questo elemento fornisce inoltre il recapito ordinato dei messaggi \(facoltativo\).  Questa sessione implementata può attraversare intermediari SOAP e di trasporto.  
  
 Ogni elemento di associazione rappresenta una fase di elaborazione durante l'invio o la ricezione di messaggi.  In fase di esecuzione gli elementi di associazione creano le channel factory e i listener necessari per compilare stack di canali in uscita e in ingresso richiesti per l'invio e la ricezione di messaggi.  La classe `reliableSession` fornisce un livello facoltativo nello stack che può stabilire una sessione affidabile tra endpoint e configurare il comportamento di questa sessione.  
  
 Per altre informazioni, vedere [Sessioni affidabili](../../../../../docs/framework/wcf/feature-details/reliable-sessions.md).  
  
## Esempio  
 Nell'esempio seguente è dimostrato come configurare un'associazione personalizzata con vari elementi di codifica di trasporto e messaggio, in particolare l'attivazione di sessioni affidabili, che mantiene lo stato client e specifica assicurazioni di recapito nell'ordine.  Questa funzionalità è configurata nei file di configurazione dell'applicazione per il client e il servizio.  Nell'esempio è illustrata la configurazione del servizio.  
  
```  
<?xml version="1.0" encoding="utf-8" ?>  
<configuration>  
  <system.serviceModel>  
    <services>  
      <service   
          name="Microsoft.ServiceModel.Samples.CalculatorService"  
          behaviorConfiguration="CalculatorServiceBehavior">  
        <!-- This endpoint is exposed at the base address provided by host: http://localhost/servicemodelsamples/service.svc  -->  
        <!-- specify customBinding binding and a binding configuration to use -->  
        <endpoint address=""  
                  binding="customBinding"  
                  bindingConfiguration="Binding1"   
                  contract="Microsoft.ServiceModel.Samples.ICalculator" />  
        <!-- The mex endpoint is exposed at http://localhost/servicemodelsamples/service.svc/mex -->  
        <endpoint address="mex"  
                  binding="mexHttpBinding"  
                  contract="IMetadataExchange" />  
      </service>  
    </services>  
  
    <!-- custom binding configuration - configures HTTP transport, reliable sessions -->  
    <bindings>  
      <customBinding>  
        <binding name="Binding1">  
          <reliableSession />  
          <security authenticationMode="SecureConversation"  
                     requireSecurityContextCancellation="true">  
          </security>  
          <compositeDuplex />  
          <oneWay />  
          <textMessageEncoding messageVersion="Soap12WSAddressing10" writeEncoding="utf-8" />  
          <httpTransport authenticationScheme="Anonymous" bypassProxyOnLocal="false"  
                        hostNameComparisonMode="StrongWildcard"   
                        proxyAuthenticationScheme="Anonymous" realm=""   
                        useDefaultWebProxy="true" />  
        </binding>  
      </customBinding>  
    </bindings>  
  
    <!--For debugging purposes set the includeExceptionDetailInFaults attribute to true-->  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="CalculatorServiceBehavior">  
          <serviceMetadata httpGetEnabled="True"/>  
          <serviceDebug includeExceptionDetailInFaults="False" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
```  
  
## Vedere anche  
 <xref:System.ServiceModel.Configuration.ReliableSessionElement>   
 <xref:System.ServiceModel.Channels.CustomBinding>   
 <xref:System.ServiceModel.Channels.ReliableSessionBindingElement>   
 [Sessioni affidabili](../../../../../docs/framework/wcf/feature-details/reliable-sessions.md)   
 [Associazioni](../../../../../docs/framework/wcf/bindings.md)   
 [Estensione delle associazioni](../../../../../docs/framework/wcf/extending/extending-bindings.md)   
 [Associazioni personalizzate](../../../../../docs/framework/wcf/extending/custom-bindings.md)   
 [\<customBinding\>](../../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)