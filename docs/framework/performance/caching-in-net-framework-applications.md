---
title: "Caching in .NET Framework Applications | Microsoft Docs"
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
  - "ASP.NET caching"
  - "caching [.NET Framework]"
  - "caching [ASP.NET]"
ms.assetid: c4b47ee0-4b82-4124-9bce-818088385e34
caps.latest.revision: 26
author: "tdykstra"
ms.author: "tdykstra"
manager: "wpickett"
caps.handback.revision: 26
---
# Caching in .NET Framework Applications
La memorizzazione nella cache consente di archiviare i dati in memoria per l'accesso rapido.  Quando si accede nuovamente ai dati, le applicazioni possono ottenere i dati dalla cache anziché recuperarli dall'origine.  Ciò può migliorare prestazioni e scalabilità.  Inoltre, la memorizzazione nella cache rende disponibili i dati quando l'origine dati non è temporaneamente disponibile.  
  
 .NET Framework fornisce funzionalità di memorizzazione nella cache che è possibile utilizzare per migliorare le prestazioni e la scalabilità sia del client Windows che delle applicazioni server, come ASP.NET.  
  
> [!NOTE]
>  In [!INCLUDE[net_v35_short](../../../includes/net-v35-short-md.md)] e versioni precedenti, ASP.NET fornisce un'implementazione della cache in memoria nello spazio dei nomi <xref:System.Web.Caching>.  Nelle versioni precedenti di [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] la memorizzazione nella cache è disponibile solo nello spazio dei nomi <xref:System.Web> e pertanto richiede una dipendenza nelle classi ASP.NET.  In .NET Framework 4 lo spazio dei nomi <xref:System.Runtime.Caching> contiene le API progettate sia per le applicazioni Web che non Web.  
  
## Memorizzazione di dati nella cache  
 È possibile memorizzare nella cache le informazioni utilizzando le classi nello spazio dei nomi <xref:System.Runtime.Caching>.  Le classi di memorizzazione nella cache in questo spazio dei nomi forniscono le funzionalità seguenti:  
  
-   Tipi astratti che forniscono gli elementi fondamentali per la creazione di implementazioni della cache personalizzate.  
  
-   Un'implementazione della cache oggetti in memoria concreta.  
  
 La classe di base astratta di memorizzazione nella cache \(<xref:System.Runtime.Caching.ObjectCache>\) definisce le attività di memorizzazione nella cache seguenti:  
  
-   Creazione e gestione delle voci della cache.  
  
-   Specifica delle informazioni sulla scadenza e sulla rimozione.  
  
-   Attivazione degli eventi generati in risposta a modifiche apportate alle voci della cache.  
  
 La classe <xref:System.Runtime.Caching.MemoryCache> è un'implementazione della cache oggetti in memoria della classe <xref:System.Runtime.Caching.ObjectCache>.  È possibile utilizzare la classe <xref:System.Runtime.Caching.MemoryCache> per la maggior parte delle attività di memorizzazione nella cache.  
  
> [!NOTE]
>  La classe <xref:System.Runtime.Caching.MemoryCache> viene modellata sull'oggetto cache ASP.NET definito nello spazio dei nomi <xref:System.Web.Caching>.  Di conseguenza, la logica di memorizzazione nella cache interna è simile alla logica fornita nelle versioni precedenti di ASP.NET.  
  
 Per un esempio di come utilizzare la memorizzazione nella cache in un'applicazione WPF, vedere [Procedura dettagliata: memorizzazione dei dati di un'applicazione nella cache di un'applicazione WPF](../../../docs/framework/wpf/advanced/walkthrough-caching-application-data-in-a-wpf-application.md).  
  
## Memorizzazione nella cache nelle applicazioni ASP.NET  
 Le classi di memorizzazione nella cache nello spazio dei nomi <xref:System.Runtime.Caching> forniscono le funzionalità per memorizzare i dati nella cache in ASP.NET.  
  
> [!NOTE]
>  Se l'applicazione è destinata a [!INCLUDE[net_v35_short](../../../includes/net-v35-short-md.md)] o versioni precedenti, è necessario utilizzare le classi di memorizzazione nella cache definite nello spazio dei nomi <xref:System.Web.Caching>.  Per ulteriori informazioni, vedere [ASP.NET Caching Overview](../Topic/ASP.NET%20Caching%20Overview.md).  
  
> [!NOTE]
>  Quando si sviluppano nuove applicazioni, è consigliabile utilizzare la classe <xref:System.Runtime.Caching.MemoryCache>.  L'API fornita nello spazio dei nomi <xref:System.Runtime.Caching> è analoga all'API fornita nello spazio dei nomi <xref:System.Web.Caching.Cache>.  Di conseguenza, l'API risulterà familiare se è già stata utilizzata la memorizzazione nella cache nelle versioni precedenti di ASP.NET. Per un esempio di come utilizzare la memorizzazione nella cache nelle applicazioni ASP.NET, vedere [Walkthrough: Caching Application Data in ASP.NET](../Topic/Walkthrough:%20Caching%20Application%20Data%20in%20ASP.NET.md).  
  
