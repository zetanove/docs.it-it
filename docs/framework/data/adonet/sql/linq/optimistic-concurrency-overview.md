---
title: "Cenni preliminari sulla concorrenza ottimistica | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c2e38512-d0c8-4807-b30a-cb7e30338694
caps.latest.revision: 2
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 2
---
# Cenni preliminari sulla concorrenza ottimistica
In [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] è supportato il controllo della concorrenza ottimistica.  Nella tabella seguente vengono descritti i termini applicabili alla concorrenza ottimistica nella documentazione di [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)]:  
  
|Termini|Descrizione|  
|-------------|-----------------|  
|concorrenza|Situazione in cui due o più utenti tentano contemporaneamente di aggiornare la stessa riga del database.|  
|conflitto di concorrenza|Situazione in cui due o più utenti tentano contemporaneamente di inviare valori in conflitto a una o più colonne di una riga.|  
|controllo della concorrenza|Tecnica usata per risolvere i conflitti di concorrenza.|  
|controllo di concorrenza ottimistica|Tecnica che consente di esaminare se i valori presenti in una riga in altre transazioni sono stati modificati prima di consentire l'invio di modifiche.<br /><br /> Si differenzia dal *controllo pessimistico della concorrenza*che blocca il record per evitare conflitti di concorrenza.<br /><br /> Il controllo *ottimistico* viene così definito perché considera improbabile la possibilità che una transazione interferisca con un'altra.|  
|risoluzione dei conflitti|Processo di aggiornamento di un elemento in conflitto mediante la riesecuzione di una query sul database e la risoluzione delle differenze.<br /><br /> Quando un oggetto viene aggiornato, la funzionalità di ricerca delle modifiche di [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] conserva i dati seguenti:<br /><br /> -   I valori rilevati in origine dal database e usati per il controllo degli aggiornamenti.<br />-   I nuovi valori del database dalla query successiva.<br /><br /> [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] determina quindi se l'oggetto è in conflitto, ovvero se uno o più valori del membro sono stati modificati.  Se l'oggetto è in conflitto, in [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] vengono determinati i membri in conflitto.<br /><br /> Qualsiasi conflitto fra membri individuato da [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] viene aggiunto a un elenco di conflitti.|  
  
 Nel modello a oggetti di [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] si verifica un *conflitto di concorrenza ottimistica* quando entrambe le condizioni seguenti sono vere:  
  
-   Il client tenta di inviare modifiche al database.  
  
-   Uno o più valori di controllo degli aggiornamenti sono stati aggiornati nel database dall'ultima lettura effettuata dal client.  
  
 Per risolvere questo conflitto, è necessario individuare i membri dell'oggetto in conflitto, quindi decidere come procedere.  
  
> [!NOTE]
>  Solo i membri di cui è stato eseguito il mapping come <xref:System.Data.Linq.Mapping.UpdateCheck> o <xref:System.Data.Linq.Mapping.UpdateCheck> fanno parte dei controlli di concorrenza ottimistica.  Per i membri contrassegnati come <xref:System.Data.Linq.Mapping.UpdateCheck> non viene eseguito alcun controllo.  Per altre informazioni, vedere <xref:System.Data.Linq.Mapping.UpdateCheck>.  
  
## Esempio  
 Nel seguente scenario, ad esempio, User1 prepara un aggiornamento mediante l'esecuzione di una query su una riga del database.  User1 riceve una riga con i valori Alfreds, Maria e Sales.  
  
 User1 desidera modificare il valore della colonna Manager in Alfred e il valore della colonna Department in Marketing.  Prima che User1 possa inviare le modifiche, User2 ha già inviato le proprie modifiche al database.  Ora il valore della colonna Assistant è stato modificato in Mary e il valore della colonna Department è cambiato in Service.  
  
 Quando User1 tenta di inviare le modifiche, l'invio non viene completato e viene generata un'eccezione <xref:System.Data.Linq.ChangeConflictException>.  Questo risultato si verifica perché i valori del database per le colonna Assistant e Department non sono quelli previsti.  I membri che rappresentano le colonne Assistant e Department sono in conflitto.  Nella tabella seguente è riepilogata questa situazione:  
  
