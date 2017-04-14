---
title: "Procedure consigliate per il caricamento di assembly | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "assembly, associazione"
  - "assembly, caricamento"
  - "errori di caricamento assembly"
  - "contesto di caricamento predefinito"
  - "contesti di caricamento"
  - "contesto di origine del caricamento"
  - "LoadFrom (metodo)"
  - "LoadWithPartialName (metodo)"
  - "TypeLoadException (classe), cause"
ms.assetid: 68d1c539-6a47-4614-ab59-4b071c9d4b4c
caps.latest.revision: 10
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 10
---
# Procedure consigliate per il caricamento di assembly
In questo articolo viene illustrato come evitare problemi di identità del tipo che possono causare l'eccezione <xref:System.InvalidCastException> o <xref:System.MissingMethodException> e altri errori.  Nell'articolo vengono discussi i seguenti suggerimenti:  
  
-   [Comprendere i vantaggi e gli svantaggi dei contesti di caricamento](#load_contexts)  
  
-   [Evitare l'associazione di nomi di assembly parziali](#avoid_partial_names)  
  
-   [Evitare il caricamento di un assembly in più contesti](#avoid_loading_into_multiple_contexts)  
  
-   [Evitare il caricamento di più versioni di un assembly nello stesso contesto](#avoid_loading_multiple_versions)  
  
-   [Considerare il passaggio al contesto di caricamento predefinito](#switch_to_default)  
  
 Nel primo suggerimento, [comprendere i vantaggi e gli svantaggi dei contesti di caricamento](#load_contexts), vengono fornite informazioni complementari per gli altri suggerimenti, in quanto tutti dipendono da una conoscenza dei contesti di caricamento.  
  
<a name="load_contexts"></a>   
## Comprendere i vantaggi e gli svantaggi dei contesti di caricamento  
 All'interno di un dominio applicazione è possibile caricare gli assembly in tre contesti diversi, oppure senza contesto:  
  
-   Il contesto di caricamento predefinito contiene gli assembly rilevati tramite sondaggio della Global Assembly Cache, l'archivio di assembly su host se il runtime è ospitato \(ad esempio in SQL Server\) e le proprietà <xref:System.AppDomainSetup.ApplicationBase%2A> e <xref:System.AppDomainSetup.PrivateBinPath%2A> del dominio applicazione.  La maggior parte degli overload del metodo <xref:System.Reflection.Assembly.Load%2A> caricano gli assembly in questo contesto.  
  
-   Il contesto di origine del caricamento contiene gli assembly caricati da percorsi nei quali il caricatore non esegue ricerche.  Ad esempio, i componenti aggiuntivi potrebbero essere installati in una directory che non si trova nel percorso dell'applicazione.  <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=fullName>, <xref:System.AppDomain.CreateInstanceFrom%2A?displayProperty=fullName> e <xref:System.AppDomain.ExecuteAssembly%2A?displayProperty=fullName> sono esempi di metodi che vengono caricati tramite il percorso.  
  
-   Il contesto ReflectionOnly contiene gli assembly caricati con i metodi <xref:System.Reflection.Assembly.ReflectionOnlyLoad%2A> e <xref:System.Reflection.Assembly.ReflectionOnlyLoadFrom%2A>.  Il codice in questo contesto non può essere eseguito, pertanto non viene discusso qui.  Per ulteriori informazioni, vedere [How to: Load Assemblies into the Reflection\-Only Context](../../../docs/framework/reflection-and-codedom/how-to-load-assemblies-into-the-reflection-only-context.md).  
  
-   Se un assembly dinamico temporaneo è stato generato tramite reflection emit, non si trova in nessun contesto.  Inoltre, la maggior parte degli assembly caricati tramite il metodo <xref:System.Reflection.Assembly.LoadFile%2A> vengono caricati senza contesto, mentre gli assembly caricati da matrici di byte vengono caricati senza contesto a meno che l'identità, dopo l'applicazione dei criteri, non stabilisca che si trovano nella Global Assembly Cache.  
  
 I contesti di esecuzione presentano vantaggi e svantaggi, come illustrato nelle sezioni seguenti.  
  
### Contesto di caricamento predefinito  
 Quando gli assembly vengono caricati nel contesto di caricamento predefinito, le relative dipendenze vengono caricate automaticamente.  Le dipendenze caricate nel contesto di caricamento predefinito vengono rilevate automaticamente per gli assembly che si trovano in tale contesto o nel contesto di origine del caricamento.  Il caricamento tramite identità dell'assembly aumenta la stabilità delle applicazioni assicurando che non vengano utilizzate versioni sconosciute degli assembly \(vedere la sezione [Evitare l'associazione di nomi di assembly parziali](#avoid_partial_names)\).  
  
 L'utilizzo del contesto di caricamento predefinito presenta i seguenti svantaggi:  
  
-   Le dipendenze caricate in altri contesti non sono disponibili.  
  
-   Non è possibile caricare assembly da percorsi esterni al percorso di sondaggio nel contesto di caricamento predefinito.  
  
### Contesto di origine del caricamento  
 Il contesto di origine del caricamento consente di caricare un assembly da un percorso al di fuori del percorso dell'applicazione, pertanto non incluso nel sondaggio.  Consente di individuare e caricare le dipendenze da quel percorso, poiché le informazioni sul percorso vengono gestite dal contesto.  Inoltre, gli assembly in questo contesto possono utilizzare le dipendenze caricate nel contesto di caricamento predefinito.  
  
 Il caricamento di assembly tramite il metodo <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=fullName>, o uno degli altri metodi che caricano tramite percorso, presenta i seguenti svantaggi:  
  
-   Se è stato già caricato un assembly con la stessa identità, <xref:System.Reflection.Assembly.LoadFrom%2A> restituisce l'assembly caricato, anche se è stato specificato un percorso diverso.  
  
-   Se un assembly viene caricato con <xref:System.Reflection.Assembly.LoadFrom%2A> e successivamente un assembly nel contesto di caricamento predefinito tenta di caricare lo stesso assembly tramite il nome visualizzato, il tentativo di caricamento fallisce.  Questo caso si può verificare quando un assembly viene deserializzato.  
  
-   Se un assembly viene caricato con <xref:System.Reflection.Assembly.LoadFrom%2A> e il percorso di sondaggio include un assembly con la stessa identità ma situato in un percorso diverso, è possibile che si verifichi un'eccezione <xref:System.InvalidCastException>, <xref:System.MissingMethodException> o un altro comportamento imprevisto.  
  
-   <xref:System.Reflection.Assembly.LoadFrom%2A> richiede <xref:System.Security.Permissions.FileIOPermissionAccess?displayProperty=fullName> e <xref:System.Security.Permissions.FileIOPermissionAccess?displayProperty=fullName> oppure <xref:System.Net.WebPermission>, sul percorso specificato.  
  
-   Se esiste un'immagine nativa per l'assembly, questa non viene utilizzata.  
  
-   L'assembly non può essere caricato come modulo indipendente dal dominio.  
  
-   Nelle versioni 1.0 e 1.1 di .NET Framework i criteri non vengono applicati.  
  
### Nessun contesto  
 Il caricamento senza contesto è l'unica opzione possibile per gli assembly temporanei generati con reflection emit.  Questo tipo di caricamento rappresenta il solo metodo per caricare più assembly con la stessa identità in un unico dominio applicazione  ed evita il rischio di un sondaggio.  
  
 Gli assembly caricati da matrici di byte vengono caricati senza contesto a meno che l'identità dell'assembly, stabilita quando vengono applicati i criteri, non corrisponda all'identità di un assembly situato nella Global Assembly Cache; in tal caso, l'assembly viene caricato dalla Global Assembly Cache.  
  
 Il caricamento di assembly senza contesto presenta i seguenti svantaggi:  
  
-   Gli altri assembly non possono essere associati agli assembly caricati senza contesto, a meno che non si gestisca l'evento <xref:System.AppDomain.AssemblyResolve?displayProperty=fullName>.  
  
-   Le dipendenze non vengono caricate automaticamente.  È possibile precaricarle senza contesto, precaricarle nel contesto di caricamento predefinito oppure caricarle tramite gestione dell'evento <xref:System.AppDomain.AssemblyResolve?displayProperty=fullName>.  
  
-   Il caricamento di più assembly con la stessa identità senza contesto può causare problemi di identità del tipo simili a quelli causati dal caricamento di assembly con la stessa identità in più contesti.  Vedere [Evitare il caricamento di un assembly in più contesti](#avoid_loading_into_multiple_contexts).  
  
-   Se esiste un'immagine nativa per l'assembly, questa non viene utilizzata.  
  
-   L'assembly non può essere caricato come modulo indipendente dal dominio.  
  
-   Nelle versioni 1.0 e 1.1 di .NET Framework i criteri non vengono applicati.  
  
<a name="avoid_partial_names"></a>   
## Evitare l'associazione di nomi di assembly parziali  
 L'associazione di un nome parziale si ha quando, durante il caricamento di un assembly, si specifica solo parte del nome visualizzato dell'assembly \(<xref:System.Reflection.Assembly.FullName%2A>\).  Ad esempio, è possibile chiamare il metodo <xref:System.Reflection.Assembly.Load%2A?displayProperty=fullName> con il solo nome semplice dell'assembly, omettendo la versione, le impostazioni cultura e il token di chiave pubblica.  Oppure è possibile chiamare il metodo <xref:System.Reflection.Assembly.LoadWithPartialName%2A?displayProperty=fullName>, il quale prima chiama il metodo <xref:System.Reflection.Assembly.Load%2A?displayProperty=fullName> e, se questo non riesce a individuare l'assembly, esegue ricerche nella Global Assembly Cache e carica la versione disponibile più recente dell'assembly.  
  
 L'associazione di nomi parziali può causare molti problemi, tra cui i seguenti:  
  
-   Il metodo <xref:System.Reflection.Assembly.LoadWithPartialName%2A?displayProperty=fullName> potrebbe caricare un assembly diverso con lo stesso nome semplice.  Ad esempio, due applicazioni potrebbero installare due assembly completamente diversi, entrambi con il nome semplice `GraphicsLibrary`, nella Global Assembly Cache.  
  
-   L'assembly realmente caricato potrebbe non essere compatibile con le versioni precedenti.  Ad esempio, il fatto di non specificare la versione potrebbe comportare il caricamento di una versione di molto successiva rispetto alla versione che il programma doveva originariamente utilizzare.  Le modifiche apportate nella versione successiva potrebbero causare errori nell'applicazione.  
  
-   L'assembly realmente caricato potrebbe non essere compatibile con le versioni successive.  Ad esempio, l'applicazione potrebbe essere stata compilata e testata con la versione più recente di un assembly, ma l'associazione parziale potrebbe caricare una versione di molto precedente in cui mancano le funzionalità utilizzate dall'applicazione.  
  
-   L'installazione di nuove applicazioni può provocare l'interruzione delle applicazioni esistenti.  È possibile che un'applicazione che utilizza il metodo <xref:System.Reflection.Assembly.LoadWithPartialName%2A> venga interrotta in seguito all'installazione di una versione più recente e incompatibile di un assembly condiviso.  
  
-   Può verificarsi un caricamento di dipendenze imprevisto.  Se si caricano due assembly che condividono una dipendenza, il caricamento con associazione parziale potrebbe provocare l'utilizzo, da parte di uno degli assembly, di un componente con il quale non è stato compilato né testato.  
  
 Considerati i problemi che può causare, il metodo <xref:System.Reflection.Assembly.LoadWithPartialName%2A> è stato contrassegnato come obsoleto.  Per contro, si consiglia di utilizzare il metodo <xref:System.Reflection.Assembly.Load%2A?displayProperty=fullName> e di specificare i nomi visualizzati degli assembly completi.  Vedere [Comprendere i vantaggi e gli svantaggi dei contesti di caricamento](#load_contexts) e [Considerare il passaggio al contesto di caricamento predefinito](#switch_to_default).  
  
 Se si desidera utilizzare il metodo <xref:System.Reflection.Assembly.LoadWithPartialName%2A> poiché facilita il caricamento degli assembly, considerare che un eventuale esito negativo dell'applicazione con un messaggio di errore che identifica l'assembly mancante fornisce probabilmente un'esperienza utente migliore rispetto all'utilizzo automatico di una versione sconosciuta dell'assembly, che potrebbe provocare un comportamento imprevedibile e problemi di sicurezza.  
  
<a name="avoid_loading_into_multiple_contexts"></a>   
## Evitare il caricamento di un assembly in più contesti  
 Il caricamento di un assembly in più contesti può causare problemi di identità del tipo.  Il fatto che lo stesso tipo venga caricato dallo stesso assembly in due contesti diversi equivale al caricamento di due tipi diversi con lo stesso nome.  Se si tenta di eseguire il cast di un tipo all'altro tipo, viene generata un'eccezione <xref:System.InvalidCastException> con un messaggio ambiguo che indica l'impossibilità di eseguire il cast del tipo `MyType` al tipo `MyType`.  
  
 Si supponga ad esempio che l'interfaccia `ICommunicate` viene dichiarata in un assembly denominato `Utility`, al quale fanno riferimento il programma e anche altri assembly caricati dal programma.  Gli altri assembly contengono tipi che implementano l'interfaccia `ICommunicate`, consentendo al programma di utilizzarli.  
  
 Si consideri ora cosa accade quando viene eseguito il programma.  Gli assembly ai quali fa riferimento il programma vengono caricati nel contesto di caricamento predefinito.  Se si carica un assembly di destinazione tramite identità, utilizzando il metodo <xref:System.Reflection.Assembly.Load%2A>, questo sarà collocato nel contesto di caricamento predefinito insieme alle relative dipendenze.  Sia il programma sia l'assembly di destinazione utilizzeranno lo stesso assembly `Utility`.  
  
 Tuttavia, si supponga di caricare l'assembly di destinazione tramite percorso del file, utilizzando il metodo <xref:System.Reflection.Assembly.LoadFile%2A>.  L'assembly viene caricato senza contesto, pertanto le relative dipendenze non vengono caricate automaticamente.  Si potrebbe disporre di un gestore affinché l'evento <xref:System.AppDomain.AssemblyResolve?displayProperty=fullName> fornisca la dipendenza, e questo potrebbe caricare l'assembly `Utility` senza contesto utilizzando il metodo <xref:System.Reflection.Assembly.LoadFile%2A>.  Ora, quando si crea un'istanza di un tipo contenuto nell'assembly di destinazione e si tenta di assegnarla a una variabile di tipo `ICommunicate`, viene generata un'eccezione <xref:System.InvalidCastException> poiché il runtime considera le interfacce `ICommunicate` nelle due copie dell'assembly `Utility` come tipi diversi.  
  
 Esistono molti altri scenari nei quali un assembly può essere caricato in più contesti.  Il migliore approccio consiste nell'evitare conflitti ricollocando l'assembly di destinazione nel percorso dell'applicazione e utilizzando il metodo <xref:System.Reflection.Assembly.Load%2A> con il nome visualizzato completo.  L'assembly viene quindi caricato nel contesto di caricamento predefinito ed entrambi gli assembly utilizzano lo stesso assembly `Utility`.  
  
 Se l'assembly di destinazione deve rimanere al di fuori del percorso dell'applicazione, è possibile utilizzare il metodo <xref:System.Reflection.Assembly.LoadFrom%2A> per caricarlo nel contesto di origine del caricamento.  Se l'assembly di destinazione è stato compilato con un riferimento all'assembly `Utility` dell'applicazione, esso utilizzerà l'assembly `Utility` caricato dall'applicazione nel contesto di caricamento predefinito.  Possono verificarsi problemi nel caso in cui l'assembly di destinazione dipenda da una copia dell'assembly `Utility` situata al di fuori del percorso dell'applicazione.  Se tale assembly viene caricato nel contesto di origine del caricamento prima che l'applicazione carichi l'assembly `Utility`, il caricamento dell'applicazione avrà esito negativo.  
  
 Nella sezione [Considerare il passaggio al contesto di caricamento predefinito](#switch_to_default) vengono illustrate le alternative all'utilizzo di caricamenti nel percorso del file, ad esempio <xref:System.Reflection.Assembly.LoadFile%2A> e <xref:System.Reflection.Assembly.LoadFrom%2A>.  
  
<a name="avoid_loading_multiple_versions"></a>   
## Evitare il caricamento di più versioni di un assembly nello stesso contesto  
 Il caricamento di più versioni di un assembly in un unico contesto può causare problemi di identità del tipo.  Il fatto che lo stesso tipo venga caricato da due versioni dello stesso assembly equivale al caricamento di due tipi diversi con lo stesso nome.  Se si tenta di eseguire il cast di un tipo all'altro tipo, viene generata un'eccezione <xref:System.InvalidCastException> con un messaggio ambiguo che indica l'impossibilità di eseguire il cast del tipo `MyType` al tipo `MyType`.  
  
 Ad esempio, il programma potrebbe caricare direttamente una versione dell'assembly `Utility` e successivamente caricare un altro assembly che carica una versione diversa dell'assembly `Utility`.  Oppure, in seguito a un errore di codifica, due percorsi di codice diversi nell'applicazione potrebbero caricare versioni diverse di un assembly.  
  
 Nel contesto di caricamento predefinito, questo problema può verificarsi quando si utilizza il metodo <xref:System.Reflection.Assembly.Load%2A?displayProperty=fullName> e si specificano nomi visualizzati degli assembly completi che includono numeri di versione diversi.  Nel caso degli assembly caricati senza contesto, il problema può verificarsi in seguito all'utilizzo del metodo <xref:System.Reflection.Assembly.LoadFile%2A?displayProperty=fullName> per caricare lo stesso assembly da percorsi diversi.  Il runtime considera due assembly caricati da percorsi diversi come assembly diversi, sebbene le identità siano uguali.  
  
 Oltre ai problemi di identità del tipo, più versioni di un assembly possono provocare un'eccezione <xref:System.MissingMethodException> nel caso in cui un tipo caricato da una versione dell'assembly venga passato a codice che si aspetta di ricevere il tipo da una versione diversa.  Ad esempio, il codice potrebbe aspettarsi un metodo aggiunto alla versione successiva.  
  
 Errori più insidiosi possono verificarsi se il comportamento del tipo è cambiato da una versione all'altra.  Ad esempio, un metodo potrebbe generare un'eccezione imprevista o restituire un valore imprevisto.  
  
 Esaminare attentamente il codice per accertare che sia stata caricata un'unica versione di un assembly.  È possibile utilizzare il metodo <xref:System.AppDomain.GetAssemblies%2A?displayProperty=fullName> per determinare quali assembly vengono caricati in un determinato momento.  
  
<a name="switch_to_default"></a>   
## Considerare il passaggio al contesto di caricamento predefinito  
 Si prendano in esame i modelli di caricamento e distribuzione degli assembly dell'applicazione.  È possibile eliminare gli assembly caricati da matrici di byte?  È possibile spostare gli assembly nel percorso di sondaggio?  Se gli assembly si trovano nella Global Assembly Cache o nel percorso di sondaggio del dominio applicazione \(vale a dire <xref:System.AppDomainSetup.ApplicationBase%2A> e <xref:System.AppDomainSetup.PrivateBinPath%2A>\), è possibile caricare l'assembly tramite l'identità.  
  
 Se non è possibile inserire tutti gli assembly nel percorso di sondaggio, considerare alternative quali l'utilizzo del modello del componente aggiuntivo di .NET Framework, l'inserimento degli assembly nella Global Assembly Cache o la creazione di domini applicazione.  
  
### Considerare l'utilizzo del modello del componente aggiuntivo di .NET Framework  
 Se si utilizza il contesto di origine del caricamento per implementare i componenti aggiuntivi, che in genere non vengono installati nella base dell'applicazione, utilizzare il modello del componente aggiuntivo di .NET Framework.  Questo modello fornisce l'isolamento a livello del dominio applicazione o del processo e non richiede alcuna gestione dei domini applicazione da parte dell'utente.  Per informazioni sul modello del componente aggiuntivo, vedere [Componenti aggiuntivi ed estensibilità](../../../ml/index.xml).  
  
### Considerare l'utilizzo della Global Assembly Cache  
 L'inserimento degli assembly nella Global Assembly Cache consente di sfruttare il vantaggio di un percorso dell'assembly condiviso al di fuori della base dell'applicazione, senza perdere i vantaggi del contesto di caricamento predefinito né avere gli svantaggi degli altri contesti.  
  
### Considerare l'utilizzo dei domini applicazione  
 Se si riscontra l'impossibilità di distribuire alcuni degli assembly nel percorso di sondaggio dell'applicazione, prendere in considerazione la creazione di un nuovo dominio applicazione per tali assembly.  Utilizzare un oggetto <xref:System.AppDomainSetup> per creare il nuovo dominio applicazione e la proprietà <xref:System.AppDomainSetup.ApplicationBase%2A?displayProperty=fullName> per specificare il percorso che contiene gli assembly da caricare.  Se si hanno più directory da sondare, è possibile impostare la proprietà <xref:System.AppDomainSetup.ApplicationBase%2A> su una directory radice e utilizzare la proprietà <xref:System.AppDomainSetup.PrivateBinPath%2A?displayProperty=fullName> per identificare le sottodirectory da sondare.  In alternativa, è possibile creare più domini applicazione e impostare la proprietà <xref:System.AppDomainSetup.ApplicationBase%2A> di ogni dominio sul percorso appropriato per gli assembly.  
  
 Per caricare questi assembly è possibile utilizzare il metodo <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=fullName>.  Dal momento che ora si trovano nel percorso di sondaggio, verranno caricati nel contesto di caricamento predefinito anziché nel contesto di origine del caricamento.  Tuttavia, si consiglia di passare al metodo <xref:System.Reflection.Assembly.Load%2A?displayProperty=fullName> e di fornire i nomi visualizzati degli assembly completi per assicurare che vengano sempre utilizzate versioni corrette.  
  
## Vedere anche  
 <xref:System.Reflection.Assembly.Load%2A?displayProperty=fullName>   
 <xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=fullName>   
 <xref:System.Reflection.Assembly.LoadFile%2A?displayProperty=fullName>   
 <xref:System.AppDomain.AssemblyResolve?displayProperty=fullName>   
 [Componenti aggiuntivi ed estensibilità](../../../ml/index.xml)