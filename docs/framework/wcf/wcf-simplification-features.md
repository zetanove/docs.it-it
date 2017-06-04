---
title: "Funzionalit&#224; di semplificazione WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4535a511-6064-4da0-b361-80262a891663
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Funzionalit&#224; di semplificazione WCF
In questo argomento vengono descritte le nuove funzionalità che rendono più semplice la scrittura di applicazioni WCF.  
  
## File di configurazione generati semplificati  
 Quando si aggiunge un riferimento al servizio in Visual Studio o si utilizza lo strumento SvcUtil.exe, viene generato un file di configurazione client.Nelle versioni precedenti di WCF, questi file di configurazione contenevano il valore di ogni proprietà di associazione anche se il relativo valore è quello predefinito.In WCF 4.5 i file di configurazione generati contengono soltanto le proprietà di associazione che sono impostate su un valore non predefinito.  
  
 Di seguito è riportato un esempio di un file di configurazione generato da WCF 3.0.  
  
```  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
    <system.serviceModel>  
        <bindings>  
            <basicHttpBinding>  
                <binding name="BasicHttpBinding_IService1" closeTimeout="00:01:00"  
                    openTimeout="00:01:00" receiveTimeout="00:10:00" sendTimeout="00:01:00"  
                    allowCookies="false" bypassProxyOnLocal="false"   
                    hostNameComparisonMode="StrongWildcard" maxBufferSize="65536"   
                    maxBufferPoolSize="524288" maxReceivedMessageSize="65536"  
                    messageEncoding="Text" textEncoding="utf-8" transferMode="Buffered"  
                    useDefaultWebProxy="true">  
                    <readerQuotas maxDepth="32" maxStringContentLength="8192"   
                        maxArrayLength="16384" maxBytesPerRead="4096"  
                        maxNameTableCharCount="16384" />  
                    <security mode="None">  
                        <transport clientCredentialType="None" proxyCredentialType="None"  
                            realm="" />  
                        <message clientCredentialType="UserName" algorithmSuite="Default" />  
                    </security>  
                </binding>  
            </basicHttpBinding>  
        </bindings>  
        <client>  
            <endpoint address="http://localhost:36906/Service1.svc" binding="basicHttpBinding"  
                bindingConfiguration="BasicHttpBinding_IService1" contract="IService1"  
                name="BasicHttpBinding_IService1" />  
        </client>  
    </system.serviceModel>  
</configuration>  
  
```  
  
 Di seguito è riportato un esempio dello stesso file di configurazione generato da WCF 4.5.  
  
```  
  
<?xml version="1.0" encoding="utf-8"?>  
<configuration>  
    <system.serviceModel>  
        <bindings>  
            <basicHttpBinding>  
                <binding name="BasicHttpBinding_IService1" />  
            </basicHttpBinding>  
        </bindings>  
        <client>  
            <endpoint address="http://localhost:36906/Service1.svc" binding="basicHttpBinding"  
                bindingConfiguration="BasicHttpBinding_IService1" contract="IService1"  
                name="BasicHttpBinding_IService1" />  
        </client>  
    </system.serviceModel>  
</configuration>  
  
```  
  
## Sviluppo con priorità al contratto \("contract\-first"\)  
 WCF supporta ora lo sviluppo con priorità al contratto \("contract\-first"\).Lo strumento svcutl.exe dispone di un'opzione \/serviceContract che consente di generare contratti di servizio e dati da un documento WSDL.  
  
## Aggiungere un riferimento al servizio da un progetto di subset portabili  
 I progetti di subset portabili consentono ai programmatori di assembly .NET di gestire un unico albero di origine e di compilare il sistema supportando allo stesso tempo più piattaforme .NET \(desktop, Silverlight, Windows Phone e XBOX\).I progetti di subset portabili fanno riferimento solo alle librerie portabili .NET che rappresentano un assembly .NET Framework che può essere utilizzato in qualsiasi piattaforma .NET principale.L'esperienza dello sviluppatore equivale all'aggiunta di un riferimento al servizio all'interno di qualsiasi altra applicazione client WCF.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)][Aggiungere un riferimento al servizio in un progetto di subset portabili](../../../docs/framework/wcf/add-service-reference-in-a-portable-subset-project.md).  
  
