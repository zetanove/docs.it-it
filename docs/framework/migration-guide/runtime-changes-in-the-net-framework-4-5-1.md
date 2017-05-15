---
title: Modifiche al runtime in .NET Framework 4.5.1 | Microsoft Docs
ms.custom: 
ms.date: 03/30/2017
ms.prod: .net-framework
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- application compatibility
- runtime changes
- .NET Framework 4.5.1
ms.assetid: da880ad7-ba0a-4368-b340-705e3533c351
caps.latest.revision: 15
author: rpetrusha
ms.author: ronpet
manager: wpickett
ms.translationtype: Human Translation
ms.sourcegitcommit: 9f5b8ebb69c9206ff90b05e748c64d29d82f7a16
ms.openlocfilehash: 4e4903c2f25354005f95b3ed8f9728cfe8a0a92e
ms.contentlocale: it-it
ms.lasthandoff: 04/18/2017

---
# <a name="runtime-changes-in-the-net-framework-451"></a>Modifiche in fase di esecuzione in .NET Framework 4.5.1
In rari casi, le modifiche in fase di esecuzione potrebbero incidere sulle app esistenti destinate alla versione [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)] o 4.5 ma vengono eseguite in fase di esecuzione nella versione 4.51. Sono incluse le modifiche apportate nelle seguenti aree:  
  
