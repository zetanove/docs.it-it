---
title: "Spazio di memorizzazione isolato | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "codice, spazio di memorizzazione isolato"
  - "archiviazione di dati mediante spazio di memorizzazione isolato"
  - "archiviazione di dati mediante spazio di memorizzazione isolato, opzioni"
  - "archiviazione di dati mediante spazio di memorizzazione isolato, quando evitare l'utilizzo"
  - "spazio di memorizzazione isolato"
  - "spazio di memorizzazione isolato, opzioni"
  - "spazio di memorizzazione isolato, quando evitare l'utilizzo"
  - "isolamento"
  - "percorso di spazio di memorizzazione isolato nel file system"
  - "standardizzazione dei sistemi di archiviazione"
  - "archivi"
  - "dati (archiviazione mediante spazio di memorizzazione isolato)"
  - "dati (archiviazione mediante spazio di memorizzazione isolato), opzioni"
  - "dati (archiviazione mediante spazio di memorizzazione isolato), quando evitare l'utilizzo"
ms.assetid: aff939d7-9e49-46f2-a8cd-938d3020e94e
caps.latest.revision: 32
author: "mairaw"
ms.author: "mairaw"
manager: "wpickett"
caps.handback.revision: 31
---
# Spazio di memorizzazione isolato
<a name="top"></a> Per le applicazioni [!INCLUDE[desktop_appname](../../../includes/desktop-appname-md.md)], lo spazio di memorizzazione isolato è un meccanismo di archiviazione dati che offre isolamento e sicurezza definendo modi standardizzati di associare il codice ai dati salvati. La standardizzazione offre anche altri vantaggi. Gli amministratori possono utilizzare strumenti in grado di modificare l'archiviazione isolata per configurare lo spazio di archiviazione dei file, per impostare i criteri di sicurezza e per eliminare dati inutilizzati. Con lo spazio di memorizzazione isolato, non occorre più fornire al codice percorsi univoci per individuare posizioni sicure nel file system e i dati sono protetti da altre applicazioni che dispongono esclusivamente dell'accesso allo spazio di memorizzazione isolato. Non è necessario specificare informazioni hardcoded che indicano il percorso dell'area di archiviazione di un'applicazione.  
  
