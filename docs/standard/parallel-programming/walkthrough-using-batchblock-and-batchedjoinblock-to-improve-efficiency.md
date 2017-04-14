---
title: "Walkthrough: Using BatchBlock and BatchedJoinBlock to Improve Efficiency | Microsoft Docs"
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
  - "Task Parallel Library, dataflows"
  - "TPL dataflow library, improving efficiency"
ms.assetid: 5beb4983-80c2-4f60-8c51-a07f9fd94cb3
caps.latest.revision: 8
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 8
---
# Walkthrough: Using BatchBlock and BatchedJoinBlock to Improve Efficiency
La libreria del flusso di dati TPL fornisce le classi <xref:System.Threading.Tasks.Dataflow.BatchedJoinBlock%602?displayProperty=fullName> e <xref:System.Threading.Tasks.Dataflow.BatchBlock%601?displayProperty=fullName> in modo da ricevere e memorizzazione nel buffer i dati da una o più origini quindi passare all'esterno i dati memorizzati nel buffer come una raccolta unica.  Questo meccanismo di divisione in gruppi è utile quando si raccolgono dati da una o più origini e quindi si elaborano più elementi di dati come gruppo.  Ad esempio, si consideri un'applicazione che utilizza il flusso di dati per inserire i record in un database.  Questa operazione può risultare più efficace se più elementi vengono inseriti contemporaneamente anziché uno alla volta in sequenza.  In questo documento viene descritto come utilizzare la classe <xref:System.Threading.Tasks.Dataflow.BatchBlock%601> per migliorare l'efficienza di tali operazioni di inserimento del database.  Viene descritto inoltre come utilizzare la classe <xref:System.Threading.Tasks.Dataflow.BatchedJoinBlock%602> per acquisire i risultati e tutte le eccezioni che si verificano quando il programma legge da un database.  
  
> [!TIP]
>  La libreria del flusso di dati TPL \(spazio dei nomi <xref:System.Threading.Tasks.Dataflow?displayProperty=fullName>\) non viene distribuita con [!INCLUDE[net_v45](../../../includes/net-v45-md.md)].  Per installare lo spazio dei nomi <xref:System.Threading.Tasks.Dataflow>, aprire il progetto in [!INCLUDE[vs_dev11_long](../../../includes/vs-dev11-long-md.md)], scegliere **Gestisci pacchetti NuGet** dal menu del progetto e scegliere cerca online il pacchetto `Microsoft.Tpl.Dataflow`.  
  
## Prerequisiti  
  
1.  Leggere la sezione dei blocchi di join nel documento [Flusso di dati](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md) prima di iniziare questa procedura dettagliata.  
  
2.  Assicurarsi di disporre di una copia del database Northwind, Northwind.sdf, disponibile nel computer.  Questo file si trova in genere nella cartella %Program Files%\\Microsoft SQL Server Compact Edition\\v3.5\\Samples\\.  
  
    > [!IMPORTANT]
    >  In alcune versioni di Windows, non è possibile effettuare la connessione a Northwind.sdf se è in esecuzione [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] in modalità non\-amministratore.  Per la connessione a Northwind.sdf, avviare [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] o un prompt dei comandi [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)] in modalità **Esegui come amministratore**.  
  
 In questa procedura dettagliata sono contenute le sezioni seguenti:  
  
