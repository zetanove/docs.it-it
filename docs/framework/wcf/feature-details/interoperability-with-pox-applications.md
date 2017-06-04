---
title: "Interoperabilit&#224; con applicazioni POX | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 449276b8-4633-46f0-85c9-81f01d127636
caps.latest.revision: 15
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 15
---
# Interoperabilit&#224; con applicazioni POX
Le applicazioni "Plain Old XML" \(POX\) comunicano scambiando messaggi HTTP non elaborati che contengono solo dati di applicazioni XML non inclusi all'interno di una SOAP envelope.[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] può fornire servizi e client che utilizzano messaggi POX.Nel servizio, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] può essere utilizzato per implementare servizi che espongono endpoint a client, ad esempio browser Web e linguaggi di script che inviano e ricevono messaggi POX.Nel client, il modello di programmazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] può essere utilizzato per implementare client che comunicano con servizi basati su POX.  
  
> [!NOTE]
>  Questo documento è stato scritto originariamente per [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 3.0.[!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] 3.5 dispone di supporto incorporato per l'utilizzo di applicazioni POX.[!INCLUDE[crabout](../../../../includes/crabout-md.md)] vedere [Modello di programmazione HTTP Web WCF](../../../../docs/framework/wcf/feature-details/wcf-web-http-programming-model.md)  
  
## Programmazione POX con WCF  
 I servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] che comunicano su HTTP tramite messaggi POX utilizzano un [\<customBinding\>](../../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md).  
  
```  
<customBinding>  
   <binding name="poxServerBinding">  
       <textMessageEncoding messageVersion="None" />  
       <httpTransport />  
   </binding>  
</customBinding>  
  
```  
  
 Questa associazione personalizzata contiene due elementi:  
  
-   [\<trasportoHttp\>](../../../../docs/framework/configure-apps/file-schema/wcf/httptransport.md) e  
  
-   [\<codificaMessaggiTesto\>](../../../../docs/framework/configure-apps/file-schema/wcf/textmessageencoding.md).  
  
 Il codificatore dei messaggi di testo [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] standard è configurato per l'utilizzo del valore <xref:System.ServiceModel.Channels.MessageVersion.None%2A> che consente di elaborare payload di messaggi XML che non arrivano incapsulati in una SOAP envelope.  
  
 I client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] che comunicano su HTTP tramite messaggi POX utilizzano un'associazione simile \(illustrata nel codice imperativo seguente\).  
  
```  
private static Binding CreatePoxBinding()  
{  
    TextMessageEncodingBindingElement encoder =   
    new TextMessageEncodingBindingElement( MessageVersion.None, Encoding.UTF8 );  
    HttpTransportBindingElement transport = new HttpTransportBindingElement();  
    transport.ManualAddressing = true;  
    return new CustomBinding( new BindingElement[] { encoder, transport } );  
}   
```  
  
 Poiché i client POX devono specificare in modo esplicito gli URI ai quali inviano messaggi, devono in genere configurare <xref:System.ServiceModel.Channels.HttpTransportBindingElement> come modalità di indirizzamento manuale impostando la proprietà <xref:System.ServiceModel.Channels.TransportBindingElement.ManualAddressing%2A> su `true` nell'elemento.Ciò consente ai messaggi di essere indirizzati in modo esplicito dal codice dell'applicazione e non sarà quindi necessario creare un nuovo <xref:System.ServiceModel.ChannelFactory> ogni volta che un'applicazione invia un messaggio a un URI HTTP diverso.  
  
 Poiché i messaggi POX non utilizzano intestazioni SOAP per trasmettere informazioni importanti sul protocollo, i client e i servizi POX spesso devono modificare parti della richiesta HTTP sottostante utilizzata per inviare o ricevere un messaggio.Le informazioni sul protocollo specifiche di HTTP, ad esempio le intestazioni e i codici di stato HTTP, nel modello di programmazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] assumono la forma di due classi:  
  
-   <xref:System.ServiceModel.Channels.HttpRequestMessageProperty> che contiene informazioni sulla richiesta HTTP, ad esempio le intestazioni di metodo e di richiesta HTTP.  
  
-   <xref:System.ServiceModel.Channels.HttpResponseMessageProperty> che contiene informazioni sulla risposta HTTP, ad esempio il codice di stato e la descrizione dello stato HTTP, come pure qualsiasi intestazione di risposta HTTP.  
  
 Nell'esempio di codice seguente viene illustrato come creare un messaggio di richiesta HTTP GET indirizzato a http:\/\/localhost:8100\/customers.  
  
```  
Message request = Message.CreateMessage( MessageVersion.None, String.Empty );  
request.Headers.To = “http://localhost:8100/customers”;  
  
HttpRequestMessageProperty property = new HttpRequestMessageProperty();  
property.Method = “GET”;  
property.SuppressEntityBody = true;  
request.Properties.Add( HttpRequestMessageProperty.Name, property );  
```  
  
 In primo luogo viene creata una richiesta vuota <xref:System.ServiceModel.Channels.Message> chiamando <xref:System.ServiceModel.Channels.Message.CreateMessage%28System.ServiceModel.Channels.MessageVersion%2CSystem.String%29>.Il parametro <xref:System.ServiceModel.Channels.MessageVersion.None%2A> viene utilizzato per indicare che non è necessaria una SOAP envelope e il parametro <xref:System.String.Empty> viene passato come Action.Il messaggio di richiesta viene quindi indirizzato impostando l'intestazione <xref:System.ServiceModel.Channels.MessageHeaders.To%2A> sull'URI desiderato.Viene quindi creato <xref:System.ServiceModel.Channels.HttpRequestMessageProperty> e <xref:System.ServiceModel.Channels.HttpRequestMessageProperty.Method%2A> viene impostato sul metodo del verbo HTTP GET e <xref:System.ServiceModel.Channels.HttpRequestMessageProperty.SuppressEntityBody%2A> viene impostato su `true` per indicare che nessun dato deve essere inviato nel corpo del messaggio di richiesta HTTP in uscita.Infine la proprietà della richiesta viene aggiunta alla raccolta <xref:System.ServiceModel.Channels.Message.Properties%2A> del messaggio di richiesta in modo da influire sull'invio della richiesta da parte del trasporto HTTP.Il messaggio è quindi pronto per essere inviato su un'istanza appropriata di <xref:System.ServiceModel.Channels.IRequestChannel>.  
  
 È possibile utilizzare tecniche simili nel servizio per estrarre <xref:System.ServiceModel.Channels.HttpRequestMessageProperty> da un messaggio in ingresso e creare una risposta.