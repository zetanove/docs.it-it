---
title: "Generazione di comandi con CommandBuilder | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 6e3fb8b5-373b-4f9e-ab03-a22693df8e91
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# Generazione di comandi con CommandBuilder
Se la proprietà `SelectCommand` viene specificata in modo dinamico in fase di esecuzione, ad esempio mediante uno strumento per query che accetta un comando testuale dell'utente, potrebbe non essere possibile specificare l'appropriato `InsertCommand`, `UpdateCommand` o `DeleteCommand` in fase di progettazione.  Se <xref:System.Data.DataTable> esegue il mapping o viene generato da una singola tabella di database, è possibile usare l'oggetto <xref:System.Data.Common.DbCommandBuilder> per generare automaticamente gli oggetti `DeleteCommand`, `InsertCommand` e `UpdateCommand` di <xref:System.Data.Common.DbDataAdapter>.  
  
 Come requisito minimo, è necessario impostare la proprietà `SelectCommand` affinché la generazione automatica del comando venga eseguita correttamente.  Lo schema della tabella recuperato dalla proprietà `SelectCommand` determina la sintassi delle istruzioni INSERT, UPDATE e DELETE generate automaticamente.  
  
 <xref:System.Data.Common.DbCommandBuilder> deve eseguire `SelectCommand` in modo da restituire i metadati necessari per creare i comandi SQL INSERT, UPDATE e DELETE.  Di conseguenza, è necessario un ulteriore percorso all'origine dati che può ridurre le prestazioni.  Per ottenere prestazioni ottimali, specificare i comandi in modo esplicito anziché usare <xref:System.Data.Common.DbCommandBuilder>.  
  
 È inoltre necessario che `SelectCommand` restituisca almeno una chiave primaria o una colonna univoca.  In caso contrario, viene generata un'eccezione `InvalidOperation` e i comandi non vengono generati.  
  
 Quando è associato a un `DataAdapter`, <xref:System.Data.Common.DbCommandBuilder> genera automaticamente le proprietà `InsertCommand`, `UpdateCommand` e `DeleteCommand` del `DataAdapter`, se queste sono riferimenti Null.  Se esiste già un oggetto `Command` per una proprietà, viene usato l'oggetto `Command` esistente.  
  
 Le visualizzazioni di database create dall'unione di due o più tabelle non vengono considerate un'unica tabella di database.  In questo caso non è possibile usare <xref:System.Data.Common.DbCommandBuilder> per generare automaticamente i comandi ed è necessario specificarli in modo esplicito.  Per informazioni sull'impostazione esplicita dei comandi per applicare gli aggiornamenti a un `DataSet` nell'origine dati, vedere [Aggiornamenti di origini dati tramite DataAdapter](../../../../docs/framework/data/adonet/updating-data-sources-with-dataadapters.md).  
  
 È possibile eseguire il mapping dei parametri di output alla riga aggiornata di un `DataSet`.  Un'attività comune sarebbe il recupero del valore di un campo identità generato automaticamente o del timestamp da un'origine dati.  Per impostazione predefinita, <xref:System.Data.Common.DbCommandBuilder> non esegue il mapping dei parametri di output sulle colonne in una riga aggiornata.  In questo caso è necessario specificare il comando in modo esplicito.  Per un esempio di mapping di un campo identità generato automaticamente su una colonna di una riga inserita, vedere [Recupero dei valori di identità o del contatore](../../../../docs/framework/data/adonet/retrieving-identity-or-autonumber-values.md).  
  
## Regole per i comandi generati automaticamente  
 Nella tabella seguente vengono illustrate le regole per generare automaticamente i comandi.  
  
