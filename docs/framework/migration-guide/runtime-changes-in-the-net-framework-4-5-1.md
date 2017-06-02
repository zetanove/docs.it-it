---
title: "Modifiche in fase di esecuzione in .NET Framework 4.5.1 | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "compatibilità delle applicazioni"
  - "modifiche al runtime"
  - ".NET Framework 4.5.1"
ms.assetid: da880ad7-ba0a-4368-b340-705e3533c351
caps.latest.revision: 15
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 15
---
# Modifiche in fase di esecuzione in .NET Framework 4.5.1
In rari casi, le modifiche in fase di esecuzione potrebbero incidere sulle app esistenti destinate alla versione [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] o 4.5 ma vengono eseguite in fase di esecuzione nella versione 4.51. Sono incluse le modifiche apportate nelle seguenti aree:  
  
-   [Componenti di base](#Core)  
  
-   [Windows Communication Foundation (WCF)](#WCF)  
  
 La colonna Ambito nelle tabelle seguenti contiene il significato di ogni modifica:  
  
-   Principale Una modifica significativa che influisce su un numero elevato di app o che richiede variazioni sostanziali del codice. Notare che nessuna delle modifiche in fase di esecuzione rientra in questa categoria.  
  
-   Secondaria. Una modifica che influisce su un numero ridotto di app o che richiede variazioni marginali del codice.  
  
-   Bordo. Una modifica che influisce sulle app in scenari molto specifici e non comuni.  
  
-   Trasparente. Una modifica che non ha effetti evidenti sullo sviluppatore o sull'utente dell'app. L'app non dovrebbe richiedere variazioni a causa di questa modifica.  
  
<a name="Core"></a>   
## <a name="core-runtime-changes"></a>Modifiche in fase di esecuzione core  
  
|Funzionalità|Modifica|Impatto|Ambito|  
|-------------|------------|------------|-----------|  
|<xref:System.Collections.Concurrent.ConcurrentDictionary%602?displayProperty=fullName> serializzazione</TKey, TValue>|Oggetto <xref:System.Collections.Concurrent.ConcurrentDictionary%602> oggetto serializzato in .NET Framework 4.5 con il <xref:System.Runtime.Serialization.NetDataContractSerializer> non può essere deserializzato in .NET Framework 4.5.1 e 4.5.2 solo a causa della modifica il tipo interno.\</TKey, TValue><br /><br /> Questa modifica viene *non* applica nei seguenti scenari:<br /><br /> Oggetto <xref:System.Collections.Concurrent.ConcurrentDictionary%602> oggetto serializzato in .NET Framework 4.5 e deserializzato nel [!INCLUDE[net_v46](../../../includes/net-v46-md.md)].</TKey, TValue> Il <xref:System.Runtime.Serialization.NetDataContractSerializer> nel [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] è in grado di deserializzare l'oggetto.<br /><br /> Oggetto <xref:System.Collections.Concurrent.ConcurrentDictionary%602> oggetto serializzato in una versione successiva di .NET Framework e deserializzato in .NET Framework 4.5.\</TKey, TValue> Il <xref:System.Runtime.Serialization.NetDataContractSerializer> in .NET Framework 4.5 è in grado di deserializzare l'oggetto.<br /><br /> Versione tra serializzazione e deserializzazione di un <xref:System.Collections.Concurrent.ConcurrentDictionary%602> oggetto tra qualsiasi versione di .NET Framework dopo .NET Framework 4.5.</TKey, TValue> Questa modifica si applica a oggetti serializzati con .NET Framework 4.5 *solo*.|Due soluzioni alternative sono disponibili se è necessario serializzare una <xref:System.Collections.Concurrent.ConcurrentDictionary%602> oggetto .NET Framework 4.5 e deserializzarla in una versione successiva di .NET Framework:\</TKey, TValue><br /><br /> Utilizzare un serializzatore alternativo, ad esempio il <xref:System.Runtime.Serialization.DataContractSerializer> o <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>.<br /><br /> Aggiornamento per il [!INCLUDE[net_v46](../../../includes/net-v46-md.md)], che supporta la deserializzazione di <xref:System.Collections.Concurrent.ConcurrentDictionary%602> oggetto serializzato con .NET Framework 4.5.\</TKey, TValue>|Secondario|  
|<xref:System.Diagnostics.Tracing.EventListener?displayProperty=fullName> (classe)|<xref:System.Diagnostics.Tracing.EventListener> tronca le stringhe con caratteri null incorporati. Caratteri null non sono supportati per il <xref:System.Diagnostics.Tracing.EventSource> (classe).|La modifica interessa solo le applicazioni che utilizzano <xref:System.Diagnostics.Tracing.EventListener> leggere <xref:System.Diagnostics.Tracing.EventSource> dati nel processo e che utilizzano caratteri null come delimitatori.|Microsoft Edge|  
|<xref:System.Diagnostics.Tracing.EventSource?displayProperty=fullName> (classe)|Il runtime applica ora il contratto che specifica le operazioni seguenti: una classe derivata da <xref:System.Diagnostics.Tracing.EventSource> che definisce un ETW evento metodo deve chiamare la classe di base <xref:System.Diagnostics.Tracing.EventSource.WriteEvent%2A?displayProperty=fullName> metodo con l'ID evento seguito dagli stessi argomenti passati al metodo eventi ETW.|Un <xref:System.IndexOutOfRangeException> eccezione viene generata se un <xref:System.Diagnostics.Tracing.EventListener> legge <xref:System.Diagnostics.Tracing.EventSource> dati in-process per un'origine evento che viola questo contratto.<br /><br /> Vedere [attenuazione: chiamate di metodo EventSource WriteEvent](../../../docs/framework/migration-guide/mitigation-eventsource-writeevent-method-calls.md)|Secondario|  
|Deserializzazione di oggetti tra domini applicazione|In alcuni casi, quando un'app usa due o più domini di app con diverse basi dell'applicazione, il tentativo di deserializzare gli oggetti nel contesto di una chiamata logica tra domini di app genera un'eccezione.|Quest problema si manifesta in uno scenario altamente specifico. Per ulteriori informazioni e prevenzione, vedere [attenuazione: deserializzazione di oggetti tra domini App](../../../docs/framework/migration-guide/mitigation-deserialization-of-objects-across-app-domains.md).|Microsoft Edge|  
|<xref:System.IO.Stream.Dispose%2A?displayProperty=fullName> (metodo)|In [!INCLUDE[win8_appstore_long](../../../includes/win8-appstore-long-md.md)] App, [!INCLUDE[wrt](../../../includes/wrt-md.md)] adattatori del flusso non chiamano più il <xref:System.IO.Stream.FlushAsync%2A> metodo il <xref:System.IO.Stream.Dispose%2A> metodo.|Questa modifica dovrebbe essere trasparente. Gli sviluppatori potranno ripristinare il comportamento precedente scrivendo del codice simile al seguente:<br /><br /> `using (System.IO.Stream stream = GetWindowsRuntimeStream() As Stream)  {     // do something     await stream.FlushAsync();   }`|Trasparente|  
  
<a name="WCF"></a>   
## <a name="windows-communication-foundation-wcf-runtime-changes"></a>Modifiche in fase di esecuzione di Windows Communication Foundation (WCF)  
  
|Funzionalità|Modifica|Impatto|Ambito|  
|-------------|------------|------------|-----------|  
|[minFreeMemoryPercentageToActiveService](http://msdn.microsoft.com/library/ms731336.aspx) l'impostazione di configurazione|Questa impostazione consente di stabilire la quantità minima di memoria che deve essere disponibile sul server per poter attivare un servizio WCF. È progettato per impedire <xref:System.OutOfMemoryException> eccezioni. In [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], questa impostazione non aveva alcun effetto. In [!INCLUDE[net_v451](../../../includes/net-v451-md.md)], l'impostazione viene applicata.|Viene generata un'eccezione se la quantità di memoria libera disponibile sul server Web è inferiore alla percentuale definita dall'impostazione di configurazione. Alcuni servizi WCF correttamente avviati ed eseguiti in un ambiente di memoria limitato potrebbero avere esito negativo.<br /><br /> Vedere [attenuazione: configurazione minFreeMemoryPercentageToActiveService](../../../docs/framework/migration-guide/mitigation-minfreememorypercentagetoactiveservice-configuration-setting.md).|Secondario|  
  
## <a name="see-also"></a>Vedere anche  
 [Modifiche di reindirizzamento](../../../docs/framework/migration-guide/retargeting-changes-in-the-net-framework-4-5-1.md)   
 [Compatibilità delle applicazioni in 4.5](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-5.md)   
 [Compatibilità delle applicazioni nella versione 4.5.2](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-5-2.md)