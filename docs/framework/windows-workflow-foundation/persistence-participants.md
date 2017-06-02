---
title: "Partecipanti di persistenza | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f84d2d5d-1c1b-4f19-be45-65b552d3e9e3
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# Partecipanti di persistenza
Un partecipante di persistenza può far parte di un'operazione di persistenza \(Save o Load\) attivata da un'applicazione host.In [!INCLUDE[netfx_current_long](../../../includes/netfx-current-long-md.md)] sono disponibili due classi astratte, **PersistenceParticipant** e **PersistenceIOParticipant**, che possono essere utilizzate per creare un partecipante di persistenza.Un partecipante di persistenza deriva da una di queste classi, implementa i metodi di interesse, quindi aggiunge un'istanza della classe alla raccolta <xref:System.ServiceModel.Activities.WorkflowServiceHost.WorkflowExtensions%2A> nell'oggetto <xref:System.ServiceModel.Activities.WorkflowServiceHost>.L'applicazione host può cercare tali estensioni del flusso di lavoro quando rende persistente un'istanza del flusso di lavoro e richiamare metodi appropriati sui partecipanti di persistenza in momenti appropriati.  
  
 Nell'elenco seguente vengono descritte le attività eseguite dal sottosistema di persistenza in fasi diverse dell'operazione Persist \(Save\).I partecipanti di persistenza vengono utilizzati nella terza e quarta fase.Se il partecipante è un partecipante di IO, ovvero un partecipante di persistenza che fa parte anche di operazioni di IO, viene utilizzato anche nella sesta fase.  
  
1.  Raccoglie i valori predefiniti, inclusi lo stato del flusso di lavoro, i segnalibri, le variabili mappate e il timestamp.  
  
2.  Raccoglie tutti i partecipanti di persistenza aggiunti alla raccolta di estensioni associata all'istanza del flusso di lavoro.  
  
3.  Richiama il metodo <xref:System.Activities.Persistence.PersistenceParticipant.CollectValues%2A> implementato da tutti i partecipanti di persistenza.  
  
4.  Richiama il metodo <xref:System.Activities.Persistence.PersistenceParticipant.MapValues%2A> implementato da tutti i partecipanti di persistenza.  
  
5.  Rende persistente o salva il flusso di lavoro nell'archivio di persistenza.  
  
6.  Richiama il metodo <xref:System.Activities.Persistence.PersistenceIOParticipant.BeginOnSave%2A> su tutti i partecipanti di IO di persistenza.Se il partecipante non è un partecipante di IO, questa attività viene ignorata.Se l'episodio di persistenza è transazionale, la transazione viene fornita nella proprietà Transaction.Current.  
  
7.  Attende il completamento di tutti i partecipanti di persistenza.Se tutti i partecipanti riescono a rendere persistenti i dati dell'istanza, esegue il commit della transazione.  
  
 Un partecipante di persistenza deriva dalla classe **PersistenceParticipant** e può implementare i metodi **CollectValues** e **MapValues**.Un partecipante di IO di persistenza deriva dalla classe **PersistenceIOParticipant** e può implementare il metodo **BeginOnSave** oltre ai metodi **CollectValues** e **MapValues**.  
  
 Ogni fase viene completata prima dell'inizio della fase successiva.Ad esempio i valori vengono raccolti da **tutti** i partecipanti di persistenza nella prima fase.Quindi tutti i valori raccolti nella prima fase vengono forniti a tutti i partecipanti di persistenza nella seconda fase per il mapping.Successivamente tutti i valori raccolti e mappati nella prima e seconda fase vengono forniti al provider di persistenza nella terza fase e così via.  
  
 Nell'elenco seguente vengono descritte le attività eseguite dal sottosistema di persistenza in fasi diverse dell'operazione Load.I partecipanti di persistenza vengono utilizzati nella quarta fase.I partecipanti di IO di persistenza, ovvero i partecipanti di persistenza che fanno parte anche di operazioni di IO, vengono utilizzati anche nella terza fase.  
  
1.  Raccoglie tutti i partecipanti di persistenza aggiunti alla raccolta di estensioni associata all'istanza del flusso di lavoro.  
  
2.  Carica il flusso di lavoro dall'archivio di persistenza.  
  
3.  Richiama il metodo <xref:System.Activities.Persistence.PersistenceIOParticipant.BeginOnLoad%2A> su tutti i partecipanti di IO di persistenza e attende il completamento di tutti i partecipanti di persistenza.Se l'episodio di persistenza è transazionale, la transazione viene fornita nell'oggetto Transaction.Current.  
  
4.  Carica l'istanza del flusso di lavoro in memoria in base ai dati recuperati dall'archivio di persistenza.  
  
5.  Richiama il metodo <xref:System.Activities.Persistence.PersistenceParticipant.PublishValues%2A> su ogni partecipante di persistenza.  
  
 Un partecipante di persistenza deriva dalla classe **PersistenceParticipant** e può implementare il metodo **PublishValues**.Un partecipante di IO di persistenza deriva dalla classe **PersistenceIOParticipant** e può implementare il metodo **BeginOnLoad** oltre al metodo **PublishValues**.  
  
 Quando si carica un'istanza del flusso di lavoro, il provider di persistenza crea un blocco su tale istanza.In questo modo l'istanza non può essere caricata da più di un host in uno scenario che presenta molteplici nodi.Se si tenta di caricare un'istanza del flusso di lavoro bloccata, verrà generata un'eccezione analoga alla seguente: Eccezione "System.ServiceModel.Persistence.InstanceLockException: Impossibile completare l'operazione richiesta perché non è possibile acquisire il blocco dell'istanza "00000000\-0000\-0000\-0000\-000000000000".Generalmente questo errore si verifica in presenza di una delle seguenti condizioni:  
  
-   In uno scenario a molteplici nodi l'istanza viene caricata da un altro host.Esistono alcuni modi per risolvere questi tipi di conflitti: inoltrare l'elaborazione al nodo proprietario del blocco e tentare o forzare il caricamento, che impedirà all'altro host di salvare il lavoro.  
  
-   In uno scenario a nodo singolo l'host si è arrestato in modo anomalo.Quando un host viene riavviato \(riciclo di un processo o creando una nuova factory del provider di persistenza\), il nuovo host tenta di caricare un'istanza che però è ancora bloccata dall'host precedente poiché il blocco non è ancora scaduto.  
  
-   In uno scenario a nodo singolo, l'istanza in questione è stata interrotta a un certo punto e viene creata una nuova istanza del provider di persistenza con un ID host differente.  
  
 Il valore di timeout del blocco predefinito è 5 minuti; è possibile specificare un valore di timeout diverso quando viene chiamato il metodo <xref:System.ServiceModel.Persistence.PersistenceProvider.Load%2A>.  
  
## In questa sezione  
  
-   [Procedura: creare un partecipante di persistenza personalizzato](../../../docs/framework/windows-workflow-foundation//how-to-create-a-custom-persistence-participant.md)  
  
## Vedere anche  
 [Estensibilità dell'archivio](../../../docs/framework/windows-workflow-foundation//store-extensibility.md)