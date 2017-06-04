---
title: "Abilitazione di MARS (Multiple Active Result Set) | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 576079e4-debe-4ab5-9204-fcbe2ca7a5e2
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# Abilitazione di MARS (Multiple Active Result Set)
MARS \(Multiple Active Result Set\) è un servizio che funziona in combinazione con SQL Server per consentire l'esecuzione di più batch in un'unica connessione.  Quando MARS è abilitato per l'uso con SQL Server, ciascun oggetto comando usato aggiunge una sessione alla connessione.  
  
> [!NOTE]
>  Una singola sessione MARS apre un'unica connessione logica per MARS e quindi un'unica connessione logica per ogni comando attivo.  
  
## Abilitazione e disabilitazione di MARS nella stringa di connessione  
  
> [!NOTE]
>  Le stringhe di connessione seguenti usano il database di esempio **AdventureWorks** fornito con SQL Server  e presuppongono che il database sia installato in un server denominato MSSQL1.  Modificare la stringa di connessione per adattarla all'ambiente, se necessario.  
  
 Per impostazione predefinita la funzionalità MARS è disabilitata.  Può essere abilitata aggiungendo la coppia di parole chiave "MultipleActiveResultSets\=True" alla stringa di connessione. "  True" è l'unico valore valido per l'abilitazione di MARS.  Nell'esempio seguente viene mostrato come eseguire la connessione a un'istanza di SQL Server e come specificare l'abilitazione di MARS.  
  
```vb  
Dim connectionString As String = "Data Source=MSSQL1;" & _  
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" & _  
    "MultipleActiveResultSets=True"  
```  
  
```csharp  
string connectionString = "Data Source=MSSQL1;" +   
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" +  
    "MultipleActiveResultSets=True";  
```  
  
 È possibile disabilitare MARS aggiungendo la coppia di parole chiave "MultipleActiveResultSets\=False" alla stringa di connessione. "  False" è l'unico valore valido per la disabilitazione di MARS.  Nella stringa di connessione seguente viene mostrato come disabilitare MARS.  
  
```vb  
Dim connectionString As String = "Data Source=MSSQL1;" & _  
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" & _  
    "MultipleActiveResultSets=False"  
```  
  
```csharp  
string connectionString = "Data Source=MSSQL1;" +   
    "Initial Catalog=AdventureWorks;Integrated Security=SSPI;" +  
    "MultipleActiveResultSets=False";  
```  
  
## Considerazioni specifiche sull'utilizzo di MARS  
 In generale, le applicazioni esistenti non necessitano di alcuna modifica per usare una connessione con MARS abilitato.  Tuttavia, se si desidera usare le funzionalità di MARS in determinate applicazioni, è necessario comprendere le considerazioni specifiche seguenti.  
  
### Interfoliazione delle istruzioni  
 Le operazioni MARS vengono eseguite sul server in modalità sincrona.  L'interfoliazione delle istruzioni SELECT e BULK INSERT è consentita.  Tuttavia, le istruzioni DML \(Data Manipulation Language\) e DDL \(Data Definition Language\) vengono eseguite atomicamente.  Eventuali istruzioni eseguite durante l'esecuzione di un batch atomico vengono bloccate.  L'esecuzione parallela sul server non è una funzionalità MARS.  
  
 Se i due batch vengono inviati in una connessione MARS, uno con un'istruzione SELECT e l'altro con un'istruzione DML, l'esecuzione dell'istruzione DML può iniziare contemporaneamente all'esecuzione dell'istruzione SELECT.  Tuttavia, l'istruzione DML deve essere eseguita completamente prima che venga eseguita l'istruzione SELECT.  Se entrambe le istruzioni sono in esecuzione nella stessa transazione, eventuali modifiche apportate da un'istruzione DML dopo che è stata avviata l'esecuzione dell'istruzione SELECT non risultano visibili per l'operazione di lettura.  
  
 Un'istruzione WAITFOR all'interno di un'istruzione SELECT non restituisce la transazione in fase di attesa, ovvero, finché non viene generata la prima riga.  Ciò implica che durante l'attesa di un'istruzione WAITFOR non possono essere eseguiti altri batch all'interno della connessione.  
  
