---
title: "Novit&#224; di .NET Framework | Microsoft Docs"
ms.custom: ""
ms.date: "04/07/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "novità [.NET Framework]"
ms.assetid: 1d971dd7-10fc-4692-8dac-30ca308fc0fa
caps.latest.revision: 292
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 287
---
# Novit&#224; di .NET Framework
<a name="introduction"></a>In questo articolo riepiloga le nuove funzionalità principali e i miglioramenti nelle seguenti versioni di .NET Framework:  
  
 [.NET framework 4.6.2](#v462)   
 [.NET framework 4.6.1](#v461)   
 [.NET 2015 e .NET Framework 4.6](#v46)   
 [.NET framework 4.5.2](#v452)   
 [.NET framework 4.5.1](#v451)   
 [.NET framework 4.5](#core)  
  
 Non vengono fornite informazioni complete su ogni nuova funzionalità e l'articolo è soggetto a modifiche. Per informazioni generali su .NET Framework, vedere [Introduzione](../../../docs/framework/get-started/index.md). Per le piattaforme supportate, vedere [requisiti di sistema](../../../docs/framework/get-started/system-requirements.md). Per i collegamenti ai download e istruzioni di installazione, vedere [Guida all'installazione](../../../docs/framework/install/guide-for-developers.md).  
  
> [!NOTE]
>  Il team di .NET Framework rilascia anche funzionalità fuori programma con NuGet per espandere il supporto di piattaforme e introdurre nuove funzionalità, ad esempio le raccolte non modificabili e tipi di vettori abilitati per SIMD. Per ulteriori informazioni, vedere [altre librerie di classi e API](../../../ml/index.xml) e [di .NET Framework e rilascio Out-of-Band](../../../docs/framework/get-started/the-net-framework-and-out-of-band-releases.md). Vedere un [elenco completo dei pacchetti NuGet](http://blogs.msdn.com/b/dotnet/p/nugetpackages.aspx) per .NET Framework o sottoscrivere [nostro feed](https://nuget.org/api/v2/curated-feeds/dotnetframework/Packages/).  
  
<a name="v462"></a>   
## <a name="introducing-the-net-framework-462"></a>Introduzione a .NET Framework 4.6.2  
 [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] è basato su .NET Framework 4.6 e 4.6.1 con l'aggiunta di molte nuove correzioni e funzionalità, pur rimanendo un prodotto molto stabile.  
  
### <a name="downloading-and-installing-the-net-framework-462"></a>Download e installazione di .NET Framework 4.6.2  
 È possibile scaricare [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] dalle posizioni seguenti:  
  
-   [Programma di installazione di .NET framework 4.6.2 Web](http://go.microsoft.com/fwlink/?LinkId=780597)  
  
-   [Programma di installazione Offline di NET Framework 4.6.2](http://go.microsoft.com/fwlink/?LinkId=780601)  
  
 [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] può essere installato in Windows 10, Windows 8.1, Windows 7 e nelle piattaforme server corrispondenti a partire da Windows Server 2008 R2 SP1. Si può installare [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] usando il programma di installazione Web o il programma di installazione offline. Per la maggior parte degli utenti è consigliabile usare il programma di installazione Web.  
  
 È possibile destinare il [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] in Visual Studio 2012 o versioni successive mediante l'installazione di [Developer Pack per .NET Framework 4.6.2](http://go.microsoft.com/fwlink/?LinkId=780617).  
  
### <a name="whats-new-in-the-net-framework-462"></a>Novità di .NET Framework 4.6.2  
 [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] include nuove funzionalità nelle aree seguenti:  
  
-   [ASP.NET&2;.0](#ASPNET462)  
  
-   [Categorie di caratteri](#Strings)  
  
-   [Crittografia](#Crypto462)  
  
-   [SqlClient](#SQLClient)  
  
-   [Windows Communication Foundation](#WCF)  
  
-   [Windows Presentation Foundation (WPF)](#WPF462)  
  
-   [Windows Workflow Foundation (WF)](#WF462)  
  
-   [ClickOnce](#ClickOnce)  
  
-   [Conversione di Windows Form e WPF App per App UWP](#UWPConvert)  
  
-   [Miglioramenti apportati al debug](#Debug462)  
  
 Per aggiunta un elenco delle nuove API di [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], vedere [modifiche all'API di .NET Framework 4.6.2](https://github.com/Microsoft/dotnet/blob/master/releases/net462/dotnet462-api-changes.md) su GitHub. Per un elenco dei miglioramenti delle funzionalità e correzioni di bug nel [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], vedere [modifiche all'API di .NET Framework 4.6.2](http://go.microsoft.com/fwlink/?LinkId=708778) su GitHub.  Per ulteriori informazioni, vedere [annuncio di .NET Framework 4.6.2](https://blogs.msdn.microsoft.com/dotnet/2016/08/02/announcing-net-framework-4-6-2/) nel Blog di .NET.  
  
<a name="ASPNET462"></a>   
### <a name="aspnet"></a>ASP.NET  
 In [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], ASP.NET include i miglioramenti seguenti:  
  
 **Supporto migliorato per i messaggi di errore localizzato di convalide di annotazione dei dati**  
 I validator di annotazione dei dati consentono di eseguire la convalida aggiungendo uno o più attributi a una proprietà di classe. L'attributo <xref:System.ComponentModel.DataAnnotations.ValidationAttribute.ErrorMessage%2A?displayProperty=fullName> elemento definisce il testo del messaggio di errore se la convalida non riesce. A partire da [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], ASP.NET semplifica la localizzazione dei messaggi di errore. I messaggi di errore verranno localizzati se:  
  
1.  Il <xref:System.ComponentModel.DataAnnotations.ValidationAttribute.ErrorMessage%2A?displayProperty=fullName> viene fornito nell'attributo di convalida.  
  
2.  Il file di risorse è archiviato nella cartella App_LocalResources.  
  
3.  Il nome del file di risorse localizzate ha il formato `DataAnnotation.Localization.{` *nome*`}.resx`, dove *nome* è un nome di impostazioni cultura nel formato *languageCode*`-`*paese/regionCode* o *languageCode*.  
  
4.  Il nome della chiave della risorsa è la stringa assegnata al <xref:System.ComponentModel.DataAnnotations.ValidationAttribute.ErrorMessage%2A?displayProperty=fullName> attributo e il relativo valore è il messaggio di errore localizzato.  
  
 Ad esempio, l'attributo di annotazione dati seguente definisce il messaggio di errore della lingua predefinita per un valore di classificazione non valido.  
  
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
  
 È quindi possibile creare un file di risorse, DataAnnotation.Localization.fr.resx, la cui chiave è la stringa di messaggio di errore e il cui valore è il messaggio di errore localizzato. Il file deve trovarsi nel `App.LocalResources` cartella. Ad esempio, di seguito è la chiave e il relativo valore nel messaggio di errore localizzato lingua francese (fr):  
  
|Nome|Valore|  
|----------|-----------|  
|La classificazione deve essere compreso tra 1 e 10.|Si noti la être doit costituiscono entre 1 e 10.|  
  
 Questo file può quindi  
  
 La localizzazione dell'annotazione dei dati è anche estensibile. Gli sviluppatori possono plug-nel proprio provider di localizzatore stringa mediante l'implementazione di <xref:System.Web.Globalization.IStringLocalizerProvider> interfaccia per archiviare stringhe di localizzazione in un punto diverso in un file di risorse.  
  
 **Supporto asincrono con i provider dell'archivio dello stato sessione**  
 ASP.NET ora offre metodi di restituzione di Task da usare con i provider dell'archivio per lo stato sessione, consentendo quindi alle applicazioni ASP.NET di sfruttare i vantaggi delle operazioni asincrone in termini di scalabilità. Supporta operazioni asincrone con lo stato della sessione provider di archiviazione, ASP.NET include una nuova interfaccia, <xref:System.Web.SessionState.ISessionStateModule?displayProperty=fullName>, che eredita da <xref:System.Web.IHttpModule> e consente agli sviluppatori di implementare i propri provider dello stato sessione modulo e async sessione archivio. L'interfaccia viene definita come segue:  
  
```csharp  
  
public interface ISessionStateModule : IHttpModule {  
    void ReleaseSessionState(HttpContext context);  
    Task ReleaseSessionStateAsync(HttpContext context);  
}  
  
```  
  
 Inoltre, il <xref:System.Web.SessionState.SessionStateUtility> classe include due nuovi metodi, <xref:System.Web.SessionState.SessionStateUtility.IsSessionStateReadOnly%2A> e <xref:System.Web.SessionState.SessionStateUtility.IsSessionStateRequired%2A>, che può essere utilizzato per supportare le operazioni asincrone.  
  
 **Supporto asincrono per i provider di cache di output**  
 A partire da [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], i metodi di restituzione di Task possono essere usati con i provider di cache di output per usufruire dei vantaggi di scalabilità offerti dalle operazioni asincrone.  I provider che implementano questi metodi riducono i blocchi dei thread su un server Web e migliorano la scalabilità di un servizio ASP.NET.  
  
 Per supportare i provider di cache di output asincroni sono state aggiunte le API seguenti:  
  
-   Il <xref:System.Web.Caching.OutputCacheProviderAsync?displayProperty=fullName> , classe che eredita da <xref:System.Web.Caching.OutputCacheProvider?displayProperty=fullName> e consente agli sviluppatori di implementare un provider di cache di output asincrono.  
  
-   Il <xref:System.Web.Caching.OutputCacheUtility> (classe), che fornisce i metodi di supporto per la configurazione della cache di output.  
  
-   18 nuovi metodi di <xref:System.Web.HttpCachePolicy?displayProperty=fullName>(classe). Questi includono <xref:System.Web.HttpCachePolicy.GetCacheability%2A>, <xref:System.Web.HttpCachePolicy.GetCacheExtensions%2A>, <xref:System.Web.HttpCachePolicy.GetETag%2A>, <xref:System.Web.HttpCachePolicy.GetETagFromFileDependencies%2A>, <xref:System.Web.HttpCachePolicy.GetMaxAge%2A>, <xref:System.Web.HttpCachePolicy.GetMaxAge%2A>, <xref:System.Web.HttpCachePolicy.GetNoStore%2A>, <xref:System.Web.HttpCachePolicy.GetNoTransforms%2A>, <xref:System.Web.HttpCachePolicy.GetOmitVaryStar%2A>, <xref:System.Web.HttpCachePolicy.GetProxyMaxAge%2A>, <xref:System.Web.HttpCachePolicy.GetRevalidation%2A>, <xref:System.Web.HttpCachePolicy.GetUtcLastModified%2A>, <xref:System.Web.HttpCachePolicy.GetVaryByCustom%2A>, <xref:System.Web.HttpCachePolicy.HasSlidingExpiration%2A>, e <xref:System.Web.HttpCachePolicy.IsValidUntilExpires%2A>.  
  
-   2 nuovi metodi di <xref:System.Web.HttpCacheVaryByContentEncodings?displayProperty=fullName> classe: <xref:System.Web.HttpCacheVaryByContentEncodings.GetContentEncodings%2A> e <xref:System.Web.HttpCacheVaryByContentEncodings.SetContentEncodings%2A>.  
  
-   2 nuovi metodi di <xref:System.Web.HttpCacheVaryByHeaders?displayProperty=fullName> classe: <xref:System.Web.HttpCacheVaryByHeaders.GetHeaders%2A> e <xref:System.Web.HttpCacheVaryByHeaders.SetHeaders%2A>.  
  
-   2 nuovi metodi di <xref:System.Web.HttpCacheVaryByParams?displayProperty=fullName> classe: <xref:System.Web.HttpCacheVaryByParams.GetParams%2A> e <xref:System.Web.HttpCacheVaryByParams.SetParams%2A>.  
  
-   Nel <xref:System.Web.Caching.AggregateCacheDependency?displayProperty=fullName> (classe), il <xref:System.Web.Caching.AggregateCacheDependency.GetFileDependencies%2A> metodo.  
  
-   Nel <xref:System.Web.Caching.CacheDependency>, <xref:System.Web.Caching.CacheDependency.GetFileDependencies%2A> metodo.  
  
<a name="Strings"></a>   
### <a name="character-categories"></a>Categorie di caratteri  
 I caratteri di [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] sono classificati in base il [Unicode Standard, versione 8.0.0](http://www.unicode.org/versions/Unicode8.0.0/). In [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] e [!INCLUDE[net_v461](../../../includes/net-v461-md.md)], i caratteri sono stati classificati in base alle categorie di caratteri Unicode 6.3.  
  
 Supporto per Unicode 8.0 è limitato per la classificazione dei caratteri per il <xref:System.Globalization.CharUnicodeInfo> classe e ai tipi e metodi che si basano su di esso. Sono inclusi il <xref:System.Globalization.StringInfo> classe di overload <xref:System.Char.GetUnicodeCategory%2A?displayProperty=fullName> (metodo) e [classi character](../../../docs/standard/base-types/character-classes-in-regular-expressions.md) riconosciuto dal motore delle espressioni regolari di .NET Framework.  Il confronto e l'ordinamento di stringhe e caratteri non sono interessati da questa modifica e continuano a basarsi sul sistema operativo sottostante o, nei sistemi Windows 7, sui dati dei caratteri provenienti da .NET Framework.  
  
 Per le modifiche in categorie di caratteri da Unicode 6.0 a 7.0 Unicode, vedere [lo Unicode Standard, versione 7.0.0](http://www.unicode.org/versions/Unicode7.0.0/) sul sito Web di Unicode Consortium. Per le modifiche da 7.0 Unicode a Unicode 8.0, vedere [lo Unicode Standard, versione 8.0.0](http://www.unicode.org/versions/Unicode8.0.0/) sul sito Web di Unicode Consortium.  
  
<a name="Crypto462"></a>   
### <a name="cryptography"></a>Crittografia  
 **Supporto per X509 certificati contiene DSA FIPS 186-3**  
 [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] aggiunge il supporto per certificati DSA (Digital Signature Algorithm) X509 le cui chiavi superano il limite FIPS 186-2 di 1024 bit.  
  
 Oltre a supportare le dimensioni della chiave più grandi di FIPS 186-3, [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] consente di calcolare le firme con la famiglia SHA-2 di algoritmi hash (SHA256, SHA384 e SHA512). FIPS 186-3 sono supportati dal nuovo <xref:System.Security.Cryptography.DSACng?displayProperty=fullName> (classe).  
  
 In conformità con le modifiche più recenti di <xref:System.Security.Cryptography.RSA> classe in .NET Framework 4.6 e <xref:System.Security.Cryptography.ECDsa> classe in .NET Framework 4.6.1, il <xref:System.Security.Cryptography.DSA> nella classe di base astratta [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] sono disponibili ulteriori metodi per consentire ai chiamanti di usare questa funzionalità senza eseguire il cast. È possibile chiamare il <xref:System.Security.Cryptography.X509Certificates.DSACertificateExtensions.GetDSAPrivateKey%2A?displayProperty=fullName> metodo di estensione per firmare i dati, come illustrato nell'esempio seguente.  
  
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
  
 Ed è possibile chiamare il <xref:System.Security.Cryptography.X509Certificates.DSACertificateExtensions.GetDSAPublicKey%2A?displayProperty=fullName> metodo di estensione per verificare i dati firmati, come illustrato nell'esempio seguente.  
  
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
  
 **Per gli input alle routine di derivazione della chiave ECDiffieHellman più efficacemente**  
 .NET Framework 3.5 offre in più il supporto per la chiave concordata Ellipic Curve Diffie-Hellman con tre diverse routine di funzione di derivazione chiave (KDF). Gli input per le routine e le routine, sono stati configurati tramite la proprietà sul <xref:System.Security.Cryptography.ECDiffieHellmanCng> oggetto. Ma poiché non tutte le routine leggono tutte le proprietà di input, in passato era molto probabile che si creasse confusione per lo sviluppatore.  
  
 Per risolvere questo problema nel [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], sono stati aggiunti tre metodi seguenti di <xref:System.Security.Cryptography.ECDiffieHellman> classe per rappresentare più chiaramente le routine di utilizzo e i relativi input di base:  
  
|Metodo ECDiffieHellman|Descrizione|  
|----------------------------|-----------------|  
|[DeriveKeyFromHash (Byte ECDiffieHellmanPublicKey, HashAlgorithmName,\[\], Byte\<xref:System.Security.Cryptography.ECDiffieHellman.DeriveKeyFromHash%28System.Security.Cryptography.ECDiffieHellmanPublicKey%2CSystem.Security.Cryptography.HashAlgorithmName%2CSystem.Byte%5B%5D%2CSystem.Byte%5B%5D%29>|Deriva il materiale della chiave usando la formula<br /><br /> HASH(secretPrepend || *x* | | secretAppend)<br /><br /> HASH (secretPrepend OrElse *x* OrElse secretAppend)<br /><br /> dove *x* è il risultato calcolato dell'algoritmo Diffie-Hellman CE.|  
|[DeriveKeyFromHmac (Byte ECDiffieHellmanPublicKey, HashAlgorithmName,\[\], Byte\[\], Byte\<xref:System.Security.Cryptography.ECDiffieHellman.DeriveKeyFromHmac%28System.Security.Cryptography.ECDiffieHellmanPublicKey%2CSystem.Security.Cryptography.HashAlgorithmName%2CSystem.Byte%5B%5D%2CSystem.Byte%5B%5D%2CSystem.Byte%5B%5D%29>|Deriva il materiale della chiave usando la formula<br /><br /> Codice HMAC (hmacKey, secretPrepend | | *x* | | secretAppend)<br /><br /> Codice HMAC (hmacKey, secretPrepend OrElse *x* secretAppend OrElse)<br /><br /> dove *x* è il risultato calcolato dell'algoritmo Diffie-Hellman CE.|  
|[DeriveKeyTls (ECDiffieHellmanPublicKey, Byte\[\], Byte\<xref:System.Security.Cryptography.ECDiffieHellman.DeriveKeyTls%28System.Security.Cryptography.ECDiffieHellmanPublicKey%2CSystem.Byte%5B%5D%2CSystem.Byte%5B%5D%29>|Deriva il materiale della chiave usando l'algoritmo di derivazione TLS della funzione pseudocasuale.|  
  
 **Supporto per la crittografia simmetrica chiave persistente**  
 La libreria di crittografia di Windows (CNG) ha aggiunto il supporto per l'archiviazione delle chiavi simmetriche persistenti e l'uso delle chiavi simmetriche archiviate nell'hardware e [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] rende possibile l'uso di questa funzionalità da parte degli sviluppatori.  Poiché le nozioni di nome della chiave e provider di chiavi sono specifiche dell'implementazione, questa funzionalità richiede l'uso del costruttore dei tipi di implementazione concreti anziché della modalità factory preferita, ad esempio la chiamata a `Aes.Create`.  
  
 Supporto della crittografia simmetrica chiave persistente esiste per AES (<xref:System.Security.Cryptography.AesCng>) e 3DES (<xref:System.Security.Cryptography.TripleDESCng>) algoritmi. Ad esempio:  
  
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
  
 **Supporto SignedXml per generare un hash SHA-2**  
 Il [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] aggiunge il supporto per il <xref:System.Security.Cryptography.Xml.SignedXml> classe per i metodi di firma RSA-SHA256, SHA384 RSA e SHA512 RSA PKCS&#1; e SHA256, SHA384 e SHA512 fanno riferimento gli algoritmi.  
  
 Le costanti URI sono esposte in <xref:System.Security.Cryptography.Xml.SignedXml>:  
  
|Campo SignedXml|Costante|  
|---------------------|--------------|  
|<xref:System.Security.Cryptography.Xml.SignedXml.XmlDsigSHA256Url>|"http://www.w3.org/2001/04/xmlenc#sha256"|  
|<xref:System.Security.Cryptography.Xml.SignedXml.XmlDsigRSASHA256Url>|"http://www.w3.org/2001/04/xmldsig-more#rsa-sha256"|  
|<xref:System.Security.Cryptography.Xml.SignedXml.XmlDsigSHA384Url>|"http://www.w3.org/2001/04/xmldsig-more#sha384"|  
|<xref:System.Security.Cryptography.Xml.SignedXml.XmlDsigRSASHA384Url>|"http://www.w3.org/2001/04/xmldsig-more#rsa-sha384"|  
|<xref:System.Security.Cryptography.Xml.SignedXml.XmlDsigSHA512Url>|"http://www.w3.org/2001/04/xmlenc#sha512"|  
|<xref:System.Security.Cryptography.Xml.SignedXml.XmlDsigRSASHA512Url>|"http://www.w3.org/2001/04/xmldsig-more#rsa-sha512"|  
  
 Tutti i programmi che hanno registrato un oggetto personalizzato <xref:System.Security.Cryptography.SignatureDescription> gestore in <xref:System.Security.Cryptography.CryptoConfig> per aggiungere il supporto per questi algoritmi continueranno a funzionare come facevano in passato, ma poiché esistono ora piattaforma per impostazione predefinita, il <xref:System.Security.Cryptography.CryptoConfig> registrazione non è più necessaria.  
  
<a name="SQLClient"></a>   
### <a name="sqlclient"></a>SqlClient  
 Provider di dati .NET framework per SQL Server (<xref:System.Data.SqlClient?displayProperty=fullName>) include le nuove funzionalità seguenti di [!INCLUDE[net_v462](../../../includes/net-v462-md.md)]:  
  
 **Il pool di connessioni e i timeout con i database SQL Azure**  
 Quando il pool di connessioni è abilitato e si verifica un timeout o un altro errore di accesso, nella cache viene memorizzata un'eccezione e tale l'eccezione memorizzata nella cache viene generata per qualsiasi tentativo di connessione effettuato nei 5 secondi successivi e fino a 1 minuto.  Per ulteriori informazioni, vedere [SQL Server Connection Pooling (ADO.NET)](../../../docs/framework/data/adonet/sql-server-connection-pooling.md).  
  
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
  
 **Miglioramenti per sempre crittografato**  
 SQLClient introduce due miglioramenti per Always Encrypted:  
  
-   Per migliorare le prestazioni delle query con parametri su colonne di database crittografate, i metadati di crittografia per i parametri di query ora vengono memorizzati nella cache. Con il <xref:System.Data.SqlClient.SqlConnection.ColumnEncryptionQueryMetadataCacheEnabled%2A?displayProperty=fullName> impostata su `true` (ovvero il valore predefinito), se la stessa query viene chiamata più volte, il client recupera i metadati del parametro dal server di una sola volta.  
  
-   Crittografia chiave le voci delle colonne nella chiave cache ora vengono rimossi dopo un intervallo di tempo configurabile, impostato utilizzando il <xref:System.Data.SqlClient.SqlConnection.ColumnEncryptionKeyCacheTtl%2A?displayProperty=fullName> proprietà.  
  
<a name="WCF"></a>   
### <a name="windows-communication-foundation"></a>Windows Communication Foundation  
 In [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] Windows Communication Foundation è stato ottimizzato nelle aree seguenti:  
  
 **Supporto della sicurezza WCF trasporto per i certificati archiviati utilizzando CNG**  
 La sicurezza del trasporto WCF supporta i certificati archiviati usando la libreria di crittografia di Windows (CNG). In [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] questo supporto è limitato all'utilizzo dei certificati con una chiave pubblica che ha un esponente di lunghezza non superiore a 32 bit. Quando un'applicazione ha come destinazione [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], questa funzionalità è attivata per impostazione predefinita.  
  
 Per le applicazioni che utilizzano il [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] e versioni precedenti ma sono in esecuzione nel [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], questa funzionalità può essere abilitata aggiungendo la riga seguente al [ <> \> ](../../../docs/framework/configure-apps/file-schema/runtime/runtime-element.md) sezione del file app. config o Web. config.  
  
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
  
 **Migliore supporto per più regole di regolazione dell'ora legale dalla classe DataContractJsonSerializer**  
 I clienti possono utilizzare un'impostazione di configurazione dell'applicazione per determinare se il <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> classe supporta più regole di regolazione per un singolo fuso orario. È una funzionalità che prevede il consenso esplicito. Per abilitarla aggiungere la seguente impostazione nel file di configurazione dell'applicazione:  
  
```xml  
  
<runtime>  
     <AppContextSwitchOverrides value="Switch.System.Runtime.Serialization.DoNotUseTimeZoneInfo=false" />  
</runtime>  
  
```  
  
 Quando questa funzionalità è abilitata, un <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> viene utilizzata da object il <xref:System.TimeZoneInfo> digitare anziché il <xref:System.TimeZone> tipo per deserializzare i dati di data e ora. <xref:System.TimeZoneInfo> supporta più regole di regolazione, che rende possibile lavorare con dati cronologici fuso orario.   <xref:System.TimeZone> non esiste.  
  
 Per ulteriori informazioni sui <xref:System.TimeZoneInfo> struttura e regolazioni del fuso orario, vedere [Panoramica sul fuso orario](../../../docs/standard/datetime/time-zone-overview.md).  
  
 **Supporto per mantenere un UTC ora la serializzazione e deserializzazione con la classe XMLSerializer**  
 In genere, quando il <xref:System.Xml.Serialization.XmlSerializer> classe viene utilizzata per serializzare un UTC <xref:System.DateTime> valore, viene creata una stringa di tempo serializzato che mantiene la data e l'ora ma si presuppone l'ora locale.  Ad esempio, se si crea un'istanza di data e ora UTC chiamando il codice seguente:  
  
```csharp  
DateTime utc = new DateTime(2016, 11, 07, 3, 0, 0, DateTimeKind.Utc);  
```  
  
```vb  
Dim utc As New Date(2016, 11, 07, 3, 0, 0, DateTimeKind.Utc)  
```  
  
 il risultato è la stringa di ora serializzata "03:00:00.0000000-08:00" per un sistema otto ore indietro rispetto all'ora UTC.  E i valori serializzati vengono sempre deserializzati come valori di data e ora locali.  
  
 È possibile utilizzare un'impostazione di configurazione dell'applicazione per determinare se il <xref:System.Xml.Serialization.XmlSerializer> mantiene informazioni sul fuso orario UTC durante la serializzazione e deserializzazione <xref:System.DateTime> valori:  
  
```xml  
  
<runtime>  
     <AppContextSwitchOverrides   
          value="Switch.System.Runtime.Serialization.DisableSerializeUTCDateTimeToTimeAndDeserializeUTCTimeToUTCDateTime=false" />  
</runtime>  
  
```  
  
 Quando questa funzionalità è abilitata, un <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> viene utilizzata da object il <xref:System.TimeZoneInfo> digitare anziché il <xref:System.TimeZone> tipo per deserializzare i dati di data e ora. <xref:System.TimeZoneInfo> supporta più regole di regolazione, che rende possibile lavorare con dati cronologici fuso orario.   <xref:System.TimeZone> non esiste.  
  
 Per ulteriori informazioni sui <xref:System.TimeZoneInfo> struttura e regolazioni del fuso orario, vedere [Panoramica sul fuso orario](../../../docs/standard/datetime/time-zone-overview.md).  
  
 **Corrispondenza migliore NetNamedPipeBinding**  
 WCF offre una nuova impostazione di applicazione che può essere specificata sulle applicazioni client in modo da assicurare che si connettano sempre al servizio in ascolto sull'URI che meglio corrisponde a quello richiesto. Con questa impostazione di app impostata su `false` (impostazione predefinita), è possibile che i client che utilizzano <xref:System.ServiceModel.NetNamedPipeBinding> tenterà di connettersi a un servizio in ascolto su un URI che è una sottostringa dell'URI richiesto.  
  
 Ad esempio, un client tenta di connettersi a un servizio in ascolto su `net.pipe://localhost/Service1`, ma un altro servizio in esecuzione nello stesso computer con privilegi di amministratore è in ascolto su `net.pipe://localhost`. Con l'impostazione di applicazione impostata su `false`, il client tenterebbe di connettersi al servizio errato. Dopo aver impostato l'impostazione di applicazione su `true`, il client si connetterà sempre al servizio più pertinente.  
  
> [!NOTE]
>  I client che utilizzano <xref:System.ServiceModel.NetNamedPipeBinding> trovare servizi in base all'indirizzo di base del servizio (se presente) anziché l'indirizzo endpoint completo. Per assicurarsi che l'impostazione funzioni sempre, il servizio deve usare un indirizzo di base univoco.  
  
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
  
-   Il <xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement.SslProtocols%2A?displayProperty=fullName> proprietà  
  
-   Il <xref:System.ServiceModel.TcpTransportSecurity.SslProtocols%2A?displayProperty=fullName> proprietà  
  
-   The [<>\>](../../../docs/framework/configure-apps/file-schema/wcf/transport-of-nettcpbinding.md) section of the [<>\>](../../../docs/framework/configure-apps/file-schema/wcf/nettcpbinding.md) section  
  
-   The [<>\>](../../../docs/framework/configure-apps/file-schema/wcf/sslstreamsecurity.md) section of the [<>\>](../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md) section  
  
<a name="WPF462"></a>   
### <a name="windows-presentation-foundation-wpf"></a>Windows Presentation Foundation (WPF)  
 In [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] Windows Presentation Foundation è stato ottimizzato nelle aree seguenti:  
  
 **Ordinamento di gruppo**  
 Un'applicazione che utilizza un <xref:System.Windows.Data.CollectionView> oggetto per raggruppare i dati ora puoi dichiarare esplicitamente come ordinare i gruppi. L'ordinamento esplicito risolve il problema dell'ordinamento non intuitivo che si verifica quando un'applicazione aggiunge o rimuove in modo dinamico i gruppi o quando modifica il valore delle proprietà dell'elemento interessate dal raggruppamento. Può anche migliorare le prestazioni del processo di creazione dei gruppi spostando i confronti delle proprietà di raggruppamento dall'ordinamento della raccolta completa all'ordinamento dei gruppi.  
  
 Per supportare l'ordinamento di gruppo, il nuovo <xref:System.ComponentModel.GroupDescription.SortDescriptions%2A?displayProperty=fullName> e <xref:System.ComponentModel.GroupDescription.CustomSort%2A?displayProperty=fullName> proprietà viene descritto come ordinare la raccolta di gruppi di prodotti dal <xref:System.ComponentModel.GroupDescription> oggetto. Questo comportamento è analogo a quello che lo stesso nome <xref:System.Windows.Data.ListCollectionView> proprietà viene descritto come ordinare gli elementi di dati.  
  
 Due nuove proprietà statiche di <xref:System.Windows.Data.PropertyGroupDescription> (classe), <xref:System.Windows.Data.PropertyGroupDescription.CompareNameAscending%2A> e <xref:System.Windows.Data.PropertyGroupDescription.CompareNameDescending%2A>, può essere utilizzato per il maggior parte dei casi.  
  
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
  
 **Supporto di tastiera software**  
 Il supporto per la tastiera software consente di rilevare lo stato attivo nelle applicazioni WPF chiamando e chiudendo automaticamente la nuova tastiera software in Windows 10 quando l'input del tocco viene ricevuto da un controllo in grado di accettare input testuale.  
  
 Nelle versioni precedenti di .NET Framework, non è possibile attivare il rilevamento dello stato attivo nelle applicazioni WPF senza disabilitare il supporto WPF per il rilevamento dei movimenti di tocco e penna.  Di conseguenza, le applicazioni WPF devono scegliere tra il supporto completo WPF per il tocco e la promozione del mouse di Windows.  
  
 **DPI monitor**  
 Per supportare la recente proliferazione di ambienti ad alta risoluzione e risoluzione ibrida per le applicazioni WPF, in [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] WPF consente di abilitare la sensibilità ai valori DPI del monitor. Vedere il [esempi e Guida per gli sviluppatori](https://github.com/Microsoft/WPF-Samples/tree/master/PerMonitorDPI) su GitHub per ulteriori informazioni su come abilitare l'applicazione WPF per diventare DPI monitor al grado di riconoscere.  
  
 Nelle versioni precedenti di .NET Framework, le applicazioni WPF sono compatibili con i valori DPI del sistema. In altre parole, l'interfaccia utente dell'applicazione viene adeguata in modo appropriato dal sistema operativo, in base alla risoluzione del monitor in cui viene eseguito il rendering dell'applicazione. ,  
  
 Per le applicazioni in esecuzione con il [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], è possibile disabilitare le modifiche DPI monitor nelle applicazioni WPF tramite l'aggiunta di un'istruzione di configurazione per il [ <> \> ](../../../docs/framework/configure-apps/file-schema/runtime/runtime-element.md) file sezione di configurazione dell'applicazione, come segue:  
  
```xml  
  
<runtime>  
   <AppContextSwitchOverrides value=”Switch.System.Windows.DoNotScaleForDpiChanges=false”/>  
</runtime>  
  
```  
  
<a name="WF462"></a>   
### <a name="windows-workflow-foundation-wf"></a>Windows Workflow Foundation (WF)  
 In [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] Windows Workflow Foundation è stato ottimizzato nell'area seguente:  
  
 **Supporto per espressioni c# e IntelliSense nella finestra di progettazione WF Re-hosted**  
 A partire da [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], WF supporta le espressioni C# sia nella progettazione di Visual Studio che nei flussi di lavoro di codice. La riallocazione della progettazione del flusso di lavoro è una funzionalità chiave di WF che consente di usare la finestra di progettazione del flusso di lavoro in un'applicazione esterna a Visual Studio, ad esempio WPF.  Windows Workflow Foundation offre la possibilità di supportare le espressioni C# e IntelliSense nell'utilità di progettazione del flusso di lavoro riallocata. Per ulteriori informazioni, vedere il [blog di Windows Workflow Foundation](http://go.microsoft.com/fwlink/?LinkID=809042&clcid=0x409).  
  
 `Availability of IntelliSense when a customer rebuilds a workflow project from Visual Studio`  
 Nelle versioni di .NET Framework precedenti a [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] IntelliSense viene interrotta nella progettazione del flusso di lavoro quando un cliente ricompila un progetto di flusso di lavoro da Visual Studio. Durante la compilazione del progetto ha esito positivo, i tipi di flusso di lavoro non vengono trovati nella finestra di progettazione e verranno visualizzati gli avvisi da IntelliSense per i tipi di flusso di lavoro mancante nel **elenco errori** finestra. [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] risolve questo problema e rende disponibile IntelliSense.  
  
 **Le applicazioni V1 del flusso di lavoro con il rilevamento del flusso di lavoro sul ora eseguite in modalità FIPS**  
 I computer con modalità di compatibilità FIPS abilitata ora sono in grado di eseguire correttamente un'applicazione di flusso di lavoro tipo versione 1 con tracciabilità del flusso di lavoro attivata. Per abilitare questo scenario, è necessario apportare le modifiche seguenti al file di configurazione dell'applicazione:  
  
```xml  
<add key="microsoft:WorkflowRuntime:FIPSRequired" value="true" />  
```  
  
 Se questo scenario non è abilitato, eseguire l'applicazione continua a generare un'eccezione con il messaggio "Questa implementazione non fa parte degli algoritmi crittografici convalidati per Windows Platform FIPS".  
  
 **Miglioramenti del flusso di lavoro quando si utilizza l'aggiornamento dinamico con Progettazione flussi di lavoro di Visual Studio**  
 La finestra di progettazione del flusso di lavoro ActivityDesigner diagramma di flusso e altri ActivityDesigner del flusso di lavoro ora caricare e visualizzare correttamente i flussi di lavoro che sono state salvate dopo la chiamata di <xref:System.Activities.DynamicUpdate.DynamicUpdateServices.PrepareForUpdate%2A?displayProperty=fullName> metodo. Nelle versioni di .NET Framework prima di [!INCLUDE[net_v462](../../../includes/net-v462-md.md)], caricamento di un file XAML in Visual Studio per un flusso di lavoro è stato salvato dopo la chiamata <xref:System.Activities.DynamicUpdate.DynamicUpdateServices.PrepareForUpdate%2A?displayProperty=fullName> può comportare i seguenti problemi:  
  
-   Progettazione flussi di lavoro non può caricare correttamente il file XAML (quando il <xref:System.Activities.Presentation.ViewState.ViewStateData.Id%2A?displayProperty=fullName> si trova alla fine della riga).  
  
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
 Il *API di debug non gestito* è stato migliorato nel [!INCLUDE[net_v462](../../../includes/net-v462-md.md)] per eseguire ulteriori analisi, quando un <xref:System.NullReferenceException> viene generata in modo che sia possibile determinare che la variabile in una singola riga di codice sorgente è `null`.   A supporto di questo scenario, le API seguenti sono state aggiunte all'API di debug non gestito.  
  
-   Il [ICorDebugCode4](../../../ocs/framework/unmanaged-api/debugging/icordebugcode4-interface.md), [ICorDebugVariableHome](../../../ocs/framework/unmanaged-api/debugging/icordebugvariablehome-interface.md), e [ICorDebugVariableHomeEnum](../../../ocs/framework/unmanaged-api/debugging/icordebugvariablehomeenum-interface.md) interfacce, che espongono le abitazioni native di variabili gestite. Questo consente ai debugger di effettuare alcune analisi di flusso di codice quando un <xref:System.NullReferenceException> si verifica e di lavorare con le versioni precedenti per determinare la variabile di tipo gestita che corrisponde al percorso nativo che è stato `null`.  
  
-   Il [ICorDebugType2::GetTypeID](../Topic/ICorDebugType2::GetTypeID%20Method.md) metodo fornisce un mapping per ICorDebugType per [COR_TYPEID](../../../ocs/framework/unmanaged-api/debugging/cor-typeid-structure.md), che consente al debugger di ottenere un [COR_TYPEID](../../../ocs/framework/unmanaged-api/debugging/cor-typeid-structure.md) senza un'istanza delle ICorDebugType. Le API esistenti in [COR_TYPEID](../../../ocs/framework/unmanaged-api/debugging/cor-typeid-structure.md) può quindi essere utilizzato per determinare il layout della classe del tipo.  
  
<a name="v461"></a>   
## <a name="whats-new-in-the-net-framework-461"></a>Novità di .NET Framework 4.6.1  
 [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] include nuove funzionalità nelle aree seguenti:  
  
-   [Crittografia](#Crypto)  
  
-   [ADO.NET](#ADO.NET461)  
  
-   [Windows Presentation Foundation (WPF)](#WPF461)  
  
-   [Windows Workflow Foundation](#WWF461)  
  
-   [Profilatura](#Profile461)  
  
-   [NGen](#NGEN461)  
  
 Per altre informazioni su [!INCLUDE[net_v461](../../../includes/net-v461-md.md)], vedere gli argomenti seguenti:  
  
-   Il [elenco .NET Framework 4.6.1 delle modifiche](http://go.microsoft.com/fwlink/?LinkId=622964)  
  
-   [Compatibilità delle applicazioni in 4.6.1](../../../docs/framework/migration-guide/application-compatibility-in-the-net-framework-4-6-1.md)  
  
-   [Le differenze delle API di .NET Framework](http://go.microsoft.com/fwlink/?LinkId=622989) (su GitHub)  
  
<a name="Crypto"></a>   
### <a name="cryptography-support-for-x509-certificates-containing-ecdsa"></a>Crittografia: supporto di certificati X509 contenenti ECDSA  
 In .NET Framework 4.6 è stato aggiunto il supporto RSACng per i certificati X509. [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] aggiunge il supporto di certificati X509 con ECDSA (Elliptic Curve Digital Signature Algorithm).  
  
 Offrendo prestazioni migliori e trattandosi di un algoritmo di crittografia più sicuro rispetto a RSA, ECDSA rappresenta un'ottima scelta per ambienti in cui la scalabilità e le prestazioni TLS (Transport Layer Security) sono fattori importanti. L'implementazione di .NET Framework esegue il wrapping delle chiamate nelle funzionalità di Windows esistenti.  
  
 L'esempio di codice seguente illustra quanto sia semplice generare una firma per un flusso di byte usando il nuovo supporto dei certificati X509 ECDSA incluso in [!INCLUDE[net_v461](../../../includes/net-v461-md.md)].  
  
 [!code-csharp[whatsnew.461.crypto#1](../../../samples/snippets/csharp/VS_Snippets_CLR/whatsnew.461.crypto/cs/Code46.cs#1)]
 [!code-vb[whatsnew.461.crypto#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/whatsnew.461.crypto/vb/Code461.vb#1)]  
  
 Emerge una netta differenza rispetto al codice necessario per generare una firma in .NET Framework 4.6.  
  
 [!code-csharp[whatsnew.461.crypto#2](../../../samples/snippets/csharp/VS_Snippets_CLR/whatsnew.461.crypto/cs/Code46.cs#2)]
 [!code-vb[whatsnew.461.crypto#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/whatsnew.461.crypto/vb/Code46.vb#2)]  
  
<a name="ADO.NET461"></a>   
### <a name="adonet"></a>ADO.NET  
 In ADO.NET è stato aggiunto quanto segue:  
  
 Supporto di Crittografia sempre attiva per le chiavi hardware protette  
 ADO.NET ora supporta l'archiviazione nativa delle chiavi master di colonna con Crittografia sempre attiva nei moduli di protezione hardware. Grazie a questo supporto, i clienti possono usare le chiavi asimmetriche archiviate nei moduli di protezione hardware senza dover scrivere provider dell'archivio chiavi master di colonna personalizzati e senza doverli registrare nelle applicazioni.  
  
 I clienti devono installare il provider CSP fornito dal fornitore dei moduli di protezione hardware o i provider dell'archivio chiavi CNG nei server applicazioni o nei computer client per accedere ai dati con Crittografia sempre attiva protetti con le chiavi master di colonna archiviate in un modulo di protezione hardware.  
  
 Migliorare <xref:System.Data.SqlClient.SqlConnectionStringBuilder.MultiSubnetFailover%2A> il comportamento della connessione per AlwaysOn  
 SqlClient ora fornisce automaticamente una connessione più veloce a un gruppo di disponibilità AlwaysOn. Rileva in modo trasparente se l'applicazione si connette a un gruppo di disponibilità AlwaysOn su una subnet diversa e individua rapidamente il server attivo corrente e gli fornisce una connessione. Prima di questa versione, un'applicazione doveva impostare la stringa di connessione in modo da includere `“MultisubnetFailover=true”` per indicare che era connessa a un gruppo di disponibilità AlwaysOn. Senza impostare la parola chiave di connessione su `true`, potrebbe verificarsi un timeout durante la connessione di un'applicazione a un gruppo di disponibilità AlwaysOn. Con questa versione, un'applicazione ha *non* è necessario impostare <xref:System.Data.SqlClient.SqlConnectionStringBuilder.MultiSubnetFailover%2A> a `true` più. Per ulteriori informazioni sul supporto SqlClient per gruppi di disponibilità AlwaysOn, vedere [supporto SqlClient per disponibilità elevata, ripristino di emergenza](../../../docs/framework/data/adonet/sql/sqlclient-support-for-high-availability-disaster-recovery.md).  
  
<a name="WPF461"></a>   
### <a name="windows-presentation-foundation-wpf"></a>Windows Presentation Foundation (WPF)  
 Windows Presentation Foundation include molti miglioramenti e cambiamenti.  
  
 Miglioramento delle prestazioni  
 Il ritardo di attivazione degli eventi tocco è stato risolto in [!INCLUDE[net_v461](../../../includes/net-v461-md.md)]. Inoltre, digitando un <xref:System.Windows.Controls.RichTextBox> controllo non occupano non è più il thread di rendering durante l'input veloce.  
  
 Miglioramenti di controllo ortografico  
 Il controllo ortografico in WPF è stato aggiornato in Windows 8.1 e versioni successive per sfruttare il supporto di altre lingue per il controllo ortografico offerto dal sistema operativo.  La funzionalità non è stata modificata nelle versioni di Windows precedenti a Windows 8.1.  
  
 Come nelle versioni precedenti di .NET Framework, la lingua per un <xref:System.Windows.Controls.TextBox> controllo ora <xref:System.Windows.Controls.RichTextBox> blocco viene rilevato mediante la ricerca di informazioni nell'ordine seguente:  
  
-   `xml:lang`, se presente.  
  
-   Lingua di input corrente.  
  
-   Impostazioni cultura del thread corrente.  
  
 Per ulteriori informazioni sul supporto lingua in WPF, vedere il [post di blog WPF sulle funzionalità di .NET Framework 4.6.1](http://go.microsoft.com/fwlink/?LinkID=691819).  
  
 Supporto aggiuntivo per i dizionari personalizzati per utente  
 In [!INCLUDE[net_v461](../../../includes/net-v461-md.md)] WPF riconosce i dizionari personalizzati che sono registrati a livello globale. Questa funzionalità si aggiunge alla possibilità di registrarli a livello di controllo.  
  
 Nelle versioni precedenti di WPF, i dizionari personalizzati non riconoscono le parole escluse e gli elenchi di correzione automatica. Sono supportati in Windows 8.1 e Windows 10 mediante l'uso di file che possono essere inseriti nella directory `%AppData%\Microsoft\Spelling\<language tag>`.  A questi file si applicano le regole seguenti:  
  
-   I file devono avere estensione dic (per le parole aggiunte), exc (per le parole escluse) o acl (per la correzione automatica).  
  
-   I file devono essere in testo normale UTF-16 LE che inizia con l'indicatore dell'ordine dei byte (BOM, Byte Order Mark).  
  
-   Ogni riga deve essere costituito da una parola (in elenchi di parole aggiunte ed esclusi) o una coppia di correzione automatica con le parole separate da una barra verticale ("|") (nell'elenco di correzione automatica word).  
  
-   Questi file sono considerati di sola lettura e non vengono modificati dal sistema.  
  
> [!NOTE]
>  Questi nuovi formati di file non sono supportati direttamente dalle API di controllo ortografico WPF e i dizionari personalizzati forniti a WPF nelle applicazioni devono continuare a usare i file con estensione lex.  
  
 Esempi  
 Esistono una serie di [esempi WPF](https://msdn.microsoft.com/library/ms771633.aspx) su MSDN. Più di 200 esempi più comuni (in base all'utilizzo) verrà spostato in un [repository GitHub di origine aprire](https://github.com/Microsoft/WPF-Samples). Aiutaci a migliorare esempi inviando a Microsoft una richiesta di pull o apertura un [GitHub problema](https://github.com/Microsoft/WPF-Samples/issues).  
  
 Estensioni DirectX  
 WPF include un [pacchetto NuGet](http://go.microsoft.com/fwlink/?LinkID=691342) che fornisce nuove implementazioni di <xref:System.Windows.Interop.D3DImage> che semplificano la creazione per poter interagire con Dx11 e DX10 contenuto. Il codice per questo pacchetto è stato aperto originato ed è disponibile [su GitHub](https://github.com/Microsoft/WPFDXInterop).  
  
<a name="WWF461"></a>   
### <a name="windows-workflow-foundation-transactions"></a>Windows Workflow Foundation: Transazioni  
 Il <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A?displayProperty=fullName> metodo ora possibile utilizzare un gestore delle transazioni distribuite diverso da MSDTC per promuovere la transazione. Eseguire questa operazione specificando identificatore GUID transazione promotore al nuovo <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%28System.Transactions.IPromotableSinglePhaseNotification%2CSystem.Guid%29?displayProperty=fullName> overload. Se l'operazione riesce, le funzionalità della transazione sono soggette a limitazioni. Dopo un promotore di transazione MSDTC non è integrata, i metodi seguenti generano un <xref:System.Transactions.TransactionPromotionException> perché questi metodi devono essere innalzati a MSDTC:  
  
-   <xref:System.Transactions.Transaction.EnlistDurable%2A?displayProperty=fullName>  
  
-   <xref:System.Transactions.TransactionInterop.GetDtcTransaction%2A?displayProperty=fullName>  
  
-   <xref:System.Transactions.TransactionInterop.GetExportCookie%2A?displayProperty=fullName>  
  
-   <xref:System.Transactions.TransactionInterop.GetTransmitterPropagationToken%2A?displayProperty=fullName>  
  
 Quando viene integrato un promotore di transazione non MSDTC, occorre usarlo per le future integrazioni durevoli usando i protocolli che definisce. Il <xref:System.Guid> della transazione promotore può essere ottenuto utilizzando il <xref:System.Transactions.Transaction.PromoterType%2A> proprietà. Quando la transazione Alza di livello, il promotore di transazione fornisce un <xref:System.Byte> matrice che rappresenta il token innalzate di livello. Un'applicazione può ottenere il token innalzate di livello per una transazione non MSDTC alzate di livello con il <xref:System.Transactions.Transaction.GetPromotedToken%2A> metodo.  
  
 Gli utenti del nuovo <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%28System.Transactions.IPromotableSinglePhaseNotification%2CSystem.Guid%29?displayProperty=fullName> overload deve seguire una sequenza di chiamate specifico affinché l'operazione di innalzamento di livello per il completamento. Queste regole sono descritte nella documentazione relativa al metodo.  
  
<a name="Profile461"></a>   
### <a name="profiling"></a>Profilatura  
 L'API di profilatura non gestita è stata migliorata nel modo seguente:  
  
 Supporto migliorato per l'accesso ai file PDB nel [ICorProfilerInfo7](../../../ocs/framework/unmanaged-api/profiling/icorprofilerinfo7-interface.md) interfaccia  
 In ASP.Net 5 è sempre più comune che gli assembly vengano compilati in memoria mediante Roslyn. Per gli sviluppatori che creano strumenti di profilatura, ciò significa che i PDB che in passato erano serializzati sul disco potrebbero non essere più presenti. Gli strumenti profiler spesso usano PDB per rimappare il codice alle righe di origine per attività come il code coverage o l'analisi delle prestazioni riga per riga. Il [ICorProfilerInfo7](../../../ocs/framework/unmanaged-api/profiling/icorprofilerinfo7-interface.md) interfaccia include ora due nuovi metodi, [ICorProfilerInfo7::GetInMemorySymbolsLength](../Topic/ICorProfilerInfo7::GetInMemorySymbolsLength%20Method.md) e [ICorProfilerInfo7::ReadInMemorySymbols](../Topic/ICorProfilerInfo7::ReadInMemorySymbols.md), per fornire accesso ai dati di file PDB in memoria, questi strumenti profiler utilizzando le nuove API, un profiler può ottenere il contenuto di un file PDB in memoria come matrice di byte e quindi elaborarla o eseguirne la serializzazione su disco.  
  
 Strumentazione migliore con l'interfaccia ICorProfiler  
 I profiler che usano la funzionalità ReJit dell'API `ICorProfiler` per la strumentazione dinamica ora possibile modificare alcuni metadati. In precedenza quegli strumenti potevano instrumentare IL in qualsiasi momento, ma i metadati potevano essere modificati solo in fase di caricamento del modulo. Poiché IL fa riferimento ai metadati, questo limitava i tipi di strumentazione possibile. È stato sollevato alcune di tali limiti aggiungendo il [ICorProfilerInfo7::ApplyMetaData](../Topic/ICorProfilerInfo7::ApplyMetaData%20Method.md) metodo supporta un sottoinsieme di modifica dei metadati dopo che il modulo viene caricato, in particolare tramite l'aggiunta di nuovi `AssemblyRef`, `TypeRef`, `TypeSpec`, `MemberRef`, `MemberSpec`, e `UserString` record. Questa modifica rende possibile una gamma più ampia di strumentazioni immediate.  
  
<a name="NGEN461"></a>   
### <a name="native-image-generator-ngen-pdbs"></a>PDB del generatore di immagini native (NGEN)  
 La traccia eventi tra computer consente ai clienti di profilare un programma sul Computer A e osservare i dati di profilatura con mapping della riga di origine sul Computer B. Nelle versioni precedenti di .NET Framework, l'utente copiava tutti i moduli e le immagini native dalla macchina profilata alla macchina di analisi contenente il PDB IL per creare il mapping sorgente-nativo. Anche se questo processo può funzionare bene quando i file sono relativamente piccoli, ad esempio per le applicazioni telefoniche, i file possono avere dimensioni molto grandi sui sistemi desktop e la copia può richiedere molto tempo.  
  
 Con i PDB Ngen, NGen può creare un PDB che contiene il mapping da IL a nativo senza una dipendenza dal PDB IL. In questo scenario di traccia eventi tra più computer, è sufficiente è copiare l'immagine nativa PDB generato dal computer A computer b e usare [Debug interfaccia accesso API](https://msdn.microsoft.com/en-us/library/ee8x173s.aspx) per leggere il mapping di origine a livello di integrità del file PDB IL e i mapping per IL codice nativo del file PDB immagini native. La combinazione di entrambi i mapping fornisce un mapping da codice sorgente a codice nativo. Poiché il PDB di immagine nativa è molto più piccolo rispetto a tutti i moduli e alle immagini native, il processo di copia dal Computer A al Computer B è molto più veloce.  
  
<a name="v46"></a>   
## <a name="whats-new-in-net-2015"></a>Novità di .NET 2015  
 .NET 2015 introduce [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] e .NET Core. Alcune nuove funzionalità sono valide per entrambi, mentre altre sono specifiche di [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] o [!INCLUDE[net_core](../../../includes/net-core-md.md)].  
  
-   **ASP.NET 5**  
  
     .NET 2015 include ASP.NET 5, una piattaforma .NET snella per la compilazione di app moderne basate su cloud. Si tratta di una piattaforma modulare che consente di includere solo le funzionalità necessarie nell'applicazione. Può essere ospitata su IIS o in modo indipendente in un processo personalizzato ed è possibile eseguire app con diverse versioni di .NET Framework nello stesso server. Include un nuovo sistema di configurazione dell'ambiente progettato per la distribuzione cloud.  
  
     MVC, API Web e pagine Web sono riunite in un unico framework denominato MVC 6. Le app ASP.NET 5 vengono compilate mediante i nuovi strumenti in Visual Studio 2015. Le applicazioni esistenti funzioneranno nel nuovo .NET Framework ma per compilare un'app che usa MVC 6 o SignalR 3 è necessario usare il sistema di progetto in Visual Studio 2015.  
  
     Per informazioni, vedere [ASP.NET 5](http://go.microsoft.com/fwlink/?LinkId=518238).  
  
-   **Aggiornamenti di ASP.NET**  
  
    -   **API basata su attività per lo scaricamento di risposta asincrona**  
  
         ASP.NET offre ora una semplice API basata su attività per lo scaricamento di risposta asincrona, <xref:System.Web.HttpResponse.FlushAsync%2A?displayProperty=fullName>, che consente le risposte di essere scaricate in modo asincrono utilizzando il linguaggio `async/await` supportano.  
  
    -   `Model binding supports task-returning methods`  
  
         In [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] ASP.NET ha aggiunto la funzionalità di associazione di modelli che ha reso possibile un approccio estendibile, focalizzato sul codice, per le operazioni di dati basate su CRUD nelle pagine Web Form e nei controlli utente. Il sistema di associazione del modello supporta ora <xref:System.Threading.Tasks.Task>-restituzione metodi del modello di associazione. Questa funzionalità consente agli sviluppatori di Web Form di ottenere i vantaggi di scalabilità di async con la facilità del sistema di associazione dati quando usano versioni più recenti di ORM, tra cui Entity Framework.  
  
         L'associazione di modelli async è controllata dall'impostazione di configurazione `aspnet:EnableAsyncModelBinding`.  
  
        ```  
  
        <appSettings>  
           <add key=" aspnet:EnableAsyncModelBinding" value="true|false" />  
        </appSettings>  
  
        ```  
  
         Per le app destinate a [!INCLUDE[net_v46](../../../includes/net-v46-md.md)], l'impostazione predefinita è `true`. Per le app in esecuzione su [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] e che sono destinate a una versione precedente di .NET Framework, è `false` per impostazione predefinita. Può essere abilitata impostando l'impostazione di configurazione su `true`.  
  
    -   **Supporto HTTP/2 (Windows 10)**  
  
         [HTTP/2](http://www.wikipedia.org/wiki/HTTP/2) è una nuova versione del protocollo HTTP che fornisce molto uso migliore della connessione (meno round trip tra client e server), che per gli utenti di caricamento della pagina web latenza inferiore.  Le pagine Web (a differenza dei servizi) traggono maggiori vantaggi dal protocollo HTTP/2, poiché ottimizza più elementi richiesti come parte di un'esperienza unica. Il supporto HTTP/2 è stato aggiunto ad ASP.NET in .NET Framework 4.6. Poiché la funzionalità di rete esiste a più livelli, si sono rese necessarie nuove funzionalità in Windows, IIS e ASP.NET per abilitare HTTP/2. È necessario eseguire Windows 10 per usare HTTP/2 con ASP.NET.  
  
         HTTP/2 è inoltre supportato e per impostazione predefinita per Windows 10 Universal Windows App piattaforma UWP () che usano il <xref:System.Net.Http.HttpClient?displayProperty=fullName> API.  
  
         Per fornire un modo per utilizzare il [PUSH_PROMISE](http://http2.github.io/http2-spec/#PUSH_PROMISE) funzionalità nelle applicazioni ASP.NET, un nuovo metodo con due overload, <xref:System.Web.HttpResponse.PushPromise%28System.String%29> e <xref:System.Web.HttpResponse.PushPromise%28System.String%2CSystem.String%2CSystem.Collections.Specialized.NameValueCollection%29>, è stato aggiunto il <xref:System.Web.HttpResponse> (classe).  
  
        > [!NOTE]
        >  Mentre ASP.NET 5 supporta HTTP/2, il supporto della funzionalità PUSH PROMISE non è ancora stato aggiunto.  
  
         Il browser e il server Web (IIS su Windows) eseguono tutte le operazioni. Gli utenti non dovranno eseguire alcuna operazione impegnativa.  
  
         La maggior parte del [principali browser supporta HTTP/2](http://www.wikipedia.org/wiki/HTTP/2), dunque è probabile che gli utenti trarranno vantaggio dal supporto HTTP/2, se supportato dal server.  
  
    -   **Supporto per il protocollo di associazione dei Token**  
  
         Microsoft e Google stanno collaborando a un nuovo approccio all'autenticazione, denominato il [Token Binding Protocol](https://github.com/TokenBinding/Internet-Drafts). Il presupposto è che i token di autenticazione (nella cache del browser) possono essere rubati e utilizzati da utenti malintenzionati per accedere alle risorse protette in caso contrario (ad esempio, il conto bancario) senza richiedere la password o altre informazioni riservate. L'obiettivo del nuovo protocollo è attenuare questo problema.  
  
         Il Token Binding Protocol verrà implementato in Windows 10 come funzionalità del browser. Le app ASP.NET parteciperanno al protocollo, in modo che sia convalidata la legittimità dei token di autenticazione. Le implementazioni di client e server stabiliscono la protezione end-to-end specificata dal protocollo.  
  
    -   **Algoritmi di hash stringa casuale**  
  
         .NET Framework 4.5 introdotto un [algoritmo hash stringa casuale](https://msdn.microsoft.com/library/jj152924.aspx). Tuttavia, non era supportato da ASP.NET perché alcune funzionalità ASP.NET dipendevano da un codice hash stabile. In [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] gli algoritmi di hash della stringa casuale sono ora supportati. Per abilitare questa funzionalità, usare l'impostazione di configurazione `aspnet:UseRandomizedStringHashAlgorithm`.  
  
        ```  
  
        <appSettings>  
           <add key="aspnet:UseRandomizedStringHashAlgorithm" value="true|false" />  
        </appSettings>  
  
        ```  
  
-   **ADO.NET**  
  
     ADO .NET supporta ora la funzionalità Crittografia sempre attiva disponibile in SQL Server 2016 Community Technology Preview 2 (CTP2). Con Crittografia sempre attiva, SQL Server può eseguire operazioni su dati crittografati e, soprattutto, la chiave di crittografia risiede con l'applicazione all'interno dell'ambiente attendibile del cliente e non sul server. Crittografia sempre attiva protegge i dati dei clienti in modo che gli amministratori di database non abbiano accesso ai dati di testo normale. La crittografia e la decrittografia dei dati avvengono in modo trasparente a livello di driver, riducendo al minimo le modifiche che è necessario apportare alle applicazioni esistenti. Per informazioni dettagliate, vedere [sempre crittografati (Database Engine)](https://msdn.microsoft.com/library/mt163865\(v=sql.130\).aspx) e [sempre crittografati (sviluppo per client)](https://msdn.microsoft.com/library/mt147923\(v=sql.130\).aspx).  
  
-   **Compilatore JIT a&64; bit per codice gestito**  
  
     .NET Framework 4.6 presenta una nuova versione del compilatore JIT a 64 bit (il cui nome in codice iniziale era RyuJIT). Il nuovo compilatore a 64 bit offre miglioramenti significativi delle prestazioni rispetto al compilatore JIT a 64 bit esistente. Il nuovo compilatore a 64 bit è abilitato per i processi a 64 bit in esecuzione su NET Framework 4.6. L'app verrà eseguita in un processo a 64 bit se è compilata come 64 bit o AnyCPU e se viene eseguita su un sistema operativo a 64 bit. Nonostante si sia cercato di rendere il più possibile trasparente la transizione al nuovo compilatore, potrebbero verificarsi cambiamenti del comportamento. Microsoft è interessata a conoscere i commenti diretti degli utenti sugli eventuali problemi riscontrati durante l'uso del nuovo compilatore JIT. Contattare Microsoft tramite [Microsoft Connect](http://connect.microsoft.com/) se si verifica un problema che può essere correlato per il nuovo compilatore JIT a 64 bit.  
  
     Il nuovo compilatore JIT a 64 bit include inoltre funzionalità di accelerazione SIMD hardware quando è associata a tipi abilitati per SIMD il <xref:System.Numerics> spazio dei nomi, che può produrre i miglioramenti di prestazioni ottimali.  
  
-   **Miglioramenti al caricatore di assembly**  
  
     Il caricatore di assembly usa la memoria in modo più efficiente scaricando gli assembly IL dopo il caricamento di un'immagine NGEN corrispondente. Questa modifica riduce la memoria virtuale, aspetto particolarmente utile per app a 32 bit di grandi dimensioni (ad esempio Visual Studio) e consente anche di risparmiare memoria fisica.  
  
-   **Modifiche apportate alla libreria di classe di base**  
  
     Sono state aggiunte molte nuove API a [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] per abilitare gli scenari principali. Sono incluse le modifiche e le aggiunte seguenti:  
  
    -   **IReadOnlyCollection<> \</> \> implementazioni**  
  
         Altre raccolte implementano <xref:System.Collections.Generic.IReadOnlyCollection%601> , ad esempio <xref:System.Collections.Generic.Queue%601> e <xref:System.Collections.Generic.Stack%601>.  
  
    -   **CultureInfo. CurrentCulture e CultureInfo. CurrentUICulture**  
  
         Il <xref:System.Globalization.CultureInfo.CurrentCulture%2A?displayProperty=fullName> e <xref:System.Globalization.CultureInfo.CurrentUICulture%2A?displayProperty=fullName> proprietà ora sono in lettura / scrittura anziché sola lettura. Se si assegna un nuovo <xref:System.Globalization.CultureInfo> a queste proprietà, le impostazioni cultura correnti di thread definita dall'oggetto di `Thread.CurrentThread.CurrentCulture` proprietà e il thread UI corrente definite dalla `Thread.CurrentThread.CurrentUICulture` inoltre modificare le proprietà.  
  
    -   **Miglioramenti apportati a garbage collection (GC)**  
  
         Il <xref:System.GC> classe include ora <xref:System.GC.TryStartNoGCRegion%2A> e <xref:System.GC.EndNoGCRegion%2A> metodi che consentono di impedire l'operazione di garbage collection durante l'esecuzione di un percorso critico.  
  
         Un nuovo overload di <xref:System.GC.Collect%28System.Int32%2CSystem.GCCollectionMode%2CSystem.Boolean%2CSystem.Boolean%29?displayProperty=fullName> metodo consente di controllare se l'heap oggetti piccoli e heap oggetti grandi sono sweep e compattati o solo sottoposti a sweep.  
  
    -   **Tipi abilitati per SIMD**  
  
         Il <xref:System.Numerics> dello spazio dei nomi include ora un numero di tipi abilitati per SIMD, ad esempio <xref:System.Numerics.Matrix3x2>, <xref:System.Numerics.Matrix4x4>, <xref:System.Numerics.Plane>, <xref:System.Numerics.Quaternion>, <xref:System.Numerics.Vector2>, <xref:System.Numerics.Vector3>, e <xref:System.Numerics.Vector4>.  
  
         Il nuovo compilatore JIT a 64 bit include anche funzionalità di accelerazione SIMD hardware, quindi le prestazioni migliorano notevolmente quando si usano i tipi abilitati per SIMD con il nuovo compilatore JIT a 64 bit.  
  
    -   **Aggiornamenti di crittografia**  
  
         Il <xref:System.Security.Cryptography?displayProperty=fullName> API viene aggiornata per supportare il [API di crittografia CNG di Windows](https://msdn.microsoft.com/library/windows/desktop/aa376214.aspx). Le versioni precedenti di .NET Framework si sono affidati interamente in un [versione precedente delle API di crittografia Windows](https://msdn.microsoft.com/library/windows/desktop/aa380255.aspx) come base per il <xref:System.Security.Cryptography?displayProperty=fullName> implementazione. Abbiamo avuto richieste per supportare l'API CNG, poiché supporta [algoritmi di crittografia moderna](https://msdn.microsoft.com/library/windows/desktop/bb204775.aspx#suite_b_support), che sono importanti per determinate categorie di applicazioni.  
  
         .NET Framework 4.6 include i nuovi miglioramenti seguenti per supportare le API di crittografia di CNG di Windows:  
  
        -   Un set di metodi di estensione per certificati X509, `System.Security.Cryptography.X509Certificates.RSACertificateExtensions.GetRSAPublicKey(System.Security.Cryptography.X509Certificates.X509Certificate2)` e `System.Security.Cryptography.X509Certificates.RSACertificateExtensions.GetRSAPrivateKey(System.Security.Cryptography.X509Certificates.X509Certificate2)`, che restituiscono, quando possibile, un'implementazione basata su CNG invece di un'implementazione basata su CAPI. Ad esempio, alcune smart card richiedono comunque CAPI e le API gestiscono il fallback.  
  
        -   Il <xref:System.Security.Cryptography.RSACng?displayProperty=fullName> classe, che fornisce un'implementazione CNG dell'algoritmo RSA.  
  
        -   Miglioramenti all'API RSA in modo che le azioni comuni non richiedano più il cast. Ad esempio, la crittografia dei dati mediante un <xref:System.Security.Cryptography.X509Certificates.X509Certificate2> oggetto richiede codice simile al seguente nelle versioni precedenti di .NET Framework.  
  
             [!code-csharp[WhatsNew.Casting#1](../../../samples/snippets/csharp/VS_Snippets_CLR/whatsnew.casting/cs/program.cs#1)]
             [!code-vb[WhatsNew.Casting#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/whatsnew.casting/vb/module1.vb#1)]  
  
             Il codice che usa le nuove API di crittografia in Framework .NET 4.6 può essere riscritto nel modo seguente per evitare il cast.  
  
             [!code-csharp[WhatsNew.Casting#2](../../../samples/snippets/csharp/VS_Snippets_CLR/whatsnew.casting/cs/program.cs#2)]
             [!code-vb[WhatsNew.Casting#2](../../../samples/snippets/visualbasic/VS_Snippets_CLR/whatsnew.casting/vb/module1.vb#2)]  
  
    -   **Supporto per la conversione di date e ore a o da Unix time**  
  
         Sono stati aggiunti i seguenti nuovi metodi di <xref:System.DateTimeOffset> struttura per supportare la conversione di valori di data e ora in o da Unix time:  
  
        -   <xref:System.DateTimeOffset.FromUnixTimeSeconds%2A?displayProperty=fullName>  
  
        -   <xref:System.DateTimeOffset.FromUnixTimeMilliseconds%2A?displayProperty=fullName>  
  
        -   <xref:System.DateTimeOffset.ToUnixTimeSeconds%2A?displayProperty=fullName>  
  
        -   <xref:System.DateTimeOffset.ToUnixTimeMilliseconds%2A?displayProperty=fullName>  
  
    -   **Opzioni di compatibilità**  
  
         Il nuovo <xref:System.AppContext> classe aggiunge una nuova funzionalità di compatibilità che consente agli autori di libreria di fornire un meccanismo di rifiuto uniforme per la nuova funzionalità per gli utenti. che stabilisce un contratto a regime di controllo libero ("loosely-coupled") tra componenti per poter comunicare una richiesta di rinuncia esplicita. Questa funzionalità è importante in genere quando viene apportata una modifica alle funzionalità esistenti. Al contrario, esiste già un consenso esplicito per la nuova funzionalità.  
  
         Con <xref:System.AppContext>, le librerie definiscono ed espongono le opzioni di compatibilità, mentre il codice che dipende da tali possono impostare tali opzioni influenzano il comportamento della libreria. Per impostazione predefinita, le librerie forniscono la nuova funzionalità e la modificano (cioè offrono la funzionalità precedente) solo se l'opzione è impostata.  
  
         Un'applicazione (o una libreria) può dichiarare il valore di un'opzione (che è sempre un <xref:System.Boolean> valore) che definisce una libreria dipendente. L'opzione è sempre implicitamente `false`. Impostare l'opzione su `true` la abilita. Impostare in modo esplicito l'opzione su `false` fornisce il nuovo comportamento.  
  
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
  
        -   *Switch*.* spazio dei nomi*.* SwitchName*  
  
        -   *Switch*.* library*.* SwitchName*  
  
    -   **Modifiche per il modello asincrono basato su attività (TAP)**  
  
         Per le applicazioni che usano il [!INCLUDE[net_v46](../../../includes/net-v46-md.md)], <xref:System.Threading.Tasks.Task> e <xref:System.Threading.Tasks.Task%601> gli oggetti ereditano le impostazioni cultura e le impostazioni cultura dell'interfaccia utente del thread chiamante. Questo non incide sul comportamento delle app per versioni precedenti di .NET Framework o non destinate a una versione specifica di .NET Framework. Per ulteriori informazioni, vedere la sezione "Impostazioni cultura e le operazioni asincrone basate sulle attività" di <xref:System.Globalization.CultureInfo> argomento relativo alla classe.  
  
         Il <xref:System.Threading.AsyncLocal%601?displayProperty=fullName> classe consente di rappresentare i dati di ambiente sono locali a un flusso di controllo asincrono specificato, ad esempio un `async` metodo. Può essere usato per rendere persistenti i dati tra thread. È inoltre possibile definire un metodo di callback che riceve una notifica ogni volta che i dati di ambiente viene modificato uno di <xref:System.Threading.AsyncLocal%601.Value%2A?displayProperty=fullName> proprietà è stata modificata in modo esplicito, o perché il thread ha rilevato una transizione di contesto.  
  
         Tre metodi pratici, <xref:System.Threading.Tasks.Task.CompletedTask%2A?displayProperty=fullName>, <xref:System.Threading.Tasks.Task.FromCanceled%2A?displayProperty=fullName>, e <xref:System.Threading.Tasks.Task.FromException%2A?displayProperty=fullName>, sono state aggiunte le attività-modello asincrono basato su (TAP) per restituire le attività completate in un determinato stato.  
  
         Il <xref:System.IO.Pipes.NamedPipeClientStream> classe ora supporta la comunicazione asincrona con il nuovo <xref:System.IO.Pipes.NamedPipeClientStream.ConnectAsync%2A>. ProcessOnStatus.  
  
    -   **EventSource ora supporta la scrittura nel registro eventi**  
  
         È ora possibile utilizzare il <xref:System.Diagnostics.Tracing.EventSource> classe registro amministrativo o operativo messaggi nel registro eventi, inoltre eventuali sessioni ETW esistenti create nel computer. In passato era necessario usare il pacchetto Microsoft.Diagnostics.Tracing.EventSource NuGet per questa funzionalità. Questa funzionalità è ora integrata in .NET Framework 4.6.  
  
         Sia il pacchetto NuGet sia .NET Framework 4.6 sono stati aggiornati con le funzionalità seguenti:  
  
        -   **Eventi dinamici**  
  
             Consente eventi definiti al momento senza creare metodi di eventi.  
  
        -   **Payload RTF**  
  
             Consente di passare classi e matrici attribuite in modo specifico nonché tipi primitivi come un payload  
  
        -   **Rilevamento delle attività**  
  
             Comporta l'applicazione di tag di eventi tra gli eventi Start e Stop con un ID che rappresenta tutte le attività attualmente attive.  
  
         Per supportare queste funzionalità, il metodo di overload <xref:System.Diagnostics.Tracing.EventSource.Write%2A> metodo è stato aggiunto il <xref:System.Diagnostics.Tracing.EventSource> (classe).  
  
-   **Windows Presentation Foundation (WPF)**  
  
    -   **Miglioramenti di HDPI**  
  
         Il supporto di HDPI in WPF è stato migliorato in [!INCLUDE[net_v46](../../../includes/net-v46-md.md)]. Sono state apportate modifiche all'arrotondamento del layout per ridurre le istanze di ritaglio nei controlli con bordi. Per impostazione predefinita, questa funzionalità è abilitata solo se il <xref:System.Runtime.Versioning.TargetFrameworkAttribute> è impostato su .NET 4.6.  Applicazioni che le versioni precedenti di framework, ma eseguono il [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] possono optare per il nuovo comportamento aggiungendo la riga seguente al [ <> \> ](../../../docs/framework/configure-apps/file-schema/runtime/runtime-element.md) sezione del file app. config:  
  
        ```  
  
        <AppContextSwitchOverrides  
        value="Switch.MS.Internal.DoNotApplyLayoutRoundingToMarginsAndBorderThickness=false"  
        />  
  
        ```  
  
         Le finestre WPF che si estendono su più monitor con impostazioni DPI diverse (configurazione di più DPI) sono ora visualizzate completamente senza aree nere. È possibile rifiutare esplicitamente questo comportamento disabilitandolo con l'aggiunta della riga seguente alla sezione `<appSettings>` del file di configurazione dell'app:  
  
        ```  
  
        <add key="EnableMultiMonitorDisplayClipping" value="true"/>  
  
        ```  
  
         Il supporto per caricare automaticamente il cursore destra in base all'impostazione DPI è stato aggiunto a <xref:System.Windows.Input.Cursor?displayProperty=fullName>.  
  
    -   **È consigliabile touch**  
  
         Fornisce un report sui clienti [Connect](https://connect.microsoft.com/VisualStudio/feedback/details/903760/) che toccano produce un comportamento imprevedibile sono stati risolti nel [!INCLUDE[net_v46](../../../includes/net-v46-md.md)]. La soglia relativa al doppio tocco per le app di Windows Store e le applicazioni WPF ora è lo stesso in Windows 8.1 e versioni successive.  
  
    -   **Supporto di finestre figlio trasparenti**  
  
         WPF in [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] supporta le finestre figlio trasparenti in Windows 8.1 e versioni successive. Ciò consente di creare finestre figlio non rettangolari e trasparenti nelle finestre di primo livello. È possibile abilitare questa funzionalità impostando il <xref:System.Windows.Interop.HwndSourceParameters.UsesPerPixelTransparency%2A?displayProperty=fullName> proprietà `true`.  
  
-   **Windows Communication Foundation (WCF)**  
  
    -   **Supporto SSL**  
  
         WCF ora supporta la versione SSL TLS 1.1 e TLS 1.2, oltre a SSL 3.0 e TLS 1.0, quando si usa NetTcp con la sicurezza del trasporto e l'autenticazione client. Ora è possibile selezionare il protocollo da usare o disabilitare i protocolli precedenti, che sono meno sicuri. Questa operazione può essere eseguita impostando la <xref:System.ServiceModel.TcpTransportSecurity.SslProtocols%2A> proprietà o aggiungendo il codice seguente in un file di configurazione.  
  
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
  
    -   **L'invio di messaggi utilizzando diverse connessioni HTTP**  
  
         WCF ora consente agli utenti di garantire l'invio di determinati messaggi usando diverse connessioni HTTP sottostanti. Questo risultato può essere raggiunto in due modi:  
  
        -   **Utilizza un prefisso di nome gruppo di connessione**  
  
             Gli utenti possono specificare una stringa che WCF userà per ottenere un prefisso per il nome del gruppo di connessione. Due messaggi con prefissi diversi vengono inviati usando diverse connessioni HTTP sottostanti. Il prefisso è impostato tramite l'aggiunta di una coppia chiave/valore per il messaggio <xref:System.ServiceModel.Channels.Message.Properties%2A?displayProperty=fullName> proprietà. La chiave è "HttpTransportConnectionGroupNamePrefix"; il valore è il prefisso desiderato.  
  
        -   **Utilizzo di channel factory diverse**  
  
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
  
     È ora possibile includere l'identificatore di transazione distribuita per la transazione che ha causato un'eccezione derivata da <xref:System.Transactions.TransactionException> possono essere generate. A questo scopo, aggiungere la chiave seguente alla sezione `appSettings` del file di configurazione dell'app:  
  
    ```  
    <add key="Transactions:IncludeDistributedTransactionIdInExceptionMessage" value="true"/>   
    ```  
  
     Il valore predefinito è `false`.  
  
-   **Funzionalità di rete**  
  
    -   **Riutilizzo di socket**  
  
         Windows 10 include un nuovo algoritmo di rete ad alta scalabilità che consente di migliorare l'uso delle risorse del computer riutilizzando porte locali per le connessioni TCP in uscita. .NET Framework 4.6 supporta il nuovo algoritmo, consentendo alle app .NET di sfruttare il nuovo comportamento. Nelle versioni precedenti di Windows era presente un limite di connessioni simultanee artificiali (in genere 16.384, la dimensione predefinita dell'intervallo di porte dinamiche), che poteva limitare la scalabilità di un servizio causando l'esaurimento delle porte quando sono sotto carico.  
  
         In [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] sono state aggiunte due nuove API per consentire il riutilizzo delle porte, che rimuove in modo efficace il limite di 64.000 sulle connessioni simultanee:  
  
        -   Il <xref:System.Net.Sockets.SocketOptionName?displayProperty=fullName> valore di enumerazione.  
  
        -   Il <xref:System.Net.ServicePointManager.ReusePort%2A?displayProperty=fullName> proprietà.  
  
         Per impostazione predefinita, il <xref:System.Net.ServicePointManager.ReusePort%2A?displayProperty=fullName> è `false` a meno che non la `HWRPortReuseOnSocketBind` valore il `HKLM\SOFTWARE\Microsoft\.NETFramework\v4.0.30319` chiave del Registro di sistema è impostata su 0x1. Per abilitare il riutilizzo di porta locale per le connessioni HTTP, impostare il <xref:System.Net.ServicePointManager.ReusePort%2A?displayProperty=fullName> proprietà `true`. In questo modo tutte le connessioni socket TCP in uscita dal <xref:System.Net.Http.HttpClient> e <xref:System.Net.HttpWebRequest> per utilizzare la nuova opzione di socket Windows 10, [SO_REUSE_UNICASTPORT](https://msdn.microsoft.com/library/windows/desktop/ms740532.aspx), che consente il riutilizzo di porta locale.  
  
         Scrittura di un'applicazione solo sockets gli sviluppatori possono specificare il <xref:System.Net.Sockets.SocketOptionName?displayProperty=fullName> opzione quando si chiama un metodo, ad esempio <xref:System.Net.Sockets.Socket.SetSocketOption%2A?displayProperty=fullName> in modo che in uscita sockets riutilizzare porte locali durante l'associazione.  
  
    -   **Supporto per nomi di dominio internazionali e PunyCode**  
  
         Una nuova proprietà <xref:System.Uri.IdnHost%2A>, è stato aggiunto il <xref:System.Uri> classe per un supporto migliore PunyCode e nomi di dominio internazionali.  
  
-   **Ridimensionamento nei controlli Windows Form.**  
  
     Questa funzionalità è stata espansa [!INCLUDE[net_v46](../../../includes/net-v46-md.md)] per includere il <xref:System.Windows.Forms.DomainUpDown>, <xref:System.Windows.Forms.NumericUpDown>, <xref:System.Windows.Forms.DataGridViewComboBoxColumn>, <xref:System.Windows.Forms.DataGridViewColumn> e <xref:System.Windows.Forms.ToolStripSplitButton> tipi e il rettangolo specificato dal <xref:System.Drawing.Design.PaintValueEventArgs.Bounds%2A> proprietà usato per disegnare un <xref:System.Drawing.Design.UITypeEditor>.  
  
     È una funzionalità che prevede il consenso esplicito. Per attivarla, impostare l'elemento `EnableWindowsFormsHighDpiAutoResizing` su `true` nel file di configurazione dell'applicazione (app.config):  
  
    ```  
  
    <appSettings>  
       <add key="EnableWindowsFormsHighDpiAutoResizing" value="true" />  
    </appSettings>  
  
    ```  
  
-   **Supporto per codifiche della tabella codici**  
  
     [!INCLUDE[net_core](../../../includes/net-core-md.md)] supporta principalmente le codifiche Unicode e per impostazione predefinita offre un supporto limitato per le codifiche della tabella codici. È possibile aggiungere il supporto per codifiche della tabella codici disponibili in .NET Framework ma non supportate in [!INCLUDE[net_core](../../../includes/net-core-md.md)] registrando codifiche della tabella codici con il <xref:System.Text.Encoding.RegisterProvider%2A?displayProperty=fullName> metodo. Per ulteriori informazioni, vedere [System.Text.CodePagesEncodingProvider](https://msdn.microsoft.com/en-us/library/system.text.codepagesencodingprovider.aspx).  
  
-   **.NET native**  
  
     Le app di Windows per Windows 10 destinate a [!INCLUDE[net_core](../../../includes/net-core-md.md)] e scritte in C# o Visual Basic ora possono avvalersi di una nuova tecnologia che compila le app in codice nativo anziché IL. Producono app caratterizzate da maggiore rapidità di avvio ed esecuzione. Per ulteriori informazioni, vedere [la compilazione di applicazioni con .NET Native](../../../docs/framework/net-native/index.md). Per una panoramica di .NET Native che esamina le differenze rispetto alla compilazione JIT e NGEN e il che significa per il codice, vedere [.NET Native e compilazione](../../../docs/framework/net-native/net-native-and-compilation.md).  
  
     Le app vengono compilate in codice nativo per impostazione predefinita quando si compilano con Visual Studio 2015. Per ulteriori informazioni, vedere [Introduzione a .NET Native](../../../docs/framework/net-native/getting-started-with-net-native.md).  
  
     Per supportare il debug di app .NET Native, è stata aggiunta una serie di nuove interfacce ed enumerazioni all'API di debug non gestito. Per ulteriori informazioni, vedere il [debug (riferimenti alle API non gestite)](../../../ml/index.xml) argomento.  
  
-   **Pacchetti di .NET Framework open source**  
  
     [!INCLUDE[net_core](../../../includes/net-core-md.md)]pacchetti, ad esempio le raccolte non modificabili, [API SIMD](http://go.microsoft.com/fwlink/?LinkID=518639), e le API di rete, ad esempio quelle disponibili nel <xref:System.Net.Http> dello spazio dei nomi sono ora disponibili come pacchetti open source in [GitHub](https://github.com/). Per accedere al codice, vedere [NetFx su GitHub](http://go.microsoft.com/fwlink/?LinkID=518634). Per ulteriori informazioni e come contribuire a questi pacchetti, vedere [.NET Core e Open Source](../../../docs/framework/get-started/net-core-and-open-source.md), [Home Page di .NET su GitHub](http://go.microsoft.com/fwlink/?LinkID=518635).  
  
 [Torna all'inizio](#introduction)  
  
<a name="v452"></a>   
## <a name="whats-new-in-the-net-framework-452"></a>Novità di .NET Framework 4.5.2  
  
-   **Nuove API per le applicazioni ASP.NET.** Il nuovo <xref:System.Web.HttpResponse.AddOnSendingHeaders%2A?displayProperty=fullName> e <xref:System.Web.HttpResponseBase.AddOnSendingHeaders%2A?displayProperty=fullName> metodi consentono di esaminare e modificare le intestazioni di risposta e codice di stato mentre la risposta viene scaricata l'applicazione client. Si consiglia di utilizzare questi metodi anziché i <xref:System.Web.HttpApplication.PreSendRequestHeaders> e <xref:System.Web.HttpApplication.PreSendRequestContent> degli eventi, sono più efficienti e affidabili.  
  
     Il <xref:System.Web.Hosting.HostingEnvironment.QueueBackgroundWorkItem%2A?displayProperty=fullName> metodo consente di pianificare gli elementi di lavoro di piccole dimensioni in background. ASP.NET tiene traccia di questi elementi e impedisce a IIS di chiudere improvvisamente il processo di lavoro finché non saranno stati completati tutti gli elementi di lavoro in background. Non è possibile chiamare questo metodo all'esterno del dominio dell'app gestita di ASP.NET.  
  
     Il nuovo <xref:System.Web.HttpResponse.HeadersWritten?displayProperty=fullName> e <xref:System.Web.HttpResponseBase.HeadersWritten?displayProperty=fullName> restituiscono valori booleani che indicano se le intestazioni di risposta sono state scritte. È possibile utilizzare queste proprietà per assicurarsi che le chiamate alle API come <xref:System.Web.HttpResponse.StatusCode%2A?displayProperty=fullName> (che genera eccezioni se le intestazioni sono state scritte) abbiano esito positivo.  
  
-   **Ridimensionamento nei controlli Windows Form.** Questa funzionalità è stata ampliata. È ora possibile usare l'impostazione DPI di sistema per ridimensionare i componenti dei seguenti controlli aggiuntivi (ad esempio, la freccia a discesa nelle caselle combinate):  
  
     <xref:System.Windows.Forms.ComboBox>   
     <xref:System.Windows.Forms.ToolStripComboBox>   
     <xref:System.Windows.Forms.ToolStripMenuItem>   
     <xref:System.Windows.Forms.Cursor>   
     <xref:System.Windows.Forms.DataGridView>   
     <xref:System.Windows.Forms.DataGridViewComboBoxColumn>  
  
     È una funzionalità che prevede il consenso esplicito. Per attivarla, impostare l'elemento `EnableWindowsFormsHighDpiAutoResizing` su `true` nel file di configurazione dell'applicazione (app.config):  
  
    ```  
    <appSettings>  
       <add key="EnableWindowsFormsHighDpiAutoResizing" value="true" />  
    </appSettings>  
    ```  
  
-   **Nuova funzionalità di flusso di lavoro.** Un gestore di risorse che utilizza il <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A> (metodo) (e che quindi implementa il <xref:System.Transactions.IPromotableSinglePhaseNotification> interface) può usare il nuovo <xref:System.Transactions.Transaction.PromoteAndEnlistDurable%2A?displayProperty=fullName> metodo per richiedere quanto segue:  
  
    -   Promuova la transazione in transazione MSDTC (Microsoft Distributed Transaction Coordinator).  
  
    -   Sostituire <xref:System.Transactions.IPromotableSinglePhaseNotification> con un <xref:System.Transactions.ISinglePhaseNotification>, cioè un'integrazione durevole che supporta i commit monofase.  
  
     È possibile eseguire questa operazione nello stesso dominio dell'app; inoltre, non è necessario altro codice non gestito che interagisca con MSDTC per eseguire la promozione. Il nuovo metodo può essere chiamato solo quando esiste una chiamata inevasa da <xref:System.Transactions?displayProperty=fullName> per il <xref:System.Transactions.IPromotableSinglePhaseNotification> `Promote` metodo implementato dall'integrazione promuovibile.  
  
-   **Miglioramenti della profilatura.** Le seguenti nuove API di profilatura non gestite offrono funzioni di profilatura più solide:  
  
     [Struttura COR_PRF_ASSEMBLY_REFERENCE_INFO](../../../ocs/framework/unmanaged-api/profiling/cor-prf-assembly-reference-info-structure.md)   
     [Enumerazione COR_PRF_HIGH_MONITOR](../../../ocs/framework/unmanaged-api/profiling/cor-prf-high-monitor-enumeration.md)   
     [Metodo GetAssemblyReferences](../Topic/ICorProfilerCallback6::GetAssemblyReferences%20Method.md)   
     [Metodo GetEventMask2](../Topic/ICorProfilerInfo5::GetEventMask2%20Method.md)   
     [Metodo SetEventMask2](../Topic/ICorProfilerInfo5::SetEventMask2%20Method.md)   
     [Metodo AddAssemblyReference](../Topic/ICorProfilerAssemblyReferenceProvider::AddAssemblyReference%20Method.md)  
  
     Le precedenti implementazioni di `ICorProfiler` supportavano il caricamento differito degli assembly dipendenti. Le nuove API di profilatura richiedono assembly dipendenti inseriti dal profiler per il caricamento immediato, invece di essere caricato dopo la completa inizializzazione dell'app. Questa modifica non incide sugli utenti delle API `ICorProfiler` esistenti.  
  
-   **Miglioramenti apportati al debug.** Le seguenti nuove API di debug non gestite offrono una migliore integrazione con un profiler. È ora possibile accedere ai metadati inseriti dal profiler oltre alle variabili e al codice locali prodotti dalle richieste ReJIT del compilatore durante il debug di dump.  
  
     [Metodo SetWriteableMetadataUpdateMode](../Topic/ICorDebugProcess7::SetWriteableMetadataUpdateMode%20Method.md)   
     [Metodo EnumerateLocalVariablesEx](../Topic/ICorDebugILFrame4::EnumerateLocalVariablesEx%20Method.md)   
     [Metodo GetLocalVariableEx](../Topic/ICorDebugILFrame4::GetLocalVariableEx%20Method.md)   
     [Metodo GetCodeEx](../Topic/ICorDebugILFrame4::GetCodeEx%20Method.md)   
     [Metodo GetActiveReJitRequestILCode](../Topic/ICorDebugFunction3::GetActiveReJitRequestILCode%20Method.md)   
     [Metodo GetInstrumentedILMap](../Topic/ICorDebugILCode2::GetInstrumentedILMap%20Method.md)  
  
-   **Modifiche della traccia eventi.** .NET Framework 4.5.2 consente di eseguire attività out-of-process basate su Event Tracing for Windows (ETW) per una superficie maggiore. Ciò consente ai fornitori di Advanced Power Management (APM) di offrire strumenti semplici che tengono accuratamente traccia dei costi delle singole richieste e attività cross-thread.  Questi eventi vengono generati solo quando sono abilitati dai controller ETW; di conseguenza, le modifiche non influiscono sul codice ETW scritto in precedenza oppure sul codice eseguito con ETW disattivato.  
  
-   **Promozione di una transazione e convertirla in un elenco durevole**  
  
     <xref:System.Transactions.Transaction.PromoteAndEnlistDurable%2A?displayProperty=fullName> è una nuova API aggiunte a .NET Framework 4.5.2 e 4.6:  
  
    ```  
  
    [System.Security.Permissions.PermissionSetAttribute(System.Security.Permissions.SecurityAction.LinkDemand, Name = "FullTrust")]  
    public Enlistment PromoteAndEnlistDurable(Guid resourceManagerIdentifier,  
                                              IPromotableSinglePhaseNotification promotableNotification,  
                                              ISinglePhaseNotification enlistmentNotification,  
                                              EnlistmentOptions enlistmentOptions)  
  
    ```  
  
     Il metodo può essere utilizzato da un elenco che è stato creato in precedenza da <xref:System.Transactions.Transaction.EnlistPromotableSinglePhase%2A?displayProperty=fullName> in risposta al <xref:System.Transactions.ITransactionPromoter.Promote%2A?displayProperty=fullName> metodo. Chiede a `System.Transactions` di alzare la transazione al livello di transazione MSDTC e di "convertire" l'elenco promuovibile in un elenco durevole. Dopo che questo metodo viene completato correttamente, il <xref:System.Transactions.IPromotableSinglePhaseNotification> interfaccia non faranno riferimento non è più `System.Transactions`, e le notifiche future arrivano in forniti <xref:System.Transactions.ISinglePhaseNotification> interfaccia. L'elenco in questione deve agire come un elenco durevole, supportando la registrazione e il ripristino delle transazioni. Fare riferimento a <xref:System.Transactions.Transaction.EnlistDurable%2A?displayProperty=fullName> per informazioni dettagliate. Inoltre, deve supportare l'integrazione <xref:System.Transactions.ISinglePhaseNotification>.  Questo metodo può *solo* essere chiamato durante l'elaborazione di un <xref:System.Transactions.ITransactionPromoter.Promote%2A?displayProperty=fullName> chiamare. Se non è il caso, un <xref:System.Transactions.TransactionException> viene generata un'eccezione.  
  
 [Torna all'inizio](#introduction)  
  
<a name="v451"></a>   
## <a name="whats-new-in-the-net-framework-451"></a>Novità di .NET Framework 4.5.1  
 **Aggiornamenti di aprile 2014**:  
  
-   [Visual Studio 2013 Update 2](http://go.microsoft.com/fwlink/p/?LinkId=393658) include aggiornamenti ai modelli di libreria di classi portabile per supportare i seguenti scenari:  
  
    -   È possibile usare le API di Windows Runtime in librerie portabili destinate a Windows 8.1, Windows Phone 8.1 e Windows Phone Silverlight 8.1.  
  
    -   È possibile includere XAML (tipi Windows.UI.XAML) nelle librerie portabili quando la destinazione è Windows 8.1 o Windows Phone 8.1. Sono supportati i modelli XAML seguenti: Pagina vuota, Dizionario risorse, Controllo basato su modelli e Controllo utente.  
  
    -   È possibile creare una componente Windows Runtime portabile (.winmd file) da usare in app di Windows Store destinate a Windows 8.1 e Windows Phone 8.1.  
  
    -   È possibile cambiare associazione a una libreria di classi Windows Store o Windows Phone Store come una Libreria di classi portabile.  
  
     Per ulteriori informazioni su queste modifiche, vedere [libreria di classi portabile](../../../docs/standard/cross-platform/cross-platform-development-with-the-portable-class-library.md).  
  
-   Il set di contenuti di .NET Framework ora include la documentazione relativa a [!INCLUDE[net_native](../../../includes/net-native-md.md)], una tecnologia di precompilazione per la creazione e la distribuzione di app di Windows. [!INCLUDE[net_native](../../../includes/net-native-md.md)] compila le app direttamente in codice nativo piuttosto che in linguaggio intermedio (IL), per ottenere migliori prestazioni. Per informazioni dettagliate, vedere [la compilazione di applicazioni con .NET Native](../../../docs/framework/net-native/index.md).  
  
-   Il [origine riferimento di .NET Framework](http://referencesource.microsoft.com/) offre una nuova esperienza di navigazione e funzionalità migliorate. È possibile esplorare il codice sorgente di .NET Framework online, [scaricare i riferimenti](http://referencesource.microsoft.com/download.html) per la visualizzazione non in linea e origini (inclusi aggiornamenti e patch) durante il debug. Per ulteriori informazioni, vedere il post di blog [nuovo aspetto dell'origine riferimento di .NET](http://blogs.msdn.com/b/dotnet/archive/2014/02/24/a-new-look-for-net-reference-source.aspx).  
  
 Le nuove funzionalità e i miglioramenti principali in .NET Framework 4.5.1 includono:  
  
-   Reindirizzamento di associazione automatico per assembly. A partire da [!INCLUDE[vs_dev12](../../../includes/vs-dev12-md.md)], quando si compila un'app destinata a [!INCLUDE[net_v451](../../../includes/net-v451-md.md)], è possibile aggiungere reindirizzamenti di associazione al file di configurazione dell'app se quest'ultima o i relativi componenti fanno riferimento a più versioni dello stesso assembly. È inoltre possibile abilitare questa funzionalità per i progetti destinati a versioni precedenti di .NET Framework. Per ulteriori informazioni, vedere [procedura: abilitare e disabilitare il reindirizzamento di associazione automatico](../../../docs/framework/configure-apps/how-to-enable-and-disable-automatic-binding-redirection.md).  
  
-   Possibilità di raccogliere informazioni di diagnostica che consentono agli sviluppatori di migliorare le prestazioni delle applicazioni server e cloud. Per ulteriori informazioni, vedere il <xref:System.Diagnostics.Tracing.EventSource.WriteEventWithRelatedActivityId%2A> e <xref:System.Diagnostics.Tracing.EventSource.WriteEventWithRelatedActivityIdCore%2A> metodi di <xref:System.Diagnostics.Tracing.EventSource> (classe).  
  
-   Capacità di compattare in modo esplicito gli heap di oggetti grandi durante la Garbage Collection. Per ulteriori informazioni, vedere il <xref:System.Runtime.GCSettings.LargeObjectHeapCompactionMode%2A?displayProperty=fullName> proprietà.  
  
-   Altri miglioramenti alle prestazioni, quali la sospensione di app ASP.NET, i miglioramenti JIT multicore e un avvio più rapido delle app in seguito a un aggiornamento di .NET Framework. Per informazioni dettagliate, vedere il [annuncio di .NET Framework 4.5.1](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx) e [sospensione dell'applicazione ASP.NET](http://blogs.msdn.com/b/dotnet/archive/2013/10/09/asp-net-app-suspend-responsive-shared-net-web-hosting.aspx) post di blog.  
  
 I miglioramenti di Windows Form includono:  
  
-   Ridimensionamento nei controlli Windows Form. È possibile usare l'impostazione DPI per ridimensionare i componenti dei controlli (ad esempio, le icone visualizzate in una griglia delle proprietà) scegliendo una voce nel file di configurazione dell'applicazione (app.config) relativo alla propria app. Questa funzionalità è attualmente supportata nei seguenti controlli Windows Form:  
  
     <xref:System.Windows.Forms.PropertyGrid>   
     <xref:System.Windows.Forms.TreeView>   
     Alcuni aspetti di <xref:System.Windows.Forms.DataGridView> (vedere [nuove funzionalità nella versione 4.5.2](#v452) per altri controlli supportati)  
  
     Per abilitare questa funzionalità, aggiungere un nuovo <> \> elemento al file di configurazione (app. config) e impostare il `EnableWindowsFormsHighDpiAutoResizing` elemento `true`:  
  
    ```  
    <appSettings>  
       <add key="EnableWindowsFormsHighDpiAutoResizing" value="true" />  
    </appSettings>  
    ```  
  
 I miglioramenti durante il debug delle app .NET Framework in [!INCLUDE[vs_dev12](../../../includes/vs-dev12-md.md)] includono:  
  
-   Valori restituiti nel debugger di Visual Studio. Quando si esegue il debug di un'app gestita in [!INCLUDE[vs_dev12](../../../includes/vs-dev12-md.md)], nella finestra Auto vengono restituiti tipi e valori per i metodi. Queste informazioni sono disponibili per applicazioni desktop, Windows Store e Windows Phone. Per ulteriori informazioni, vedere [esaminare valori restituiti delle chiamate al metodo](http://msdn.microsoft.com/library/e3245b37-8e2e-4200-ba84-133726e95f1f\(v=vs.120\).aspx) in MSDN Library.  
  
-   Modifica e continua per app a 64 bit. In [!INCLUDE[vs_dev12](../../../includes/vs-dev12-md.md)] è supportata la funzionalità Modifica e continuazione per le applicazioni gestite a 64 bit per desktop, Windows Store e Windows Phone. Le limitazioni esistenti rimangono attive per App a 32 bit e 64 bit (vedere l'ultima sezione di [modifiche al codice supportate (c#)](http://msdn.microsoft.com/library/ms164927\(v=vs.120\).aspx) articolo).  
  
-   Debug asincrono. Per semplificare il debug delle app asincrone in [!INCLUDE[vs_dev12](../../../includes/vs-dev12-md.md)], lo stack di chiamate nasconde il codice dell'infrastruttura fornito dai compilatori per supportare la programmazione asincrona e inoltre si concatena nei frame padre logici, in modo da poter seguire più chiaramente l'esecuzione logica del programma. La finestra Attività in parallelo è stata sostituita da una finestra Attività, contenente le attività correlate a uno specifico punto di interruzione e qualsiasi altra attività attualmente attiva o pianificata nell'app. Per ulteriori informazioni nella sezione "debug asincrono" di questa funzionalità di [annuncio di .NET Framework 4.5.1](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).  
  
-   Supporto avanzato delle eccezioni per i componenti Windows Runtime. In [!INCLUDE[win81](../../../includes/win81-md.md)] le eccezioni generate dalle app di Windows Store conservano le informazioni sull'errore che ha generato l'eccezione, anche oltre i limiti di linguaggio. Per ulteriori informazioni nella sezione "Sviluppo di applicazioni Windows Store" di questa funzionalità di [annuncio di .NET Framework 4.5.1](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).  
  
 A partire da [!INCLUDE[vs_dev12](../../../includes/vs-dev12-md.md)], è possibile utilizzare il [gestito strumento di ottimizzazione PGO (Mpgo.exe)](../../../docs/framework/tools/mpgo-exe-managed-profile-guided-optimization-tool.md) per ottimizzare [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] applicazioni nonché le applicazioni desktop.  
  
 Per le nuove funzionalità di ASP.NET 4.5.1, vedere [ASP.NET 4.5.1 e Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=309094) nel sito ASP.NET.  
  
 [Torna all'inizio](#introduction)  
  
<a name="core"></a>   
## <a name="whats-new-in-the-net-framework-45"></a>Novità di .NET Framework 4.5  
  
### <a name="core-new-features-and-improvements"></a>Miglioramenti e nuove funzionalità principali  
  
-   Possibilità di ridurre i riavvii di sistema rilevando e chiudendo le applicazioni .NET Framework 4 durante la distribuzione. Vedere [sistema di riduzione dei riavvii durante le installazioni di .NET Framework 4.5](../../../docs/framework/deployment/reducing-system-restarts.md).  
  
-   Supporto per le matrici di dimensioni maggiori di 2 GB nelle piattaforme a 64 bit. Questa funzionalità può essere abilitata nel file di configurazione dell'applicazione. Vedere il [ <> \> elemento](../../../docs/framework/configure-apps/file-schema/runtime/gcallowverylargeobjects-element.md), cui vengono inoltre elencate altre restrizioni sulle dimensioni dell'oggetto e dimensioni della matrice.  
  
-   Miglioramento delle prestazioni tramite Garbage Collection in background per server. Se si usa la funzionalità di Garbage Collection del server in [!INCLUDE[net_v45](../../../includes/net-v45-md.md)], verrà automaticamente abilità la Garbage Collection in background. Vedere la sezione Server Garbage Collection in Background di [principi fondamentali di Garbage Collection](../../../docs/standard/garbage-collection/fundamentals.md) argomento.  
  
-   Compilazione JIT in background, eventualmente disponibile nei processori multicore per migliorare le prestazioni delle applicazioni. Vedere <xref:System.Runtime.ProfileOptimization>.  
  
-   Possibilità di limitare il periodo in cui il motore delle espressioni regolari tenta di risolvere un'espressione regolare prima che si verifichi il timeout. Vedere il <xref:System.Text.RegularExpressions.Regex.MatchTimeout%2A?displayProperty=fullName> proprietà.  
  
-   Possibilità di definire le impostazioni cultura predefinite per un dominio di applicazione. Vedere il <xref:System.Globalization.CultureInfo> (classe).  
  
-   Supporto della console per la codifica Unicode (UTF-16). Vedere il <xref:System.Console> (classe).  
  
-   Supporto per il controllo delle versioni dei dati di confronto e ordinamento delle stringhe di impostazioni cultura. Vedere il <xref:System.Globalization.SortVersion> (classe).  
  
-   Miglioramento delle prestazioni in fase di recupero di risorse. Vedere [assemblaggio e distribuzione delle risorse](../../../docs/framework/resources/packaging-and-deploying-resources-in-desktop-apps.md).  
  
-   Miglioramenti delle compressioni ZIP per ridurre la dimensione di un file compresso. Vedere il <xref:System.IO.Compression?displayProperty=fullName> dello spazio dei nomi.  
  
-   Possibilità di personalizzare un contesto di reflection per eseguire l'override di comportamento di reflection predefinito tramite il <xref:System.Reflection.Context.CustomReflectionContext> (classe).  
  
-   Supporto per la versione 2008 di Internationalized Domain Names in Applications IDNA () standard quando la <xref:System.Globalization.IdnMapping?displayProperty=fullName> classe viene utilizzata in [!INCLUDE[win8](../../../includes/win8-md.md)].  
  
-   Delega del confronto tra stringhe al sistema operativo, che effettua l'implementazione di Unicode 6.0, quando .NET Framework viene usato in [!INCLUDE[win8](../../../includes/win8-md.md)]. Quando è in esecuzione in altre piattaforme, .NET Framework include i propri dati di confronto tra stringhe, che effettua l'implementazione di Unicode 5.x. Vedere il <xref:System.String> classe e la sezione Note del <xref:System.Globalization.SortVersion> (classe).  
  
-   Possibilità di calcolare i codici hash per le stringhe in base al dominio dell'applicazione. See [<>\> Element](../../../docs/framework/configure-apps/file-schema/runtime/userandomizedstringhashalgorithm-element.md).  
  
-   Supporto di reflection suddiviso tra i tipi <xref:System.Type> e <xref:System.Reflection.TypeInfo> classi. Vedere [Reflection in .NET Framework per applicazioni Windows Store](../../../docs/framework/reflection-and-codedom/reflection-for-windows-store-apps.md).  
  
### <a name="managed-extensibility-framework-mef"></a>Managed Extensibility Framework (MEF)  
 In [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] la libreria Managed Extensibility Framework (MEF) offre le seguenti nuove funzionalità:  
  
-   Supporto per tipi generici.  
  
-   Modello di programmazione basato su convenzioni che consente di creare parti basate sulle convenzioni di denominazione, anziché sugli attributi.  
  
-   Più ambiti.  
  
-   Subset di MEF che è possibile usare in fase di creazione delle applicazioni [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]. Questo subset è disponibile come un [pacchetto scaricabile](http://go.microsoft.com/fwlink/?LinkId=256238) dalla raccolta NuGet. Per installare il pacchetto, aprire il progetto in Visual Studio, scegliere **Gestisci pacchetti NuGet** dal **progetto** menu e cercare online il `Microsoft.Composition` pacchetto.  
  
 Per ulteriori informazioni, vedere [Managed Extensibility Framework (MEF)](../../../docs/framework/mef/index.md).  
  
### <a name="asynchronous-file-operations"></a>Operazioni asincrone sui file.  
 In [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] sono state aggiunte nuove funzionalità asincrone nei linguaggi C# e Visual Basic. Con queste funzionalità viene introdotto un modello basato su attività per eseguire operazioni asincrone. Per impiegare questo nuovo modello, usare i metodi asincroni nelle classi I/O. Vedere [i/o di File asincrono](../../../docs/standard/io/i-o-di-file-asincrono.md).  
  
<a name="tools"></a>   
### <a name="tools"></a>Strumenti  
 In [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] il generatore di file di risorse (Resgen.exe) consente di creare un file con estensione resw per l'uso nelle applicazioni [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] da un file con estensione resources incorporato in un assembly .NET Framework. Per ulteriori informazioni, vedere [Resgen.exe (Generatore di File di risorse)](../../../docs/framework/tools/resgen-exe-resource-file-generator.md).  
  
 L'ottimizzazione PGO gestita (Mpgo.exe) consente di migliorare i tempi di avvio delle applicazioni, l'uso della memoria (dimensione del working set) e la velocità effettiva attraverso l'ottimizzazione degli assembly di immagini nativi. Lo strumento da riga di comando genera dati di profilo per assembly di applicazioni di immagini nativi. Vedere [Mpgo.exe (strumento per l'ottimizzazione guidata da profilo gestito)](../../../docs/framework/tools/mpgo-exe-managed-profile-guided-optimization-tool.md). A partire da [!INCLUDE[vs_dev12](../../../includes/vs-dev12-md.md)] è possibile usare Mgpo.exe per ottimizzare le applicazioni [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] e quelle desktop.  
  
<a name="parallel"></a>   
### <a name="parallel-computing"></a>Elaborazione parallela  
 In [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] vengono forniti diversi miglioramenti e nuove funzionalità per il calcolo parallelo. Alcuni esempi: miglioramento delle prestazioni, maggiore controllo, supporto avanzato per la programmazione asincrona, una nuova libreria di flussi di dati e un miglioramento del supporto per il debug parallelo e l'analisi delle prestazioni. Vedere la voce [novità del parallelismo in .NET 4.5](http://go.microsoft.com/fwlink/?LinkId=235061) in parallelo blog sulla programmazione con .NET.  
  
<a name="web"></a>   
### <a name="web"></a>Web  
 In ASP.NET 4.5 e 4.5.1 vengono aggiunti associazione di modelli per Web Form, supporto di WebSocket, gestori asincroni, miglioramenti delle prestazioni e molte altre funzionalità. Per altre informazioni, vedere le seguenti risorse:  
  
-   [ASP.NET 4.5 e Visual Studio 2012](../Topic/ASP.NET%20Core%20and%20Visual%20Studio%202015.md) in MSDN Library.  
  
-   [ASP.NET 4.5.1 e Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=309094) nel sito ASP.NET.  
  
<a name="networking"></a>   
### <a name="networking"></a>Rete  
 In [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] viene fornita una nuova interfaccia di programmazione per applicazioni HTTP. Per ulteriori informazioni, vedere la nuova <xref:System.Net.Http?displayProperty=fullName> e <xref:System.Net.Http.Headers?displayProperty=fullName> gli spazi dei nomi.  
  
 Il supporto viene incluso anche per una nuova interfaccia di programmazione per l'accettazione e l'interazione con una connessione WebSocket usando esistente <xref:System.Net.HttpListener> e le classi correlate. Per ulteriori informazioni, vedere la nuova <xref:System.Net.WebSockets> dello spazio dei nomi e il <xref:System.Net.HttpListener> (classe).  
  
 In [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] sono inoltre inclusi i seguenti miglioramenti di rete:  
  
-   Supporto URI conforme a RFC. Per ulteriori informazioni, vedere <xref:System.Uri> e le classi correlate.  
  
-   Supporto per l'analisi IDN (Internationalized Domain Name). Per ulteriori informazioni, vedere <xref:System.Uri> e le classi correlate.  
  
-   Supporto per EAI (Email Address Internationalization). Per ulteriori informazioni, vedere il <xref:System.Net.Mail> dello spazio dei nomi.  
  
-   Supporto IPv6 avanzato. Per ulteriori informazioni, vedere il <xref:System.Net.NetworkInformation> dello spazio dei nomi.  
  
-   Supporto per socket dual mode. Per ulteriori informazioni, vedere il <xref:System.Net.Sockets.Socket> e <xref:System.Net.Sockets.TcpListener> classi.  
  
<a name="client"></a>   
### <a name="windows-presentation-foundation-wpf"></a>Windows Presentation Foundation (WPF)  
 In [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] Windows Presentation Foundation (WPF) include miglioramenti e modifiche nelle aree seguenti:  
  
-   Il nuovo <xref:System.Windows.Controls.Ribbon.Ribbon> controllo, che consente di implementare un'interfaccia utente della barra multifunzione che ospita una barra di accesso rapido, Menu dell'applicazione e schede.  
  
-   Il nuovo <xref:System.ComponentModel.INotifyDataErrorInfo> interfaccia, che supporta la convalida di dati sincroni e asincroni.  
  
-   Nuove funzionalità per il <xref:System.Windows.Controls.VirtualizingPanel> e <xref:System.Windows.Threading.Dispatcher> classi.  
  
-   Miglioramento delle prestazioni durante la visualizzazione di grandi set di dati raggruppati e mediante l'accesso alle raccolte in thread non dell'interfaccia utente.  
  
-   Un'associazione dati a proprietà statiche, associazione di dati personalizzati a tipi che implementano il <xref:System.Reflection.ICustomTypeProvider> interfaccia e il recupero di informazioni sull'associazione di dati da un'espressione di associazione.  
  
-   Riposizionamento di dati contestuale alla modifica dei valori (shaping attivo).  
  
-   Possibilità di controllare se il contesto dei dati per un contenitore di elementi è disconnesso.  
  
-   Possibilità di impostare la quantità di tempo che deve trascorrere tra le modifiche alle proprietà e gli aggiornamenti delle origini dati.  
  
-   Supporto avanzato per l'implementazione di modelli di eventi deboli. Inoltre, gli eventi possono ora accettare estensioni di markup.  
  
<a name="windows_communication_foundation"></a>   
### <a name="windows-communication-foundation-wcf"></a>Windows Communication Foundation (WCF)  
 In [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] le seguenti funzionalità sono state aggiunte per semplificare la scrittura e la gestione di applicazioni Windows Communication Foundation (WCF):  
  
-   Semplificazione dei file di configurazione generati.  
  
-   Supporto per lo sviluppo con priorità al contratto ("contract-first").  
  
-   Possibilità di configurare la modalità di compatibilità ASP.NET in modo più semplice.  
  
-   Modifiche ai valori predefiniti delle proprietà di trasporto per ridurre la probabilità di doverli impostare.  
  
-   Aggiorna il <xref:System.Xml.XmlDictionaryReaderQuotas> (classe) ridurre la probabilità che è necessario configurare manualmente le quote per i reader del dizionario XML.  
  
-   Convalida dei file di configurazione WCF da parte di Visual Studio nell'ambito del processo di compilazione, in modo da poter rilevare errori di configurazione prima di eseguire l'applicazione.  
  
-   Nuovo supporto per lo streaming asincrono.  
  
-   Nuovo mapping del protocollo HTTPS per semplificare l'esposizione di un endpoint su HTTPS con Internet Information Services (IIS).  
  
-   Possibilità di generare metadati in un singolo documento WSDL aggiungendo `?singleWSDL` all'URL del servizio.  
  
-   Supporto di WebSocket per consentire un'effettiva comunicazione bidirezionale sulle porte 80 e 443 con caratteristiche di prestazioni simili al trasporto TCP.  
  
-   Supporto per la configurazione dei servizi nel codice.  
  
-   Descrizioni comando dell'editor XML.  
  
-   <xref:System.ServiceModel.ChannelFactory> supporto di memorizzazione nella cache.  
  
-   Supporto della compressione del codificatore binario.  
  
-   Supporto per un trasporto UDP che consente agli sviluppatori di scrivere servizi che usano la messaggistica di tipo "Fire and Forget". Un client invia un messaggio a un servizio e non prevede alcuna risposta dal servizio.  
  
-   Possibilità di supportare più modalità di autenticazione in un singolo endpoint WCF quando si usa il trasporto HTTP e la sicurezza del trasporto.  
  
-   Supporto per servizi WCF che usano IDN (Internationalized Domain Name).  
  
 Per ulteriori informazioni, vedere [What's New in Windows Communication Foundation](http://go.microsoft.com/fwlink/?LinkId=228173).  
  
<a name="windows_workflow_foundation"></a>   
### <a name="windows-workflow-foundation-wf"></a>Windows Workflow Foundation (WF)  
 In [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] sono state introdotte numerose nuove funzionalità in Windows Workflow Foundation (WF), tra cui:  
  
-   Stato macchina i flussi di lavoro, che sono stati introdotti come parte di .NET Framework 4.0.1 ([.NET Framework 4 Platform Update 1](http://go.microsoft.com/fwlink/?LinkID=215092)). In questo aggiornamento erano incluse diverse nuove classi e attività che consentivano agli sviluppatori di creare flussi di lavoro macchina a stati. Queste classi e attività sono state aggiornate per [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] al fine di includere:  
  
    -   Possibilità di impostare punti di interruzione negli stati.  
  
    -   Possibilità di copiare e incollare transizioni in Workflow Designer.  
  
    -   Supporto della finestra di progettazione per la creazione di transizioni con trigger condivisi.  
  
    -   Attività per la creazione di flussi di lavoro di computer, tra cui: <xref:System.Activities.Statements.StateMachine>, <xref:System.Activities.Statements.State>, e <xref:System.Activities.Statements.Transition>.  
  
-   Funzionalità avanzate di Workflow Designer, tra cui:  
  
    -   Funzionalità avanzate di flusso di lavoro ricerca in Visual Studio, tra cui **ricerca veloce** e **Cerca nei file**.  
  
    -   Possibilità di creare automaticamente un'attività Sequence quando viene aggiunta una seconda attività figlio a un'attività del contenitore e di includere entrambe le attività nell'attività Sequence.  
  
    -   Supporto per panoramica, che consente di modificare la parte visibile di un flusso di lavoro senza ricorrere a barre di scorrimento.  
  
    -   Un nuovo **struttura documento** visualizzazione che mostra i componenti di un flusso di lavoro in una visualizzazione struttura ad albero e consente di selezionare un componente di **struttura documento** visualizzazione.  
  
    -   Possibilità di aggiungere annotazioni alle attività.  
  
    -   Capacità di definire e usare delegati di attività mediante Workflow Designer.  
  
    -   Connessione e inserimento automatici per attività e transizioni nei flussi di lavoro macchina a stati e del diagramma di flusso.  
  
-   Archiviazione di informazioni sullo stato di visualizzazione per un flusso di lavoro in un singolo elemento nel file XAML, in modo da poter individuare e modificare agevolmente tali informazioni.  
  
-   Attività del contenitore NoPersistScope per impedire la conservazione delle attività figlio.  
  
-   Supporto per espressioni C#:  
  
    -   I progetti di flusso di lavoro che usano Visual Basic impiegheranno espressioni Visual Basic, mentre i progetti di flusso di lavoro C# useranno espressioni C#.  
  
    -   I progetti di flusso di lavoro C# creati in Visual Studio 2010 e con espressioni Visual Basic sono compatibili con i progetti di flusso di lavoro C# che usano espressioni C#.  
  
-   Miglioramenti del controllo delle versioni:  
  
    -   Il nuovo <xref:System.Activities.WorkflowIdentity> (classe), che fornisce un mapping tra un'istanza del flusso di lavoro persistente e la relativa definizione del flusso di lavoro.  
  
    -   Esecuzione side-by-side di più versioni del flusso di lavoro nello stesso host, tra cui <xref:System.ServiceModel.Activities.WorkflowServiceHost>.  
  
    -   In Aggiornamento dinamico, capacità di modificare la definizione di un'istanza di flusso di lavoro persistente.  
  
-   Sviluppo di flussi di lavoro con priorità al contratto ("contract-first"), che fornisce supporto per generare automaticamente attività in modo da soddisfare un contratto di servizio esistente.  
  
 Per ulteriori informazioni, vedere [What's New in Windows Workflow Foundation](http://go.microsoft.com/fwlink/?LinkId=228176).  
  
<a name="tailored"></a>   
### [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)]  
 Le applicazioni [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] sono progettate per fattori di forma specifici e sfruttano la potenza del sistema operativo Windows. Un subset di [!INCLUDE[net_v45](../../../includes/net-v45-md.md)] o 4.5.1 è disponibile per la compilazione di applicazioni [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)] per Windows usando C# o Visual Basic. Questo subset è denominato [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)] e viene discusso in un [Panoramica](http://go.microsoft.com/fwlink/?LinkId=228491) nel Centro sviluppatori Windows.  
  
<a name="portable"></a>   
### <a name="portable-class-libraries"></a>Librerie di classi portabili  
 Il progetto Libreria di classi portabile in [!INCLUDE[vs_dev11_long](../../../includes/vs-dev11-long-md.md)] (e versioni successive) consente di scrivere e compilare assembly gestiti compatibili con più piattaforme .NET Framework. Se si usa un progetto Libreria di classi portabile, si scelgono le piattaforme (ad esempio Windows Phone e [!INCLUDE[net_win8_profile](../../../includes/net-win8-profile-md.md)]) di destinazione. I tipi e i membri disponibili nel progetto sono automaticamente limitati a tipi e membri comuni in queste piattaforme. Per ulteriori informazioni, vedere [libreria di classi portabile](../../../docs/standard/cross-platform/cross-platform-development-with-the-portable-class-library.md).  
  
## <a name="see-also"></a>Vedere anche  
 [.NET Framework e Out-of-Band versioni](../../../docs/framework/get-started/the-net-framework-and-out-of-band-releases.md)   
 [Novità di Visual Studio 2013](http://msdn.microsoft.com/library/bb386063\(v=vs.120\).aspx)   
 [ASP.NET 4.5.1 e strumenti Web per Visual Studio 2013](http://go.microsoft.com/fwlink/?LinkID=309094)   
 [ASP.NET e Visual Studio per il Web](../Topic/ASP.NET%20and%20Visual%20Studio%20for%20Web.md)   
 [Novità di Windows Communication Foundation](http://go.microsoft.com/fwlink/?LinkId=228173)   
 [Novità di Windows Workflow Foundation](http://go.microsoft.com/fwlink/?LinkId=228176)   
 [Novità di Visual C++](http://msdn.microsoft.com/library/hh409293\(v=vs.120\).aspx)