-   [Base](#Core)  
  
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
|Serializzazione <xref:System.Collections.Concurrent.ConcurrentDictionary%602?displayProperty=fullName>|Un oggetto <xref:System.Collections.Concurrent.ConcurrentDictionary%602> serializzato in .NET Framework 4.5 con <xref:System.Runtime.Serialization.NetDataContractSerializer> non può essere deserializzato in .NET Framework 4.5.1 e 4.5.2 solo a causa di modifiche interne del tipo.<br /><br /> Questa modifica *non* si applica negli scenari seguenti:<br /><br /> Un oggetto <xref:System.Collections.Concurrent.ConcurrentDictionary%602> serializzato in .NET Framework 4.5 e deserializzato in [!INCLUDE[net_v46](../../../includes/net-v46-md.md)]. <xref:System.Runtime.Serialization.NetDataContractSerializer> in [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] è in grado di deserializzare l'oggetto.<br /><br /> Un oggetto <xref:System.Collections.Concurrent.ConcurrentDictionary%602> serializzato in una versione successiva di .NET Framework e deserializzato in .NET Framework 4.5. <xref:System.Runtime.Serialization.NetDataContractSerializer> in .NET Framework 4.5 è in grado di deserializzare l'oggetto.<br /><br /> Serializzazione e deserializzazione tra versioni di un oggetto <xref:System.Collections.Concurrent.ConcurrentDictionary%602> tra qualsiasi versione di .NET Framework successiva a .NET Framework 4.5. Questa modifica si applica *solo* agli oggetti serializzati con .NET Framework 4.5.|Sono disponibili due soluzioni se è necessario serializzare un oggetto <xref:System.Collections.Concurrent.ConcurrentDictionary%602> in .NET Framework 4.5 e deserializzarlo in una versione successiva di .NET Framework:<br /><br /> Usare un serializzatore alternativo, ad esempio <xref:System.Runtime.Serialization.DataContractSerializer> o <xref:System.Runtime.Serialization.Formatters.Binary.BinaryFormatter>.<br /><br /> Eseguire l'aggiornamento a [!INCLUDE[net_v46](../../../includes/net-v46-md.md)], che supporta la deserializzazione dell'oggetto <xref:System.Collections.Concurrent.ConcurrentDictionary%602> serializzato con .NET Framework 4.5.|Secondario|  
|Classe <xref:System.Diagnostics.Tracing.EventListener?displayProperty=fullName>|<xref:System.Diagnostics.Tracing.EventListener> tronca le stringhe con valori null incorporati. I caratteri null non sono supportati dalla classe <xref:System.Diagnostics.Tracing.EventSource>.|La modifica influisce solo sulle app che usano <xref:System.Diagnostics.Tracing.EventListener> per leggere i dati <xref:System.Diagnostics.Tracing.EventSource> in-process e che usano caratteri null come delimitatori.|Microsoft Edge|  
|Classe <xref:System.Diagnostics.Tracing.EventSource?displayProperty=fullName>|Il runtime applica ora il contratto che specifica quanto segue: una classe derivata da <xref:System.Diagnostics.Tracing.EventSource> che definisce un metodo di eventi ETW deve chiamare il metodo <xref:System.Diagnostics.Tracing.EventSource.WriteEvent%2A?displayProperty=fullName> della classe di base con l'ID evento seguito dagli stessi argomenti passati al metodo di eventi ETW.|Viene generata un'eccezione <xref:System.IndexOutOfRangeException> se un <xref:System.Diagnostics.Tracing.EventListener> legge i dati <xref:System.Diagnostics.Tracing.EventSource> in-process per un'origine evento che viola questo contratto.<br /><br /> Vedere: [Mitigazione: Chiamate al metodo EventSource.WriteEvent](../../../docs/framework/migration-guide/mitigation-eventsource-writeevent-method-calls.md)|Secondario|  
|Deserializzazione di oggetti tra domini applicazione|In alcuni casi, quando un'app usa due o più domini di app con diverse basi dell'applicazione, il tentativo di deserializzare gli oggetti nel contesto di una chiamata logica tra domini di app genera un'eccezione.|Quest problema si manifesta in uno scenario altamente specifico. Per altre informazioni e per la mitigazione, vedere [Mitigazione: Deserializzazione di oggetti tra domini app](../../../docs/framework/migration-guide/mitigation-deserialization-of-objects-across-app-domains.md).|Microsoft Edge|  
|Metodo <xref:System.IO.Stream.Dispose%2A?displayProperty=fullName>|Nelle app di [!INCLUDE[win8_appstore_long](../../../includes/win8-appstore-long-md.md)], gli adattatori flusso di [!INCLUDE[wrt](../../../includes/wrt-md.md)] non chiamano più il metodo <xref:System.IO.Stream.FlushAsync%2A> dal metodo <xref:System.IO.Stream.Dispose%2A>.|Questa modifica dovrebbe essere trasparente. Gli sviluppatori potranno ripristinare il comportamento precedente scrivendo del codice simile al seguente:<br /><br /> `using (System.IO.Stream stream = GetWindowsRuntimeStream() As Stream)  {     // do something     await stream.FlushAsync();   }`|Trasparente|  
  
<a name="WCF"></a>   
## <a name="windows-communication-foundation-wcf-runtime-changes"></a>Modifiche in fase di esecuzione di Windows Communication Foundation (WCF)  
  
|Funzionalità|Modifica|Impatto|Ambito|  
|-------------|------------|------------|-----------|  
|Impostazione di configurazione [minFreeMemoryPercentageToActiveService](http://msdn.microsoft.com/library/ms731336.aspx)|Questa impostazione consente di stabilire la quantità minima di memoria che deve essere disponibile sul server per poter attivare un servizio WCF. È progettata in modo da prevenire eccezioni <xref:System.OutOfMemoryException>. In [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], questa impostazione non aveva alcun effetto. In [!INCLUDE[net_v451](../../../includes/net-v451-md.md)], l'impostazione viene applicata.|Viene generata un'eccezione se la quantità di memoria libera disponibile sul server Web è inferiore alla percentuale definita dall'impostazione di configurazione. Alcuni servizi WCF correttamente avviati ed eseguiti in un ambiente di memoria limitato potrebbero avere esito negativo.<br /><br /> Vedere [Mitigazione: Impostazione della configurazione minFreeMemoryPercentageToActiveService](../../../docs/framework/migration-guide/mitigation-minfreememorypercentagetoactiveservice-configuration-setting.md).|Secondario|  
  
## <a name="see-also"></a>Vedere anche  
 [Modifiche di reindirizzamento](../../../docs/framework/migration-guide/retargeting-changes-in-the-net-framework-4-5-1.md)   
 [Compatibilità delle applicazioni nella versione 4.5](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-5.md)   
 [Compatibilità delle applicazioni nella versione 4.5.2](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-5-2.md)