|Comando|Regola|  
|-------------|------------|  
|`InsertCommand`|Consente di inserire una riga nell'origine dati per ogni riga della tabella con una proprietà <xref:System.Data.DataRow.RowState%2A> uguale a <xref:System.Data.DataRowState>.  I valori vengono inseriti in tutte le colonne aggiornabili, quindi non nelle colonne di identità, espressioni o timestamp.|  
|`UpdateCommand`|Aggiorna le righe nell'origine dati per tutte le righe della tabella con `RowState` uguale a <xref:System.Data.DataRowState>.  I valori vengono aggiornati in tutte le colonne aggiornabili, quindi non nelle colonne di identità o di espressioni.  Vengono aggiornate tutte le righe in cui i valori delle colonne nell'origine dati corrispondono ai valori delle colonne della chiave primaria della riga e in cui le restanti colonne dell'origine dati corrispondono ai valori originali della riga.  Per altre informazioni, vedere la sezione "Modello di concorrenza ottimistica per aggiornamenti ed eliminazioni" contenuta in questo argomento.|  
|`DeleteCommand`|Elimina le righe nell'origine dati per tutte le righe della tabella con `RowState` uguale a <xref:System.Data.DataRowState>.  Vengono eliminate tutte le righe in cui i valori delle colonne corrispondono ai valori delle colonne della chiave primaria della riga e in cui le restanti colonne dell'origine dati corrispondono ai valori originali della riga.  Per altre informazioni, vedere la sezione "Modello di concorrenza ottimistica per aggiornamenti ed eliminazioni" contenuta in questo argomento.|  
  
## Modello di concorrenza ottimistica per aggiornamenti ed eliminazioni  
 La logica per generare automaticamente i comandi per le istruzioni UPDATE e DELETE si basa sulla *concorrenza ottimistica*. In altre parole, la modifica dei record non è bloccata e altri utenti o processi possono modificarli in qualsiasi momento.  Poiché un record può essere modificato dopo che è stato restituito dall'istruzione SELECT, ma prima che sia eseguita l'istruzione UPDATE o DELETE, nell'istruzione UPDATE o DELETE generata automaticamente è contenuta una clausola WHERE, tale che una riga viene aggiornata solo se contiene tutti i valori originali e non è stata eliminata dall'origine dati.  In questo modo si evita di sovrascrivere i nuovi dati.  Nei casi in cui un comando Update generato automaticamente tenta di aggiornare una riga che è stata eliminata o che non contiene i valori originali rilevati in <xref:System.Data.DataSet>, il comando non ha alcun effetto sui record e viene generata un'eccezione <xref:System.Data.DBConcurrencyException>.  
  
 Se si desidera che le istruzioni UPDATE o DELETE vengano completate a prescindere dai valori originali, è necessario impostare in modo esplicito `UpdateCommand` per il `DataAdapter` e non usare la generazione automatica dei comandi.  
  
## Limiti della logica per la generazione automatica dei comandi  
 I limiti che seguono si riferiscono alla generazione automatica dei comandi.  
  
### Solo tabelle non correlate  
 La logica per la generazione automatica dei comandi genera un'istruzione INSERT, UPDATE o DELETE per le tabelle autonome senza tenere conto delle relazioni con altre tabelle nell'origine dati.  Di conseguenza, è possibile che venga rilevato un errore quando si chiama `Update` per inviare le modifiche a una colonna che fa parte di un vincolo di chiave esterna nel database.  Per evitare questa eccezione, non usare <xref:System.Data.Common.DbCommandBuilder> per aggiornare le colonne incluse in un vincolo di chiave esterna e specificare in modo esplicito le istruzioni usate per eseguire l'operazione.  
  
### Nomi di tabelle e colonne  
 La logica per la generazione automatica dei comandi potrebbe non essere eseguita correttamente se i nomi delle colonne o delle tabelle contengono caratteri speciali quali spazi, punti, virgolette o altri caratteri non alfanumerici, anche se racchiusi tra parentesi.  A seconda del provider, l'impostazione dei parametri QuoteSuffix e QuotePrefix può consentire alla logica di generazione di elaborare gli spazi, ma non i caratteri speciali di escape.  Sono supportati nomi di tabella completi nel formato *catalogo.schema.tabella*.  
  
