---
title: "Intestazioni di indirizzo | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b0c94d4a-3bde-4b4d-bb6d-9f12bc3a6940
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# Intestazioni di indirizzo
Nell'esempio delle intestazioni di indirizzo viene illustrato come i client possano passare parametri di riferimento a un servizio utilizzando [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine di questo argomento.  
  
 La specifica WS\-Addressing definisce la nozione di un riferimento dell'endpoint come un modo di indirizzare un particolare endpoint servizio Web.In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], i riferimenti all'endpoint vengono modellati utilizzando la classe `EndpointAddress`: `EndpointAddress` è il tipo del campo Indirizzo della classe `ServiceEndpoint`.  
  
 Parte del modello di riferimento all'endpoint è che ogni riferimento può portare alcuni parametri di riferimento che aggiungono informazioni di identificazione aggiuntive.In [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], questi parametri di riferimento vengono modellati come istanze della classe `AddressHeader`.  
  
 In questo esempio, il client aggiunge un parametro di riferimento a `EndpointAddress` dell'endpoint client.Il servizio cerca questo parametro di riferimento e ne utilizza il valore nella logica dell'operazione del servizio "Hello".  
  
## Client  
 Il client deve aggiungere un `AddressHeader` al `EndpointAddress` del `ServiceEndpoint` per inviare un parametro di riferimento.Poiché la classe `EndpointAddress` è immutabile, è necessario modificare l'indirizzo endpoint utilizzando la classe `EndpointAddressBuilder`.Nel codice seguente il client viene inizializzato per inviare un parametro di riferimento come parte del messaggio.  
  
```  
HelloClient client = new HelloClient();  
EndpointAddressBuilder builder =   
    new EndpointAddressBuilder(client.Endpoint.Address);  
AddressHeader header =   
    AddressHeader.CreateAddressHeader(IDName, IDNamespace, "John");  
builder.Headers.Add(header);  
client.Endpoint.Address = builder.ToEndpointAddress();  
```  
  
 Il codice crea un `EndpointAddressBuilder` utilizzando il `EndpointAddress` originale come valore iniziale.Viene quindi aggiunta una nuova intestazione di indirizzo. La chiamata a `CreateAddressHeadercreates` crea un'intestazione con un nome, uno spazio dei nomi e un valore particolari.In questo esempio il valore è "John."Una volta aggiunta l'intestazione al generatore, il metodo `ToEndpointAddress()` converte nuovamente il generatore \(mutevole\) in un indirizzo endpoint \(immutabile\), il quale viene assegnato di nuovo al campo Indirizzo dell'endpoint client.  
  
 Quando il client chiama `Console.WriteLine(client.Hello());`, il servizio è in grado di ottenere il valore di questo parametro di indirizzo, come si può vedere nell'output risultante del client.  
  
 `Hello, John`  
  
## Server  
 L'implementazione dell'operazione del servizio `Hello()` utilizza il `OperationContext` corrente per controllare i valori delle intestazioni nel messaggio in arrivo.  
  
```  
string id = null;  
// look at headers on incoming message  
for (int i = 0;   
     i < OperationContext.Current.IncomingMessageHeaders.Count;   
     ++i)  
{  
    MessageHeaderInfo h =   
        OperationContext.Current.IncomingMessageHeaders[i];  
    // for any reference parameters with the correct name & namespace  
    if (h.IsReferenceParameter &&   
        h.Name == IDName &&   
        h.Namespace == IDNamespace)  
    {  
        // read the value of that header  
        XmlReader xr =   
OperationContext.Current.IncomingMessageHeaders.GetReaderAtHeader(i);  
        id = xr.ReadElementContentAsString();  
    }  
}  
return "Hello, " + id;  
```  
  
 Il codice scorre tutte le intestazioni nel messaggio in arrivo, cercando intestazioni che sono parametri di riferimento dotati del nome particolare.Una volta individuato il parametro, il codice legge il valore del parametro e lo archivia nella variabile "id".  
  
#### Per impostare, compilare ed eseguire l'esempio  
  
1.  Assicurarsi di avere eseguito [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare l'edizione in C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Per eseguire l'esempio in una configurazione con un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Client\AddressHeaders`  
  
## Vedere anche