-   [Creazione dell'applicazione console](#creating)  
  
-   [Definizione della classe Dipendente](#employeeClass)  
  
-   [Definizione delle Operazioni del Database dei Dipendenti](#operations)  
  
-   [Aggiunta di Dati dei Dipendenti al Database senza utilizzare il Buffer](#nonBuffering)  
  
-   [Utilizzo di Buffer per Aggiungere i Dati dei Dipendenti al Database](#buffering)  
  
-   [Utilizzo di Join bufferizzata per leggere i dati dei dipendenti dal database](#bufferedJoin)  
  
-   [Esempio completo](#complete)  
  
<a name="creating"></a>   
## Creazione dell'applicazione console  
  
<a name="consoleApp"></a>   
1.  In [!INCLUDE[vsprvs](../../../includes/vsprvs-md.md)], creare un progetto **Applicazione Console** in Visual C\# o Visual Basic.  In questo documento, il progetto viene denominato `DataflowBatchDatabase`.  
  
2.  Nel progetto, aggiungere un riferimento a System.Data.SqlServerCe.dll e un riferimento a System.Threading.Tasks.Dataflow.dll.  
  
3.  Assicurarsi che Form1.cs \(Form1.vb per [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]\) contenga le seguenti istruzioni `using` \(`Imports` in [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)]\).  
  
     [!code-csharp[TPLDataflow_BatchDatabase#1](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_batchdatabase/cs/dataflowbatchdatabase.cs#1)]
     [!code-vb[TPLDataflow_BatchDatabase#1](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_batchdatabase/vb/dataflowbatchdatabase.vb#1)]  
  
4.  Aggiungere i seguenti membri dati alla classe `Program`.  
  
     [!code-csharp[TPLDataflow_BatchDatabase#2](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_batchdatabase/cs/dataflowbatchdatabase.cs#2)]
     [!code-vb[TPLDataflow_BatchDatabase#2](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_batchdatabase/vb/dataflowbatchdatabase.vb#2)]  
  
<a name="employeeClass"></a>   
## Definizione della classe Dipendente  
 Aggiungere alla classe `Program` la classe `Employee`.  
  
 [!code-csharp[TPLDataflow_BatchDatabase#3](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_batchdatabase/cs/dataflowbatchdatabase.cs#3)]
 [!code-vb[TPLDataflow_BatchDatabase#3](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_batchdatabase/vb/dataflowbatchdatabase.vb#3)]  
  
 La classe `Employee` contiene tre proprietà `EmployeeID`, `LastName` e `FirstName`.  Queste proprietà corrispondono alle colonne `Employee ID`, `Last Name` e `First Name` nella tabella `Employees` del database Northwind.  Per questa dimostrazione, la classe `Employee` definisce anche il metodo `Random`, che crea un oggetto `Employee` con valori casuali per le proprietà.  
  
<a name="operations"></a>   
## Definizione delle Operazioni del Database dei Dipendenti  
 Aggiungere alla classe `Program` i metodi `InsertEmployees`, `GetEmployeeCount` e `GetEmployeeID`.  
  
 [!code-csharp[TPLDataflow_BatchDatabase#4](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_batchdatabase/cs/dataflowbatchdatabase.cs#4)]
 [!code-vb[TPLDataflow_BatchDatabase#4](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_batchdatabase/vb/dataflowbatchdatabase.vb#4)]  
  
 Il metodo `InsertEmployees` aggiunge nuovi record dipendente al database.  Il metodo `GetEmployeeCount` recupera il numero di voci nella tabella `Employees`.  Il metodo `GetEmployeeID` recupera l'identificatore del primo dipendente con il nome specificato.  Ognuno di questi metodi accetta una stringa di connessione al database Northwind e utilizza le funzionalità nello spazio dei nomi `System.Data.SqlServerCe` per comunicare con il database.  
  
<a name="nonBuffering"></a>   
## Aggiunta di Dati dei Dipendenti al Database senza utilizzare il Buffer  
 Aggiungere alla classe `Program` i metodi `AddEmployees` e `PostRandomEmployees`.  
  
 [!code-csharp[TPLDataflow_BatchDatabase#5](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_batchdatabase/cs/dataflowbatchdatabase.cs#5)]
 [!code-vb[TPLDataflow_BatchDatabase#5](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_batchdatabase/vb/dataflowbatchdatabase.vb#5)]  
  
 Il metodo `AddEmployees` aggiunge dati casuali del dipendente al database tramite il flusso di dati.  Crea un oggetto <xref:System.Threading.Tasks.Dataflow.ActionBlock%601> che chiama il metodo `InsertEmployees` per aggiungere una voce dipendente al database.  Il metodo `AddEmployees` chiama quindi il metodo `PostRandomEmployees` per inserire più oggetti `Employee` all'oggetto <xref:System.Threading.Tasks.Dataflow.ActionBlock%601>.  Il metodo `AddEmployees` attende che tutte le operazioni di inserimento finiscano.  
  
<a name="buffering"></a>   
## Utilizzo di Buffer per Aggiungere i Dati dei Dipendenti al Database  
 Aggiungere alla classe `Program` il metodo `AddEmployeesBatched`.  
  
 [!code-csharp[TPLDataflow_BatchDatabase#6](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_batchdatabase/cs/dataflowbatchdatabase.cs#6)]
 [!code-vb[TPLDataflow_BatchDatabase#6](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_batchdatabase/vb/dataflowbatchdatabase.vb#6)]  
  
 Questo metodo è simile a `AddEmployees`, con la differenza che utilizza anche la classe <xref:System.Threading.Tasks.Dataflow.BatchBlock%601> per la memorizzazione nel buffer di più oggetti `Employee` prima di inviare tali oggetti all'oggetto <xref:System.Threading.Tasks.Dataflow.ActionBlock%601>.  Poiché la classe <xref:System.Threading.Tasks.Dataflow.BatchBlock%601> propaga più elementi come una raccolta, l'oggetto <xref:System.Threading.Tasks.Dataflow.ActionBlock%601> viene modificato per lavorare su un array di oggetti `Employee`.  Come nel metodo `AddEmployees`, `AddEmployeesBatched` chiama il metodo `PostRandomEmployees` per inserire più oggetti `Employee`; tuttavia, `AddEmployeesBatched` inserisce questi oggetti nell'oggetto <xref:System.Threading.Tasks.Dataflow.BatchBlock%601>.  Il metodo `AddEmployeesBatched`  attende anche che tutte le operazioni di inserimento finiscano.  
  
<a name="bufferedJoin"></a>   
## Utilizzo di Join bufferizzata per leggere i dati dei dipendenti dal database  
 Aggiungere alla classe `Program` il metodo `GetRandomEmployees`.  
  
 [!code-csharp[TPLDataflow_BatchDatabase#7](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_batchdatabase/cs/dataflowbatchdatabase.cs#7)]
 [!code-vb[TPLDataflow_BatchDatabase#7](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_batchdatabase/vb/dataflowbatchdatabase.vb#7)]  
  
 Questo metodo visualizza le informazioni sui dipendenti casuali nella console.  Crea diversi oggetti casuali `Employee` e chiama il metodo `GetEmployeeID` per recuperare l'identificatore univoco per ogni oggetto.  Poiché il metodo `GetEmployeeID` genera un'eccezione se non esiste alcun dipendente corrispondente al nome e cognome specificato, il metodo `GetRandomEmployees` utilizza la classe <xref:System.Threading.Tasks.Dataflow.BatchedJoinBlock%602> per archiviare oggetti `Employee` per le chiamate riuscite a `GetEmployeeID` e oggetti <xref:System.Exception?displayProperty=fullName> per le chiamate che falliscono.  L'oggetto <xref:System.Threading.Tasks.Dataflow.ActionBlock%601> in questo esempio agisce su un oggetto <xref:System.Tuple%602> che contiene un elenco di oggetti `Employee` e un elenco di oggetti <xref:System.Exception>.  L'oggetto <xref:System.Threading.Tasks.Dataflow.BatchedJoinBlock%602> propaga questi dati quando la somma degli oggetti `Employee` e <xref:System.Exception> ricevuti equivale alle dimensioni del batch.  
  
<a name="complete"></a>   
## Esempio completo  
 Nell'esempio seguente viene illustrato il codice completo.  Il metodo `Main` confronta il tempo necessario per eseguire gli inserimenti in batch del database rispetto al tempo per eseguire l'inserimento non in batch.  Viene inoltre illustrato l'utilizzo di join bufferizzato per leggere i dati dei dipendenti dal database e anche segnalare errori.  
  
 [!code-csharp[TPLDataflow_BatchDatabase#100](../../../samples/snippets/csharp/VS_Snippets_Misc/tpldataflow_batchdatabase/cs/dataflowbatchdatabase.cs#100)]
 [!code-vb[TPLDataflow_BatchDatabase#100](../../../samples/snippets/visualbasic/VS_Snippets_Misc/tpldataflow_batchdatabase/vb/dataflowbatchdatabase.vb#100)]  
  
## Vedere anche  
 [Flusso di dati](../../../docs/standard/parallel-programming/dataflow-task-parallel-library.md)