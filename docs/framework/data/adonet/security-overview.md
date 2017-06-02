---
title: "Cenni preliminari sulla sicurezza | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 33e09965-61d5-48cc-9e8c-3b047cc4f194
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Cenni preliminari sulla sicurezza
La protezione di un'applicazione è un processo costante.  Lo sviluppatore non sarà mai in grado di garantire l'assoluta sicurezza di un'applicazione da tutti gli attacchi, in quanto non è possibile prevedere i tipi di attacchi che consentiranno di elaborare le nuove tecnologie.  Al contrario, proprio perché nessuno ha ancora individuato \(o pubblicato\) i punti deboli nella sicurezza di un sistema, questo non implica che non ne esista nessuno.  Durante la fase di progettazione del progetto è necessario pianificare la sicurezza nonché le procedure previste di manutenzione per l'intera durata dell'applicazione.  
  
## Progettazione della sicurezza  
 Uno dei problemi principali per lo sviluppo di applicazioni protette è che la sicurezza è spesso un processo che viene implementato in una fase successiva al completamento del codice di un progetto.  Se la sicurezza non viene incorporata nella fase iniziale, l'applicazione non sarà protetta perché non sono stati valutati con attenzione tutti gli aspetti che la rendono tale.  
  
 Se la sicurezza viene implementata nella fase finale, si verificherà anche un maggior numero di bug, in quanto il software non sarà in grado di supportare le nuove restrizioni o dovrà essere riscritto per consentire l'inserimento di una funzionalità non prevista.  In ogni riga di codice modificato può essere introdotto un nuovo bug.  Per questo motivo, è necessario prendere in considerazione la sicurezza in una fase iniziale del processo di sviluppo, in modo che questo possa procedere congiuntamente allo sviluppo di nuove funzionalità.  
  
### Classificazione dei rischi  
 Non è possibile proteggere un sistema se non si comprendono tutti i potenziali attacchi ai quali è esposto.  Il processo di valutazione dei rischi per la sicurezza, denominato *classificazione dei rischi*, è necessario per determinare la probabilità e le implicazioni delle violazioni della sicurezza nell'applicazione ADO.NET.  
  
 La classificazione dei rischi si compone di tre passaggi generali: identificare il punto di vista dell'avversario, caratterizzare la sicurezza del sistema e determinare i rischi.  
  
 La classificazione dei rischi è un approccio iterativo alla valutazione delle vulnerabilità presenti nell'applicazione, il cui obiettivo è individuare quelle che sono più pericolose in quanto espongono i dati più sensibili.  Una volta identificate le vulnerabilità, è necessario classificarle in ordine di gravità e creare un set di contromisure, in ordine di priorità, per contrastare le minacce.  
  
 Per altre informazioni, vedere le risorse seguenti.  
  
