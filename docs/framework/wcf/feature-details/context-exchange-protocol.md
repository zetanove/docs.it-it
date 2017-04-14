---
title: "Protocollo di scambio del contesto | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3dfd38e0-ae52-491c-94f4-7a862b9843d4
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Protocollo di scambio del contesto
In questa sezione viene illustrato il protocollo di scambio del contesto introdotto in [!INCLUDE[netfx35_long](../../../../includes/netfx35-long-md.md)] di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].Questo protocollo consente al canale client di accettare un contesto fornito da un servizio e di applicarlo a tutte le richieste successive a quel servizio inviate sulla stessa istanza del canale client.L'implementazione del protocollo di scambio del contesto può utilizzare uno dei due meccanismi seguenti per propagare il contesto tra il server e il client: cookie HTTP o un'intestazione SOAP.  
  
 Il protocollo di scambio del contesto viene implementato in un livello del canale personalizzato.Il canale comunica il contesto da e verso il livello dell'applicazione utilizzando una proprietà <xref:System.ServiceModel.Channels.ContextMessageProperty>.Per la trasmissione tra endpoint, il valore del contesto viene serializzato come intestazione SOAP a livello del canale oppure convertito in o da le proprietà del messaggio che rappresentano una richiesta e una risposta HTTP.Nel secondo caso, è previsto che uno dei livelli di canale sottostanti converta la richiesta HTTP e le proprietà del messaggio di risposta rispettivamente in e da cookie HTTP.Il meccanismo utilizzato per scambiare il contesto viene scelto utilizzando la proprietà <xref:System.ServiceModel.Channels.ContextExchangeMechanism> in <xref:System.ServiceModel.Channels.ContextBindingElement>.I valori validi sono `HttpCookie` e `SoapHeader`.  
  
 Sul client, un'istanza di un canale può operare in due modalità basate sulle impostazioni nella proprietà del canale, <xref:System.ServiceModel.Channels.IContextManager.Enabled%2A>.  
  
## Modalità 1: gestione del contesto del canale  
 Questa è la modalità predefinita, in cui <xref:System.ServiceModel.Channels.IContextManager.Enabled%2A> è impostato su `true`.In questa modalità il canale del contesto gestisce il contesto e lo memorizza nella cache per la sua durata.Il contesto può essere recuperato dal canale tramite la proprietà del canale `IContextManager` chiamando il metodo `GetContext`.Il canale può inoltre essere preinizializzato con un contesto specifico prima di venire aperto, chiamando il metodo `SetContext` sulla proprietà del canale.Dopo essere stato inizializzato con il contesto, il canale non può essere reimpostato.  
  
 Di seguito vengono elencate le invarianti in questa modalità:  
  
-   Qualsiasi tentativo di reimpostare il contesto utilizzando `SetContext` dopo che il canale è stato aperto genera una <xref:System.InvalidOperationException>.  
  
-   Qualsiasi tentativo di inviare il contesto utilizzando <xref:System.ServiceModel.Channels.ContextMessageProperty> in un messaggio in uscita genera una <xref:System.InvalidOperationException>.  
  
-   Se un messaggio viene ricevuto dal server con un contesto specifico, quando il canale è già stato inizializzato con un contesto specifico, viene generata una <xref:System.ServiceModel.ProtocolException>.  
  
    > [!NOTE]
    >  La ricezione di un contesto iniziale dal server è appropriata solo se il canale viene aperto senza alcun contesto impostato in modo esplicito.  
  
-   <xref:System.ServiceModel.Channels.ContextMessageProperty> su un messaggio in arrivo è sempre null.  
  
