---
title: "Novità di .NET Framework | Microsoft Docs"
ms.custom: 
ms.date: 05/02/2017
ms.prod: .net-framework
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
ms.translationtype: Human Translation
ms.sourcegitcommit: ec57b79f67f826dbe61aa81bb5f82e20d61db2e3
ms.openlocfilehash: cec16529ea93773362715cac7694b451ce3dddfe
ms.contentlocale: it-it
ms.lasthandoff: 05/11/2017

---
# <a name="whats-new-in-the-net-framework"></a>Novità di .NET Framework
<a name="introduction"></a> Questo articolo offre un riepilogo dei principali nuovi miglioramenti e funzionalità introdotti nelle versioni seguenti di .NET Framework:

 [.NET Framework 4.7](#v47)   
 [.NET Framework 4.6.2](#v462)   
 [.NET Framework 4.6.1](#v461)   
 [.NET 2015 e .NET Framework 4.6](#v46)   
 [.NET Framework 4.5.2](#v452)   
 [.NET Framework 4.5.1](#v451)   
 [.NET Framework 4.5](#core)   

 Non vengono fornite informazioni complete su ogni nuova funzionalità e l'articolo è soggetto a modifiche. Per informazioni generali su .NET Framework, vedere [Introduzione a .NET Framework](../../../docs/framework/get-started/index.md). Per informazioni sulle piattaforme supportate, vedere [Requisiti di sistema di .NET Framework](~/docs/framework/get-started/system-requirements.md). Per i collegamenti per il download e le istruzioni di installazione, vedere [Guida all'installazione](../../../docs/framework/install/guide-for-developers.md).

> [!NOTE]
>  Il team di .NET Framework rende disponibili anche alcune funzionalità fuori programma con NuGet per espandere le piattaforme supportate e introdurre nuove funzionalità, ad esempio le raccolte non modificabili e i tipi di vettore abilitati per SIMD. Per altre informazioni, vedere [API e librerie di classi aggiuntive](../additional-apis/index.md) e [.NET Framework e rilascio fuori programma](~/docs/framework/get-started/the-net-framework-and-out-of-band-releases.md). Vedere l'[elenco completo dei pacchetti NuGet](https://blogs.msdn.microsoft.com/dotnet/p/nugetpackages/) per .NET Framework oppure sottoscrivere [questo feed](https://nuget.org/api/v2/curated-feeds/dotnetframework/Packages/).

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
#### <a name="core"></a>Base

.NET Framework 4.7 migliora la serializzazione da <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>:

**Funzionalità migliorate con l'algoritmo ECC (Elliptic Curve Cryptography)***

In .NET Framework 4.7, sono stati aggiunti i metodi `ImportParameters(ECParameters)` alle classi <xref:System.Security.Cryptography.ECDsa> e <xref:System.Security.Cryptography.ECDiffieHellman> per consentire a un oggetto di rappresentare una chiave già stabilita. È stato anche aggiunto un metodo `ExportParameters(Boolean)` per l'esportazione della chiave usando parametri della curva esplicita.

.NET Framework 4.7 aggiunge anche il supporto per le curve aggiuntive (inclusa la suite di curve Brainpool) e ha aggiunto definizioni predefinite per semplificare la creazione attraverso i nuovi metodi factory <xref:System.Security.Cryptography.ECDsa.Create%2A> e <xref:System.Security.Cryptography.ECDiffieHellman.Create%2A>.

È possibile visualizzare un [esempio dei miglioramenti alla crittografia di .NET Framework 4.7](https://gist.github.com/richlander/5a182899895a87a296c21ada97f7a54e) su GitHub.

**Supporto migliorato per i caratteri di controllo da DataContractJsonSerializer**

In .NET Framework 4.7 <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> serializza i caratteri di controllo in conformità con lo standard ECMAScript 6. Questo comportamento è abilitato per impostazione predefinita per le applicazioni che utilizzano .NET Framework 4.7 ed è una funzionalità che prevede il consenso esplicito per le applicazioni che sono in esecuzione con .NET Framework 4.7, ma sono destinate a una versione precedente di .NET Framework. Per altre informazioni, vedere [Reindirizzamento delle modifiche in .NET Framework versione 4.7](../../../docs/framework/migration-guide/retargeting-changes-in-the-net-framework-4-7.md).

<a name="net47" />
#### <a name="networking"></a>Rete

.NET Framework 4.7 aggiunge la seguente funzionalità relativa alla rete:

**Supporto del sistema operativo predefinito per i protocolli TLS***

Lo stack TLS, che viene usato da <xref:System.Net.Security.SslStream?displayProperty=fullName> e i componenti up-stack, ad esempio HTTP, FTP e SMTP, consentono agli sviluppatori di usare i protocolli TLS predefiniti supportati dal sistema operativo. Gli sviluppatori non devono più impostare come hardcoded una versione TLS.

<a name="ASP-NET47" />
#### <a name="aspnet"></a>ASP.NET

In .NET Framework 4.7, ASP.NET include le nuove funzionalità seguenti:

**Estendibilità della cache oggetti**

A partire da Framework .NET 4.7, ASP.NET aggiunge un nuovo set di API che consente agli sviluppatori di sostituire le implementazioni di ASP.NET predefinite per la cache di oggetti in memoria e il monitoraggio della memoria. Gli sviluppatori possono ora sostituire uno qualsiasi dei seguenti tre componenti se l'implementazione di ASP.NET non è sufficiente:

- **Archivio cache oggetti**. Usando la nuova sezione di configurazione dei provider di cache, gli sviluppatori possono inserire nuove implementazioni di una cache oggetti per un'applicazione ASP.NET con la nuova interfaccia **ICacheStoreProvider**.
 
- **Monitoraggio della memoria**. Il monitoraggio della memoria predefinito in ASP.NET invia una notifica alle applicazioni quando stanno per raggiungere il limite di byte privati configurato per il processo o quando la RAM fisica totale disponibile nel computer è insufficiente. Quando si approssimano questi limiti, vengono generate le notifiche. Per alcune applicazioni, le notifiche vengono generate troppo vicino ai limiti configurati per consentire reazioni utili. Gli sviluppatori possono ora scrivere monitoraggi della memoria personalizzati in modo da sostituire quello predefinito usando la proprietà <xref:System.Web.Hosting.ApplicationMonitors.MemoryMonitor%2A?displayProperty=fullName>.

- **Reazioni al limite di memoria**. Per impostazione predefinita, ASP.NET prova a ridurre la cache oggetti e a chiamare periodicamente <xref:System.GC.Collect%2A?displayProperty=fullName> quando si approssima il limite di byte privati per il processo. Per alcune applicazioni, la frequenza delle chiamate a <xref:System.GC.Collect%2A?displayProperty=fullName> o la quantità di cache che verrà tagliata sono inefficienti. Gli sviluppatori possono ora sostituire o integrare il comportamento predefinito sottoscrivendo le implementazioni **IObserver** al monitoraggio della memoria dell'applicazione.

<a name="wcf47" />
#### <a name="windows-communication-foundation-wcf"></a>Windows Communication Foundation (WCF)

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
- Maggiore affidabilità delle operazioni di serializzazione durante la chiamata del metodo <xref:System.Runtime.Serialization.FormatterServices.GetSerializableMembers%28System.Type%29?displayProperty=fullName>.
- Maggiore affidabilità durante la rimozione di un oggetto waiter con la chiamata del metodo **ChannelSynchronizer.RemoveWaiter**.

<a name="wf47" />
#### <a name="windows-forms"></a>Windows Form

In Framework .NET 4.7, Windows Form migliora il supporto per i monitor di valori DPI alti.

**Supporto di valori DPI alti**

A partire dalle applicazioni destinate a .NET Framework 4.7, le funzionalità di .NET Framework prevedono il supporto dei di valori DPI alti e dinamici per Windows Forms Application. Il supporto di valori DPI alti migliora il layout e l'aspetto dei moduli e dei controlli nei monitor di valori DPI alti. I valori DPI cambiano il layout e l'aspetto dei moduli e dei controlli quando l'utente modifica i valori DPI o visualizza il fattore di scala di un'applicazione in esecuzione.

Il supporto di valori DPI alti è una funzionalità che prevede il consenso esplicito e si configurare definendo una sezione [\<System.Windows.Forms.ConfigurationSection>](../configure-apps/file-schema/winforms/index.md) nel file di configurazione dell'applicazione. Per altre informazioni sull'aggiunta del supporto di valori DPI elevati e dinamici a un'applicazione Windows Form, vedere [Supporto di valori DPI elevati in Windows Form](../winforms/high-dpi-support-in-windows-forms.md).

<a name="WPF47"></a> 
#### <a name="windows-presentation-foundation-wpf"></a>Windows Presentation Foundation (WPF)

In .NET Framework 4.7, WPF include i miglioramenti seguenti:

**Supporto per lo stack di tocco/stilo basato sui messaggi basato sui messaggi WM_POINTER Windows**

È ora possibile scegliere di usare uno stack di tocco/stilo basato sui [messaggi WM_POINTER](https://msdn.microsoft.com/library/windows/desktop/hh454903.aspx) invece che su WISP (Windows Ink Services Platform). È una funzionalità di .NET Framework che prevede il consenso esplicito. Per altre informazioni, vedere [Reindirizzamento delle modifiche in .NET Framework versione 4.7](../migration-guide/retargeting-changes-in-the-net-framework-4-7.md).

**Nuova implementazione per le API di stampa WPF**

Le API di stampa di WPF nella classe <xref:System.Printing.PrintQueue?displayProperty=fullName> chiamano l'[API del pacchetto dei documenti di stampa](https://msdn.microsoft.com/library/windows/desktop/hh448418(v=vs.85).aspx) di Windows anziché l'[API di stampa XPS](https://msdn.microsoft.com/library/windows/desktop/ff686814(v=vs.85).aspx) deprecata. Per l'impatto di questa modifica sulla compatibilità delle applicazioni, vedere [Reindirizzamento delle modifiche in .NET Framework versione 4.7](../migration-guide/retargeting-changes-in-the-net-framework-4-7.md). 

<a name="v462"></a> 
## <a name="whats-new-in-the-net-framework-462"></a>Novità di .NET Framework 4.6.2
 [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] include nuove funzionalità nelle aree seguenti:

- [ASP.NET 2.0](#ASPNET462)

- [Categorie di caratteri](#Strings)

- [Crittografia](#Crypto462)

- [SqlClient](#SQLClient)

- [Windows Communication Foundation](#WCF)

- [Windows Presentation Foundation (WPF)](#WPF462)

- [Windows Workflow Foundation (WF)](#WF462)

- [ClickOnce](#ClickOnce)

- [Conversione di Windows Form e applicazioni WPF in applicazioni UWP](#UWPConvert)

- [Miglioramenti apportati al debug](#Debug462)

Per un elenco delle nuove API aggiunte a .NET Framework 4.6.2, vedere l'argomento sulle [modifiche apportate all'API di .NET Framework 4.6.2](https://github.com/Microsoft/dotnet/blob/master/releases/net462/dotnet462-api-changes.md) su GitHub. Per l'elenco dei miglioramenti apportati alle funzionalità e delle correzioni di bug in .NET Framework 4.6.2, vedere l'argomento [.NET Framework 4.6.2 List of Changes](http://go.microsoft.com/fwlink/?LinkId=708778) (Elenco delle modifiche in .NET Framework 4.6.2) su GitHub.  Per altre informazioni, vedere l'[annuncio di .NET Framework 4.6.2](https://blogs.msdn.microsoft.com/dotnet/2016/08/02/announcing-net-framework-4-6-2/) in .NET Blog.

<a name="ASPNET462"></a> 
### <a name="aspnet"></a>ASP.NET
 In [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], ASP.NET include i miglioramenti seguenti:

 **Migliore supporto per i messaggi di errore localizzati nei validator di annotazioni dei dati **
 I validator di annotazioni dei dati consentono di eseguire la convalida aggiungendo uno o più attributi a una proprietà di classe. L'elemento <xref:System.ComponentModel.DataAnnotations.ValidationAttribute.ErrorMessage%2A?displayProperty=fullName> dell'attributo definisce il testo del messaggio di errore se la convalida non riesce. A partire da [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], ASP.NET semplifica la localizzazione dei messaggi di errore. I messaggi di errore verranno localizzati se:

1.  L'elemento <xref:System.ComponentModel.DataAnnotations.ValidationAttribute.ErrorMessage%2A?displayProperty=fullName> viene specificato nell'attributo di convalida.

2.  Il file di risorse è archiviato nella cartella App_LocalResources.

3.  Il nome del file di risorse localizzato ha il formato `DataAnnotation.Localization.{`*nome*`}.resx`, dove *nome* è il nome delle impostazioni cultura con il formato *codicelingua*`-`*codicepaese/area geografica* o *codicelingua*.

4.  Il nome della chiave della risorsa è la stringa assegnata all'attributo <xref:System.ComponentModel.DataAnnotations.ValidationAttribute.ErrorMessage%2A?displayProperty=fullName> e il suo valore è il messaggio di errore localizzato.

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
   <Required(ErrorMessage = "The rating must be between 1 and 10.")>
   <Display(Name = "Your Rating")>
   Public Property Rating As Integer = 1
End Class
```

 È quindi possibile creare il file di risorse DataAnnotation.Localization.fr.resx, la cui chiave è la stringa del messaggio di errore e il cui valore è il messaggio di errore localizzato. Il file deve essere salvato nella cartella `App.LocalResources`. Ad esempio, di seguito vengono riportati la chiave e il relativo valore in un messaggio di errore in lingua francese (fr):

|Nome|Valore|
|----------|-----------|
|La classificazione deve essere compresa tra 1 e 10.|La note doit être comprise entre 1 et 10.|

 Questo file può quindi

 La localizzazione dell'annotazione dei dati è anche estensibile. Gli sviluppatori possono collegare il proprio provider di localizzazione delle stringhe implementando l'interfaccia <xref:System.Web.Globalization.IStringLocalizerProvider> per archiviare la stringa di localizzazione in una posizione diversa da un file di risorse.

 **Supporto per le operazioni asincrone con i provider dello stato sessione**
 ASP.NET offre ora metodi con restituzione di Task da usare con i provider dello stato sessione, consentendo quindi alle app ASP.NET di usufruire dei vantaggi della scalabilità delle operazioni asincrone. Per supportare le operazioni asincrone con provider di archiviazione dello stato sessione, ASP.NET include la nuova interfaccia <xref:System.Web.SessionState.ISessionStateModule?displayProperty=fullName>, che eredita da <xref:System.Web.IHttpModule> e permette agli sviluppatori di implementare i propri provider di moduli dello stato sessione e di archiviazione asincrona delle sessioni. L'interfaccia viene definita come segue:

```csharp

public interface ISessionStateModule : IHttpModule {
    void ReleaseSessionState(HttpContext context);
    Task ReleaseSessionStateAsync(HttpContext context);
}

```

 Inoltre, la classe <xref:System.Web.SessionState.SessionStateUtility> include due nuovi metodi, <xref:System.Web.SessionState.SessionStateUtility.IsSessionStateReadOnly%2A> e <xref:System.Web.SessionState.SessionStateUtility.IsSessionStateRequired%2A>, che possono essere usati per supportare le operazioni asincrone.

 **Supporto per le operazioni asincrone con i provider di cache di output**
 A partire da [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], i metodi con restituzione di Task possono essere usati con i provider di cache di output per usufruire dei vantaggi della scalabilità delle operazioni asincrone.  I provider che implementano questi metodi riducono i blocchi dei thread su un server Web e migliorano la scalabilità di un servizio ASP.NET.

 Per supportare i provider di cache di output asincroni sono state aggiunte le API seguenti:

- Classe <xref:System.Web.Caching.OutputCacheProviderAsync?displayProperty=fullName>, che eredita da <xref:System.Web.Caching.OutputCacheProvider?displayProperty=fullName> e permette agli sviluppatori di implementare un provider di cache di output asincrono.

- Classe <xref:System.Web.Caching.OutputCacheUtility>, che fornisce metodi helper per la configurazione della cache di output.

- 18 nuovi metodi nella classe <xref:System.Web.HttpCachePolicy?displayProperty=fullName>. Sono inclusi <xref:System.Web.HttpCachePolicy.GetCacheability%2A>, <xref:System.Web.HttpCachePolicy.GetCacheExtensions%2A>, <xref:System.Web.HttpCachePolicy.GetETag%2A>, <xref:System.Web.HttpCachePolicy.GetETagFromFileDependencies%2A>, <xref:System.Web.HttpCachePolicy.GetMaxAge%2A>, <xref:System.Web.HttpCachePolicy.GetMaxAge%2A>, <xref:System.Web.HttpCachePolicy.GetNoStore%2A>, <xref:System.Web.HttpCachePolicy.GetNoTransforms%2A>, <xref:System.Web.HttpCachePolicy.GetOmitVaryStar%2A>, <xref:System.Web.HttpCachePolicy.GetProxyMaxAge%2A>, <xref:System.Web.HttpCachePolicy.GetRevalidation%2A>, <xref:System.Web.HttpCachePolicy.GetUtcLastModified%2A>, <xref:System.Web.HttpCachePolicy.GetVaryByCustom%2A>, <xref:System.Web.HttpCachePolicy.HasSlidingExpiration%2A> e <xref:System.Web.HttpCachePolicy.IsValidUntilExpires%2A>.

- 2 nuovi metodi nella classe <xref:System.Web.HttpCacheVaryByContentEncodings?displayProperty=fullName>: <xref:System.Web.HttpCacheVaryByContentEncodings.GetContentEncodings%2A> e <xref:System.Web.HttpCacheVaryByContentEncodings.SetContentEncodings%2A>.

- 2 nuovi metodi nella classe <xref:System.Web.HttpCacheVaryByHeaders?displayProperty=fullName>: <xref:System.Web.HttpCacheVaryByHeaders.GetHeaders%2A> e <xref:System.Web.HttpCacheVaryByHeaders.SetHeaders%2A>.

- 2 nuovi metodi nella classe <xref:System.Web.HttpCacheVaryByParams?displayProperty=fullName>: <xref:System.Web.HttpCacheVaryByParams.GetParams%2A> e <xref:System.Web.HttpCacheVaryByParams.SetParams%2A>.

- Metodo <xref:System.Web.Caching.AggregateCacheDependency.GetFileDependencies%2A> nella classe <xref:System.Web.Caching.AggregateCacheDependency?displayProperty=fullName>.

- Metodo <xref:System.Web.Caching.CacheDependency.GetFileDependencies%2A> nella classe <xref:System.Web.Caching.CacheDependency>.

<a name="Strings"></a> 
### <a name="character-categories"></a>Categorie di caratteri
 I caratteri in [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] sono classificati in base allo [standard Unicode, versione 8.0.0](http://www.unicode.org/versions/Unicode8.0.0/). In [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] e [!INCLUDE[net_v461](../../../includes/net-v461-md.md)], i caratteri sono stati classificati in base alle categorie di caratteri Unicode 6.3.

 Il supporto per Unicode 8.0 è limitato alla classificazione dei caratteri tramite la classe <xref:System.Globalization.CharUnicodeInfo> e ai tipi e ai metodi basati sulla classe. Sono inclusi la classe <xref:System.Globalization.StringInfo>, il metodo di overload <xref:System.Char.GetUnicodeCategory%2A?displayProperty=fullName> e le [classi di caratteri](../../../docs/standard/base-types/character-classes-in-regular-expressions.md) riconosciute dal motore delle espressioni regolari di .NET Framework.  Il confronto e l'ordinamento di stringhe e caratteri non sono interessati da questa modifica e continuano a basarsi sul sistema operativo sottostante o, nei sistemi Windows 7, sui dati dei caratteri provenienti da .NET Framework.

 Per informazioni sulle modifiche nelle categorie di caratteri da Unicode 6.0 a Unicode 7.0, vedere [The Unicode Standard, Version 7.0.0](http://www.unicode.org/versions/Unicode7.0.0/) nel sito Web The Unicode Consortium. Per informazioni sulle modifiche da Unicode 7.0 a Unicode 8.0, vedere [The Unicode Standard, Version 8.0.0](http://www.unicode.org/versions/Unicode8.0.0/) nel sito Web The Unicode Consortium.

<a name="Crypto462"></a> 
### <a name="cryptography"></a>Crittografia
 **Supporto per i certificati X509 contenenti l'algoritmo di firma digitale (DSA) FIPS 186-3**
 [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] supporta ora i certificati DSA (Digital Signature Algorithm) X509 le cui chiavi superano il limite di 1024 bit specificato da FIPS 186-2.

 Oltre a supportare le dimensioni della chiave più grandi di FIPS 186-3, [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] consente di calcolare le firme con la famiglia SHA-2 di algoritmi hash (SHA256, SHA384 e SHA512). Il supporto per FIPS 186-3 viene fornito dalla nuova classe <xref:System.Security.Cryptography.DSACng?displayProperty=fullName>.

 In conformità alle recenti modifiche apportate alla classe <xref:System.Security.Cryptography.RSA> in .NET Framework 4.6 e alla classe <xref:System.Security.Cryptography.ECDsa> in .NET Framework 4.6.1, la classe base astratta <xref:System.Security.Cryptography.DSA> in [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] include altri metodi che permettono ai chiamanti di usare questa funzionalità senza eseguire il cast. È possibile chiamare il metodo di estensione <xref:System.Security.Cryptography.X509Certificates.DSACertificateExtensions.GetDSAPrivateKey%2A?displayProperty=fullName> per firmare i dati, come mostrato nell'esempio seguente.

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

 È anche possibile chiamare il metodo di estensione <xref:System.Security.Cryptography.X509Certificates.DSACertificateExtensions.GetDSAPublicKey%2A?displayProperty=fullName> per verificare i dati firmati, come mostrato nell'esempio seguente.

```csharp
public static bool VerifyDataDsaSha384(byte[] data, byte[] signature, X509Certificate2 cert)
{
    using (DSA dsa = cert.GetDSAPublicKey())
    {
        return dsa.VerifyData(data, signature, HashAlgorithmName.SHA384);
    }
}
```

```vb
 Public Shared Function VerifyDataDsaSha384(data As Byte(), signature As Byte(), cert As X509Certificate2) As Boolean
    Using dsa As DSA = cert.GetDSAPublicKey()
        Return dsa.VerifyData(data, signature, HashAlgorithmName.SHA384)
    End Using
End Function
```

 **Migliore chiarezza per gli input alle routine di derivazione della chiave ECDiffieHellman**
 .NET Framework 3.5 supporta ora la chiave concordata Ellipic Curve Diffie-Hellman con tre diverse routine di funzione di derivazione di chiave (KDF). Gli input per le routine, insieme alle routine stesse, sono stati configurati tramite proprietà nell'oggetto <xref:System.Security.Cryptography.ECDiffieHellmanCng>. Ma poiché non tutte le routine leggono tutte le proprietà di input, in passato era molto probabile che si creasse confusione per lo sviluppatore.

 Per gestire questo aspetto in [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], sono stati aggiunti i tre metodi seguenti alla classe base <xref:System.Security.Cryptography.ECDiffieHellman> per rappresentare in modo chiaro le routine di funzione di derivazione chiave e i rispettivi input:

|Metodo ECDiffieHellman|Descrizione|
|----------------------------|-----------------|
|<xref:System.Security.Cryptography.ECDiffieHellman.DeriveKeyFromHash%28System.Security.Cryptography.ECDiffieHellmanPublicKey%2CSystem.Security.Cryptography.HashAlgorithmName%2CSystem.Byte%5B%5D%2CSystem.Byte%5B%5D%29>|Deriva il materiale della chiave usando la formula<br /><br /> HASH(secretPrepend &#124;&#124; *x* &#124;&#124; secretAppend)<br /><br /> HASH(secretPrepend OrElse *x* OrElse secretAppend)<br /><br /> dove *x* è il risultato calcolato dell'algoritmo EC Diffie-Hellman.|
|<xref:System.Security.Cryptography.ECDiffieHellman.DeriveKeyFromHmac%28System.Security.Cryptography.ECDiffieHellmanPublicKey%2CSystem.Security.Cryptography.HashAlgorithmName%2CSystem.Byte%5B%5D%2CSystem.Byte%5B%5D%2CSystem.Byte%5B%5D%29>|Deriva il materiale della chiave usando la formula<br /><br /> HMAC(hmacKey, secretPrepend &#124;&#124; *x* &#124;&#124; secretAppend)<br /><br /> HMAC(hmacKey, secretPrepend OrElse *x* OrElse secretAppend)<br /><br /> dove *x* è il risultato calcolato dell'algoritmo EC Diffie-Hellman.|
|<xref:System.Security.Cryptography.ECDiffieHellman.DeriveKeyTls%28System.Security.Cryptography.ECDiffieHellmanPublicKey%2CSystem.Byte%5B%5D%2CSystem.Byte%5B%5D%29>|Deriva il materiale della chiave usando l'algoritmo di derivazione TLS della funzione pseudocasuale.|

 **Supporto per la crittografia simmetrica con chiave permanente**
 La libreria di crittografia di Windows (CNG) supporta ora l'archiviazione delle chiavi simmetriche persistenti e l'uso delle chiavi simmetriche archiviate nell'hardware e [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] rende possibile l'uso di questa funzionalità per gli sviluppatori.  Poiché le nozioni di nome della chiave e provider di chiavi sono specifiche dell'implementazione, questa funzionalità richiede l'uso del costruttore dei tipi di implementazione concreti anziché della modalità factory preferita, ad esempio la chiamata a `Aes.Create`.

 È stato aggiunto il supporto per la crittografia simmetrica con chiave persistente per gli algoritmi AES (<xref:System.Security.Cryptography.AesCng>) e 3DES (<xref:System.Security.Cryptography.TripleDESCng>). Ad esempio:

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

 **Supporto di SignedXml per creare hash SHA-2**
  [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] supporta la classe  <xref:System.Security.Cryptography.Xml.SignedXml> per i metodi di firma RSA-SHA256, RSA-SHA384 e RSA-SHA512 PKCS#1 e per gli algoritmi con classificazione di riferimento SHA256, SHA384 e SHA512.

 Le costanti URI sono tutte esposte in <xref:System.Security.Cryptography.Xml.SignedXml>:

|Campo SignedXml|Costante|
|---------------------|--------------|
|<xref:System.Security.Cryptography.Xml.SignedXml.XmlDsigSHA256Url>|"http://www.w3.org/2001/04/xmlenc#sha256"|
|<xref:System.Security.Cryptography.Xml.SignedXml.XmlDsigRSASHA256Url>|"http://www.w3.org/2001/04/xmldsig-more#rsa-sha256"|
|<xref:System.Security.Cryptography.Xml.SignedXml.XmlDsigSHA384Url>|"http://www.w3.org/2001/04/xmldsig-more#sha384"|
|<xref:System.Security.Cryptography.Xml.SignedXml.XmlDsigRSASHA384Url>|"http://www.w3.org/2001/04/xmldsig-more#rsa-sha384"|
|<xref:System.Security.Cryptography.Xml.SignedXml.XmlDsigSHA512Url>|"http://www.w3.org/2001/04/xmlenc#sha512"|
|<xref:System.Security.Cryptography.Xml.SignedXml.XmlDsigRSASHA512Url>|"http://www.w3.org/2001/04/xmldsig-more#rsa-sha512"|

 Qualsiasi programma che ha registrato un gestore <xref:System.Security.Cryptography.SignatureDescription> personalizzato in <xref:System.Security.Cryptography.CryptoConfig> per aggiungere il supporto per questi algoritmi continuerà a funzionare come in passato, ma poiché sono ora disponibili impostazioni predefinite per la piattaforma, la registrazione di <xref:System.Security.Cryptography.CryptoConfig> non è più necessaria.

<a name="SQLClient"></a> 
### <a name="sqlclient"></a>SqlClient
 Il provider di dati .NET Framework per SQL Server (<xref:System.Data.SqlClient?displayProperty=fullName>) include le nuove funzionalità seguenti in [!INCLUDE[net_v462](../../../includes/net-v462-md.md)]:

 **Pool e timeout di connessioni con i database di Azure SQL**
 Quando il pool di connessioni è abilitato e si verifica un timeout o un altro errore di accesso, viene memorizzata un'eccezione nella cache e tale eccezione viene generata ad ogni tentativo di connessione effettuato nei 5 secondi successivi fino a 1 minuto.  Per altre informazioni, vedere [Pool di connessioni SQL Server (ADO.NET)](../../../docs/framework/data/adonet/sql-server-connection-pooling.md).

 Questo comportamento è da evitare quando ci si connette ai database SQL di Azure, poiché i tentativi di connessione possono non riuscire per errori temporanei che in genere si risolvono rapidamente. Per ottimizzare l'esperienza dei tentativi di connessione, il comportamento del periodo di blocco del pool di connessioni viene rimosso quando le connessioni ai database SQL di Azure hanno esito negativo.

 L'aggiunta della nuova parola chiave `PoolBlockingPeriod` consente di selezionare il periodo di blocco più adatto per l'applicazione. I valori includono:

 `Auto`
 Il periodo di blocco del pool di connessioni per un'applicazione che si connette a un database di Azure SQL è disabilitato e il periodo di blocco del pool di connessioni per un'applicazione che si connette a qualsiasi altra istanza di SQL Server è abilitato. Rappresenta il valore predefinito. Se il nome dell'endpoint server termina in uno dei modi seguenti, vengono considerati i database SQL di Azure:

- .database.windows.net

- .database.chinacloudapi.cn

- .database.usgovcloudapi.net

- .database.cloudapi.de

 `AlwaysBlock` Il periodo di blocco del pool di connessioni è sempre abilitato.

 `NeverBlock` Il periodo di blocco del pool di connessioni è sempre disabilitato.

 **Miglioramenti per Always Encrypted** SQLClient introduce due miglioramenti per Always Encrypted:

- Per migliorare le prestazioni delle query con parametri su colonne di database crittografate, i metadati di crittografia per i parametri di query ora vengono memorizzati nella cache. Se quando la proprietà <xref:System.Data.SqlClient.SqlConnection.ColumnEncryptionQueryMetadataCacheEnabled%2A?displayProperty=fullName> è impostata su `true` (valore predefinito) viene chiamata la stessa query più volte, il client recupera i metadati dei parametri dal server solo una volta.

- Le voci delle chiavi di crittografia delle colonne nella cache delle chiavi vengono ora eliminate dopo un intervallo di tempo configurabile, impostato usando la proprietà <xref:System.Data.SqlClient.SqlConnection.ColumnEncryptionKeyCacheTtl%2A?displayProperty=fullName>.

<a name="WCF"></a> 
### <a name="windows-communication-foundation"></a>Windows Communication Foundation
 In [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] Windows Communication Foundation è stato ottimizzato nelle aree seguenti:

 **Supporto della sicurezza del trasporto WCF per i certificati archiviati tramite CNG**
 La sicurezza del trasporto WCF supporta i certificati archiviati tramite la libreria di crittografia di Windows (CNG). In [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] questo supporto è limitato all'utilizzo dei certificati con una chiave pubblica che ha un esponente di lunghezza non superiore a 32 bit. Quando un'applicazione ha come destinazione [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], questa funzionalità è attivata per impostazione predefinita.

 Per le applicazioni destinate a [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] e versioni precedenti, ma eseguite in [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], questa funzionalità può essere abilitata aggiungendo la riga seguente alla sezione [\<runtime>](../../../docs/framework/configure-apps/file-schema/runtime/runtime-element.md) del file app.config o web.config.

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

 **Migliore supporto per l'uso di più regole di adattamento all'ora legale tramite la classe DataContractJsonSerializer**
 I clienti possono ora usare un'impostazione di configurazione dell'applicazione per determinare se la classe <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> supporta più regole di adattamento per un fuso orario singolo. È una funzionalità che prevede il consenso esplicito. Per abilitarla aggiungere la seguente impostazione nel file di configurazione dell'applicazione:

```xml
<runtime>
     <AppContextSwitchOverrides value="Switch.System.Runtime.Serialization.DoNotUseTimeZoneInfo=false" />
</runtime>
```

Quando questa funzionalità è abilitata, un oggetto <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> usa il tipo <xref:System.TimeZoneInfo> invece del tipo <xref:System.TimeZone> per deserializzare i dati di data e ora. <xref:System.TimeZoneInfo> supporta più regole di regolazione, permettendo quindi di lavorare con dati cronologici relativi al fuso orario, diversamente da <xref:System.TimeZone> .

Per altre informazioni sulla struttura di <xref:System.TimeZoneInfo> e sulle regolazioni per il fuso orario, vedere [Panoramica sul fuso orario](../../../docs/standard/datetime/time-zone-overview.md).

**Supporto per mantenere un'ora UTC durante la serializzazione e la deserializzazione con la classe XMLSerializer** In genere, quando si usa la classe <xref:System.Xml.Serialization.XmlSerializer> per serializzare un valore <xref:System.DateTime> UTC, viene creata una stringa di data e ora serializzata che mantiene la data e l'ora, ma presuppone che l'ora sia locale.  Ad esempio, se si crea un'istanza di data e ora UTC chiamando il codice seguente:

```csharp
DateTime utc = new DateTime(2016, 11, 07, 3, 0, 0, DateTimeKind.Utc);
```

```vb
Dim utc As New Date(2016, 11, 07, 3, 0, 0, DateTimeKind.Utc)
```

Il risultato è la stringa di ora serializzata "03:00:00.0000000-08:00" per un sistema otto ore indietro rispetto all'ora UTC.  E i valori serializzati vengono sempre deserializzati come valori di data e ora locali.

 È possibile usare un'impostazione di configurazione dell'applicazione per determinare se <xref:System.Xml.Serialization.XmlSerializer> mantiene le informazioni sul fuso orario UTC durante la serializzazione e la deserializzazione di valori <xref:System.DateTime>:

```xml 
<runtime>
     <AppContextSwitchOverrides 
          value="Switch.System.Runtime.Serialization.DisableSerializeUTCDateTimeToTimeAndDeserializeUTCTimeToUTCDateTime=false" />
</runtime>
```

Quando questa funzionalità è abilitata, un oggetto <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> usa il tipo <xref:System.TimeZoneInfo> invece del tipo <xref:System.TimeZone> per deserializzare i dati di data e ora. <xref:System.TimeZoneInfo> supporta più regole di regolazione, permettendo quindi di lavorare con dati cronologici relativi al fuso orario, diversamente da <xref:System.TimeZone> .

Per altre informazioni sulla struttura di <xref:System.TimeZoneInfo> e sulle regolazioni per il fuso orario, vedere [Panoramica sul fuso orario](../../../docs/standard/datetime/time-zone-overview.md).

 **Migliore corrispondenza di NetNamedPipeBinding**
 WCF offre una nuova impostazione per le app, che può essere configurata nelle applicazioni client per garantire sempre la connessione al servizio in ascolto sull'URI che corrisponde meglio a quello richiesto dalle applicazioni. Con questa impostazione dell'app configurata su `false` (valore predefinito), i client che usano <xref:System.ServiceModel.NetNamedPipeBinding> sono in grado di tentare la connessione a un servizio in ascolto su un URI che è una sottostringa dell'URI richiesto.

 Ad esempio, un client tenta di connettersi a un servizio in ascolto su `net.pipe://localhost/Service1`, ma un altro servizio in esecuzione nello stesso computer con privilegi di amministratore è in ascolto su `net.pipe://localhost`. Con l'impostazione di applicazione impostata su `false`, il client tenterebbe di connettersi al servizio errato. Dopo aver impostato l'impostazione di applicazione su `true`, il client si connetterà sempre al servizio più pertinente.

> [!NOTE]
>  I client che usano <xref:System.ServiceModel.NetNamedPipeBinding> trovano i servizi in base all'indirizzo di base del servizio (se esistente), invece che all'indirizzo completo dell'endpoint. Per assicurarsi che l'impostazione funzioni sempre, il servizio deve usare un indirizzo di base univoco.

 Per abilitare questa modifica, aggiungere la seguente impostazione di applicazione al file di configurazione dell'applicazione o del Web dell'applicazione client:

```xml
<configuration>
    <appSettings>
        <add key="wcf:useBestMatchNamedPipeUri" value="true" />
    </appSettings>
</configuration>
```

 **SSL 3.0 non è un protocollo predefinito**
 Quando si usa NetTcp con la sicurezza di trasporto e un tipo di credenziali di certificato, SSL 3.0 non è più un protocollo predefinito usato per negoziare una connessione protetta. Nella maggior parte dei casi non vi sarà alcun impatto sulle applicazioni esistenti, poiché TLS 1.0 è incluso nell'elenco di protocolli per NetTcp. Tutti i client esistenti devono essere in grado di negoziare una connessione usando almeno TLS 1.0.      Se è necessario il protocollo Ssl3, usare uno dei meccanismi di configurazione seguenti per aggiungerlo all'elenco dei protocolli negoziati.

- Proprietà <xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement.SslProtocols%2A?displayProperty=fullName>

- Proprietà <xref:System.ServiceModel.TcpTransportSecurity.SslProtocols%2A?displayProperty=fullName>

- Sezione [\<transport>](../../../docs/framework/configure-apps/file-schema/wcf/transport-of-nettcpbinding.md) della sezione [\<netTcpBinding>](../../../docs/framework/configure-apps/file-schema/wcf/nettcpbinding.md)

- Sezione [\<sslStreamSecurity>](../../../docs/framework/configure-apps/file-schema/wcf/sslstreamsecurity.md) della sezione [\<customBinding>](../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md)

<a name="WPF462"></a> 
### <a name="windows-presentation-foundation-wpf"></a>Windows Presentation Foundation (WPF)
 In [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] Windows Presentation Foundation è stato ottimizzato nelle aree seguenti:

 **Ordinamento dei gruppi**
 Un'applicazione che usa un oggetto <xref:System.Windows.Data.CollectionView> per raggruppare dati può ora dichiarare in modo esplicito l'ordinamento dei gruppi. L'ordinamento esplicito risolve il problema dell'ordinamento non intuitivo che si verifica quando un'applicazione aggiunge o rimuove in modo dinamico i gruppi o quando modifica il valore delle proprietà dell'elemento interessate dal raggruppamento. Può anche migliorare le prestazioni del processo di creazione dei gruppi spostando i confronti delle proprietà di raggruppamento dall'ordinamento della raccolta completa all'ordinamento dei gruppi.

 Per supportare l'ordinamento dei gruppi, le nuove proprietà <xref:System.ComponentModel.GroupDescription.SortDescriptions%2A?displayProperty=fullName> e <xref:System.ComponentModel.GroupDescription.CustomSort%2A?displayProperty=fullName> descrivono come ordinare la raccolta di gruppi prodotta dall'oggetto <xref:System.ComponentModel.GroupDescription>. Questo comportamento è analogo al modo in cui le proprietà <xref:System.Windows.Data.ListCollectionView> omonime descrivono come ordinare gli elementi di dati.

 Per la maggior parte dei casi è possibile usare due nuove proprietà statiche della classe <xref:System.Windows.Data.PropertyGroupDescription>: <xref:System.Windows.Data.PropertyGroupDescription.CompareNameAscending%2A> e <xref:System.Windows.Data.PropertyGroupDescription.CompareNameDescending%2A>.

 Ad esempio, il seguente XAML raggruppa i dati in base all'età, ordina i gruppi di età in ordine crescente e raggruppa gli elementi all'interno di ogni gruppo di età in base al cognome.

```xaml
<GroupDescriptions>
     <PropertyGroupDescription 
         PropertyName=”Age” 
         CustomSort= 
              ”{x:Static PropertyGroupDescription.CompareNamesAscending}”/>
     </PropertyGroupDescription>
</GroupDescriptions>

<SortDescriptions>
     <SortDescription PropertyName=”LastName”/>
</SortDescriptions>
```

 **Supporto per la tastiera su schermo**
 Il supporto per la tastiera su schermo consente di rilevare lo stato attivo nelle applicazioni WPF chiamando e chiudendo automaticamente la nuova tastiera su schermo in Windows 10 quando l'input tocco viene ricevuto da un controllo in grado di accettare input testuale.

 Nelle versioni precedenti di .NET Framework, non è possibile attivare il rilevamento dello stato attivo nelle applicazioni WPF senza disabilitare il supporto WPF per il rilevamento dei movimenti di tocco e penna.  Di conseguenza, le applicazioni WPF devono scegliere tra il supporto completo WPF per il tocco e la promozione del mouse di Windows.

 **Valori DPI del monitor**
 Per supportare la recente proliferazione di ambienti a DPI elevato e a risoluzione ibrida per le app WPF, WPF in [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] consente di abilitare la sensibilità ai valori del monitor. Per altre informazioni su come abilitare l'app WPF per la sensibilità ai valori DPI del monitor, vedere gli [esempi e la guida per gli sviluppatori](https://github.com/Microsoft/WPF-Samples/tree/master/PerMonitorDPI) su GitHub.

 Nelle versioni precedenti di .NET Framework, le applicazioni WPF sono compatibili con i valori DPI del sistema. In altre parole, l'interfaccia utente dell'applicazione viene adeguata in modo appropriato dal sistema operativo, in base alla risoluzione del monitor in cui viene eseguito il rendering dell'applicazione. ,

 Per le app eseguite in [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], è possibile disabilitare le modifiche dei valori DPI per monitor nelle app WPF aggiungendo un'istruzione di configurazione alla sezione [\<runtime>](../../../docs/framework/configure-apps/file-schema/runtime/runtime-element.md) del file di configurazione dell'applicazione in questo modo:

```xml
<runtime>
   <AppContextSwitchOverrides value=”Switch.System.Windows.DoNotScaleForDpiChanges=false”/>
</runtime>
```

<a name="WF462"></a> 
### <a name="windows-workflow-foundation-wf"></a>Windows Workflow Foundation (WF)
 In [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] Windows Workflow Foundation è stato ottimizzato nell'area seguente:

 **Supporto per espressioni C# e IntelliSense nella progettazione di WF riallocata**
 A partire da [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], WF supporta espressioni C# nella finestra di progettazione di Visual Studio e nei flussi di lavoro con codice. La riallocazione della progettazione del flusso di lavoro è una funzionalità chiave di WF che consente di usare la finestra di progettazione del flusso di lavoro in un'applicazione esterna a Visual Studio, ad esempio WPF.  Windows Workflow Foundation offre la possibilità di supportare le espressioni C# e IntelliSense nell'utilità di progettazione del flusso di lavoro riallocata. Per altre informazioni, vedere il [blog di Windows Workflow Foundation](http://go.microsoft.com/fwlink/?LinkID=809042&clcid=0x409).

 `Availability of IntelliSense when a customer rebuilds a workflow project from Visual Studio`
 Nelle versioni di .NET Framework precedenti a [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], IntelliSense viene interrotta nella finestra di progettazione del flusso di lavoro quando un cliente ricompila un progetto di flusso di lavoro da Visual Studio. Anche se la compilazione del progetto ha esito positivo, i tipi di flusso di lavoro non vengono trovati nell'utilità di progettazione e vengono visualizzati alcuni avvisi di IntelliSense per i tipi di flusso di lavoro mancanti nella finestra **Elenco errori**. [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] risolve questo problema e rende disponibile IntelliSense.

 **Le applicazioni del flusso di lavoro V1 con la tracciabilità flusso di lavoro attivata vengono ora eseguite in modalità FIPS**
 I computer con modalità di compatibilità FIPS abilitata sono ora in grado di eseguire correttamente un'applicazione di flusso di lavoro tipo versione 1 con la tracciabilità flusso di lavoro attivata. Per abilitare questo scenario, è necessario apportare le modifiche seguenti al file di configurazione dell'applicazione:

```xml
<add key="microsoft:WorkflowRuntime:FIPSRequired" value="true" />
```

 Se questo scenario non è abilitato, eseguire l'applicazione continua a generare un'eccezione con il messaggio "Questa implementazione non fa parte degli algoritmi crittografici convalidati per Windows Platform FIPS".

 **Miglioramenti del flusso di lavoro quando si usa l'aggiornamento dinamico con la progettazione flussi di lavoro di Visual Studio**
 La Progettazione flussi di lavoro, ActivityDesigner Diagramma di flusso e gli altri strumenti di progettazione delle attività dei flussi di lavoro caricano e visualizzano correttamente i flussi di lavoro che sono stati salvati dopo la chiamata del metodo <xref:System.Activities.DynamicUpdate.DynamicUpdateServices.PrepareForUpdate%2A?displayProperty=fullName>. Nelle versioni di .NET Framework precedenti a [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] il caricamento di un file XAML in Visual Studio per un flusso di lavoro salvato dopo la chiamata di <xref:System.Activities.DynamicUpdate.DynamicUpdateServices.PrepareForUpdate%2A?displayProperty=fullName> può causare i problemi seguenti:

- Progettazione flussi di lavoro non è in grado di caricare correttamente il file XAML (quando <xref:System.Activities.Presentation.ViewState.ViewStateData.Id%2A?displayProperty=fullName> si trova alla fine della riga).

- ActivityDesigner Diagramma di flusso o altri ActivityDesigner del flusso di lavoro possono visualizzare tutti gli oggetti nei propri percorsi predefiniti anziché i valori della proprietà associata.

<a name="ClickOnce"></a> 
### <a name="clickonce"></a>ClickOnce
 ClickOnce è stato aggiornato per supportare TLS 1.1 e TLS 1.2 oltre al protocollo 1.0 che supporta già. ClickOnce rileva automaticamente il protocollo richiesto e non sono necessarie altre operazioni nell'applicazione ClickOnce per abilitare il supporto per TLS 1.1 e 1.2.

<a name="UWPConvert"></a> 
### <a name="converting-windows-forms-and-wpf-apps-to--uwp-apps"></a>Conversione di Windows Form e applicazioni WPF in applicazioni UWP
 Windows ora offre funzionalità che consentono di portare le applicazioni desktop Windows esistenti, incluse le applicazioni WPF e Windows Form, sulla piattaforma UWP (Universal Windows Platform). Questa tecnologia funge da ponte e consente di eseguire gradualmente la migrazione della codebase esistente a UWP, rendendo in tal modo l'applicazione disponibile in tutti i dispositivi Windows 10.

 Le applicazioni desktop convertite ottengono un'identità di applicazione simile a quella delle applicazioni UWP e in questo modo le API UWP diventano accessibili per abilitare funzionalità come i riquadri animati e le notifiche. L'applicazione continua a comportarsi come in precedenza e viene eseguita come applicazione con attendibilità totale. Dopo avere convertito l'applicazione, è possibile aggiungere un processo contenitore di applicazioni al processo di attendibilità totale esistente per aggiungere un'interfaccia utente adattiva. Quando tutte le funzionalità vengono spostate nel processo contenitore di applicazioni, il processo di attendibilità totale può essere rimosso e la nuova applicazione UWP può essere resa disponibile per tutti i dispositivi Windows 10.

<a name="Debug462"></a> 
### <a name="debugging-improvements"></a>Miglioramenti apportati al debug
 L'*API di debug non gestito* è stata ottimizzata in [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] per l'esecuzione di un'analisi aggiuntiva quando viene generata un'eccezione <xref:System.NullReferenceException>, in modo che sia possibile determinare quale variabile in una singola riga di codice sorgente è `null`.   A supporto di questo scenario, le API seguenti sono state aggiunte all'API di debug non gestito.

- Interfacce [ICorDebugCode4](../../../docs/framework/unmanaged-api/debugging/icordebugcode4-interface.md), [ICorDebugVariableHome](../../../docs/framework/unmanaged-api/debugging/icordebugvariablehome-interface.md) e [ICorDebugVariableHomeEnum](../../../docs/framework/unmanaged-api/debugging/icordebugvariablehomeenum-interface.md), che espongono le posizioni native delle variabili gestite. Questo permette ai debugger di eseguire alcune analisi del flusso di codice quando viene generata un'eccezione <xref:System.NullReferenceException> e di eseguire un controllo a ritroso per determinare quale variabile gestita corrispondente alla posizione nativa è `null`.

- Il metodo [ICorDebugType2::GetTypeID](../../../docs/framework/unmanaged-api/debugging/icordebugtype2-gettypeid-method.md) fornisce un mapping per ICorDebugType a [COR_TYPEID](../../../docs/framework/unmanaged-api/debugging/cor-typeid-structure.md), che permette al debugger di ottenere un oggetto [COR_TYPEID](../../../docs/framework/unmanaged-api/debugging/cor-typeid-structure.md) senza un'istanza di ICorDebugType. È quindi possibile usare le API esistenti in [COR_TYPEID](../../../docs/framework/unmanaged-api/debugging/cor-typeid-structure.md) per determinare il layout di classe del tipo.

<a name="v461"></a> 
## <a name="whats-new-in-the-net-framework-461"></a>Novità di .NET Framework 4.6.1
 [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] include nuove funzionalità nelle aree seguenti:

- [Crittografia](#Crypto)

- [ADO.NET](#ADO.NET461)

- [Windows Presentation Foundation (WPF)](#WPF461)

- [Windows Workflow Foundation](#WWF461)

- [Profilatura](#Profile461)

- [NGen](#NGEN461)

 Per altre informazioni su [!INCLUDE[net_v461](../../../includes/net-v461-md.md)], vedere gli argomenti seguenti:

- [Elenco delle modifiche di .NET Framework 4.6.1](http://go.microsoft.com/fwlink/?LinkId=622964)

- [Compatibilità delle applicazioni nella versione 4.6.1](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-6-1.md)

- [Differenze nell'API di .NET Framework](http://go.microsoft.com/fwlink/?LinkId=622989) (su GitHub)

<a name="Crypto"></a> 
### <a name="cryptography-support-for-x509-certificates-containing-ecdsa"></a>Crittografia: supporto di certificati X509 contenenti ECDSA
 In .NET Framework 4.6 è stato aggiunto il supporto RSACng per i certificati X509. [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] aggiunge il supporto di certificati X509 con ECDSA (Elliptic Curve Digital Signature Algorithm).

 Offrendo prestazioni migliori e trattandosi di un algoritmo di crittografia più sicuro rispetto a RSA, ECDSA rappresenta un'ottima scelta per ambienti in cui la scalabilità e le prestazioni TLS (Transport Layer Security) sono fattori importanti. L'implementazione di .NET Framework esegue il wrapping delle chiamate nelle funzionalità di Windows esistenti.

 L'esempio di codice seguente illustra quanto sia semplice generare una firma per un flusso di byte usando il nuovo supporto dei certificati X509 ECDSA incluso in [!INCLUDE[net_v461](../../../includes/net-v461-md.md)].

 [!code-csharp[whatsnew.461.crypto#1](../../../samples/snippets/csharp/VS_Snippets_CLR/whatsnew.461.crypto/cs/Code46.cs#1)] [!code-vb[whatsnew.461.crypto#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/whatsnew.461.crypto/vb/Code461.vb#1)]

 Emerge una netta differenza rispetto al codice necessario per generare una firma in .NET Framework 4.6.

 [!code-csharp[whatsnew.461.crypto#2](../../../samples/snippets/csharp/VS_Snippets_CLR/whatsnew.461.crypto/cs/Code46.cs#2)] [!code-vb[whatsnew.461.crypto#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/whatsnew.461.crypto/vb/Code46.vb#2)]

<a name="ADO.NET461"></a> 
### <a name="adonet"></a>ADO.NET
 In ADO.NET è stato aggiunto quanto segue:

 Supporto di Always Encrypted per le chiavi protette da hardware ADO.NET supporta ora l'archiviazione delle chiavi master di colonna di Always Encrypted in modo nativo in moduli di protezione hardware (HSM). Grazie a questo supporto, i clienti possono usare le chiavi asimmetriche archiviate nei moduli di protezione hardware senza dover scrivere provider dell'archivio chiavi master di colonna personalizzati e senza doverli registrare nelle applicazioni.

 I clienti devono installare il provider CSP fornito dal fornitore dei moduli di protezione hardware o i provider dell'archivio chiavi CNG nei server applicazioni o nei computer client per accedere ai dati con Crittografia sempre attiva protetti con le chiavi master di colonna archiviate in un modulo di protezione hardware.

 Migliore comportamento di connessione di <xref:System.Data.SqlClient.SqlConnectionStringBuilder.MultiSubnetFailover%2A> per AlwaysOn SqlClient offre ora automaticamente una connessione più veloce a un gruppo di disponibilità AlwaysOn (AG). Rileva in modo trasparente se l'applicazione si connette a un gruppo di disponibilità AlwaysOn su una subnet diversa e individua rapidamente il server attivo corrente e gli fornisce una connessione. Prima di questa versione, un'applicazione doveva impostare la stringa di connessione in modo da includere `“MultisubnetFailover=true”` per indicare che era connessa a un gruppo di disponibilità AlwaysOn. Senza impostare la parola chiave di connessione su `true`, potrebbe verificarsi un timeout durante la connessione di un'applicazione a un gruppo di disponibilità AlwaysOn. Con questa versione, un'applicazione *non* deve più impostare <xref:System.Data.SqlClient.SqlConnectionStringBuilder.MultiSubnetFailover%2A> su `true`. Per altre informazioni sul supporto SqlClient per gruppi di disponibilità Always On, vedere [Supporto SqlClient per disponibilità elevata, ripristino di emergenza](../../../docs/framework/data/adonet/sql/sqlclient-support-for-high-availability-disaster-recovery.md).

<a name="WPF461"></a> 
### <a name="windows-presentation-foundation-wpf"></a>Windows Presentation Foundation (WPF)
 Windows Presentation Foundation include molti miglioramenti e cambiamenti.

 Migliori prestazioni Il ritardo nell'esecuzione di eventi tocco è stato risolto in [!INCLUDE[net_v461](../../../includes/net-v461-md.md)]. Inoltre, l'immissione di un controllo <xref:System.Windows.Controls.RichTextBox> non blocca più il thread di rendering durante l'input veloce.

 Controllo ortografia più efficiente Il correttore ortografico di WPF è stato aggiornato a Windows 8.1 e versioni successive per usufruire del supporto del sistema operativo per il controllo ortografia di lingue aggiuntive.  La funzionalità non è stata modificata nelle versioni di Windows precedenti a Windows 8.1.

 Come nelle versioni precedenti di .NET Framework, la lingua per un controllo <xref:System.Windows.Controls.TextBox> o un blocco <xref:System.Windows.Controls.RichTextBox> viene rilevata cercando le informazioni nell'ordine seguente:

- `xml:lang`, se presente.

- Lingua di input corrente.

- Impostazioni cultura del thread corrente.

 Per altre informazioni sul supporto delle lingue in WPF, vedere il [post di blog di WPF sulle funzionalità di .NET Framework 4.6.1](http://go.microsoft.com/fwlink/?LinkID=691819).

 Supporto aggiuntivo per i dizionari personalizzati per utente In [!INCLUDE[net_v461](../../../includes/net-v461-md.md)], WPF riconosce i dizionari personalizzati registrati a livello globale. Questa funzionalità si aggiunge alla possibilità di registrarli a livello di controllo.

 Nelle versioni precedenti di WPF, i dizionari personalizzati non riconoscono le parole escluse e gli elenchi di correzione automatica. Sono supportati in Windows 8.1 e Windows 10 mediante l'uso di file che possono essere inseriti nella directory `%AppData%\Microsoft\Spelling\<language tag>`.  A questi file si applicano le regole seguenti:

- I file devono avere estensione dic (per le parole aggiunte), exc (per le parole escluse) o acl (per la correzione automatica).

- I file devono essere in testo normale UTF-16 LE che inizia con l'indicatore dell'ordine dei byte (BOM, Byte Order Mark).

- Ogni riga deve essere costituita da una parola (negli elenchi di parole aggiunte ed escluse) o da una coppia di correzione automatica con le parole separate da una barra verticale ("&#124;") (nell'elenco di parole della correzione automatica).

- Questi file sono considerati di sola lettura e non vengono modificati dal sistema.

> [!NOTE]
>  Questi nuovi formati di file non sono supportati direttamente dalle API di controllo ortografico WPF e i dizionari personalizzati forniti a WPF nelle applicazioni devono continuare a usare i file con estensione lex.

 Esempi In MSDN sono disponibili diversi [esempi di WPF](https://msdn.microsoft.com/library/ms771633.aspx). Più di 200 degli esempi più comuni (in base all'utilizzo) verranno spostati in un [archivio GitHub open source](https://github.com/Microsoft/WPF-Samples). Per aiutare Microsoft a migliorare gli esempi, inviare una richiesta di pull o segnalare un [problema di GitHub](https://github.com/Microsoft/WPF-Samples/issues).

 Estensioni di DirectX WPF include un [pacchetto NuGet](http://go.microsoft.com/fwlink/?LinkID=691342) che offre nuove implementazioni di <xref:System.Windows.Interop.D3DImage> per semplificare l'interazione con contenuto DX10 e Dx11. Il codice per questo pacchetto è stato reso open source ed è disponibile su [GitHub](https://github.com/Microsoft/WPFDXInterop).

<a name="WWF461"></a> 
### <a name="windows-workflow-foundation-transactions"></a>Windows Workflow Foundation: Transazioni
 Il metodo <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A?displayProperty=fullName> può ora usare uno strumento di gestione transazioni distribuite diverso da MSDTC per alzare di livello la transazione. A questo scopo, specificare l'identificatore di un promotore di transazione GUID per il nuovo overload <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%28System.Transactions.IPromotableSinglePhaseNotification%2CSystem.Guid%29?displayProperty=fullName>. Se l'operazione riesce, le funzionalità della transazione sono soggette a limitazioni. Quando viene integrato un promotore di transazione non MSDTC, i metodi seguenti generano un'eccezione <xref:System.Transactions.TransactionPromotionException>, perché questi metodi richiedono l'innalzamento di livello a MSDTC:

- <xref:System.Transactions.Transaction.EnlistDurable%2A?displayProperty=fullName>

- <xref:System.Transactions.TransactionInterop.GetDtcTransaction%2A?displayProperty=fullName>

- <xref:System.Transactions.TransactionInterop.GetExportCookie%2A?displayProperty=fullName>

- <xref:System.Transactions.TransactionInterop.GetTransmitterPropagationToken%2A?displayProperty=fullName>

 Quando viene integrato un promotore di transazione non MSDTC, occorre usarlo per le future integrazioni durevoli usando i protocolli che definisce. L'identificatore <xref:System.Guid> del promotore di transazione può essere ottenuto usando la proprietà <xref:System.Transactions.Transaction.PromoterType%2A>. Quando la transazione viene innalzata di livello, il promotore di transazione fornisce una matrice <xref:System.Byte> che rappresenta il token innalzato di livello. Un'applicazione può ottenere il token innalzato di livello per una transazione non MSDTC innalzata di livello con il metodo <xref:System.Transactions.Transaction.GetPromotedToken%2A>.

 Gli utenti del nuovo overload <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%28System.Transactions.IPromotableSinglePhaseNotification%2CSystem.Guid%29?displayProperty=fullName> devono seguire una sequenza di chiamata specifica perché l'operazione di promozione venga eseguita correttamente. Queste regole sono descritte nella documentazione relativa al metodo.

<a name="Profile461"></a> 
### <a name="profiling"></a>Profilatura
 L'API di profilatura non gestita è stata migliorata nel modo seguente:

 Migliore supporto per l'accesso ai file PDB nell'interfaccia [ICorProfilerInfo7](../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo7-interface.md) In ASP.Net 5, sta diventando prassi comune compilare gli assembly in memoria tramite Roslyn. Per gli sviluppatori che creano strumenti di profilatura, ciò significa che i PDB che in passato erano serializzati sul disco potrebbero non essere più presenti. Gli strumenti profiler spesso usano PDB per rimappare il codice alle righe di origine per attività come il code coverage o l'analisi delle prestazioni riga per riga. L'interfaccia [ICorProfilerInfo7](../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo7-interface.md) include ora due nuovi metodi, [ICorProfilerInfo7::GetInMemorySymbolsLength](../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo7-getinmemorysymbolslength-method.md) e [ICorProfilerInfo7::ReadInMemorySymbols](../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo7-readinmemorysymbols.md), per fornire a questi strumenti profiler l'accesso ai dati dei PDB in memoria. Usando le nuove API, un profiler può ottenere il contenuto di un PDB in memoria come matrice di byte e quindi elaborarlo o serializzarlo su disco.

 Migliore strumentazione con l'interfaccia ICorProfiler I profiler che usano la funzionalità ReJit dell'API `ICorProfiler` per la strumentazione dinamica possono ora modificare alcuni metadati. In precedenza quegli strumenti potevano instrumentare IL in qualsiasi momento, ma i metadati potevano essere modificati solo in fase di caricamento del modulo. Poiché IL fa riferimento ai metadati, questo limitava i tipi di strumentazione possibile. Alcuni di questi limiti sono stati innalzati aggiungendo il metodo [ICorProfilerInfo7::ApplyMetaData](../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo7-applymetadata-method.md) per supportare un subset di modifiche ai metadati dopo il caricamento del modulo, in particolare aggiungendo nuovi record `AssemblyRef`, `TypeRef`, `TypeSpec`, `MemberRef`, `MemberSpec` e `UserString`. Questa modifica rende possibile una gamma più ampia di strumentazioni immediate.

<a name="NGEN461"></a> 
### <a name="native-image-generator-ngen-pdbs"></a>PDB del generatore di immagini native (NGEN)
 La traccia eventi tra computer consente ai clienti di profilare un programma sul Computer A e osservare i dati di profilatura con mapping della riga di origine sul Computer B. Nelle versioni precedenti di .NET Framework, l'utente copiava tutti i moduli e le immagini native dalla macchina profilata alla macchina di analisi contenente il PDB IL per creare il mapping sorgente-nativo. Anche se questo processo può funzionare bene quando i file sono relativamente piccoli, ad esempio per le applicazioni telefoniche, i file possono avere dimensioni molto grandi sui sistemi desktop e la copia può richiedere molto tempo.

 Con i PDB Ngen, NGen può creare un PDB che contiene il mapping da IL a nativo senza una dipendenza dal PDB IL. In questo scenario di traccia eventi in più computer, è sufficiente copiare il PDB di immagine nativa generato dal Computer A nel Computer B e usare le [API di accesso all'interfaccia di debug](https://msdn.microsoft.com/library/ee8x173s.aspx) per leggere il mapping da codice sorgente a codice IL del PDB IL e il mapping da codice IL a codice nativo del PDB di immagine nativa. La combinazione di entrambi i mapping fornisce un mapping da codice sorgente a codice nativo. Poiché il PDB di immagine nativa è molto più piccolo rispetto a tutti i moduli e alle immagini native, il processo di copia dal Computer A al Computer B è molto più veloce.

<a name="v46"></a> 
## <a name="whats-new-in-net-2015"></a>Novità di .NET 2015
 .NET 2015 introduce [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] e .NET Core. Alcune nuove funzionalità sono valide per entrambi, mentre altre sono specifiche di [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] o [!INCLUDE[net_core](../../../includes/net-core-md.md)].

- **ASP.NET 5**

     .NET 2015 include ASP.NET 5, una piattaforma .NET snella per la compilazione di app moderne basate su cloud. Si tratta di una piattaforma modulare che consente di includere solo le funzionalità necessarie nell'applicazione. Può essere ospitata su IIS o in modo indipendente in un processo personalizzato ed è possibile eseguire app con diverse versioni di .NET Framework nello stesso server. Include un nuovo sistema di configurazione dell'ambiente progettato per la distribuzione cloud.

     MVC, API Web e pagine Web sono riunite in un unico framework denominato MVC 6. Le app ASP.NET 5 vengono compilate mediante i nuovi strumenti in Visual Studio 2015. Le applicazioni esistenti funzioneranno nel nuovo .NET Framework ma per compilare un'app che usa MVC 6 o SignalR 3 è necessario usare il sistema di progetto in Visual Studio 2015.

     Per informazioni, vedere [ASP.NET 5](http://go.microsoft.com/fwlink/?LinkId=518238).

- **Aggiornamenti di ASP.NET**

    - **API basata su attività per lo scaricamento asincrono delle risposte**

         ASP.NET fornisce ora la semplice API basata su attività <xref:System.Web.HttpResponse.FlushAsync%2A?displayProperty=fullName>, che permette lo scaricamento asincrono delle risposte tramite il supporto `async/await` del linguaggio usato.

    - `Model binding supports task-returning methods`

         In [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] ASP.NET ha aggiunto la funzionalità di associazione di modelli che ha reso possibile un approccio estendibile, focalizzato sul codice, per le operazioni di dati basate su CRUD nelle pagine Web Form e nei controlli utente. Il sistema di associazione di modelli supporta ora metodi di associazione di modelli che restituiscono <xref:System.Threading.Tasks.Task>. Questa funzionalità consente agli sviluppatori di Web Form di ottenere i vantaggi di scalabilità di async con la facilità del sistema di associazione dati quando usano versioni più recenti di ORM, tra cui Entity Framework.

         L'associazione di modelli async è controllata dall'impostazione di configurazione `aspnet:EnableAsyncModelBinding`.

        ```
        <appSettings>
           <add key=" aspnet:EnableAsyncModelBinding" value="true|false" />
        </appSettings>
        ```

         Per le app destinate a [!INCLUDE[net_v46](../../../includes/net-v46-md.md)], l'impostazione predefinita è `true`. Per le app in esecuzione su [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] e che sono destinate a una versione precedente di .NET Framework, è `false` per impostazione predefinita. Può essere abilitata impostando l'impostazione di configurazione su `true`.

    - **Supporto HTTP/2 (Windows 10)**

         [HTTP/2](http://www.wikipedia.org/wiki/HTTP/2) è una nuova versione del protocollo HTTP che permette un utilizzo molto migliore della connessione, con meno round trip tra client e server, offrendo una latenza minore per il caricamento delle pagine Web per gli utenti.  Le pagine Web (a differenza dei servizi) traggono maggiori vantaggi dal protocollo HTTP/2, poiché ottimizza più elementi richiesti come parte di un'esperienza unica. Il supporto HTTP/2 è stato aggiunto ad ASP.NET in .NET Framework 4.6. Poiché la funzionalità di rete esiste a più livelli, si sono rese necessarie nuove funzionalità in Windows, IIS e ASP.NET per abilitare HTTP/2. È necessario eseguire Windows 10 per usare HTTP/2 con ASP.NET.

         HTTP/2 è anche supportato e attivato per impostazione predefinita per le app UWP (Universal Windows Platform) per Windows 10 che usano l'API <xref:System.Net.Http.HttpClient?displayProperty=fullName>.

         Per permettere l'uso della funzionalità [PUSH_PROMISE](http://http2.github.io/http2-spec/#PUSH_PROMISE) in applicazioni ASP.NET, è stato aggiunto un nuovo metodo con due overload, <xref:System.Web.HttpResponse.PushPromise%28System.String%29> e <xref:System.Web.HttpResponse.PushPromise%28System.String%2CSystem.String%2CSystem.Collections.Specialized.NameValueCollection%29>, alla classe <xref:System.Web.HttpResponse>.

        > [!NOTE]
        >  Mentre ASP.NET 5 supporta HTTP/2, il supporto della funzionalità PUSH PROMISE non è ancora stato aggiunto.

         Il browser e il server Web (IIS su Windows) eseguono tutte le operazioni. Gli utenti non dovranno eseguire alcuna operazione impegnativa.

         Poiché la maggior parte dei [principali browser supporta HTTP/2](http://www.wikipedia.org/wiki/HTTP/2), è probabile che gli utenti trarranno vantaggio dal supporto HTTP/2, se supportato dal server in uso.

    - **Supporto per Token Binding Protocol**

         Microsoft e Google stanno collaborando a un nuovo approccio all'autenticazione, chiamato [Token Binding Protocol](https://github.com/TokenBinding/Internet-Drafts). Il presupposto è che i token di autenticazione (nella cache del browser) possono essere rubati e usati da utenti malintenzionati per accedere a risorse altrimenti sicure, ad esempio un conto bancario, senza richiedere la password o altre informazioni riservate. L'obiettivo del nuovo protocollo è attenuare questo problema.

         Il Token Binding Protocol verrà implementato in Windows 10 come funzionalità del browser. Le app ASP.NET parteciperanno al protocollo, in modo che sia convalidata la legittimità dei token di autenticazione. Le implementazioni di client e server stabiliscono la protezione end-to-end specificata dal protocollo.

    - **Algoritmi hash casuali per le stringhe**

         In .NET Framework 4.5 è stato introdotto un [algoritmo hash casuale per le stringhe](../configure-apps/file-schema/runtime/userandomizedstringhashalgorithm-element.md). Tuttavia, non era supportato da ASP.NET perché alcune funzionalità ASP.NET dipendevano da un codice hash stabile. In [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] gli algoritmi di hash della stringa casuale sono ora supportati. Per abilitare questa funzionalità, usare l'impostazione di configurazione `aspnet:UseRandomizedStringHashAlgorithm`.

        ```
        <appSettings>
           <add key="aspnet:UseRandomizedStringHashAlgorithm" value="true|false" />
        </appSettings>
        ```

- **ADO.NET**

     ADO .NET supporta ora la funzionalità Crittografia sempre attiva disponibile in SQL Server 2016 Community Technology Preview 2 (CTP2). Con Crittografia sempre attiva, SQL Server può eseguire operazioni su dati crittografati e, soprattutto, la chiave di crittografia risiede con l'applicazione all'interno dell'ambiente attendibile del cliente e non sul server. Crittografia sempre attiva protegge i dati dei clienti in modo che gli amministratori di database non abbiano accesso ai dati di testo normale. La crittografia e la decrittografia dei dati avvengono in modo trasparente a livello di driver, riducendo al minimo le modifiche che è necessario apportare alle applicazioni esistenti. Per informazioni dettagliate, vedere [Crittografia sempre attiva (motore di database)](/sql/relational-databases/security/encryption/always-encrypted-database-engine) e [Crittografia sempre attiva (sviluppo client)](/sql/relational-databases/security/encryption/always-encrypted-client-development).

- **Compilatore JIT a 64 bit per il codice gestito**

     .NET Framework 4.6 presenta una nuova versione del compilatore JIT a 64 bit (il cui nome in codice iniziale era RyuJIT). Il nuovo compilatore a 64 bit offre miglioramenti significativi delle prestazioni rispetto al compilatore JIT a 64 bit esistente. Il nuovo compilatore a 64 bit è abilitato per i processi a 64 bit in esecuzione su NET Framework 4.6. L'app verrà eseguita in un processo a 64 bit se è compilata come 64 bit o AnyCPU e se viene eseguita su un sistema operativo a 64 bit. Nonostante si sia cercato di rendere il più possibile trasparente la transizione al nuovo compilatore, potrebbero verificarsi cambiamenti del comportamento. Microsoft è interessata a conoscere i commenti diretti degli utenti sugli eventuali problemi riscontrati durante l'uso del nuovo compilatore JIT. In caso di problemi che potrebbero essere correlati al nuovo compilatore JIT a 64 bit, contattare Microsoft tramite [Microsoft Connect](http://connect.microsoft.com/).

     Il nuovo compilatore JIT a 64 bit include anche funzionalità di accelerazione SIMD hardware quando è associato a tipi abilitati per SIMD nello spazio dei nomi <xref:System.Numerics>, con notevoli miglioramenti in termini di prestazioni.

- **Miglioramenti apportati al caricatore di assembly**

     Il caricatore di assembly usa la memoria in modo più efficiente scaricando gli assembly IL dopo il caricamento di un'immagine NGEN corrispondente. Questa modifica riduce la memoria virtuale, aspetto particolarmente utile per app a 32 bit di grandi dimensioni (ad esempio Visual Studio) e consente anche di risparmiare memoria fisica.

- **Modifiche apportate alla libreria di classi base**

     Sono state aggiunte molte nuove API a [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] per abilitare gli scenari principali. Sono incluse le modifiche e le aggiunte seguenti:

    - Implementazioni **IReadOnlyCollection\<T>**

         Raccolte aggiuntive che implementano <xref:System.Collections.Generic.IReadOnlyCollection%601>, come <xref:System.Collections.Generic.Queue%601> e <xref:System.Collections.Generic.Stack%601>.

    - **CultureInfo.CurrentCulture e CultureInfo.CurrentUICulture**

         Le proprietà <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName> e <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName> sono ora di lettura/scrittura invece che di sola lettura. Se si assegna un nuovo oggetto <xref:System.Globalization.CultureInfo> a queste proprietà, cambiano anche le impostazioni cultura del thread corrente definite dalla proprietà `Thread.CurrentThread.CurrentCulture` e le impostazioni cultura del thread UI corrente definite dalle proprietà `Thread.CurrentThread.CurrentUICulture`.

    - **Miglioramenti apportati a Garbage Collection (GC)**

         La classe <xref:System.GC> include ora i metodi <xref:System.GC.TryStartNoGCRegion%2A> e <xref:System.GC.EndNoGCRegion%2A>, che permettono di disabilitare Garbage Collection durante l'esecuzione di un percorso critico.

         Un nuovo overload del metodo <xref:System.GC.Collect%28System.Int32%2CSystem.GCCollectionMode%2CSystem.Boolean%2CSystem.Boolean%29?displayProperty=fullName> permette di controllare se l'heap oggetti piccoli e l'heap oggetti grandi vengono sottoposti a sweep e compattati o solo sottoposti a sweep.

    - **Tipi abilitati per SIMD**

         Lo spazio dei nomi The <xref:System.Numerics> include ora alcuni tipi abilitati per SIMD, come <xref:System.Numerics.Matrix3x2>, <xref:System.Numerics.Matrix4x4>, <xref:System.Numerics.Plane>, <xref:System.Numerics.Quaternion>, <xref:System.Numerics.Vector2>, <xref:System.Numerics.Vector3> e <xref:System.Numerics.Vector4>.

         Il nuovo compilatore JIT a 64 bit include anche funzionalità di accelerazione SIMD hardware, quindi le prestazioni migliorano notevolmente quando si usano i tipi abilitati per SIMD con il nuovo compilatore JIT a 64 bit.

    - **Aggiornamenti della crittografia**

         L'API <xref:System.Security.Cryptography?displayProperty=fullName> è stata aggiornata per supportare le [API di crittografia CNG Windows](https://msdn.microsoft.com/library/windows/desktop/aa376214.aspx). Le versioni precedenti di .NET Framework si basavano interamente su una [versione precedente delle API di crittografia Windows](https://msdn.microsoft.com/library/windows/desktop/aa380255.aspx) per l'implementazione di <xref:System.Security.Cryptography?displayProperty=fullName>. Microsoft ha ricevuto alcune richieste relative all'aggiunta del supporto per l'API CNG, perché questa supporta [algoritmi di crittografia moderni](https://msdn.microsoft.com/library/windows/desktop/bb204775.aspx#suite_b_support), che sono importanti per determinate categorie di app.

         .NET Framework 4.6 include i nuovi miglioramenti seguenti per supportare le API di crittografia di CNG di Windows:

        - Un set di metodi di estensione per certificati X509, `System.Security.Cryptography.X509Certificates.RSACertificateExtensions.GetRSAPublicKey(System.Security.Cryptography.X509Certificates.X509Certificate2)` e `System.Security.Cryptography.X509Certificates.RSACertificateExtensions.GetRSAPrivateKey(System.Security.Cryptography.X509Certificates.X509Certificate2)`, che restituiscono, quando possibile, un'implementazione basata su CNG invece di un'implementazione basata su CAPI. Ad esempio, alcune smart card richiedono comunque CAPI e le API gestiscono il fallback.

        - Classe <xref:System.Security.Cryptography.RSACng?displayProperty=fullName>, che fornisce un'implementazione CNG dell'algoritmo RSA.

        - Miglioramenti all'API RSA in modo che le azioni comuni non richiedano più il cast. Ad esempio, per la crittografia dei dati eseguita con un oggetto <xref:System.Security.Cryptography.X509Certificates.X509Certificate2>, è necessario aggiungere codice simile al seguente nelle versioni precedenti di .NET Framework.

             [!code-csharp[WhatsNew.Casting#1](../../../samples/snippets/csharp/VS_Snippets_CLR/whatsnew.casting/cs/program.cs#1)]    [!code-vb[WhatsNew.Casting#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/whatsnew.casting/vb/module1.vb#1)]

             Il codice che usa le nuove API di crittografia in Framework .NET 4.6 può essere riscritto nel modo seguente per evitare il cast.

             [!code-csharp[WhatsNew.Casting#2](../../../samples/snippets/csharp/VS_Snippets_CLR/whatsnew.casting/cs/program.cs#2)]    [!code-vb[WhatsNew.Casting#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/whatsnew.casting/vb/module1.vb#2)]

    - **Supporto per la conversione di date e ore da o verso l'ora di Unix**

         Sono stati aggiunti i nuovi metodi seguenti alla struttura <xref:System.DateTimeOffset> per supportare la conversione di valori di data e ora da o verso l'ora di Unix:

        - <xref:System.DateTimeOffset.FromUnixTimeSeconds%2A?displayProperty=fullName>

        - <xref:System.DateTimeOffset.FromUnixTimeMilliseconds%2A?displayProperty=fullName>

        - <xref:System.DateTimeOffset.ToUnixTimeSeconds%2A?displayProperty=fullName>

        - <xref:System.DateTimeOffset.ToUnixTimeMilliseconds%2A?displayProperty=fullName>

    - **Opzioni di compatibilità**

         La nuova classe <xref:System.AppContext> aggiunge una nuova funzionalità di compatibilità che permette agli sviluppatori di librerie di fornire agli utenti un meccanismo uniforme per la rinuncia esplicita alla nuova funzionalità, che stabilisce un contratto a regime di controllo libero ("loosely-coupled") tra componenti per poter comunicare una richiesta di rinuncia esplicita. Questa funzionalità è importante in genere quando viene apportata una modifica alle funzionalità esistenti. Al contrario, esiste già un consenso esplicito per la nuova funzionalità.

         Con <xref:System.AppContext>, le librerie definiscono ed espongono opzioni di compatibilità, mentre il codice che dipende dalle librerie può impostare queste opzioni in modo da influire sul comportamento delle librerie. Per impostazione predefinita, le librerie forniscono la nuova funzionalità e la modificano (cioè offrono la funzionalità precedente) solo se l'opzione è impostata.

         Un'applicazione (o una libreria) può dichiarare il valore di un'opzione (che è sempre un valore <xref:System.Boolean>) definita da una libreria dipendente. L'opzione è sempre implicitamente `false`. Impostare l'opzione su `true` la abilita. Impostare in modo esplicito l'opzione su `false` fornisce il nuovo comportamento.

        ```csharp
        AppContext.SetSwitch("Switch.AmazingLib.ThrowOnException", true);
        ```

         La libreria deve controllare se un consumer è dichiarato il valore dell'opzione e si comporta in modo appropriato in base ad essa.

        ```csharp
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

        - *Opzione*.*spaziodeinomi*.*nomeopzione*

        - *Opzione*.*libreria*.*nomeopzione*

    - **Modifiche apportate al modello asincrono basato su attività**

         Per le app destinate a [!INCLUDE[net_v46](../../../includes/net-v46-md.md)], gli oggetti <xref:System.Threading.Tasks.Task> e <xref:System.Threading.Tasks.Task%601> ereditano le impostazioni cultura e le impostazioni cultura dell'interfaccia utente del thread chiamante. Questo non incide sul comportamento delle app per versioni precedenti di .NET Framework o non destinate a una versione specifica di .NET Framework. Per altre informazioni, vedere la sezione relativa alle impostazioni cultura e alle operazioni asincrone basate su attività dell'argomento Classe <xref:System.Globalization.CultureInfo>.

         La classe <xref:System.Threading.AsyncLocal%601?displayProperty=fullName> permette di rappresentare dati di ambiente locali rispetto a un determinato flusso di controllo asincrono, ad esempio un metodo `async`. Può essere usato per rendere persistenti i dati tra thread. È anche possibile definire un metodo di callback che riceve una notifica ogni volta che i dati di ambiente subiscono una modifica perché la proprietà <xref:System.Threading.AsyncLocal%601.Value%2A?displayProperty=fullName> è stata modificata in modo esplicito oppure il thread ha rilevato una transizione di contesto.

         Sono stati aggiunti tre metodi pratici, <xref:System.Threading.Tasks.Task.CompletedTask%2A?displayProperty=fullName>, <xref:System.Threading.Tasks.Task.FromCanceled%2A?displayProperty=fullName> e <xref:System.Threading.Tasks.Task.FromException%2A?displayProperty=fullName>, al modello asincrono basato su attività per restituire le attività completate in uno stato specifico.

         La classe <xref:System.IO.Pipes.NamedPipeClientStream> supporta ora la comunicazione asincrona con il nuovo oggetto <xref:System.IO.Pipes.NamedPipeClientStream.ConnectAsync%2A>. ProcessOnStatus.

    - **EventSource supporta ora la scrittura nel registro eventi**

         È ora possibile usare la classe <xref:System.Diagnostics.Tracing.EventSource> per registrare nel registro eventi messaggi amministrativi o operativi, oltre a tutte le sessioni ETW esistenti create nel computer. In passato era necessario usare il pacchetto Microsoft.Diagnostics.Tracing.EventSource NuGet per questa funzionalità. Questa funzionalità è ora integrata in .NET Framework 4.6.

         Sia il pacchetto NuGet sia .NET Framework 4.6 sono stati aggiornati con le funzionalità seguenti:

        - **Eventi dinamici**

             Consente eventi definiti al momento senza creare metodi di eventi.

        - **Payload avanzati**

             Consente di passare classi e matrici attribuite in modo specifico nonché tipi primitivi come un payload

        - **Rilevamento attività**

             Comporta l'applicazione di tag di eventi tra gli eventi Start e Stop con un ID che rappresenta tutte le attività attualmente attive.

         Per supportare queste funzionalità, è stato aggiunto il metodo di overload <xref:System.Diagnostics.Tracing.EventSource.Write%2A> alla classe <xref:System.Diagnostics.Tracing.EventSource>.

- **Windows Presentation Foundation (WPF)**

    - **Miglioramenti apportati a HDPI**

         Il supporto di HDPI in WPF è stato migliorato in [!INCLUDE[net_v46](../../../includes/net-v46-md.md)]. Sono state apportate modifiche all'arrotondamento del layout per ridurre le istanze di ritaglio nei controlli con bordi. Per impostazione predefinita, questa funzionalità è abilitata solo se <xref:System.Runtime.Versioning.TargetFrameworkAttribute> è impostato su .NET 4.6.  Le applicazioni destinate alle versioni precedenti del framework, ma eseguite in [!INCLUDE[net_v46](../../../includes/net-v46-md.md)], possono scegliere il nuovo comportamento aggiungendo la riga seguente alla sezione [\<runtime>](../../../docs/framework/configure-apps/file-schema/runtime/runtime-element.md) del file app.config:

        ```
        <AppContextSwitchOverrides
        value="Switch.MS.Internal.DoNotApplyLayoutRoundingToMarginsAndBorderThickness=false"
        />
        ```

         Le finestre WPF che si estendono su più monitor con impostazioni DPI diverse (configurazione di più DPI) sono ora visualizzate completamente senza aree nere. È possibile rifiutare esplicitamente questo comportamento disabilitandolo con l'aggiunta della riga seguente alla sezione `<appSettings>` del file di configurazione dell'app:

        ```
        <add key="EnableMultiMonitorDisplayClipping" value="true"/>
        ```

         È stato aggiunto a <xref:System.Windows.Input.Cursor?displayProperty=fullName> il supporto per il caricamento automatico del cursore appropriato in base all'impostazione DPI.

    - **Miglioramento della funzionalità touch**

         I clienti hanno segnalato su [Connect](https://connect.microsoft.com/VisualStudio/feedback/details/903760/) che il comportamento imprevedibile della funzionalità touch è stato risolto in [!INCLUDE[net_v46](../../../includes/net-v46-md.md)]. La soglia relativa al doppio tocco per le app di Windows Store e le applicazioni WPF ora è lo stesso in Windows 8.1 e versioni successive.

    - **Supporto per finestre figlio trasparenti**

         WPF in [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] supporta le finestre figlio trasparenti in Windows 8.1 e versioni successive. Ciò consente di creare finestre figlio non rettangolari e trasparenti nelle finestre di primo livello. È possibile abilitare questa funzionalità impostando la proprietà <xref:System.Windows.Interop.HwndSourceParameters.UsesPerPixelTransparency%2A?displayProperty=fullName> su `true`.

- **Windows Communication Foundation (WCF)**

    - **Supporto di SSL**

         WCF ora supporta la versione SSL TLS 1.1 e TLS 1.2, oltre a SSL 3.0 e TLS 1.0, quando si usa NetTcp con la sicurezza del trasporto e l'autenticazione client. Ora è possibile selezionare il protocollo da usare o disabilitare i protocolli precedenti, che sono meno sicuri. A questo scopo, è possibile impostare la proprietà <xref:System.ServiceModel.TcpTransportSecurity.SslProtocols%2A> o aggiungere il codice seguente a un file di configurazione.

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

    - **Invio di messaggi tramite connessioni HTTP diverse**

         WCF ora consente agli utenti di garantire l'invio di determinati messaggi usando diverse connessioni HTTP sottostanti. Questo risultato può essere raggiunto in due modi:

        - **Uso di un prefisso del nome del gruppo di connessione**

             Gli utenti possono specificare una stringa che WCF userà per ottenere un prefisso per il nome del gruppo di connessione. Due messaggi con prefissi diversi vengono inviati usando diverse connessioni HTTP sottostanti. Per impostare il prefisso, aggiungere una coppia chiave/valore alla proprietà <xref:System.ServiceModel.Channels.Message.Properties%2A?displayProperty=fullName> del messaggio. La chiave è "HttpTransportConnectionGroupNamePrefix", mentre il valore è il prefisso desiderato.

        - **Uso di channel factory diverse**

             Gli utenti possono anche attivare una funzionalità che assicura che i messaggi inviati con i canali creati da channel factory diverse useranno connessioni HTTP sottostanti diverse. Per abilitare questa funzionalità, gli utenti devono impostare `appSetting` su `true`:

            ```
            <appSettings>
               <add key="wcf:httpTransportBinding:useUniqueConnectionPoolPerFactory" value="true" />
            </appSettings>
            ```

- **Windows Workflow Foundation (WWF)**

     Ora è possibile specificare il numero di secondi che un servizio del flusso di lavoro attenderà per una richiesta di operazione non ordinata quando esiste un segnalibro "non protocollo" in attesa prima del timeout della richiesta. Un segnalibro "non protocollo" è un segnalibro che non è correlato alle attività di ricezione in attesa. Alcune attività creano segnalibri non protocollo all'interno della propria implementazione, quindi potrebbe non essere evidente che un segnalibro non protocollo esista. Sono incluse le attività relative allo stato e alla selezione. Pertanto, se si ha un servizio del flusso di lavoro implementato con una macchina a stati o contenente un'attività di selezione, probabilmente si avranno segnalibri non protocollo. Specificare l'intervallo aggiungendo una riga simile alla seguente alla sezione `appSettings` del file di configurazione dell'app:

    ```
    <add key="microsoft:WorkflowServices:FilterResumeTimeoutInSeconds" value="60"/>
    ```

     Il valore predefinito è 60 secondi. Se `value` è impostato su 0, le richieste non ordinate vengono immediatamente rifiutate con un messaggio di errore simile al seguente:

    ```
    Operation 'Request3|{http://tempuri.org/}IService' on service instance with identifier '2b0667b6-09c8-4093-9d02-f6c67d534292' cannot be performed at this time. Please ensure that the operations are performed in the correct order and that the binding in use provides ordered delivery guarantees. 
    ```

     Si tratta dello stesso messaggio che viene visualizzato se si riceve un messaggio di operazione non ordinato e non sono presenti segnalibri non protocollo.

     Se il valore dell'elemento `FilterResumeTimeoutInSeconds` è diverso da zero, sono presenti segnalibri non protocollo, l'intervallo di timeout scade e l'operazione ha esito negativo con un messaggio di timeout.

- **Transazioni**

     È ora possibile includere l'identificatore di transazione distribuita per la transazione che ha generato un'eccezione derivata da <xref:System.Transactions.TransactionException>. A questo scopo, aggiungere la chiave seguente alla sezione `appSettings` del file di configurazione dell'app:

    ```
    <add key="Transactions:IncludeDistributedTransactionIdInExceptionMessage" value="true"/> 
    ```

     Il valore predefinito è `false`.

- **Rete**

    - **Riutilizzo di socket**

         Windows 10 include un nuovo algoritmo di rete ad alta scalabilità che consente di migliorare l'uso delle risorse del computer riutilizzando porte locali per le connessioni TCP in uscita. .NET Framework 4.6 supporta il nuovo algoritmo, consentendo alle app .NET di sfruttare il nuovo comportamento. Nelle versioni precedenti di Windows era presente un limite di connessioni simultanee artificiali (in genere 16.384, la dimensione predefinita dell'intervallo di porte dinamiche), che poteva limitare la scalabilità di un servizio causando l'esaurimento delle porte quando sono sotto carico.

         In [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] sono state aggiunte due nuove API per consentire il riutilizzo delle porte, che rimuove in modo efficace il limite di 64.000 sulle connessioni simultanee:

        - Valore di enumerazione <xref:System.Net.Sockets.SocketOptionName?displayProperty=fullName>.

        - Proprietà <xref:System.Net.ServicePointManager.ReusePort%2A?displayProperty=fullName>.

         Per impostazione predefinita, la proprietà <xref:System.Net.ServicePointManager.ReusePort%2A?displayProperty=fullName> è `false`, a meno che il valore `HWRPortReuseOnSocketBind` della chiave del Registro di sistema `HKLM\SOFTWARE\Microsoft\.NETFramework\v4.0.30319` non sia impostato su 0x1. Per abilitare il riutilizzo delle porte locali in connessioni HTTP, impostare la proprietà <xref:System.Net.ServicePointManager.ReusePort%2A?displayProperty=fullName> su `true`. In questo modo, tutte le connessioni socket TCP in uscita da <xref:System.Net.Http.HttpClient> e <xref:System.Net.HttpWebRequest> usano una nuova opzione di socket di Windows 10, [SO_REUSE_UNICASTPORT](https://msdn.microsoft.com/library/windows/desktop/ms740532.aspx), che permette il riutilizzo delle porte locali.

         Gli sviluppatori che scrivono un'applicazione solo socket possono specificare l'opzione <xref:System.Net.Sockets.SocketOptionName?displayProperty=fullName> durante la chiamata di un metodo come <xref:System.Net.Sockets.Socket.SetSocketOption%2A?displayProperty=fullName>, in modo che i socket in uscita riutilizzino le porte locali durante l'associazione.

    - **Supporto di nomi di dominio internazionali e di PunyCode**

         È stata aggiunta la nuova proprietà <xref:System.Uri.IdnHost%2A> alla classe <xref:System.Uri> per migliorare il supporto dei nomi di dominio internazionali e di PunyCode.

- **Ridimensionamento nei controlli Windows Form**

     Questa funzionalità è stata ampliata in [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] per includere i tipi <xref:System.Windows.Forms.DomainUpDown>, <xref:System.Windows.Forms.NumericUpDown>, <xref:System.Windows.Forms.DataGridViewComboBoxColumn>, <xref:System.Windows.Forms.DataGridViewColumn> e <xref:System.Windows.Forms.ToolStripSplitButton> e il rettangolo specificato dalla proprietà <xref:System.Drawing.Design.PaintValueEventArgs.Bounds%2A> usata per disegnare un oggetto <xref:System.Drawing.Design.UITypeEditor>.

     È una funzionalità che prevede il consenso esplicito. Per attivarla, impostare l'elemento `EnableWindowsFormsHighDpiAutoResizing` su `true` nel file di configurazione dell'applicazione (app.config):

    ```
    <appSettings>
       <add key="EnableWindowsFormsHighDpiAutoResizing" value="true" />
    </appSettings>
    ```

- **Supporto per le codifiche della tabella codici**

     [!INCLUDE[net_core](../../../includes/net-core-md.md)] supporta principalmente le codifiche Unicode e per impostazione predefinita offre un supporto limitato per le codifiche della tabella codici. È possibile aggiungere supporto per le codifiche della tabella codici disponibili in .NET Framework, ma che non sono supportate in [!INCLUDE[net_core](../../../includes/net-core-md.md)], registrando le codifiche con il metodo <xref:System.Text.Encoding.RegisterProvider%2A?displayProperty=fullName>. Per altre informazioni, vedere <xref:System.Text.CodePagesEncodingProvider?displayProperty=fullName>.

- **.NET Native**

     Le app di Windows per Windows 10 destinate a [!INCLUDE[net_core](../../../includes/net-core-md.md)] e scritte in C# o Visual Basic ora possono avvalersi di una nuova tecnologia che compila le app in codice nativo anziché IL. Producono app caratterizzate da maggiore rapidità di avvio ed esecuzione. Per altre informazioni, vedere [Compilazione di app con .NET Native](../../../docs/framework/net-native/index.md). Per una panoramica di .NET Native che esamina le differenze rispetto alla compilazione JIT e NGEN e descrive tutti i vantaggi per il codice, vedere [Compilazione e .NET Native](../../../docs/framework/net-native/net-native-and-compilation.md).

     Le app vengono compilate in codice nativo per impostazione predefinita quando si compilano con Visual Studio 2015. Per altre informazioni, vedere [Introduzione a .NET Native](../../../docs/framework/net-native/getting-started-with-net-native.md).

     Per supportare il debug di app .NET Native, è stata aggiunta una serie di nuove interfacce ed enumerazioni all'API di debug non gestito. Per altre informazioni, vedere l'argomento [Debug (riferimenti alle API non gestite)](../../../docs/framework/unmanaged-api/debugging/index.md).

- **Pacchetti .NET Framework open source**

     I pacchetti [!INCLUDE[net_core](../../../includes/net-core-md.md)] come le raccolte non modificabili, le [API SIMD](http://go.microsoft.com/fwlink/?LinkID=518639) e le API di rete come quelle incluse nello spazio dei nomi <xref:System.Net.Http> sono ora disponibili come pacchetti open source su [GitHub](https://github.com/). Per accedere al codice, vedere [NetFx su GitHub](http://go.microsoft.com/fwlink/?LinkID=518634). Per altre informazioni e indicazioni su come contribuire a questi pacchetti, vedere [Componenti di base e open source di .NET](../../../docs/framework/get-started/net-core-and-open-source.md) e la [home page di .NET su GitHub](http://go.microsoft.com/fwlink/?LinkID=518635).

 [Torna all'inizio](#introduction)

<a name="v452"></a> 
## <a name="whats-new-in-the-net-framework-452"></a>Novità di .NET Framework 4.5.2

- **Nuove API per app ASP.NET** I nuovi metodi <xref:System.Web.HttpResponse.AddOnSendingHeaders%2A?displayProperty=fullName> e <xref:System.Web.HttpResponseBase.AddOnSendingHeaders%2A?displayProperty=fullName> permettono di esaminare e modificare le intestazioni della risposta e il codice di stato quando la risposta viene scaricata nell'app client. Provare a usare questi metodi invece degli eventi <xref:System.Web.HttpApplication.PreSendRequestHeaders> e <xref:System.Web.HttpApplication.PreSendRequestContent>, perché sono più efficienti e affidabili.

     Il metodo <xref:System.Web.Hosting.HostingEnvironment.QueueBackgroundWorkItem%2A?displayProperty=fullName> permette di pianificare piccoli elementi di lavoro in background. ASP.NET tiene traccia di questi elementi e impedisce a IIS di chiudere improvvisamente il processo di lavoro finché non saranno stati completati tutti gli elementi di lavoro in background. Non è possibile chiamare questo metodo all'esterno del dominio dell'app gestita di ASP.NET.

     Le nuove proprietà <xref:System.Web.HttpResponse.HeadersWritten?displayProperty=fullName> e <xref:System.Web.HttpResponseBase.HeadersWritten?displayProperty=fullName> restituiscono valori booleani che indicano se le intestazioni della risposta sono state scritte. È possibile usare queste proprietà per accertarsi che le chiamate alle API come <xref:System.Web.HttpResponse.StatusCode%2A?displayProperty=fullName>, che genera eccezioni se le intestazioni sono state scritte, riescano.

- **Ridimensionamento nei controlli Windows Form** Questa funzionalità è stata ampliata. È ora possibile usare l'impostazione DPI di sistema per ridimensionare i componenti dei seguenti controlli aggiuntivi (ad esempio, la freccia a discesa nelle caselle combinate):

     <xref:System.Windows.Forms.ComboBox>    <xref:System.Windows.Forms.ToolStripComboBox>    <xref:System.Windows.Forms.ToolStripMenuItem>    <xref:System.Windows.Forms.Cursor>    <xref:System.Windows.Forms.DataGridView>    <xref:System.Windows.Forms.DataGridViewComboBoxColumn>

     È una funzionalità che prevede il consenso esplicito. Per attivarla, impostare l'elemento `EnableWindowsFormsHighDpiAutoResizing` su `true` nel file di configurazione dell'applicazione (app.config):

    ```
    <appSettings>
       <add key="EnableWindowsFormsHighDpiAutoResizing" value="true" />
    </appSettings>
    ```

- **Nuova funzionalità per il flusso di lavoro** Un gestore di risorse che usa il metodo <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A>, e di conseguenza implementa l'interfaccia <xref:System.Transactions.IPromotableSinglePhaseNotification>, può usare il nuovo metodo <xref:System.Transactions.Transaction.PromoteAndEnlistDurable%2A?displayProperty=fullName> per richiedere le operazioni seguenti:

    - Promozione della transazione in transazione MSDTC (Microsoft Distributed Transaction Coordinator).

    - Sostituzione di <xref:System.Transactions.IPromotableSinglePhaseNotification> con un oggetto <xref:System.Transactions.ISinglePhaseNotification>, che è un'integrazione durevole che supporta commit a fase singola.

     È possibile eseguire questa operazione nello stesso dominio dell'app; inoltre, non è necessario altro codice non gestito che interagisca con MSDTC per eseguire la promozione. Il nuovo metodo può essere chiamato solo in presenza di una chiamata in attesa da <xref:System.Transactions?displayProperty=fullName> al metodo <xref:System.Transactions.IPromotableSinglePhaseNotification>`Promote` implementato dall'integrazione promuovibile.

- **Miglioramenti apportati alla profilatura** Le seguenti nuove API di profilatura non gestite offrono funzioni di profilatura più solide:

     [Struttura COR_PRF_ASSEMBLY_REFERENCE_INFO](../../../docs/framework/unmanaged-api/profiling/cor-prf-assembly-reference-info-structure.md) 
     [Enumerazione COR_PRF_HIGH_MONITOR](../../../docs/framework/unmanaged-api/profiling/cor-prf-high-monitor-enumeration.md) 
     [Metodo GetAssemblyReferences](../../../docs/framework/unmanaged-api/profiling/icorprofilercallback6-getassemblyreferences-method.md) 
     [Metodo GetEventMask2](../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo5-geteventmask2-method.md) 
     [Metodo SetEventMask2](../../../docs/framework/unmanaged-api/profiling/icorprofilerinfo5-seteventmask2-method.md) 
     [Metodo AddAssemblyReference](../../../docs/framework/unmanaged-api/profiling/icorprofilerassemblyreferenceprovider-addassemblyreference-method.md)

     Le precedenti implementazioni di `ICorProfiler` supportavano il caricamento differito degli assembly dipendenti. Le nuove API di profilatura richiedono assembly dipendenti inseriti dal profiler per il caricamento immediato, invece di essere caricato dopo la completa inizializzazione dell'app. Questa modifica non incide sugli utenti delle API `ICorProfiler` esistenti.

- **Miglioramenti apportati al debug** Le seguenti nuove API di debug non gestite offrono una migliore integrazione con un profiler. È ora possibile accedere ai metadati inseriti dal profiler oltre alle variabili e al codice locali prodotti dalle richieste ReJIT del compilatore durante il debug di dump.

     [Metodo SetWriteableMetadataUpdateMode](../../../docs/framework/unmanaged-api/debugging/icordebugprocess7-setwriteablemetadataupdatemode-method.md) 
     [Metodo EnumerateLocalVariablesEx](../../../docs/framework/unmanaged-api/debugging/icordebugilframe4-enumeratelocalvariablesex-method.md) 
     [Metodo GetLocalVariableEx](../../../docs/framework/unmanaged-api/debugging/icordebugilframe4-getlocalvariableex-method.md) 
     [Metodo GetCodeEx](../../../docs/framework/unmanaged-api/debugging/icordebugilframe4-getcodeex-method.md) 
     [Metodo GetActiveReJitRequestILCode](../../../docs/framework/unmanaged-api/debugging/icordebugfunction3-getactiverejitrequestilcode-method.md) 
     [Metodo GetInstrumentedILMap](../../../docs/framework/unmanaged-api/debugging/icordebugilcode2-getinstrumentedilmap-method.md)

- **Modifiche apportate alla traccia eventi** .NET Framework 4.5.2 consente di eseguire attività out-of-process basate su Event Tracing for Windows (ETW) per una superficie maggiore. Ciò consente ai fornitori di Advanced Power Management (APM) di offrire strumenti semplici che tengono accuratamente traccia dei costi delle singole richieste e attività cross-thread.  Questi eventi vengono generati solo quando sono abilitati dai controller ETW; di conseguenza, le modifiche non influiscono sul codice ETW scritto in precedenza oppure sul codice eseguito con ETW disattivato.

- **Promozione di una transazione e relativa conversione in integrazione durevole**

     <xref:System.Transactions.Transaction.PromoteAndEnlistDurable%2A?displayProperty=fullName> è una nuova API aggiunta a .NET Framework 4.5.2 e 4.6:

    ```csharp
    [System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name = "FullTrust")]
    public Enlistment PromoteAndEnlistDurable(Guid resourceManagerIdentifier,
                                              IPromotableSinglePhaseNotification promotableNotification,
                                              ISinglePhaseNotification enlistmentNotification,
                                              EnlistmentOptions enlistmentOptions)
    ```

     Il metodo può essere usato da un'integrazione precedentemente creata da <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A?displayProperty=fullName> in risposta al metodo <xref:System.Transactions.ITransactionPromoter.Promote%2A?displayProperty=fullName>. Chiede a `System.Transactions` di alzare la transazione al livello di transazione MSDTC e di "convertire" l'elenco promuovibile in un elenco durevole. Dopo il completamento di questo metodo, l'interfaccia <xref:System.Transactions.IPromotableSinglePhaseNotification> non sarà più usata come riferimento da `System.Transactions` e tutte le eventuali notifiche passeranno all'interfaccia <xref:System.Transactions.ISinglePhaseNotification> specificata. L'elenco in questione deve agire come un elenco durevole, supportando la registrazione e il ripristino delle transazioni. Per informazioni dettagliate, fare riferimento a <xref:System.Transactions.Transaction.EnlistDurable%2A?displayProperty=fullName>. L'integrazione deve anche supportare <xref:System.Transactions.ISinglePhaseNotification>.  Questo metodo può essere chiamato *solo* durante l'elaborazione di una chiamata di <xref:System.Transactions.ITransactionPromoter.Promote%2A?displayProperty=fullName>. In caso contrario, verrà generata un'eccezione <xref:System.Transactions.TransactionException>.

 [Torna all'inizio](#introduction)

<a name="v451"></a> 
## <a name="whats-new-in-the-net-framework-451"></a>Novità di .NET Framework 4.5.1
 **Aggiornamenti di aprile 2014**:

- [Visual Studio 2013 Update 2](http://go.microsoft.com/fwlink/p/?LinkId=393658) include alcuni aggiornamenti ai modelli di libreria di classi portabile per supportare questi scenari:

    - È possibile usare le API di Windows Runtime in librerie portabili destinate a Windows 8.1, Windows Phone 8.1 e Windows Phone Silverlight 8.1.

    - È possibile includere XAML (tipi Windows.UI.XAML) nelle librerie portabili quando la destinazione è Windows 8.1 o Windows Phone 8.1. Sono supportati i modelli XAML seguenti: Pagina vuota, Dizionario risorse, Controllo basato su modelli e Controllo utente.

    - È possibile creare una componente Windows Runtime portabile (.winmd file) da usare in app di Windows Store destinate a Windows 8.1 e Windows Phone 8.1.

    - È possibile cambiare associazione a una libreria di classi Windows Store o Windows Phone Store come una Libreria di classi portabile.

     Per altre informazioni su queste modifiche, vedere [Libreria di classi portabile](../../../docs/standard/cross-platform/cross-platform-development-with-the-portable-class-library.md).

- Il set di contenuti di .NET Framework ora include la documentazione relativa a [!INCLUDE[net_native](../../../includes/net-native-md.md)], una tecnologia di precompilazione per la creazione e la distribuzione di app di Windows. [!INCLUDE[net_native](../../../includes/net-native-md.md)] compila le app direttamente in codice nativo piuttosto che in linguaggio intermedio (IL), per ottenere migliori prestazioni. Per informazioni dettagliate, vedere [Compilazione di app con .NET Native](../../../docs/framework/net-native/index.md).

- [Reference Source per .NET Framework](http://referencesource.microsoft.com/) offre una nuova esperienza di esplorazione e funzionalità migliorate. È ora possibile esplorare il codice sorgente di .NET Framework online, [scaricare i riferimenti](http://referencesource.microsoft.com/download.html) per la visualizzazione offline ed eseguire le origini (inclusi aggiornamenti e patch) durante il debug. Per altre informazioni, vedere il post di blog relativo al [nuovo aspetto di Reference Source per .NET](https://blogs.msdn.microsoft.com/dotnet/2014/02/24/a-new-look-for-net-reference-source/).

 Le nuove funzionalità e i miglioramenti principali in .NET Framework 4.5.1 includono:

- Reindirizzamento di associazione automatico per assembly. A partire da [!INCLUDE[vs_dev12](../../../includes/vs-dev12-md.md)], quando si compila un'app destinata a [!INCLUDE[net_v451](../../../includes/net-v451-md.md)], è possibile aggiungere reindirizzamenti di associazione al file di configurazione dell'app se quest'ultima o i relativi componenti fanno riferimento a più versioni dello stesso assembly. È inoltre possibile abilitare questa funzionalità per i progetti destinati a versioni precedenti di .NET Framework. Per altre informazioni, vedere [Procedura: abilitare e disabilitare il reindirizzamento di associazione automatico](../../../docs/framework/configure-apps/how-to-enable-and-disable-automatic-binding-redirection.md).

- Possibilità di raccogliere informazioni di diagnostica che consentono agli sviluppatori di migliorare le prestazioni delle applicazioni server e cloud. Per altre informazioni, vedere i metodi <xref:System.Diagnostics.Tracing.EventSource.WriteEventWithRelatedActivityId%2A> e <xref:System.Diagnostics.Tracing.EventSource.WriteEventWithRelatedActivityIdCore%2A> nella classe <xref:System.Diagnostics.Tracing.EventSource>.

- Capacità di compattare in modo esplicito gli heap di oggetti grandi durante la Garbage Collection. Per altre informazioni, vedere la proprietà <xref:System.Runtime.GCSettings.LargeObjectHeapCompactionMode%2A?displayProperty=fullName>.

- Altri miglioramenti alle prestazioni, quali la sospensione di app ASP.NET, i miglioramenti JIT multicore e un avvio più rapido delle app in seguito a un aggiornamento di .NET Framework. Per informazioni dettagliate, vedere l'[annuncio di .NET Framework 4.5.1](https://blogs.msdn.microsoft.com/dotnet/2013/06/26/announcing-the-net-framework-4-5-1-preview/) e il post di blog sulla [sospensione di app ASP.NET](https://blogs.msdn.microsoft.com/dotnet/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting/).

 I miglioramenti di Windows Form includono:

- Ridimensionamento nei controlli Windows Form. È possibile usare l'impostazione DPI per ridimensionare i componenti dei controlli (ad esempio, le icone visualizzate in una griglia delle proprietà) scegliendo una voce nel file di configurazione dell'applicazione (app.config) relativo alla propria app. Questa funzionalità è attualmente supportata nei seguenti controlli Windows Form:

     <xref:System.Windows.Forms.PropertyGrid>    <xref:System.Windows.Forms.TreeView>    Alcuni aspetti di <xref:System.Windows.Forms.DataGridView> (per gli altri controlli supportati, vedere le [nuove funzionalità della versione 4.5.2](#v452))

     Per attivare questa funzionalità, aggiungere un nuovo elemento \<appSettings> al file di configurazione (app.config) e impostare l'elemento `EnableWindowsFormsHighDpiAutoResizing` su `true`:

    ```
    <appSettings>
       <add key="EnableWindowsFormsHighDpiAutoResizing" value="true" />
    </appSettings>
    ```

 I miglioramenti durante il debug delle app .NET Framework in [!INCLUDE[vs_dev12](../../../includes/vs-dev12-md.md)] includono:

- Valori restituiti nel debugger di Visual Studio. Quando si esegue il debug di un'app gestita in [!INCLUDE[vs_dev12](../../../includes/vs-dev12-md.md)], nella finestra Auto vengono restituiti tipi e valori per i metodi. Queste informazioni sono disponibili per applicazioni desktop, Windows Store e Windows Phone. Per altre informazioni, vedere [Esaminare i valori restituiti dalle chiamate di metodo](http://msdn.microsoft.com/library/e3245b37-8e2e-4200-ba84-133726e95f1f\(v=vs.120\).aspx) in MSDN Library.

- Modifica e continua per app a 64 bit. In [!INCLUDE[vs_dev12](../../../includes/vs-dev12-md.md)] è supportata la funzionalità Modifica e continuazione per le applicazioni gestite a 64 bit per desktop, Windows Store e Windows Phone. Le limitazioni esistenti restano valide per le app a 32 bit e a 64 bit. Vedere l'ultima sezione dell'articolo [Modifiche al codice supportate (C#)](/visualstudio/debugger/supported-code-changes-csharp).

- Debug asincrono. Per semplificare il debug delle app asincrone in [!INCLUDE[vs_dev12](../../../includes/vs-dev12-md.md)], lo stack di chiamate nasconde il codice dell'infrastruttura fornito dai compilatori per supportare la programmazione asincrona e inoltre si concatena nei frame padre logici, in modo da poter seguire più chiaramente l'esecuzione logica del programma. La finestra Attività in parallelo è stata sostituita da una finestra Attività, contenente le attività correlate a uno specifico punto di interruzione e qualsiasi altra attività attualmente attiva o pianificata nell'app. Informazioni su questa funzionalità sono disponibili nella sezione relativa al debug asincrono nell'[annuncio di .NET Framework 4.5.1](https://blogs.msdn.microsoft.com/dotnet/2013/06/26/announcing-the-net-framework-4-5-1-preview/).

- Supporto avanzato delle eccezioni per i componenti Windows Runtime. In [!INCLUDE[win81](../../../includes/win81-md.md)] le eccezioni generate dalle app di Windows Store conservano le informazioni sull'errore che ha generato l'eccezione, anche oltre i limiti di linguaggio. Informazioni su questa funzionalità sono disponibili nella sezione relativa allo sviluppo di app di Windows Store nell'[annuncio di .NET Framework 4.5.1](https://blogs.msdn.microsoft.com/dotnet/2013/06/26/announcing-the-net-framework-4-5-1-preview/). 

 A partire da [!INCLUDE[vs_dev12](../../../includes/vs-dev12-md.md)], è possibile usare lo [strumento Mpgo.exe (Managed Profile Guided Optimization)](../../../docs/framework/tools/mpgo-exe-managed-profile-guided-optimization-tool.md) per ottimizzare le app di [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] e quelle desktop.

 Per le nuove funzionalità di ASP.NET 4.5.1, vedere [ASP.NET 4.5.1 e Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=309094) nel sito Web ASP.NET.

 [Torna all'inizio](#introduction)

<a name="core"></a> 
## <a name="whats-new-in-the-net-framework-45"></a>Novità di .NET Framework 4.5

### <a name="core-new-features-and-improvements"></a>Miglioramenti e nuove funzionalità principali

- Possibilità di ridurre i riavvii di sistema rilevando e chiudendo le applicazioni .NET Framework 4 durante la distribuzione. Vedere [Riduzione dei riavvii del sistema durante le installazioni di .NET Framework 4.5](../../../docs/framework/deployment/reducing-system-restarts.md).

- Supporto per le matrici di dimensioni maggiori di 2 GB nelle piattaforme a 64 bit. Questa funzionalità può essere abilitata nel file di configurazione dell'applicazione. Vedere l'[\<elemento gcAllowVeryLargeObjects>](../../../docs/framework/configure-apps/file-schema/runtime/gcallowverylargeobjects-element.md), che elenca anche altre restrizioni per le dimensioni di oggetti e matrici.

- Miglioramento delle prestazioni tramite Garbage Collection in background per server. Se si usa la funzionalità di Garbage Collection del server in [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], verrà automaticamente abilità la Garbage Collection in background. Vedere la sezione "Operazione di Garbage Collection in background per server" nell'argomento [Principi fondamentali di Garbage Collection](../../../docs/standard/garbage-collection/fundamentals.md).

- Compilazione JIT in background, eventualmente disponibile nei processori multicore per migliorare le prestazioni delle applicazioni. Vedere <xref:System.Runtime.ProfileOptimization>.

- Possibilità di limitare il periodo in cui il motore delle espressioni regolari tenta di risolvere un'espressione regolare prima che si verifichi il timeout. Vedere la proprietà <xref:System.Text.RegularExpressions.Regex.MatchTimeout%2A?displayProperty=fullName>.

- Possibilità di definire le impostazioni cultura predefinite per un dominio di applicazione. Vedere la classe <xref:System.Globalization.CultureInfo>.

- Supporto della console per la codifica Unicode (UTF-16). Vedere la classe <xref:System.Console>.

- Supporto per il controllo delle versioni dei dati di confronto e ordinamento delle stringhe di impostazioni cultura. Vedere la classe <xref:System.Globalization.SortVersion>.

- Miglioramento delle prestazioni in fase di recupero di risorse. Vedere [Creazione del pacchetto e distribuzione delle risorse in applicazioni desktop](../../../docs/framework/resources/packaging-and-deploying-resources-in-desktop-apps.md).

- Miglioramenti delle compressioni ZIP per ridurre la dimensione di un file compresso. Vedere lo spazio dei nomi <xref:System.IO.Compression?displayProperty=fullName>.

- Possibilità di personalizzare un contesto di reflection per eseguire l'override del comportamento di reflection predefinito tramite la classe <xref:System.Reflection.Context.CustomReflectionContext>.

- Supporto per la versione 2008 dello standard IDNA (Internationalized Domain Names in Applications) quando si usa la classe <xref:System.Globalization.IdnMapping?displayProperty=fullName> in [!INCLUDE[win8](../../../includes/win8-md.md)].

- Delega del confronto tra stringhe al sistema operativo, che effettua l'implementazione di Unicode 6.0, quando .NET Framework viene usato in [!INCLUDE[win8](../../../includes/win8-md.md)]. Quando è in esecuzione in altre piattaforme, .NET Framework include i propri dati di confronto tra stringhe, che effettua l'implementazione di Unicode 5.x. Vedere la classe <xref:System.String> e la sezione Osservazioni per la classe <xref:System.Globalization.SortVersion>.

- Possibilità di calcolare i codici hash per le stringhe in base al dominio dell'applicazione. Vedere [\<Elemento UseRandomizedStringHashAlgorithm>](../../../docs/framework/configure-apps/file-schema/runtime/userandomizedstringhashalgorithm-element.md).

- Supporto della reflection sui tipi diviso tra le classi <xref:System.Type> e <xref:System.Reflection.TypeInfo> . Vedere [Reflection in .NET Framework per app di Windows Store](../../../docs/framework/reflection-and-codedom/reflection-for-windows-store-apps.md).

### <a name="managed-extensibility-framework-mef"></a>Managed Extensibility Framework (MEF)
 In [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] la libreria Managed Extensibility Framework (MEF) offre le seguenti nuove funzionalità:

- Supporto per tipi generici.

- Modello di programmazione basato su convenzioni che consente di creare parti basate sulle convenzioni di denominazione, anziché sugli attributi.

- Più ambiti.

- Subset di MEF che è possibile usare in fase di creazione delle applicazioni [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]. Questo subset è disponibile come [pacchetto scaricabile](http://go.microsoft.com/fwlink/?LinkId=256238) dalla raccolta NuGet. Per installare il pacchetto, aprire il progetto in Visual Studio, scegliere **Gestisci pacchetti NuGet** dal menu **Progetto** ed eseguire una ricerca online del pacchetto `Microsoft.Composition`.

 Per altre informazioni, vedere [Managed Extensibility Framework (MEF)](../../../docs/framework/mef/index.md).

### <a name="asynchronous-file-operations"></a>Operazioni asincrone sui file.
 In [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] sono state aggiunte nuove funzionalità asincrone nei linguaggi C# e Visual Basic. Con queste funzionalità viene introdotto un modello basato su attività per eseguire operazioni asincrone. Per impiegare questo nuovo modello, usare i metodi asincroni nelle classi I/O. Vedere [I/O di file asincrono](../../../docs/standard/io/asynchronous-file-i-o.md).

<a name="tools"></a> 
### <a name="tools"></a>Strumenti
 In [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] il generatore di file di risorse (Resgen.exe) consente di creare un file con estensione resw per l'uso nelle applicazioni [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] da un file con estensione resources incorporato in un assembly .NET Framework. Per altre informazioni, vedere [Resgen.exe (generatore di file di risorse)](../../../docs/framework/tools/resgen-exe-resource-file-generator.md).

 L'ottimizzazione PGO gestita (Mpgo.exe) consente di migliorare i tempi di avvio delle applicazioni, l'uso della memoria (dimensione del working set) e la velocità effettiva attraverso l'ottimizzazione degli assembly di immagini nativi. Lo strumento da riga di comando genera dati di profilo per assembly di applicazioni di immagini nativi. Vedere [Strumento Mpgo.exe (Managed Profile Guided Optimization)](../../../docs/framework/tools/mpgo-exe-managed-profile-guided-optimization-tool.md). A partire da [!INCLUDE[vs_dev12](../../../includes/vs-dev12-md.md)] è possibile usare Mgpo.exe per ottimizzare le applicazioni [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] e quelle desktop.

<a name="parallel"></a> 
### <a name="parallel-computing"></a>Elaborazione parallela
 In [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] vengono forniti diversi miglioramenti e nuove funzionalità per il calcolo parallelo. Alcuni esempi: miglioramento delle prestazioni, maggiore controllo, supporto avanzato per la programmazione asincrona, una nuova libreria di flussi di dati e un miglioramento del supporto per il debug parallelo e l'analisi delle prestazioni. Vedere la voce relativa alle [novità per il parallelismo in .NET 4.5](http://go.microsoft.com/fwlink/?LinkId=235061) nel blog sulla programmazione parallela con .NET.

<a name="web"></a> 
### <a name="web"></a>Web
 In ASP.NET 4.5 e 4.5.1 vengono aggiunti associazione di modelli per Web Form, supporto di WebSocket, gestori asincroni, miglioramenti delle prestazioni e molte altre funzionalità. Per altre informazioni, vedere le seguenti risorse:

- [ASP.NET 4.5 e Visual Studio 2012](http://msdn.microsoft.com/library/ac9bb7f6-f094-4af7-bad0-acf49a5dbc55) in MSDN Library.

- [ASP.NET 4.5.1 e Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=309094) nel sito Web ASP.NET.

<a name="networking"></a> 
### <a name="networking"></a>Rete
 In [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] viene fornita una nuova interfaccia di programmazione per applicazioni HTTP. Per altre informazioni, vedere i nuovi spazi dei nomi <xref:System.Net.Http?displayProperty=fullName> e <xref:System.Net.Http.Headers?displayProperty=fullName>.

 È inoltre incluso il supporto per una nuova interfaccia di programmazione per l'accettazione e l'interazione con una connessione WebSocket usando l'oggetto <xref:System.Net.HttpListener> esistente e le classi correlate. Per altre informazioni, vedere il nuovo spazio dei nomi <xref:System.Net.WebSockets> e la classe <xref:System.Net.HttpListener>.

 In [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] sono inoltre inclusi i seguenti miglioramenti di rete:

- Supporto URI conforme a RFC. Per altre informazioni, vedere <xref:System.Uri> e le classi correlate.

- Supporto per l'analisi IDN (Internationalized Domain Name). Per altre informazioni, vedere <xref:System.Uri> e le classi correlate.

- Supporto per EAI (Email Address Internationalization). Per altre informazioni, vedere lo spazio dei nomi <xref:System.Net.Mail>.

- Supporto IPv6 avanzato. Per altre informazioni, vedere lo spazio dei nomi <xref:System.Net.NetworkInformation>.

- Supporto per socket dual mode. Per altre informazioni vedere le classi <xref:System.Net.Sockets.Socket> e <xref:System.Net.Sockets.TcpListener>.

<a name="client"></a> 
### <a name="windows-presentation-foundation-wpf"></a>Windows Presentation Foundation (WPF)
 In [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] Windows Presentation Foundation (WPF) include miglioramenti e modifiche nelle aree seguenti:

- Nuovo controllo <xref:System.Windows.Controls.Ribbon.Ribbon>, che permette di implementare l'interfaccia utente di una barra multifunzione che ospita una barra di accesso rapido, il menu dell'applicazione e alcune schede.

- Nuova interfaccia <xref:System.ComponentModel.INotifyDataErrorInfo>, che supporta la convalida sincrona e asincrona dei dati.

- Nuove funzionalità per le classi <xref:System.Windows.Controls.VirtualizingPanel> e <xref:System.Windows.Threading.Dispatcher>.

- Miglioramento delle prestazioni durante la visualizzazione di grandi set di dati raggruppati e mediante l'accesso alle raccolte in thread non dell'interfaccia utente.

- Data binding a proprietà statiche, data binding a tipi personalizzati che implementano l'interfaccia <xref:System.Reflection.ICustomTypeProvider> e recupero di informazioni sul data binding da un'espressione di binding.

- Riposizionamento di dati contestuale alla modifica dei valori (shaping attivo).

- Possibilità di controllare se il contesto dei dati per un contenitore di elementi è disconnesso.

- Possibilità di impostare la quantità di tempo che deve trascorrere tra le modifiche alle proprietà e gli aggiornamenti delle origini dati.

- Supporto avanzato per l'implementazione di modelli di eventi deboli. Inoltre, gli eventi possono ora accettare estensioni di markup.

<a name="windows_communication_foundation"></a> 
### <a name="windows-communication-foundation-wcf"></a>Windows Communication Foundation (WCF)
 In [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] le seguenti funzionalità sono state aggiunte per semplificare la scrittura e la gestione di applicazioni Windows Communication Foundation (WCF):

- Semplificazione dei file di configurazione generati.

- Supporto per lo sviluppo con priorità al contratto ("contract-first").

- Possibilità di configurare la modalità di compatibilità ASP.NET in modo più semplice.

- Modifiche ai valori predefiniti delle proprietà di trasporto per ridurre la probabilità di doverli impostare.

- Aggiornamenti alla classe <xref:System.Xml.XmlDictionaryReaderQuotas> per ridurre la probabilità di dover configurare manualmente le quote per i lettori di dizionario XML.

- Convalida dei file di configurazione WCF da parte di Visual Studio nell'ambito del processo di compilazione, in modo da poter rilevare errori di configurazione prima di eseguire l'applicazione.

- Nuovo supporto per lo streaming asincrono.

- Nuovo mapping del protocollo HTTPS per semplificare l'esposizione di un endpoint su HTTPS con Internet Information Services (IIS).

- Possibilità di generare metadati in un singolo documento WSDL aggiungendo `?singleWSDL` all'URL del servizio.

- Supporto di WebSocket per consentire un'effettiva comunicazione bidirezionale sulle porte 80 e 443 con caratteristiche di prestazioni simili al trasporto TCP.

- Supporto per la configurazione dei servizi nel codice.

- Descrizioni comando dell'editor XML.

- Supporto per la memorizzazione nella cache di <xref:System.ServiceModel.ChannelFactory>.

- Supporto della compressione del codificatore binario.

- Supporto per un trasporto UDP che consente agli sviluppatori di scrivere servizi che usano la messaggistica di tipo "Fire and Forget". Un client invia un messaggio a un servizio e non prevede alcuna risposta dal servizio.

- Possibilità di supportare più modalità di autenticazione in un singolo endpoint WCF quando si usa il trasporto HTTP e la sicurezza del trasporto.

- Supporto per servizi WCF che usano IDN (Internationalized Domain Name).

 Per altre informazioni, vedere [Novità di Windows Communication Foundation](http://go.microsoft.com/fwlink/?LinkId=228173).

<a name="windows_workflow_foundation"></a> 
### <a name="windows-workflow-foundation-wf"></a>Windows Workflow Foundation (WF)
 In [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] sono state introdotte numerose nuove funzionalità in Windows Workflow Foundation (WF), tra cui:

- Flussi di lavoro della macchina a stati, introdotti per la prima volta in .NET Framework 4.0.1 ([.NET Framework 4 Platform Update 1](http://go.microsoft.com/fwlink/?LinkID=215092)). In questo aggiornamento erano incluse diverse nuove classi e attività che consentivano agli sviluppatori di creare flussi di lavoro macchina a stati. Queste classi e attività sono state aggiornate per [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] al fine di includere:

    - Possibilità di impostare punti di interruzione negli stati.

    - Possibilità di copiare e incollare transizioni in Workflow Designer.

    - Supporto della finestra di progettazione per la creazione di transizioni con trigger condivisi.

    - Attività per la creazione di flussi di lavoro della macchina a stati, tra cui: <xref:System.Activities.Statements.StateMachine>, <xref:System.Activities.Statements.State> e <xref:System.Activities.Statements.Transition>.

- Funzionalità avanzate di Workflow Designer, tra cui:

    - Funzionalità avanzate di ricerca di flussi di lavoro in Visual Studio, tra cui **Ricerca veloce** e **Cerca nei file**.

    - Possibilità di creare automaticamente un'attività Sequence quando viene aggiunta una seconda attività figlio a un'attività del contenitore e di includere entrambe le attività nell'attività Sequence.

    - Supporto per panoramica, che consente di modificare la parte visibile di un flusso di lavoro senza ricorrere a barre di scorrimento.

    - Nuova visualizzazione **Struttura documento** che mostra i componenti di un flusso di lavoro in una visualizzazione in stile albero e permette di selezionare un componente nella visualizzazione **Struttura documento**.

    - Possibilità di aggiungere annotazioni alle attività.

    - Capacità di definire e usare delegati di attività mediante Workflow Designer.

    - Connessione e inserimento automatici per attività e transizioni nei flussi di lavoro macchina a stati e del diagramma di flusso.

- Archiviazione di informazioni sullo stato di visualizzazione per un flusso di lavoro in un singolo elemento nel file XAML, in modo da poter individuare e modificare agevolmente tali informazioni.

- Attività del contenitore NoPersistScope per impedire la conservazione delle attività figlio.

- Supporto per espressioni C#:

    - I progetti di flusso di lavoro che usano Visual Basic impiegheranno espressioni Visual Basic, mentre i progetti di flusso di lavoro C# useranno espressioni C#.

    - I progetti di flusso di lavoro C# creati in Visual Studio 2010 e con espressioni Visual Basic sono compatibili con i progetti di flusso di lavoro C# che usano espressioni C#.

- Miglioramenti del controllo delle versioni:

    - Nuova classe <xref:System.Activities.WorkflowIdentity>, che fornisce un mapping tra un'istanza di flusso di lavoro persistente e la definizione del flusso di lavoro.

    - Esecuzione affiancata di più versioni del flusso di lavoro nello stesso host, incluso <xref:System.ServiceModel.Activities.WorkflowServiceHost>.

    - In Aggiornamento dinamico, capacità di modificare la definizione di un'istanza di flusso di lavoro persistente.

- Sviluppo di flussi di lavoro con priorità al contratto ("contract-first"), che fornisce supporto per generare automaticamente attività in modo da soddisfare un contratto di servizio esistente.

 Per altre informazioni, vedere [Novità di Windows Workflow Foundation](http://go.microsoft.com/fwlink/?LinkId=228176).

<a name="tailored"></a> 
### [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)]
 Le applicazioni [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] sono progettate per fattori di forma specifici e sfruttano la potenza del sistema operativo Windows. Un subset di [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] o 4.5.1 è disponibile per la compilazione di applicazioni [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] per Windows usando C# o Visual Basic. Questo subset è denominato [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)] e viene descritto in una [panoramica](http://go.microsoft.com/fwlink/?LinkId=228491) in Windows Dev Center.

<a name="portable"></a> 
### <a name="portable-class-libraries"></a>Librerie di classi portabili
 Il progetto Libreria di classi portabile in [!INCLUDE[vs_dev11_long](../../../includes/vs-dev11-long-md.md)] (e versioni successive) consente di scrivere e compilare assembly gestiti compatibili con più piattaforme .NET Framework. Se si usa un progetto Libreria di classi portabile, si scelgono le piattaforme (ad esempio Windows Phone e [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)]) di destinazione. I tipi e i membri disponibili nel progetto sono automaticamente limitati a tipi e membri comuni in queste piattaforme. Per altre informazioni, vedere [Libreria di classi portabile](../../../docs/standard/cross-platform/cross-platform-development-with-the-portable-class-library.md).

## <a name="see-also"></a>Vedere anche
 [.NET Framework e rilascio fuori programma](../../../docs/framework/get-started/the-net-framework-and-out-of-band-releases.md)   
 [Novità di Visual Studio 2017](/visualstudio/ide/whats-new-in-visual-studio)   
 [ASP.NET](/aspnet)   
 [Novità di Visual C++](/cpp/what-s-new-for-visual-cpp-in-visual-studio) 