## Uso di CommandBuilder per generare automaticamente un'istruzione SQL  
 Per generare automaticamente le istruzioni SQL per un oggetto `DataAdapter`, impostare innanzitutto la proprietà `SelectCommand` di `DataAdapter`. Creare quindi un oggetto `CommandBuilder` e specificare come argomento l'oggetto `DataAdapter` per il quale l'oggetto `CommandBuilder` genererà automaticamente le istruzioni SQL.  
  
```vb  
' Assumes that connection is a valid SqlConnection object   
' inside of a Using block.  
Dim adapter As SqlDataAdapter = New SqlDataAdapter( _  
  "SELECT * FROM dbo.Customers", connection)  
Dim builder As SqlCommandBuilder = New SqlCommandBuilder(adapter)  
builder.QuotePrefix = "["  
builder.QuoteSuffix = "]"  
```  
  
```csharp  
// Assumes that connection is a valid SqlConnection object  
// inside of a using block.  
SqlDataAdapter adapter = new SqlDataAdapter(  
  "SELECT * FROM dbo.Customers", connection);  
SqlCommandBuilder builder = new SqlCommandBuilder(adapter);  
builder.QuotePrefix = "[";  
builder.QuoteSuffix = "]";  
```  
  
## Modifica di SelectCommand  
 Se si modifica `CommandText` di `SelectCommand` dopo la generazione automatica di un comando INSERT, UPDATE o DELETE, è possibile che venga generata un'eccezione.  Se l'oggetto `SelectCommand.CommandText` modificato contiene informazioni sullo schema che non sono coerenti con l'oggetto `SelectCommand.CommandText` usato durante la generazione automatica del comando di inserimento, aggiornamento o eliminazione, nelle future chiamate al metodo `DataAdapter.Update` potrebbe essere eseguito un tentativo di accesso a colonne che non esistono più nella tabella corrente a cui `SelectCommand` fa riferimento e verrà generata un'eccezione.  
  
 È possibile aggiornare le informazioni sullo schema usate da `CommandBuilder` per generare automaticamente i comandi chiamando il metodo `RefreshSchema` di `CommandBuilder`.  
  
 Se si desidera conoscere il comando che è stato generato automaticamente, è possibile ottenere un riferimento ai comandi generati automaticamente tramite i metodi `GetInsertCommand`, `GetUpdateCommand` e `GetDeleteCommand` dell'oggetto `CommandBuilder` e selezionare la proprietà `CommandText`del comando associato.  
  
 Nell'esempio di codice seguente viene scritto sulla console il comando di aggiornamento che è stato generato automaticamente.  
  
```  
Console.WriteLine(builder.GetUpdateCommand().CommandText)  
```  
  
 Nell'esempio seguente viene ricreata la tabella `Customers` nel set di dati `custDS`.  Il metodo **RefreshSchema** viene chiamato per aggiornare i comandi generati automaticamente con le informazioni sulla nuova colonna.  
  
```vb  
' Assumes an open SqlConnection and SqlDataAdapter inside of a Using block.  
adapter.SelectCommand.CommandText = _  
  "SELECT CustomerID, ContactName FROM dbo.Customers"  
builder.RefreshSchema()  
  
custDS.Tables.Remove(custDS.Tables("Customers"))  
adapter.Fill(custDS, "Customers")  
```  
  
```csharp  
// Assumes an open SqlConnection and SqlDataAdapter inside of a using block.  
adapter.SelectCommand.CommandText =   
  "SELECT CustomerID, ContactName FROM dbo.Customers";  
builder.RefreshSchema();  
  
custDS.Tables.Remove(custDS.Tables["Customers"]);  
adapter.Fill(custDS, "Customers");  
```  
  
## Vedere anche  
 [Comandi e parametri](../../../../docs/framework/data/adonet/commands-and-parameters.md)   
 [Esecuzione di un comando](../../../../docs/framework/data/adonet/executing-a-command.md)   
 [DbConnection, DbCommand e DbException](../../../../docs/framework/data/adonet/dbconnection-dbcommand-and-dbexception.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)