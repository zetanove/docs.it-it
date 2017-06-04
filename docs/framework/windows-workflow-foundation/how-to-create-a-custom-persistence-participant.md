---
title: "Procedura: creare un partecipante di persistenza personalizzato | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1d9cc47a-8966-4286-94d5-4221403d9c06
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Procedura: creare un partecipante di persistenza personalizzato
Nella procedura riportata di seguito sono illustrati i passaggi per creare un partecipante di persistenza.Per informazioni sulle implementazioni dei partecipanti di persistenza, vedere l'esempio [Participating in Persistence](http://go.microsoft.com/fwlink/?LinkID=177735) e l'argomento [Estensibilità dell'archivio](../../../docs/framework/windows-workflow-foundation//store-extensibility.md).  
  
1.  Creare una classe che deriva dalla classe <xref:System.Activities.Persistence.PersistenceParticipant> o <xref:System.Activities.Persistence.PersistenceIOParticipant>.Oltre alla possibilità di partecipare alle operazioni di IO, la classe PersistenceIOParticipant dispone degli stessi punti di estensibilità della classe PersistenceParticipant.Attenersi ad almeno uno dei passaggi seguenti.  
  
2.  Implementare il metodo <xref:System.Activities.Persistence.PersistenceParticipant.CollectValues%2A>.Il metodo **CollectValues** dispone di due parametri di dizionario, uno per l'archiviazione di valori di lettura\/scrittura e l'altro per l'archiviazione di valori di sola scrittura \(utilizzati di seguito nelle query\).In tale metodo, è necessario popolare questi dizionari con i dati specifici di un partecipante di persistenza.Ogni dizionario contiene il nome del valore come chiave e il valore stesso come oggetto <xref:System.Runtime.DurableInstancing.InstanceValue>.  
  
     I valori del dizionario readWriteValues vengono impacchettati come oggetti **InstanceValue**,mentre i valori del dizionario di sola scrittura vengono impacchettati come oggetti **InstanceValue** con gli oggetti InstanceValueOptions.Optional e InstanceValueOption.WriteOnly impostati.Il nome di ogni oggetto **InstanceValue** fornito dalle implementazioni **CollectValues** in tutti i partecipanti di persistenza deve essere univoco.  
  
    ```  
    protected virtual void CollectValues (out IDictionary<XName,Object> readWriteValues, out IDictionary<XName,Object> writeOnlyValues)  
  
    ```  
  
3.  Implementare il metodo <xref:System.Activities.Persistence.PersistenceParticipant.MapValues%2A>.Il metodo **MapValues** accetta due parametri simili ai parametri ricevuti dal metodo **CollectValues**.Tutti i valori raccolti nella fase **CollectValues** vengono passati tramite questi parametri di dizionario.I nuovi valori aggiunti dalla fase **MapValues** vengono aggiunti ai valori di sola scrittura.Il dizionario di sola scrittura viene utilizzato per fornire dati a un'origine esterna non direttamente associata ai valori dell'istanza.Il nome di ogni valore fornito dalle implementazioni del metodo **MapValues** in tutti i partecipanti di persistenza deve essere univoco.  
  
    ```  
    protected virtual IDictionary<XName,Object> MapValues (IDictionary<XName,Object> readWriteValues,IDictionary<XName,Object> writeOnlyValues)  
    ```  
  
     Il metodo <xref:System.Activities.Persistence.PersistenceParticipant.MapValues%2A> fornisce la funzionalità che non è offerta da <xref:System.Activities.Persistence.PersistenceParticipant.CollectValues%2A>, nel senso che consente di utilizzare una dipendenza da un altro valore fornito da un altro partecipante di persistenza che non è stato ancora elaborato da <xref:System.Activities.Persistence.PersistenceParticipant.CollectValues%2A>.  
  
4.  Implementare il metodo **PublishValues**.Il metodo **PublishValues** riceve un dizionario contenente tutti i valori caricati dall'archivio di persistenza.  
  
    ```  
    protected virtual void PublishValues (IDictionary<XName,Object> readWriteValues)  
  
    ```  
  
5.  Implementare il metodo **BeginOnSave** se il partecipante è un partecipante di IO di persistenza.Questo metodo viene chiamato durante un'operazione di salvataggio.In questo metodo, è necessario eseguire l'aggiunta di IO alla persistenza delle istanze del flusso di lavoro \(salvataggio\).Se l'host sta utilizzando una transazione per il comando di persistenza corrispondente, la stessa transazione viene fornita in Transaction.Current.Inoltre, l'oggetto PersistenceIOParticipants può annunciare un requisito di coerenza transazionale e, in tal caso, l'host crea una transazione per l'episodio di persistenza, qualora non venisse altrimenti utilizzata.  
  
    ```  
  
    protected virtual IAsyncResult BeginOnSave (IDictionary<XName,Object> readWriteValues, IDictionary<XName,Object> writeOnlyValues, TimeSpan timeout, AsyncCallback callback, Object state)  
    ```  
  
6.  Implementare il metodo **BeginOnLoad** se il partecipante è un partecipante di IO di persistenza.Questo metodo viene chiamato durante un'operazione di caricamento.In questo metodo, è necessario eseguire l'aggiunta di IO al caricamento delle istanze del flusso di lavoro.Se l'host sta utilizzando una transazione per il comando di persistenza corrispondente, la stessa transazione viene fornita in Transaction.Current.Inoltre, i partecipanti di IO di persistenza possono annunciare un requisito di coerenza transazionale e, in tal caso, l'host crea una transazione per l'episodio di persistenza, qualora non venisse altrimenti utilizzata.  
  
    ```  
  
    protected virtual IAsyncResult BeginOnLoad (IDictionary<XName,Object> readWriteValues, TimeSpan timeout, AsyncCallback callback, Object state)  
  
    ```