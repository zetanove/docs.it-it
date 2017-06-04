---
title: "Filtri avanzati | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 8d81590f-e036-4f96-824a-4a187f462764
caps.latest.revision: 23
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 23
---
# Filtri avanzati
Nell'esempio viene descritto un servizio di routing di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].Il servizio di routing è un componente di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] che semplifica l'aggiunta nell'applicazione di un router basato sul contenuto.L'esempio adatta l'esempio standard relativo alla calcolatrice di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] per comunicazioni tramite il servizio di routing.In questo esempio viene illustrato come definire la logica di routing basata sul contenuto tramite l'utilizzo di filtri messaggi e tabelle dei filtri messaggi.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\RoutingServices\AdvancedFilters`  
  
## Dettagli dell'esempio  
 Nella tabella seguente vengono mostrati i filtri messaggi aggiunti alla tabella dei filtri messaggi del servizio di routing.  
  
|Filtro|Regola|Priorità|  
|------------|------------|--------------|  
|If \(dispone di intestazione\)|Rounding|2|  
|If \(mostrato in Ep2\)|Regular|1|  
|If \(mostrato con Address2\)|Rounding|1|  
|If \(RoundRobin1\)|Regular|0|  
|If \(RoundRobin2\)|Rounding|0|  
  
 I filtri messaggi e le tabelle dei filtri messaggi possono essere creati e configurati tramite codice o nel file di configurazione dell'applicazione.Per questo esempio, è possibile trovare i filtri messaggi e le tabelle dei filtri messaggi definiti tramite codice nel file RoutingService\\routing.cs o definiti nel file di configurazione dell'applicazione nel file RoutingService\\App.config.Nei paragrafi seguenti viene descritta la creazione tramite codice di filtri messaggi e di tabelle dei filtri messaggi per questo esempio.  
  
 In primo luogo, <xref:System.ServiceModel.Dispatcher.XPathMessageFilter> effettua la ricerca dell'intestazione personalizzata.Si noti che <xref:System.ServiceModel.WSHttpBinding> determina una versione envelope che utilizza SOAP 1.2, pertanto l'istruzione XPath è definita per utilizzare lo spazio dei nomi di SOAP 1.2.Il gestore dello spazio dei nomi predefinito per <xref:System.ServiceModel.Dispatcher.XPathMessageFilter> definisce già un prefisso per lo spazio dei nomi di SOAP 1.2, \/s12, che è possibile utilizzare.Tuttavia, il gestore dello spazio dei nomi predefinito non dispone dello spazio dei nomi personalizzato utilizzato dal client per definire il valore dell'intestazione effettivo, pertanto il prefisso deve essere definito.Qualsiasi messaggio visualizzato con questa intestazione corrisponde al filtro.  
  
```  
XPathMessageContext namespaceManager = new XPathMessageContext();  
namespaceManager.AddNamespace("custom", "http://my.custom.namespace/");  
  
XPathMessageFilter xpathFilter = new XPathMessageFilter("/s12:Envelope/s12:Header/custom:RoundingCalculator = 1", namespaceManager);  
  
```  
  
 Il secondo filtro è un oggetto <xref:System.ServiceModel.Dispatcher.EndpointNameMessageFilter>, che corrisponde a qualsiasi messaggio ricevuto nell'oggetto `calculatorEndpoint`.Il nome dell'endpoint viene definito quando viene creato un oggetto endpoint del servizio.  
  
```  
EndpointNameMessageFilter endpointNameFilter = new EndpointNameMessageFilter("calculatorEndpoint");  
  
```  
  
 Il terzo filtro è un oggetto <xref:System.ServiceModel.Dispatcher.PrefixEndpointAddressMessageFilter>.Corrisponde a qualsiasi messaggio visualizzato in un endpoint con un indirizzo che corrisponde al prefisso dell'indirizzo fornito \(o alla prima parte di tale indirizzo\).In questo esempio il prefisso dell'indirizzo è definito come "http:\/\/localhost\/routingservice\/router\/rounding\/".Ciò significa che per qualsiasi messaggio in arrivo indirizzato a "http:\/\/localhost\/routingservice\/router\/rounding\/\*" viene individuata una corrispondenza da parte di tale filtro.In questo caso, si tratta di messaggi visualizzati nell'endpoint del servizio di calcolo che esegue l'arrotondamento e che dispone dell'indirizzo "http:\/\/localhost\/routingservice\/router\/rounding\/calculator".  
  
```  
PrefixEndpointAddressMessageFilter prefixAddressFilter = new PrefixEndpointAddressMessageFilter(new EndpointAddress("http://localhost/routingservice/router/rounding/"));  
  