|Risorsa|Descrizione|  
|-------------|-----------------|  
|Pagina Web sulla [classificazione dei rischi](http://go.microsoft.com/fwlink/?LinkId=98353) in MSDN Security Developer Center|Le risorse riportate in questa pagina contengono informazioni sul processo di classificazione dei rischi e consentono di compilare modelli di rischio da usare per proteggere le applicazioni|  
  
## Principio dei privilegi minimi  
 Durante la progettazione, la compilazione e la distribuzione di un'applicazione, è necessario presupporre che sarà sottoposta ad attacchi.  Spesso si tratta di attacchi di malware che viene eseguito con le autorizzazioni dell'utente che esegue il codice.  In altri casi derivano da codice corretto che è stato sfruttato da un utente non autorizzato.  Nel pianificare la sicurezza è opportuno presupporre sempre che possa verificarsi l'ipotesi più pessimistica.  
  
 Una delle contromisure da adottare è tentare di erigere quante più barriere possibile intorno al codice tramite l'esecuzione con privilegi minimi.  In base al principio dei privilegi minimi, ogni dato privilegio deve essere concesso per la quantità minima di codice necessario e per l'intervallo più breve di tempo richiesto per completare il lavoro.  
  
 La procedura consigliata per la creazione di applicazioni protette è iniziare senza autorizzazioni, quindi aggiungere le autorizzazioni minime per la specifica attività da eseguire.  Se invece si negano singole autorizzazioni dopo aver iniziato concedendole tutte, le applicazioni potrebbero risultare non protette, difficili da testare e mantenere nonché contenere problemi di sicurezza non intenzionali derivanti dalla concessione di un numero di autorizzazioni maggiore di quello necessario.  
  
 Per altre informazioni sulla protezione delle applicazioni, vedere le risorse seguenti.  
  
|Risorsa|Descrizione|  
|-------------|-----------------|  
|[Protezione delle applicazioni](../Topic/Securing%20Applications.md)|Contiene collegamenti ad argomenti generici sulla sicurezza,  oltre che ad argomenti per la protezione di applicazioni distribuite, Web, per PC portatili e per PC desktop.|  
  
## Sicurezza per l'accesso al codice \(CAS, Code Access Security\)  
 La sicurezza dall'accesso di codice è un meccanismo che consente di limitare l'accesso del codice alle risorse e alle operazioni protette.  In .NET Framework vengono svolte le seguenti funzioni:  
  
-   Definizione di autorizzazioni e set di autorizzazioni che rappresentano il diritto di accedere a varie risorse di sistema.  
  
-   Possibilità per gli amministratori di configurare criteri di sicurezza associando set di autorizzazioni a gruppi di codice.  
  
-   Possibilità di richiedere le autorizzazioni necessarie per l'esecuzione del codice, oltre a quelle che potrebbero migliorare il funzionamento, e di specificare le autorizzazioni che invece non devono essere mai concesse al codice.  
  
-   Concessione di autorizzazioni a ogni assembly caricato, in base alle autorizzazioni richieste dal codice e alle operazioni autorizzate dai criteri di sicurezza.  
  
-   Possibilità di esigere dai chiamanti del codice il possesso di autorizzazioni specifiche.  
  
-   Possibilità di esigere dai chiamanti del codice il possesso di una firma digitale, in modo che solo i chiamanti appartenenti a un'organizzazione o a un sito particolare siano autorizzati a chiamare il codice sicuro.  
  
-   Applicazione di restrizioni sul codice in fase di esecuzione confrontando le autorizzazioni concesse a ogni chiamante dello stack di chiamate con le autorizzazioni effettivamente necessarie.  
  
 Per minimizzare il quantità di danni che possono verificarsi se un attacco riesce, scegliere un contesto di sicurezza per il codice che conceda l'accesso solo alle risorse necessarie per completare il lavoro.  
  
 Per altre informazioni, vedere le risorse seguenti.  
  
|Risorsa|Descrizione|  
|-------------|-----------------|  
|[Sicurezza dall'accesso di codice e ADO.NET](../../../../docs/framework/data/adonet/code-access-security.md)|Vengono descritte le interazioni tra la sicurezza dall'accesso del codice, la sicurezza basata sui ruoli e gli ambienti parzialmente attendibili dal punto di vista delle applicazioni ADO.NET.|  
|[Code Access Security](http://msdn.microsoft.com/it-it/23a20143-241d-4fe5-9d9f-3933fd594c03)|Contiene collegamenti ad argomenti aggiuntivi in cui viene descritta la sicurezza dall'accesso di codice in .NET Framework.|  
  
## Sicurezza dei database  
 Il principio dei privilegi minimi si applica anche all'origine dati.  Le linee guida generali per la sicurezza dei database includono:  
  
-   Creare account con il livello di privilegi minimo possibile.  
  
-   Non consentire l'accesso ad account amministrativi solo per ottenere il funzionamento del codice.  
  
-   Non restituire i messaggi di errore lato server alle applicazioni client.  
  
-   Convalidare tutto l'input, sia nel client che nel server.  
  
-   Usare comandi con parametri ed evitare istruzioni SQL dinamiche.  
  
-   Abilitare le funzionalità di controllo della sicurezza e registrazione per il database in uso, in modo da ricevere avvisi in caso di violazioni della sicurezza.  
  
 Per altre informazioni, vedere le risorse seguenti.  
  
|Risorsa|Descrizione|  
|-------------|-----------------|  
|[Sicurezza di SQL Server](../../../../docs/framework/data/adonet/sql/sql-server-security.md)|Viene fornita una panoramica delle funzionalità di sicurezza di SQL Server, nonché scenari per la creazione di applicazioni ADO.NET protette da usare con SQL Server.|  
|[Recommendations for Data Access Strategies](http://msdn.microsoft.com/it-it/72411f32-d12a-4de8-b961-e54fca7faaf5)|Vengono forniti suggerimenti per l'accesso ai dati e l'esecuzione di operazioni di database.|  
  
## Amministrazione e criteri di sicurezza  
 Se i criteri di sicurezza dall'accesso di codice vengono amministrati in modo non corretto, possono verificarsi problemi di sicurezza.  Una volta distribuita l'applicazione, è necessario usare tecniche per il monitoraggio della sicurezza e valutare i rischi quando emergono nuove minacce.  
  
 Per altre informazioni, vedere le risorse seguenti.  
  
|Risorsa|Descrizione|  
|-------------|-----------------|  
|[NIB: Security Policy Management](http://msdn.microsoft.com/it-it/d754e05d-29dc-4d3a-a2c2-95eaaf1b82b9)|Fornisce informazioni sulla creazione e sull'amministrazione dei criteri di sicurezza.|  
|[NIB: Security Policy Best Practices](http://msdn.microsoft.com/it-it/d49bc4d5-efb7-4caa-a2fe-e4d3cec63c05)|Vengono forniti collegamenti ad argomenti in cui viene descritto come amministrare i criteri di sicurezza.|  
  
## Vedere anche  
 [Protezione di applicazioni ADO.NET](../../../../docs/framework/data/adonet/securing-ado-net-applications.md)   
 [PAVE Security in Native and .NET Framework Code](http://msdn.microsoft.com/it-it/bd61be84-c143-409a-a75a-44253724f784)   
 [Sicurezza di SQL Server](../../../../docs/framework/data/adonet/sql/sql-server-security.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)