> [!IMPORTANT]
>  Lo spazio di memorizzazione isolato non è disponibile per le applicazioni [!INCLUDE[win8_appname_long](../../../includes/win8-appname-long-md.md)]. Al contrario, utilizzare le classi di dati dell'applicazione negli spazi dei nomi `Windows.Storage` inclusi nell'API [!INCLUDE[wrt](../../../includes/wrt-md.md)] per archiviare dati e file locali. Per altre informazioni, vedere [Dati dell'applicazione](http://go.microsoft.com/fwlink/?LinkId=229175) nel Centro per sviluppatori Windows.  
  
 Di seguito sono elencate le diverse sezioni di questo argomento:  
  
-   [Raggruppamenti e archivi dati](#data_compartments_and_stores)  
  
-   [Quote per lo spazio di memorizzazione isolato](#quotas)  
  
-   [Accesso sicuro](#secure_access)  
  
-   [Utilizzo consentito e rischi di sicurezza](#allowed_usage)  
  
-   [Percorsi dello spazio di memorizzazione isolato](#isolated_storage_locations)  
  
-   [Creazione, enumerazione ed eliminazione dello spazio di memorizzazione isolato](#isolated_storage_tasks)  
  
-   [Scenari per l'utilizzo dell'archiviazione isolata](#scenarios_for_isolated_storage)  
  
-   [Argomenti correlati](#related_topics)  
  
-   [Riferimento](#reference)  
  
<a name="data_compartments_and_stores"></a>   
## Raggruppamenti e archivi dati  
 Quando un'applicazione memorizza dati in un file, il nome del file e il percorso di archiviazione devono essere scelti attentamente, per ridurre la possibilità che il percorso di archiviazione venga individuato da un'altra applicazione e sia quindi soggetto a danneggiamenti. Senza un sistema standard in grado di gestire questi problemi, può risultare complesso sviluppare tecniche specifiche che riducano i conflitti di archiviazione e i risultati conseguiti potrebbero non essere affidabili.  
  
 Con l'archiviazione isolata i dati vengono sempre isolati in base all'utente o all'assembly. L'identità dell'assembly viene determinata da credenziali quali l'origine o il nome sicuro. I dati possono essere isolati anche in base al dominio applicazione, utilizzando credenziali analoghe.  
  
 Quando si utilizza lo spazio di memorizzazione isolato, le applicazioni salvano i dati in un raggruppamento dati univoco, associato ad alcuni aspetti dell'identità del codice quali l'autore o la firma. Il contesto dati è un'astrazione, non è un percorso di archiviazione specifico. È costituito da uno o più file di archiviazione isolata, denominati archivi, contenenti i percorsi di directory in cui sono effettivamente memorizzati i dati. È possibile, ad esempio, che a un'applicazione sia associato un raggruppamento dati e che una directory del file system implementi l'archivio in cui sono effettivamente conservati i dati dell'applicazione. Nell'archivio è possibile salvare qualsiasi tipo di dati, dalle preferenze utente allo stato dell'applicazione. Per lo sviluppatore, la posizione del contesto dati è trasparente. Gli archivi solitamente risiedono sul client, ma un'applicazione server può utilizzare gli archivi isolati per archiviare le informazioni impersonando l'utente sta funzionando. Tramite l'archiviazione isolata è inoltre possibile memorizzare informazioni su un server con un profilo utente comune, in modo che sia possibile spostare le informazioni insieme all'utente.  
  
 [Torna all'inizio](#top)  
  
<a name="quotas"></a>   
## Quote per lo spazio di memorizzazione isolato  
 Una quota è un limite allo spazio che può essere utilizzato per l'archiviazione isolata. La quota definisce i byte di spazio su file, l'overhead associato alla directory e altre informazioni dell'archivio. Lo spazio di memorizzazione isolato utilizza le quote di autorizzazione, ovvero limiti di archiviazione impostati utilizzando gli oggetti <xref:System.Security.Permissions.IsolatedStoragePermission>. Se si tenta di scrivere dati oltre il limite definito dalla quota, verrà generata un'eccezione <xref:System.IO.IsolatedStorage.IsolatedStorageException>.  I criteri di protezione , modificabili tramite lo strumento .NET Framework Configuration \(Mscorcfg.msc\), determinano le autorizzazioni concesse al codice. Il codice a cui è stata concessa <xref:System.Security.Permissions.IsolatedStoragePermission> è limitato all'utilizzo di spazio di archiviazione non superiore a quanto consente la proprietà <xref:System.Security.Permissions.IsolatedStoragePermission.UserQuota%2A>. Poiché tuttavia il codice può eludere le quote presentando diverse identità utente, le quote rappresentano per il codice un limite indicativo piuttosto che un limite di protezione.  
  
 Le quote non si applicano agli archivi roaming. Perché il codice possa farne uso, occorre pertanto un livello di autorizzazione leggermente superiore. I valori di enumerazione <xref:System.Security.Permissions.IsolatedStorageContainment> e <xref:System.Security.Permissions.IsolatedStorageContainment> specificano un'autorizzazione a utilizzare lo spazio di memorizzazione isolato per un utente mobile.  
  
 [Torna all'inizio](#top)  
  
<a name="secure_access"></a>   
## Accesso sicuro  
 L'utilizzo dell'archiviazione isolata consente alle applicazioni parzialmente attendibili di archiviare i dati in modo controllato dal criterio di sicurezza del computer. Questa caratteristica si rivela particolarmente utile per l'esecuzione controllata di componenti scaricati. I criteri di sicurezza concedono raramente questo tipo di autorizzazione del codice quando si accede al file system utilizzando meccanismi di I\/O standard. Tuttavia, per impostazione predefinita, all'esecuzione di codice dal computer locale, da una rete locale o da Internet è concesso il diritto di utilizzare lo spazio di memorizzazione isolato.  
  
 Gli amministratori possono limitare lo spazio di archiviazione isolata a disposizione di un'applicazione o di un utente, in base a un appropriato livello di attendibilità. Gli amministratori possono inoltre rimuovere completamente i dati persistenti di un utente. Per creare o accedere a spazio di memorizzazione isolato è necessario che il codice disponga di un'autorizzazione <xref:System.Security.Permissions.IsolatedStorageFilePermission> appropriata.  
  
 Per accedere all'archiviazione isolata, il codice deve disporre di tutti i diritti nativi del sistema operativo della piattaforma. È necessario soddisfare gli elenchi di controllo di accesso \(ACL, Access Control List\) che determinano quali utenti dispongono dei diritti per l'utilizzo del file system. Le applicazioni .NET Framework dispongono già dei diritti del sistema operativo per accedere allo spazio di memorizzazione isolato, a meno che non eseguano la rappresentazione \(specifica della piattaforma\). In questo caso l'applicazione deve verificare che l'identità dell'utente impersonato disponga di appropriati diritti del sistema operativo per accedere all'archiviazione isolata. Tale tipo di accesso consente al codice in esecuzione o che viene scaricato dal Web di leggere e scrivere in un'area di archiviazione relativa a un particolare utente.  
  
 Per controllare l'accesso allo spazio di memorizzazione isolato, Common Language Runtime utilizza gli oggetti <xref:System.Security.Permissions.IsolatedStorageFilePermission>. Ogni oggetto dispone di proprietà che specificano i seguenti valori:  
  
-   Utilizzo consentito, che indica il tipo di accesso consentito. I valori sono i membri dell'enumerazione <xref:System.Security.Permissions.IsolatedStorageContainment>. Per ulteriori informazioni su questi valori, vedere la tabella nella sezione successiva.  
  
-   Quota di archiviazione, come illustrato nella sezione precedente.  
  
 Il runtime richiede l'autorizzazione <xref:System.Security.Permissions.IsolatedStorageFilePermission> la prima volta che il codice tenta di aprire un archivio. Decide quindi se concedere o meno questa autorizzazione in base al grado di attendibilità del codice. Se l'autorizzazione viene concessa, i valori di quota di archiviazione e di utilizzo consentito verranno determinati dai criteri di sicurezza e dalla richiesta avanzata dal codice per <xref:System.Security.Permissions.IsolatedStorageFilePermission>. I criteri di sicurezza vengono impostati mediante lo strumento .NET Framework Configuration \(Mscorcfg.msc\). Tutti i chiamanti nello stack di chiamate vengono controllati per garantire che ciascun chiamante disponga almeno dell'utilizzo consentito appropriato. Il runtime controlla inoltre la quota imposta al codice che ha aperto o creato l'archivio in cui si deve salvare il file. Se le condizioni vengono soddisfatte, verrà concessa l'autorizzazione. La quota viene controllata nuovamente ogni volta che un file viene scritto nell'archivio.  
  
 Non occorre che il codice dell'applicazione richieda l'autorizzazione, perché Common Language Runtime concederà qualsiasi <xref:System.Security.Permissions.IsolatedStorageFilePermission> appropriato in base ai criteri di sicurezza. Tuttavia, esistono buone ragioni per richiedere le autorizzazioni specifiche necessarie all'applicazione, comprese <xref:System.Security.Permissions.IsolatedStorageFilePermission>.  
  
 [Torna all'inizio](#top)  
  
<a name="allowed_usage"></a>   
## Utilizzo consentito e rischi di sicurezza  
 L'utilizzo consentito specificato da <xref:System.Security.Permissions.IsolatedStorageFilePermission> determina il grado in cui al codice verrà consentito di creare e utilizzare lo spazio di memorizzazione isolato. Nella tabella riportata di seguito viene illustrato come l'utilizzo consentito specificato nell'autorizzazione corrisponde ai tipi di isolamento. Vengono inoltre riepilogati i rischi di sicurezza associati a ciascun utilizzo consentito.  
  
|Utilizzo consentito|Tipi di isolamento|Impatto sulla sicurezza|  
|-------------------------|------------------------|-----------------------------|  
|<xref:System.Security.Permissions.IsolatedStorageContainment>|Non è consentito alcun utilizzo dell'archiviazione isolata.|Non vi è impatto per la sicurezza.|  
|<xref:System.Security.Permissions.IsolatedStorageContainment>|Isolamento in base all'utente, al dominio e all'assembly. Ciascun assembly presenta un archivio secondario all'interno del dominio. Gli archivi che utilizzano questa autorizzazione vengono isolati in modo implicito dal computer.|Questo livello di autorizzazione lascia le risorse vulnerabili all'utilizzo eccessivo non autorizzato, nonostante la resistenza offerta dall'adozione delle quote. Tale abuso viene definito denial of service \(negazione del servizio\).|  
|<xref:System.Security.Permissions.IsolatedStorageContainment>|Come `DomainIsolationByUser`, ma l'archivio viene salvato in un percorso di cui verrà effettuato il roaming se i profili degli utenti mobili sono attivati e le quote non sono applicate.|Poiché le quote devono essere disabilitate, le risorse di archiviazione sono più soggette ad attacchi denial of service.|  
|<xref:System.Security.Permissions.IsolatedStorageContainment>|Isolamento in base all'utente e all'assembly. Gli archivi che utilizzano questa autorizzazione vengono isolati in modo implicito dal computer.|A questo livello vengono attivate le quote, per offrire una maggior resistenza agli attacchi denial of service. Lo stesso assembly in esecuzione in un altro dominio può accedere a questo archivio, rendendo possibile la fuga di informazioni tra applicazioni.|  
|<xref:System.Security.Permissions.IsolatedStorageContainment>|Come `AssemblyIsolationByUser`, ma l'archivio viene salvato in un percorso di cui verrà effettuato il roaming se i profili degli utenti mobili sono attivati e le quote non sono applicate.|Come `AssemblyIsolationByUser`, ma senza quote. Aumenta il rischio che i servizi vengano attaccati.|  
|<xref:System.Security.Permissions.IsolatedStorageContainment>|Isolamento in base all'utente. In genere questo livello di autorizzazione viene utilizzato solo per gli strumenti di debug e di amministrazione.|L'accesso con questa autorizzazione consente al codice di visualizzare o rimuovere i file o le directory dell'archiviazione isolata di un utente, indipendentemente dall'isolamento dell'assembly. I rischi includono, tra l'altro, la fuga di informazioni e la perdita di dati.|  
|<xref:System.Security.Permissions.IsolatedStorageContainment>|Isolamento in base a tutti gli utenti, i domini e gli assembly. In genere questo livello di autorizzazione viene utilizzato solo per gli strumenti di debug e di amministrazione.|Questa autorizzazione crea la possibilità che vengano compromessi tutti gli archivi isolati di tutti gli utenti.|  
  
 [Torna all'inizio](#top)  
  
<a name="isolated_storage_locations"></a>   
## Percorsi dello spazio di memorizzazione isolato  
 Talvolta risulta utile verificare una modifica nello spazio di memorizzazione isolato utilizzando il file system del sistema operativo. È possibile che si voglia conoscere il percorso dei file di spazio di memorizzazione isolato. Il percorso varia in base al sistema operativo. Nella tabella che segue vengono illustrati i percorsi principali in cui viene creata l'archiviazione isolata in alcuni sistemi operativi. Cercare la directory Microsoft\\IsolatedStorage in questo percorso radice. Per visualizzare cartelle e file nascosti, in modo da poter individuare l'archiviazione isolata nel file system, è necessario modificare le impostazioni della cartella.  
  
|Sistema operativo|Percorso nel file system|  
|-----------------------|------------------------------|  
|Windows 2000, Windows XP, Windows Server 2003 \- \(aggiornamento da Windows NT 4.0\)|Archivi con supporto roaming \=<br /><br /> \<SYSTEMROOT\>\\Profiles\\\<utente\>\\Application Data<br /><br /> Archivi non abilitati al roaming \=<br /><br /> \<SYSTEMROOT\>\\Profiles\\\<utente\>\\Local Settings\\Application Data|  
|Windows 2000 \- installazione pulita \(e aggiornamenti da Windows 98 e Windows NT 3.51\)|Archivi con supporto roaming \=<br /><br /> \<SYSTEMDRIVE\>\\Documents and Settings\\\<utente\>\\Application Data<br /><br /> Archivi non abilitati al roaming \=<br /><br /> \<SYSTEMDRIVE\>\\Documents and Settings\\\<utente\>\\Local Settings\\Application Data|  
|Windows XP, Windows Server 2003 \- installazione pulita \(e aggiornamenti da Windows 2000 e Windows 98\)|Archivi con supporto roaming \=<br /><br /> \<SYSTEMDRIVE\>\\Documents and Settings\\\<utente\>\\Application Data<br /><br /> Archivi non abilitati al roaming \=<br /><br /> \<SYSTEMDRIVE\>\\Documents and Settings\\\<utente\>\\Local Settings\\Application Data|  
|[!INCLUDE[win8](../../../includes/win8-md.md)], Windows 7, Windows Server 2008, Windows Vista|Archivi con supporto roaming \=<br /><br /> \<SYSTEMDRIVE\>\\Users\\\<utente\>\\AppData\\Roaming<br /><br /> Archivi non abilitati al roaming \=<br /><br /> \<SYSTEMDRIVE\>\\Users\\\<utente\>\\AppData\\Local|  
  
 [Torna all'inizio](#top)  
  
<a name="isolated_storage_tasks"></a>   
## Creazione, enumerazione ed eliminazione dello spazio di memorizzazione isolato  
 .NET Framework fornisce tre classi dello spazio dei nomi <xref:System.IO.IsolatedStorage> per aiutare ad eseguire attività che coinvolgono lo spazio di memorizzazione isolato:  
  
-   <xref:System.IO.IsolatedStorage.IsolatedStorageFile>, che deriva da <xref:System.IO.IsolatedStorage.IsolatedStorage?displayProperty=fullName> e fornisce la gestione di base di file di applicazione e assembly archiviati. Un'istanza della classe <xref:System.IO.IsolatedStorage.IsolatedStorageFile> rappresenta un singolo archivio contenuto nel file system.  
  
-   <xref:System.IO.IsolatedStorage.IsolatedStorageFileStream>, che deriva da <xref:System.IO.FileStream?displayProperty=fullName> e fornisce l'accesso ai file di un archivio.  
  
-   <xref:System.IO.IsolatedStorage.IsolatedStorageScope> è un'enumerazione che consente di creare e selezionare un archivio con il tipo di isolamento appropriato.  
  
 Le classi di archiviazione isolata consentono di creare, enumerare ed eliminare l'archiviazione isolata. I metodi per l'esecuzione di queste attività sono disponibili tramite l'oggetto <xref:System.IO.IsolatedStorage.IsolatedStorageFile>. Per alcune operazioni occorre disporre dell'autorizzazione <xref:System.Security.Permissions.IsolatedStorageFilePermission>, che rappresenta il diritto di amministrare lo spazio di memorizzazione isolato. Potrebbero essere necessari anche i diritti di sistema operativo per accedere al file o alla directory.  
  
 Per una serie di esempi che illustrano le attività dello spazio di memorizzazione isolato comuni, vedere gli argomenti relativi alle procedure elencati in [Argomenti correlati](#related_topics).  
  
 [Torna all'inizio](#top)  
  
<a name="scenarios_for_isolated_storage"></a>   
## Scenari per l'utilizzo dell'archiviazione isolata  
 Lo spazio di memorizzazione isolato risulta utile in molte situazioni, inclusi i seguenti quattro scenari:  
  
-   Controlli di cui è stato eseguito il download. Ai controlli di codice gestito scaricati da Internet non è consentito scrivere sul disco fisso mediante le normali classi di I\/O, ma è permesso l'utilizzo dell'archiviazione isolata per la memorizzazione degli stati dell'applicazione e delle impostazioni dell'utente.  
  
-   Archiviazione di componenti condivisi. I componenti condivisi tra le applicazioni possono utilizzare l'archiviazione isolata per fornire accesso controllato agli archivi di dati.  
  
-   Archiviazione server. Le applicazioni server possono utilizzare l'archiviazione isolata per fornire singoli archivi a un ampio numero di utenti che inoltrano richieste all'applicazione. Poiché l'archiviazione isolata è sempre isolata dall'utente, il server deve impersonare l'utente che inoltra la richiesta. In questo caso, i dati vengono isolati in base all'identità del principale, che è la stessa usata dall'applicazione per distinguere gli utenti.  
  
-   Roaming. Le applicazioni possono anche utilizzare l'archiviazione isolata con i profili di utente roaming. In questo modo gli archivi isolati di un utente possono spostarsi con il profilo.  
  
 Non utilizzare lo spazio di memorizzazione isolato nelle seguenti situazioni:  
  
-   Per archiviare informazioni segrete di grande importanza quali password o chiavi non crittografate, in quanto lo spazio di memorizzazione isolato non è protetto da codice a elevata attendibilità, da codice non gestito o da utenti attendibili del computer.  
  
-   Per archiviare codice.  
  
-   Per salvare le impostazioni di distribuzione e di configurazione controllate dagli amministratori. Si noti che le preferenze utente non sono considerate impostazioni di configurazione, poiché gli amministratori non le controllano.  
  
 Molte applicazioni utilizzano un database per memorizzare e isolare dati. In questo caso una o più righe di un database possono rappresentare l'archiviazione di un utente specifico. È possibile utilizzare l'archiviazione isolata invece di un database quando il numero di utenti è ridotto, quando l'overhead per l'utilizzo di un database è notevole o quando non si dispone di un database. Inoltre, l'archiviazione isolata rappresenta una valida alternativa quando l'applicazione richiede un'archiviazione più flessibile e complessa di quanto non consenta una riga in un database.  
  
 [Torna all'inizio](#top)  
  
<a name="related_topics"></a>   
## Argomenti correlati  
  
|Titolo|Descrizione|  
|------------|-----------------|  
|[Tipi di isolamento](../../../docs/standard/io/types-of-isolation.md)|Vengono descritti i vari tipi di isolamento.|  
|[Procedura: Recuperare archivi per lo spazio di memorizzazione isolato](../../../docs/standard/io/how-to-obtain-stores-for-isolated-storage.md)|Viene fornito un esempio di utilizzo della classe <xref:System.IO.IsolatedStorage.IsolatedStorageFile> per ottenere uno spazio di memorizzazione isolato in base all'utente e all'assembly.|  
|[Procedura: Enumerare gli archivi per lo spazio di memorizzazione isolato](../../../docs/standard/io/how-to-enumerate-stores-for-isolated-storage.md)|Viene illustrato come utilizzare il metodo <xref:System.IO.IsolatedStorage.IsolatedStorageFile.GetEnumerator%2A?displayProperty=fullName> per calcolare la dimensione dell'intero spazio di memorizzazione isolato dell'utente.|  
|[Procedura: Eliminare gli archivi nello spazio di memorizzazione isolato](../../../docs/standard/io/how-to-delete-stores-in-isolated-storage.md)|Vengono illustrati i due possibili utilizzi del metodo <xref:System.IO.IsolatedStorage.IsolatedStorageFile.Remove%2A?displayProperty=fullName> per l'eliminazione degli spazi di memorizzazione isolati.|  
|[Procedura: Anticipare le condizioni di spazio insufficiente con lo spazio di memorizzazione isolato](../../../docs/standard/io/how-to-anticipate-out-of-space-conditions-with-isolated-storage.md)|Viene illustrato come misurare lo spazio rimanente in un archivio isolato.|  
|[Procedura: Creare file e directory nello spazio di memorizzazione isolato](../../../docs/standard/io/how-to-create-files-and-directories-in-isolated-storage.md)|Vengono forniti alcuni esempi di creazione di file e directory in un archivio isolato.|  
|[Procedura: Trovare file e directory esistenti nello spazio di memorizzazione isolato](../../../docs/standard/io/how-to-find-existing-files-and-directories-in-isolated-storage.md)|Viene illustrato come leggere la struttura di directory e i file dell'archiviazione isolata.|  
|[Procedura: leggere e scrivere sui file nello spazio di memorizzazione isolato](../../../docs/standard/io/how-to-read-and-write-to-files-in-isolated-storage.md)|Viene fornito un esempio di scrittura e rilettura di una stringa in un file di spazio di memorizzazione isolato.|  
|[Procedura: Eliminare file e directory nello spazio di memorizzazione isolato](../../../docs/standard/io/how-to-delete-files-and-directories-in-isolated-storage.md)|Viene illustrato come eliminare file e directory di uno spazio di memorizzazione isolato.|  
|[I\/O di file e di flussi](../../../docs/standard/io/index.md)|Illustra le modalità di esecuzione di un file sincrono e asincrono e dell'accesso al flusso di dati.|  
  
<a name="reference"></a>   
## Riferimento  
 <xref:System.IO.IsolatedStorage.IsolatedStorage?displayProperty=fullName>  
  
 <xref:System.IO.IsolatedStorage.IsolatedStorageFile?displayProperty=fullName>  
  
 <xref:System.IO.IsolatedStorage.IsolatedStorageFileStream?displayProperty=fullName>  
  
 <xref:System.IO.IsolatedStorage.IsolatedStorageScope?displayProperty=fullName>