```  
  
 Gli ultimi due filtri messaggi sono oggetti <xref:System.ServiceModel.Dispatcher.MessageFilter> personalizzati.In questo esempio, viene utilizzato un filtro messaggi "RoundRobin".Il filtro messaggi viene creato nel file RoutingService\\RoundRobinMessageFilter.cs fornito.Quando sono impostati sullo stesso gruppo, questi filtri alternano segnalazioni relative alla corrispondenza o meno con il messaggio, in modo tale che solo uno di essi alla volta restituisca `true`.  
  
```  
RoundRobinMessageFilter roundRobinFilter1 = new RoundRobinMessageFilter("group1");  
  
RoundRobinMessageFilter roundRobinFilter2 = new RoundRobinMessageFilter("group1");  
  
```  
  
 In seguito, tutti i messaggi in questione vengono aggiunti a un oggetto <xref:System.ServiceModel.Dispatcher.MessageFilterTable%601>.In questo modo, vengono specificate le priorità per influenzare l'ordine di esecuzione dei filtri nella tabella dei filtri messaggi.Maggiore è la priorità, prima viene eseguito il filtro; minore è la priorità, più tardi viene eseguito un filtro.Pertanto, un filtro con priorità 2 viene eseguito prima di un filtro con priorità 1.Se non viene specificato alcun livello di priorità, viene utilizzato quello predefinito, ovvero 0.Una tabella dei filtri messaggi esegue tutti i filtri a un determinato livello di priorità prima di passare al livello di priorità inferiore successivo.Se viene individuata una corrispondenza a un livello di priorità specifico, la tabella dei filtri messaggi interrompe la ricerca di corrispondenze per il livello di priorità inferiore successivo.  
  
> [!NOTE]
>  Sebbene in questo esempio venga illustrato come utilizzare le priorità dei filtri messaggi, in genere la scelta migliore e più efficace è progettare e configurare i filtri in modo che non richiedano la definizione di priorità per funzionare correttamente.  
  
 Il primo filtro da aggiungere è il filtro XPath e la priorità viene impostata su 2.Si tratta del primo filtro messaggi in esecuzione.Se tale filtro individua l'intestazione personalizzata, a prescindere dai risultati degli altri filtri, il messaggio viene indirizzato all'endpoint del servizio di calcolo che esegue l'arrotondamento.  
  
 Al livello di priorità 1, vengono aggiunti due filtri.Anche in questo caso, tali filtri vengono eseguiti solo se il filtro XPath con priorità 2 non corrisponde al messaggio.Questi due filtri mostrano due diverse modalità per determinare dove è stato indirizzato il messaggio al momento della visualizzazione.Poiché i due filtri verificano di fatto se il messaggio è arrivato a uno dei due endpoint, possono essere eseguiti allo stesso livello di priorità, dal momento che non restituiscono entrambi `true` contemporaneamente.  
  
 Infine, al livello di priorità 0 \(la priorità minima\) vengono eseguiti i filtri messaggi RoundRobin.Poiché i filtri vengono configurati con lo stesso nome del gruppo, solo uno di essi alla volta individua una corrispondenza.Dal momento che tutti i messaggi con l'intestazione personalizzata sono stati indirizzati a specifici endpoint virtualizzati, i messaggi gestiti dai filtri messaggi RoundRobin sono gli unici messaggi indirizzati all'endpoint del router predefinito senza l'intestazione personalizzata.Poiché tali messaggi attivano un messaggio per ogni chiamata, metà delle operazioni viene indirizzata all'endpoint del servizio di calcolatrice normale e l'altra metà all'endpoint del servizio di calcolatrice che esegue l'arrotondamento.  
  
#### Per utilizzare questo esempio  
  
1.  Utilizzando [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)], aprire AdvancedFilters.sln.  
  
2.  Per aprire **Esplora soluzioni**, scegliere **Esplora soluzioni** dal menu **Visualizza**.  
  
3.  Premere F5 o CTRL\+MAIUSC\+B in [!INCLUDE[vs_current_short](../../../../includes/vs-current-short-md.md)].  
  
    1.  Se si desidera che i progetti necessari vengano avviati automaticamente quando si preme F5, fare clic con il pulsante destro del mouse sulla soluzione e scegliere **Proprietà**.Selezionare il nodo **Progetto di avvio** in **Proprietà comuni** nel riquadro sinistro.Selezionare il pulsante di opzione **Progetti di avvio multipli** e impostare tutti i progetti in modo che dispongano dell'azione **Avvia**.  
  
    2.  Se si compila il progetto con CTRL\+MAIUSC\+B, sarà necessario avviare le applicazioni seguenti:  
  
        1.  Client calcolatrice \(.\/CalculatorClient\/bin\/client.exe\)  
  
        2.  Servizio di calcolatrice \(.\/CalculatorService\/bin\/service.exe\)  
  
        3.  Servizio di routing relativo alla calcolatrice \(.\/RoundingCalcService\/bin\/service.exe\)  
  
        4.  RoutingService \(.\/RoutingService\/bin\/RoutingService.exe\)  
  
4.  Nella finestra console del client calcolatrice premere INVIO per avviare il client.Il client restituisce un elenco di endpoint di destinazione da selezionare.  
  
5.  Scegliere un endpoint di destinazione digitando la lettera corrispondente, quindi premere INVIO.  
  
6.  In seguito, il client chiede se si desidera aggiungere un'intestazione personalizzata.Premere Y per Sì o N per No, quindi premere INVIO.  
  
7.  In base alle selezioni effettuate, verranno visualizzati output diversi.  
  
    1.  Quello riportato di seguito è l'output restituito se è stata aggiunta un'intestazione personalizzata ai messaggi.  
  
        ```Output  
        Add(100,15.99) = 116  
        Subtract(145,76.54) = 68.5  
        Multiply(9,81.25) = 731.3  
        Divide(22,7) = 3.1  
  
        ```  
  
    2.  Quello riportato di seguito è l'output restituito se è stato selezionato l'endpoint del servizio di calcolatrice che esegue l'arrotondamento senza un'intestazione personalizzata.  
  
        ```Output  
        Add(100,15.99) = 116  
        Subtract(145,76.54) = 68.5  
        Multiply(9,81.25) = 731.3  
        Divide(22,7) = 3.1  
  
        ```  
  
    3.  Quello riportato di seguito è l'output restituito se è stato selezionato l'endpoint del servizio di calcolatrice normale senza un'intestazione personalizzata.  
  
        ```Output  
        Add(100,15.99) = 115.99  
        Subtract(145,76.54) = 68.46  
        Multiply(9,81.25) = 731.25  
        Divide(22,7) = 3.14285714285714  
  
        ```  
  
    4.  Quello riportato di seguito è l'output restituito se è stato selezionato l'endpoint del router predefinito senza un'intestazione personalizzata.  
  
        ```Output  
        Add(100,15.99) = 116  
        Subtract(145,76.54) = 68.46  
        Multiply(9,81.25) = 731.3  
        Divide(22,7) = 3.14285714285714  
  
        ```  
  
8.  Il servizio di calcolatrice e il servizio di calcolo che esegue l'arrotondamento stampano inoltre un log delle operazioni richiamate nelle rispettive finestre della console.  
  
9. Nella finestra console del client digitare `quit` e premere INVIO per uscire.  
  
10. Premere INVIO nelle finestre della console dei servizi per terminare i servizi.  
  
## Configurabile tramite codice o App.config  
 L'esempio proposto è configurato per l'utilizzo di un file App.config per definire il comportamento del router.È inoltre possibile modificare il nome del file RoutingService\\App.config affinché non venga riconosciuto e rimuovere i commenti dalla chiamata al metodo `ConfigureRouterViaCode()` in RoutingService\\routing.cs.Entrambi i metodi restituiscono lo stesso comportamento da parte del router.  
  
### Scenario  
 In questo esempio, il router agisce come router basato sul contenuto che consente a più tipi o implementazioni di servizi di essere esposti mediante un endpoint.  
  
### Scenario reale  
 Contoso desidera virtualizzare i propri servizi per esporre pubblicamente solo un endpoint tramite il quale viene offerto l'accesso a più tipi diversi di servizi.In questo caso, le funzionalità di routing basate sul contenuto del servizio di routing vengono utilizzate per determinare dove devono essere inviate le richieste in entrata.  
  
## Vedere anche  
 [Hosting e salvataggio permanente](http://go.microsoft.com/fwlink/?LinkId=193961)