### Cache della sessione MARS  
 Quando viene aperta una connessione con MARS abilitato, viene creata una sessione logica, che consente di aggiungere overhead.  Per ridurre l'overhead e migliorare le prestazioni, **SqlClient** memorizza nella cache la sessione MARS all'interno di una connessione.  La cache può contenere fino a 10 sessioni MARS.  Questo valore non può essere regolato dall'utente.  Se viene raggiunto il limite, viene creata una nuova sessione senza che vengano generati errori.  La cache e le sessioni in essa contenute sono per connessione e non sono condivise tra le connessioni.  Quando viene rilasciata, la sessione viene restituita al pool a meno che non sia stato raggiunto il limite superiore del pool.  Se il pool della cache è pieno, la sessione è chiusa.  Le sessioni MARS non scadono,  ma vengono eliminate quando l'oggetto connessione viene rimosso.  La cache della sessione MARS non è precaricata,  ma viene caricata quando vengono richieste più sessioni dall'applicazione.  
  
### Thread safety  
 Le operazioni MARS non sono thread\-safe.  
  
### Pool di connessioni  
 Le connessioni con MARS abilitato sono in pool come qualsiasi altra connessione.  Se un'applicazione apre due connessioni, una con MARS abilitato e un'altra con MARS disabilitato, le due connessioni risulteranno in pool diversi.  Per altre informazioni, vedere [Pool di connessioni di SQL Server \(ADO.NET\)](../../../../../docs/framework/data/adonet/sql-server-connection-pooling.md).  
  
### Ambiente di esecuzione in batch di SQL Server  
 Quando si apre una connessione, viene definito un ambiente predefinito  che viene quindi copiato in una sessione MARS logica.  
  
 L'ambiente di esecuzione in batch include i componenti seguenti:  
  
-   Opzioni di impostazione \(ad esempio, ANSI\_NULLS, DATE\_FORMAT, LANGUAGE, TEXTSIZE\)  
  
-   Contesto di sicurezza \(ruolo utente\/applicazione\)  
  
-   Contesto database \(database corrente\)  
  
-   Esecuzione di variabili di stato \(ad esempio, @@ERROR, @@ROWCOUNT, @@FETCH\_STATUS @@IDENTITY\)  
  
-   Tabelle temporanee principali  
  
 Con MARS, un ambiente di esecuzione predefinito viene associato a una connessione.  Ogni nuovo batch che viene eseguito in una determinata connessione riceve una copia dell'ambiente predefinito.  Quando il codice viene eseguito in un determinato batch, tutte le modifiche apportate all'ambiente sono limitate al batch specifico.  Al termine dell'esecuzione, le impostazioni di esecuzione vengono copiate nell'ambiente predefinito.  Nel caso di un singolo batch in cui vengono generati diversi comandi da eseguire in ordine sequenziale nella stessa transazione, la semantica è identica a quella esposta dalle connessioni che implicano client e server con versioni precedenti.  
  
### Esecuzione parallela  
 Il servizio MARS non è progettato per eliminare tutte le esigenze relative a più connessioni in un'applicazione.  Se per un'applicazione è necessaria l'esecuzione parallela effettiva di comandi su un server, è necessario usare più connessioni.  
  
 Ad esempio, si consideri il seguente scenario.  Vengono creati due oggetti comando, uno per l'elaborazione di un set di risultati e un altro per l'aggiornamento dei dati. Entrambi gli oggetti condividono una connessione comune tramite MARS.  In questo scenario, con `Transaction`.`Commit` l'aggiornamento non avrà esito positivo finché non saranno stati letti tutti i risultati sul primo oggetto comando, restituendo l'eccezione seguente:  
  
 Messaggio: Il contesto della transazione è in uso in un'altra sessione.  
  
 Fonte: "Provider di dati .Net SqlClient"  
  
 Previsto: \(null\)  
  
 Ricevuto: System.Data.SqlClient.SqlException  
  
 Sono disponibili tre opzioni per la gestione di questo scenario:  
  
1.  Avviare la transazione dopo aver creato il lettore, affinché non sia parte della transazione.  Ogni aggiornamento diventa quindi la propria transazione.  
  
2.  Eseguire il commit di tutto il lavoro dopo aver chiuso il lettore.  Questa operazione ha il potenziale per un batch sostanziale di aggiornamenti.  
  
3.  Non usare MARS, ma una connessione diversa per ciascun oggetto comando come se non si disponesse di MARS.  
  
### Rilevamento del supporto di MARS  
 L'applicazione può verificare il supporto di MARS mediante la lettura del valore `SqlConnection.ServerVersion`.  Il valore massimo deve essere 9 per SQL Server 2005 e 10 per SQL Server 2008.  
  
## Vedere anche  
 [MARS \(Multiple Active Result Set\)](../../../../../docs/framework/data/adonet/sql/multiple-active-result-sets-mars.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)