### Memorizzazione nella cache dell'output  
 Per memorizzare manualmente nella cache i dati dell'applicazione, è possibile utilizzare la classe <xref:System.Runtime.Caching.MemoryCache> in ASP.NET. ASP.NET supporta inoltre la memorizzazione nella cache di output, che consente di archiviare in memoria l'output generato di pagine, controlli e risposte HTTP.  È possibile configurare la memorizzazione nella cache di output in modo dichiarativo in una pagina Web ASP.NET oppure utilizzando le impostazioni del file Web.config.  Per ulteriori informazioni, vedere [Elemento outputCache per caching \(schema delle impostazioni ASP.NET\)](http://msdn.microsoft.com/it-it/47cd2b47-316f-4dfd-bbf8-539be3066fee).  
  
 ASP.NET consente di estendere la memorizzazione nella cache di output creando provider di cache di output personalizzati.  Utilizzando i provider personalizzati, è possibile archiviare il contenuto memorizzato nella cache mediante altri dispositivi di archiviazione, come dischi, archiviazione di tipo cloud e motori di cache distribuiti.  Per creare un provider di cache di output personalizzato, è necessario creare una classe che deriva dalla classe <xref:System.Web.Caching.OutputCacheProvider> e configurare l'applicazione per l'utilizzo del provider di cache di output personalizzato.  
  
## Memorizzazione nella cache nei servizi WCF REST  
 Per i servizi WCF REST, .NET Framework consente di usufruire della memorizzazione nella cache di output dichiarativa, disponibile in ASP.NET. Ciò consente di memorizzare nella cache le risposte inviate dalle operazioni dei servizi WCF REST.  Quando un utente invia una richiesta HTTP GET a un servizio configurato per la memorizzazione nella cache, ASP.NET restituisce la risposta memorizzata nella cache e il metodo del servizio non viene chiamato.  Dopo la scadenza della cache, al successivo invio di una richiesta HTTP GET da parte dell'utente, viene chiamato il metodo del servizio e la risposta viene nuovamente memorizzata nella cache.  
  
 .NET Framework consente inoltre di implementare la memorizzazione condizionale nella cache di HTTP GET.  Negli scenari REST, una richiesta HTTP GET condizionale viene spesso utilizzata dai servizi per implementare la memorizzazione intelligente nella cache HTTP come descritto in [Specifica HTTP](http://go.microsoft.com/fwlink/?LinkId=165800).  Per ulteriori informazioni, vedere [Memorizzare nella cache supporto per i servizi HTTP Web WCF](http://go.microsoft.com/fwlink/?LinkId=184598).  
  
## Estensione della memorizzazione nella cache in .NET Framework  
 La memorizzazione nella cache in .NET Framework è progettata per essere estensibile.  La classe <xref:System.Runtime.Caching.ObjectCache> consente di creare un'implementazione della cache personalizzata.  Questa classe fornisce membri disponibili per tutte le applicazioni gestite, tra cui Windows Form, Windows Presentation Foundation \(WPF\) e Windows Communications Foundation \(WCF\).  È possibile eseguire questa operazione per creare una classe cache che utilizza un meccanismo di archiviazione diverso oppure se si desidera il controllo granulare per le operazioni della cache.  
  
 Per estendere la memorizzazione nella cache, è possibile effettuare le operazioni seguenti:  
  
-   Creare una classe personalizzata che deriva dalla classe <xref:System.Runtime.Caching.ObjectCache>, quindi fornire un'implementazione della cache personalizzata nella classe derivata.  
  
-   Creare una classe che deriva dalla classe <xref:System.Runtime.Caching.MemoryCache> e personalizzare o estendere la classe derivata.  Per un esempio di come eseguire questa operazione, vedere [Memorizzazione nella cache dei Dati dell'applicazione mediante più oggetti cache in un'applicazione ASP.NET](http://blogs.msdn.com/aspnetue/archive/2010/03/22/caching-application-data-by-using-multiple-cache-objects-in-an-asp-net-application.aspx).  
  
-   Creare una classe che deriva dalla classe <xref:System.Web.Caching.OutputCacheProvider> e configurare l'applicazione per utilizzare il provider di cache di output personalizzato.  
  
 Per ulteriori informazioni, vedere l'intervento relativo alla [Memorizzazione nella cache di output estensibile con ASP.NET 4 \(VS 2010 e .NET 4.0\)](http://go.microsoft.com/fwlink/?LinkId=185772) nel blog di Scott Guthrie.  
  
## Vedere anche  
 <xref:System.Runtime.Caching.ObjectCache>   
 <xref:System.Runtime.Caching.MemoryCache>   
 [Procedura dettagliata: memorizzazione dei dati di un'applicazione nella cache di un'applicazione WPF](../../../docs/framework/wpf/advanced/walkthrough-caching-application-data-in-a-wpf-application.md)   
 [Walkthrough: Caching Application Data in ASP.NET](../Topic/Walkthrough:%20Caching%20Application%20Data%20in%20ASP.NET.md)