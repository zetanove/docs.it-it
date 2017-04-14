---
title: "Code Access Security | Microsoft Docs"
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
  - "named permission sets, code access security"
  - "call stacks"
  - "malicious code"
  - "stack walk"
  - "security [.NET Framework], code access security"
  - "permissions [.NET Framework], code access security"
  - "trusted code"
  - "mobile code security"
  - "unmanaged code, code access security"
  - "granting permissions, code access security"
  - "user authentication, code access security"
  - "code access security"
ms.assetid: 859af632-c80d-4736-8d6f-1e01b09ce127
caps.latest.revision: 25
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 23
---
# Code Access Security
Gli attuali computer con connessione elevata sono spesso esposti a codice che deriva da origini svariate e magari sconosciute.  Il codice può essere allegato a un messaggio di posta elettronica, contenuto in documenti o scaricato da Internet.  Sfortunatamente, molti utenti hanno sperimentato in prima persona gli effetti dei codici mobili dannosi, tra cui virus e worm, che possono danneggiare o distruggere i dati e costare tempo e denaro.  
  
 La maggior parte dei comuni meccanismi di sicurezza concede agli utenti diritti basati sulle credenziali di accesso \(in genere una password\) e limita le risorse \(spesso directory e file\) a cui l'utente può accedere.  Tuttavia, questo approccio non riesce a risolvere alcuni problemi: gli utenti ottengono il codice da molte origini, alcune delle quali potrebbero non essere affidabili, il codice può contenere bug o vulnerabilità che permettono ai malware di sfruttarlo e a volte il codice esegue operazioni di cui l'utente non è a conoscenza.  Di conseguenza, quando utenti attenti e affidabili eseguono software dannoso o con errori, possono verificarsi danni al sistemi del computer e ai dati privati.  La maggior parte dei meccanismi di sicurezza del sistema operativo richiede che ogni parte del codice da eseguire sia completamente attendibile, ad eccezione forse degli script di una pagina Web.  Dunque esiste ancora la necessità di un meccanismo di sicurezza applicabile su vasta scala, che consenta di eseguire il codice derivante dal sistema di un computer in modo protetto su un altro sistema, anche quando non esiste alcuna relazione di trust tra i sistemi.  
  
 .NET Framework fornisce un meccanismo di sicurezza, detto sicurezza dall'accesso di codice, che permette di proteggere i sistemi dei computer dal codice mobile dannoso, consentendo così di eseguire in modo protetto il codice di origine sconosciuta, e di impedire al codice attendibile di compromettere la sicurezza intenzionalmente o accidentalmente.  Mediante la sicurezza dall'accesso di codice è possibile considerare il codice come attendibile a vari livelli, a seconda dell'origine del codice e di altri aspetti relativi all'identità del codice.  La sicurezza dall'accesso di codice applica anche i diversi livelli di attendibilità al codice, riducendo al minimo la quantità di codice che deve essere completamente attendibile per poter essere eseguito.  L'uso della sicurezza dall'accesso di codice può ridurre la probabilità che il codice venga usato in modo improprio da malware o da codice con errori.  Può ridurre la responsabilità dell'utente, perché è possibile specificare il set di operazioni che possono essere eseguite dal codice.  La sicurezza dall'accesso di codice permette anche di ridurre al minimo i danni che possono derivare da vulnerabilità di protezione nel codice.  
  
> [!NOTE]
>  In [!INCLUDE[net_v40_long](../../../includes/net-v40-long-md.md)] sono state apportate importanti modifiche alla sicurezza dall'accesso di codice.  La modifica più importante è stata la [trasparenza della sicurezza](../../../docs/framework/misc/security-transparent-code.md), ma ci sono anche altre modifiche significative che influiscono sulla sicurezza dall'accesso di codice.  Per informazioni su queste modifiche, vedere [Modifiche della sicurezza](../../../docs/framework/security/security-changes.md).  
  
 La sicurezza dall'accesso di codice influisce principalmente sul codice di libreria e sulle applicazioni parzialmente attendibili.  Gli sviluppatori di librerie devono proteggere il codice da accesso non autorizzato da applicazioni parzialmente attendibili.  Le applicazioni parzialmente attendibili sono applicazioni che vengono caricate da origini esterne, ad esempio da Internet.  Le applicazioni installate nel desktop o nella rete Intranet locale vengono eseguite con attendibilità totale.  Le applicazioni con attendibilità totale non sono interessate dalla sicurezza dall'accesso di codice a meno che non siano contrassegnate come [trasparenti per la sicurezza](../../../docs/framework/misc/security-transparent-code.md), perché sono completamente attendibili.  L'unica limitazione per le applicazioni con attendibilità totale è che le applicazioni contrassegnate con l'attributo <xref:System.Security.SecurityTransparentAttribute> non possono chiamare il codice contrassegnato con l'attributo <xref:System.Security.SecurityCriticalAttribute>.  Le applicazioni parzialmente attendibili devono essere eseguite in una sandbox \(ad esempio, in Internet Explorer\), per poter applicare la sicurezza dall'accesso di codice.  Se si scarica un'applicazione da Internet e si cerca di eseguirla dal desktop, verrà generata un'eccezione <xref:System.NotSupportedException> con il messaggio: "È stato effettuato un tentativo di caricamento di un assembly da un percorso di rete, il che avrebbe causato la creazione mediante sandbox dell'assembly nelle versioni precedenti di .NET Framework.  In questa versione di .NET Framework i criteri di sicurezza dall'accesso di codice non sono abilitati per impostazione predefinita, pertanto questo tipo di caricamento può risultare pericoloso". Se si è sicuri circa l'attendibilità dell'applicazione, è possibile consentirne l'esecuzione con attendibilità totale tramite l'elemento [\<loadFromRemoteSources\>](../../../docs/framework/configure-apps/file-schema/runtime/loadfromremotesources-element.md).  Per informazioni sull'esecuzione di un'applicazione in una sandbox, vedere [How to: Run Partially Trusted Code in a Sandbox](../../../docs/framework/misc/how-to-run-partially-trusted-code-in-a-sandbox.md).  
  
 Tutto il codice gestito destinato a Common Language Runtime sfrutta i vantaggi della sicurezza dall'accesso di codice, anche se tale codice non effettua un'unica chiamata alla sicurezza dall'accesso di codice.  Per altre informazioni, vedere [Code Access Security Basics](../../../docs/framework/misc/code-access-security-basics.md).  
  
