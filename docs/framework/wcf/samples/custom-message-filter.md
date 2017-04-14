---
title: "Filtro messaggi personalizzato | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 98dd0af8-fce6-4255-ac32-42eb547eea67
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# Filtro messaggi personalizzato
Questo esempio dimostra come sostituire i filtri messaggi che [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] utilizza per distribuire messaggi agli endpoint.  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine di questo argomento.  
  
 Quando il primo messaggio su un canale arriva al server, il server deve determinare quale degli endpoint associati all'URI \(se presenti\) deve ricevere il messaggio.Questo processo viene controllato dagli oggetti <xref:System.ServiceModel.Dispatcher.MessageFilter> allegati a <xref:System.ServiceModel.Dispatcher.EndpointDispatcher>.  
  
 Ogni endpoint di un servizio ha un solo <xref:System.ServiceModel.Dispatcher.EndpointDispatcher>.La classe <xref:System.ServiceModel.Dispatcher.EndpointDispatcher> è dotata delle proprietà <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.AddressFilter%2A> e <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.ContractFilter%2A>.L'unione di questi due filtri è il filtro messaggi utilizzato per quell'endpoint.  
  
 Per impostazione predefinita, la proprietà <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.AddressFilter%2A> per un endpoint corrisponde a qualsiasi messaggio indirizzato a un indirizzo che corrisponde alla classe <xref:System.ServiceModel.EndpointAddress> dell'endpoint del servizio.Per impostazione predefinita, la proprietà <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.ContractFilter%2A> per un endpoint esamina l'azione del messaggio in ingresso e corrisponde a qualsiasi messaggio con un'azione che corrisponde a una delle azioni delle operazioni del contratto dell'endpoint del servizio \(vengono considerate solo le azioni `IsInitiating`\=`true`\).Di conseguenza, per impostazione predefinita il filtro per un endpoint corrisponde solo se l'intestazione di destinazione del messaggio rappresenta la classe <xref:System.ServiceModel.EndpointAddress> dell'endpoint e l'azione del messaggio corrisponde a una delle azioni dell'operazione dell'endpoint.  
  
 Questi filtri possono essere modificati utilizzando un comportamento.Nell'esempio, il servizio crea un'interfaccia <xref:System.ServiceModel.Description.IEndpointBehavior> che sostituisce le proprietà <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.AddressFilter%2A> e <xref:System.ServiceModel.Dispatcher.EndpointDispatcher.ContractFilter%2A> nella classe <xref:System.ServiceModel.Dispatcher.EndpointDispatcher>:  
  
```  
class FilteringEndpointBehavior : IEndpointBehavior …  
```  
  
 Vengono definiti due filtri per l'indirizzo:  
  
```  
// Matches any message whose To address contains the letter 'e'  
class MatchEAddressFilter : MessageFilter …  
// Matches any message whose To address does not contain the letter 'e'  
class MatchNoEAddressFilter : MessageFilter  
```  
  
 `FilteringEndpointBehavior` è reso configurabile e consente due variazioni diverse.  
  
```  
public class FilteringEndpointBehaviorExtension : BehaviorExtensionElement  
  
```  
  
 La variazione 1 corrisponde solo agli indirizzi che contengono una 'e' \(ma che sono dotati di qualsiasi azione\), mentre la variazione 2 corrisponde solo agli indirizzi a cui manca una 'e':  
  
```  
if (Variation == 1)  
    return new FilteringEndpointBehavior(  
        new MatchEAddressFilter(), new MatchAllMessageFilter());  
else  
    return new FilteringEndpointBehavior(  
        new MatchNoEAddressFilter(), new MatchAllMessageFilter());  
  
```  
  
 Il servizio registra il nuovo comportamento nel file di configurazione:  
  
```  
<extensions>  
    <behaviorExtensions>  
        <add name="filteringEndpointBehavior" type="Microsoft.ServiceModel.Samples.FilteringEndpointBehaviorExtension, service" />  
    </behaviorExtensions>  
</extensions>      
```  
  
 Il servizio quindi crea le configurazioni `endpointBehavior` per ogni variazione:  
  
```  
<endpointBehaviors>  
    <behavior name="endpoint1">  
        <filteringEndpointBehavior variation="1" />  
    </behavior>  
    <behavior name="endpoint2">  
        <filteringEndpointBehavior variation="2" />  
    </behavior>  
</endpointBehaviors>  
  
```  
  
 L'endpoint del servizio infine fa riferimento a uno degli elementi `behaviorConfigurations`:  
  
```  
<endpoint address=""  
        bindingConfiguration="ws"  
        listenUri=""   
        binding="wsHttpBinding"  
        contract="Microsoft.ServiceModel.Samples.IHello"   
        behaviorConfiguration="endpoint2" />  
  
```  
  
 L'implementazione dell'applicazione client è semplice: crea due canali sull'URI del servizio passando quel valore come il secondo parametro \(`via`\) su <xref:System.ServiceModel.Channels.IChannelFactory%601.CreateChannel%28System.ServiceModel.EndpointAddress%29> e invia un solo messaggio su ogni canale, utilizzando però indirizzi endpoint diversi per ognuno.Di conseguenza, i messaggi in uscita dal client hanno designazioni di destinazione diverse e il server risponde appropriatamente, come dimostrato dall'output del client:  
  
```  
Sending message to urn:e...  
Exception: The message with To 'urn:e' cannot be processed at the receiver, due to an AddressFilter mismatch at the EndpointDispatcher.  Check that the sender and receiver's EndpointAddresses agree.  
  
Sending message to urn:a...  
Hello  
```  
  
 La commutazione della variazione nel file di configurazione del server determina lo scambio del filtro e la visualizzazione da parte del client del comportamento contrario \(il messaggio a `urn:e` ha esito positivo, mentre il messaggio a `urn:a` ha esito negativo\).  
  
```  
<endpoint address=""  
          bindingConfiguration="ws"  
          listenUri=""   
          binding="wsHttpBinding"  
          contract="Microsoft.ServiceModel.Samples.IHello"   
          behaviorConfiguration="endpoint1" />  
  
```  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Extensibility\MessageFilter`  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Per compilare la soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
2.  Per eseguire l'esempio su un solo computer, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
3.  Per eseguire l'esempio tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md) e modificare la seguente riga in Client.cs.  
  
    ```  
    Uri serviceVia = new Uri("http://localhost/ServiceModelSamples/service.svc");  
    ```  
  
     Sostituire localhost con il nome del server.  
  
    ```  
    Uri serviceVia = new Uri("http://servermachinename/ServiceModelSamples/service.svc");  
    ```  
  
## Vedere anche