---
title: "Servizi duplex | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 396b875a-d203-4ebe-a3a1-6a330d962e95
caps.latest.revision: 17
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 17
---
# Servizi duplex
Un contratto di servizio duplex è un modello di scambio di messaggi nel quale entrambi gli endpoint possono inviare messaggi l'uno all'altro in modo indipendente. Un servizio duplex, pertanto, può inviare messaggi all'endpoint client, fornendo un comportamento simile a quello degli eventi. Una comunicazione duplex ha luogo quando un client si connette a un servizio e fornisce a quest'ultimo un canale utilizzabile per inviare messaggi al client. Si noti che il comportamento simile a quello degli eventi di servizi duplex funziona solo all'interno di una sessione.  
  
 Per creare un contratto duplex è necessario creare una coppia di interfacce. La prima è l'interfaccia del contratto di servizio che descrive le operazioni che un client può richiamare. Contratto di servizio è necessario specificare un *contratto di callback* nel <xref:System.ServiceModel.ServiceContractAttribute.CallbackContract%2A?displayProperty=fullName> proprietà. Il contratto callback è l'interfaccia che definisce le operazioni che il servizio può chiamare sull'endpoint client. Un contratto duplex non richiede sessioni, sebbene le associazioni duplex fornite dal sistema le utilizzino.  
  
 Di seguito è riportato un esempio di contratto duplex.  
  
 [!code-csharp[c_DuplexServices#0](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_duplexservices/cs/service.cs#0)]
 [!code-vb[c_DuplexServices#0](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_duplexservices/vb/service.vb#0)]  
  
 La classe `CalculatorService` implementa l'interfaccia `ICalculatorDuplex` primaria. Il servizio utilizza il <xref:System.ServiceModel.InstanceContextMode> modalità dell'istanza per gestire il risultato per ogni sessione. Una proprietà privata denominata `Callback` accede al canale callback al client. Il servizio usa il callback per inviare i messaggi al client tramite l'interfaccia callback, come illustrato nel codice di esempio seguente.  
  
 [!code-csharp[c_DuplexServices#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_duplexservices/cs/service.cs#1)]
 [!code-vb[c_DuplexServices#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_duplexservices/vb/service.vb#1)]  
  
 Il client deve fornire una classe che implementi l'interfaccia callback del contratto duplex per ricevere messaggi dal servizio. Nel codice di esempio seguente viene illustrata una classe `CallbackHandler` che implementa l'interfaccia `ICalculatorDuplexCallback`.  
  
 [!code-csharp[c_DuplexServices#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_duplexservices/cs/client.cs#2)]
 [!code-vb[c_DuplexServices#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_duplexservices/vb/client.vb#2)]  
  
 Il [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] client generato per un contratto duplex richiede una <xref:System.ServiceModel.InstanceContext> classe devono essere fornite durante la costruzione. Questo <xref:System.ServiceModel.InstanceContext> classe viene usata come sito per un oggetto che implementa l'interfaccia di callback e gestisce i messaggi inviati dal servizio. Un <xref:System.ServiceModel.InstanceContext> viene costruita con un'istanza della classe di `CallbackHandler` (classe). Questo oggetto gestisce i messaggi inviati dal servizio al client sull'interfaccia di callback.  
  
 [!code-csharp[c_DuplexServices#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_duplexservices/cs/client.cs#3)]
 [!code-vb[c_DuplexServices#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_duplexservices/vb/client.vb#3)]  
  
 La configurazione per il servizio deve essere impostata in modo da fornire un'associazione che supporta sia la comunicazione della sessione che la comunicazione duplex. L'elemento `wsDualHttpBinding` supporta la comunicazione della sessione e consente la comunicazione duplex fornendo connessioni HTTP doppie, una per ogni direzione.  
  
 Sul client, è necessario configurare un indirizzo utilizzabile dal server per la connessione al client, come illustrato nella configurazione di esempio seguente.  
  
  
  
> [!NOTE]
>  I client non duplex che non riescono a eseguire l'autenticazione mediante conversazione protetta in genere generano un <xref:System.ServiceModel.Security.MessageSecurityException>. Tuttavia, se un client duplex che usa una conversazione protetta non riesce a eseguire l'autenticazione, il client riceve un <xref:System.TimeoutException> invece.  
  
 Quando si crea un client/servizio usando l'elemento `WSHttpBinding` e non si include l'endpoint di callback client, verrà restituito l'errore seguente.  
  
```  
HTTP could not register URL  
htp://+:80/Temporary_Listen_Addresses/<guid> because TCP port 80 is being used by another application.  
```  
  
 Nel codice di esempio seguente viene illustrato come specificare l'indirizzo endpoint client nel codice.  
  
```  
WSDualHttpBinding binding = new WSDualHttpBinding();  
EndpointAddress endptadr = new EndpointAddress("http://localhost:12000/DuplexTestUsingCode/Server");  
binding.ClientBaseAddress = new Uri("http://localhost:8000/DuplexTestUsingCode/Client/");  
```  
  
 Nel codice di esempio seguente viene illustrato come specificare l'indirizzo endpoint client nella configurazione.  
  
```  
<client>  
    <endpoint name ="ServerEndpoint"   
          address="http://localhost:12000/DuplexTestUsingConfig/Server"  
          bindingConfiguration="WSDualHttpBinding_IDuplexTest"   
            binding="wsDualHttpBinding"  
           contract="IDuplexTest" />  
</client>  
<bindings>  
    <wsDualHttpBinding>  
        <binding name="WSDualHttpBinding_IDuplexTest"    
          clientBaseAddress="http://localhost:8000/myClient/" >  
            <security mode="None"/>  
         </binding>  
    </wsDualHttpBinding>  
</bindings>  
  
```  
  
> [!WARNING]
>  Il modello duplex non consente di rilevare automaticamente il momento in cui un servizio o un client permette la chiusura del proprio canale. Pertanto, se un client viene terminato in modo imprevisto, per impostazione predefinita, non sarà inviata alcuna notifica al servizio. Client e servizi sono in grado di implementare il proprio protocollo per inviarsi vicendevolmente una notifica, se necessario.  
  
## <a name="see-also"></a>Vedere anche  
 [Duplex](../../../../docs/framework/wcf/samples/duplex.md)   
 [Specifica del comportamento in fase di esecuzione Client](../../../../docs/framework/wcf/specifying-client-run-time-behavior.md)   
 [Procedura: creare una Channel Factory e usarla per la creazione e gestione di canali](../../../../docs/framework/wcf/feature-details/how-to-create-a-channel-factory-and-use-it-to-create-and-manage-channels.md)