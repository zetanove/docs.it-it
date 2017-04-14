---
title: "Servizi unidirezionali | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "contratti di servizio [WCF], definizione unidirezionale"
  - "WCF [WCF], contratti di servizio unidirezionale"
  - "Windows Communication Foundation [WCF], contratti di servizio unidirezionale"
ms.assetid: 19053a36-4492-45a3-bfe6-0365ee0205a3
caps.latest.revision: 18
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 18
---
# Servizi unidirezionali
Il comportamento predefinito di un'operazione del servizio segue il modello request\-reply,in base al quale il client resta in attesa del messaggio di risposta, anche se l'operazione del servizio è rappresentata nel codice come metodo `void`.Con un'operazione unidirezionale, viene invece trasmesso solo un messaggio.Il destinatario non invia un messaggio di risposta, né il mittente ne aspetta uno.  
  
 Utilizzare il modello di progettazione unidirezionale nelle situazioni seguenti:  
  
-   Quando il client deve chiamare operazioni e il risultato dell'operazione non influisce su di esso a livello di operazione.  
  
-   Quando si utilizza la classe <xref:System.ServiceModel.NetMsmqBinding> o la classe <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding>.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] su questo scenario, vedere [Code in WCF](../../../../docs/framework/wcf/feature-details/queues-in-wcf.md).  
  
 Quando un'operazione è unidirezionale, non ci sarà alcun messaggio di risposta per trasportare le informazioni di errore al client.È possibile rilevare le condizioni di errore utilizzando le funzionalità dell'associazione sottostante, ad esempio le sessioni affidabili, o progettando un contratto di servizio duplex che utilizza due operazioni unidirezionali, ovvero un contratto unidirezionale dal client al servizio per chiamare l'operazione del servizio e un altro contratto unidirezionale tra il servizio e il client in modo che il servizio possa inviare gli errori al client utilizzando un callback implementato dal client.  
  
 Per creare un contratto di servizio unidirezionale, definire il contratto del servizio, applicare la classe <xref:System.ServiceModel.OperationContractAttribute> a ogni operazione e impostare la proprietà <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> su `true`, come illustrato nel codice di esempio seguente.  
  
```  
[ServiceContract(Namespace="http://Microsoft.ServiceModel.Samples")]  
public interface IOneWayCalculator  
{  
    [OperationContract(IsOneWay=true)]  
    void Add(double n1, double n2);  
    [OperationContract(IsOneWay = true)]  
    void Subtract(double n1, double n2);  
    [OperationContract(IsOneWay = true)]  
    void Multiply(double n1, double n2);  
    [OperationContract(IsOneWay = true)]  
    void Divide(double n1, double n2);  
}  
```  
  
 Per un esempio completo, vedere [Unidirezionale](../../../../docs/framework/wcf/samples/one-way.md).  
  
## Blocco dei client con operazioni unidirezionali  
 È importante tenere presente che, mentre alcune applicazioni unidirezionali eseguono la restituzione non appena i dati in uscita vengono scritti nella connessione di rete, in vari scenari l'implementazione di un'associazione o di un servizio può causare il blocco di un client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] quando si utilizzano operazioni unidirezionali.Nelle applicazioni client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], l'oggetto client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non esegue la restituzione fino a quando i dati in uscita non sono stati scritti nella connessione di rete.Questo vale per tutti i modelli di scambio dei messaggi, comprese le operazioni bidirezionali; ciò significa che qualsiasi problema durante la scrittura dei dati sul trasporto impedisce al client di eseguire la restituzione.A seconda del problema, il risultato potrebbe essere un'eccezione o un ritardo nell'invio di messaggi al servizio.  
  
 Ad esempio, se il trasporto non è in grado di individuare l'endpoint, viene generata un'eccezione <xref:System.ServiceModel.EndpointNotFoundException?displayProperty=fullName> senza molto ritardo.È tuttavia possibile che per qualche motivo il servizio non sia in grado di leggere i dati fuori transito, impedendo così all'operazione di invio del trasporto client di eseguire la restituzione.In questi casi, se viene superato il periodo di <xref:System.ServiceModel.Channels.Binding.SendTimeout%2A?displayProperty=fullName> sull'associazione del trasporto client, viene generata una <xref:System.TimeoutException?displayProperty=fullName>, ma non prima che il periodo di timeout sia scaduto.È inoltre possibile che siano generati così tanti messaggi su un servizio che il servizio non è in grado di elaborarli oltre un certo punto.Anche in questo caso il client unidirezionale si blocca fino a quando il servizio non può elaborare i messaggi o fino a quando non viene generata un'eccezione.  
  
 Un'altra variazione è rappresentata dalla situazione in cui la proprietà  <xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A?displayProperty=fullName> del servizio è impostata su <xref:System.ServiceModel.ConcurrencyMode> e l'associazione utilizza sessioni.In questo caso, il dispatcher applica l'ordinamento sui messaggi in arrivo \(un requisito delle sessioni\), il che impedisce ai messaggi successivi di essere letti fuori rete fino a quando il servizio non ha elaborato il messaggio precedente per tale sessione.Il client quindi si blocca, ma la generazione di un'eccezione dipende da se il servizio è in grado di elaborare i dati in attesa prima delle impostazioni di timeout sul client.  
  
 È possibile attenuare parte di questo problema inserendo un buffer tra l'oggetto client e l'operazione di invio del trasporto client.Ad esempio, l'utilizzo di chiamate asincrone o di una coda di messaggi in memoria può consentire all'oggetto client di eseguire rapidamente la restituzione.Entrambi gli approcci possono aumentare la funzionalità, ma la dimensione del pool di thread e della coda di messaggi impongono dei limiti.  
  
 È invece consigliabile esaminare i vari controlli sul servizio e sul client e quindi testare gli scenari dell'applicazione per determinare la configurazione migliore su ogni lato.Ad esempio, se l'utilizzo di sessioni blocca l'elaborazione di messaggi nel servizio, è possibile impostare la proprietà <xref:System.ServiceModel.ServiceBehaviorAttribute.InstanceContextMode%2A?displayProperty=fullName> su <xref:System.ServiceModel.InstanceContextMode>, in modo che ogni messaggio possa essere elaborato da un'istanza diversa del servizio, e impostare la proprietà <xref:System.ServiceModel.ServiceBehaviorAttribute.ConcurrencyMode%2A> su <xref:System.ServiceModel.ConcurrencyMode> per consentire a più di un thread alla volta di inviare messaggi.Un altro approccio consiste nell'aumentare le quote di lettura delle associazioni del servizio e del client.  
  
## Vedere anche  
 [Unidirezionale](../../../../docs/framework/wcf/samples/one-way.md)