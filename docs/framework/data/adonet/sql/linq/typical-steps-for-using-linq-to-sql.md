---
title: "Passaggi comuni per l&#39;utilizzo di LINQ to SQL | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9a88bd51-bd74-48f7-a9b1-f650e8d55a3e
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Passaggi comuni per l&#39;utilizzo di LINQ to SQL
Per implementare un'applicazione [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)], attenersi ai passaggi descritti in questo argomento.  Molti passaggi sono tuttavia facoltativi  ed è molto probabile che si possa usare il modello a oggetti nello stato predefinito.  
  
 Per iniziare velocemente, usare [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)] per creare il modello a oggetti e avviare la codifica delle query.  
  
## Creazione del modello a oggetti  
 Il primo passaggio consiste nel creare un modello a oggetti basato sui metadati di un database relazionale esistente.  Il modello a oggetti rappresenta il database secondo il linguaggio di programmazione dello sviluppatore.  Per altre informazioni, vedere [Il modello a oggetti LINQ to SQL](../../../../../../docs/framework/data/adonet/sql/linq/the-linq-to-sql-object-model.md).  
  
### 1.Selezionare uno strumento per creare il modello.  
 Per la creazione del modello sono disponibili tre strumenti.  
  
-   Il tipo [!INCLUDE[vs_ordesigner_long](../../../../../../includes/vs-ordesigner-long-md.md)]  
  
     Questa finestra di progettazione offre un'interfaccia utente avanzata per la creazione di un modello a oggetti da un database esistente.  Questo strumento fa parte dell'IDE di [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] ed è più adatto per i database di piccole o medie dimensioni.  
  
-   Strumento per la generazione del codice SQLMetal  
  
     Questa utilità della riga di comando offre un set di opzioni leggermente diverso rispetto a [!INCLUDE[vs_ordesigner_short](../../../../../../includes/vs-ordesigner-short-md.md)].  Questo strumento è più adatto per la modellazione di database di grandi dimensioni.  For altre informazioni, vedere [SqlMetal.exe \(strumento per la generazione del codice\)](../../../../../../docs/framework/tools/sqlmetal-exe-code-generation-tool.md).  
  