## Modalità 2: gestione del contesto dell'applicazione  
 Questa è la modalità quando <xref:System.ServiceModel.Channels.IContextManager.Enabled%2A> è impostato su `false`.In questa modalità il canale del contesto non gestisce il contesto.È di responsabilità dell'applicazione recuperare, gestire e applicare il contesto utilizzando <xref:System.ServiceModel.Channels.ContextMessageProperty>.Qualsiasi tentativo di chiamare `GetContext` o `SetContext` genera una <xref:System.InvalidOperationException>.  
  
 A prescindere dalla modalità scelta, la channel factory del client supporta i modelli di scambio dei messaggi <xref:System.ServiceModel.Channels.IRequestChannel>, <xref:System.ServiceModel.Channels.IRequestSessionChannel> e <xref:System.ServiceModel.Channels.IDuplexSessionChannel>.  
  
 Nel servizio, un'istanza del canale ha la responsabilità di convertire il contesto fornito dal client sui messaggi in arrivo a <xref:System.ServiceModel.Channels.ContextMessageProperty>.Il livello dell'applicazione o altri canali più in alto nello stack delle chiamate possono quindi accedere alla proprietà del messaggio.Il canale del servizio consente inoltre al livello dell'applicazione di specificare un nuovo valore del contesto da propagare indietro al client allegando una <xref:System.ServiceModel.Channels.ContextMessageProperty> al messaggio di risposta.Questa proprietà viene convertita nell'intestazione SOAP o nel cookie HTTP che contiene il contesto, in base alla configurazione dell'associazione.Il listener del canale del servizio supporta i modelli di scambio dei messaggi <xref:System.ServiceModel.Channels.IReplyChannel>, <xref:System.ServiceModel.Channels.IReplySessionChannel> e <xref:System.ServiceModel.Channels.IReplySessionChannel>.  
  
 Il protocollo di scambio del contesto introduce una nuova intestazione SOAP `wsc:Context` per rappresentare le informazioni del contesto quando i cookie HTTP non sono utilizzati per propagare il contesto.Lo schema dell'intestazione del contesto consente un numero qualsiasi di elementi figlio, ognuno con una chiave di stringa e un contenuto di stringa.Di seguito è riportato un esempio di intestazione del contesto.  
  
 `<Context xmlns="http://schemas.microsoft.com/ws/2006/05/context">`  
  
 `<property name="myContext">context-2</property>`  
  
 `</Context>`  
  
 In modalità `HttpCookie`, i cookie sono impostati utilizzando l'intestazione `SetCookie`.Il nome del cookie è `WscContext`.Il valore del cookie è la codifica Base64 dell'intestazione `wsc:Context`.Questo valore è racchiuso tra virgolette.  
  
 Il valore del contesto deve essere protetto dalle modifiche mentre è in transito, per la stessa ragione per cui sono protette le intestazioni WS\-Addressing. L'intestazione è utilizzata per determinare dove inviare la richiesta nel servizio.È pertanto necessario che l'intestazione `wsc:Context` sia firmata digitalmente o firmata e crittografata a livello SOAP o di trasporto quando l'associazione offre funzionalità di protezione dei messaggi.Quando i cookie HTTP sono utilizzati per propagare il contesto, devono essere protetti utilizzando sicurezza del trasporto.  
  
 Gli endpoint del servizio che richiedono il supporto per il protocollo di scambio del contesto possono renderlo esplicito nel criterio pubblicato.Per rappresentare il requisito che il client supporti il protocollo di scambio del contesto a livello di SOAP o abiliti il supporto di cookie HTTP, sono state introdotte due nuove asserzioni di criteri.La generazione di queste asserzioni all'interno del criterio nel servizio è controllata dal valore della proprietà <xref:System.ServiceModel.Channels.ContextBindingElement.ContextExchangeMechanism%2A> come segue:  
  
-   Per <xref:System.ServiceModel.Channels.ContextExchangeMechanism>, viene generata l'asserzione seguente:  
  
    ```  
    <IncludeContext   
    xmlns="http://schemas.microsoft.com/ws/2006/05/context"  
    protectionLevel="Sign" />  
    ```  
  
-   Per <xref:System.ServiceModel.Channels.ContextExchangeMechanism>, viene generata l'asserzione seguente:  
  
    ```  
    <HttpUseCookie xmlns="http://schemas.xmlsoap.org/soap/http"/>  
    ```  
  
## Vedere anche  
 [Guida di interoperabilità dei protocolli di servizi Web](../../../../docs/framework/wcf/feature-details/web-services-protocols-interoperability-guide.md)