## Modifica dell'impostazione predefinita della modalità di compatibilità ASP.NET  
 WCF fornisce la modalità di compatibilità ASP.NET per garantire agli sviluppatori l'accesso completo alle funzionalità nella pipeline HTTP ASP.NET in caso di scrittura di servizi WCF.Per utilizzare questa modalità, è necessario impostare l'attributo `aspNetCompatibilityEnabled` su True nella sezione [\<serviceHostingEnvironment\>](../../../docs/framework/configure-apps/file-schema/wcf/servicehostingenvironment.md) di web.config.Inoltre, la proprietà `RequirementsMode` dell'oggetto <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsAttribute> di qualsiasi servizio in questo appDomain deve essere impostata sul campo <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode> o <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode>.Per impostazione predefinita, l'oggetto <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsAttribute> è ora impostato sul campo <xref:System.ServiceModel.Activation.AspNetCompatibilityRequirementsMode> e il modello predefinito dell'applicazione del servizio WCF imposta l'attributo `aspNetCompatibilityEnabled` su `true`.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)][Novità in Windows Communication Foundation 4.5](../../../docs/framework/wcf/whats-new.md) e [Servizi WCF e ASP.NET](../../../docs/framework/wcf/feature-details/wcf-services-and-aspnet.md).  
  
## Miglioramenti del flusso  
  
-   In WCF è stato aggiunto un nuovo supporto per il flusso asincrono.Per abilitare il flusso asincrono, aggiungere il comportamento dell'endpoint <xref:System.ServiceModel.Description.DispatcherSynchronizationBehavior> all'host del servizio e impostare la relativa proprietà <xref:System.ServiceModel.Description.DispatcherSynchronizationBehavior.AsynchronousSendEnabled%2A> su `true`.Questa operazione può migliorare la scalabilità quando un servizio sta inviando messaggi trasmessi a più client che leggono lentamente.WCF non blocca più un thread per client e libererà il thread per soddisfare un altro client.  
  
