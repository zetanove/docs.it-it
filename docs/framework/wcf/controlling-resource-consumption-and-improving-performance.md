---
title: "Controllo dell&#39;utilizzo di risorse e miglioramento delle prestazioni | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9a829669-5f76-4c88-80ec-92d0c62c0660
caps.latest.revision: 18
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 18
---
# Controllo dell&#39;utilizzo di risorse e miglioramento delle prestazioni
In questo argomento vengono descritte varie proprietà in aree diverse dell'architettura di [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] che controllano l'utilizzo di risorse e incidono sulla misurazione delle prestazioni.  
  
## Proprietà che limitano l'utilizzo di risorse in WCF  
 In [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] vengono applicati vincoli ad alcuni tipi di processi a scopo di sicurezza o di tutela delle prestazioni.I vincoli si presentano in due forme principali: quote e velocità.Le *quote* sono limiti che, una volta raggiunti o superati, generano un'eccezione immediata in un punto determinato nel sistema.Le *velocità* sono limiti che non determinano la generazione immediata di un'eccezione.Quando viene raggiunto un limite di velocità, invece, l'elaborazione continua rimanendo nei limiti impostati dal valore della velocità.Questa elaborazione limitata potrebbe generare un'eccezione in un altro punto, ma questo dipende dall'applicazione.  
  
 Oltre alla distinzione tra quote e velocità, alcune proprietà di limitazione si trovano al livello della serializzazione, alcune al livello del trasporto e alcune al livello dell'applicazione.La proprietà <xref:System.ServiceModel.Channels.TransportBindingElement.MaxReceivedMessageSize%2A?displayProperty=fullName> della quota, ad esempio, implementata da tutti gli elementi dell'associazione del trasporto forniti dal sistema, è pari a 65.536 byte per impostazione predefinita per impedire a client dannosi di effettuare attacchi Denial of Service contro un servizio provocando un consumo di memoria eccessivo.È in genere possibile migliorare le prestazioni abbassando questo valore.  
  
 Un esempio di quota di serializzazione è la proprietà <xref:System.Runtime.Serialization.DataContractSerializer.MaxItemsInObjectGraph%2A?displayProperty=fullName>, che specifica il numero massimo di oggetti serializzati o deserializzati dal serializzatore in una sola chiamata al metodo <xref:System.Runtime.Serialization.DataContractSerializer.ReadObject%2A>.Un esempio di limite a livello di applicazione è la proprietà <xref:System.ServiceModel.Dispatcher.ServiceThrottle.MaxConcurrentSessions%2A?displayProperty=fullName> che per impostazione predefinita limita a 10 il numero di connessioni simultanee del canale con sessione.A differenza delle quote, se viene raggiunto questo valore limite, l'applicazione continua l'elaborazione ma non accetta nuovi canali con sessione. Non è quindi possibile connettere nuovi client fino a quando uno degli altri canali con sessione non è stato terminato.  
  
 Questi controlli sono stati progettati per fornire una mitigazione automatica di alcuni tipi di attacchi o per migliorare la misurazione delle prestazioni, ad esempio footprint di memoria, ora di avvio e così via.A seconda dell'applicazione, tuttavia, questi controlli possono limitare le prestazioni dell'applicazione di servizio o ostacolare del tutto il funzionamento dell'applicazione.Un'applicazione progettata per trasmettere video, ad esempio, può facilmente superare il valore della proprietà <xref:System.ServiceModel.Channels.TransportBindingElement.MaxReceivedMessageSize%2A?displayProperty=fullName>.In questo argomento viene fornita una panoramica dei vari controlli applicati alle applicazioni a tutti i livelli di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], viene descritto come ottenere più informazioni sul possibile ostacolo rappresentato da un'impostazione per l'applicazione e vengono descritte le modalità di risoluzione dei vari problemi.Molte velocità e alcune quote sono disponibili a livello di applicazione, anche quando la proprietà di base è un limite per la serializzazione o il trasporto.È ad esempio possibile impostare la proprietà <xref:System.Runtime.Serialization.DataContractSerializer.MaxItemsInObjectGraph%2A?displayProperty=fullName> utilizzando la proprietà <xref:System.ServiceModel.ServiceBehaviorAttribute.MaxItemsInObjectGraph%2A?displayProperty=fullName> nella classe del servizio.  
  
> [!NOTE]
>  Per problemi particolari, è consigliabile leggere prima l'argomento [Guida rapida alla risoluzione dei problemi di WCF](../../../docs/framework/wcf/wcf-troubleshooting-quickstart.md) per verificare se il problema \(e una soluzione\) è citato.  
  
 Le proprietà che limitano i processi di serializzazione sono elencate in [Considerazioni sulla protezione per i dati](../../../docs/framework/wcf/feature-details/security-considerations-for-data.md).Le proprietà che limitano l'utilizzo di risorse relativamente ai trasporti sono elencate in [Quote dei trasporti](../../../docs/framework/wcf/feature-details/transport-quotas.md).Le proprietà che limitano l'utilizzo di risorse a livello di applicazione sono membri della classe <xref:System.ServiceModel.Dispatcher.ServiceThrottle>.  
  