> [!CAUTION]
>  Sicurezza dall'accesso di codice e codice parzialmente attendibile  
>   
>  .NET Framework fornisce un meccanismo denominato sicurezza dall'accesso di codice, che consente di applicare vari livelli di attendibilità a codice diverso in esecuzione nella stessa applicazione.  La sicurezza dall'accesso di codice in .NET Framework non va usata come limite di sicurezza con codice parzialmente attendibile, in particolare con codice di origine sconosciuta.  Non è consigliabile caricare ed eseguire codice di origine sconosciuta in assenza di misure di sicurezza alternative.  
>   
>  Questi criteri si applicano a tutte le versioni di .NET Framework, ma non alla versione di .NET Framework inclusa in Silverlight.  
  
<a name="key_functions"></a>   
## Funzioni chiave della sicurezza dall'accesso di codice  
 La sicurezza dall'accesso di codice consente di limitare l'accesso del codice alle risorse e alle operazioni protette.  In .NET Framework la sicurezza dall'accesso di codice svolge le seguenti funzioni:  
  
-   Definizione di autorizzazioni e set di autorizzazioni che rappresentano il diritto di accedere a varie risorse di sistema.  
  
-   Possibilità di esigere dai chiamanti del codice il possesso di autorizzazioni specifiche.  
  
-   Possibilità di esigere dai chiamanti del codice il possesso di una firma digitale, in modo che solo i chiamanti appartenenti a un'organizzazione o a un sito particolare siano autorizzati a chiamare il codice sicuro.  
  
-   Applicazione di restrizioni sul codice in fase di esecuzione confrontando le autorizzazioni concesse a ogni chiamante dello stack di chiamate con le autorizzazioni effettivamente necessarie.  
  
<a name="walking_the_call_stack"></a>   
## Analisi dello stack di chiamate  
 Per determinare se il codice è autorizzato ad accedere a una risorsa o a eseguire un'operazione, il sistema di sicurezza del runtime analizza lo stack di chiamate, confrontando le autorizzazioni concesse di ogni chiamante con l'autorizzazione richiesta.  Se un qualsiasi chiamante nello stack di chiamate non dispone dell'autorizzazione richiesta, viene generata un'eccezione di sicurezza e l'accesso viene rifiutato.  L'analisi dello stack è progettata per impedire attacchi luring, in cui un codice meno attendibile chiama un codice altamente attendibile e lo usa per eseguire azioni non autorizzate.  La richiesta delle autorizzazioni di tutti i chiamanti in fase di esecuzione ha effetto sulle prestazioni, ma è fondamentale per proteggere il codice dagli attacchi luring da parte di codice meno attendibile.  Per ottimizzare le prestazioni, è possibile far analizzare al codice meno percorsi dello stack. Tuttavia, è necessario assicurarsi ogni volta di non esporre un punto debole nella sicurezza.  
  
 La figura seguente mostra il risultato dell'analisi dello stack quando un metodo in Assembly A4 richiede che i chiamanti dispongano dell'autorizzazione P.  
  
 ![Sicurezza dall'accesso di codice](../../../docs/framework/misc/media/slide-10a.gif "slide\_10a")  
Analisi dello stack di sicurezza  
  
<a name="related_topics"></a>   
## Argomenti correlati  
  
|Titolo|Descrizione|  
|------------|-----------------|  
|[Code Access Security Basics](../../../docs/framework/misc/code-access-security-basics.md)|Descrive la sicurezza dall'accesso di codice e gli usi più comuni.|  
|[Security\-Transparent Code, Level 2](../../../docs/framework/misc/security-transparent-code-level-2.md)|Descrive il modello di trasparenza della sicurezza in [!INCLUDE[net_v40_short](../../../includes/net-v40-short-md.md)].|  
|[Using Libraries from Partially Trusted Code](../../../docs/framework/misc/using-libraries-from-partially-trusted-code.md)|Descrive come abilitare le librerie per usarle con codice non gestito e come usare le librerie provenienti da codice non gestito.|  
|[Key Security Concepts](../../../docs/standard/security/key-security-concepts.md)|Fornisce una panoramica di diversi termini e concetti chiave usati nel sistema di sicurezza di .NET Framework.|  
|[Role\-Based Security](../../../docs/standard/security/role-based-security.md)|Descrive come incorporare la sicurezza basata sui ruoli.|  
|[Servizi di crittografia](../../../docs/standard/security/cryptographic-services.md)|Descrive come incorporare la crittografia nelle applicazioni.|