---
title: "Creazione del pacchetto e distribuzione delle risorse in applicazioni desktop | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-bcl"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "distribuzione di applicazioni [.NET Framework], risorse"
  - "file di risorse, distribuzione"
  - "distribuzione di risorse (modello hub e spoke)"
  - "file di risorse, creazione del pacchetto"
  - "risorse dell'applicazione, creazione del pacchetto"
  - "assembly di risorse singolo"
  - "assembly satellite"
  - "impostazioni cultura predefinite per le applicazioni"
  - "nomi [.NET Framework], risorse"
  - "processo fallback per le risorse"
  - "raggruppamento di impostazioni cultura"
  - "risorse dell'applicazione, distribuzione"
  - "risorse dell'applicazione, convenzioni di denominazione"
  - "impostazioni cultura, creazione del pacchetto e distribuzione delle risorse"
  - "file di risorse, convenzioni di denominazione"
  - "creazione di pacchetti di risorse dell'applicazione"
  - "risorse dell'applicazione, processi fallback"
  - "file di risorse, processi fallback"
  - "risorse (localizzazione)"
  - "impostazioni cultura neutre"
ms.assetid: b224d7c0-35f8-4e82-a705-dd76795e8d16
caps.latest.revision: 26
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 26
---
# Creazione del pacchetto e distribuzione delle risorse in applicazioni desktop
Le applicazioni si basano su .NET Framework Resource Manager, rappresentate dalla classe <xref:System.Resources.ResourceManager>, per recuperare le risorse localizzate.  Il Gestione Risorse presuppone che un modello hub e spoke sia utilizzato per assemblare e distribuire le risorse.  L'hub è l'assembly principale che contiene il codice eseguibile non localizzabile e le risorse relative a singole impostazioni cultura, denominate neutre o predefinite.  Le impostazioni di lingua predefinite sono le impostazioni di lingua di fallback dell'applicazione; se le risorse localizzate non vengono trovate, quest'ultima è la lingua utilizzata per le risorse.  Ciascuno spoke si collega a un assembly satellite che contiene le risorse relative a singole impostazioni cultura, ma non contiene codice.  
  
 Questo modello presenta diversi vantaggi:  
  
-   Una volta distribuita un'applicazione, sarà possibile aggiungere risorse per nuove impostazioni cultura in modo incrementale.  Poiché lo sviluppo successivo di risorse specifiche delle impostazioni cultura può richiedere molto tempo, questa soluzione consente di rilasciare l'applicazione principale e distribuire successivamente le risorse specifiche delle impostazioni cultura.  
  
-   È possibile aggiornare e modificare gli assembly satellite di un'applicazione senza ricompilare l'applicazione.  
  
-   L'applicazione può limitarsi a caricare solo gli assembly che contengono le risorse necessarie per particolari impostazioni cultura.  In tal modo è possibile ridurre notevolmente l'utilizzo delle risorse di sistema.  
  
 Questo modello presenta tuttavia anche alcuni svantaggi:  
  
-   È necessario gestire più insiemi di risorse.  
  
-   Il costo iniziale del test di un'applicazione aumenta, perché è necessario verificare diverse configurazioni.  Si osservi però che a lungo termine sarà più semplice e meno costoso eseguire il test di un'applicazione centrale con vari satelliti, piuttosto che verificare e gestire diverse versioni internazionali parallele.  
  
