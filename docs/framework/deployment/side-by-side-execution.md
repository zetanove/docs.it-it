---
title: "Esecuzione side-by-side in .NET Framework | Microsoft Docs"
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
  - "esecuzione affiancata"
ms.assetid: 649f1342-766b-49e6-a90d-5b019a751e11
caps.latest.revision: 21
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 21
---
# Esecuzione side-by-side in .NET Framework
L'esecuzione side\-by\-side consente di eseguire più versioni di un'applicazione o di un componente sullo stesso computer.  È possibile disporre contemporaneamente sullo stesso computer di più versioni di Common Language Runtime e di più versioni di applicazioni e componenti che usano una versione runtime.  
  
 Nella figura riportata di seguito viene illustrato l'uso di due diverse versioni runtime da parte di più applicazioni sullo stesso computer.  Nelle applicazioni A, B e C viene usata la versione runtime 1.0, mentre nell'applicazione D viene usata la versione runtime 1.1.  
  
 ![Esecuzione side&#45;by&#45;side](../../../docs/framework/deployment/media/simplesbs.gif "simplesbs")  
Esecuzione side\-by\-side di due versioni runtime  
  
 .NET Framework è costituito dal Common Language Runtime e da una raccolta di assembly contenenti i tipi di API.  Per il runtime e gli assembly .NET Framework vengono usate versioni distinte.  La versione runtime 4.0, ad esempio, corrisponde in realtà alla versione 4.0.319, mentre la versione 1.0 degli assembly .NET Framework rappresenta la versione 1.0.3300.0.  
  
 Nella figura riportata di seguito viene illustrato l'uso di due diverse versioni di un componente da parte di più applicazioni sullo stesso computer.  Nelle applicazioni A e B viene usata la versione 1.0 del componente, mentre nell'applicazione C viene usata la versione 2.0 dello stesso componente.  
  
 ![Esecuzione side&#45;by&#45;side](../../../docs/framework/deployment/media/compsbs.gif "compsbs")  
Esecuzione side\-by\-side di due versioni di un componente  
  
 L'esecuzione side\-by\-side offre un maggiore controllo sulle versioni di un componente a cui viene associata un'applicazione, nonché sulla versione runtime usata da un'applicazione.  
  
## Vantaggi dell'esecuzione side\-by\-side  
 Prima del rilascio di Windows XP e .NET Framework si verificavano conflitti tra le DLL poiché le applicazioni non erano in grado di effettuare una distinzione tra versioni incompatibili dello stesso codice.  Le informazioni sui tipi contenute in una DLL erano associate solo a un nome file.  Un'applicazione non disponeva di alcuno strumento per verificare se i tipi contenuti in una DLL corrispondevano ai tipi con cui l'applicazione era stata compilata.  Di conseguenza, una nuova versione di un componente poteva sovrascrivere una versione precedente pregiudicando l'esecuzione delle applicazioni.  
  
 Allo scopo di eliminare i conflitti tra DLL, l'esecuzione side\-by\-side e .NET Framework forniscono le funzionalità illustrate di seguito.  
  
-   Assembly con nome sicuro.  
  
     Nell'ambito dell'esecuzione side\-by\-side vengono usati assembly con nome sicuro per associare le informazioni sui tipi a una specifica versione di un assembly.  In questo modo viene impedita l'associazione di un'applicazione o di un componente a una versione non valida di un assembly.  Gli assembly con nome sicuro consentono la presenza di più versioni di un file sullo stesso computer e il relativo uso da parte delle applicazioni.  Per altre informazioni, vedere [Assembly con nomi sicuri](../../../docs/framework/app-domains/strong-named-assemblies.md).  
  
-   Archiviazione del codice con supporto della versione.  
  
     .NET Framework consente l'archiviazione del codice con supporto della versione nella Global Assembly Cache.  La Global Assembly Cache rappresenta una cache di codice a livello di computer presente su tutti i computer su cui è installato .NET Framework.  Questa cache, in cui gli assembly vengono archiviati in base alle informazioni sulla versione, sulle impostazioni cultura e sull'editore, supporta più versioni di componenti e applicazioni.  Per altre informazioni, vedere [Global Assembly Cache](../../../docs/framework/app-domains/gac.md).  
  
-   Isolamento.  
  
     Usando .NET Framework, è possibile creare applicazioni e componenti eseguiti in isolamento.  L'isolamento è un componente essenziale dell'esecuzione side\-by\-side.  Per l'isolamento è necessario tenere traccia delle risorse usate e condividere in modo sicuro le risorse tra più versioni di un'applicazione o di un componente.  L'isolamento comprende inoltre l'archiviazione dei file in base alla versione.  Per altre informazioni sull'isolamento, vedere [Linee guida per la creazione di componenti per l'esecuzione affiancata di più versioni](../../../docs/framework/deployment/guidelines-for-creating-components-for-side-by-side-execution.md).  
  
## Compatibilità tra versioni  
 Le versioni 1.0 e 1.1 di .NET Framework sono state progettate in modo da garantirne la compatibilità.  È previsto che un'applicazione compilata con .NET Framework versione 1.0 possa essere eseguita con la versione 1.1 e che un'applicazione compilata con .NET Framework versione 1.1 possa essere eseguita con la versione 1.0.  Le funzionalità delle API aggiunte nella versione 1.1 di .NET Framework non possono tuttavia essere usate nella versione 1.0.  Le applicazioni create con la versione 2.0 potranno essere eseguite solo con quella stessa versione.  Pertanto non sarà possibile eseguirle con la versione 1.1 o precedente.  
  
 Le versioni di .NET Framework vengono gestite come una singola unità costituita dal runtime e dagli assembly .NET Framework associati, in base a un concetto definito unificazione degli assembly.  È possibile reindirizzare l'associazione di assembly in modo da includere altre versioni degli assembly .NET Framework. L'override dell'associazione di assembly predefinita può tuttavia rivelarsi rischioso e richiede l'esecuzione di test accurati prima della distribuzione.  
  
## Individuazione delle informazioni sulla versione runtime  
 Le informazioni sulla versione runtime con cui è stata compilata un'applicazione o un componente e le versioni runtime richieste per l'esecuzione dall'applicazione sono archiviate in due posizioni.  Quando viene compilata un'applicazione o un componente, le informazioni sulla versione runtime usata per la compilazione vengono archiviate nel file eseguibile gestito.  Le informazioni sulle versioni di runtime richieste dall'applicazione o dal componente vengono archiviate nel file di configurazione dell'applicazione.  
  
### Informazioni sulla versione runtime nel file eseguibile gestito  
 L'intestazione del file eseguibile di tipo PE di tutte le applicazioni e componenti gestiti contiene informazioni sulla versione runtime con cui sono stati compilati.  Common Language Runtime usa queste informazioni per determinare la versione runtime che è più probabile venga eseguita dall'applicazione.  
  
### Informazioni sulla versione runtime nel file di configurazione dell'applicazione  
 Oltre alle informazioni nell'intestazione del file PE, un'applicazione può essere distribuita con un file di configurazione dell'applicazione che fornisce informazioni sulla versione runtime.  Il file di configurazione dell'applicazione è un file basato su XML fornito con un'applicazione, che viene creato dallo sviluppatore dell'applicazione.  L'[Elemento \<requiredRuntime\>](../../../docs/framework/configure-apps/file-schema/startup/requiredruntime-element.md) della [sezione \<startup\>](../../../docs/framework/configure-apps/file-schema/startup/startup-element.md), se presente in questo file, specifica le versioni di runtime e le versioni di un componente supportate dall'applicazione.  Questo file può essere anche usato durante i test per verificare la compatibilità di un'applicazione con diverse versioni di runtime.  
  
 Il codice non gestito, incluse le applicazioni COM e COM\+, può disporre di file di configurazione dell'applicazione usate dal runtime per l'interazione con il codice gestito.  Il file di configurazione dell'applicazione ha effetto sul codice gestito attivato tramite COM.  Il file può specificare le versioni di runtime supportate, nonché i reindirizzamenti dell'assembly.  Per impostazione predefinita, la chiamata delle applicazioni di interoperabilità COM al codice gestito usa la versione runtime più recente installata nel computer.  
  
 Per altre informazioni sui file di configurazione dell'applicazione, vedere [Configurazione di app](../../../docs/framework/configure-apps/index.md).  
  
## Determinazione della versione runtime da caricare  
 Common Language Runtime usa le informazioni seguenti per determinare la versione runtime da caricare per un'applicazione:  
  
-   Le versioni di runtime disponibili.  
  
-   Le versioni di runtime supportate da un'applicazione.  
  
### Versioni di runtime supportate  
 Il runtime usa il file di configurazione dell'applicazione e l'intestazione del file eseguibile di tipo PE per determinare quale versione runtime è supportata da un'applicazione.  Se non sono presenti file di configurazione dell'applicazione, il runtime carica la versione runtime specificata nell'intestazione del file PE dell'applicazione, se disponibile.  
  
 Se è presente un file di configurazione dell'applicazione, il runtime determina la versione runtime appropriata per eseguire il caricamento in base ai risultati del processo riportato di seguito:  
  
1.  Il runtime esamina l'elemento [Elemento \<supportedRuntime\>](../../../docs/framework/configure-apps/file-schema/startup/supportedruntime-element.md) nel file di configurazione dell'applicazione.  Se sono presenti una o più le versioni runtime supportate specificate nell'elemento **\<supportedRuntime\>**, tramite il runtime viene caricata la versione runtime specificata dal primo elemento **\<supportedRuntime\>**.  Se questa versione non è disponibile, tramite il runtime viene esaminato l'elemento **\<supportedRuntime\>** successivo e viene effettuato il tentativo di caricamento della versione runtime specificata.  Se questa versione non è disponibile, vengono esaminati gli elementi **\<supportedRuntime\>** successivi.  Se non è disponibile alcuna versione runtime supportata, il runtime non riesce a caricare una versione runtime e viene visualizzato un messaggio per l'utente \(vedere il passaggio 3\).  
  
2.  Il runtime legge l'intestazione del file PE del file eseguibile dell'applicazione.  Se la versione runtime specificata dall'intestazione del file PE è disponibile, il runtime carica tale versione.  Se la versione runtime specificata non è disponibile, il runtime cerca una versione runtime indicata da Microsoft come compatibile con la versione runtime nell'intestazione del file PE.  Se tale versione non viene trovata, il processo procede al passaggio 3.  
  
3.  Il runtime visualizza un messaggio che informa che non è disponibile la versione runtime supportata dall'applicazione.  Il runtime non viene caricato.  
  
    > [!NOTE]
    >  È possibile impedire la visualizzazione del messaggio usando il valore NoGuiFromShim nella chiave del Registro di sistema HKLM\\Software\\Microsoft\\. NETFramework o la variabile di ambiente COMPLUS\_NoGuiFromShim.  Ad esempio, è possibile eliminare il messaggio per le applicazioni che in genere non interagiscono con l'utente, ad esempio le installazioni automatiche o i servizi di Windows.  Quando si sceglie di non visualizzare il messaggio, il runtime scrive un messaggio nel log eventi.  Impostare il valore del Registro di sistema NoGuiFromShim su 1 per impedire la visualizzazione di questo messaggio in tutte le applicazioni di un computer.  In alternativa, impostare la variabile di ambiente COMPLUS\_NoGuiFromShim su 1 per eliminare il messaggio nelle applicazioni in esecuzione in uno specifico contesto utente.  
  
> [!NOTE]
>  Dopo aver caricato una versione runtime, i reindirizzamenti dell'associazione di assembly possono richiedere il caricamento di una versione diversa di un singolo assembly di .NET Framework.  Questi reindirizzamenti dell'associazione hanno effetto solo sull'assembly reindirizzato.  
  
## Nomi parziali di assembly ed esecuzione side\-by\-side di più versioni  
 I riferimenti ad assembly parziali possono essere usati solo per l'associazione ad assembly contenuti in una directory dell'applicazione perché possono causare problemi nell'esecuzione side\-by\-side.  Evitare riferimenti ad assembly parziali nel codice.  
  
 Per limitare l'effetto dei riferimenti ad assembly parziali nel codice, è possibile usare l'elemento [\<qualifyAssembly\>](../../../docs/framework/configure-apps/file-schema/runtime/qualifyassembly-element.md) del file di configurazione di un'applicazione per rendere completi i riferimenti ad assembly parziali presenti nel codice.  Usare l'elemento **\<qualifyAssembly\>** per specificare solo i campi non impostati nel riferimento parziale.  L'identità dell'assembly elencata nell'attributo **fullName** deve contenere tutte le informazioni necessarie per completare il nome dell'assembly: nome dell'assembly, chiave pubblica, impostazioni cultura e versione.  
  
 L'esempio seguente mostra la voce del file di configurazione dell'applicazione che consente di completare un assembly denominato `myAssembly`.  
  
```  
<assemblyBinding xmlns="urn:schemas-microsoft-com:asm.v1">   
<qualifyAssembly partialName="myAssembly"   
fullName="myAssembly,  
      version=1.0.0.0,   
publicKeyToken=...,   
      culture=neutral"/>   
</assemblyBinding>   
```  
  
 Se un'istruzione di caricamento dell'assembly fa riferimento a `myAssembly`, queste impostazioni del file di configurazione attivano la conversione automatica da parte del runtime del riferimento `myAssembly` parziale in riferimento completo.  Ad esempio, Assembly.Load\("myAssembly"\) diventa Assembly.Load\("myAssembly, version\=1.0.0.0, publicKeyToken\=..., culture\=neutral"\).  
  
> [!NOTE]
>  È possibile usare il metodo **LoadWithPartialName** per ignorare la restrizione di Common Language Runtime che impedisce il caricamento degli assembly con riferimento parziale dalla Global Assembly Cache.  Questo metodo deve essere usato solo in scenari remoti perché può causare problemi nell'esecuzione side\-by\-side.  
  
## Argomenti correlati  
  
|Titolo|Descrizione|  
|------------|-----------------|  
|[Procedura: abilitare e disabilitare il reindirizzamento di associazione automatico](../../../docs/framework/configure-apps/how-to-enable-and-disable-automatic-binding-redirection.md)|Viene descritto come associare un'applicazione a una versione specifica di un assembly.|  
|[Configurazione del reindirizzamento dell'associazione di assembly](../../../docs/framework/deployment/configuring-assembly-binding-redirection.md)|Viene illustrato come reindirizzare i riferimenti di associazione di assembly a una specifica versione degli assembly di .NET Framework.|  
|[Esecuzione side\-by\-side in\-process](../../../docs/framework/deployment/in-process-side-by-side-execution.md)|Viene illustrato come usare l'attivazione dell'host di runtime side\-by\-side in\-process per eseguire più versioni di CLR in un solo processo.|  
|[Assembly in Common Language Runtime](../../../docs/framework/app-domains/assemblies-in-the-common-language-runtime.md)|Viene fornita una panoramica sui concetti di base relativi agli assembly.|  
|[Domini applicazione](../../../docs/framework/app-domains/application-domains.md)|Viene fornita una panoramica sui concetti di base relativi ai domini applicazione.|  
  
## Riferimento  
 [Elemento \<supportedRuntime\>](../../../docs/framework/configure-apps/file-schema/startup/supportedruntime-element.md)