## Rilevazione di problemi in applicazioni e prestazioni relativi alle impostazioni delle quote  
 Le impostazioni predefinite dei valori precedenti sono state scelte per abilitare le funzionalità di base dell'applicazione in un'ampia gamma di tipi di applicazioni pur fornendo una protezione di base nei confronti di problemi di sicurezza comuni.Concezioni diverse delle applicazioni possono, tuttavia, superare una o più impostazioni della velocità sebbene l'applicazione sia per altri versi protetta e il suo funzionamento sia quello previsto.In questi casi è necessario identificare il valore di velocità superato e il livello al quale si è verificato il superamento e decidere l'intervento appropriato per aumentare la velocità effettiva dell'applicazione.  
  
 In genere, durante la scrittura dell'applicazione e l'esecuzione del debug, la proprietà <xref:System.ServiceModel.Description.ServiceDebugBehavior.IncludeExceptionDetailInFaults%2A?displayProperty=fullName> viene impostata su `true` nel file di configurazione o a livello di programmazione.In tal modo viene indicato a [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] di restituire tracce dello stack di eccezioni del servizio all'applicazione client perché vengano visualizzate.Questa funzionalità consente di segnalare la maggior parte delle eccezioni a livello di applicazione in modo da visualizzare le impostazioni delle quote interessate, se questo è il problema.  
  
 Alcune eccezioni si verificano in fase di esecuzione e non sono visibili al livello dell'applicazione, quindi non vengono restituite con questo meccanismo e potrebbero non essere gestite da un'implementazione <xref:System.ServiceModel.Dispatcher.IErrorHandler?displayProperty=fullName> personalizzata.In un ambiente di sviluppo quale Microsoft Visual Studio la maggior parte di queste eccezioni viene visualizzata automaticamente.Alcune eccezioni, tuttavia, possono essere mascherate da impostazioni dell'ambiente di sviluppo, ad esempio le impostazioni [Just My code](http://go.microsoft.com/fwlink/?LinkId=82174) in Visual Studio 2005.  
  
 Indipendentemente dalle funzionalità dell'ambiente di sviluppo utilizzato, è possibile utilizzare le funzionalità di traccia e registrazione messaggi di [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] per eseguire il debug di tutte le eccezioni e ottimizzare le prestazioni delle applicazioni.Per ulteriori informazioni, vedere [Utilizzo delle tracce per risolvere i problemi di un'applicazione](../../../docs/framework/wcf/diagnostics/tracing/using-tracing-to-troubleshoot-your-application.md).  
  
## Problemi di prestazioni e XmlSerializer  
 I servizi e le applicazioni client che utilizzano tipi di dati serializzabili tramite <xref:System.Xml.Serialization.XmlSerializer> generano e compilano il codice di serializzazione per tali dati in fase di esecuzione, il che può rallentare le prestazioni all'avvio.  
  
> [!NOTE]
>  Un codice di serializzazione pregenerato può essere utilizzato solamente nelle applicazioni client e non nei servizi.  
  
 [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) può migliorare le prestazioni all'avvio per queste applicazioni generando il codice di serializzazione necessario dagli assembly compilati per l'applicazione.Per ulteriori informazioni, vedere [Procedura: migliorare il tempo di avvio di applicazioni client WCF utilizzando XmlSerializer](../../../docs/framework/wcf/feature-details/startup-time-of-wcf-client-applications-using-the-xmlserializer.md).  
  
## Problemi di prestazioni quando ASP.NET ospita servizi WCF  
 Quando un servizio WCF viene ospitato da IIS e ASP.NET, le impostazioni di configurazione di IIS e ASP.NET possono influire sulla velocità effettiva e sul footprint di memoria del servizio WCF.[!INCLUDE[crabout](../../../includes/crabout-md.md)] prestazioni ASP.NET, vedere [Migliorare le prestazioni ASP.NET](http://go.microsoft.com/fwlink/?LinkId=186462) \(la pagina potrebbe essere in inglese\).Un'impostazione che potrebbe avere conseguenze impreviste è <xref:System.Web.Configuration.ProcessModelSection.MinWorkerThreads%2A>, che è una proprietà di <xref:System.Web.Configuration.ProcessModelSection>.Se l'applicazione dispone di un numero fisso o piccolo di client, l'impostazione di <xref:System.Web.Configuration.ProcessModelSection.MinWorkerThreads%2A> su 2 potrebbe fornire una spinta di velocità effettiva in un computer con multiprocessore con un utilizzo della CPU vicino al 100%.Questo aumento nelle prestazioni ha comunque un costo: determinerà anche un aumento dell'utilizzo della memoria, con conseguente riduzione della scalabilità.  
  
## Vedere anche  
 [Amministrazione e diagnostica](../../../docs/framework/wcf/diagnostics/index.md)   
 [Dati di grandi dimensioni e flussi](../../../docs/framework/wcf/feature-details/large-data-and-streaming.md)