||Manager|Assistant|Department|  
|------|-------------|---------------|----------------|  
|Stato originale|Alfreds|Maria|Sales|  
|Utente1|Alfred||Marketing|  
|User2||Mary|Servizio|  
  
 È possibile risolvere questo tipo di conflitti in diversi modi.  Per altre informazioni, vedere [Procedura: gestire i conflitti di modifiche](../../../../../../docs/framework/data/adonet/sql/linq/how-to-manage-change-conflicts.md).  
  
## Elenco di controllo per il rilevamento e la risoluzione dei conflitti  
 È possibile rilevare e risolvere i conflitti a qualsiasi livello di dettaglio.  Da una parte è possibile risolvere tutti i conflitti usando una delle tre modalità disponibili \(vedere <xref:System.Data.Linq.RefreshMode>\) senza ulteriori considerazioni.  Dall'altra è possibile definire un'azione specifica per ogni tipo di conflitto e per ogni membro in conflitto.  
  
-   Specificare o modificare le opzioni per <xref:System.Data.Linq.Mapping.UpdateCheck> nel modello a oggetti.  
  
     Per altre informazioni, vedere [Procedura: specificare i membri da testare per i conflitti di concorrenza](../../../../../../docs/framework/data/adonet/sql/linq/how-to-specify-which-members-are-tested-for-concurrency-conflicts.md).  
  
-   Nel blocco try\/catch della chiamata a <xref:System.Data.Linq.DataContext.SubmitChanges%2A> specificare a che punto dovranno essere generate eccezioni.  
  
     Per altre informazioni, vedere [Procedura: specificare quando vengono generate le eccezioni di concorrenza](../../../../../../docs/framework/data/adonet/sql/linq/how-to-specify-when-concurrency-exceptions-are-thrown.md).  
  
-   Determinare la quantità di dettagli sul conflitto da recuperare, quindi includere nel blocco try\/catch il codice necessario.  
  
     Per altre informazioni, vedere [Procedura: recuperare informazioni sul conflitto tra entità](../../../../../../docs/framework/data/adonet/sql/linq/how-to-retrieve-entity-conflict-information.md) e [Procedura: recuperare informazioni sul conflitto tra membri](../../../../../../docs/framework/data/adonet/sql/linq/how-to-retrieve-member-conflict-information.md).  
  
-   Includere nel codice `try`\/`catch` come si desidera risolvere i diversi conflitti individuati.  
  
     Per altre informazioni, vedere [Procedura: risolvere conflitti mediante la conservazione dei valori di database](../../../../../../docs/framework/data/adonet/sql/linq/how-to-resolve-conflicts-by-retaining-database-values.md), [Procedura: risolvere conflitti mediante la sovrascrittura dei valori di database](../../../../../../docs/framework/data/adonet/sql/linq/how-to-resolve-conflicts-by-overwriting-database-values.md) e [Procedura: risolvere conflitti mediante l'unione con i valori di database](../../../../../../docs/framework/data/adonet/sql/linq/how-to-resolve-conflicts-by-merging-with-database-values.md).  
  
## Tipi LINQ to SQL che supportano l'individuazione e la risoluzione dei conflitti  
 Di seguito sono elencate le classi e le funzionalità di [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] che supportano la risoluzione di conflitti nella concorrenza ottimistica:  
  
-   <xref:System.Data.Linq.ObjectChangeConflict?displayProperty=fullName>  
  
-   <xref:System.Data.Linq.MemberChangeConflict?displayProperty=fullName>  
  
-   <xref:System.Data.Linq.ChangeConflictCollection?displayProperty=fullName>  
  
-   <xref:System.Data.Linq.ChangeConflictException?displayProperty=fullName>  
  
-   <xref:System.Data.Linq.DataContext.ChangeConflicts%2A?displayProperty=fullName>  
  
-   <xref:System.Data.Linq.DataContext.SubmitChanges%2A?displayProperty=fullName>  
  
-   <xref:System.Data.Linq.DataContext.Refresh%2A?displayProperty=fullName>  
  
-   <xref:System.Data.Linq.Mapping.ColumnAttribute.UpdateCheck%2A?displayProperty=fullName>  
  
-   <xref:System.Data.Linq.Mapping.UpdateCheck?displayProperty=fullName>  
  
-   <xref:System.Data.Linq.RefreshMode?displayProperty=fullName>  
  
## Vedere anche  
 [Procedura: gestire i conflitti di modifiche](../../../../../../docs/framework/data/adonet/sql/linq/how-to-manage-change-conflicts.md)