-   Eliminazione delle limitazioni relativamente al buffer dei messaggi quando un servizio è ospitato da IIS.Nelle versioni precedenti di WCF, quando si riceveva un messaggio per un servizio ospitato da IIS che utilizzava il trasferimento dei messaggi di flusso, ASP.NET avrebbe memorizzato nel buffer l'intero messaggio prima di inviarlo a WCF.Questa condizione comportava un elevato consumo di memoria.Questo buffering è stato rimosso in .NET 4.5 e ora i servizi WCF ospitati da IIS possono iniziare l'elaborazione del flusso in ingresso prima che l'intero messaggio sia stato ricevuto, permettendo quindi un flusso vero.In questo modo, WCF risponde immediatamente ai messaggi e consente prestazioni migliori.Inoltre, non è più necessario specificare un valore per `maxRequestLength`, cioè il limite di dimensioni ASP.NET per le richieste in ingresso.Se questa proprietà è impostata, verrà ignorata.[!INCLUDE[crabout](../../../includes/crabout-md.md)]`maxRequestLength`, vedere la pagina relativa all'[elemento di configurazione \<httpRuntime\>](http://go.microsoft.com/fwlink/?LinkId=223344).Sarà comunque ancora necessario configurare maxAllowedContentLength. [!INCLUDE[crdefault](../../../includes/crdefault-md.md)] la pagina relativa ai [limiti delle richieste di IIS](http://go.microsoft.com/fwlink/?LinkId=225908).  
  
## Nuovi valori predefiniti di trasporto  
 Nella tabella seguente vengono descritte le impostazioni che sono state modificate e dove reperire informazioni aggiuntive.  
  
|Proprietà|Su|Nuova impostazione predefinita|Ulteriori informazioni|  
|---------------|--------|------------------------------------|----------------------------|  
|channelInitializationTimeout|<xref:System.ServiceModel.NetTcpBinding>|30 secondi|Questa proprietà determina il possibile tempo necessario per l'autenticazione di una connessione TCP utilizzando il protocollo .Net Framing.Un client deve inviare alcuni dati iniziali prima che il server disponga di informazioni sufficienti per effettuare l'autenticazione.Questo timeout viene reso intenzionalmente più piccolo rispetto a ReceiveTimeout \(10 min\) in modo che eventuali client non autenticati dannosi non possano mantenere le connessioni al server per molto tempo.Il valore predefinito è 30 secondi.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)]<xref:System.ServiceModel.Channels.ConnectionOrientedTransportBindingElement.ChannelInitializationTimeout%2A>|  
|listenBacklog|<xref:System.ServiceModel.NetTcpBinding>|16 \* il numero di processori|È la proprietà a livello di socket che descrive il numero di richieste "in attesa di accettazione" da mettere in coda.Se la coda del backlog in ascolto si riempie, le nuove richieste del socket verranno rifiutate.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)]<xref:System.ServiceModel.NetTcpBinding.ListenBacklog%2A>|  
|maxPendingAccepts|ConnectionOrientedTransportBindingElement<br /><br /> SMSvcHost.exe|2 \* il numero di processori per trasporto<br /><br /> 4 \* il numero di processori per SMSvcHost.exe|Questa proprietà limita il numero di canali che il server può avere in attesa su un listener.Se i dati MaxPendingAccepts sono troppo bassi, si verificherà un piccolo intervallo di tempo in cui tutti canali in attesa hanno avviato connessioni di servizio, ma nessun nuovo canale ha iniziato l'ascolto.Durante questo intervallo può verificarsi una connessione che non riuscirà perché nulla è in sua attesa sul server.Questa proprietà può essere configurata impostando la proprietà <xref:System.ServiceModel.Channels.ConnectionOrientedTransportBindingElement.MaxPendingConnections%2A> su un numero più grande.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)].<xref:System.ServiceModel.Channels.ConnectionOrientedTransportBindingElement.MaxPendingAccepts%2A> e [Configuring the Net.TCP Port Sharing Service](http://msdn.microsoft.com/it-it/b6dd81fa-68b7-4e1b-868e-88e5901b7ea0)|  
|maxPendingConnections|ConnectionOrientedTransportBindingElement|12 \* il numero di processori|Questa proprietà controlla il numero di connessioni che sono state accettate da un trasporto, ma non prelevate dal dispatcher ServiceModel.Per impostare questo valore, utilizzare `MaxConnections` nell'associazione o `maxOutboundConnectionsPerEndpoint` nell'elemento di associazione.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)]<xref:System.ServiceModel.Channels.ConnectionOrientedTransportBindingElement.MaxPendingConnections%2A>|  
|receiveTimeout|SMSvcHost.exe|30 secondi|Questa proprietà specifica il timeout per la lettura dei dati sui frame TCP e per l'esecuzione dell'invio della connessione dalle connessioni sottostanti.Questa proprietà è utile per applicare un limite al tempo in cui il servizio SMSvcHost.exe viene utilizzato per leggere i dati del preambolo da una connessione in ingresso.[!INCLUDE[crdefault](../../../includes/crdefault-md.md)][Configuring the Net.TCP Port Sharing Service](http://msdn.microsoft.com/it-it/b6dd81fa-68b7-4e1b-868e-88e5901b7ea0).|  
  
> [!NOTE]
>  Le nuove impostazioni predefinite vengono utilizzate solo se si distribuisce il servizio WCF in un computer con .NET Framework 4.5.Se si distribuisce lo stesso servizio in un computer con .NET Framework 4.0, vengono utilizzati i valori predefiniti di .NET Framework 4.0.In questi casi è consigliabile configurare queste impostazioni in modo esplicito.  
  
## XmlDictionaryReaderQuotas  
 L'oggetto <xref:System.Xml.XmlDictionaryReaderQuotas> contiene i valori di quota configurabili per lettori di dizionari XML che limitano la quantità di memoria utilizzata da un codificatore durante la creazione di un messaggio.Anche se queste quote sono configurabili, i valori predefiniti sono stati modificati per ridurre la possibilità che uno sviluppatore debba impostarle in modo esplicito.La quota `MaxReceivedMessageSize` non è stata modificata, pertanto può ancora limitare il consumo di memoria evitando all'utente di dover gestire la complessità dell'oggetto <xref:System.Xml.XmlDictionaryReaderQuotas>.Nella tabella seguente sono illustrate le quote, i relativi nuovi valori predefiniti e una breve descrizione dell'utilizzo di ciascuna quota.  
  
|Nome della quota|Valore predefinito|Descrizione|  
|----------------------|------------------------|-----------------|  
|<xref:System.Xml.XmlDictionaryReaderQuotas.MaxArrayLength%2A>|Int32.MaxValue|Ottiene e imposta la lunghezza massima consentita della matrice.Questa quota limita la dimensione massima di una matrice di primitive che viene restituita dal lettore XML, incluse matrici di byte.La quota non limita l'utilizzo di memoria nel lettore XML stesso, bensì in un qualsiasi componente che utilizza il lettore.Ad esempio, quando la classe <xref:System.Runtime.Serialization.DataContractSerializer> utilizza un lettore protetto con <xref:System.Xml.XmlDictionaryReaderQuotas.MaxArrayLength%2A>, non deserializza matrici di byte che superano questa quota.|  
|<xref:System.Xml.XmlDictionaryReaderQuotas.MaxBytesPerRead%2A>|Int32.MaxValue|Ottiene e imposta i byte massimi consentiti restituiti per ogni lettura.Questa quota limita il numero di byte letti in una sola operazione di lettura, durante la lettura del tag iniziale dell'elemento e dei relativi attributi.In casi in cui non viene utilizzato il flusso, il nome dell'elemento stesso non viene contato ai fini della quota.La presenza di troppi attributi XML può causare un prolungamento eccessivo dei tempi di elaborazione perché è necessario controllare che i nomi degli attributi siano univoci.Utilizzando la proprietà <xref:System.Xml.XmlDictionaryReaderQuotas.MaxBytesPerRead%2A> la minaccia viene mitigata.|  
|<xref:System.Xml.XmlDictionaryReaderQuotas.MaxDepth%2A>|128 nodi di profondità|Questa quota limita la profondità massima di annidamento degli elementi XML.<xref:System.Xml.XmlDictionaryReaderQuotas.MaxDepth%2A> interagisce con <xref:System.Xml.XmlDictionaryReaderQuotas.MaxBytesPerRead%2A>: il lettore mantiene sempre i dati in memoria per l'elemento corrente e tutti i suoi predecessori, pertanto l'utilizzo massimo di memoria da parte del lettore è proporzionale al prodotto di queste due impostazioni.Quando un oggetto grafico profondamente annidato viene deserializzato, il deserializzatore deve utilizzare l'intero stack e generare un'eccezione <xref:System.StackOverflowException> irreversibile.Esiste una correlazione diretta tra l'annidamento XML e l'annidamento di oggetti sia per la classe<xref:System.Runtime.Serialization.DataContractSerializer> sia per la classe <xref:System.Runtime.Serialization.XmlSerializer>.La proprietà <xref:System.Xml.XmlDictionaryReaderQuotas.MaxDepth%2A> viene utilizzata per mitigare questa minaccia.|  
|<xref:System.Xml.XmlDictionaryReaderQuotas.MaxNameTableCharCount%2A>|Int32.MaxValue|Questa quota limita il numero massimo di caratteri consentiti in una tabella dei nomi.La tabella NameTable contiene alcune stringhe \(ad esempio spazi dei nomi e prefissi\) incontrate durante l'elaborazione di un documento XML.Poiché tali stringhe vengono memorizzate nel buffer, questa quota viene utilizzata per impedire la memorizzazione di un'eccessiva quantità di dati nel buffer quando si prevede un flusso.|  
|<xref:System.Xml.XmlDictionaryReaderQuotas.MaxStringContentLength%2A>|Int32.MaxValue|Questa quota limita la dimensione massima della stringa restituita dal lettore XMLe non l'utilizzo di memoria nel lettore XML stesso, bensì nel componente che utilizza il lettore.Ad esempio, quando la classe <xref:System.Runtime.Serialization.DataContractSerializer> utilizza un lettore protetto con <xref:System.Xml.XmlDictionaryReaderQuotas.MaxStringContentLength%2A>, non deserializza stringhe che superano questa quota.|  
  
> [!IMPORTANT]
>  Fare riferimento a "Utilizzo sicuro di XML" in [Considerazioni sulla protezione per i dati](../../../docs/framework/wcf/feature-details/security-considerations-for-data.md) per ulteriori informazioni sulla sicurezza dei dati.  
  
> [!NOTE]
>  Le nuove impostazioni predefinite vengono utilizzate solo se si distribuisce il servizio WCF in un computer con .NET Framework 4.5.Se si distribuisce lo stesso servizio in un computer con .NET Framework 4.0, vengono utilizzati i valori predefiniti di .NET Framework 4.0.In questi casi è consigliabile configurare queste impostazioni in modo esplicito.  
  
## Convalida della configurazione WCF  
 Il processo di compilazione in Visual Studio include ora la convalida dei file di configurazione WCF.Se la convalida non riesce, in Visual Studio viene visualizzato un elenco di errori o avvisi di convalida.  
  
## Descrizioni comandi dell'editor XML  
 Per consentire agli sviluppatori di servizi WCF nuovi ed esistenti di configurare i propri servizi, l'editor XML di Visual Studio offre ora le descrizioni comandi per ogni elemento di configurazione e le relative proprietà che fanno parte del file di configurazione del servizio.  
  
## Miglioramenti di BasicHttpBinding  
  
1.  Consente a un singolo endpoint WCF di rispondere a diverse modalità di autenticazione.  
  
2.  Consente il controllo delle impostazioni di sicurezza di un servizio WCF da parte di IIS