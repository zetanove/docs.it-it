---
title: "Migrazione dell&#39;app di Windows Store a .NET Native | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4153aa18-6f56-4a0a-865b-d3da743a1d05
caps.latest.revision: 29
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 29
---
# Migrazione dell&#39;app di Windows Store a .NET Native
[!INCLUDE[net_native](../../../includes/net-native-md.md)] fornisce la compilazione statica di applicazioni in Windows Store o sul computer dello sviluppatore. Ciò differisce dalla compilazione dinamica eseguita per applicazioni Windows Store dal compilatore just\-in\-time \(JIT\) o il [Native Image Generator \(Ngen.exe\)](../../../docs/framework/tools/ngen-exe-native-image-generator.md) sul dispositivo. Nonostante le differenze, [!INCLUDE[net_native](../../../includes/net-native-md.md)] prova a mantenere la compatibilità con [.NET per applicazioni Windows Store](http://msdn.microsoft.com/library/windows/apps/br230302.aspx). Nella maggior parte dei casi, ciò che funziona sulle app .NET per Windows Store funziona anche con [!INCLUDE[net_native](../../../includes/net-native-md.md)].  Tuttavia, in alcuni casi, è possibile riscontrare differenze di comportamento. In questo documento vengono illustrate le differenze tra .NET per applicazioni Windows Store standard e [!INCLUDE[net_native](../../../includes/net-native-md.md)] nelle seguenti aree:  
  
-   [Differenze generali di runtime](#Runtime)  
  
-   [Differenze di programmazione dinamica](#Dynamic)  
  
-   [Altre differenze correlate alla reflection](#Reflection)  
  
-   [Scenari e API non supportati](#Unsupported)  
  
-   [Differenze di Visual Studio](#VS)  
  
<a name="Runtime"></a>   
## Differenze generali di runtime  
  
-   Eccezioni, ad esempio <xref:System.TypeLoadException>, che vengono generate dal compilatore JIT quando un'applicazione eseguita su Common Language Runtime \(CLR\), in genere producono errori in fase di compilazione quando vengono elaborate da [!INCLUDE[net_native](../../../includes/net-native-md.md)].  
  
-   Non chiamare il metodo <xref:System.GC.WaitForPendingFinalizers%2A?displayProperty=fullName> da un thread UI dell'app. Ciò può causare un deadlock in [!INCLUDE[net_native](../../../includes/net-native-md.md)].  
  
-   Non fare affidamento sull'ordine di chiamata del costruttore di classe statica. In [!INCLUDE[net_native](../../../includes/net-native-md.md)], l'ordine di chiamata è diverso dall'ordine di runtime standard \(anche con il runtime standard, non è consigliabile fare affidamento sull'ordine di esecuzione dei costruttori di classe statici\).  
  
-   Un ciclo infinito senza eseguire una chiamata \(ad esempio, `while(true);`\) su qualsiasi thread può comportare l'arresto dell'applicazione. Allo stesso modo, attese lunghe o infinite possono portare all'arresto dell'applicazione.  
  
-   Alcuni cicli di inizializzazione generici non generano eccezioni in [!INCLUDE[net_native](../../../includes/net-native-md.md)]. Ad esempio, il codice seguente genera un'eccezione <xref:System.TypeLoadException> sul CLR standard, mentre in [!INCLUDE[net_native](../../../includes/net-native-md.md)] ciò non accade.  
  
     [!code-csharp[ProjectN#8](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/compat1.cs#8)]  
  
-   In alcuni casi, [!INCLUDE[net_native](../../../includes/net-native-md.md)] fornisce implementazioni diverse di librerie di classi .NET Framework. Un oggetto restituito da un metodo implementerà sempre i membri del tipo restituito. Tuttavia, poiché l'implementazione di supporto è diversa, potrebbe non essere possibile eseguire il cast per la stessa raccolta di tipi come su altre piattaforme di.NET Framework. Ad esempio, in alcuni casi, potrebbe non essere possibile eseguire il cast dell'oggetto di interfaccia <xref:System.Collections.Generic.IEnumerable%601> restituito da metodi quali <xref:System.Reflection.TypeInfo.DeclaredMembers%2A?displayProperty=fullName> o <xref:System.Reflection.TypeInfo.DeclaredProperties%2A?displayProperty=fullName> a `T[]`.  
  
-   La cache di WinINet non è abilitata per impostazione predefinita su .NET per applicazioni Windows Store, ma lo è su [!INCLUDE[net_native](../../../includes/net-native-md.md)]. Questo migliora le prestazioni, ma ha implicazioni sul working set. Non è necessaria alcuna azione da parte dello sviluppatore.  
  
<a name="Dynamic"></a>   
## Differenze di programmazione dinamica  
 [!INCLUDE[net_native](../../../includes/net-native-md.md)] collega in modo statico il codice da .NET Framework per rendere il codice app\-local e ottenere prestazioni ottimali. Tuttavia, le dimensioni binarie devono rimanere ridotte, in modo da non consentire il passaggio dell'intero.NET Framework. Il compilatore di [!INCLUDE[net_native](../../../includes/net-native-md.md)] risolve questa limitazione usando un riduttore di dipendenza che rimuove i riferimenti al codice non usato. Tuttavia, [!INCLUDE[net_native](../../../includes/net-native-md.md)] può non gestire o generare alcune informazioni sul tipo e il codice quando tali informazioni non possono essere dedotte in modo statico in fase di compilazione, ma al contrario vengono recuperate in modo dinamico in fase di esecuzione.  
  
 [!INCLUDE[net_native](../../../includes/net-native-md.md)] non attiva la reflection e la programmazione dinamica. Tuttavia, non tutti i tipi possono essere contrassegnati per la reflection, perché ciò rende eccessive le dimensioni del codice generato \(soprattutto perché la reflection sulle API pubbliche in .NET Framework è supportata\). Il compilatore di [!INCLUDE[net_native](../../../includes/net-native-md.md)] opera scelte intelligenti su quali tipi devono supportare la reflection e mantiene i metadati generando il codice solo per i tipi.  
  
 Ad esempio, il data binding richiede che un'applicazione possa eseguire il mapping dei nomi di proprietà alle funzioni. In .NET per applicazioni Windows Store, Common Language Runtime usa automaticamente la reflection per fornire questa funzionalità per i tipi gestiti e i tipi nativi disponibili al pubblico. In [!INCLUDE[net_native](../../../includes/net-native-md.md)], il compilatore include automaticamente i metadati per i tipi a cui associare i dati.  
  
 Il compilatore di [!INCLUDE[net_native](../../../includes/net-native-md.md)] può anche gestire i tipi generici usati comunemente come <xref:System.Collections.Generic.List%601> e <xref:System.Collections.Generic.Dictionary%602>, che funzionano senza richiedere suggerimenti o direttive. È supportata anche la parola chiave [dinamica](../Topic/dynamic%20\(C%23%20Reference\).md) entro certi limiti.  
  
> [!NOTE]
>  È consigliabile verificare accuratamente tutti i percorsi di codice dinamico durante l'importazione dell'applicazione in [!INCLUDE[net_native](../../../includes/net-native-md.md)].  
  
 La configurazione predefinita per [!INCLUDE[net_native](../../../includes/net-native-md.md)] è sufficiente per la maggior parte degli sviluppatori, ma per alcuni sviluppatori potrebbe essere necessario ritoccare le relative configurazioni usando un file delle direttive di runtime \(rd.xml\). Inoltre, in alcuni casi, il compilatore [!INCLUDE[net_native](../../../includes/net-native-md.md)] non può determinare quali metadati devono essere disponibili per la reflection e si basa su suggerimenti, in particolare nei seguenti casi:  
  
-   Alcuni costrutti come <xref:System.Type.MakeGenericType%2A?displayProperty=fullName> e <xref:System.Reflection.MethodInfo.MakeGenericMethod%2A?displayProperty=fullName> non possono essere determinati staticamente.  
  
-   Poiché il compilatore non può determinare le istanze create, un tipo generico di cui si vuole effettuare la reflection deve essere specificato dalle direttive di runtime. Ciò non solo perché è necessario includere tutto il codice, ma anche perché la reflection sui tipi può creare un ciclo infinito \(ad esempio, quando un metodo generico viene richiamato su un tipo generico\).  
  
> [!NOTE]
>  Le direttive di runtime sono definite in un file nelle direttive di runtime \(rd.xml\). Per informazioni generali sull'uso di questo file, vedere [Introduzione](../../../docs/framework/net-native/getting-started-with-net-native.md). Per informazioni sulle direttive di runtime, vedere [Riferimento a file di configurazione di direttive di runtime \(rd.xml\)](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md).  
  
 [!INCLUDE[net_native](../../../includes/net-native-md.md)] include anche strumenti di profilatura che consentono allo sviluppatore di determinare quali tipi all'esterno del set predefinito devono supportare la reflection.  
  
<a name="Reflection"></a>   
## Altre differenze correlate alla reflection  
 Esistono numerose altre differenze di comportamento relative alla reflection tra .NET per applicazioni Windows Store e [!INCLUDE[net_native](../../../includes/net-native-md.md)].  
  
 In [!INCLUDE[net_native](../../../includes/net-native-md.md)]:  
  
-   La reflection privata su tipi e membri della libreria di classi .NET Framework non è supportata. È tuttavia possibile riflettere sui propri tipi e membri privati, nonché sui tipi e membri nelle librerie di terze parti.  
  
-   La proprietà <xref:System.Reflection.ParameterInfo.HasDefaultValue%2A?displayProperty=fullName> restituisce correttamente `false` per un oggetto <xref:System.Reflection.ParameterInfo> che rappresenta un valore restituito. In .NET per applicazioni Windows Store, restituisce `true`. IL \(Intermediate language\) non supporta direttamente questa funzione, e quindi l'interpretazione viene lasciata al linguaggio.  
  
-   I membri pubblici sulle strutture <xref:System.RuntimeFieldHandle> e <xref:System.RuntimeMethodHandle> non sono supportati. Questi tipi sono supportati solo per LINQ, gli alberi delle espressioni e l'inizializzazione di matrice statica.  
  
-   <xref:System.Reflection.RuntimeReflectionExtensions.GetRuntimeProperties%2A?displayProperty=fullName> e <xref:System.Reflection.RuntimeReflectionExtensions.GetRuntimeEvents%2A?displayProperty=fullName> includono membri nascosi in classi di base e perciò potrebbero essere sottoposti a override esplicito. Ciò vale anche per gli altri metodi [RuntimeReflectionExtensions.GetRuntime\*](http://msdn.microsoft.com/library/system.reflection.runtimereflectionextensions_methods.aspx).  
  
-   <xref:System.Type.MakeArrayType%2A?displayProperty=fullName> e <xref:System.Type.MakeByRefType%2A?displayProperty=fullName> non hanno esito negativo quando si prova a creare determinate combinazioni \(ad esempio, una matrice di ByRef\).  
  
-   Non è possibile usare la reflection per richiamare i membri con parametri di puntatore.  
  
-   Non è possibile usare la reflection per ottenere o impostare un campo del puntatore.  
  
-   Quando il numero di argomenti è errato e il tipo di uno degli argomenti non è corretto, [!INCLUDE[net_native](../../../includes/net-native-md.md)] genera una <xref:System.ArgumentException> invece di una <xref:System.Reflection.TargetParameterCountException>.  
  
-   In genere la serializzazione binaria delle eccezioni non è supportata. Di conseguenza, è possibile aggiungere gli oggetti non serializzabili al dizionario <xref:System.Exception.Data%2A?displayProperty=fullName>.  
  
<a name="Unsupported"></a>   
## Scenari e API non supportati  
 Nelle sezioni seguenti vengono elencati gli scenari e le API non supportati per lo sviluppo generale, l'interoperabilità e le tecnologie, ad esempio HTTPClient e Windows Communication Foundation \(WCF\):  
  
-   [Sviluppo generale](#General)  
  
-   [HttpClient](#HttpClient)  
  
-   [Interoperabilità](#Interop)  
  
-   [API non supportate](#APIs)  
  
<a name="General"></a>   
### Differenze generali per lo sviluppo  
 **Tipi di valore**  
  
-   Se si esegue l'override dei metodi <xref:System.ValueType.Equals%2A?displayProperty=fullName> e <xref:System.ValueType.GetHashCode%2A?displayProperty=fullName> per un tipo di valore, non chiamare le implementazioni della classe di base. In .NET per applicazioni Windows Store, questi metodi si basano sulla reflection. In fase di compilazione, [!INCLUDE[net_native](../../../includes/net-native-md.md)] genera un'implementazione che non si basa sulla reflection di runtime. Ciò significa che se si non esegue l'override di questi due metodi, funzioneranno come previsto, perché [!INCLUDE[net_native](../../../includes/net-native-md.md)] genera l'implementazione in fase di compilazione. Tuttavia, se si esegue l'override di questi metodi, ma si chiama l'implementazione della classe base verrà generata un'eccezione.  
  
-   Non sono supportati i tipi di valore superiori a un megabyte.  
  
-   I tipi di valore non possono avere un costruttore predefinito in [!INCLUDE[net_native](../../../includes/net-native-md.md)] \(C\# e Visual Basic vietano i costruttori predefiniti sui tipi di valore. Tuttavia, è possibile crearli in IL\).  
  
 **Matrici**  
  
-   Non sono supportate le matrici con limite inferiore diverso da zero. Solitamente, queste matrici vengono create chiamando l'overload di [Array.CreateInstance\(Type, Int32\[\], Int32\<xref:System.Array.CreateInstance%28System.Type%2CSystem.Int32%5B%5D%2CSystem.Int32%5B%5D%29?displayProperty=fullName>.  
  
-   Non è supportata la creazione dinamica di matrici multidimensionali. Tali matrici vengono in genere creata dalla chiamata di un overload del metodo <xref:System.Array.CreateInstance%2A?displayProperty=fullName> che include un parametro `lengths` oppure dalla chiamata del metodo <xref:System.Type.MakeArrayType%28System.Int32%29?displayProperty=fullName>.  
  
-   Le matrici multidimensionali con quattro o più dimensioni non sono supportate; vale a dire il relativo valore della proprietà <xref:System.Array.Rank%2A?displayProperty=fullName> è 4 o superiore. Usare invece le [matrici irregolari](../Topic/Jagged%20Arrays%20\(C%23%20Programming%20Guide\).md) \(una matrice di matrici\). Ad esempio, `array[x,y,z]` non è valido, mentre `array[x][y][z]` è valido.  
  
-   La varianza per le matrici multidimensionali non è supportata e causa un'eccezione <xref:System.InvalidCastException> in fase di esecuzione.  
  
 **Generics**  
  
-   L'espansione di tipo generico infinito genera un errore del compilatore. Ad esempio, questo codice non viene compilato:  
  
     [!code-csharp[ProjectN#9](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/compat2.cs#9)]  
  
 **Pointers**  
  
-   Le matrici di puntatori non sono supportate.  
  
-   Non è possibile usare la reflection per ottenere o impostare un campo del puntatore.  
  
 **Serializzazione**  
  
 L'attributo <xref:System.Runtime.Serialization.KnownTypeAttribute.%23ctor%28System.String%29> non è supportato. Usare piuttosto l'attributo <xref:System.Runtime.Serialization.KnownTypeAttribute.%23ctor%28System.Type%29>.  
  
 **Risorse**  
  
 L'uso di risorse localizzate con la classe <xref:System.Diagnostics.Tracing.EventSource> non è supportato. La proprietà <xref:System.Diagnostics.Tracing.EventSourceAttribute.LocalizationResources%2A?displayProperty=fullName> non definisce le risorse localizzate.  
  
 **Delegati**  
  
 `Delegate.BeginInvoke` e `Delegate.EndInvoke` non sono supportati.  
  
 **Async**  
  
 La logica di threading negli overload di Task IAsync non è supportata.  
  
 **Varie API**  
  
-   La proprietà <xref:System.Reflection.TypeInfo.GUID%2A?displayProperty=fullName> genera un'eccezione <xref:System.PlatformNotSupportedException> se un attributo <xref:System.Runtime.InteropServices.GuidAttribute> non viene applicato al tipo. Il GUID viene usato principalmente per il supporto COM.  
  
-   Il metodo <xref:System.DateTime.Parse%2A?displayProperty=fullName> analizza correttamente le stringhe che contengono date brevi in [!INCLUDE[net_native](../../../includes/net-native-md.md)]. Tuttavia, non mantiene la compatibilità con le modifiche nell'analisi di data e ora descritte negli articoli della Microsoft Knowledge Base [KB2803771](http://support.microsoft.com/kb/2803771) e [KB2803755](http://support.microsoft.com/kb/2803755).  
  
-   <xref:System.Numerics.BigInteger.ToString%2A?displayProperty=fullName> `("E")` è arrotondata correttamente in [!INCLUDE[net_native](../../../includes/net-native-md.md)]. In alcune versioni di CLR, la stringa di risultato viene troncata anziché arrotondata.  
  
<a name="HttpClient"></a>   
### Differenze di HttpClient  
 In [!INCLUDE[net_native](../../../includes/net-native-md.md)] la classe <xref:System.Net.Http.HttpClientHandler> usa internamente WinINet \(tramite la classe [HttpBaseProtocolFilter](http://msdn.microsoft.com/library/windows/apps/windows.web.http.filters.httpbaseprotocolfilter.aspx)\) anziché le classi <xref:System.Net.WebRequest> e <xref:System.Net.WebResponse> usate nella versione standard di .NET per applicazioni Windows Store.  WinINet non supporta tutte le opzioni di configurazione supportate dalla classe <xref:System.Net.Http.HttpClientHandler>.  Di conseguenza, si verifica quanto segue:  
  
-   Alcune delle proprietà di capacità su <xref:System.Net.Http.HttpClientHandler> restituiscono `false` su [!INCLUDE[net_native](../../../includes/net-native-md.md)], laddove restituiscono `true` in .NET per applicazioni Windows Store standard.  
  
-   Alcune delle le funzioni di accesso `get` della proprietà di configurazione restituisce sempre un valore fisso in [!INCLUDE[net_native](../../../includes/net-native-md.md)], diverso da quello predefinito configurabile in .NET per applicazioni Windows Store.  
  
 Nelle sottosezioni riportate di seguito sono descritte alcune differenze di comportamento aggiuntive.  
  
 **Proxy**  
  
 La classe [HttpBaseProtocolFilter](http://msdn.microsoft.com/library/windows/apps/windows.web.http.filters.httpbaseprotocolfilter.aspx) non supporta la configurazione o l'override del proxy in base a ogni richiesta.  Ciò significa che tutte le richieste su [!INCLUDE[net_native](../../../includes/net-native-md.md)] usano il server proxy configurato dal sistema o nessun server proxy, a seconda del valore della proprietà <xref:System.Net.Http.HttpClientHandler.UseProxy%2A?displayProperty=fullName>.  In .NET per applicazioni Windows Store il server proxy viene definito dalla proprietà <xref:System.Net.Http.HttpClientHandler.Proxy%2A?displayProperty=fullName>.  In [!INCLUDE[net_native](../../../includes/net-native-md.md)], l'impostazione di <xref:System.Net.Http.HttpClientHandler.Proxy%2A?displayProperty=fullName> su un valore diverso da `null` genera un'eccezione <xref:System.PlatformNotSupportedException>.  La proprietà <xref:System.Net.Http.HttpClientHandler.SupportsProxy%2A?displayProperty=fullName> restituisce `false` su [!INCLUDE[net_native](../../../includes/net-native-md.md)], laddove restituisce `true` in .NET per applicazioni Windows Store standard.  
  
 **Reindirizzamento automatico**  
  
 La classe [HttpBaseProtocolFilter](http://msdn.microsoft.com/library/windows/apps/windows.web.http.filters.httpbaseprotocolfilter.aspx) non consente la configurazione del numero massimo di reindirizzamenti automatici.  Il valore della proprietà <xref:System.Net.Http.HttpClientHandler.MaxAutomaticRedirections%2A?displayProperty=fullName> è 50 per impostazione predefinita in .NET per applicazioni Windows Store standard e può essere modificato. In [!INCLUDE[net_native](../../../includes/net-native-md.md)], il valore di questa proprietà è 10 e se si prova a modificarlo viene generata un'eccezione <xref:System.PlatformNotSupportedException>.  La proprietà <xref:System.Net.Http.HttpClientHandler.SupportsRedirectConfiguration%2A?displayProperty=fullName> restituisce `false` su [!INCLUDE[net_native](../../../includes/net-native-md.md)], laddove restituisce `true` in .NET per applicazioni Windows Store.  
  
 **Decompressione automatica**  
  
 .NET per applicazioni Windows Store consente di impostare la proprietà <xref:System.Net.Http.HttpClientHandler.AutomaticDecompression%2A?displayProperty=fullName> su <xref:System.Net.DecompressionMethods>, <xref:System.Net.DecompressionMethods>, sia <xref:System.Net.DecompressionMethods> che <xref:System.Net.DecompressionMethods> o <xref:System.Net.DecompressionMethods>.[!INCLUDE[net_native](../../../includes/net-native-md.md)] supporta solo <xref:System.Net.DecompressionMethods> assieme a <xref:System.Net.DecompressionMethods> o <xref:System.Net.DecompressionMethods>.  Provare a impostare la proprietà <xref:System.Net.Http.HttpClientHandler.AutomaticDecompression%2A> su <xref:System.Net.DecompressionMethods> o <xref:System.Net.DecompressionMethods> da soli comporta l'impostazione automatica su <xref:System.Net.DecompressionMethods> e <xref:System.Net.DecompressionMethods>.  
  
 **Cookie**  
  
 La gestione dei cookie viene eseguita simultaneamente da <xref:System.Net.Http.HttpClient> e WinINet.  I cookie di <xref:System.Net.CookieContainer> vengono combinati con i cookie nella cache dei cookie di WinINet.  La rimozione di un cookie da <xref:System.Net.CookieContainer> impedisce a <xref:System.Net.Http.HttpClient> di inviarlo, ma se è già stato rilevato da WinINet, e i cookie non sono stati eliminati dall'utente, WinINet lo invia.  Non è possibile rimuovere a livello di codice un cookie da WinINet usando le API <xref:System.Net.Http.HttpClient>, <xref:System.Net.Http.HttpClientHandler> o <xref:System.Net.CookieContainer>.  L'impostazione della proprietà <xref:System.Net.Http.HttpClientHandler.UseCookies%2A?displayProperty=fullName> su `false` fa solo sì che <xref:System.Net.Http.HttpClient> smetta di inviare cookie; WinINet potrebbe ancora includere i propri cookie nella richiesta.  
  
 **Credenziali**  
  
 In .NET per applicazioni Windows Store, le proprietà <xref:System.Net.Http.HttpClientHandler.UseDefaultCredentials%2A?displayProperty=fullName> e <xref:System.Net.Http.HttpClientHandler.Credentials%2A?displayProperty=fullName> funzionano in maniera indipendente.  Inoltre, la proprietà <xref:System.Net.Http.HttpClientHandler.Credentials%2A> accetta qualsiasi oggetto che implementa l'interfaccia <xref:System.Net.ICredentials>.  In [!INCLUDE[net_native](../../../includes/net-native-md.md)], impostare la proprietà <xref:System.Net.Http.HttpClientHandler.UseDefaultCredentials%2A> su `true` fa sì che la proprietà <xref:System.Net.Http.HttpClientHandler.Credentials%2A> diventi `null`.  Inoltre, la proprietà <xref:System.Net.Http.HttpClientHandler.Credentials%2A> può essere impostata solo su `null`, <xref:System.Net.CredentialCache.DefaultCredentials%2A> o un oggetto di tipo <xref:System.Net.NetworkCredential>.  L'assegnazione di qualsiasi altro oggetto <xref:System.Net.ICredentials>, il più popolare dei quali è <xref:System.Net.CredentialCache>, alla proprietà <xref:System.Net.Http.HttpClientHandler.Credentials%2A> genera una <xref:System.PlatformNotSupportedException>.  
  
 **Altre funzionalità non supportate o non configurabili**  
  
 In [!INCLUDE[net_native](../../../includes/net-native-md.md)]:  
  
-   Il valore della proprietà <xref:System.Net.Http.HttpClientHandler.ClientCertificateOptions%2A?displayProperty=fullName> è sempre <xref:System.Net.Http.ClientCertificateOption>.  In .NET per applicazioni Windows Store, il valore predefinito è <xref:System.Net.Http.ClientCertificateOption>.  
  
-   La proprietà <xref:System.Net.Http.HttpClientHandler.MaxRequestContentBufferSize%2A?displayProperty=fullName> non è configurabile.  
  
-   La proprietà <xref:System.Net.Http.HttpClientHandler.PreAuthenticate%2A?displayProperty=fullName> è sempre `true`.  In .NET per applicazioni Windows Store, il valore predefinito è `false`.  
  
-   L'intestazione `SetCookie2` nelle risposte verrà ignorata come obsoleta.  
  
<a name="Interop"></a>   
### Differenze di interoperabilità  
 **API deprecate**  
  
 Una serie di API usate con minore frequenza per l'interoperabilità con codice gestito è stata deprecata. Quando usate con [!INCLUDE[net_native](../../../includes/net-native-md.md)], queste API possono generare un'eccezione <xref:System.NotImplementedException> o <xref:System.PlatformNotSupportedException> oppure produrre un errore del compilatore. In .NET per applicazioni Windows Store, queste API vengono contrassegnate come obsolete, anche se la chiamata genera un avviso del compilatore invece di un errore del compilatore.  
  
 API deprecate per il marshalling di `VARIANT`:  
  
||  
|-|  
|<xref:System.Runtime.InteropServices.BStrWrapper?displayProperty=fullName>|  
|<xref:System.Runtime.InteropServices.CurrencyWrapper?displayProperty=fullName>|  
|<xref:System.Runtime.InteropServices.DispatchWrapper?displayProperty=fullName>|  
|<xref:System.Runtime.InteropServices.ErrorWrapper?displayProperty=fullName>|  
|<xref:System.Runtime.InteropServices.UnknownWrapper?displayProperty=fullName>|  
|<xref:System.Runtime.InteropServices.VariantWrapper?displayProperty=fullName>|  
|<xref:System.Runtime.InteropServices.UnmanagedType?displayProperty=fullName>|  
|<xref:System.Runtime.InteropServices.UnmanagedType?displayProperty=fullName>|  
|<xref:System.Runtime.InteropServices.VarEnum?displayProperty=fullName>|  
  
 <xref:System.Runtime.InteropServices.UnmanagedType?displayProperty=fullName> è supportata, ma genera un'eccezione in alcuni scenari, ad esempio quando viene usata con [IDispatch](http://msdn.microsoft.com/library/windows/apps/ms221608.aspx) o varianti di ByRef.  
  
 Le API deprecate per [IDispatch](http://msdn.microsoft.com/library/windows/apps/ms221608.aspx) supportano:  
  
|Tipo|Membro|  
|----------|------------|  
|<xref:System.Runtime.InteropServices.ClassInterfaceType?displayProperty=fullName>|<xref:System.Runtime.InteropServices.ClassInterfaceType>|  
|<xref:System.Runtime.InteropServices.ClassInterfaceType?displayProperty=fullName>|<xref:System.Runtime.InteropServices.ClassInterfaceType>|  
|<xref:System.Runtime.InteropServices.ComDefaultInterfaceAttribute?displayProperty=fullName>|L'attributo non è supportato.|  
  
 API deprecate per eventi COM classici:  
  
||  
|-|  
|<xref:System.Runtime.InteropServices.ComEventsHelper?displayProperty=fullName>|  
|<xref:System.Runtime.InteropServices.ComSourceInterfacesAttribute>|  
  
 API deprecate nell'interfaccia <xref:System.Runtime.InteropServices.ICustomQueryInterface?displayProperty=fullName>, che non è supportata in [!INCLUDE[net_native](../../../includes/net-native-md.md)]:  
  
|Tipo|Membro|  
|----------|------------|  
|<xref:System.Runtime.InteropServices.ICustomQueryInterface?displayProperty=fullName>|Tutti i membri.|  
|<xref:System.Runtime.InteropServices.CustomQueryInterfaceMode?displayProperty=fullName>|Tutti i membri.|  
|<xref:System.Runtime.InteropServices.CustomQueryInterfaceResult?displayProperty=fullName>|Tutti i membri.|  
|<xref:System.Runtime.InteropServices.Marshal?displayProperty=fullName>|<xref:System.Runtime.InteropServices.Marshal.GetComInterfaceForObject%28System.Object%2CSystem.Type%2CSystem.Runtime.InteropServices.CustomQueryInterfaceMode%29?displayProperty=fullName>|  
  
 Altre funzionalità di interoperabilità non supportate:  
  
|Tipo|Membro|  
|----------|------------|  
|<xref:System.Runtime.InteropServices.ICustomAdapter?displayProperty=fullName>|Tutti i membri.|  
|<xref:System.Runtime.InteropServices.SafeBuffer?displayProperty=fullName>|Tutti i membri.|  
|<xref:System.Runtime.InteropServices.UnmanagedType?displayProperty=fullName>|<xref:System.Runtime.InteropServices.UnmanagedType>|  
|<xref:System.Runtime.InteropServices.UnmanagedType?displayProperty=fullName>|<xref:System.Runtime.InteropServices.UnmanagedType>|  
|<xref:System.Runtime.InteropServices.UnmanagedType?displayProperty=fullName>|<xref:System.Runtime.InteropServices.UnmanagedType>|  
|<xref:System.Runtime.InteropServices.UnmanagedType?displayProperty=fullName>|<xref:System.Runtime.InteropServices.UnmanagedType>|  
|<xref:System.Runtime.InteropServices.UnmanagedType?displayProperty=fullName>|<xref:System.Runtime.InteropServices.UnmanagedType>|  
  
 API di marshalling raramente usate:  
  
|Tipo|Membro|  
|----------|------------|  
|<xref:System.Runtime.InteropServices.Marshal?displayProperty=fullName>|<xref:System.Runtime.InteropServices.Marshal.ReadByte%28System.Object%2CSystem.Int32%29>|  
|<xref:System.Runtime.InteropServices.Marshal?displayProperty=fullName>|<xref:System.Runtime.InteropServices.Marshal.ReadInt16%28System.Object%2CSystem.Int32%29>|  
|<xref:System.Runtime.InteropServices.Marshal?displayProperty=fullName>|<xref:System.Runtime.InteropServices.Marshal.ReadInt32%28System.Object%2CSystem.Int32%29>|  
|<xref:System.Runtime.InteropServices.Marshal?displayProperty=fullName>|<xref:System.Runtime.InteropServices.Marshal.ReadInt64%28System.Object%2CSystem.Int32%29>|  
|<xref:System.Runtime.InteropServices.Marshal?displayProperty=fullName>|<xref:System.Runtime.InteropServices.Marshal.ReadIntPtr%28System.Object%2CSystem.Int32%29>|  
|<xref:System.Runtime.InteropServices.Marshal?displayProperty=fullName>|<xref:System.Runtime.InteropServices.Marshal.WriteByte%28System.Object%2CSystem.Int32%2CSystem.Byte%29>|  
|<xref:System.Runtime.InteropServices.Marshal?displayProperty=fullName>|<xref:System.Runtime.InteropServices.Marshal.WriteInt16%28System.Object%2CSystem.Int32%2CSystem.Int16%29>|  
|<xref:System.Runtime.InteropServices.Marshal?displayProperty=fullName>|<xref:System.Runtime.InteropServices.Marshal.WriteInt32%28System.Object%2CSystem.Int32%2CSystem.Int32%29>|  
|<xref:System.Runtime.InteropServices.Marshal?displayProperty=fullName>|<xref:System.Runtime.InteropServices.Marshal.WriteInt64%28System.Object%2CSystem.Int32%2CSystem.Int64%29>|  
|<xref:System.Runtime.InteropServices.Marshal?displayProperty=fullName>|<xref:System.Runtime.InteropServices.Marshal.WriteIntPtr%28System.Object%2CSystem.Int32%2CSystem.IntPtr%29>|  
  
 **Compatibilità platform invoke e interoperabilità COM**  
  
 La maggior parte dei scenari di platform invoke e interoperabilità COM sono ancora supportati in [!INCLUDE[net_native](../../../includes/net-native-md.md)]. In particolare, sono supportate tutte le API di interoperabilità con Windows Runtime \(WinRT\) e tutti i marshalling richiesti per Windows Runtime. Ciò include il supporto del marshalling per:  
  
-   Matrici \(inclusa <xref:System.Runtime.InteropServices.UnmanagedType?displayProperty=fullName>\)  
  
-   `BStr`  
  
-   Delegati  
  
-   Stringhe \(Unicode, Ansi e HSTRING\)  
  
-   Struct \(`byref` e `byval`\)  
  
-   Unioni  
  
-   Handle Win32  
  
-   Tutti i costrutti di WinRT  
  
-   Supporto parziale per il marshalling dei tipi variant. È supportato quanto segue:  
  
    -   <xref:System.Boolean>  
  
    -   <xref:System.Byte>  
  
    -   <xref:System.Decimal>  
  
    -   <xref:System.Double>  
  
    -   <xref:System.Int16>  
  
    -   <xref:System.Int32>  
  
    -   <xref:System.Int64>  
  
    -   <xref:System.SByte>  
  
    -   <xref:System.Single>  
  
    -   <xref:System.UInt16>  
  
    -   <xref:System.UInt32>  
  
    -   <xref:System.UInt64>  
  
    -   `BStr`  
  
    -   [IUnknown](http://msdn.microsoft.com/library/windows/desktop/ms680509.aspx)  
  
 Tuttavia, [!INCLUDE[net_native](../../../includes/net-native-md.md)] non supporta quanto segue:  
  
-   Utilizzo degli eventi COM classici  
  
-   Implementazione dell'interfaccia <xref:System.Runtime.InteropServices.ICustomQueryInterface?displayProperty=fullName> su un tipo gestito  
  
-   Implementazione dell'interfaccia [IDispatch](http://msdn.microsoft.com/library/windows/apps/ms221608.aspx) su un tipo gestito tramite l'attributo <xref:System.Runtime.InteropServices.ComDefaultInterfaceAttribute?displayProperty=fullName>. Notare tuttavia che non è possibile chiamare oggetti COM tramite `IDispatch` e l'oggetto gestito non può implementare `IDispatch`.  
  
 L'uso della reflection per richiamare un metodo platform invoke non è supportato. È possibile aggirare questa limitazione eseguendo il wrapping della chiamata al metodo in un altro metodo e usando la reflection per chiamare invece il wrapper.  
  
<a name="APIs"></a>   
### Altre differenze rispetto alle API .NET per app di Windows Store  
 In questa sezione sono elencate le API rimanenti che non sono supportate in [!INCLUDE[net_native](../../../includes/net-native-md.md)]. Il set più grande di API non supportate è rappresentato dalle API di Windows Communication Foundation \(WCF\).  
  
 **DataAnnotations \(System.ComponentModel.DataAnnotations\)**  
  
 I tipi negli spazi dei nomi <xref:System.ComponentModel.DataAnnotations> e <xref:System.ComponentModel.DataAnnotations.Schema> non sono supportati in [!INCLUDE[net_native](../../../includes/net-native-md.md)]. Questi includono i seguenti tipi che sono presenti in .NET per applicazioni Windows Store per Windows 8:  
  
||  
|-|  
|<xref:System.ComponentModel.DataAnnotations.AssociationAttribute?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.ConcurrencyCheckAttribute?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.CustomValidationAttribute?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.DataType?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.DataTypeAttribute?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.DisplayAttribute?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.DisplayColumnAttribute?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.DisplayFormatAttribute>|  
|<xref:System.ComponentModel.DataAnnotations.EditableAttribute>|  
|<xref:System.ComponentModel.DataAnnotations.EnumDataTypeAttribute>|  
|<xref:System.ComponentModel.DataAnnotations.FilterUIHintAttribute?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.KeyAttribute?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.RangeAttribute?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.RegularExpressionAttribute?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.RequiredAttribute?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.StringLengthAttribute?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.TimestampAttribute?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.UIHintAttribute?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.ValidationAttribute?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.ValidationContext?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.ValidationException?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.ValidationResult?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.Validator?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.Schema.DatabaseGeneratedAttribute?displayProperty=fullName>|  
|<xref:System.ComponentModel.DataAnnotations.Schema.DatabaseGeneratedOption?displayProperty=fullName>|  
  
 **Visual Basic**  
  
 Visual Basic non è attualmente supportato in [!INCLUDE[net_native](../../../includes/net-native-md.md)]. I seguenti tipi negli spazi dei nomi <xref:Microsoft.VisualBasic> e <xref:Microsoft.VisualBasic.CompilerServices> non sono disponibili in [!INCLUDE[net_native](../../../includes/net-native-md.md)]:  
  
||  
|-|  
|<xref:Microsoft.VisualBasic.CallType?displayProperty=fullName>|  
|<xref:Microsoft.VisualBasic.Constants?displayProperty=fullName>|  
|<xref:Microsoft.VisualBasic.HideModuleNameAttribute?displayProperty=fullName>|  
|<xref:Microsoft.VisualBasic.Strings?displayProperty=fullName>|  
|<xref:Microsoft.VisualBasic.CompilerServices.Conversions?displayProperty=fullName>|  
|<xref:Microsoft.VisualBasic.CompilerServices.DesignerGeneratedAttribute?displayProperty=fullName>|  
|<xref:Microsoft.VisualBasic.CompilerServices.IncompleteInitialization?displayProperty=fullName>|  
|<xref:Microsoft.VisualBasic.CompilerServices.NewLateBinding?displayProperty=fullName>|  
|<xref:Microsoft.VisualBasic.CompilerServices.ObjectFlowControl?displayProperty=fullName>|  
|<xref:Microsoft.VisualBasic.CompilerServices.ObjectFlowControl.ForLoopControl?displayProperty=fullName>|  
|<xref:Microsoft.VisualBasic.CompilerServices.Operators?displayProperty=fullName>|  
|<xref:Microsoft.VisualBasic.CompilerServices.OptionCompareAttribute?displayProperty=fullName>|  
|<xref:Microsoft.VisualBasic.CompilerServices.OptionTextAttribute?displayProperty=fullName>|  
|<xref:Microsoft.VisualBasic.CompilerServices.ProjectData?displayProperty=fullName>|  
|<xref:Microsoft.VisualBasic.CompilerServices.StandardModuleAttribute?displayProperty=fullName>|  
|<xref:Microsoft.VisualBasic.CompilerServices.StaticLocalInitFlag?displayProperty=fullName>|  
|<xref:Microsoft.VisualBasic.CompilerServices.Utils?displayProperty=fullName>|  
  
 **Contesto Reflection \(spazio dei nomi System.Reflection.Context\)**  
  
 La classe <xref:System.Reflection.Context.CustomReflectionContext?displayProperty=fullName> non è supportata in [!INCLUDE[net_native](../../../includes/net-native-md.md)].  
  
 **RTC \(System.Net.Http.Rtc\)**  
  
 La classe <xref:System.Net.Http.RtcRequestFactory?displayProperty=fullName> non è supportata in [!INCLUDE[net_native](../../../includes/net-native-md.md)].  
  
 **Windows Communication Foundation \(WCF\) \(System.ServiceModel.\*\)**  
  
 I tipi negli [spazi dei nomi System.ServiceModel.\*](http://msdn.microsoft.com/library/gg145010.aspx) non sono supportati in [!INCLUDE[net_native](../../../includes/net-native-md.md)]. Sono inclusi i tipi seguenti:  
  
||  
|-|  
|<xref:System.ServiceModel.ActionNotSupportedException?displayProperty=fullName>|  
|<xref:System.ServiceModel.BasicHttpBinding?displayProperty=fullName>|  
|<xref:System.ServiceModel.BasicHttpMessageCredentialType?displayProperty=fullName>|  
|<xref:System.ServiceModel.BasicHttpSecurity?displayProperty=fullName>|  
|<xref:System.ServiceModel.BasicHttpSecurityMode?displayProperty=fullName>|  
|<xref:System.ServiceModel.CallbackBehaviorAttribute?displayProperty=fullName>|  
|<xref:System.ServiceModel.ChannelFactory?displayProperty=fullName>|  
|<xref:System.ServiceModel.ChannelFactory%601?displayProperty=fullName>|  
|<xref:System.ServiceModel.ClientBase%601?displayProperty=fullName>|  
|<xref:System.ServiceModel.ClientBase%601.BeginOperationDelegate?displayProperty=fullName>|  
|<xref:System.ServiceModel.ClientBase%601.ChannelBase%601?displayProperty=fullName>|  
|<xref:System.ServiceModel.ClientBase%601.EndOperationDelegate?displayProperty=fullName>|  
|<xref:System.ServiceModel.ClientBase%601.InvokeAsyncCompletedEventArgs?displayProperty=fullName>|  
|<xref:System.ServiceModel.CommunicationException?displayProperty=fullName>|  
|<xref:System.ServiceModel.CommunicationObjectAbortedException?displayProperty=fullName>|  
|<xref:System.ServiceModel.CommunicationObjectFaultedException?displayProperty=fullName>|  
|<xref:System.ServiceModel.CommunicationState?displayProperty=fullName>|  
|<xref:System.ServiceModel.DataContractFormatAttribute?displayProperty=fullName>|  
|<xref:System.ServiceModel.DnsEndpointIdentity?displayProperty=fullName>|  
|<xref:System.ServiceModel.DuplexChannelFactory%601?displayProperty=fullName>|  
|<xref:System.ServiceModel.DuplexClientBase%601?displayProperty=fullName>|  
|<xref:System.ServiceModel.EndpointAddress?displayProperty=fullName>|  
|<xref:System.ServiceModel.EndpointAddressBuilder?displayProperty=fullName>|  
|<xref:System.ServiceModel.EndpointIdentity?displayProperty=fullName>|  
|<xref:System.ServiceModel.EndpointNotFoundException?displayProperty=fullName>|  
|<xref:System.ServiceModel.EnvelopeVersion?displayProperty=fullName>|  
|<xref:System.ServiceModel.ExceptionDetail?displayProperty=fullName>|  
|<xref:System.ServiceModel.FaultCode?displayProperty=fullName>|  
|<xref:System.ServiceModel.FaultContractAttribute?displayProperty=fullName>|  
|<xref:System.ServiceModel.FaultException?displayProperty=fullName>|  
|<xref:System.ServiceModel.FaultException%601?displayProperty=fullName>|  
|<xref:System.ServiceModel.FaultReason?displayProperty=fullName>|  
|<xref:System.ServiceModel.FaultReasonText?displayProperty=fullName>|  
|<xref:System.ServiceModel.HttpBindingBase?displayProperty=fullName>|  
|<xref:System.ServiceModel.HttpClientCredentialType?displayProperty=fullName>|  
|<xref:System.ServiceModel.HttpTransportSecurity?displayProperty=fullName>|  
|<xref:System.ServiceModel.IClientChannel?displayProperty=fullName>|  
|<xref:System.ServiceModel.ICommunicationObject?displayProperty=fullName>|  
|<xref:System.ServiceModel.IContextChannel?displayProperty=fullName>|  
|<xref:System.ServiceModel.IDefaultCommunicationTimeouts?displayProperty=fullName>|  
|<xref:System.ServiceModel.IExtensibleObject%601?displayProperty=fullName>|  
|<xref:System.ServiceModel.IExtension%601?displayProperty=fullName>|  
|<xref:System.ServiceModel.IExtensionCollection%601?displayProperty=fullName>|  
|<xref:System.ServiceModel.InstanceContext?displayProperty=fullName>|  
|<xref:System.ServiceModel.InvalidMessageContractException?displayProperty=fullName>|  
|<xref:System.ServiceModel.MessageBodyMemberAttribute?displayProperty=fullName>|  
|<xref:System.ServiceModel.MessageContractAttribute?displayProperty=fullName>|  
|<xref:System.ServiceModel.MessageContractMemberAttribute?displayProperty=fullName>|  
|<xref:System.ServiceModel.MessageCredentialType?displayProperty=fullName>|  
|<xref:System.ServiceModel.MessageHeader%601?displayProperty=fullName>|  
|<xref:System.ServiceModel.MessageHeaderException?displayProperty=fullName>|  
|<xref:System.ServiceModel.MessageParameterAttribute?displayProperty=fullName>|  
|<xref:System.ServiceModel.MessageSecurityOverTcp?displayProperty=fullName>|  
|<xref:System.ServiceModel.MessageSecurityVersion?displayProperty=fullName>|  
|<xref:System.ServiceModel.NetHttpBinding?displayProperty=fullName>|  
|<xref:System.ServiceModel.NetHttpMessageEncoding?displayProperty=fullName>|  
|<xref:System.ServiceModel.NetTcpBinding?displayProperty=fullName>|  
|<xref:System.ServiceModel.NetTcpSecurity?displayProperty=fullName>|  
|<xref:System.ServiceModel.OperationContext?displayProperty=fullName>|  
|<xref:System.ServiceModel.OperationContextScope?displayProperty=fullName>|  
|<xref:System.ServiceModel.OperationContractAttribute?displayProperty=fullName>|  
|<xref:System.ServiceModel.OperationFormatStyle?displayProperty=fullName>|  
|<xref:System.ServiceModel.ProtocolException?displayProperty=fullName>|  
|<xref:System.ServiceModel.QuotaExceededException?displayProperty=fullName>|  
|<xref:System.ServiceModel.SecurityMode?displayProperty=fullName>|  
|<xref:System.ServiceModel.ServerTooBusyException?displayProperty=fullName>|  
|<xref:System.ServiceModel.ServiceActivationException?displayProperty=fullName>|  
|<xref:System.ServiceModel.ServiceContractAttribute?displayProperty=fullName>|  
|<xref:System.ServiceModel.ServiceKnownTypeAttribute?displayProperty=fullName>|  
|<xref:System.ServiceModel.SpnEndpointIdentity?displayProperty=fullName>|  
|<xref:System.ServiceModel.TcpClientCredentialType?displayProperty=fullName>|  
|<xref:System.ServiceModel.TcpTransportSecurity?displayProperty=fullName>|  
|<xref:System.ServiceModel.TransferMode?displayProperty=fullName>|  
|<xref:System.ServiceModel.UnknownMessageReceivedEventArgs?displayProperty=fullName>|  
|<xref:System.ServiceModel.UpnEndpointIdentity?displayProperty=fullName>|  
|<xref:System.ServiceModel.XmlSerializerFormatAttribute?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.AddressHeader?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.AddressHeaderCollection?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.AddressingVersion?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.BinaryMessageEncodingBindingElement?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.ChannelManagerBase?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.ChannelParameterCollection?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.CommunicationObject?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.CompressionFormat?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.ConnectionOrientedTransportBindingElement?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.CustomBinding?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.FaultConverter?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.HttpRequestMessageProperty?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.HttpResponseMessageProperty?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.HttpsTransportBindingElement?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.HttpTransportBindingElement?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.IChannel?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.IChannelFactory?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.IChannelFactory%601?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.IDuplexChannel?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.IDuplexSession?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.IDuplexSessionChannel?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.IHttpCookieContainerManager?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.IInputChannel?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.IInputSession?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.IInputSessionChannel?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.IMessageProperty?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.IOutputChannel?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.IOutputSession?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.IOutputSessionChannel?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.IRequestChannel?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.IRequestSessionChannel?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.ISession?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.ISessionChannel%601?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.LocalClientSecuritySettings?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.Message?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.MessageBuffer?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.MessageEncoder?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.MessageEncoderFactory?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.MessageEncodingBindingElement?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.MessageFault?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.MessageHeader?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.MessageHeaderInfo?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.MessageHeaders?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.MessageProperties?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.MessageState?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.MessageVersion?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.RequestContext?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.SecurityBindingElement?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.SecurityHeaderLayout?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.SslStreamSecurityBindingElement?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.TcpConnectionPoolSettings?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.TcpTransportBindingElement?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.TextMessageEncodingBindingElement?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.TransportBindingElement?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.TransportSecurityBindingElement?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.WebSocketTransportSettings?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.WebSocketTransportUsage?displayProperty=fullName>|  
|<xref:System.ServiceModel.Channels.WindowsStreamSecurityBindingElement?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.ClientCredentials?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.ContractDescription?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.DataContractSerializerOperationBehavior?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.FaultDescription?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.FaultDescriptionCollection?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.IContractBehavior?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.IEndpointBehavior?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.IOperationBehavior?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.MessageBodyDescription?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.MessageDescription?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.MessageDescriptionCollection?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.MessageDirection?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.MessageHeaderDescription?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.MessageHeaderDescriptionCollection?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.MessagePartDescription?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.MessagePartDescriptionCollection?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.MessagePropertyDescription?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.MessagePropertyDescriptionCollection?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.OperationDescription?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.OperationDescriptionCollection?displayProperty=fullName>|  
|<xref:System.ServiceModel.Description.ServiceEndpoint?displayProperty=fullName>|  
|<xref:System.ServiceModel.Dispatcher.ClientOperation?displayProperty=fullName>|  
|<xref:System.ServiceModel.Dispatcher.ClientRuntime?displayProperty=fullName>|  
|<xref:System.ServiceModel.Dispatcher.DispatchOperation?displayProperty=fullName>|  
|<xref:System.ServiceModel.Dispatcher.DispatchRuntime?displayProperty=fullName>|  
|<xref:System.ServiceModel.Dispatcher.EndpointDispatcher?displayProperty=fullName>|  
|<xref:System.ServiceModel.Dispatcher.IClientMessageFormatter?displayProperty=fullName>|  
|<xref:System.ServiceModel.Dispatcher.IClientMessageInspector?displayProperty=fullName>|  
|<xref:System.ServiceModel.Dispatcher.IClientOperationSelector?displayProperty=fullName>|  
|<xref:System.ServiceModel.Dispatcher.IParameterInspector?displayProperty=fullName>|  
|<xref:System.ServiceModel.Security.BasicSecurityProfileVersion?displayProperty=fullName>|  
|<xref:System.ServiceModel.Security.HttpDigestClientCredential?displayProperty=fullName>|  
|<xref:System.ServiceModel.Security.MessageSecurityException?displayProperty=fullName>|  
|<xref:System.ServiceModel.Security.SecureConversationVersion?displayProperty=fullName>|  
|<xref:System.ServiceModel.Security.SecurityAccessDeniedException?displayProperty=fullName>|  
|<xref:System.ServiceModel.Security.SecurityPolicyVersion?displayProperty=fullName>|  
|<xref:System.ServiceModel.Security.SecurityVersion?displayProperty=fullName>|  
|<xref:System.ServiceModel.Security.TrustVersion?displayProperty=fullName>|  
|<xref:System.ServiceModel.Security.UserNamePasswordClientCredential?displayProperty=fullName>|  
|<xref:System.ServiceModel.Security.WindowsClientCredential?displayProperty=fullName>|  
|<xref:System.ServiceModel.Security.Tokens.SecureConversationSecurityTokenParameters?displayProperty=fullName>|  
|<xref:System.ServiceModel.Security.Tokens.SecurityTokenParameters?displayProperty=fullName>|  
|<xref:System.ServiceModel.Security.Tokens.SupportingTokenParameters?displayProperty=fullName>|  
|<xref:System.ServiceModel.Security.Tokens.UserNameSecurityTokenParameters?displayProperty=fullName>|  
  
### Differenze nei serializzatori  
 Le differenze riportate di seguito riguardano la serializzazione e la deserializzazione con le classi <xref:System.Runtime.Serialization.DataContractSerializer>, <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> e <xref:System.Xml.Serialization.XmlSerializer>:  
  
-   In [!INCLUDE[net_native](../../../includes/net-native-md.md)], <xref:System.Runtime.Serialization.DataContractSerializer> e <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> non riescono a serializzare o deserializzare una classe derivata che ha un membro della classe di base il cui tipo non è un tipo di serializzazione radice. Ad esempio, nel codice seguente, il tentativo di serializzare o deserializzare `Y` genererà un errore:  
  
     [!code-csharp[ProjectN#10](../../../samples/snippets/csharp/VS_Snippets_CLR/projectn/cs/compat3.cs#10)]  
  
     Il tipo `InnerType` non è noto al serializzatore, perché i membri della classe base non vengono attraversati durante la serializzazione.  
  
-   <xref:System.Runtime.Serialization.DataContractSerializer> e <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> non riescono a serializzare una classe o una struttura che implementa l'interfaccia <xref:System.Collections.Generic.IEnumerable%601>. Ad esempio, i seguenti tipi non riesco a serializzare o deserializzare:  
  
  
  
-   <xref:System.Xml.Serialization.XmlSerializer> non riesce a serializzare il valore dell'oggetto seguente, perché non conoscere il tipo esatto dell'oggetto da serializzare:  
  
  
  
-   <xref:System.Xml.Serialization.XmlSerializer> non riesce a serializzare o deserializzare se il tipo di oggetto serializzato è <xref:System.Xml.XmlQualifiedName>.  
  
-   Tutti i serializzatori \(<xref:System.Runtime.Serialization.DataContractSerializer>, <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer> e <xref:System.Xml.Serialization.XmlSerializer>\) non riescono a generare un codice di serializzazione per il tipo <xref:System.Xml.Linq.XElement?displayProperty=fullName> o per un tipo che contiene <xref:System.Xml.Linq.XElement>, visualizzando invece gli errori in fase di compilazione.  
  
-   Il funzionamento corretto dei seguenti costruttori dei tipi di serializzazione non è garantito:  
  
    -   <xref:System.Runtime.Serialization.DataContractSerializer.%23ctor%28System.Type%2CSystem.Collections.Generic.IEnumerable%7BSystem.Type%7D%29?displayProperty=fullName>  
  
    -   <xref:System.Runtime.Serialization.DataContractSerializer.%23ctor%28System.Type%2CSystem.Runtime.Serialization.DataContractSerializerSettings%29?displayProperty=fullName>  
  
    -   <xref:System.Runtime.Serialization.DataContractSerializer.%23ctor%28System.Type%2CSystem.String%2CSystem.String%2CSystem.Collections.Generic.IEnumerable%7BSystem.Type%7D%29?displayProperty=fullName>  
  
    -   <xref:System.Runtime.Serialization.DataContractSerializer.%23ctor%28System.Type%2CSystem.Xml.XmlDictionaryString%2CSystem.Xml.XmlDictionaryString%2CSystem.Collections.Generic.IEnumerable%7BSystem.Type%7D%29?displayProperty=fullName>  
  
    -   <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.%23ctor%28System.Type%2CSystem.Runtime.Serialization.Json.DataContractJsonSerializerSettings%29?displayProperty=fullName>  
  
    -   <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer.%23ctor%28System.Type%2CSystem.Collections.Generic.IEnumerable%7BSystem.Type%7D%29?displayProperty=fullName>  
  
    -   <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Type%2CSystem.String%29?displayProperty=fullName>  
  
    -   [XmlSerializer.XmlSerializer\(Type, Type\<xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Type%2CSystem.Type%5B%5D%29?displayProperty=fullName>  
  
    -   <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Type%2CSystem.Xml.Serialization.XmlAttributeOverrides%29?displayProperty=fullName>  
  
    -   <xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Type%2CSystem.Xml.Serialization.XmlRootAttribute%29?displayProperty=fullName>  
  
    -   [XmlSerializer.XmlSerializer\(Type, XmlAttributeOverrides, Type\<xref:System.Xml.Serialization.XmlSerializer.%23ctor%28System.Type%2CSystem.Xml.Serialization.XmlAttributeOverrides%2CSystem.Type%5B%5D%2CSystem.Xml.Serialization.XmlRootAttribute%2CSystem.String%29?displayProperty=fullName>  
  
-   <xref:System.Xml.Serialization.XmlSerializer> non riesce a generare il codice per un tipo che ha metodi con uno qualsiasi dei seguenti attributi:  
  
    -   <xref:System.Runtime.Serialization.OnSerializingAttribute>  
  
    -   <xref:System.Runtime.Serialization.OnSerializedAttribute>  
  
    -   <xref:System.Runtime.Serialization.OnDeserializingAttribute>  
  
    -   <xref:System.Runtime.Serialization.OnDeserializedAttribute>  
  
-   <xref:System.Xml.Serialization.XmlSerializer> non soddisfa l'interfaccia di serializzazione personalizzata di <xref:System.Xml.Serialization.IXmlSerializable>. Se si ha una classe che implementa questa interfaccia, <xref:System.Xml.Serialization.XmlSerializer> considera il tipo come un oggetto Plain Old CLR Object \(POCO\) di CLR e ne serializza solo le proprietà pubbliche.  
  
-   La serializzazione di un oggetto <xref:System.Exception> POCO, come il seguente, non ha esito positivo con <xref:System.Runtime.Serialization.DataContractSerializer> e <xref:System.Runtime.Serialization.Json.DataContractJsonSerializer>:  
  
  
  
<a name="VS"></a>   
## Differenze di Visual Studio  
 **Eccezioni e debug**  
  
 Quando si eseguono applicazioni compilate usando [!INCLUDE[net_native](../../../includes/net-native-md.md)] nel debugger, vengono abilitate le eccezioni first\-chance per i seguenti tipi di eccezione:  
  
-   <xref:System.MemberAccessException>  
  
-   <xref:System.TypeAccessException>  
  
 **Creazione di applicazioni**  
  
 Usare gli strumenti di compilazione x86 usati per impostazione predefinita da Visual Studio. Non è consigliabile usare gli strumenti di MSBuild AMD64, disponibili in C:\\Program Files \(x86\)\\MSBuild\\12.0\\bin\\amd64, perché possono creare problemi di compilazione.  
  
 **Profiler**  
  
-   Il profiler della CPU di Visual Studio e il profiler della memoria XAML non visualizzano Just My Code correttamente.  
  
-   Il profiler della memoria di XAML non visualizza in modo accurato i dati di heap gestito.  
  
-   Il profiler della CPU non identifica correttamente i moduli e consente di visualizzare i nomi di funzione con prefisso.  
  
 **Progetti di librerie unit test**  
  
 L'abilitazione di [!INCLUDE[net_native](../../../includes/net-native-md.md)] su una libreria unit test per un progetto di app di Windows Store non è supportata e produce la mancata compilazione del progetto.  
  
## Vedere anche  
 [Introduzione](../../../docs/framework/net-native/getting-started-with-net-native.md)   
 [Riferimento a file di configurazione di direttive di runtime \(rd.xml\)](../../../docs/framework/net-native/runtime-directives-rd-xml-configuration-file-reference.md)   
 [Panoramica di .NET per applicazioni Windows Store](http://msdn.microsoft.com/library/windows/apps/br230302.aspx)   
 [Supporto .NET Framework per applicazioni Windows Store e Windows Runtime](../../../docs/standard/cross-platform/support-for-windows-store-apps-and-windows-runtime.md)