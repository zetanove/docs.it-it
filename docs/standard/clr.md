---
title: "Common Language Runtime (CLR) | Microsoft Docs"
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
  - ".NET Framework, Common Language Runtime"
  - "codice, esecuzione"
  - "codice, funzionalità di runtime"
  - "Common Language Runtime"
  - "compilazione di codice sorgente, funzionalità di runtime"
  - "compilatori di linguaggio"
  - "codice gestito"
  - "dati gestiti"
  - "metadati, funzionalità di runtime"
  - "runtime"
  - "esecuzione di codice sorgente"
ms.assetid: 059a624e-f7db-4134-ba9f-08b676050482
caps.latest.revision: 24
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 18
---
# Common Language Runtime (CLR)
In .NET Framework viene fornito un ambiente di runtime, denominato Common Language Runtime, in cui viene eseguito il codice e vengono offerti servizi che facilitano il processo di sviluppo.  
  
 I compilatori e gli strumenti dei linguaggi espongono le funzionalità di Common Language Runtime e consentono di scrivere codice che sfrutta i vantaggi di tale ambiente di esecuzione gestito.  Il codice sviluppato tramite un compilatore di linguaggio basato su Common Language Runtime viene definito codice gestito e si avvantaggia di funzionalità quali l'integrazione tra i linguaggi, la gestione delle eccezioni con linguaggi diversi, la sicurezza avanzata, il supporto per il controllo delle versioni e la distribuzione, un modello semplificato per l'interazione tra componenti e servizi di debug e di profilatura.  
  
> [!WARNING]
>  I compilatori e gli strumenti sono in grado di produrre un output che può essere usato da Common Language Runtime perché il sistema di tipi, il formato dei metadati e l'ambiente di runtime \(il sistema di esecuzione virtuale\) sono tutti definiti da uno standard pubblico, la specifica di ECMA Common Language Infrastructure.  Per altre informazioni, vedere la pagina relativa alle [specifiche ECMA C\# e Common Language Infrastructure](http://go.microsoft.com/fwlink/?LinkId=99212).  
  
 Per consentire all'ambiente di esecuzione di fornire servizi al codice gestito, è necessario che i compilatori di linguaggio generino metadati che descrivono i tipi, i membri e i riferimenti presenti nel codice.  I metadati sono memorizzati con il codice: ogni file eseguibile trasportabile \(PE, Portable Executable\) caricabile in Common Language Runtime contiene metadati.  I metadati vengono usati nell'ambiente di esecuzione per individuare e caricare classi, disporre istanze in memoria, risolvere chiamate di metodo, generare codice nativo, garantire sicurezza e impostare limiti di contesto per la fase di esecuzione.  
  
 Il layout degli oggetti e i riferimenti agli oggetti vengono gestiti automaticamente: quando non sono più in uso, gli oggetti vengono rilasciati.  Gli oggetti la cui durata viene amministrata con queste modalità vengono denominati dati gestiti.  La procedura di Garbage Collection consente di eliminare il rischio di perdite di memoria e di altri errori comuni di programmazione.  Se si impiega codice gestito, è possibile usare nell'applicazione .NET Framework sia dati gestiti che dati non gestiti, anche simultaneamente.  Dal momento che i compilatori di linguaggio forniscono autonomamente tipi, quali i tipi primitivi, è possibile che non sempre lo sviluppatore sappia, o abbia l'esigenza di sapere, se i dati che usa sono gestiti.  
  
 Common Language Runtime facilita la progettazione di componenti e applicazioni i cui oggetti interagiscano in contesti di linguaggi diversi.  Oggetti scritti in linguaggi differenti possono infatti interagire e funzionare in modo strettamente integrato.  Una volta definita una classe, ad esempio, è possibile usare un linguaggio differente per derivarne un'altra classe o per chiamarvi un metodo.  È anche possibile passare l'istanza di una classe al metodo di una classe scritta in un linguaggio differente.  Questa integrazione tra linguaggi è possibile perché i compilatori e gli strumenti dei linguaggi destinati alla fase di esecuzione usano un sistema di tipi comuni, definito dall'ambiente di esecuzione, e seguono le regole di tale ambiente per la definizione di nuovi tipi, oltre che per la creazione, l'utilizzo, il mantenimento e l'associazione a tipi.  
  
 In quanto parte dei rispettivi metadati, tutti i componenti gestiti contengono informazioni sui componenti e le risorse in base ai quali sono stati compilati.  Il runtime usa tali informazioni per garantire la disponibilità delle versioni specificate del software necessario al funzionamento del componente o dell'applicazione, riducendo così il rischio di interruzioni del codice dovute all'irreperibilità di alcune dipendenze.  Le informazioni di registrazione e i dati dello stato non vengono più memorizzati nel Registro di sistema, in cui poteva essere difficile individuarli e gestirli.  Le informazioni sui tipi definiti e sulle relative dipendenze vengono invece archiviate con il codice in forma di metadati, semplificando di gran lunga le attività di replica e rimozione di componenti.  
  
 I compilatori e gli strumenti dei linguaggi sono progettati per esporre le funzionalità del runtime secondo modalità utili e intuitive per gli sviluppatori.  Alcune di queste funzionalità potrebbero quindi essere più evidenti in un ambiente operativo anziché in un altro.  Il modo di percepire il funzionamento dell'ambiente di esecuzione dipende dai compilatori o dagli strumenti dei linguaggi usati.  Lo sviluppatore in Visual Basic, ad esempio, potrà rilevare in questo linguaggio una maggiore presenza di funzionalità orientate a oggetti, conferitagli da Common Language Runtime.  Il runtime offre i vantaggi seguenti:  
  