-   Editor di codice  
  
     È possibile scrivere codice personalizzato usando l'editor di codice [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)] o un altro editor.  Si sconsiglia di usare questo approccio, che può essere soggetto a errori, se si dispone già di un database ed è possibile usare [!INCLUDE[vs_ordesigner_short](../../../../../../includes/vs-ordesigner-short-md.md)] o lo strumento SQLMetal.  L'editor di codice può tuttavia essere utile per perfezionare o modificare il codice già generato usando altri strumenti.  Per altre informazioni, vedere [Procedura: personalizzare le classi di entità mediante l'editor di codice](../../../../../../docs/framework/data/adonet/sql/linq/how-to-customize-entity-classes-by-using-the-code-editor.md).  
  
### 2.Selezionare il tipo di codice che si desidera generare.  
  
-   File di codice sorgente C\# o [!INCLUDE[vbprvb](../../../../../../includes/vbprvb-md.md)] per il mapping basato sugli attributi.  
  
     Questo file di codice verrà quindi incluso nel progetto [!INCLUDE[vs_current_short](../../../../../../includes/vs-current-short-md.md)]. Per altre informazioni, vedere [Mapping basato su attributi](../../../../../../docs/framework/data/adonet/sql/linq/attribute-based-mapping.md).  
  
-   File XML per il mapping esterno.  
  
     Usando questo approccio è possibile evitare di includere i metadati di mapping nel codice dell'applicazione.  Per altre informazioni, vedere [Mapping esterno](../../../../../../docs/framework/data/adonet/sql/linq/external-mapping.md).  
  
    > [!NOTE]
    >  [!INCLUDE[vs_ordesigner_short](../../../../../../includes/vs-ordesigner-short-md.md)] non supporta la generazione di file di mapping esterni.  Per implementare questa funzionalità è necessario usare lo strumento SQLMetal.  
  
-   File DBML che potrà essere modificato prima di generare un file di codice finale.  
  
     Si tratta di una funzionalità avanzata.  
  
### 3.Perfezionare il file di codice in modo che rifletta le esigenze dell'applicazione.  
 A questo scopo, è possibile usare [!INCLUDE[vs_ordesigner_short](../../../../../../includes/vs-ordesigner-short-md.md)] o l'editor di codice.  
  
## Uso del modello a oggetti  
 Nell'immagine seguente viene illustrata la relazione tra lo sviluppatore e i dati in un scenario a due livelli.  Per altri scenari, vedere [Applicazioni a più livelli e remote con LINQ to SQL](../../../../../../docs/framework/data/adonet/sql/linq/n-tier-and-remote-applications-with-linq-to-sql.md).  
  
 ![DLinqObjectModel](../../../../../../docs/framework/data/adonet/sql/linq/media/dlinqobjectmodel.png "DLinqObjectModel")  
  
 Dopo avere creato il modello a oggetti, si procederà alla descrizione delle richieste di informazioni e alla modifica dei dati all'interno del modello.  Il modello a oggetti deve essere considerato in termini di oggetti e proprietà e non di righe e colonne del database.  Infatti, non si gestisce direttamente il database.  
  
 Quando si indica a [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] di eseguire una query di cui è stata fornita una descrizione o di chiamare l'oggetto `SubmitChanges()` sui dati modificati, [!INCLUDE[vbtecdlinq](../../../../../../includes/vbtecdlinq-md.md)] comunica con il database nel linguaggio del database.  
  
 Di seguito sono riportati i passaggi comuni per l'uso del modello a oggetti creato.  
  
### 1.Creare query per recuperare informazioni dal database.  
 Per altre informazioni, vedere [Concetti relativi alle query](../../../../../../docs/framework/data/adonet/sql/linq/query-concepts.md) e [Esempi di query](../../../../../../docs/framework/data/adonet/sql/linq/query-examples.md).  
  
### 2.Eseguire l'override dei comportamenti predefiniti per le operazioni Insert, Update e Delete.  
 Questo passaggio è facoltativo.  Per altre informazioni, vedere [Personalizzazione delle operazioni Insert, Update e Delete](../../../../../../docs/framework/data/adonet/sql/linq/customizing-insert-update-and-delete-operations.md).  
  
### 3.Impostare le opzioni appropriate per rilevare e segnalare i conflitti di concorrenza.  
 Per gestire i conflitti di concorrenza, è possibile mantenere i valori predefiniti del modello oppure modificarli in base agli scopi del progetto.  Per altre informazioni, vedere [Procedura: specificare i membri da testare per i conflitti di concorrenza](../../../../../../docs/framework/data/adonet/sql/linq/how-to-specify-which-members-are-tested-for-concurrency-conflicts.md) e [Procedura: specificare quando vengono generate le eccezioni di concorrenza](../../../../../../docs/framework/data/adonet/sql/linq/how-to-specify-when-concurrency-exceptions-are-thrown.md).  
  
### 4.Definire una gerarchia di ereditarietà  
 Questo passaggio è facoltativo.  Per altre informazioni, vedere [Supporto dell'ereditarietà](../../../../../../docs/framework/data/adonet/sql/linq/inheritance-support.md).  
  
### 5.Fornire un'interfaccia utente adatta.  
 Questo passaggio è facoltativo e dipende dalla modalità di uso dell'applicazione.  
  
### 6.Eseguire il debug e il test dell'applicazione.  
 Per altre informazioni, vedere [Supporto per il debug](../../../../../../docs/framework/data/adonet/sql/linq/debugging-support.md).  
  
## Vedere anche  
 [Introduzione](../../../../../../docs/framework/data/adonet/sql/linq/getting-started.md)   
 [Creazione del modello a oggetti](../../../../../../docs/framework/data/adonet/sql/linq/creating-the-object-model.md)   
 [Stored procedure](../../../../../../docs/framework/data/adonet/sql/linq/stored-procedures.md)