## Convenzioni di denominazione delle risorse  
 Quando si crea il package delle risorse dell'applicazione, è necessario denominarle utilizzando le convenzioni di denominazione delle risorse richieste da Common Language Runtime.  Il runtime identifica una risorsa in base al nome della lingua.  Alle diverse lingue è assegnato un nome univoco costituito solitamente da una sigla di due caratteri minuscoli che identifica una lingua e, se necessario, da una sigla di due caratteri maiuscoli che identifica un paese o un'area geografica specifica.  La seconda sigla è separata dalla prima tramite un trattino \(\-\).  Esempi validi includono ja\-JP per il giapponese, la lingua del Giappone, en\-US per l'inglese degli Stati Uniti, de\-DE per la lingua tedesca, o de\-AT per la lingua dell'Austria.  Vedere [Riferimenti per API nazionale \(NLS\) del supporto linguistico](http://go.microsoft.com/fwlink/?LinkId=200048) nel Centro per Sviluppatori Go Global per un elenco completo dei nomi delle impostazioni cultura.  
  
> [!NOTE]
>  Per informazioni sulla creazione dei file di risorse, vedere [Creazione di file di risorse](../../../docs/framework/resources/creating-resource-files-for-desktop-apps.md) e [Creazione di assembly satellite](../../../docs/framework/resources/creating-satellite-assemblies-for-desktop-apps.md) in MSDN Library.  
  
<a name="cpconpackagingdeployingresourcesanchor1"></a>   
## Il processo di fallback delle risorse  
 Nel modello hub e spoke per la creazione del package e la distribuzione delle risorse viene utilizzato un processo di fallback per l'individuazione delle risorse appropriate.  Se un'applicazione richiede una risorsa localizzata non disponibile, il runtime delle lingue comuni ricerca la gerarchia delle lingue per una risorsa di fallback appropriata che corrisponda il più possibile alla richiesta dell'applicazione, e lanci un'eccezione solo in ultima analisi.  A ciascun livello della gerarchia, se viene individuata una risorsa appropriata, questa viene utilizzata dal runtime.  In caso contrario, la ricerca continua al livello successivo.  
  
 Per migliorare le prestazioni di ricerca, applicare l'attributo <xref:System.Resources.NeutralResourcesLanguageAttribute> all'assembly principale, passandogli il nome della lingua non associata ad alcuna impostazione cultura adatta all'assembly principale.  
  
> [!TIP]
>  È possibile utilizzare l'elemento di configurazione [\<relativeBindForResources\>](../../../docs/framework/configure-apps/file-schema/runtime/relativebindforresources-element.md) per ottimizzare il processo di fallback delle risorse e il processo con cui il runtime esegue la ricerca degli assembly di risorse.  Per ulteriori informazioni, vedere la sezione [Ottimizzare il processo di fallback delle risorse](../../../docs/framework/resources/packaging-and-deploying-resources-in-desktop-apps.md#Optimizing).  
  
 Il processo di fallback delle risorse viene descritto nei passaggi riportati di seguito.  
  
1.  Il runtime esegue la ricerca nella [Global Assembly Cache](../../../docs/framework/app-domains/gac.md) di un assembly che corrisponde alle impostazioni di lingua richieste dall'applicazione.  
  
     La Global Assembly Cache può memorizzare assembly di risorse condivisi da più applicazioni.  In tal modo non è necessario includere set di risorse specifici nella struttura di directory di ogni applicazione creata.  Se il runtime trova un riferimento all'assembly, cerca nell'assembly la risorsa richiesta.  Se trova la voce nell'assembly, utilizza la risorsa.  Se non trova la voce, continua la ricerca.  
  
2.  Il runtime cerca quindi nella directory dell'assembly in esecuzione una directory che corrisponda alla lingua richiesta.  Se la trova, vi cerca un assembly satellite valido per le impostazioni cultura richieste.  Il runtime cerca quindi nell'assembly satellite la risorsa richiesta.  Se trova la risorsa, la utilizza.  Se non trova la risorsa, continua la ricerca.  
  
3.  Il runtime successivamente interroga Windows Installer per determinare se l'assembly satellite debba essere installato su richiesta.  In caso affermativo, si occupa dell'installazione, carica l'assembly e lo cerca o richiede la risorsa.  Se trova la risorsa, la utilizza.  Se non trova la risorsa, continua la ricerca.  
  
4.  Il runtime genera l'evento <xref:System.AppDomain.AssemblyResolve?displayProperty=fullName> per indicare che non è in grado di trovare l'assembly satellite.  Se si sceglie di gestire l'evento, il gestore eventi può restituire un riferimento all'assembly satellite delle risorse che verranno utilizzate per la ricerca.  In caso contrario, il gestore eventi restituisce `null` e la ricerca continua.  
  
5.  Il runtime esegue una nuova ricerca nella Global Assembly Cache, questa volta al fine di individuare l'assembly padre della lingua richiesta.  Se la Global Assembly Cache contiene l'assembly padre, il runtime vi cerca la risorsa richiesta.  
  
     La lingua padre viene considerata come la lingua fallback appropriata.  Avvalersi del padre come candidato fallback è la soluzione più indicata. È preferibile fornire una risorsa qualsiasi piuttosto che generare un'eccezione.  Questo processo consente anche di riutilizzare le risorse.  È necessario includere una risorsa particolare a livello del padre solo se la lingua del figlio non richiede la localizzazione della risorsa desiderata.  Se, ad esempio, vengono forniti assembly satellite per en \(inglese neutro\), en\-GB \(l'inglese del Regno Unito\) ed en\-US \(l'inglese degli Stati Uniti\), il satellite en conterrà la terminologia comune e i satelliti en\-GB ed en\-US potranno fornire gli override per i soli termini che differiscono.  
  
6.  Il runtime cerca quindi una directory padre nella directory dell'assembly in esecuzione.  Se esiste una directory padre, il runtime vi cerca un assembly satellite valido per le impostazioni cultura padre.  Se trova l'assembly, il runtime vi cerca la risorsa richiesta.  Se trova la risorsa, la utilizza.  Se non trova la risorsa, continua la ricerca.  
  
7.  Il runtime successivamente interroga Windows Installer per determinare se l'assembly satellite padre debba essere installato su richiesta.  In caso affermativo, si occupa dell'installazione, carica l'assembly e lo cerca o richiede la risorsa.  Se trova la risorsa, la utilizza.  Se non trova la risorsa, continua la ricerca.  
  
8.  Il runtime genera l'evento <xref:System.AppDomain.AssemblyResolve?displayProperty=fullName> per indicare che non riesce a trovare una risorsa di fallback appropriata.  Se si sceglie di gestire l'evento, il gestore eventi può restituire un riferimento all'assembly satellite delle risorse che verranno utilizzate per la ricerca.  In caso contrario, il gestore eventi restituisce `null` e la ricerca continua.  
  
9. Il runtime cerca quindi gli assembly padre, come nei tre passaggi precedenti, in numerosi livelli.  Le lingue hanno un solo padre, definito dalla proprietà <xref:System.Globalization.CultureInfo.Parent%2A?displayProperty=fullName>, ma un padre può avere il proprio padre.  La ricerca della lingua padre viene arrestata quando la proprietà <xref:System.Globalization.CultureInfo.Parent%2A> restituisce <xref:System.Globalization.CultureInfo.InvariantCulture%2A?displayProperty=fullName>; per fallback delle risorse, la lingua inglese non è considerata lingua padre o lingua che possa disporre di risorse.  
  
10. Se la risorsa non viene trovata nelle impostazioni cultura originariamente specificate né in alcuno degli elementi padre, verrà utilizzata la risorsa delle impostazioni cultura di fallback predefinite.  In genere, le risorse per la lingua predefinite sono incluse nell'assembly principale dell'applicazione.  Tuttavia, è possibile specificare un valore <xref:System.Resources.UltimateResourceFallbackLocation> per la proprietà <xref:System.Resources.NeutralResourcesLanguageAttribute.Location%2A> dell'attributo <xref:System.Resources.NeutralResourcesLanguageAttribute> per indicare che il percorso di fallback finale delle risorse è un assembly satellite, anziché l'assembly principale.  
  
    > [!NOTE]
    >  La risorsa predefinita è l'unica risorsa compilata con l'assembly principale.  Finché non si specifica un assembly satellite usando l'attributo <xref:System.Resources.NeutralResourcesLanguageAttribute>, esso sarà il fallback finale.  Pertanto, si raccomanda di includere sempre un set predefinito di risorse nell'assembly principale.  Questo consente di evitare che vengano generate eccezioni.  L'inclusione di un file di risorse predefinito assicura la disponibilità di un fallback per tutte le risorse e garantisce che per l'utente sia presente almeno una risorsa, anche se non è specifica della lingua.  
  
11. Infine, se il runtime non trova una risorsa per la lingua predefinita \(fallback\), verrà generata un'eccezione <xref:System.Resources.MissingManifestResourceException> o <xref:System.Resources.MissingSatelliteAssemblyException> in cui viene indicato che la risorsa non è stata trovata.  
  
 Ad esempio, si supponga che l'applicazione richieda una risorsa localizzata in Spagnolo \(Messico\) \(lingua es\-MX\).  Il runtime cerca innanzitutto nella Global Assembly Cache che l'assembly corrispondente es\-MX, ma non lo trova.  Il runtime cerca quindi una directory "es\-MX" nella directory dell'assembly in esecuzione.  Se non la trova, il runtime cerca nuovamente nella Global Assembly Cache un assembly padre che corrisponda alla lingua di fallback appropriata, in questo caso "es" \(spagnolo\).  Se l'assembly padre non viene trovato, il runtime risale l'intera gerarchia alla ricerca dell'assembly per la lingua "es\-MX", finché non trova una risorsa corrispondente.  Se non trova alcuna risorsa, il runtime utilizza la risorsa della lingua predefinita.  
  
<a name="Optimizing"></a>   
### Ottimizzare il processo di fallback delle risorse  
 Nelle seguenti circostanze, è possibile ottimizzare il processo con cui il runtime cerca le risorse negli assembly satellite  
  
-   Gli assembly satellite vengono distribuiti nella stessa posizione dell'assembly di codice.  Se l'assembly di codice è installato in [Global Assembly Cache](../../../docs/framework/app-domains/gac.md), gli assembly satellite vengono installati nella Global Assembly Cache.  Se il codice assembly viene installato in una directory, gli assembly satellite vengono installati in cartelle della lingua specifica della directory.  
  
-   Gli assembly satellite non sono installati su richiesta.  
  
-   Il codice dell'applicazione non gestisce l'evento <xref:System.AppDomain.AssemblyResolve?displayProperty=fullName>.  
  
 È possibile ottimizzare le ricerche per gli assembly satellite includendo l'elemento [\<relativeBindForResources\>](../../../docs/framework/configure-apps/file-schema/runtime/relativebindforresources-element.md) e impostando il relativo attributo `enabled` a `true` nel file di configurazione dell'applicazione, come illustrato nell'esempio seguente.  
  
```  
  
<configuration>  
   <runtime>  
      <relativeBindForResources enabled="true" />  
   </runtime>  
</configuration>  
  
```  
  
 Le ricerche ottimizzate per gli assembly satellite sono una caratteristica opt\-in.  Ovvero il runtime osserva i passaggi illustrati in [Il processo di fallback delle risorse](../../../docs/framework/resources/packaging-and-deploying-resources-in-desktop-apps.md#cpconpackagingdeployingresourcesanchor1) a meno che l'elemento [\<relativeBindForResources\>](../../../docs/framework/configure-apps/file-schema/runtime/relativebindforresources-element.md) sia presente nel file di configurazione dell'applicazione e il relativo attributo `enabled` è impostato su `true`.  In questo caso, il processo di ricerca per un assembly satellite viene modificato come segue:  
  
-   Il runtime utilizza la posizione del codice assembly padre da ricercare per l'assembly satellite.  Se l'assembly padre viene installato nella Global Assembly Cache, il runtime esegue la ricerca nella cache non nella directory dell'applicazione.  Se l'assembly padre viene installato nella directory dell'applicazione, il runtime esegue la ricerca nella directory dell'applicazione, non nella global assembly cache.  
  
-   Il runtime non interroga Windows Installer per un'installazione su richiesta dell'assembly satellite.  
  
-   Se le ricerche per una particolare risorsa assembly fallisce, il runtime non genera l'evento <xref:System.AppDomain.AssemblyResolve?displayProperty=fullName>.  
  
### Fallback finale in un assembly satellite  
 È possibile rimuovere le risorse dall'assembly principale e specificare che il runtime deve caricare le risorse di fallback finali da un assembly satellite corrispondente ad una lingua specifica.  Per controllare il processo di fallback, utilizzare il costruttore <xref:System.Resources.NeutralResourcesLanguageAttribute.%23ctor%28System.String%2CSystem.Resources.UltimateResourceFallbackLocation%29?displayProperty=fullName> e fornire un valore per il parametro <xref:System.Resources.UltimateResourceFallbackLocation> che specifica se Gestione risorse deve estrarre le risorse di fallback dall'assembly principale o da un assembly satellite.  
  
 Nell'esempio seguente viene utilizzato l'attributo <xref:System.Resources.NeutralResourcesLanguageAttribute> per archiviare le risorse di fallback di un'applicazione in un assembly satellite per la lingua francese \(fr\).  L'esempio presenta due file di risorse basati su testo che definiscono una risorsa stringa denominata `Greeting`.  Il primo, resources.fr.txt, contiene una risorsa in lingua francese.  
  
```  
Greeting=Bon jour!  
```  
  
 Il secondo, le risorse, ru.txt, contiene una risorsa di lingua russa.  
  
```  
Greeting=Добрый день  
```  
  
 Questi due file vengono compilati nel file .resources eseguendo il file di risorse [\(Resgen.exe\)](../../../docs/framework/tools/resgen-exe-resource-file-generator.md) da riga di comando.  Per la risorsa in lingua francese, il comando è:  
  
 **resgen.exe resources.fr.txt**  
  
 Per la risorsa in lingua russa, il comando è:  
  
 **resgen.exe resources.ru.txt**  
  
 I file con estensione .resources sono incorporati nelle librerie a collegamento dinamico eseguendo [assembly linker \(Al.exe\)](../../../docs/framework/tools/al-exe-assembly-linker.md) dalla riga di comando per la risorsa in lingua francese come segue:  
  
 **al \/t:lib \/embed:resources.fr.resources \/culture:fr \/out:fr\\Example1.resources.dll**  
  
 e per la risorsa di lingua russa come segue:  
  
 **al \/t:lib \/embed:resources.ru.resources \/culture:ru \/out:ru\\Example1.resources.dll**  
  
 Il codice sorgente dell'applicazione risiede in un file denominato Example1.cs o Example1.vb.  Include l'attributo <xref:System.Resources.NeutralResourcesLanguageAttribute> per indicare che la risorsa predefinita dell'applicazione consiste nella sottodirectory fr.  Crea un'istanza di Gestione Risorse, recupera il valore della risorsa `Greeting` e lo visualizza nella console.  
  
 [!code-csharp[Conceptual.Resources.Packaging#1](../../../samples/snippets/csharp/VS_Snippets_CLR/conceptual.resources.packaging/cs/example1.cs#1)]
 [!code-vb[Conceptual.Resources.Packaging#1](../../../samples/snippets/visualbasic/VS_Snippets_CLR/conceptual.resources.packaging/vb/example1.vb#1)]  
  
 È quindi possibile compilare il codice sorgente C\# dalla riga di comando come segue:  
  
 **csc Example1.cs**  
  
 Il comando del compilatore Visual Basic è molto simile:  
  
 **vbc Example1.vb**  
  
 Poiché non sono disponibili risorse incorporate nell'assembly principale, non è necessario eseguire la compilazione utilizzando l'opzione `/resource`.  
  
 Quando si esegue l'esempio dal sistema in cui la lingua è diversa dal Russo, viene visualizzato il seguente output:  
  
```  
Bon jour!  
```  
  
## Alternativa suggerita per la creazione del package  
 Limiti di tempo o di budget può prevenire dal creare un set di risorse per tutte le lingue secondarie supportate dall'applicazione.  È possibile invece creare un assembly satellite singolo per la lingua padre che tutte le relative sotto lingue possono utilizzare.  È possibile fornire, ad esempio, un singolo assembly satellite inglese \(en\), che verrà recuperato dagli tutti gli utenti che richiedono risorse in inglese e un singolo assembly satellite tedesco \(de\) per tutti gli utenti che richiedono risorse in tedesco.  In quest'ultimo caso, le richieste di risorse in tedesco della Germania \(de\-DE\), tedesco dell'Austria \(de\-AT\) e tedesco della Svizzera \(de\-CH\) verrebbero tutte ricondotte all'unico assembly satellite tedesco \(de\).  Le risorse predefinite rappresentano il fallback finale e, pertanto, è possibile che siano le risorse che verranno richieste dalla maggior parte degli utenti dell'applicazione; usate queste risorse con molta attenzione.  Questa soluzione prevede la distribuzione di risorse meno specifiche in termini di lingua, ma consente di ridurre notevolmente i costi di localizzazione dell'applicazione.  
  
## Vedere anche  
 [Risorse nelle applicazioni desktop](../../../docs/framework/resources/index.md)   
 [Global Assembly Cache](../../../docs/framework/app-domains/gac.md)   
 [Creazione di file di risorse](../../../docs/framework/resources/creating-resource-files-for-desktop-apps.md)   
 [Creazione di assembly satellite](../../../docs/framework/resources/creating-satellite-assemblies-for-desktop-apps.md)