-   Miglioramenti delle prestazioni.  
  
-   La possibilità di usare con facilità componenti sviluppati in altri linguaggi.  
  
-   La disponibilità dei tipi estensibili forniti da una libreria di classi.  
  
-   Funzionalità del linguaggio come ereditarietà, interfacce e overload per la programmazione orientata a oggetti.  
  
-   Supporto per il modello di threading Free esplicito che consente la creazione di applicazioni scalabili a thread multipli.  
  
-   Supporto per la gestione delle eccezioni strutturata.  
  
-   Supporto per gli attributi personalizzati.  
  
-   Garbage Collection.  
  
-   Utilizzo dei delegati invece dei puntatori a funzioni con conseguente miglioramento dell'indipendenza dai tipi e della sicurezza dei tipi.  Per altre informazioni sui delegati, vedere [Common Type System](../../docs/standard/base-types/common-type-system.md).  
  
## Versioni di Common Language Runtime  
 Il numero di versione di .NET Framework non corrisponde necessariamente al numero di versione di CLR inclusa.  Nella tabella seguente viene mostrata la correlazione tra due numeri di versione.  
  
|Versione di .NET Framework|Include la versione CLR|  
|--------------------------------|-----------------------------|  
|1.0|1.0|  
|1.1|1.1|  
|2.0|2.0|  
|3.0|2.0|  
|3.5|2.0|  
|4|4|  
|4.5 \(incluse 4.5.1 e 4.5.2\)|4|  
  
## Argomenti correlati  
  
|Titolo|Descrizione|  
|------------|-----------------|  
|[Processo di esecuzione gestita](../../docs/standard/managed-execution-process.md)|Vengono descritti i passaggi necessari per essere in condizione di sfruttare i vantaggi di Common Language Runtime.|  
|[Gestione automatica della memoria](../../docs/standard/automatic-memory-management.md)|Viene descritta la modalità usata dal Garbage Collector per allocare e liberare memoria.|  
|[NIB: Overview of the .NET Framework](http://msdn.microsoft.com/it-it/ea38ac1e-92af-4d1b-8db1-e8a5ea10ed85)|Vengono descritti i concetti principali di .NET Framework quali Common Type System, l'interoperabilità tra più linguaggi, l'esecuzione gestita, i domini delle applicazioni e gli assembly.|  
|[Common Type System](../../docs/standard/base-types/common-type-system.md)|Vengono descritte le modalità di dichiarazione, utilizzo e gestione dei tipi nell'ambiente di esecuzione in supporto all'integrazione tra i linguaggi.|  
  
## Vedere anche  
 [Versioni e dipendenze](../../docs/framework/migration-guide/versions-and-dependencies.md)