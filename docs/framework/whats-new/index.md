---
title: "Novità di .NET Framework | Microsoft Docs"
ms.custom: 
ms.date: 05/02/2017
ms.prod: .net-framework-4.6
ms.reviewer: 
ms.suite: 
ms.technology:
- dotnet-clr
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- what's new [.NET Framework]
ms.assetid: 1d971dd7-10fc-4692-8dac-30ca308fc0fa
caps.latest.revision: 292
author: rpetrusha
ms.author: ronpet
manager: wpickett
translationtype: Human Translation
ms.sourcegitcommit: adb9c30b6dc52ea17410423fd76c938e258549eb
ms.openlocfilehash: 7f83abf73931117d563ec1d609aae5764adfb57d
ms.lasthandoff: 05/02/2017

---
# <a name="what39s-new-in-the-net-framework"></a>Novità di .NET Framework
<a name="introduction"></a> Questo articolo offre un riepilogo dei principali nuovi miglioramenti e funzionalità introdotti nelle versioni seguenti di .NET Framework:  
  
 [.NET Framework 4.7](#v47)   
 [.NET Framework 4.6.2](#v462)   
 [.NET Framework 4.6.1](#v461)   
 [.NET 2015 e .NET Framework 4.6](#v46)   
 [.NET Framework 4.5.2](#v452)   
 [.NET Framework 4.5.1](#v451)   
 [.NET Framework 4.5](#core)  
  
 Non vengono fornite informazioni complete su ogni nuova funzionalità e l'articolo è soggetto a modifiche. Per informazioni generali su .NET Framework, vedere [Introduzione a .NET Framework](http://msdn.microsoft.com/library/c693fd34-88fe-4d90-b332-19eeadf3b7e7). Per informazioni sulle piattaforme supportate, vedere [Requisiti di sistema di .NET Framework](~/docs/framework/get-started/system-requirements.md). Per i collegamenti per il download e le istruzioni di installazione, vedere [Guida all'installazione](../../../docs/framework/install/guide-for-developers.md).  
  
> [!NOTE]
>  Il team di .NET Framework rende disponibili anche alcune funzionalità fuori programma con NuGet per espandere le piattaforme supportate e introdurre nuove funzionalità, ad esempio le raccolte non modificabili e i tipi di vettore abilitati per SIMD. Per altre informazioni, vedere [API e librerie di classi aggiuntive](http://msdn.microsoft.com/library/cf2d9006-b631-4e5d-81cd-20aab78c60f1) e [.NET Framework e rilascio fuori programma](~/docs/framework/get-started/the-net-framework-and-out-of-band-releases.md). Vedere l'[elenco completo dei pacchetti NuGet](http://blogs.msdn.com/b/dotnet/p/nugetpackages.aspx) per .NET Framework oppure sottoscrivere [questo feed](https://nuget.org/api/v2/curated-feeds/dotnetframework/Packages/).  
  
<a name="v47"></a>   
## <a name="introducing-the-net-framework-47"></a>Introduzione a .NET Framework 4.7  
 .NET Framework 4.7 è basato su .NET Framework 4.6, 4.6.1 e 4.6.2 con l'aggiunta di molte nuove correzioni e funzionalità, pur rimanendo un prodotto molto stabile.  

### <a name="downloading-and-installing-the-net-framework-47"></a>Download e installazione di .NET Framework 4.7
 
È possibile scaricare .NET Framework 4.7 dalle posizioni seguenti:  
  
- [Programma di installazione Web di .NET Framework 4.7](http://go.microsoft.com/fwlink/?LinkId=825299)  
  
- [Programma di installazione offline di .NET Framework 4.7](http://go.microsoft.com/fwlink/?LinkId=825303)  
  
.NET Framework 4.7 può essere installato in Windows 10, Windows 8.1, Windows 7 e nelle piattaforme server corrispondenti a partire da Windows Server 2008 R2 SP1. È possibile installare .NET Framework 4.7 usando il programma di installazione Web o il programma di installazione offline. Per la maggior parte degli utenti è consigliabile usare il programma di installazione Web.  
  
Per .NET Framework 4.7 in Visual Studio 2012 o versioni successive è possibile installare [.NET Framework 4.7 Developer Pack](http://go.microsoft.com/fwlink/?LinkId=825319).  
  
### <a name="whats-new-in-the-net-framework-47"></a>Novità di .NET Framework 4.7

.NET Framework 4.7 include nuove funzionalità nelle aree seguenti:

- [Base](#Core47)
- [Rete](#net47)
- [ASP.NET 2.0](#ASP-NET47)
- [Windows Communication Foundation (WCF)](#wcf47)
- [Windows Form](#wf47)
- [Windows Presentation Foundation (WPF)](#WPF47)

Per l'elenco delle nuove API aggiunte a .NET Framework 4.7, vedere l'argomento [.NET Framework 4.7 API Changes](https://github.com/Microsoft/dotnet/blob/master/releases/net47/dotnet47-api-changes.md) (Modifiche alle API di .NET Framework 4.7) su GitHub. Per l'elenco delle correzioni di bug e dei miglioramenti apportati alle funzionalità in .NET Framework 4.7, vedere l'argomento [.NET Framework 4.7 List of Changes](http://gutithub.com/Microsoft/dotnet/blob/master/releases/net47/dotnet47-changes.md) (Elenco delle modifiche di .NET Framework 4.7) su GitHub.  Per altre informazioni, vedere [Annuncio del rilascio di .NET Framework 4.7](https://blogs.msdn.microsoft.com/dotnet/2017/04/05/announcing-the-net-framework-4-7/) in .NET Blog.
  
<a name="Core47" />
### <a name="core"></a>Base ###

.NET Framework 4.7 migliora la serializzazione da <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>:

**Funzionalità migliorate con l'algoritmo ECC (Elliptic Curve Cryptography)***

In .NET Framework 4.7, sono stati aggiunti i metodi `ImportParameters(ECParameters)` alle classi <xref:System.Security.Cryptography.ECDsa> e <xref:System.Security.Cryptography.ECDiffieHellman> per consentire a un oggetto di rappresentare una chiave già stabilita. È stato anche aggiunto un metodo `ExportParameters(Boolean)` per l'esportazione della chiave usando parametri della curva esplicita.

.NET Framework 4.7 aggiunge anche il supporto per le curve aggiuntive (inclusa la suite di curve Brainpool) e ha aggiunto definizioni predefinite per semplificare la creazione attraverso i nuovi metodi factory <xref:System.Security.Cryptography.ECDsa.Create%2A> e <xref:System.Security.Cryptography.ECDiffieHellman.Create%2A>.

È possibile visualizzare un [esempio dei miglioramenti alla crittografia di .NET Framework 4.7](https://gist.github.com/richlander/5a182899895a87a296c21ada97f7a54e) su GitHub.

**Supporto migliorato per i caratteri di controllo da DataContractJsonSerializer**

In .NET Framework 4.7 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> serializza i caratteri di controllo in conformità con lo standard ECMAScript 6. Questo comportamento è abilitato per impostazione predefinita per le applicazioni che utilizzano .NET Framework 4.7 ed è una funzionalità che prevede il consenso esplicito per le applicazioni che sono in esecuzione con .NET Framework 4.7, ma sono destinate a una versione precedente di .NET Framework. Per altre informazioni, vedere [Reindirizzamento delle modifiche in .NET Framework versione 4.7](../../../docs/framework/migration-guide/retargeting-changes-in-the-net-framework-4-7.md).

<a name="net47" />
### <a name="networking"></a>Rete ###

.NET Framework 4.7 aggiunge la seguente funzionalità relativa alla rete:

**Supporto del sistema operativo predefinito per i protocolli TLS***

Lo stack TLS, che viene usato da <xref:System.Net.Security.SslStream?displayProperty=fullName> e i componenti up-stack, ad esempio HTTP, FTP e SMTP, consentono agli sviluppatori di usare i protocolli TLS predefiniti supportati dal sistema operativo. Gli sviluppatori non devono più impostare come hardcoded una versione TLS.

<a name="ASP-NET47" />
### <a name="aspnet"></a>ASP.NET ###

In .NET Framework 4.7, ASP.NET include le nuove funzionalità seguenti:

**Estendibilità della cache oggetti**

A partire da Framework .NET 4.7, ASP.NET aggiunge un nuovo set di API che consente agli sviluppatori di sostituire le implementazioni di ASP.NET predefinite per la cache di oggetti in memoria e il monitoraggio della memoria. Gli sviluppatori possono ora sostituire uno qualsiasi dei seguenti tre componenti se l'implementazione di ASP.NET non è sufficiente:

- **Archivio cache oggetti**. Usando la nuova sezione di configurazione dei provider di cache, gli sviluppatori possono inserire nuove implementazioni di una cache oggetti per un'applicazione ASP.NET con la nuova interfaccia **ICacheStoreProvider**.
 
- **Monitoraggio della memoria**. Il monitoraggio della memoria predefinito in ASP.NET invia una notifica alle applicazioni quando stanno per raggiungere il limite di byte privati configurato per il processo o quando la RAM fisica totale disponibile nel computer è insufficiente. Quando si approssimano questi limiti, vengono generate le notifiche. Per alcune applicazioni, le notifiche vengono generate troppo vicino ai limiti configurati per consentire reazioni utili. Gli sviluppatori possono ora scrivere monitoraggi della memoria personalizzati in modo da sostituire quello predefinito usando la proprietà <xref:System.Web.Hosting.ApplicationMonitors.MemoryMonitor%2A?displayProperty=fullName>.

- **Reazioni al limite di memoria**. Per impostazione predefinita, ASP.NET prova a ridurre la cache oggetti e a chiamare periodicamente <xref:System.GC.Collect%2A?displayProperty=fullName> quando si approssima il limite di byte privati per il processo. Per alcune applicazioni, la frequenza delle chiamate a <xref:System.GC.Collect%2A?displayProperty=fullName> o la quantità di cache che verrà tagliata sono inefficienti. Gli sviluppatori possono ora sostituire o integrare il comportamento predefinito sottoscrivendo le implementazioni **IObserver** al monitoraggio della memoria dell'applicazione.

<a name="wcf47" />
### <a name="windows-communication-foundation-wcf"></a>Windows Communication Foundation (WCF) ###

Windows Communication Foundation (WFC) aggiunge le seguenti funzionalità e modifiche:

**Possibilità di configurare le impostazioni predefinite di sicurezza dei messaggi su TLS 1.1 o TLS 1.2**

A partire da .NET Framework 4.7, WCF consente di configurare TSL 1.1 o TLS 1.2, oltre a SSL 3.0 e TSL 1.0, come protocollo di sicurezza del messaggio predefinito. Questa funzionalità prevede il consenso esplicito e occorre quindi aggiungere la voce seguente al file di configurazione dell'applicazione:

```xml
<runtime>
   <AppContextSwitchOverrides value="Switch.System.ServiceModel.DisableUsingServicePointManagerSecurityProtocols=false;Switch.System.Net.DontEnableSchUseStrongCrypto=false" /> 
</runtime>
```

**Miglioramento dell'affidabilità le applicazioni WCF e della serializzazione WCF**

WCF include un numero di modifiche al codice che eliminano le race condition, migliorando così le prestazioni e l'affidabilità delle opzioni di serializzazione. Sono inclusi:

- Supporto migliorato per la combinazione di codice sincrono e asincrono nelle chiamate a **SocketConnection.BeginRead** e **SocketConnection.Read**.
- Maggiore affidabilità durante l'interruzione di una connessione con **SharedConnectionListener** e **DuplexChannelBinder**.
- Maggiore affidabilità delle operazioni di serializzazione durante la chiamata del metodo [FormatterServices.GetSerializableMembers](assetId:///System.Runtime.Serialization.FormatterServices.GetSerializableMembers(System.Type??qualifyHint=True&autoUpgrade=False).
- Maggiore affidabilità durante la rimozione di un oggetto waiter con la chiamata del metodo **ChannelSynchronizer.RemoveWaiter**.  

<a name="wf47" />
### <a name="windows-forms"></a>Windows Form ###

In Framework .NET 4.7, Windows Form migliora il supporto per i monitor di valori DPI alti.

**Supporto di valori DPI alti**

A partire dalle applicazioni destinate a .NET Framework 4.7, le funzionalità di .NET Framework prevedono il supporto dei di valori DPI alti e dinamici per Windows Forms Application. Il supporto di valori DPI alti migliora il layout e l'aspetto dei moduli e dei controlli nei monitor di valori DPI alti. I valori DPI cambiano il layout e l'aspetto dei moduli e dei controlli quando l'utente modifica i valori DPI o visualizza il fattore di scala di un'applicazione in esecuzione.

Il supporto di valori DPI alti è una funzionalità che prevede il consenso esplicito e si configurare definendo una sezione [\<System.Windows.Forms.ConfigurationSection>](Windows%20Forms%20Configuration%20Section.md) nel file di configurazione dell'applicazione. Per altre informazioni sull'aggiunta del supporto di valori DPI elevati e dinamici a un'applicazione Windows Form, vedere [Supporto di valori DPI elevati in Windows Form](High%20DPI%20Support%20In%20Windows%20Forms.md).  

<a name="WPF47"></a>   
### <a name="windows-presentation-foundation-wpf"></a>Windows Presentation Foundation (WPF)

In .NET Framework 4.7, WPF include i miglioramenti seguenti:

**Supporto per lo stack di tocco/stilo basato sui messaggi basato sui messaggi WM_POINTER Windows**

È ora possibile scegliere di usare uno stack di tocco/stilo basato sui [messaggi WM_POINTER](https://msdn.microsoft.com/library/windows/desktop/hh454903(v=vs.85).aspx) invece che su WISP (Windows Ink Services Platform). È una funzionalità di .NET Framework che prevede il consenso esplicito. Per altre informazioni, vedere [Reindirizzamento delle modifiche in .NET Framework versione 4.7](Retargeting%20Changes%20in%20the%20.NET%20Framework%204.7.md).

**Nuova implementazione per le API di stampa WPF**

Le API di stampa di WPF nella classe [System.Printing.PrintQueue](assetId:///T:System.Printing.PrintQueue?qualifyHint=True&autoUpgrade=True) chiamano l'[API di gestione del pacchetto dei documenti di stampa](https://msdn.microsoft.com/library/windows/desktop/hh448418(v=vs.85).aspx) invece dell'[API di stampa XPS](https://msdn.microsoft.com/library/windows/desktop/ff686814(v=vs.85).aspx) deprecata. Per l'impatto di questa modifica sulla compatibilità delle applicazioni, vedere [Reindirizzamento delle modifiche in .NET Framework versione 4.7](Retargeting%20Changes%20in%20the%20.NET%20Framework%204.7.md). 

<a name="v462"></a>   
## <a name="whats-new-in-the-net-framework-462"></a>Novità di .NET Framework 4.6.2  
.NET Framework 4.6.2 include nuove funzionalità nelle aree seguenti:  
  
-   [ASP.NET 2.0](#ASPNET462)  
  
-   [Categorie di caratteri](#Strings)  
  
-   [Crittografia](#Crypto462)  
  
-   [SqlClient](#SQLClient)  
  
-   [Windows Communication Foundation](#WCF)  
  
-   [Windows Presentation Foundation (WPF)](#WPF462)  
  
-   [Windows Workflow Foundation (WF)](#WF462)  
  
-   [ClickOnce](#ClickOnce)  
  
-   [Conversione di Windows Form e applicazioni WPF in applicazioni UWP](#UWPConvert)  
  
-   [Miglioramenti apportati al debug](#Debug462)  
  
 Per un elenco delle nuove API aggiunte a .NET Framework 4.6.2, vedere l'argomento sulle [modifiche apportate all'API di .NET Framework 4.6.2](https://github.com/Microsoft/dotnet/blob/master/releases/net462/dotnet462-api-changes.md) su GitHub. Per l'elenco dei miglioramenti apportati alle funzionalità e delle correzioni di bug in .NET Framework 4.6.2, vedere l'argomento [.NET Framework 4.6.2 List of Changes](http://go.microsoft.com/fwlink/?LinkId=708778) (Elenco delle modifiche in .NET Framework 4.6.2) su GitHub.  Per altre informazioni, vedere l'[annuncio di .NET Framework 4.6.2](https://blogs.msdn.microsoft.com/dotnet/2016/08/02/announcing-net-framework-4-6-2/) in .NET Blog.  
  
<a name="ASPNET462"></a>   
### <a name="aspnet"></a>ASP.NET  
 In .NET Framework 4.6.2, ASP.NET include i miglioramenti seguenti:  
  
 **Supporto migliorato per i messaggi di errore localizzati nei validator di annotazione dei dati**  
 I validator di annotazione dei dati consentono di eseguire la convalida aggiungendo uno o più attributi a una proprietà di classe. L'elemento [ValidationAttribute.ErrorMessage](assetId:///P:System.ComponentModel.DataAnnotations.ValidationAttribute.ErrorMessage?qualifyHint=True&autoUpgrade=True) dell'attributo definisce il testo del messaggio di errore se la convalida non riesce. A partire da .NET Framework 4.6.2, ASP.NET semplifica la localizzazione dei messaggi di errore. I messaggi di errore verranno localizzati se:  
  
1.  [ValidationAttribute.ErrorMessage](assetId:///P:System.ComponentModel.DataAnnotations.ValidationAttribute.ErrorMessage?qualifyHint=True&autoUpgrade=True) viene indicato nell'attributo di convalida.  
  
2.  Il file di risorse è archiviato nella cartella App_LocalResources.  
  
3.  Il nome del file di risorse localizzato ha il formato `DataAnnotation.Localization.{`*nome*`}.resx`, dove *nome* è il nome delle impostazioni cultura con il formato *codicelingua*`-`*codicepaese/area geografica* o *codicelingua*.  
  
4.  Il nome della chiave della risorsa è la stringa assegnata all'attributo [ValidationAttribute.ErrorMessage](assetId:///P:System.ComponentModel.DataAnnotations.ValidationAttribute.ErrorMessage?qualifyHint=True&autoUpgrade=True) e il relativo valore è il messaggio di errore localizzato.  
  
 Ad esempio, l'attributo di annotazione dei dati seguente definisce il messaggio di errore delle impostazioni cultura predefinite per una classificazione non valida.  
  
```csharp  
  
public class RatingInfo  
{  
   [Required(ErrorMessage = "The rating must be between 1 and 10.")]  
   [Display(Name = "Your Rating")]  
   public int Rating { get; set; }  
}  
  
```  
  
```vb  
  
Public Class RatingInfo  
   \<Required(ErrorMessage = "The rating must be between 1 and 10.")>  
   \<Display(Name = "Your Rating")>  
   Public Property Rating As Integer = 1  
End Class  
  
```  
  
 È quindi possibile creare il file di risorse DataAnnotation.Localization.fr.resx, la cui chiave è la stringa del messaggio di errore e il cui valore è il messaggio di errore localizzato. Il file deve essere salvato nella cartella `App.LocalResources`. Ad esempio, di seguito vengono riportati la chiave e il relativo valore in un messaggio di errore in lingua francese (fr):  
  
|Nome|Valore|  
|----------|-----------|  
|La classificazione deve essere compresa tra 1 e 10.|La note doit être comprise entre 1 et 10.|  
  
 Questo file può quindi  
  
 La localizzazione dell'annotazione dei dati è anche estensibile. Gli sviluppatori possono collegare il proprio provider di localizzazione delle stringhe implementando l'interfaccia di [IStringLocalizerProvider](assetId:///T:System.Web.Globalization.IStringLocalizerProvider?qualifyHint=False&autoUpgrade=True) per archiviare la stringa di localizzazione in un posto diverso da un file di risorse.  
  
 **Supporto asincrono con provider di archiviazione dello stato sessione**  
 ASP.NET ora offre metodi di restituzione di Task da usare con i provider dell'archivio per lo stato sessione, consentendo quindi alle applicazioni ASP.NET di sfruttare i vantaggi delle operazioni asincrone in termini di scalabilità. Per supportare le operazioni asincrone con provider di archiviazione dello stato sessione, ASP.NET include la nuova interfaccia [System.Web.SessionState.ISessionStateModule](assetId:///T:System.Web.SessionState.ISessionStateModule?qualifyHint=True&autoUpgrade=True), che eredita da [IHttpModule](assetId:///T:System.Web.IHttpModule?qualifyHint=False&autoUpgrade=True) e permette agli sviluppatori di implementare i propri provider di moduli dello stato sessione e di archiviazione asincrona delle sessioni. L'interfaccia viene definita come segue:  
  
```csharp  
  
public interface ISessionStateModule : IHttpModule {  
    void ReleaseSessionState(HttpContext context);  
    Task ReleaseSessionStateAsync(HttpContext context);  
}  
  
```  
  
 La classe [SessionStateUtility](assetId:///T:System.Web.SessionState.SessionStateUtility?qualifyHint=False&autoUpgrade=True) include anche due nuovi metodi, [IsSessionStateReadOnly](assetId:///M:System.Web.SessionState.SessionStateUtility.IsSessionStateReadOnly(System.Web.HttpContext)?qualifyHint=False&autoUpgrade=True) e [IsSessionStateRequired](assetId:///M:System.Web.SessionState.SessionStateUtility.IsSessionStateRequired(System.Web.HttpContext)?qualifyHint=False&autoUpgrade=True), che possono essere usati a supporto delle operazioni asincrone.  
  
 **Supporto asincrono per provider di cache di output**  
 A partire da .NET Framework 4.6.2, i metodi di restituzione di Task possono essere usati con i provider di cache di output per usufruire dei vantaggi di scalabilità offerti dalle operazioni asincrone.  I provider che implementano questi metodi riducono i blocchi dei thread su un server Web e migliorano la scalabilità di un servizio ASP.NET.  
  
 Per supportare i provider di cache di output asincroni sono state aggiunte le API seguenti:  
  
-   Classe [System.Web.Caching.OutputCacheProviderAsync](assetId:///T:System.Web.Caching.OutputCacheProviderAsync?qualifyHint=True&autoUpgrade=True), che eredita da [System.Web.Caching.OutputCacheProvider](assetId:///T:System.Web.Caching.OutputCacheProvider?qualifyHint=True&autoUpgrade=True) e permette agli sviluppatori di implementare un provider di cache di output asincrono.  
  
-   Classe [OutputCacheUtility](assetId:///T:System.Web.Caching.OutputCacheUtility?qualifyHint=False&autoUpgrade=True), che fornisce metodi helper per la configurazione della cache di output.  
  
-   18 nuovi metodi nella classe [System.Web.HttpCachePolicy](assetId:///T:System.Web.HttpCachePolicy?qualifyHint=True&autoUpgrade=True), tra cui [GetCacheability](assetId:///M:System.Web.HttpCachePolicy.GetCacheability?qualifyHint=False&autoUpgrade=True), [GetCacheExtensions](assetId:///M:System.Web.HttpCachePolicy.GetCacheExtensions?qualifyHint=False&autoUpgrade=True), [GetETag](assetId:///M:System.Web.HttpCachePolicy.GetETag?qualifyHint=False&autoUpgrade=True), [GetETagFromFileDependencies](assetId:///M:System.Web.HttpCachePolicy.GetETagFromFileDependencies?qualifyHint=False&autoUpgrade=True), [GetMaxAge](assetId:///M:System.Web.HttpCachePolicy.GetMaxAge?qualifyHint=False&autoUpgrade=True), [GetMaxAge](assetId:///M:System.Web.HttpCachePolicy.GetMaxAge?qualifyHint=False&autoUpgrade=True), [GetNoStore](assetId:///M:System.Web.HttpCachePolicy.GetNoStore?qualifyHint=False&autoUpgrade=True), [GetNoTransforms](assetId:///M:System.Web.HttpCachePolicy.GetNoTransforms?qualifyHint=False&autoUpgrade=True), [GetOmitVaryStar](assetId:///M:System.Web.HttpCachePolicy.GetOmitVaryStar?qualifyHint=False&autoUpgrade=True), [GetProxyMaxAge](assetId:///M:System.Web.HttpCachePolicy.GetProxyMaxAge?qualifyHint=False&autoUpgrade=True), [GetRevalidation](assetId:///M:System.Web.HttpCachePolicy.GetRevalidation?qualifyHint=False&autoUpgrade=True), [GetUtcLastModified](assetId:///M:System.Web.HttpCachePolicy.GetUtcLastModified?qualifyHint=False&autoUpgrade=True), [GetVaryByCustom](assetId:///M:System.Web.HttpCachePolicy.GetVaryByCustom?qualifyHint=False&autoUpgrade=True), [HasSlidingExpiration](assetId:///M:System.Web.HttpCachePolicy.HasSlidingExpiration?qualifyHint=False&autoUpgrade=True) e [IsValidUntilExpires](assetId:///M:System.Web.HttpCachePolicy.IsValidUntilExpires?qualifyHint=False&autoUpgrade=True).  
  
-   2 nuovi metodi nella classe [System.Web.HttpCacheVaryByContentEncodings](assetId:///T:System.Web.HttpCacheVaryByContentEncodings?qualifyHint=True&autoUpgrade=True): [GetContentEncodings](assetId:///M:System.Web.HttpCacheVaryByContentEncodings.GetContentEncodings?qualifyHint=False&autoUpgrade=True) e [SetContentEncodings](assetId:///M:System.Web.HttpCacheVaryByContentEncodings.SetContentEncodings(System.String[])?qualifyHint=False&autoUpgrade=True).  
  
-   2 nuovi metodi nella classe [System.Web.HttpCacheVaryByHeaders](assetId:///T:System.Web.HttpCacheVaryByHeaders?qualifyHint=True&autoUpgrade=True): [GetHeaders](assetId:///M:System.Web.HttpCacheVaryByHeaders.GetHeaders?qualifyHint=False&autoUpgrade=True) e [SetHeaders](assetId:///M:System.Web.HttpCacheVaryByHeaders.SetHeaders(System.String[])?qualifyHint=False&autoUpgrade=True).  
  
-   2 nuovi metodi nella classe [System.Web.HttpCacheVaryByParams](assetId:///T:System.Web.HttpCacheVaryByParams?qualifyHint=True&autoUpgrade=True): [GetParams](assetId:///M:System.Web.HttpCacheVaryByParams.GetParams?qualifyHint=False&autoUpgrade=True) e [SetParams](assetId:///M:System.Web.HttpCacheVaryByParams.SetParams(System.String[])?qualifyHint=False&autoUpgrade=True).  
  
-   Nella classe [System.Web.Caching.AggregateCacheDependency](assetId:///T:System.Web.Caching.AggregateCacheDependency?qualifyHint=True&autoUpgrade=True), il metodo [GetFileDependencies](assetId:///M:System.Web.Caching.AggregateCacheDependency.GetFileDependencies?qualifyHint=False&autoUpgrade=True).  
  
-   Nella classe [CacheDependency](assetId:///T:System.Web.Caching.CacheDependency?qualifyHint=False&autoUpgrade=True), il metodo [GetFileDependencies](assetId:///M:System.Web.Caching.CacheDependency.GetFileDependencies?qualifyHint=False&autoUpgrade=True).  
  
<a name="Strings"></a>   
### <a name="character-categories"></a>Categorie di caratteri  
 I caratteri in .NET Framework 4.6.2 sono classificati in base allo standard [Unicode, versione 8.0.0](http://www.unicode.org/versions/Unicode8.0.0/). In .NET Framework 4.6 e .NET Framework 4.6.1, i caratteri sono stati classificati in base alle categorie di caratteri Unicode 6.3.  
  
 Il supporto per Unicode 8.0 è limitato alla classificazione dei caratteri della classe [CharUnicodeInfo](assetId:///T:System.Globalization.CharUnicodeInfo?qualifyHint=False&autoUpgrade=True) e ai tipi e metodi basati sulla stessa. Sono inclusi la classe [StringInfo](assetId:///T:System.Globalization.StringInfo?qualifyHint=False&autoUpgrade=True), il metodo [Char.GetUnicodeCategory](assetId:///M:System.Char.GetUnicodeCategory(System.Char)?qualifyHint=True&autoUpgrade=True) in overload e le [classi di caratteri](../Topic/Character%20Classes%20in%20Regular%20Expressions.md) riconosciute dal motore delle espressioni regolari di .NET Framework.  Il confronto e l'ordinamento di stringhe e caratteri non sono interessati da questa modifica e continuano a basarsi sul sistema operativo sottostante o, nei sistemi Windows 7, sui dati dei caratteri provenienti da .NET Framework.  
  
 Per informazioni sulle modifiche nelle categorie di caratteri da Unicode 6.0 a Unicode 7.0, vedere [The Unicode Standard, Version 7.0.0](http://www.unicode.org/versions/Unicode7.0.0/) nel sito Web The Unicode Consortium. Per informazioni sulle modifiche da Unicode 7.0 a Unicode 8.0, vedere [The Unicode Standard, Version 8.0.0](http://www.unicode.org/versions/Unicode8.0.0/) nel sito Web The Unicode Consortium.  
  
<a name="Crypto462"></a>   
### <a name="cryptography"></a>Crittografia  
 **Supporto per certificati X509 contenenti FIPS 186-3 DSA**  
 .NET Framework 4.6.2 aggiunge il supporto per certificati DSA (Digital Signature Algorithm) X509 le cui chiavi superano il limite di 1024 bit di FIPS 186-2.  
  
 Oltre a supportare le dimensioni della chiave più grandi di FIPS 186-3, .NET Framework 4.6.2 consente di calcolare le firme con la famiglia SHA-2 di algoritmi hash (SHA256, SHA384 e SHA512). Il supporto per FIPS 186-3 viene fornito dalla nuova classe [System.Security.Cryptography.DSACng](assetId:///T:System.Security.Cryptography.DSACng?qualifyHint=True&autoUpgrade=True).  
  
 In conformità alle recenti modifiche apportate alla classe [RSA](assetId:///T:System.Security.Cryptography.RSA?qualifyHint=False&autoUpgrade=True) in .NET Framework 4.6 e alla classe [ECDsa](assetId:///T:System.Security.Cryptography.ECDsa?qualifyHint=False&autoUpgrade=True) in .NET Framework 4.6.1, la classe base astratta [DSA](assetId:///T:System.Security.Cryptography.DSA?qualifyHint=False&autoUpgrade=True) in .NET Framework 4.6.2 offre ulteriori metodi per consentire ai chiamanti di usare questa funzionalità senza eseguire il cast. È possibile chiamare il metodo di estensione [DSACertificateExtensions.GetDSAPrivateKey](assetId:///M:System.Security.Cryptography.X509Certificates.DSACertificateExtensions.GetDSAPrivateKey(System.Security.Cryptography.X509Certificates.X509Certificate2)?qualifyHint=True&autoUpgrade=True) per firmare i dati, come illustrato nell'esempio seguente.  
  
```csharp  
  
public static byte[] SignDataDsaSha384(byte[] data, X509Certificate2 cert)  
{  
    using (DSA dsa = cert.GetDSAPrivateKey())  
    {  
        return dsa.SignData(data, HashAlgorithmName.SHA384);  
    }  
}  
  
```  
  
```vb  
  
Public Shared Function SignDataDsaSha384(data As Byte(), cert As X509Certificate2) As Byte()  
    Using DSA As DSA = cert.GetDSAPrivateKey()  
        Return DSA.SignData(data, HashAlgorithmName.SHA384)  
    End Using  
End Function  
  
```  
  
 Ed è possibile chiamare il metodo di estensione [DSACertificateExtensions.GetDSAPublicKey](assetId:///M:System.Security.Cryptography.X509Certificates.DSACertificateExtensions.GetDSAPublicKey(System.Security.Cryptography.X509Certificates.X509Certificate2)?qualifyHint=True&autoUpgrade=True) per verificare i dati firmati, come illustrato nell'esempio seguente.  
  
```csharp  
  
public static bool VerifyDataDsaSha384(byte[] data, byte[] signature, X509Certificate2 cert)  
{  
    using (DSA dsa = cert.GetDSAPublicKey())  
    {  
        return dsa.VerifyData(data, signature, HashAlgorithmName.SHA384);  
    }  
}  
  
```  
  
```  
  
 Public Shared Function VerifyDataDsaSha384(data As Byte(), signature As Byte(), cert As X509Certificate2) As Boolean  
    Using dsa As DSA = cert.GetDSAPublicKey()  
        Return dsa.VerifyData(data, signature, HashAlgorithmName.SHA384)  
    End Using  
End Function  
  
```  
  
 **Maggiore chiarezza degli input per le routine di derivazione di chiave ECDiffieHellman**  
 .NET Framework 3.5 offre in più il supporto per la chiave concordata Ellipic Curve Diffie-Hellman con tre diverse routine di funzione di derivazione chiave (KDF). Gli input per le routine e le routine stesse sono stati configurati usando le proprietà dell'oggetto [ECDiffieHellmanCng](assetId:///T:System.Security.Cryptography.ECDiffieHellmanCng?qualifyHint=False&autoUpgrade=True). Ma poiché non tutte le routine leggono tutte le proprietà di input, in passato era molto probabile che si creasse confusione per lo sviluppatore.  
  
 Per gestire questo aspetto in .NET Framework 4.6.2, sono stati aggiunti i tre metodi seguenti alla classe base [ECDiffieHellman](assetId:///T:System.Security.Cryptography.ECDiffieHellman?qualifyHint=False&autoUpgrade=True) per rappresentare in modo chiaro le routine di funzione di derivazione chiave e i rispettivi input:  
  
|Metodo ECDiffieHellman|Descrizione|  
|----------------------------|-----------------|  
|[DeriveKeyFromHash(ECDiffieHellmanPublicKey, HashAlgorithmName, Byte\[\], Byte\[\])](assetId:///M:System.Security.Cryptography.ECDiffieHellman.DeriveKeyFromHash(System.Security.Cryptography.ECDiffieHellmanPublicKey,System.Security.Cryptography.HashAlgorithmName,System.Byte[],System.Byte[])?qualifyHint=False&autoUpgrade=False)|Deriva il materiale della chiave usando la formula<br /><br /> HASH(secretPrepend &#124;&#124; *x* &#124;&#124; secretAppend)<br /><br /> HASH(secretPrepend OrElse *x* OrElse secretAppend)<br /><br /> dove *x* è il risultato calcolato dell'algoritmo EC Diffie-Hellman.|  
|[DeriveKeyFromHmac(ECDiffieHellmanPublicKey, HashAlgorithmName, Byte\[\], Byte\[\], Byte\[\])](assetId:///M:System.Security.Cryptography.ECDiffieHellman.DeriveKeyFromHmac(System.Security.Cryptography.ECDiffieHellmanPublicKey,System.Security.Cryptography.HashAlgorithmName,System.Byte[],System.Byte[],System.Byte[])?qualifyHint=False&autoUpgrade=False)|Deriva il materiale della chiave usando la formula<br /><br /> HMAC(hmacKey, secretPrepend &#124;&#124; *x* &#124;&#124; secretAppend)<br /><br /> HMAC(hmacKey, secretPrepend OrElse *x* OrElse secretAppend)<br /><br /> dove *x* è il risultato calcolato dell'algoritmo EC Diffie-Hellman.|  
|[DeriveKeyTls(ECDiffieHellmanPublicKey, Byte\[\], Byte\[\])](assetId:///M:System.Security.Cryptography.ECDiffieHellman.DeriveKeyTls(System.Security.Cryptography.ECDiffieHellmanPublicKey,System.Byte[],System.Byte[])?qualifyHint=False&autoUpgrade=False)|Deriva il materiale della chiave usando l'algoritmo di derivazione TLS della funzione pseudocasuale.|  
  
 **Supporto per la crittografia simmetrica con chiave persistente**  
 La libreria di crittografia di Windows (CNG) ha aggiunto il supporto per l'archiviazione delle chiavi simmetriche persistenti e l'uso delle chiavi simmetriche archiviate nell'hardware e .NET Framework 4.6.2 rende possibile l'uso di questa funzionalità da parte degli sviluppatori.  Poiché le nozioni di nome della chiave e provider di chiavi sono specifiche dell'implementazione, questa funzionalità richiede l'uso del costruttore dei tipi di implementazione concreti anziché della modalità factory preferita, ad esempio la chiamata a `Aes.Create`.  
  
 Il supporto per la crittografia simmetrica con chiave persistente esiste per gli algoritmi AES ([AesCng](assetId:///T:System.Security.Cryptography.AesCng?qualifyHint=False&autoUpgrade=True)) e 3DES ([TripleDESCng](assetId:///T:System.Security.Cryptography.TripleDESCng?qualifyHint=False&autoUpgrade=True)). Ad esempio:  
  
```csharp  
  
public static byte[] EncryptDataWithPersistedKey(byte[] data, byte[] iv)  
{  
    using (Aes aes = new AesCng("AesDemoKey", CngProvider.MicrosoftSoftwareKeyStorageProvider))  
    {  
        aes.IV = iv;  
  
        // Using the zero-argument overload is required to make use of the persisted key  
        using (ICryptoTransform encryptor = aes.CreateEncryptor())  
        {  
            if (!encryptor.CanTransformMultipleBlocks)  
            {  
                throw new InvalidOperationException("This is a sample, this case wasn’t handled...");  
            }  
  
            return encryptor.TransformFinalBlock(data, 0, data.Length);  
        }  
    }  
}  
  
```  
  
```vb  
  
Public Shared Function EncryptDataWithPersistedKey(data As Byte(), iv As Byte()) As Byte()  
    Using Aes As Aes = New AesCng("AesDemoKey", CngProvider.MicrosoftSoftwareKeyStorageProvider)  
        Aes.IV = iv  
  
        ' Using the zero-argument overload Is required to make use of the persisted key  
        Using encryptor As ICryptoTransform = Aes.CreateEncryptor()  
            If Not encryptor.CanTransformMultipleBlocks Then  
                Throw New InvalidOperationException("This is a sample, this case wasn’t handled...")  
            End If  
            Return encryptor.TransformFinalBlock(data, 0, data.Length)  
        End Using  
    End Using  
End Function  
  
```  
  
 **Supporto SignedXml per la generazione di hash SHA-2**  
 .NET Framework 4.6.2 offre il supporto per la classe [SignedXml](assetId:///T:System.Security.Cryptography.Xml.SignedXml?qualifyHint=False&autoUpgrade=True) per i metodi di firma SHA256, RSA-SHA384 e RSA-SHA512 PKCS#1 e SHA256, SHA384 e SHA512 fanno riferimento agli algoritmi con classificazione.  
  
 Le costanti URI sono tutte esposte in [SignedXml](xref:System.Security.Cryptography.Xml.SignedXml?qualifyHint=False&autoUpgrade=True):  
  
|Campo SignedXml|Costante|  
|---------------------|--------------|  
|[XmlDsigSHA256Url](assetId:///F:System.Security.Cryptography.Xml.SignedXml.XmlDsigSHA256Url?qualifyHint=False&autoUpgrade=True)|"http://www.w3.org/2001/04/xmlenc#sha256"|  
|[XmlDsigRSASHA256Url](assetId:///F:System.Security.Cryptography.Xml.SignedXml.XmlDsigRSASHA256Url?qualifyHint=False&autoUpgrade=True)|"http://www.w3.org/2001/04/xmldsig-more#rsa-sha256"|  
|[XmlDsigSHA384Url](assetId:///F:System.Security.Cryptography.Xml.SignedXml.XmlDsigSHA384Url?qualifyHint=False&autoUpgrade=True)|"http://www.w3.org/2001/04/xmldsig-more#sha384"|  
|[XmlDsigRSASHA384Url](assetId:///F:System.Security.Cryptography.Xml.SignedXml.XmlDsigRSASHA384Url?qualifyHint=False&autoUpgrade=True)|"http://www.w3.org/2001/04/xmldsig-more#rsa-sha384"|  
|[XmlDsigSHA512Url](assetId:///F:System.Security.Cryptography.Xml.SignedXml.XmlDsigSHA512Url?qualifyHint=False&autoUpgrade=True)|"http://www.w3.org/2001/04/xmlenc#sha512"|  
|[XmlDsigRSASHA512Url](assetId:///F:System.Security.Cryptography.Xml.SignedXml.XmlDsigRSASHA512Url?qualifyHint=False&autoUpgrade=True)|"http://www.w3.org/2001/04/xmldsig-more#rsa-sha512"|  
  
 Tutti i programmi che hanno registrato un gestore personalizzato [SignatureDescription](assetId:///T:System.Security.Cryptography.SignatureDescription?qualifyHint=False&autoUpgrade=True) in [CryptoConfig](assetId:///T:System.Security.Cryptography.CryptoConfig?qualifyHint=False&autoUpgrade=True) per aggiungere il supporto per questi algoritmi continueranno a funzionare come prima, ma poiché ora esistono impostazioni predefinite nella piattaforma, la registrazione di [CryptoConfig](assetId:///T:System.Security.Cryptography.CryptoConfig?qualifyHint=False&autoUpgrade=True) non è più necessaria.  
  
<a name="SQLClient"></a>   
### <a name="sqlclient"></a>SqlClient  
 Il provider di dati .NET Framework per SQL Server ([System.Data.SqlClient](assetId:///N:System.Data.SqlClient?qualifyHint=True&autoUpgrade=True)) include le nuove funzionalità seguenti in .NET Framework 4.6.2:  
  
 **Pool di connessioni e timeout con database SQL di Azure**  
 Quando il pool di connessioni è abilitato e si verifica un timeout o un altro errore di accesso, nella cache viene memorizzata un'eccezione e tale l'eccezione memorizzata nella cache viene generata per qualsiasi tentativo di connessione effettuato nei 5 secondi successivi e fino a 1 minuto.  Per altre informazioni, vedere [Pool di connessioni SQL Server (ADO.NET)](../Topic/SQL%20Server%20Connection%20Pooling%20\(ADO.NET\).md).  
  
 Questo comportamento è da evitare quando ci si connette ai database SQL di Azure, poiché i tentativi di connessione possono non riuscire per errori temporanei che in genere si risolvono rapidamente. Per ottimizzare l'esperienza dei tentativi di connessione, il comportamento del periodo di blocco del pool di connessioni viene rimosso quando le connessioni ai database SQL di Azure hanno esito negativo.  
  
 L'aggiunta della nuova parola chiave `PoolBlockingPeriod` consente di selezionare il periodo di blocco più adatto per l'applicazione. I valori includono:  
  
 `Auto`  
 Il periodo di blocco del pool di connessioni per un'applicazione che si connette a un database SQL di Azure è disabilitato e il periodo di blocco del pool di connessioni per un'applicazione che si connette a qualsiasi altra istanza di SQL Server è abilitato. Rappresenta il valore predefinito. Se il nome dell'endpoint server termina in uno dei modi seguenti, vengono considerati i database SQL di Azure:  
  
-   .database.windows.net  
  
-   .database.chinacloudapi.cn  
  
-   .database.usgovcloudapi.net  
  
-   .database.cloudapi.de  
  
 `AlwaysBlock`  
 Il periodo di blocco del pool di connessioni è sempre abilitato.  
  
 `NeverBlock`  
 Il periodo di blocco del pool di connessioni è sempre disabilitato.  
  
 **Miglioramenti per Always Encrypted**  
 SQLClient introduce due miglioramenti per Always Encrypted:  
  
-   Per migliorare le prestazioni delle query con parametri su colonne di database crittografate, i metadati di crittografia per i parametri di query ora vengono memorizzati nella cache. Se quando la proprietà [SqlConnection.ColumnEncryptionQueryMetadataCacheEnabled](assetId:///P:System.Data.SqlClient.SqlConnection.ColumnEncryptionQueryMetadataCacheEnabled?qualifyHint=True&autoUpgrade=True) è impostata su `true` (valore predefinito) viene chiamata la stessa query più volte, il client recupera i metadati dei parametri dal server solo una volta.  
  
-   Le voci delle chiavi di crittografia delle colonne nella cache delle chiavi ora vengono eliminate dopo un intervallo di tempo configurabile, impostato usando la proprietà [SqlConnection.ColumnEncryptionKeyCacheTtl](assetId:///P:System.Data.SqlClient.SqlConnection.ColumnEncryptionKeyCacheTtl?qualifyHint=True&autoUpgrade=True).  
  
<a name="WCF"></a>   
### <a name="windows-communication-foundation"></a>Windows Communication Foundation  
 In .NET Framework 4.6.2, Windows Communication Foundation è stato ottimizzato nelle aree seguenti:  
  
 **Supporto della sicurezza del trasporto WCF per certificati archiviati tramite CNG**  
 La sicurezza del trasporto WCF supporta i certificati archiviati usando la libreria di crittografia di Windows (CNG). In .NET Framework 4.6.2 questo supporto è limitato all'utilizzo dei certificati con una chiave pubblica che ha un esponente di lunghezza non superiore a 32 bit. Quando un'applicazione ha come destinazione .NET Framework 4.6.2, questa funzionalità è attivata per impostazione predefinita.  
  
 Per le applicazioni destinate a .NET Framework 4.6.1 e versioni precedenti, ma eseguite in .NET Framework 4.6.2 o versioni successive, questa funzionalità può essere abilitata aggiungendo la riga seguente alla sezione [\<runtime>](../Topic/%3Cruntime%3E%20Element.md) del file app.config o web.config.  
  
```xml  
  
<AppContextSwitchOverrides  
    value="Switch.System.ServiceModel.DisableCngCertificates=false"  
/>  
  
```  
  
 L'operazione può essere eseguita anche a livello di codice nel modo seguente:  
  
```csharp  
  
private const string DisableCngCertificates = @"Switch.System.ServiceModel.DisableCngCertificates";  
AppContext.SetSwitch(disableCngCertificates, false);  
  
```  
  
```vb  
  
Const DisableCngCertificates As String = "Switch.System.ServiceModel.DisableCngCertificates"  
AppContext.SetSwitch(disableCngCertificates, False)  
  
```  
  
 **Miglioramento del supporto per più regole di regolazione dell'ora legale tramite la classe DataContractJsonSerializer**  
 I clienti possono usare un'impostazione di configurazione dell'applicazione per determinare se la classe [DataContractJsonSerializer](assetId:///T:System.Runtime.Serialization.Json.DataContractJsonSerializer?qualifyHint=False&autoUpgrade=True) supporta più regole di regolazione per un singolo fuso orario. È una funzionalità che prevede il consenso esplicito. Per abilitarla aggiungere la seguente impostazione nel file di configurazione dell'applicazione:  
  
```xml  
  
<runtime>  
     <AppContextSwitchOverrides value="Switch.System.Runtime.Serialization.DoNotUseTimeZoneInfo=false" />  
</runtime>  
  
```  
  
 Quando questa funzionalità è abilitata, un oggetto [DataContractJsonSerializer](assetId:///T:System.Runtime.Serialization.Json.DataContractJsonSerializer?qualifyHint=False&autoUpgrade=True) usa il tipo [TimeZoneInfo](assetId:///T:System.TimeZoneInfo?qualifyHint=False&autoUpgrade=True) invece del tipo [TimeZone](assetId:///T:System.TimeZone?qualifyHint=False&autoUpgrade=True) per deserializzare i dati di data e ora. [TimeZoneInfo](assetId:///T:System.TimeZoneInfo?qualifyHint=False&autoUpgrade=True) supporta più regole di regolazione, permettendo quindi di lavorare con dati cronologici relativi al fuso orario, diversamente da [TimeZone](assetId:///T:System.TimeZone?qualifyHint=False&autoUpgrade=True).  
  
 Per altre informazioni sulla struttura di [TimeZoneInfo](assetId:///T:System.TimeZoneInfo?qualifyHint=False&autoUpgrade=True) e sulle regolazioni per il fuso orario, vedere [Panoramica sul fuso orario](../Topic/Time%20Zone%20Overview.md).  
  
 **Supporto per mantenere un'ora UTC durante la serializzazione e la deserializzazione con la classe XMLSerializer**  
 In genere, quando si usa la classe [XmlSerializer](assetId:///T:System.Xml.Serialization.XmlSerializer?qualifyHint=False&autoUpgrade=True) per serializzare un valore di [DateTime](assetId:///T:System.DateTime?qualifyHint=False&autoUpgrade=True) UTC, viene creata una stringa di tempo serializzata che mantiene la data e l'ora ma presuppone che l'ora sia locale.  Ad esempio, se si crea un'istanza di data e ora UTC chiamando il codice seguente:  
  
```csharp  
DateTime utc = new DateTime(2016, 11, 07, 3, 0, 0, DateTimeKind.Utc);  
```  
  
```vb  
Dim utc As New Date(2016, 11, 07, 3, 0, 0, DateTimeKind.Utc)  
```  
  
 il risultato è la stringa di ora serializzata "03:00:00.0000000-08:00" per un sistema otto ore indietro rispetto all'ora UTC.  E i valori serializzati vengono sempre deserializzati come valori di data e ora locali.  
  
 È possibile usare un'impostazione di configurazione dell'applicazione per determinare se [XmlSerializer](assetId:///T:System.Xml.Serialization.XmlSerializer?qualifyHint=False&autoUpgrade=True) mantiene le informazioni sul fuso orario UTC durante la serializzazione e deserializzazione dei valori di [DateTime](assetId:///T:System.DateTime?qualifyHint=False&autoUpgrade=True):  
  
```xml  
  
<runtime>  
     <AppContextSwitchOverrides   
          value="Switch.System.Runtime.Serialization.DisableSerializeUTCDateTimeToTimeAndDeserializeUTCTimeToUTCDateTime=false" />  
</runtime>  
  
```  
  
 Quando questa funzionalità è abilitata, un oggetto [DataContractJsonSerializer](assetId:///T:System.Runtime.Serialization.Json.DataContractJsonSerializer?qualifyHint=False&autoUpgrade=True) usa il tipo [TimeZoneInfo](assetId:///T:System.TimeZoneInfo?qualifyHint=False&autoUpgrade=True) invece del tipo [TimeZone](assetId:///T:System.TimeZone?qualifyHint=False&autoUpgrade=True) per deserializzare i dati di data e ora. [TimeZoneInfo](assetId:///T:System.TimeZoneInfo?qualifyHint=False&autoUpgrade=True) supporta più regole di regolazione, permettendo quindi di lavorare con dati cronologici relativi al fuso orario, diversamente da [TimeZone](assetId:///T:System.TimeZone?qualifyHint=False&autoUpgrade=True).  
  
 Per altre informazioni sulla struttura di [TimeZoneInfo](assetId:///T:System.TimeZoneInfo?qualifyHint=False&autoUpgrade=True) e sulle regolazioni per il fuso orario, vedere [Panoramica sul fuso orario](../Topic/Time%20Zone%20Overview.md).  
  
 **Ricerca più accurata con NetNamedPipeBinding**  
 WCF offre una nuova impostazione di applicazione che può essere specificata sulle applicazioni client in modo da assicurare che si connettano sempre al servizio in ascolto sull'URI che meglio corrisponde a quello richiesto. Con questa impostazione impostata su `false` (impostazione predefinita), i client che usano [NetNamedPipeBinding](assetId:///T:System.ServiceModel.NetNamedPipeBinding?qualifyHint=False&autoUpgrade=True) possono provare la connessione a un servizio in ascolto su un URI che è una sottostringa dell'URI richiesto.  
  
 Ad esempio, un client tenta di connettersi a un servizio in ascolto su `net.pipe://localhost/Service1`, ma un altro servizio in esecuzione nello stesso computer con privilegi di amministratore è in ascolto su `net.pipe://localhost`. Con l'impostazione di applicazione impostata su `false`, il client tenterebbe di connettersi al servizio errato. Dopo aver impostato l'impostazione di applicazione su `true`, il client si connetterà sempre al servizio più pertinente.  
  
> [!NOTE]
>  I client che usano [NetNamedPipeBinding](assetId:///T:System.ServiceModel.NetNamedPipeBinding?qualifyHint=False&autoUpgrade=True) trovano i servizi basati sull'indirizzo di base del servizio, se esiste, anziché sull'indirizzo completo dell'endpoint. Per assicurarsi che l'impostazione funzioni sempre, il servizio deve usare un indirizzo di base univoco.  
  
 Per abilitare questa modifica, aggiungere la seguente impostazione di applicazione al file di configurazione dell'applicazione o del Web dell'applicazione client:  
  
```xml  
  
<configuration>  
    <appSettings>  
        <add key="wcf:useBestMatchNamedPipeUri" value="true" />  
    </appSettings>  
</configuration>  
  
```  
  
 **SSL 3.0 non è un protocollo predefinito**  
 Quando si usa NetTcp con la sicurezza del trasporto e un tipo di certificato con credenziali, SSL 3.0 non è più un protocollo predefinito usato per negoziare una connessione protetta. Nella maggior parte dei casi non vi sarà alcun impatto sulle applicazioni esistenti, poiché TLS 1.0 è incluso nell'elenco di protocolli per NetTcp. Tutti i client esistenti devono essere in grado di negoziare una connessione usando almeno TLS 1.0.      Se è necessario il protocollo Ssl3, usare uno dei meccanismi di configurazione seguenti per aggiungerlo all'elenco dei protocolli negoziati.  
  
-   Proprietà [SslStreamSecurityBindingElement.SslProtocols](assetId:///P:System.ServiceModel.Channels.SslStreamSecurityBindingElement.SslProtocols?qualifyHint=True&autoUpgrade=True)  
  
-   Proprietà [TcpTransportSecurity.SslProtocols](assetId:///P:System.ServiceModel.TcpTransportSecurity.SslProtocols?qualifyHint=True&autoUpgrade=True)  
  
-   Sezione [\<transport>](../Topic/%3Ctransport%3E%20of%20%3CnetTcpBinding%3E.md) della sezione [\<netTcpBinding>](../Topic/%3CnetTcpBinding%3E.md)  
  
-   Sezione [\<sslStreamSecurity>](../Topic/%3CsslStreamSecurity%3E.md) della sezione [\<customBinding>](../Topic/%3CcustomBinding%3E.md)  
  
<a name="WPF462"></a>   
### <a name="windows-presentation-foundation-wpf"></a>Windows Presentation Foundation (WPF)  
 In .NET Framework 4.6.2, Windows Presentation Foundation è stato ottimizzato nelle aree seguenti:  
  
 **Ordinamento di gruppi**  
 Un'applicazione che usa un oggetto [CollectionView](assetId:///T:System.Windows.Data.CollectionView?qualifyHint=False&autoUpgrade=True) per raggruppare i dati ora puoi dichiarare esplicitamente in che modo ordinare i gruppi. L'ordinamento esplicito risolve il problema dell'ordinamento non intuitivo che si verifica quando un'applicazione aggiunge o rimuove in modo dinamico i gruppi o quando modifica il valore delle proprietà dell'elemento interessate dal raggruppamento. Può anche migliorare le prestazioni del processo di creazione dei gruppi spostando i confronti delle proprietà di raggruppamento dall'ordinamento della raccolta completa all'ordinamento dei gruppi.  
  
 Per supportare l'ordinamento dei gruppi, le nuove proprietà [GroupDescription.SortDescriptions](assetId:///P:System.ComponentModel.GroupDescription.SortDescriptions?qualifyHint=True&autoUpgrade=True) e [GroupDescription.CustomSort](assetId:///P:System.ComponentModel.GroupDescription.CustomSort?qualifyHint=True&autoUpgrade=True) descrivono come ordinare la raccolta di gruppi generata dall'oggetto [GroupDescription](assetId:///T:System.ComponentModel.GroupDescription?qualifyHint=False&autoUpgrade=True). Questo comportamento è analogo al modo in cui le proprietà [ListCollectionView](assetId:///T:System.Windows.Data.ListCollectionView?qualifyHint=False&autoUpgrade=True) omonime descrivono come ordinare gli elementi di dati.  
  
 Due nuove proprietà statiche della classe [PropertyGroupDescription](assetId:///T:System.Windows.Data.PropertyGroupDescription?qualifyHint=False&autoUpgrade=True), [CompareNameAscending](assetId:///P:System.Windows.Data.PropertyGroupDescription.CompareNameAscending?qualifyHint=False&autoUpgrade=True) e [CompareNameDescending](assetId:///P:System.Windows.Data.PropertyGroupDescription.CompareNameDescending?qualifyHint=False&autoUpgrade=True), possono essere usate per la maggior parte dei casi.  
  
 Ad esempio, il seguente XAML raggruppa i dati in base all'età, ordina i gruppi di età in ordine crescente e raggruppa gli elementi all'interno di ogni gruppo di età in base al cognome.  
  
```xaml  
  
<GroupDescriptions>  
     \<PropertyGroupDescription   
         PropertyName=”Age”   
         CustomSort=   
              ”{x:Static PropertyGroupDescription.CompareNamesAscending}”/>  
     </PropertyGroupDescription>  
</GroupDescriptions>  
  
<SortDescriptions>  
     \<SortDescription PropertyName=”LastName”/>  
</SortDescriptions>  
  
```  
  
 **Supporto per tastiera software**  
 Il supporto per la tastiera software consente di rilevare lo stato attivo nelle applicazioni WPF chiamando e chiudendo automaticamente la nuova tastiera software in Windows 10 quando l'input del tocco viene ricevuto da un controllo in grado di accettare input testuale.  
  
 Nelle versioni precedenti di .NET Framework, non è possibile attivare il rilevamento dello stato attivo nelle applicazioni WPF senza disabilitare il supporto WPF per il rilevamento dei movimenti di tocco e penna.  Di conseguenza, le applicazioni WPF devono scegliere tra il supporto completo WPF per il tocco e la promozione del mouse di Windows.  
  
 **DPI per monitor**  
 Per supportare la recente proliferazione di ambienti ad alta risoluzione e risoluzione ibrida per le applicazioni WPF, WPF in .NET Framework 4.6.2 abilita la sensibilità ai valori DPI del monitor. Per altre informazioni su come abilitare l'app WPF per la sensibilità ai valori DPI del monitor, vedere gli [esempi e la guida per gli sviluppatori](https://github.com/Microsoft/WPF-Samples/tree/master/PerMonitorDPI) su GitHub.  
  
 Nelle versioni precedenti di .NET Framework, le applicazioni WPF sono compatibili con i valori DPI del sistema. In altre parole, l'interfaccia utente dell'applicazione viene adeguata in modo appropriato dal sistema operativo, in base alla risoluzione del monitor in cui viene eseguito il rendering dell'applicazione. ,  
  
 Per le app eseguite in .NET Framework 4.6.2, è possibile disabilitare le modifiche dei valori DPI per monitor nelle app WPF aggiungendo un'istruzione di configurazione alla sezione [\<runtime>](../Topic/%3Cruntime%3E%20Element.md) del file di configurazione dell'applicazione in questo modo:  
  
```xml  
  
<runtime>  
   \<AppContextSwitchOverrides value=”Switch.System.Windows.DoNotScaleForDpiChanges=false”/>  
</runtime>  
  
```  
  
<a name="WF462"></a>   
### <a name="windows-workflow-foundation-wf"></a>Windows Workflow Foundation (WF)  
 In .NET Framework 4.6.2, Windows Workflow Foundation è stato ottimizzato nell'area seguente:  
  
 **Supporto per espressioni C# e IntelliSense nell'utilità di progettazione di WF rieseguita nell'host**  
 A partire da .NET Framework 4.5, WF supporta le espressioni C# sia nella progettazione di Visual Studio che nei flussi di lavoro di codice. La riallocazione della progettazione del flusso di lavoro è una funzionalità chiave di WF che consente di usare la finestra di progettazione del flusso di lavoro in un'applicazione esterna a Visual Studio, ad esempio WPF.  Windows Workflow Foundation offre la possibilità di supportare le espressioni C# e IntelliSense nell'utilità di progettazione del flusso di lavoro riallocata. Per altre informazioni, vedere il [blog di Windows Workflow Foundation](http://go.microsoft.com/fwlink/?LinkID=809042&clcid=0x409).  
  
 `Availability of IntelliSense when a customer rebuilds a workflow project from Visual Studio`  
 Nelle versioni di .NET Framework precedenti a .NET Framework 4.6.2, IntelliSense viene interrotta nella progettazione del flusso di lavoro quando un cliente ricompila un progetto di flusso di lavoro da Visual Studio. Anche se la compilazione del progetto ha esito positivo, i tipi di flusso di lavoro non vengono trovati nell'utilità di progettazione e vengono visualizzati alcuni avvisi di IntelliSense per i tipi di flusso di lavoro mancanti nella finestra **Elenco errori**. .NET Framework 4.6.2 risolve questo problema e rende disponibile IntelliSense.  
  
 **Le applicazioni flusso di lavoro versione 1 con tracciabilità del flusso di lavoro vengono ora eseguite in modalità FIPS**  
 I computer con modalità di compatibilità FIPS abilitata ora sono in grado di eseguire correttamente un'applicazione di flusso di lavoro tipo versione 1 con tracciabilità del flusso di lavoro attivata. Per abilitare questo scenario, è necessario apportare le modifiche seguenti al file di configurazione dell'applicazione:  
  
```xml  
<add key="microsoft:WorkflowRuntime:FIPSRequired" value="true" />  
```  
  
 Se questo scenario non è abilitato, eseguire l'applicazione continua a generare un'eccezione con il messaggio "Questa implementazione non fa parte degli algoritmi crittografici convalidati per Windows Platform FIPS".  
  
 **Miglioramenti apportati ai flussi di lavoro quando si usa l'aggiornamento dinamico con Progettazione flussi di lavoro di Visual Studio**  
 Progettazione flussi di lavoro, Activity Designer Flowchart e altre utilità di progettazione delle attività dei flussi di lavoro ora caricano e visualizzano correttamente i flussi di lavoro che sono stati salvati dopo la chiamata del metodo [DynamicUpdateServices.PrepareForUpdate](assetId:///M:System.Activities.DynamicUpdate.DynamicUpdateServices.PrepareForUpdate(System.Activities.Activity)?qualifyHint=True&autoUpgrade=True). Nelle versioni di .NET Framework precedenti a .NET Framework 4.6.2, il caricamento di un file XAML in Visual Studio per un flusso di lavoro salvato dopo la chiamata di [DynamicUpdateServices.PrepareForUpdate](assetId:///M:System.Activities.DynamicUpdate.DynamicUpdateServices.PrepareForUpdate(System.Activities.Activity)?qualifyHint=True&autoUpgrade=True) può causare i problemi seguenti:  
  
-   Progettazione flussi di lavoro non riesce a caricare correttamente il file XAML se [ViewStateData.Id](assetId:///P:System.Activities.Presentation.ViewState.ViewStateData.Id?qualifyHint=True&autoUpgrade=True) si trova alla fine della riga.  
  
-   ActivityDesigner Diagramma di flusso o altri ActivityDesigner del flusso di lavoro possono visualizzare tutti gli oggetti nei propri percorsi predefiniti anziché i valori della proprietà associata.  
  
<a name="ClickOnce"></a>   
### <a name="clickonce"></a>ClickOnce  
 ClickOnce è stato aggiornato per supportare TLS 1.1 e TLS 1.2 oltre al protocollo 1.0 che supporta già. ClickOnce rileva automaticamente il protocollo richiesto e non sono necessarie altre operazioni nell'applicazione ClickOnce per abilitare il supporto per TLS 1.1 e 1.2.  
  
<a name="UWPConvert"></a>   
### <a name="converting-windows-forms-and-wpf-apps-to--uwp-apps"></a>Conversione di Windows Form e applicazioni WPF in applicazioni UWP  
 Windows ora offre funzionalità che consentono di portare le applicazioni desktop Windows esistenti, incluse le applicazioni WPF e Windows Form, sulla piattaforma UWP (Universal Windows Platform). Questa tecnologia funge da ponte e consente di eseguire gradualmente la migrazione della codebase esistente a UWP, rendendo in tal modo l'applicazione disponibile in tutti i dispositivi Windows 10.  
  
 Le applicazioni desktop convertite ottengono un'identità di applicazione simile a quella delle applicazioni UWP e in questo modo le API UWP diventano accessibili per abilitare funzionalità come i riquadri animati e le notifiche. L'applicazione continua a comportarsi come in precedenza e viene eseguita come applicazione con attendibilità totale. Dopo avere convertito l'applicazione, è possibile aggiungere un processo contenitore di applicazioni al processo di attendibilità totale esistente per aggiungere un'interfaccia utente adattiva. Quando tutte le funzionalità vengono spostate nel processo contenitore di applicazioni, il processo di attendibilità totale può essere rimosso e la nuova applicazione UWP può essere resa disponibile per tutti i dispositivi Windows 10.  
  
<a name="Debug462"></a>   
### <a name="debugging-improvements"></a>Miglioramenti apportati al debug  
 L'*API di debug non gestito* è stata ottimizzata in .NET Framework 4.6.2 per l'esecuzione di un'analisi aggiuntiva quando viene generata un'eccezione [NullReferenceException](assetId:///T:System.NullReferenceException?qualifyHint=False&autoUpgrade=True), in modo che sia possibile determinare quale variabile in una singola riga di codice sorgente è `null`.   A supporto di questo scenario, le API seguenti sono state aggiunte all'API di debug non gestito.  
  
-   Interfacce [ICorDebugCode4](../Topic/ICorDebugCode4%20Interface.md), [ICorDebugVariableHome](../Topic/ICorDebugVariableHome%20Interface.md) e [ICorDebugVariableHomeEnum](../Topic/ICorDebugVariableHomeEnum%20Interface.md), che espongono le posizioni native delle variabili gestite. Questo permette ai debugger di eseguire alcune analisi del flusso di codice quando viene generata un'eccezione [NullReferenceException](assetId:///T:System.NullReferenceException?qualifyHint=False&autoUpgrade=True) e di eseguire un controllo a ritroso per determinare quale variabile gestita corrispondente alla posizione nativa è `null`.  
  
-   Il metodo [ICorDebugType2::GetTypeID](../Topic/ICorDebugType2::GetTypeID%20Method.md) fornisce un mapping per ICorDebugType a [COR_TYPEID](../Topic/COR_TYPEID%20Structure.md), che permette al debugger di ottenere un oggetto [COR_TYPEID](../Topic/COR_TYPEID%20Structure.md) senza un'istanza di ICorDebugType. È quindi possibile usare le API esistenti in [COR_TYPEID](../Topic/COR_TYPEID%20Structure.md) per determinare il layout di classe del tipo.  
  
<a name="v461"></a>   
## <a name="whats-new-in-the-net-framework-461"></a>Novità di .NET Framework 4.6.1  
 .NET Framework 4.6.1 include nuove funzionalità nelle aree seguenti:  
  
-   [Crittografia](#Crypto)  
  
-   [ADO.NET](#ADO.NET461)  
  
-   [Windows Presentation Foundation (WPF)](#WPF461)  
  
-   [Windows Workflow Foundation](#WWF461)  
  
-   [Profilatura](#Profile461)  
  
-   [NGen](#NGEN461)  
  
 Per altre informazioni su .NET Framework 4.6.1, vedere gli argomenti seguenti:  
  
-   [Elenco delle modifiche di .NET Framework 4.6.1](http://go.microsoft.com/fwlink/?LinkId=622964)  
  
-   [Compatibilità delle applicazioni nella versione 4.6.1](../Topic/Application%20Compatibility%20in%20the%20.NET%20Framework%204.6.1.md)  
  
-   [Differenze nell'API di .NET Framework](http://go.microsoft.com/fwlink/?LinkId=622989) (su GitHub)  
  
<a name="Crypto"></a>   
### <a name="cryptography-support-for-x509-certificates-containing-ecdsa"></a>Crittografia: supporto di certificati X509 contenenti ECDSA  
 In .NET Framework 4.6 è stato aggiunto il supporto RSACng per i certificati X509. .NET Framework 4.6.1 aggiunge il supporto di certificati X509 con ECDSA (Elliptic Curve Digital Signature Algorithm).  
  
 Offrendo prestazioni migliori e trattandosi di un algoritmo di crittografia più sicuro rispetto a RSA, ECDSA rappresenta un'ottima scelta per ambienti in cui la scalabilità e le prestazioni TLS (Transport Layer Security) sono fattori importanti. L'implementazione di .NET Framework esegue il wrapping delle chiamate nelle funzionalità di Windows esistenti.  
  
 L'esempio di codice seguente illustra quanto sia semplice generare una firma per un flusso di byte usando il nuovo supporto dei certificati X509 ECDSA incluso in .NET Framework 4.6.1.  
  
<!-- TODO: review snippet reference  [!CODE [whatsnew.461.crypto#1](../CodeSnippet/VS_Snippets_CLR/whatsnew.461.crypto#1)]  -->  
  
 Emerge una netta differenza rispetto al codice necessario per generare una firma in .NET Framework 4.6.  
  
<!-- TODO: review snippet reference  [!CODE [whatsnew.461.crypto#2](../CodeSnippet/VS_Snippets_CLR/whatsnew.461.crypto#2)]  -->  
  
<a name="ADO.NET461"></a>   
### ADO.NET In ADO.NET è stato aggiunto quanto segue:  
  
 Supporto di Crittografia sempre attiva per le chiavi hardware protette  
 ADO.NET ora supporta l'archiviazione nativa delle chiavi master di colonna con Crittografia sempre attiva nei moduli di protezione hardware. Grazie a questo supporto, i clienti possono usare le chiavi asimmetriche archiviate nei moduli di protezione hardware senza dover scrivere provider dell'archivio chiavi master di colonna personalizzati e senza doverli registrare nelle applicazioni.  
  
 I clienti devono installare il provider CSP fornito dal fornitore dei moduli di protezione hardware o i provider dell'archivio chiavi CNG nei server applicazioni o nei computer client per accedere ai dati con Crittografia sempre attiva protetti con le chiavi master di colonna archiviate in un modulo di protezione hardware.  
  
 Miglioramento del comportamento di connessione [MultiSubnetFailover](assetId:///P:System.Data.SqlClient.SqlConnectionStringBuilder.MultiSubnetFailover?qualifyHint=False&autoUpgrade=True) per AlwaysOn  
 SqlClient ora fornisce automaticamente una connessione più veloce a un gruppo di disponibilità AlwaysOn. Rileva in modo trasparente se l'applicazione si connette a un gruppo di disponibilità AlwaysOn su una subnet diversa e individua rapidamente il server attivo corrente e gli fornisce una connessione. Prima di questa versione, un'applicazione doveva impostare la stringa di connessione in modo da includere `“MultisubnetFailover=true”` per indicare che era connessa a un gruppo di disponibilità AlwaysOn. Senza impostare la parola chiave di connessione su `true`, potrebbe verificarsi un timeout durante la connessione di un'applicazione a un gruppo di disponibilità AlwaysOn. In questa versione *non* è più necessario che un'applicazione imposti [MultiSubnetFailover](assetId:///P:System.Data.SqlClient.SqlConnectionStringBuilder.MultiSubnetFailover?qualifyHint=False&autoUpgrade=True) su `true`. Per altre informazioni sul supporto SqlClient per gruppi di disponibilità Always On, vedere [Supporto SqlClient per disponibilità elevata, ripristino di emergenza](../Topic/SqlClient%20Support%20for%20High%20Availability,%20Disaster%20Recovery.md).  
  
<a name="WPF461"></a>   
### <a name="windows-presentation-foundation-wpf"></a>Windows Presentation Foundation (WPF)  
 Windows Presentation Foundation include molti miglioramenti e cambiamenti.  
  
 Miglioramento delle prestazioni  
 Il ritardo di attivazione degli eventi tocco è stato risolto in .NET Framework 4.6.1. Inoltre, l'inserimento di un controllo [RichTextBox](assetId:///T:System.Windows.Controls.RichTextBox?qualifyHint=False&autoUpgrade=True) non blocca più il thread di rendering durante l'input veloce.  
  
 Miglioramenti di controllo ortografico  
 Il controllo ortografico in WPF è stato aggiornato in Windows 8.1 e versioni successive per sfruttare il supporto di altre lingue per il controllo ortografico offerto dal sistema operativo.  La funzionalità non è stata modificata nelle versioni di Windows precedenti a Windows 8.1.  
  
 Come nelle versioni precedenti di .NET Framework, la lingua per un controllo [TextBox](assetId:///T:System.Windows.Controls.TextBox?qualifyHint=False&autoUpgrade=True) o un blocco [RichTextBox](assetId:///T:System.Windows.Controls.RichTextBox?qualifyHint=False&autoUpgrade=True) viene rilevata cercando le informazioni nell'ordine seguente:  
  
-   `xml:lang`, se presente.  
  
-   Lingua di input corrente.  
  
-   Impostazioni cultura del thread corrente.  
  
 Per altre informazioni sul supporto delle lingue in WPF, vedere il [post di blog di WPF sulle funzionalità di .NET Framework 4.6.1](http://go.microsoft.com/fwlink/?LinkID=691819).  
  
 Supporto aggiuntivo per i dizionari personalizzati per utente  
 In .NET Framework 4.6.1, WPF riconosce i dizionari personalizzati che sono registrati a livello globale. Questa funzionalità si aggiunge alla possibilità di registrarli a livello di controllo.  
  
 Nelle versioni precedenti di WPF, i dizionari personalizzati non riconoscono le parole escluse e gli elenchi di correzione automatica. Sono supportati in Windows 8.1 e Windows 10 mediante l'uso di file che possono essere inseriti nella directory `%AppData%\Microsoft\Spelling\<language tag>`.  A questi file si applicano le regole seguenti:  
  
-   I file devono avere estensione dic (per le parole aggiunte), exc (per le parole escluse) o acl (per la correzione automatica).  
  
-   I file devono essere in testo normale UTF-16 LE che inizia con l'indicatore dell'ordine dei byte (BOM, Byte Order Mark).  
  
-   Ogni riga deve essere costituita da una parola (negli elenchi di parole aggiunte ed escluse) o da una coppia di correzione automatica con le parole separate da una barra verticale ("&#124;") (nell'elenco di parole della correzione automatica).  
  
-   Questi file sono considerati di sola lettura e non vengono modificati dal sistema.  
  
> [!NOTE]
>  Questi nuovi formati di file non sono supportati direttamente dalle API di controllo ortografico WPF e i dizionari personalizzati forniti a WPF nelle applicazioni devono continuare a usare i file con estensione lex.  
  
 Esempi  
 In MSDN sono disponibili diversi [esempi di WPF](https://msdn.microsoft.com/library/ms771633.aspx). Più di 200 degli esempi più comuni (in base all'utilizzo) verranno spostati in un [archivio GitHub open source](https://github.com/Microsoft/WPF-Samples). Per aiutare Microsoft a migliorare gli esempi, inviare una richiesta di pull o segnalare un [problema di GitHub](https://github.com/Microsoft/WPF-Samples/issues).  
  
 Estensioni DirectX  
 WPF include un [pacchetto NuGet](http://go.microsoft.com/fwlink/?LinkID=691342) che offre nuove implementazioni di [D3DImage](assetId:///T:System.Windows.Interop.D3DImage?qualifyHint=False&autoUpgrade=True) che semplificano l'interazione con il contenuto DX10 e Dx11. Il codice per questo pacchetto è stato reso open source ed è disponibile su [GitHub](https://github.com/Microsoft/WPFDXInterop).  
  
<a name="WWF461"></a>   
### <a name="windows-workflow-foundation-transactions"></a>Windows Workflow Foundation: Transazioni  
 Il metodo [Transaction.EnlistPromotableSinglePhase](assetId:///Overload:System.Transactions.Transaction.EnlistPromotableSinglePhase?qualifyHint=True&autoUpgrade=True) ora può usare un gestore di transazioni distribuite diverso da MSDTC per alzare di livello la transazione. A questo scopo, specificare l'identificatore di un promotore di transazione GUID per il nuovo overload [Transaction.EnlistPromotableSinglePhase(IPromotableSinglePhaseNotification, Guid)](assetId:///M:System.Transactions.Transaction.EnlistPromotableSinglePhase(System.Transactions.IPromotableSinglePhaseNotification,System.Guid)?qualifyHint=True&autoUpgrade=False). Se l'operazione riesce, le funzionalità della transazione sono soggette a limitazioni. Quando viene integrato un promotore di transazione non MSDTC, i metodi seguenti generano un'eccezione [TransactionPromotionException](assetId:///T:System.Transactions.TransactionPromotionException?qualifyHint=False&autoUpgrade=True), perché questi metodi richiedono l'innalzamento di livello a MSDTC:  
  
-   [Transaction.EnlistDurable](assetId:///Overload:System.Transactions.Transaction.EnlistDurable?qualifyHint=True&autoUpgrade=True)  
  
-   [TransactionInterop.GetDtcTransaction](assetId:///M:System.Transactions.TransactionInterop.GetDtcTransaction(System.Transactions.Transaction)?qualifyHint=True&autoUpgrade=True)  
  
-   [TransactionInterop.GetExportCookie](assetId:///M:System.Transactions.TransactionInterop.GetExportCookie(System.Transactions.Transaction,System.Byte[])?qualifyHint=True&autoUpgrade=True)  
  
-   [TransactionInterop.GetTransmitterPropagationToken](assetId:///M:System.Transactions.TransactionInterop.GetTransmitterPropagationToken(System.Transactions.Transaction)?qualifyHint=True&autoUpgrade=True)  
  
 Quando viene integrato un promotore di transazione non MSDTC, occorre usarlo per le future integrazioni durevoli usando i protocolli che definisce. L'oggetto [Guid](assetId:///T:System.Guid?qualifyHint=False&autoUpgrade=True) del promotore di transazione può essere ottenuto mediante la proprietà [PromoterType](assetId:///P:System.Transactions.Transaction.PromoterType?qualifyHint=False&autoUpgrade=True). Quando la transazione viene alzata di livello, il promotore di transazione fornisce una matrice [Byte](assetId:///T:System.Byte?qualifyHint=False&autoUpgrade=True) che rappresenta il token alzato di livello. Un'applicazione può ottenere il token alzato di livello per una transazione non MSDTC alzata di livello con il metodo [GetPromotedToken](assetId:///M:System.Transactions.Transaction.GetPromotedToken?qualifyHint=False&autoUpgrade=True).  
  
 Gli utenti del nuovo overload [Transaction.EnlistPromotableSinglePhase(IPromotableSinglePhaseNotification, Guid)](assetId:///M:System.Transactions.Transaction.EnlistPromotableSinglePhase(System.Transactions.IPromotableSinglePhaseNotification,System.Guid)?qualifyHint=True&autoUpgrade=False) devono seguire una sequenza di chiamata specifica perché l'operazione di promozione venga eseguita correttamente. Queste regole sono descritte nella documentazione relativa al metodo.  
  
<a name="Profile461"></a>   
### <a name="profiling"></a>Profilatura  
 L'API di profilatura non gestita è stata migliorata nel modo seguente:  
  
 Supporto migliorato per l'accesso ai PDB nell'interfaccia [ICorProfilerInfo7](../Topic/ICorProfilerInfo7%20Interface.md)  
 In ASP.Net 5 è sempre più comune che gli assembly vengano compilati in memoria mediante Roslyn. Per gli sviluppatori che creano strumenti di profilatura, ciò significa che i PDB che in passato erano serializzati sul disco potrebbero non essere più presenti. Gli strumenti profiler spesso usano PDB per rimappare il codice alle righe di origine per attività come il code coverage o l'analisi delle prestazioni riga per riga. L'interfaccia [ICorProfilerInfo7](../Topic/ICorProfilerInfo7%20Interface.md) include ora due nuovi metodi, [ICorProfilerInfo7::GetInMemorySymbolsLength](../Topic/ICorProfilerInfo7::GetInMemorySymbolsLength%20Method.md) e [ICorProfilerInfo7::ReadInMemorySymbols](../Topic/ICorProfilerInfo7::ReadInMemorySymbols.md), per fornire a questi strumenti profiler l'accesso ai dati dei PDB in memoria. Usando le nuove API, un profiler può ottenere il contenuto di un PDB in memoria come matrice di byte e quindi elaborarlo o serializzarlo su disco.  
  
 Strumentazione migliore con l'interfaccia ICorProfiler  
 I profiler che usano la funzionalità ReJit dell'API `ICorProfiler` per la strumentazione dinamica ora possibile modificare alcuni metadati. In precedenza quegli strumenti potevano instrumentare IL in qualsiasi momento, ma i metadati potevano essere modificati solo in fase di caricamento del modulo. Poiché IL fa riferimento ai metadati, questo limitava i tipi di strumentazione possibile. Alcuni di questi limiti sono stati innalzati aggiungendo il metodo [ICorProfilerInfo7::ApplyMetaData](../Topic/ICorProfilerInfo7::ApplyMetaData%20Method.md) per supportare un subset di modifiche ai metadati dopo il caricamento del modulo, in particolare aggiungendo nuovi record `AssemblyRef`, `TypeRef`, `TypeSpec`, `MemberRef`, `MemberSpec` e `UserString`. Questa modifica rende possibile una gamma più ampia di strumentazioni immediate.  
  
<a name="NGEN461"></a>   
### <a name="native-image-generator-ngen-pdbs"></a>PDB del generatore di immagini native (NGEN)  
 La traccia eventi tra computer consente ai clienti di profilare un programma sul Computer A e osservare i dati di profilatura con mapping della riga di origine sul Computer B. Nelle versioni precedenti di .NET Framework, l'utente copiava tutti i moduli e le immagini native dalla macchina profilata alla macchina di analisi contenente il PDB IL per creare il mapping sorgente-nativo. Anche se questo processo può funzionare bene quando i file sono relativamente piccoli, ad esempio per le applicazioni telefoniche, i file possono avere dimensioni molto grandi sui sistemi desktop e la copia può richiedere molto tempo.  
  
 Con i PDB Ngen, NGen può creare un PDB che contiene il mapping da IL a nativo senza una dipendenza dal PDB IL. In questo scenario di traccia eventi in più computer, è sufficiente copiare il PDB di immagine nativa generato dal Computer A nel Computer B e usare le [API di accesso all'interfaccia di debug](https://docs.microsoft.com/en-us/visualstudio/debugger/debug-interface-access/debug-interface-access-sdk-reference) per leggere il mapping da codice sorgente a codice IL del PDB IL e il mapping da codice IL a codice nativo del PDB di immagine nativa. La combinazione di entrambi i mapping fornisce un mapping da codice sorgente a codice nativo. Poiché il PDB di immagine nativa è molto più piccolo rispetto a tutti i moduli e alle immagini native, il processo di copia dal Computer A al Computer B è molto più veloce.  
  
<a name="v46"></a>   
## <a name="whats-new-in-net-2015"></a>Novità di .NET 2015  
 .NET 2015 introduce .NET Framework 4.6 e .NET Core. Alcune nuove funzionalità sono valide per entrambi, mentre altre sono specifiche di .NET Framework 4.6 o .NET Core.  
  
-   **ASP.NET 5**  
  
     .NET 2015 include ASP.NET 5, una piattaforma .NET snella per la compilazione di app moderne basate su cloud. Si tratta di una piattaforma modulare che consente di includere solo le funzionalità necessarie nell'applicazione. Può essere ospitata su IIS o in modo indipendente in un processo personalizzato ed è possibile eseguire app con diverse versioni di .NET Framework nello stesso server. Include un nuovo sistema di configurazione dell'ambiente progettato per la distribuzione cloud.  
  
     MVC, API Web e pagine Web sono riunite in un unico framework denominato MVC 6. Le app ASP.NET 5 vengono compilate mediante i nuovi strumenti in Visual Studio 2015. Le applicazioni esistenti funzioneranno nel nuovo .NET Framework ma per compilare un'app che usa MVC 6 o SignalR 3 è necessario usare il sistema di progetto in Visual Studio 2015.  
  
     Per informazioni, vedere [ASP.NET 5](http://go.microsoft.com/fwlink/?LinkId=518238).  
  
-   **Aggiornamenti di ASP.NET**  
  
    -   **API basata su attività per lo scaricamento asincrono delle risposte**  
  
         ASP.NET ora fornisce [HttpResponse.FlushAsync](assetId:///M:System.Web.HttpResponse.FlushAsync?qualifyHint=True&autoUpgrade=True),, una semplice API basata sulle attività che consente di scaricare le risposte asincrone con il supporto `async/await` del linguaggio usato.  
  
    -   `Model binding supports task-returning methods`  
  
         In .NET Framework 4.5, ASP.NET ha aggiunto la funzionalità di associazione di modelli che ha reso possibile un approccio estendibile, focalizzato sul codice, per le operazioni di dati basate su CRUD nelle pagine Web Form e nei controlli utente. Il sistema di associazione di modelli ora supporta metodi di associazione di modelli con restituzione di [attività](assetId:///T:System.Threading.Tasks.Task?qualifyHint=False&autoUpgrade=True). Questa funzionalità consente agli sviluppatori di Web Form di ottenere i vantaggi di scalabilità di async con la facilità del sistema di associazione dati quando usano versioni più recenti di ORM, tra cui Entity Framework.  
  
         L'associazione di modelli async è controllata dall'impostazione di configurazione `aspnet:EnableAsyncModelBinding`.  
  
        ```  
  
        <appSettings>  
           <add key=" aspnet:EnableAsyncModelBinding" value="true|false" />  
        </appSettings>  
  
        ```  
  
         Per le app destinate a .NET Framework 4.6, l'impostazione predefinita è `true`. Per le app in esecuzione su .NET Framework 4.6 e che sono destinate a una versione precedente di .NET Framework, è `false` per impostazione predefinita. Può essere abilitata impostando l'impostazione di configurazione su `true`.  
  
    -   **Supporto HTTP/2 (Windows 10)**  
  
         [HTTP/2](http://www.wikipedia.org/wiki/HTTP/2) è una nuova versione del protocollo HTTP che permette un utilizzo molto migliore della connessione, con meno round trip tra client e server, offrendo una latenza minore per il caricamento delle pagine Web per gli utenti.  Le pagine Web (a differenza dei servizi) traggono maggiori vantaggi dal protocollo HTTP/2, poiché ottimizza più elementi richiesti come parte di un'esperienza unica. Il supporto HTTP/2 è stato aggiunto ad ASP.NET in .NET Framework 4.6. Poiché la funzionalità di rete esiste a più livelli, si sono rese necessarie nuove funzionalità in Windows, IIS e ASP.NET per abilitare HTTP/2. È necessario eseguire Windows 10 per usare HTTP/2 con ASP.NET.  
  
         HTTP/2 è anche supportato e attivato per impostazione predefinita per le app di Windows 10 Universal Windows Platform (UWP) che usano l'API [System.Net.Http.HttpClient](assetId:///T:System.Net.Http.HttpClient?qualifyHint=True&autoUpgrade=True).  
  
         Per consentire l'uso della funzionalità [PUSH_PROMISE](http://http2.github.io/http2-spec/#PUSH_PROMISE) nelle applicazioni ASP.NET, è stato aggiunto un nuovo metodo con due overload, [PushPromise(String)](assetId:///M:System.Web.HttpResponse.PushPromise(System.String)?qualifyHint=False&autoUpgrade=False) e [PushPromise(String, String, NameValueCollection)](assetId:///M:System.Web.HttpResponse.PushPromise(System.String,System.String,System.Collections.Specialized.NameValueCollection)?qualifyHint=False&autoUpgrade=False), alla classe [HttpResponse](assetId:///T:System.Web.HttpResponse?qualifyHint=False&autoUpgrade=True).  
  
        > [!NOTE]
        >  Mentre ASP.NET 5 supporta HTTP/2, il supporto della funzionalità PUSH PROMISE non è ancora stato aggiunto.  
  
         Il browser e il server Web (IIS su Windows) eseguono tutte le operazioni. Gli utenti non dovranno eseguire alcuna operazione impegnativa.  
  
         Poiché la maggior parte dei [principali browser supporta HTTP/2](http://www.wikipedia.org/wiki/HTTP/2), è probabile che gli utenti trarranno vantaggio dal supporto HTTP/2, se supportato dal server in uso.  
  
    -   **Supporto per Token Binding Protocol**  
  
         Microsoft e Google stanno collaborando a un nuovo approccio all'autenticazione, chiamato [Token Binding Protocol](https://github.com/TokenBinding/Internet-Drafts). Il presupposto è che i token di autenticazione (nella cache del browser) possono essere rubati e usati da utenti malintenzionati per accedere a risorse altrimenti sicure, ad esempio un conto bancario, senza richiedere la password o altre informazioni riservate. L'obiettivo del nuovo protocollo è attenuare questo problema.  
  
         Il Token Binding Protocol verrà implementato in Windows 10 come funzionalità del browser. Le app ASP.NET parteciperanno al protocollo, in modo che sia convalidata la legittimità dei token di autenticazione. Le implementazioni di client e server stabiliscono la protezione end-to-end specificata dal protocollo.  
  
    -   **Algoritmi hash casuali per le stringhe**  
  
         In .NET Framework 4.5 è stato introdotto un [algoritmo hash casuale per le stringhe](https://msdn.microsoft.com/library/jj152924.aspx). Tuttavia, non era supportato da ASP.NET perché alcune funzionalità ASP.NET dipendevano da un codice hash stabile. In .NET Framework 4.6 gli algoritmi di hash della stringa casuale sono ora supportati. Per abilitare questa funzionalità, usare l'impostazione di configurazione `aspnet:UseRandomizedStringHashAlgorithm`.  
  
        ```  
  
        <appSettings>  
           <add key="aspnet:UseRandomizedStringHashAlgorithm" value="true|false" />  
        </appSettings>  
  
        ```  
  
-   **ADO.NET**  
  
     ADO .NET supporta ora la funzionalità Crittografia sempre attiva disponibile in SQL Server 2016 Community Technology Preview 2 (CTP2). Con Crittografia sempre attiva, SQL Server può eseguire operazioni su dati crittografati e, soprattutto, la chiave di crittografia risiede con l'applicazione all'interno dell'ambiente attendibile del cliente e non sul server. Crittografia sempre attiva protegge i dati dei clienti in modo che gli amministratori di database non abbiano accesso ai dati di testo normale. La crittografia e la decrittografia dei dati avvengono in modo trasparente a livello di driver, riducendo al minimo le modifiche che è necessario apportare alle applicazioni esistenti. Per informazioni dettagliate, vedere [Crittografia sempre attiva (motore di database)](https://msdn.microsoft.com/library/mt163865\(v=sql.130\).aspx) e [Crittografia sempre attiva (sviluppo client)](https://msdn.microsoft.com/library/mt147923\(v=sql.130\).aspx).  
  
-   **Compilatore JIT a 64 bit per il codice gestito**  
  
     .NET Framework 4.6 presenta una nuova versione del compilatore JIT a 64 bit (il cui nome in codice iniziale era RyuJIT). Il nuovo compilatore a 64 bit offre miglioramenti significativi delle prestazioni rispetto al compilatore JIT a 64 bit esistente. Il nuovo compilatore a 64 bit è abilitato per i processi a 64 bit in esecuzione su NET Framework 4.6. L'app verrà eseguita in un processo a 64 bit se è compilata come 64 bit o AnyCPU e se viene eseguita su un sistema operativo a 64 bit. Nonostante si sia cercato di rendere il più possibile trasparente la transizione al nuovo compilatore, potrebbero verificarsi cambiamenti del comportamento. Microsoft è interessata a conoscere i commenti diretti degli utenti sugli eventuali problemi riscontrati durante l'uso del nuovo compilatore JIT. In caso di problemi che potrebbero essere correlati al nuovo compilatore JIT a 64 bit, contattare Microsoft tramite [Microsoft Connect](http://connect.microsoft.com/).  
  
     Il nuovo compilatore JIT a 64 bit include anche funzionalità di accelerazione SIMD hardware quando è associato a tipi abilitati per SIMD nello spazio dei nomi [System.Numerics](assetId:///N:System.Numerics?qualifyHint=False&autoUpgrade=True), con notevoli miglioramenti in termini di prestazioni.  
  
-   **Miglioramenti apportati al caricatore di assembly**  
  
     Il caricatore di assembly usa la memoria in modo più efficiente scaricando gli assembly IL dopo il caricamento di un'immagine NGEN corrispondente. Questa modifica riduce la memoria virtuale, aspetto particolarmente utile per app a 32 bit di grandi dimensioni (ad esempio Visual Studio) e consente anche di risparmiare memoria fisica.  
  
-   **Modifiche apportate alla libreria di classi base**  
  
     Sono state aggiunte molte nuove API a .NET Framework 4.6 per abilitare gli scenari principali. Sono incluse le modifiche e le aggiunte seguenti:  
  
    -   Implementazioni **IReadOnlyCollection\<T>**  
  
         Altre raccolte implementano [IReadOnlyCollection\<T>](assetId:///T:System.Collections.Generic.IReadOnlyCollection`1?qualifyHint=False&autoUpgrade=True) , ad esempio [Queue<T\> ](assetId:///T:System.Collections.Generic.Queue`1?qualifyHint=False&autoUpgrade=True) e [Stack\<T>](assetId:///T:System.Collections.Generic.Stack`1?qualifyHint=False&autoUpgrade=True).  
  
    -   **CultureInfo.CurrentCulture e CultureInfo.CurrentUICulture**  
  
         Le proprietà [CultureInfo.CurrentCulture](assetId:///P:System.Globalization.CultureInfo.CurrentCulture?qualifyHint=True&autoUpgrade=True) e [CultureInfo.CurrentUICulture](assetId:///P:System.Globalization.CultureInfo.CurrentUICulture?qualifyHint=True&autoUpgrade=True) sono ora di lettura/scrittura anziché di sola lettura. Se si assegna un nuovo oggetto [CultureInfo](assetId:///T:System.Globalization.CultureInfo?qualifyHint=False&autoUpgrade=True) queste proprietà, cambiano anche le impostazioni cultura del thread corrente definite dalla proprietà `Thread.CurrentThread.CurrentCulture` e le impostazioni cultura del thread UI corrente definite dalle proprietà `Thread.CurrentThread.CurrentUICulture`.  
  
    -   **Miglioramenti apportati a Garbage Collection (GC)**  
  
         La classe [GC](assetId:///T:System.GC?qualifyHint=False&autoUpgrade=True) ora include i metodi [TryStartNoGCRegion](assetId:///M:System.GC.TryStartNoGCRegion(System.Int64)?qualifyHint=False&autoUpgrade=True) e [EndNoGCRegion](assetId:///M:System.GC.EndNoGCRegion?qualifyHint=False&autoUpgrade=True) che consentono di disabilitare le operazioni di Garbage Collection durante l'esecuzione di un percorso critico.  
  
         Un nuovo overload del metodo [GC.Collect(Int32, GCCollectionMode, Boolean, Boolean)](assetId:///M:System.GC.Collect(System.Int32,System.GCCollectionMode,System.Boolean,System.Boolean)?qualifyHint=True&autoUpgrade=False) consente di controllare se l'heap oggetti piccoli e l'heap oggetti grandi vengono entrambi sottoposti a sweep e compattati o solo sottoposti a sweep.  
  
    -   **Tipi abilitati per SIMD**  
  
         Lo spazio dei nomi [System.Numerics](assetId:///N:System.Numerics?qualifyHint=False&autoUpgrade=True) ora include una serie di tipi abilitati per SIMD, ad esempio [Matrix3x2](assetId:///T:System.Numerics.Matrix3x2?qualifyHint=False&autoUpgrade=True), [Matrix4x4](assetId:///T:System.Numerics.Matrix4x4?qualifyHint=False&autoUpgrade=True), [Plane](assetId:///T:System.Numerics.Plane?qualifyHint=False&autoUpgrade=True), [Quaternion](assetId:///T:System.Numerics.Quaternion?qualifyHint=False&autoUpgrade=True), [Vector2](assetId:///T:System.Numerics.Vector2?qualifyHint=False&autoUpgrade=True), [Vector3](assetId:///T:System.Numerics.Vector3?qualifyHint=False&autoUpgrade=True) e [Vector4](assetId:///T:System.Numerics.Vector4?qualifyHint=False&autoUpgrade=True).  
  
         Il nuovo compilatore JIT a 64 bit include anche funzionalità di accelerazione SIMD hardware, quindi le prestazioni migliorano notevolmente quando si usano i tipi abilitati per SIMD con il nuovo compilatore JIT a 64 bit.  
  
    -   **Aggiornamenti della crittografia**  
  
         L'API [System.Security.Cryptography](assetId:///N:System.Security.Cryptography?qualifyHint=True&autoUpgrade=True) è stata aggiornata per supportare le [API di crittografia CNG Windows](https://msdn.microsoft.com/library/windows/desktop/aa376214.aspx). Le versioni precedenti di .NET Framework si basavano interamente su una [versione precedente delle API di crittografia Windows](https://msdn.microsoft.com/library/windows/desktop/aa380255.aspx) per l'implementazione di [System.Security.Cryptography](assetId:///N:System.Security.Cryptography?qualifyHint=True&autoUpgrade=True). Microsoft ha ricevuto alcune richieste relative all'aggiunta del supporto per l'API CNG, perché questa supporta [algoritmi di crittografia moderni](https://msdn.microsoft.com/library/windows/desktop/bb204775.aspx#suite_b_support), che sono importanti per determinate categorie di app.  
  
         .NET Framework 4.6 include i nuovi miglioramenti seguenti per supportare le API di crittografia di CNG di Windows:  
  
        -   Un set di metodi di estensione per certificati X509, `System.Security.Cryptography.X509Certificates.RSACertificateExtensions.GetRSAPublicKey(System.Security.Cryptography.X509Certificates.X509Certificate2)` e `System.Security.Cryptography.X509Certificates.RSACertificateExtensions.GetRSAPrivateKey(System.Security.Cryptography.X509Certificates.X509Certificate2)`, che restituiscono, quando possibile, un'implementazione basata su CNG invece di un'implementazione basata su CAPI. Ad esempio, alcune smart card richiedono comunque CAPI e le API gestiscono il fallback.  
  
        -   Classe [System.Security.Cryptography.RSACng](assetId:///T:System.Security.Cryptography.RSACng?qualifyHint=True&autoUpgrade=True), che fornisce un'implementazione CNG dell'algoritmo RSA.  
  
        -   Miglioramenti all'API RSA in modo che le azioni comuni non richiedano più il cast. Ad esempio, la crittografia dei dati eseguita con un oggetto [X509Certificate2](assetId:///T:System.Security.Cryptography.X509Certificates.X509Certificate2?qualifyHint=False&autoUpgrade=True) richiede codice simile al seguente nelle versioni precedenti di .NET Framework.  
  
<!-- TODO: review snippet reference              [!CODE [WhatsNew.Casting#1](../CodeSnippet/VS_Snippets_CLR/whatsnew.casting#1)]  -->  
  
             Code that uses the new cryptography APIs in the .NET Framework 4.6 can be rewritten as follows to avoid the cast.  
  
<!-- TODO: review snippet reference              [!CODE [WhatsNew.Casting#2](../CodeSnippet/VS_Snippets_CLR/whatsnew.casting#2)]  -->  
  
    -   **Supporto per la conversione di date e ore da o verso l'ora di Unix**  
  
         Sono stati aggiunti i nuovi metodi seguenti alla struttura [DateTimeOffset](assetId:///T:System.DateTimeOffset?qualifyHint=False&autoUpgrade=True) per supportare la conversione di valori di data e ora da o verso l'ora di Unix:  
  
        -   [DateTimeOffset.FromUnixTimeSeconds](assetId:///M:System.DateTimeOffset.FromUnixTimeSeconds(System.Int64)?qualifyHint=True&autoUpgrade=True)  
  
        -   [DateTimeOffset.FromUnixTimeMilliseconds](assetId:///M:System.DateTimeOffset.FromUnixTimeMilliseconds(System.Int64)?qualifyHint=True&autoUpgrade=True)  
  
        -   [DateTimeOffset.ToUnixTimeSeconds](assetId:///M:System.DateTimeOffset.ToUnixTimeSeconds?qualifyHint=True&autoUpgrade=True)  
  
        -   [DateTimeOffset.ToUnixTimeMilliseconds](assetId:///M:System.DateTimeOffset.ToUnixTimeMilliseconds?qualifyHint=True&autoUpgrade=True)  
  
    -   **Opzioni di compatibilità**  
  
         La nuova classe [AppContext](assetId:///T:System.AppContext?qualifyHint=False&autoUpgrade=True) aggiunge una nuova funzione di compatibilità che consente agli autori di librerie di fornire agli utenti un meccanismo uniforme per la rinuncia esplicita alla nuova funzionalità, che stabilisce un contratto a regime di controllo libero ("loosely-coupled") tra componenti per poter comunicare una richiesta di rinuncia esplicita. Questa funzionalità è importante in genere quando viene apportata una modifica alle funzionalità esistenti. Al contrario, esiste già un consenso esplicito per la nuova funzionalità.  
  
         Con [AppContext](assetId:///T:System.AppContext?qualifyHint=False&autoUpgrade=True), le librerie definiscono ed espongono opzioni di compatibilità, mentre il codice che dipende dalle librerie può impostare queste opzioni in modo da influire sul comportamento delle librerie. Per impostazione predefinita, le librerie forniscono la nuova funzionalità e la modificano (cioè offrono la funzionalità precedente) solo se l'opzione è impostata.  
  
         Un'applicazione (o una libreria) può dichiarare il valore di un'opzione (che è sempre un valore [booleano](assetId:///T:System.Boolean?qualifyHint=False&autoUpgrade=True)) definito da una libreria dipendente. L'opzione è sempre implicitamente `false`. Impostare l'opzione su `true` la abilita. Impostare in modo esplicito l'opzione su `false` fornisce il nuovo comportamento.  
  
        ```csharp  
        AppContext.SetSwitch("Switch.AmazingLib.ThrowOnException", true);  
        ```  
  
         La libreria deve controllare se un consumer è dichiarato il valore dell'opzione e si comporta in modo appropriato in base ad essa.  
  
        ```  
  
        if (!AppContext.TryGetSwitch("Switch.AmazingLib.ThrowOnException", out shouldThrow))   
        {  
           // This is the case where the switch value was not set by the application.   
           // The library can choose to get the value of shouldThrow by other means.   
           // If no overrides nor default values are specified, the value should be 'false'.   
           // A false value implies the latest behavior.  
        }  
  
           // The library can use the value of shouldThrow to throw exceptions or not.  
           if (shouldThrow)   
           {  
              // old code  
           }  
           else {  
              // new code  
           }  
        }  
  
        ```  
  
         È opportuno usare un formato coerente per le opzioni, poiché si tratta di un contratto formale esposto da una libreria. Di seguito sono riportati due formati ovvi.  
  
        -   *Opzione*.*spaziodeinomi*.*nomeopzione*  
  
        -   *Opzione*.*libreria*.*nomeopzione*  
  
    -   **Modifiche apportate al modello asincrono basato su attività**  
  
         Per le app per .NET Framework 4.6, gli oggetti [Task](assetId:///T:System.Threading.Tasks.Task?qualifyHint=False&autoUpgrade=True) e [Task\<TResult>](assetId:///T:System.Threading.Tasks.Task`1?qualifyHint=False&autoUpgrade=True) ereditano le impostazioni cultura e le impostazioni cultura dell'interfaccia utente del thread chiamante. Questo non incide sul comportamento delle app per versioni precedenti di .NET Framework o non destinate a una versione specifica di .NET Framework. Per altre informazioni, vedere la sezione dedicata alle impostazioni cultura e alle operazioni asincrone basate su attività nell'argomento relativo alla classe [CultureInfo](assetId:///T:System.Globalization.CultureInfo?qualifyHint=False&autoUpgrade=True).  
  
         La classe [System.Threading.AsyncLocal\<T>](assetId:///T:System.Threading.AsyncLocal`1?qualifyHint=True&autoUpgrade=True) consente di rappresentare i dati di ambiente locali rispetto a un flusso di controllo asincrono specificato, ad esempio un metodo `async`. Può essere usato per rendere persistenti i dati tra thread. È anche possibile definire un metodo di callback che riceve una notifica ogni volta che i dati di ambiente subiscono una modifica perché la proprietà [AsyncLocal<T\>.Value](assetId:///P:System.Threading.AsyncLocal`1.Value?qualifyHint=True&autoUpgrade=True) è stata modificata in modo esplicito oppure perché il thread ha rilevato una transizione di contesto.  
  
         Tre metodi pratici, [Task.CompletedTask](assetId:///P:System.Threading.Tasks.Task.CompletedTask?qualifyHint=True&autoUpgrade=True), [Task.FromCanceled](assetId:///M:System.Threading.Tasks.Task.FromCanceled(System.Threading.CancellationToken)?qualifyHint=True&autoUpgrade=True) e [Task.FromException](assetId:///M:System.Threading.Tasks.Task.FromException(System.Exception)?qualifyHint=True&autoUpgrade=True), sono stati aggiunti al modello asincrono basato su attività (TAP) per restituire le attività completate in un determinato stato.  
  
         La classe [NamedPipeClientStream](assetId:///T:System.IO.Pipes.NamedPipeClientStream?qualifyHint=False&autoUpgrade=True) ora supporta la comunicazione asincrona con il nuovo [ConnectAsync](assetId:///M:System.IO.Pipes.NamedPipeClientStream.ConnectAsync?qualifyHint=False&autoUpgrade=True). ProcessOnStatus.  
  
    -   **EventSource supporta ora la scrittura nel registro eventi**  
  
         Ora è possibile usare la classe [EventSource](assetId:///T:System.Diagnostics.Tracing.EventSource?qualifyHint=False&autoUpgrade=True) per registrare messaggi amministrativi o operativi nel registro eventi, oltre a tutte le sessioni ETW create nel computer. In passato era necessario usare il pacchetto Microsoft.Diagnostics.Tracing.EventSource NuGet per questa funzionalità. Questa funzionalità è ora integrata in .NET Framework 4.6.  
  
         Sia il pacchetto NuGet sia .NET Framework 4.6 sono stati aggiornati con le funzionalità seguenti:  
  
        -   **Eventi dinamici**  
  
             Consente eventi definiti al momento senza creare metodi di eventi.  
  
        -   **Payload avanzati**  
  
             Consente di passare classi e matrici attribuite in modo specifico nonché tipi primitivi come un payload  
  
        -   **Rilevamento attività**  
  
             Comporta l'applicazione di tag di eventi tra gli eventi Start e Stop con un ID che rappresenta tutte le attività attualmente attive.  
  
         Per supportare queste funzionalità, il metodo [Write](assetId:///M:System.Diagnostics.Tracing.EventSource.Write(System.String)?qualifyHint=False&autoUpgrade=True) di overload è stato aggiunto alla classe [EventSource](assetId:///T:System.Diagnostics.Tracing.EventSource?qualifyHint=False&autoUpgrade=True).  
  
-   **Windows Presentation Foundation (WPF)**  
  
    -   **Miglioramenti apportati a HDPI**  
  
         Il supporto di HDPI in WPF è stato migliorato in .NET Framework 4.6. Sono state apportate modifiche all'arrotondamento del layout per ridurre le istanze di ritaglio nei controlli con bordi. Per impostazione predefinita, questa funzionalità è abilitata solo se [TargetFrameworkAttribute](assetId:///T:System.Runtime.Versioning.TargetFrameworkAttribute?qualifyHint=False&autoUpgrade=True) è impostato su .NET 4.6.  Le applicazioni destinate alle versioni precedenti del framework, ma eseguite in .NET Framework 4.6, possono scegliere il nuovo comportamento aggiungendo la riga seguente alla sezione [\<runtime>](../Topic/%3Cruntime%3E%20Element.md) del file app.config:  
  
        ```  
  
        <AppContextSwitchOverrides  
        value="Switch.MS.Internal.DoNotApplyLayoutRoundingToMarginsAndBorderThickness=false"  
        />  
  
        ```  
  
         Le finestre WPF che si estendono su più monitor con impostazioni DPI diverse (configurazione di più DPI) sono ora visualizzate completamente senza aree nere. È possibile rifiutare esplicitamente questo comportamento disabilitandolo con l'aggiunta della riga seguente alla sezione `<appSettings>` del file di configurazione dell'app:  
  
        ```  
  
        <add key="EnableMultiMonitorDisplayClipping" value="true"/>  
  
        ```  
  
         È stato aggiunto a [System.Windows.Input.Cursor](assetId:///T:System.Windows.Input.Cursor?qualifyHint=True&autoUpgrade=True) il supporto per il caricamento automatico del cursore appropriato in base all'impostazione DPI.  
  
    -   **Miglioramento della funzionalità touch**  
  
         I clienti hanno segnalato su [Connect](https://connect.microsoft.com/VisualStudio/feedback/details/903760/) che il comportamento imprevedibile della funzionalità touch è stato risolto in .NET Framework 4.6. La soglia relativa al doppio tocco per le app di Windows Store e le applicazioni WPF ora è lo stesso in Windows 8.1 e versioni successive.  
  
    -   **Supporto per finestre figlio trasparenti**  
  
         WPF in .NET Framework 4.6 supporta le finestre figlio trasparenti in Windows 8.1 e versioni successive. Ciò consente di creare finestre figlio non rettangolari e trasparenti nelle finestre di primo livello. È possibile abilitare questa funzionalità impostando la proprietà [HwndSourceParameters.UsesPerPixelTransparency](assetId:///P:System.Windows.Interop.HwndSourceParameters.UsesPerPixelTransparency?qualifyHint=True&autoUpgrade=True) su `true`.  
  
-   **Windows Communication Foundation (WCF)**  
  
    -   **Supporto di SSL**  
  
         WCF ora supporta la versione SSL TLS 1.1 e TLS 1.2, oltre a SSL 3.0 e TLS 1.0, quando si usa NetTcp con la sicurezza del trasporto e l'autenticazione client. Ora è possibile selezionare il protocollo da usare o disabilitare i protocolli precedenti, che sono meno sicuri. A tale scopo, è possibile impostare la proprietà [SslProtocols](assetId:///P:System.ServiceModel.TcpTransportSecurity.SslProtocols?qualifyHint=False&autoUpgrade=True) o aggiungere il codice seguente a un file di configurazione.  
  
        ```  
        <netTcpBinding>  
           <binding>  
              <security mode= "None|Transport|Message|TransportWithMessageCredential" >  
                 <transport clientCredentialType="None|Windows|Certificate"  
                            protectionLevel="None|Sign|EncryptAndSign"  
                            sslProtocols="Ssl3|Tls1|Tls11|Tls12">  
                    </transport>  
              </security>  
           </binding>  
        </netTcpBinding>  
  
        ```  
  
    -   **Invio di messaggi tramite connessioni HTTP diverse**  
  
         WCF ora consente agli utenti di garantire l'invio di determinati messaggi usando diverse connessioni HTTP sottostanti. Questo risultato può essere raggiunto in due modi:  
  
        -   **Uso di un prefisso del nome del gruppo di connessione**  
  
             Gli utenti possono specificare una stringa che WCF userà per ottenere un prefisso per il nome del gruppo di connessione. Due messaggi con prefissi diversi vengono inviati usando diverse connessioni HTTP sottostanti. Per impostare il prefisso, aggiungere una coppia chiave/valore alla proprietà [Message.Properties](assetId:///P:System.ServiceModel.Channels.Message.Properties?qualifyHint=True&autoUpgrade=True) del messaggio. La chiave è "HttpTransportConnectionGroupNamePrefix", mentre il valore è il prefisso desiderato.  
  
        -   **Uso di channel factory diverse**  
  
             Gli utenti possono anche attivare una funzionalità che assicura che i messaggi inviati con i canali creati da channel factory diverse useranno connessioni HTTP sottostanti diverse. Per abilitare questa funzionalità, gli utenti devono impostare `appSetting` su `true`:  
  
            ```  
  
            <appSettings>  
               <add key="wcf:httpTransportBinding:useUniqueConnectionPoolPerFactory" value="true" />  
            </appSettings>  
  
            ```  
  
-   **Windows Workflow Foundation (WWF)**  
  
     Ora è possibile specificare il numero di secondi che un servizio del flusso di lavoro attenderà per una richiesta di operazione non ordinata quando esiste un segnalibro "non protocollo" in attesa prima del timeout della richiesta. Un segnalibro "non protocollo" è un segnalibro che non è correlato alle attività di ricezione in attesa. Alcune attività creano segnalibri non protocollo all'interno della propria implementazione, quindi potrebbe non essere evidente che un segnalibro non protocollo esista. Sono incluse le attività relative allo stato e alla selezione. Pertanto, se si ha un servizio del flusso di lavoro implementato con una macchina a stati o contenente un'attività di selezione, probabilmente si avranno segnalibri non protocollo. Specificare l'intervallo aggiungendo una riga simile alla seguente alla sezione `appSettings` del file di configurazione dell'app:  
  
    ```  
    <add key="microsoft:WorkflowServices:FilterResumeTimeoutInSeconds" value="60"/>  
    ```  
  
     Il valore predefinito è 60 secondi. Se `value` è impostato su 0, le richieste non ordinate vengono immediatamente rifiutate con un messaggio di errore simile al seguente:  
  
    ```Output  
    Operation 'Request3|{http://tempuri.org/}IService' on service instance with identifier '2b0667b6-09c8-4093-9d02-f6c67d534292' cannot be performed at this time. Please ensure that the operations are performed in the correct order and that the binding in use provides ordered delivery guarantees.   
    ```  
  
     Si tratta dello stesso messaggio che viene visualizzato se si riceve un messaggio di operazione non ordinato e non sono presenti segnalibri non protocollo.  
  
     Se il valore dell'elemento `FilterResumeTimeoutInSeconds` è diverso da zero, sono presenti segnalibri non protocollo, l'intervallo di timeout scade e l'operazione ha esito negativo con un messaggio di timeout.  
  
-   **Transazioni**  
  
     Ora è possibile includere l'identificatore di transazione distribuita per la transazione che ha generato un'eccezione derivata da [TransactionException](assetId:///T:System.Transactions.TransactionException?qualifyHint=False&autoUpgrade=True). A questo scopo, aggiungere la chiave seguente alla sezione `appSettings` del file di configurazione dell'app:  
  
    ```  
    <add key="Transactions:IncludeDistributedTransactionIdInExceptionMessage" value="true"/>   
    ```  
  
     Il valore predefinito è `false`.  
  
-   **Rete**  
  
    -   **Riutilizzo di socket**  
  
         Windows 10 include un nuovo algoritmo di rete ad alta scalabilità che consente di migliorare l'uso delle risorse del computer riutilizzando porte locali per le connessioni TCP in uscita. .NET Framework 4.6 supporta il nuovo algoritmo, consentendo alle app .NET di sfruttare il nuovo comportamento. Nelle versioni precedenti di Windows era presente un limite di connessioni simultanee artificiali (in genere 16.384, la dimensione predefinita dell'intervallo di porte dinamiche), che poteva limitare la scalabilità di un servizio causando l'esaurimento delle porte quando sono sotto carico.  
  
         In .NET Framework 4.6 sono state aggiunte due nuove API per consentire il riutilizzo delle porte, che rimuove in modo efficace il limite di 64.000 sulle connessioni simultanee:  
  
        -   Valore di enumerazione [SocketOptionName.ReuseUnicastPort](assetId:///T:System.Net.Sockets.SocketOptionName?qualifyHint=True&autoUpgrade=True).  
  
        -   Proprietà [ServicePointManager.ReusePort](assetId:///P:System.Net.ServicePointManager.ReusePort?qualifyHint=True&autoUpgrade=True).  
  
         Per impostazione predefinita, la proprietà [ServicePointManager.ReusePort](assetId:///P:System.Net.ServicePointManager.ReusePort?qualifyHint=True&autoUpgrade=True) è `false`, a meno che il valore `HWRPortReuseOnSocketBind` della chiave del registro di sistema `HKLM\SOFTWARE\Microsoft\.NETFramework\v4.0.30319` sia impostato su 0x1. Per abilitare il riutilizzo delle porte locali su connessioni HTTP, impostare la proprietà [ServicePointManager.ReusePort](assetId:///P:System.Net.ServicePointManager.ReusePort?qualifyHint=True&autoUpgrade=True) su `true`. In questo modo tutte le connessioni socket TCP in uscita da [HttpClient](assetId:///T:System.Net.Http.HttpClient?qualifyHint=False&autoUpgrade=True) e [HttpWebRequest](assetId:///T:System.Net.HttpWebRequest?qualifyHint=False&autoUpgrade=True) usano la nuova opzione di socket di Windows 10, [SO_REUSE_UNICASTPORT](https://msdn.microsoft.com/library/windows/desktop/ms740532.aspx), che consente il riutilizzo delle porte locali.  
  
         Gli sviluppatori che scrivono un'applicazione solo socket possono specificare l'opzione [SocketOptionName.ReuseUnicastPort](assetId:///T:System.Net.Sockets.SocketOptionName?qualifyHint=True&autoUpgrade=True) quando si chiama un metodo come [Socket.SetSocketOption](assetId:///M:System.Net.Sockets.Socket.SetSocketOption(System.Net.Sockets.SocketOptionLevel,System.Net.Sockets.SocketOptionName,System.Byte[])?qualifyHint=True&autoUpgrade=True) in modo che i socket in uscita riutilizzino le porte locali durante l'associazione.  
  
    -   **Supporto di nomi di dominio internazionali e di PunyCode**  
  
         Una nuova proprietà, [IdnHost](assetId:///P:System.Uri.IdnHost?qualifyHint=False&autoUpgrade=True), è stata aggiunta alla classe [Uri](assetId:///T:System.Uri?qualifyHint=False&autoUpgrade=True) per migliorare il supporto dei nomi di dominio internazionali e di PunyCode.  
  
-   **Ridimensionamento nei controlli Windows Form**  
  
     Questa funzionalità è stata estesa in .NET Framework 4.6 in modo da includere i tipi [DomainUpDown](assetId:///T:System.Windows.Forms.DomainUpDown?qualifyHint=False&autoUpgrade=True), [NumericUpDown](assetId:///T:System.Windows.Forms.NumericUpDown?qualifyHint=False&autoUpgrade=True), [DataGridViewComboBoxColumn](assetId:///T:System.Windows.Forms.DataGridViewComboBoxColumn?qualifyHint=False&autoUpgrade=True), [DataGridViewColumn](assetId:///T:System.Windows.Forms.DataGridViewColumn?qualifyHint=False&autoUpgrade=True) e [ToolStripSplitButton](assetId:///T:System.Windows.Forms.ToolStripSplitButton?qualifyHint=False&autoUpgrade=True) e il rettangolo specificato dalla proprietà [Bounds](assetId:///P:System.Drawing.Design.PaintValueEventArgs.Bounds?qualifyHint=False&autoUpgrade=True) usata per disegnare un [UITypeEditor](assetId:///T:System.Drawing.Design.UITypeEditor?qualifyHint=False&autoUpgrade=True).  
  
     È una funzionalità che prevede il consenso esplicito. Per attivarla, impostare l'elemento `EnableWindowsFormsHighDpiAutoResizing` su `true` nel file di configurazione dell'applicazione (app.config):  
  
    ```  
  
    <appSettings>  
       <add key="EnableWindowsFormsHighDpiAutoResizing" value="true" />  
    </appSettings>  
  
    ```  
  
-   **Supporto per le codifiche della tabella codici**  
  
     .NET Core supporta principalmente le codifiche Unicode e per impostazione predefinita offre un supporto limitato per le codifiche della tabella codici. È possibile aggiungere supporto per le codifiche della tabella codici disponibili in .NET Framework ma che non sono supportate in .NET Core registrando tali codifiche con il metodo [Encoding.RegisterProvider](assetId:///M:System.Text.Encoding.RegisterProvider(System.Text.EncodingProvider)?qualifyHint=True&autoUpgrade=True). Per altre informazioni, vedere la documentazione relativa alla classe [System.Text.CodePagesEncodingProvider](xref:System.Text.CodePagesEncodingProvider).  
  
-   **.NET Native**  
  
     Le app di Windows per Windows 10 destinate a .NET Core e scritte in C# o Visual Basic ora possono avvalersi di una nuova tecnologia che compila le app in codice nativo anziché IL. Producono app caratterizzate da maggiore rapidità di avvio ed esecuzione. Per altre informazioni, vedere [Compilazione di app con .NET Native](../Topic/Compiling%20Apps%20with%20.NET%20Native.md). Per una panoramica di .NET Native che esamina le differenze rispetto alla compilazione JIT e NGEN e descrive tutti i vantaggi per il codice, vedere [Compilazione e .NET Native](../Topic/.NET%20Native%20and%20Compilation.md).  
  
     Le app vengono compilate in codice nativo per impostazione predefinita quando si compilano con Visual Studio 2015. Per altre informazioni, vedere [Introduzione a .NET Native](../Topic/Getting%20Started%20with%20.NET%20Native.md).  
  
     Per supportare il debug di app .NET Native, è stata aggiunta una serie di nuove interfacce ed enumerazioni all'API di debug non gestito. Per altre informazioni, vedere l'argomento [Debug (riferimenti alle API non gestite)](../Topic/Debugging%20\(Unmanaged%20API%20Reference\).md).  
  
-   **Pacchetti .NET Framework open source**  
  
     I pacchetti .NET Core come le raccolte non modificabili, le [API SIMD](http://go.microsoft.com/fwlink/?LinkID=518639) e le API di rete come quelle incluse nello spazio dei nomi [System.Net.Http](assetId:///N:System.Net.Http?qualifyHint=False&autoUpgrade=True) sono ora disponibili come pacchetti open source su [GitHub](https://github.com/). Per accedere al codice, vedere [NetFx su GitHub](http://go.microsoft.com/fwlink/?LinkID=518634). Per altre informazioni e indicazioni su come contribuire a questi pacchetti, vedere [Componenti di base e open source di .NET](../Topic/.NET%20Core%20and%20Open-Source.md) e la [home page di .NET su GitHub](http://go.microsoft.com/fwlink/?LinkID=518635).  
  
 [Torna all'inizio](#introduction)  
  
<a name="v452"></a>   
## <a name="whats-new-in-the-net-framework-452"></a>Novità di .NET Framework 4.5.2  
  
-   **Nuove API per app ASP.NET** I nuovi metodi [HttpResponse.AddOnSendingHeaders](assetId:///M:System.Web.HttpResponse.AddOnSendingHeaders(System.Action{System.Web.HttpContext})?qualifyHint=True&autoUpgrade=True) e [HttpResponseBase.AddOnSendingHeaders](assetId:///M:System.Web.HttpResponseBase.AddOnSendingHeaders(System.Action{System.Web.HttpContextBase})?qualifyHint=True&autoUpgrade=True) permettono di esaminare e modificare le intestazioni della risposta e il codice di stato quando la risposta viene scaricata nell'app client. Provare a usare questi metodi invece degli eventi [PreSendRequestHeaders](assetId:///E:System.Web.HttpApplication.PreSendRequestHeaders?qualifyHint=False&autoUpgrade=True) e [PreSendRequestContent](assetId:///E:System.Web.HttpApplication.PreSendRequestContent?qualifyHint=False&autoUpgrade=True), perché sono più efficienti e affidabili.  
  
     Il metodo [HostingEnvironment.QueueBackgroundWorkItem](assetId:///M:System.Web.Hosting.HostingEnvironment.QueueBackgroundWorkItem(System.Action{System.Threading.CancellationToken})?qualifyHint=True&autoUpgrade=True) permette di pianificare piccoli elementi di lavoro in background. ASP.NET tiene traccia di questi elementi e impedisce a IIS di chiudere improvvisamente il processo di lavoro finché non saranno stati completati tutti gli elementi di lavoro in background. Non è possibile chiamare questo metodo all'esterno del dominio dell'app gestita di ASP.NET.  
  
     Le nuove proprietà [HttpResponse.HeadersWritten](assetId:///P:System.Web.HttpResponse.HeadersWritten?qualifyHint=True&autoUpgrade=False) e [HttpResponseBase.HeadersWritten](assetId:///P:System.Web.HttpResponseBase.HeadersWritten?qualifyHint=True&autoUpgrade=False)> restituiscono valori booleani che indicano se le intestazioni della risposta sono state scritte. È possibile usare queste proprietà per accertarsi che le chiamate alle API come [HttpResponse.StatusCode](assetId:///P:System.Web.HttpResponse.StatusCode?qualifyHint=True&autoUpgrade=True) (che genera eccezioni se le intestazioni sono state scritte) abbiano esito positivo.  
  
-   **Ridimensionamento nei controlli Windows Form** Questa funzionalità è stata ampliata. È ora possibile usare l'impostazione DPI di sistema per ridimensionare i componenti dei seguenti controlli aggiuntivi (ad esempio, la freccia a discesa nelle caselle combinate):  
  
     [ComboBox](assetId:///T:System.Windows.Forms.ComboBox?qualifyHint=False&autoUpgrade=True)   
     [ToolStripComboBox](assetId:///T:System.Windows.Forms.ToolStripComboBox?qualifyHint=False&autoUpgrade=True)   
     [ToolStripMenuItem](assetId:///T:System.Windows.Forms.ToolStripMenuItem?qualifyHint=False&autoUpgrade=True)   
     [Cursor](assetId:///T:System.Windows.Forms.Cursor?qualifyHint=False&autoUpgrade=True)   
     [DataGridView](assetId:///T:System.Windows.Forms.DataGridView?qualifyHint=False&autoUpgrade=True)   
     [DataGridViewComboBoxColumn](assetId:///T:System.Windows.Forms.DataGridViewComboBoxColumn?qualifyHint=False&autoUpgrade=True)  
  
     È una funzionalità che prevede il consenso esplicito. Per attivarla, impostare l'elemento `EnableWindowsFormsHighDpiAutoResizing` su `true` nel file di configurazione dell'applicazione (app.config):  
  
    ```  
    <appSettings>  
       <add key="EnableWindowsFormsHighDpiAutoResizing" value="true" />  
    </appSettings>  
    ```  
  
-   **Nuova funzionalità per il flusso di lavoro** Un gestore di risorse che usa il metodo [EnlistPromotableSinglePhase](assetId:///M:System.Transactions.Transaction.EnlistPromotableSinglePhase(System.Transactions.IPromotableSinglePhaseNotification)?qualifyHint=False&autoUpgrade=True) e di conseguenza implementa l'interfaccia [IPromotableSinglePhaseNotification](assetId:///T:System.Transactions.IPromotableSinglePhaseNotification?qualifyHint=False&autoUpgrade=True), può usare il nuovo metodo [Transaction.PromoteAndEnlistDurable](assetId:///M:System.Transactions.Transaction.PromoteAndEnlistDurable(System.Guid,System.Transactions.IPromotableSinglePhaseNotification,System.Transactions.ISinglePhaseNotification,System.Transactions.EnlistmentOptions)?qualifyHint=True&autoUpgrade=True) per richiedere le operazioni seguenti:  
  
    -   Promuova la transazione in transazione MSDTC (Microsoft Distributed Transaction Coordinator).  
  
    -   Sostituzione di [IPromotableSinglePhaseNotification](assetId:///T:System.Transactions.IPromotableSinglePhaseNotification?qualifyHint=False&autoUpgrade=True) con un oggetto [ISinglePhaseNotification](assetId:///T:System.Transactions.ISinglePhaseNotification?qualifyHint=False&autoUpgrade=True), che è un'integrazione durevole che supporta commit a fase singola.  
  
     È possibile eseguire questa operazione nello stesso dominio dell'app; inoltre, non è necessario altro codice non gestito che interagisca con MSDTC per eseguire la promozione. Il nuovo metodo può essere chiamato solo in presenza di una chiamata in attesa da [System.Transactions](assetId:///N:System.Transactions?qualifyHint=True&autoUpgrade=True) al metodo [IPromotableSinglePhaseNotification](assetId:///T:System.Transactions.IPromotableSinglePhaseNotification?qualifyHint=False&autoUpgrade=True)`Promote` implementato dall'integrazione promuovibile.  
  
-   **Miglioramenti apportati alla profilatura** Le seguenti nuove API di profilatura non gestite offrono funzioni di profilatura più solide:  
  
     [Struttura COR_PRF_ASSEMBLY_REFERENCE_INFO](../Topic/COR_PRF_ASSEMBLY_REFERENCE_INFO%20Structure.md)   
     [Enumerazione COR_PRF_HIGH_MONITOR](../Topic/COR_PRF_HIGH_MONITOR%20Enumeration.md)   
     [Metodo GetAssemblyReferences](../Topic/ICorProfilerCallback6::GetAssemblyReferences%20Method.md)   
     [Metodo GetEventMask2](../Topic/ICorProfilerInfo5::GetEventMask2%20Method.md)   
     [Metodo SetEventMask2](../Topic/ICorProfilerInfo5::SetEventMask2%20Method.md)   
     [Metodo AddAssemblyReference](../Topic/ICorProfilerAssemblyReferenceProvider::AddAssemblyReference%20Method.md)  
  
     Le precedenti implementazioni di `ICorProfiler` supportavano il caricamento differito degli assembly dipendenti. Le nuove API di profilatura richiedono assembly dipendenti inseriti dal profiler per il caricamento immediato, invece di essere caricato dopo la completa inizializzazione dell'app. Questa modifica non incide sugli utenti delle API `ICorProfiler` esistenti.  
  
-   **Miglioramenti apportati al debug** Le seguenti nuove API di debug non gestite offrono una migliore integrazione con un profiler. È ora possibile accedere ai metadati inseriti dal profiler oltre alle variabili e al codice locali prodotti dalle richieste ReJIT del compilatore durante il debug di dump.  
  
     [Metodo SetWriteableMetadataUpdateMode](../Topic/ICorDebugProcess7::SetWriteableMetadataUpdateMode%20Method.md)   
     [Metodo EnumerateLocalVariablesEx](../Topic/ICorDebugILFrame4::EnumerateLocalVariablesEx%20Method.md)   
     [Metodo GetLocalVariableEx](../Topic/ICorDebugILFrame4::GetLocalVariableEx%20Method.md)   
     [Metodo GetCodeEx](../Topic/ICorDebugILFrame4::GetCodeEx%20Method.md)   
     [Metodo GetActiveReJitRequestILCode](../Topic/ICorDebugFunction3::GetActiveReJitRequestILCode%20Method.md)   
     [Metodo GetInstrumentedILMap](../Topic/ICorDebugILCode2::GetInstrumentedILMap%20Method.md)  
  
-   **Modifiche apportate alla traccia eventi** .NET Framework 4.5.2 consente di eseguire attività out-of-process basate su Event Tracing for Windows (ETW) per una superficie maggiore. Ciò consente ai fornitori di Advanced Power Management (APM) di offrire strumenti semplici che tengono accuratamente traccia dei costi delle singole richieste e attività cross-thread.  Questi eventi vengono generati solo quando sono abilitati dai controller ETW; di conseguenza, le modifiche non influiscono sul codice ETW scritto in precedenza oppure sul codice eseguito con ETW disattivato.  
  
-   **Promozione di una transazione e relativa conversione in integrazione durevole**  
  
     [Transaction.PromoteAndEnlistDurable](assetId:///M:System.Transactions.Transaction.PromoteAndEnlistDurable(System.Guid,System.Transactions.IPromotableSinglePhaseNotification,System.Transactions.ISinglePhaseNotification,System.Transactions.EnlistmentOptions)?qualifyHint=True&autoUpgrade=True) è una nuova API aggiunta a .NET Framework 4.5.2 e 4.6:  
  
    ```  
  
    [System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name = "FullTrust")]  
    public Enlistment PromoteAndEnlistDurable(Guid resourceManagerIdentifier,  
                                              IPromotableSinglePhaseNotification promotableNotification,  
                                              ISinglePhaseNotification enlistmentNotification,  
                                              EnlistmentOptions enlistmentOptions)  
  
    ```  
  
     Il metodo può essere usato da un'integrazione precedentemente creata da [Transaction.EnlistPromotableSinglePhase](assetId:///M:System.Transactions.Transaction.EnlistPromotableSinglePhase(System.Transactions.IPromotableSinglePhaseNotification)?qualifyHint=True&autoUpgrade=True) in risposta al metodo [ITransactionPromoter.Promote](assetId:///M:System.Transactions.ITransactionPromoter.Promote?qualifyHint=True&autoUpgrade=True). Chiede a `System.Transactions` di alzare la transazione al livello di transazione MSDTC e di "convertire" l'elenco promuovibile in un elenco durevole. Dopo il completamento di questo metodo, l'interfaccia [IPromotableSinglePhaseNotification](assetId:///T:System.Transactions.IPromotableSinglePhaseNotification?qualifyHint=False&autoUpgrade=True) non sarà più usata come riferimento da `System.Transactions` e tutte le eventuali notifiche passeranno all'interfaccia [ISinglePhaseNotification](assetId:///T:System.Transactions.ISinglePhaseNotification?qualifyHint=False&autoUpgrade=True) specificata. L'elenco in questione deve agire come un elenco durevole, supportando la registrazione e il ripristino delle transazioni. Per informazioni dettagliate, vedere [Transaction.EnlistDurable](assetId:///M:System.Transactions.Transaction.EnlistDurable(System.Guid,System.Transactions.IEnlistmentNotification,System.Transactions.EnlistmentOptions)?qualifyHint=True&autoUpgrade=True). L'integrazione deve anche supportare [ISinglePhaseNotification](assetId:///T:System.Transactions.ISinglePhaseNotification?qualifyHint=False&autoUpgrade=True).  Questo metodo può essere chiamato *solo* durante l'elaborazione di una chiamata [ITransactionPromoter.Promote](assetId:///M:System.Transactions.ITransactionPromoter.Promote?qualifyHint=True&autoUpgrade=True). In caso contrario, verrà generata un'eccezione [TransactionException](assetId:///T:System.Transactions.TransactionException?qualifyHint=False&autoUpgrade=True).  
  
 [Torna all'inizio](#introduction)  
  
<a name="v451"></a>   
## <a name="whats-new-in-the-net-framework-451"></a>Novità di .NET Framework 4.5.1  
 **Aggiornamenti di aprile 2014**:  
  
-   [Visual Studio 2013 Update 2](http://go.microsoft.com/fwlink/p/?LinkId=393658) include alcuni aggiornamenti ai modelli di libreria di classi portabile per supportare questi scenari:  
  
    -   È possibile usare le API di Windows Runtime in librerie portabili destinate a Windows 8.1, Windows Phone 8.1 e Windows Phone Silverlight 8.1.  
  
    -   È possibile includere XAML (tipi Windows.UI.XAML) nelle librerie portabili quando la destinazione è Windows 8.1 o Windows Phone 8.1. Sono supportati i modelli XAML seguenti: Pagina vuota, Dizionario risorse, Controllo basato su modelli e Controllo utente.  
  
    -   È possibile creare una componente Windows Runtime portabile (.winmd file) da usare in app di Windows Store destinate a Windows 8.1 e Windows Phone 8.1.  
  
    -   È possibile cambiare associazione a una libreria di classi Windows Store o Windows Phone Store come una Libreria di classi portabile.  
  
     Per altre informazioni su queste modifiche, vedere [Libreria di classi portabile](../Topic/Cross-Platform%20Development%20with%20the%20Portable%20Class%20Library.md).  
  
-   Il set di contenuti di .NET Framework ora include la documentazione relativa a .NET Native, una tecnologia di precompilazione per la creazione e la distribuzione di app di Windows. .NET Native compila le app direttamente in codice nativo piuttosto che in linguaggio intermedio (IL), per ottenere migliori prestazioni. Per informazioni dettagliate, vedere [Compilazione di app con .NET Native](../Topic/Compiling%20Apps%20with%20.NET%20Native.md).  
  
-   [Reference Source per .NET Framework](http://referencesource.microsoft.com/) offre una nuova esperienza di esplorazione e funzionalità migliorate. È ora possibile esplorare il codice sorgente di .NET Framework online, [scaricare i riferimenti](http://referencesource.microsoft.com/download.html) per la visualizzazione offline ed eseguire le origini (inclusi aggiornamenti e patch) durante il debug. Per altre informazioni, vedere il post di blog relativo al [nuovo aspetto di Reference Source per .NET](http://blogs.msdn.com/b/dotnet/archive/2014/02/24/a-new-look-for-net-reference-source.aspx).  
  
 Le nuove funzionalità e i miglioramenti principali in .NET Framework 4.5.1 includono:  
  
-   Reindirizzamento di associazione automatico per assembly. A partire da Visual Studio 2013, quando si compila un'app destinata a .NET Framework 4.5.1, è possibile aggiungere reindirizzamenti di associazione al file di configurazione dell'app se quest'ultima o i relativi componenti fanno riferimento a più versioni dello stesso assembly. È inoltre possibile abilitare questa funzionalità per i progetti destinati a versioni precedenti di .NET Framework. Per altre informazioni, vedere [Procedura: abilitare e disabilitare il reindirizzamento di associazione automatico](../Topic/How%20to:%20Enable%20and%20Disable%20Automatic%20Binding%20Redirection.md).  
  
-   Possibilità di raccogliere informazioni di diagnostica che consentono agli sviluppatori di migliorare le prestazioni delle applicazioni server e cloud. Per altre informazioni, vedere i metodi [WriteEventWithRelatedActivityId](assetId:///M:System.Diagnostics.Tracing.EventSource.WriteEventWithRelatedActivityId(System.Int32,System.Guid,System.Object[])?qualifyHint=False&autoUpgrade=True) e [WriteEventWithRelatedActivityIdCore](assetId:///M:System.Diagnostics.Tracing.EventSource.WriteEventWithRelatedActivityIdCore(System.Int32,System.Guid*,System.Int32,System.Diagnostics.Tracing.EventSource.EventData*)?qualifyHint=False&autoUpgrade=True) nella classe [EventSource](assetId:///T:System.Diagnostics.Tracing.EventSource?qualifyHint=False&autoUpgrade=True).  
  
-   Capacità di compattare in modo esplicito gli heap di oggetti grandi durante la Garbage Collection. Per altre informazioni, vedere la proprietà [GCSettings.LargeObjectHeapCompactionMode](assetId:///P:System.Runtime.GCSettings.LargeObjectHeapCompactionMode?qualifyHint=True&autoUpgrade=True).  
  
-   Altri miglioramenti alle prestazioni, quali la sospensione di app ASP.NET, i miglioramenti JIT multicore e un avvio più rapido delle app in seguito a un aggiornamento di .NET Framework. Per informazioni dettagliate, vedere l'[annuncio di .NET Framework 4.5.1](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx) e il post di blog sulla [sospensione di app ASP.NET](http://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx).  
  
 I miglioramenti di Windows Form includono:  
  
-   Ridimensionamento nei controlli Windows Form. È possibile usare l'impostazione DPI per ridimensionare i componenti dei controlli (ad esempio, le icone visualizzate in una griglia delle proprietà) scegliendo una voce nel file di configurazione dell'applicazione (app.config) relativo alla propria app. Questa funzionalità è attualmente supportata nei seguenti controlli Windows Form:  
  
     [PropertyGrid](assetId:///T:System.Windows.Forms.PropertyGrid?qualifyHint=False&autoUpgrade=True)   
     [TreeView](assetId:///T:System.Windows.Forms.TreeView?qualifyHint=False&autoUpgrade=True)   
     Alcuni aspetti di [DataGridView](assetId:///T:System.Windows.Forms.DataGridView?qualifyHint=False&autoUpgrade=True) (per gli altri controlli supportati, vedere le [nuove funzionalità nella versione 4.5.2](#v452))  
  
     Per attivare questa funzionalità, aggiungere un nuovo elemento \<appSettings> al file di configurazione (app.config) e impostare l'elemento `EnableWindowsFormsHighDpiAutoResizing` su `true`:  
  
    ```  
    <appSettings>  
       <add key="EnableWindowsFormsHighDpiAutoResizing" value="true" />  
    </appSettings>  
    ```  
  
 I miglioramenti durante il debug delle app .NET Framework in Visual Studio 2013 includono:  
  
-   Valori restituiti nel debugger di Visual Studio. Quando si esegue il debug di un'app gestita in Visual Studio 2013, nella finestra Auto vengono restituiti tipi e valori per i metodi. Queste informazioni sono disponibili per applicazioni desktop, Windows Store e Windows Phone. Per altre informazioni, vedere [Esaminare i valori restituiti dalle chiamate di metodo](http://msdn.microsoft.com/library/e3245b37-8e2e-4200-ba84-133726e95f1f\(v=vs.120\).aspx) in MSDN Library.  
  
-   Modifica e continua per app a 64 bit. In Visual Studio 2013 è supportata la funzionalità Modifica e continuazione per le applicazioni gestite a 64 bit per desktop, Windows Store e Windows Phone. Le limitazioni esistenti restano valide per le app a 32 bit e a 64 bit. Vedere l'ultima sezione dell'articolo [Modifiche al codice supportate (C#)](http://msdn.microsoft.com/library/ms164927\(v=vs.120\).aspx).  
  
-   Debug asincrono. Per semplificare il debug delle app asincrone in Visual Studio 2013, lo stack di chiamate nasconde il codice dell'infrastruttura fornito dai compilatori per supportare la programmazione asincrona e inoltre si concatena nei frame padre logici, in modo da poter seguire più chiaramente l'esecuzione logica del programma. La finestra Attività in parallelo è stata sostituita da una finestra Attività, contenente le attività correlate a uno specifico punto di interruzione e qualsiasi altra attività attualmente attiva o pianificata nell'app. Informazioni su questa funzionalità sono disponibili nella sezione relativa al debug asincrono nell'[annuncio di .NET Framework 4.5.1](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).  
  
-   Supporto avanzato delle eccezioni per i componenti Windows Runtime. In Windows 8.1 le eccezioni generate dalle app di Windows Store conservano le informazioni sull'errore che ha generato l'eccezione, anche oltre i limiti di linguaggio. Informazioni su questa funzionalità sono disponibili nella sezione relativa allo sviluppo di app di Windows Store nell'[annuncio di .NET Framework 4.5.1](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).  
  
 A partire da Visual Studio 2013, è possibile usare lo strumento [Mpgo.exe (Managed Profile Guided Optimization)](../Topic/Mpgo.exe%20\(Managed%20Profile%20Guided%20Optimization%20Tool\).md) per ottimizzare le app di Windows 8.x Store e quelle desktop.  
  
 Per le nuove funzionalità di ASP.NET 4.5.1, vedere [ASP.NET 4.5.1 e Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=309094) nel sito Web ASP.NET.  
  
 [Torna all'inizio](#introduction)  
  
<a name="core"></a>   
## <a name="whats-new-in-the-net-framework-45"></a>Novità di .NET Framework 4.5  
  
### <a name="core-new-features-and-improvements"></a>Miglioramenti e nuove funzionalità principali  
  
-   Possibilità di ridurre i riavvii di sistema rilevando e chiudendo le applicazioni .NET Framework 4 durante la distribuzione. Vedere [Riduzione dei riavvii del sistema durante le installazioni di .NET Framework 4.5](../Topic/Reducing%20System%20Restarts%20During%20.NET%20Framework%204.5%20Installations.md).  
  
-   Supporto per le matrici di dimensioni maggiori di 2 GB nelle piattaforme a 64 bit. Questa funzionalità può essere abilitata nel file di configurazione dell'applicazione. Vedere l'[\<elemento gcAllowVeryLargeObjects>](../Topic/%3CgcAllowVeryLargeObjects%3E%20Element.md), che elenca anche altre restrizioni per le dimensioni di oggetti e matrici.  
  
-   Miglioramento delle prestazioni tramite Garbage Collection in background per server. Se si usa la funzionalità di Garbage Collection del server in .NET Framework 4.5, verrà automaticamente abilità la Garbage Collection in background. Vedere la sezione "Operazione di Garbage Collection in background per server" nell'argomento [Principi fondamentali di Garbage Collection](../Topic/Fundamentals%20of%20Garbage%20Collection.md).  
  
-   Compilazione JIT in background, eventualmente disponibile nei processori multicore per migliorare le prestazioni delle applicazioni. Vedere [ProfileOptimization](assetId:///T:System.Runtime.ProfileOptimization?qualifyHint=False&autoUpgrade=True).  
  
-   Possibilità di limitare il periodo in cui il motore delle espressioni regolari tenta di risolvere un'espressione regolare prima che si verifichi il timeout. Vedere la proprietà [Regex.MatchTimeout](assetId:///P:System.Text.RegularExpressions.Regex.MatchTimeout?qualifyHint=True&autoUpgrade=True).  
  
-   Possibilità di definire le impostazioni cultura predefinite per un dominio di applicazione. Vedere la classe [CultureInfo](assetId:///T:System.Globalization.CultureInfo?qualifyHint=False&autoUpgrade=True).  
  
-   Supporto della console per la codifica Unicode (UTF-16). Vedere la classe [Console](assetId:///T:System.Console?qualifyHint=False&autoUpgrade=True).  
  
-   Supporto per il controllo delle versioni dei dati di confronto e ordinamento delle stringhe di impostazioni cultura. Vedere la classe [SortVersion](assetId:///T:System.Globalization.SortVersion?qualifyHint=False&autoUpgrade=True).  
  
-   Miglioramento delle prestazioni in fase di recupero di risorse. Vedere [Creazione del pacchetto e distribuzione delle risorse in applicazioni desktop](../Topic/Packaging%20and%20Deploying%20Resources%20in%20Desktop%20Apps.md).  
  
-   Miglioramenti delle compressioni ZIP per ridurre la dimensione di un file compresso. Vedere lo spazio dei nomi [System.IO.Compression](assetId:///N:System.IO.Compression?qualifyHint=True&autoUpgrade=True).  
  
-   Possibilità di personalizzare un contesto di reflection per eseguire l'override del comportamento di reflection predefinito tramite la classe [CustomReflectionContext](assetId:///T:System.Reflection.Context.CustomReflectionContext?qualifyHint=False&autoUpgrade=True).  
  
-   Supporto per la versione 2008 dello standard IDNA (Internationalized Domain Names in Applications) quando si usa la classe [System.Globalization.IdnMapping](assetId:///T:System.Globalization.IdnMapping?qualifyHint=True&autoUpgrade=True) in Windows 8.  
  
-   Delega del confronto tra stringhe al sistema operativo, che effettua l'implementazione di Unicode 6.0, quando .NET Framework viene usato in Windows 8. Quando è in esecuzione in altre piattaforme, .NET Framework include i propri dati di confronto tra stringhe, che effettua l'implementazione di Unicode 5.x. Vedere la classe [String](assetId:///T:System.String?qualifyHint=False&autoUpgrade=True) e la sezione Note della classe [SortVersion](assetId:///T:System.Globalization.SortVersion?qualifyHint=False&autoUpgrade=True).  
  
-   Possibilità di calcolare i codici hash per le stringhe in base al dominio dell'applicazione. Vedere [\<Elemento UseRandomizedStringHashAlgorithm>](../Topic/%3CUseRandomizedStringHashAlgorithm%3E%20Element.md).  
  
-   Il supporto per la reflection dei tipi è stato suddiviso tra le classi [Type](assetId:///T:System.Type?qualifyHint=False&autoUpgrade=True) e [TypeInfo](assetId:///T:System.Reflection.TypeInfo?qualifyHint=False&autoUpgrade=True). Vedere [Reflection in .NET Framework per app di Windows Store](../Topic/Reflection%20in%20the%20.NET%20Framework%20for%20Windows%20Store%20Apps.md).  
  
### <a name="managed-extensibility-framework-mef"></a>Managed Extensibility Framework (MEF)  
 In .NET Framework 4.5 la libreria Managed Extensibility Framework (MEF) offre le seguenti nuove funzionalità:  
  
-   Supporto per tipi generici.  
  
-   Modello di programmazione basato su convenzioni che consente di creare parti basate sulle convenzioni di denominazione, anziché sugli attributi.  
  
-   Più ambiti.  
  
-   Subset di MEF che è possibile usare in fase di creazione delle app di Windows 8.x Store. Questo subset è disponibile come [pacchetto scaricabile](http://go.microsoft.com/fwlink/?LinkId=256238) dalla raccolta NuGet. Per installare il pacchetto, aprire il progetto in Visual Studio, scegliere **Gestisci pacchetti NuGet** dal menu **Progetto** ed eseguire una ricerca online del pacchetto `Microsoft.Composition`.  
  
 Per altre informazioni, vedere [Managed Extensibility Framework (MEF)](../Topic/Managed%20Extensibility%20Framework%20\(MEF\).md).  
  
### <a name="asynchronous-file-operations"></a>Operazioni asincrone sui file.  
 In .NET Framework 4.5 sono state aggiunte nuove funzionalità asincrone nei linguaggi C# e Visual Basic. Con queste funzionalità viene introdotto un modello basato su attività per eseguire operazioni asincrone. Per impiegare questo nuovo modello, usare i metodi asincroni nelle classi I/O. Vedere [I/O di file asincrono](../Topic/Asynchronous%20File%20I-O.md).  
  
<a name="tools"></a>   
### <a name="tools"></a>Strumenti  
 In .NET Framework 4.5 il generatore di file di risorse (Resgen.exe) consente di creare un file con estensione resw per l'uso nelle app di Windows 8.x Store da un file con estensione resources incorporato in un assembly .NET Framework. Per altre informazioni, vedere [Resgen.exe (generatore di file di risorse)](../Topic/Resgen.exe%20\(Resource%20File%20Generator\).md).  
  
 L'ottimizzazione PGO gestita (Mpgo.exe) consente di migliorare i tempi di avvio delle applicazioni, l'uso della memoria (dimensione del working set) e la velocità effettiva attraverso l'ottimizzazione degli assembly di immagini nativi. Lo strumento da riga di comando genera dati di profilo per assembly di applicazioni di immagini nativi. Vedere [Strumento Mpgo.exe (Managed Profile Guided Optimization)](../Topic/Mpgo.exe%20\(Managed%20Profile%20Guided%20Optimization%20Tool\).md). A partire da Visual Studio 2013, è possibile usare Mpgo.exe per ottimizzare le app di Windows 8.x Store e quelle desktop.  
  
<a name="parallel"></a>   
### <a name="parallel-computing"></a>Elaborazione parallela  
 In .NET Framework 4.5 vengono forniti diversi miglioramenti e nuove funzionalità per il calcolo parallelo. Alcuni esempi: miglioramento delle prestazioni, maggiore controllo, supporto avanzato per la programmazione asincrona, una nuova libreria di flussi di dati e un miglioramento del supporto per il debug parallelo e l'analisi delle prestazioni. Vedere la voce relativa alle [novità per il parallelismo in .NET 4.5](http://go.microsoft.com/fwlink/?LinkId=235061) nel blog sulla programmazione parallela con .NET.  
  
<a name="web"></a>   
### <a name="web"></a>Web  
 In ASP.NET 4.5 e 4.5.1 vengono aggiunti associazione di modelli per Web Form, supporto di WebSocket, gestori asincroni, miglioramenti delle prestazioni e molte altre funzionalità. Per altre informazioni, vedere le seguenti risorse:  
  
-   [ASP.NET 4.5 e Visual Studio 2012](../Topic/ASP.NET%20Core%20and%20Visual%20Studio%202015.md) in MSDN Library.  
  
-   [ASP.NET 4.5.1 e Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=309094) nel sito Web ASP.NET.  
  
<a name="networking"></a>   
### <a name="networking"></a>Rete  
 In .NET Framework 4.5 viene fornita una nuova interfaccia di programmazione per applicazioni HTTP. Per altre informazioni, vedere i nuovi spazi dei nomi [System.Net.Http](assetId:///N:System.Net.Http?qualifyHint=True&autoUpgrade=True) e [System.Net.Http.Headers](assetId:///N:System.Net.Http.Headers?qualifyHint=True&autoUpgrade=True).  
  
 È anche incluso il supporto per una nuova interfaccia di programmazione per l'accettazione e l'interazione con una connessione WebSocket usando l'oggetto [HttpListener](assetId:///T:System.Net.HttpListener?qualifyHint=False&autoUpgrade=True) esistente e le classi correlate. Per altre informazioni, vedere il nuovo spazio dei nomi [System.Net.WebSockets](assetId:///N:System.Net.WebSockets?qualifyHint=False&autoUpgrade=True) e la classe [HttpListener](assetId:///T:System.Net.HttpListener?qualifyHint=False&autoUpgrade=True).  
  
 In .NET Framework 4.5 sono inclusi anche i seguenti miglioramenti di rete:  
  
-   Supporto URI conforme a RFC. Per altre informazioni, vedere [URI](assetId:///T:System.Uri?qualifyHint=False&autoUpgrade=True) e le classi correlate.  
  
-   Supporto per l'analisi IDN (Internationalized Domain Name). Per altre informazioni, vedere [URI](assetId:///T:System.Uri?qualifyHint=False&autoUpgrade=True) e le classi correlate.  
  
-   Supporto per EAI (Email Address Internationalization). Per altre informazioni, vedere lo spazio dei nomi [System.Net.Mail](assetId:///N:System.Net.Mail?qualifyHint=False&autoUpgrade=True).  
  
-   Supporto IPv6 avanzato. Per altre informazioni, vedere lo spazio dei nomi [System.Net.NetworkInformation](assetId:///N:System.Net.NetworkInformation?qualifyHint=False&autoUpgrade=True).  
  
-   Supporto per socket dual mode. Per altre informazioni, vedere le classi [Socket](assetId:///T:System.Net.Sockets.Socket?qualifyHint=False&autoUpgrade=True) e [TcpListener](assetId:///T:System.Net.Sockets.TcpListener?qualifyHint=False&autoUpgrade=True).  
  
<a name="client"></a>   
### <a name="windows-presentation-foundation-wpf"></a>Windows Presentation Foundation (WPF)  
 In .NET Framework 4.5, Windows Presentation Foundation (WPF) include miglioramenti e modifiche nelle aree seguenti:  
  
-   Nuovo controllo [Ribbon](assetId:///T:System.Windows.Controls.Ribbon.Ribbon?qualifyHint=False&autoUpgrade=True), che consente di implementare l'interfaccia utente di una barra multifunzione che ospita una barra di accesso rapido, menu di applicazione e schede.  
  
-   Nuova interfaccia [INotifyDataErrorInfo](assetId:///T:System.ComponentModel.INotifyDataErrorInfo?qualifyHint=False&autoUpgrade=True), che supporta la convalida sincrona e asincrona dei dati.  
  
-   Nuove funzionalità per le classi [VirtualizingPanel](assetId:///T:System.Windows.Controls.VirtualizingPanel?qualifyHint=False&autoUpgrade=True) e [Dispatcher](assetId:///T:System.Windows.Threading.Dispatcher?qualifyHint=False&autoUpgrade=True).  
  
-   Miglioramento delle prestazioni durante la visualizzazione di grandi set di dati raggruppati e mediante l'accesso alle raccolte in thread non dell'interfaccia utente.  
  
-   Associazione di dati a proprietà statiche, associazione di dati a tipi personalizzati che implementano l'interfaccia [ICustomTypeProvider](assetId:///T:System.Reflection.ICustomTypeProvider?qualifyHint=False&autoUpgrade=True) e recupero di informazioni sull'associazione dati da un'espressione di associazione.  
  
-   Riposizionamento di dati contestuale alla modifica dei valori (shaping attivo).  
  
-   Possibilità di controllare se il contesto dei dati per un contenitore di elementi è disconnesso.  
  
-   Possibilità di impostare la quantità di tempo che deve trascorrere tra le modifiche alle proprietà e gli aggiornamenti delle origini dati.  
  
-   Supporto avanzato per l'implementazione di modelli di eventi deboli. Inoltre, gli eventi possono ora accettare estensioni di markup.  
  
<a name="windows_communication_foundation"></a>   
### <a name="windows-communication-foundation-wcf"></a>Windows Communication Foundation (WCF)  
 In .NET Framework 4.5 le seguenti funzionalità sono state aggiunte per semplificare la scrittura e la gestione di applicazioni Windows Communication Foundation (WCF):  
  
-   Semplificazione dei file di configurazione generati.  
  
-   Supporto per lo sviluppo con priorità al contratto ("contract-first").  
  
-   Possibilità di configurare la modalità di compatibilità ASP.NET in modo più semplice.  
  
-   Modifiche ai valori predefiniti delle proprietà di trasporto per ridurre la probabilità di doverli impostare.  
  
-   Aggiornamenti alla classe [XmlDictionaryReaderQuotas](assetId:///T:System.Xml.XmlDictionaryReaderQuotas?qualifyHint=False&autoUpgrade=True) per ridurre la probabilità di dover configurare manualmente le quote per i lettori di dizionario XML.  
  
-   Convalida dei file di configurazione WCF da parte di Visual Studio nell'ambito del processo di compilazione, in modo da poter rilevare errori di configurazione prima di eseguire l'applicazione.  
  
-   Nuovo supporto per lo streaming asincrono.  
  
-   Nuovo mapping del protocollo HTTPS per semplificare l'esposizione di un endpoint su HTTPS con Internet Information Services (IIS).  
  
-   Possibilità di generare metadati in un singolo documento WSDL aggiungendo `?singleWSDL` all'URL del servizio.  
  
-   Supporto di WebSocket per consentire un'effettiva comunicazione bidirezionale sulle porte 80 e 443 con caratteristiche di prestazioni simili al trasporto TCP.  
  
-   Supporto per la configurazione dei servizi nel codice.  
  
-   Descrizioni comando dell'editor XML.  
  
-   Supporto per la memorizzazione nella cache di [ChannelFactory](assetId:///T:System.ServiceModel.ChannelFactory?qualifyHint=False&autoUpgrade=True).  
  
-   Supporto della compressione del codificatore binario.  
  
-   Supporto per un trasporto UDP che consente agli sviluppatori di scrivere servizi che usano la messaggistica di tipo "Fire and Forget". Un client invia un messaggio a un servizio e non prevede alcuna risposta dal servizio.  
  
-   Possibilità di supportare più modalità di autenticazione in un singolo endpoint WCF quando si usa il trasporto HTTP e la sicurezza del trasporto.  
  
-   Supporto per servizi WCF che usano IDN (Internationalized Domain Name).  
  
 Per altre informazioni, vedere [Novità di Windows Communication Foundation](http://go.microsoft.com/fwlink/?LinkId=228173).  
  
<a name="windows_workflow_foundation"></a>   
### <a name="windows-workflow-foundation-wf"></a>Windows Workflow Foundation (WF)  
 In .NET Framework 4.5 sono state introdotte numerose nuove funzionalità in Windows Workflow Foundation (WF), tra cui:  
  
-   Flussi di lavoro della macchina a stati, introdotti per la prima volta in .NET Framework 4.0.1 ([.NET Framework 4 Platform Update 1](http://go.microsoft.com/fwlink/?LinkID=215092)). In questo aggiornamento erano incluse diverse nuove classi e attività che consentivano agli sviluppatori di creare flussi di lavoro macchina a stati. Queste classi e attività sono state aggiornate per .NET Framework 4.5 al fine di includere:  
  
    -   Possibilità di impostare punti di interruzione negli stati.  
  
    -   Possibilità di copiare e incollare transizioni in Workflow Designer.  
  
    -   Supporto della finestra di progettazione per la creazione di transizioni con trigger condivisi.  
  
    -   Attività per creare flussi di lavoro macchina a stati, tra cui: [StateMachine](assetId:///T:System.Activities.Statements.StateMachine?qualifyHint=False&autoUpgrade=True), [State](assetId:///T:System.Activities.Statements.State?qualifyHint=False&autoUpgrade=True) e [Transition](assetId:///T:System.Activities.Statements.Transition?qualifyHint=False&autoUpgrade=True).  
  
-   Funzionalità avanzate di Workflow Designer, tra cui:  
  
    -   Funzionalità avanzate di ricerca di flussi di lavoro in Visual Studio, tra cui **Ricerca veloce** e **Cerca nei file**.  
  
    -   Possibilità di creare automaticamente un'attività Sequence quando viene aggiunta una seconda attività figlio a un'attività del contenitore e di includere entrambe le attività nell'attività Sequence.  
  
    -   Supporto per panoramica, che consente di modificare la parte visibile di un flusso di lavoro senza ricorrere a barre di scorrimento.  
  
    -   Nuova visualizzazione **Struttura documento** che mostra i componenti di un flusso di lavoro in una visualizzazione in stile albero e permette di selezionare un componente nella visualizzazione **Struttura documento**.  
  
    -   Possibilità di aggiungere annotazioni alle attività.  
  
    -   Capacità di definire e usare delegati di attività mediante Workflow Designer.  
  
    -   Connessione e inserimento automatici per attività e transizioni nei flussi di lavoro macchina a stati e del diagramma di flusso.  
  
-   Archiviazione di informazioni sullo stato di visualizzazione per un flusso di lavoro in un singolo elemento nel file XAML, in modo da poter individuare e modificare agevolmente tali informazioni.  
  
-   Attività del contenitore NoPersistScope per impedire la conservazione delle attività figlio.  
  
-   Supporto per espressioni C#:  
  
    -   I progetti di flusso di lavoro che usano Visual Basic impiegheranno espressioni Visual Basic, mentre i progetti di flusso di lavoro C# useranno espressioni C#.  
  
    -   I progetti di flusso di lavoro C# creati in Visual Studio 2010 e con espressioni Visual Basic sono compatibili con i progetti di flusso di lavoro C# che usano espressioni C#.  
  
-   Miglioramenti del controllo delle versioni:  
  
    -   Nuova classe [WorkflowIdentity](assetId:///T:System.Activities.WorkflowIdentity?qualifyHint=False&autoUpgrade=True), che fornisce un mapping tra un'istanza di flusso di lavoro persistente e la relativa definizione.  
  
    -   Esecuzione affiancata di più versioni del flusso di lavoro nello stesso host, tra cui [WorkflowServiceHost](assetId:///T:System.ServiceModel.Activities.WorkflowServiceHost?qualifyHint=False&autoUpgrade=True).  
  
    -   In Aggiornamento dinamico, capacità di modificare la definizione di un'istanza di flusso di lavoro persistente.  
  
-   Sviluppo di flussi di lavoro con priorità al contratto ("contract-first"), che fornisce supporto per generare automaticamente attività in modo da soddisfare un contratto di servizio esistente.  
  
 Per altre informazioni, vedere [Novità di Windows Workflow Foundation](http://go.microsoft.com/fwlink/?LinkId=228176).  
  
<a name="tailored"></a>   
### <a name="net-for-windows-8x-store-apps"></a>.NET per app di Windows 8.x Store  
 Le app di WIndows 8.x Store sono progettate per fattori di forma specifici e sfruttano la potenza del sistema operativo Windows. Un subset di .NET Framework 4.5 o 4.5.1 è disponibile per la compilazione di app per Windows 8.x Store usando C# o Visual Basic. Questo subset è denominato .NET per app di Windows 8.x Store e viene descritto in una [panoramica](http://go.microsoft.com/fwlink/?LinkId=228491) in Windows Dev Center.  
  
<a name="portable"></a>   
### <a name="portable-class-libraries"></a>Librerie di classi portabili  
 Il progetto Libreria di classi portabile in Visual Studio 2012 (e versioni successive) consente di scrivere e compilare assembly gestiti compatibili con più piattaforme .NET Framework. Se si usa un progetto Libreria di classi portabile, si scelgono le piattaforme (ad esempio Windows Phone e .NET per app di Windows 8.x Store) di destinazione. I tipi e i membri disponibili nel progetto sono automaticamente limitati a tipi e membri comuni in queste piattaforme. Per altre informazioni, vedere [Libreria di classi portabile](../Topic/Cross-Platform%20Development%20with%20the%20Portable%20Class%20Library.md).  
  
## <a name="see-also"></a>Vedere anche  
 [.NET Framework e rilascio fuori programma](~/docs/framework/get-started/the-net-framework-and-out-of-band-releases.md)   
 [Novità di Visual Studio 2013](http://msdn.microsoft.com/library/bb386063\(v=vs.120\).aspx)   
 [ASP.NET 4.5.1 e Strumenti Web per Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=309094)   
 [ASP.NET e Visual Studio per il Web](../Topic/ASP.NET%20and%20Visual%20Studio%20for%20Web.md)   
 [Novità in Windows Communication Foundation](http://go.microsoft.com/fwlink/?LinkId=228173)   
 [Novità in Windows Workflow Foundation](http://go.microsoft.com/fwlink/?LinkId=228176)   
 [Novità di Visual C++](http://msdn.microsoft.com/library/hh409293\(v=vs.120\).aspx)

