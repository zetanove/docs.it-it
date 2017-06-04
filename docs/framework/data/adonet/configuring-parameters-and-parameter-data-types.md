---
title: "Configurazione dei parametri e tipi di dati dei parametri | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 537d8a2c-d40b-4000-83eb-bc1fcc93f707
caps.latest.revision: 6
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 6
---
# Configurazione dei parametri e tipi di dati dei parametri
Gli oggetti comando usano i parametri per passare valori a istruzioni o stored procedure SQL, fornendo la verifica e la convalida dei tipi. A differenza del testo dei comandi, l'input dei parametri viene trattato come valore letterale, non come codice eseguibile. In questo modo è possibile difendersi da attacchi SQL injection, in cui l'autore di un attacco inserisce un comando che compromette la sicurezza del server in un'istruzione SQL.  
  
 I comandi con parametri possono anche migliorare le prestazioni di esecuzione delle query in quanto aiutano il server database a ottenere una corrispondenza accurata tra il comando in arrivo e un piano di query memorizzato nella cache appropriato. Per altre informazioni, vedere [Memorizzazione nella cache e riutilizzo del piano di esecuzione](http://go.microsoft.com/fwlink/?LinkId=120424) e [Parametri e riutilizzo del piano di esecuzione](http://go.microsoft.com/fwlink/?LinkId=120423) nella documentazione online di SQL Server. Oltre ai vantaggi in termini di sicurezza e prestazioni, i comandi con parametri offrono un metodo pratico per organizzare i valori passati a un'origine dati.  
  
 Per creare un oggetto <xref:System.Data.Common.DbParameter>, è possibile usare il relativo costruttore o aggiungerlo all'oggetto <xref:System.Data.Common.DbCommand.DbParameterCollection%2A> chiamando il metodo `Add` della raccolta <xref:System.Data.Common.DbParameterCollection>. Il metodo `Add` accetta come input argomenti del costruttore o un oggetto parametro esistente, a seconda del provider di dati.  
  
## Specifica della proprietà ParameterDirection  
 Quando si aggiungono parametri, è necessario fornire una proprietà <xref:System.Data.ParameterDirection> per i parametri diversi da quelli di input. La tabella seguente illustra i valori `ParameterDirection` che è possibile usare con l'enumerazione <xref:System.Data.ParameterDirection>.  
  
|Nome del membro|Descrizione|  
|---------------------|-----------------|  
|<xref:System.Data.ParameterDirection>|Il parametro è un parametro di input. Questa è l'impostazione predefinita.|  
|<xref:System.Data.ParameterDirection>|Il parametro può essere sia di input che di output.|  
|<xref:System.Data.ParameterDirection>|Il parametro è un parametro di output.|  
|<xref:System.Data.ParameterDirection>|Il parametro rappresenta un valore restituito da un'operazione quale una stored procedure, una funzione predefinita o una funzione definita dall'utente.|  
  
## Utilizzo dei segnaposto di parametri  
 La sintassi per i segnaposto dei parametri varia in base all'origine dati. I provider di dati [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] gestiscono in modo diverso la denominazione e la specifica di parametri e segnaposto di parametri. Questa sintassi è personalizzata in base a un'origine dati specifica, come descritto nella tabella seguente.  
  
|Provider di dati|Sintassi di denominazione di parametri|  
|----------------------|--------------------------------------------|  
|<xref:System.Data.SqlClient>|Usa parametri denominati nel formato `@`*nomeparametro*.|  
|<xref:System.Data.OleDb>|Usa marcatori dei parametri di posizione indicati da un punto interrogativo \(`?`\).|  
|<xref:System.Data.Odbc>|Usa marcatori dei parametri di posizione indicati da un punto interrogativo \(`?`\).|  
|<xref:System.Data.OracleClient>|Usa parametri denominati nel formato `:`*parmname* \(o *parmname*\).|  
  
## Specifica di un tipo di dati per i parametri  
 Il tipo di dati di un parametro è specifico del provider di dati [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)]. Se si specifica il tipo, il valore dell'oggetto `Parameter` viene convertito nel tipo del provider di dati [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] prima che il valore venga passato all'origine dati. È inoltre possibile specificare il tipo di un oggetto `Parameter` in modo generico impostando la proprietà `DbType` dell'oggetto `Parameter` su un determinato oggetto <xref:System.Data.DbType>.  
  
 Il tipo del provider di dati [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] di un oggetto `Parameter` viene inferito dal tipo [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] di `Value` dell'oggetto `Parameter` oppure da `DbType` dell'oggetto `Parameter`. La tabella seguente illustra il tipo `Parameter` dedotto in base all'oggetto passato come valore di `Parameter` o all'oggetto `DbType` specificato.  
  
|Tipo .NET Framework|DbType|SqlDbType|OleDbType|OdbcType|OracleType|  
|-------------------------|------------|---------------|---------------|--------------|----------------|  
|<xref:System.Boolean>|Booleano|Bit|Boolean|Bit|Byte|  
|<xref:System.Byte>|Byte|TinyInt|UnsignedTinyInt|TinyInt|Byte|  
|byte\[\]|Binario|VarBinary`.` La conversione implicita non riesce se la matrice di byte ha una dimensione superiore a quella massima di VarBinary, che è di 8000 byte.Per le matrici di byte maggiori di 8000 byte, impostare in modo esplicito <xref:System.Data.SqlDbType>.|VarBinary|Binario|Raw|  
|<xref:System.Char>|``|L'inferenza di un oggetto <xref:System.Data.SqlDbType> da char non è supportata.|Char|Char|Byte|  
|<xref:System.DateTime>|DateTime|DateTime|DBTimeStamp|DateTime|DateTime|  
|<xref:System.DateTimeOffset>|DateTimeOffset|DateTimeOffset in SQL Server 2008. L'inferenza di un oggetto <xref:System.Data.SqlDbType> da DateTimeOffset non è supportata nelle versioni di SQL Server precedenti a SQL Server 2008.|||DateTime|  
|<xref:System.Decimal>|Decimal|Decimal|Decimal|Numerico|Numero|  
|<xref:System.Double>|Double|Float|Double|Double|Double|  
|<xref:System.Single>|Single|Real|Single|Real|Float|  
|<xref:System.Guid>|Guid|UniqueIdentifier|Guid|UniqueIdentifier|Raw|  
|<xref:System.Int16>|Int16|SmallInt|SmallInt|SmallInt|Int16|  
|<xref:System.Int32>|Int32|Int|Int|Int|Int32|  
|<xref:System.Int64>|Int64|BigInt|BigInt|BigInt|Numero|  
|<xref:System.Object>|Oggetto|Variante|Variante|L'inferenza di un oggetto OdbcType da Object non è supportata.|Blob|  
|<xref:System.String>|String|NVarChar. La conversione implicita non riesce se la stringa ha una dimensione superiore a quella massima di NVarChar, che è di 4000 caratteri. Per le stringhe maggiori di 4000 caratteri, impostare in modo esplicito <xref:System.Data.SqlDbType>.|VarWChar|NVarChar|NVarChar|  
|<xref:System.TimeSpan>|Ora|Time in SQL Server 2008. L'inferenza di un oggetto <xref:System.Data.SqlDbType> da TimeSpan non è supportata nelle versioni di SQL Server precedenti a SQL Server 2008.|DBTime|Time|DateTime|  
|<xref:System.UInt16>|UInt16|L'inferenza di un oggetto <xref:System.Data.SqlDbType> da UInt16 non è supportata.|UnsignedSmallInt|Int|UInt16|  
|<xref:System.UInt32>|UInt32|L'inferenza di un oggetto <xref:System.Data.SqlDbType> da UInt32 non è supportata.|UnsignedInt|BigInt|UInt32|  
|<xref:System.UInt64>|UInt64|L'inferenza di un oggetto <xref:System.Data.SqlDbType> da UInt64 non è supportata.|UnsignedBigInt|Numerico|Numero|  
||AnsiString|VarChar|VarChar|VarChar|VarChar|  
||AnsiStringFixedLength|Char|Char|Char|Char|  
|``|Valuta|Money|Valuta|L'inferenza di un oggetto `OdbcType` da `Currency` non è supportata.|Numero|  
|``|Data|Date in SQL Server 2008. L'inferenza di un oggetto <xref:System.Data.SqlDbType> da Date non è supportata nelle versioni di SQL Server precedenti a SQL Server 2008.|DBDate|Date|DateTime|  
|``|SByte|L'inferenza di un oggetto <xref:System.Data.SqlDbType> da SByte non è supportata.|TinyInt|L'inferenza di un oggetto `OdbcType` da SByte non è supportata.|SByte|  
||StringFixedLength|NChar|WChar|NChar|NChar|  
||Time|Time in SQL Server 2008. L'inferenza di un oggetto <xref:System.Data.SqlDbType> da Time non è supportata nelle versioni di SQL Server precedenti a SQL Server 2008.|DBTime|Time|DateTime|  
||VarNumeric|L'inferenza di un oggetto <xref:System.Data.SqlDbType> da VarNumeric non è supportata.|VarNumeric|L'inferenza di un oggetto `OdbcType` da VarNumeric non è supportata.|Numero|  
|Tipo di oggetto definito dall'utente \(oggetto con <xref:Microsoft.SqlServer.Server.SqlUserDefinedAggregateAttribute>|Object o String, a seconda del provider \(SqlClient restituisce sempre Object, ODBC restituisce sempre String e il provider di dati gestito OleDb può vedere entrambi|SqlDbType.Udt se <xref:Microsoft.SqlServer.Server.SqlUserDefinedTypeAttribute> è in caso contrario, altrimenti Variant|OleDbType.VarWChar \(se il valore è null\) in caso contrario OleDbType.Variant.|OdbcType.NVarChar|Non supportato|  
  
> [!NOTE]
>  Le conversioni da Decimal in altri tipi sono conversioni di restrizione che arrotondano il valore Decimal al valore integer più vicino che tende allo zero. Se non è possibile rappresentare il risultato della conversione nel tipo di destinazione, verrà generata un'eccezione <xref:System.OverflowException>.  
  
> [!NOTE]
>  Quando si invia un valore di parametro null al server, è necessario specificare <xref:System.DBNull>, invece di `null` \(`Nothing` in [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)]\). Il valore null nel sistema è un oggetto vuoto senza un valore.<xref:System.DBNull> viene usato per rappresentare i valori null. Per altre informazioni sui valori null di database, vedere [Gestione di valori null](../../../../docs/framework/data/adonet/sql/handling-null-values.md).  
  
## Informazioni sui parametri  
 I parametri possono anche essere derivati da una stored procedure usando la classe `DbCommandBuilder`. Le classi `SqlCommandBuilder` e `OleDbCommandBuilder` forniscono un metodo statico, `DeriveParameters`, che popola automaticamente la raccolta di parametri di un oggetto comando con le informazioni provenienti da una stored procedure. Si noti che `DeriveParameters`  sovrascrive qualsiasi informazione esistente sui parametri per il comando.  
  
> [!NOTE]
>  La derivazione di informazioni sui parametri implica una riduzione delle prestazioni, in quando richiede un round trip aggiuntivo con l'origine dati per recuperare le informazioni. Se le informazioni sui parametri sono note in fase di progettazione, è possibile migliorare le prestazioni dell'applicazione impostando i parametri in modo esplicito.  
  
 Per altre informazioni, vedere [Generazione di comandi con CommandBuilder](../../../../docs/framework/data/adonet/generating-commands-with-commandbuilders.md).  
  
## Uso di parametri con SqlCommand e una stored procedure  
 Le stored procedure offrono numerosi vantaggi nelle applicazioni guidate dai dati. Usando le stored procedure, le operazioni nel database possono essere incapsulate in un unico comando, ottimizzate per migliorare le prestazioni e rese più sicure con funzioni di sicurezza aggiuntive. Anche se è possibile chiamare una stored procedure semplicemente passandone il nome seguito dagli argomenti dei parametri come istruzione SQL, l'uso della raccolta <xref:System.Data.Common.DbCommand.Parameters%2A> dell'oggetto [!INCLUDE[vstecado](../../../../includes/vstecado-md.md)] di <xref:System.Data.Common.DbCommand> consente di definire in modo più esplicito i parametri delle stored procedure e di accedere ai parametri di output e ai valori restituiti.  
  
> [!NOTE]
>  Le istruzioni con parametri vengono eseguite sul server tramite `sp_executesql,`, che consente il riutilizzo del piano di query. I cursori o le variabili locali del batch `sp_executesql` non sono visibili per il batch che chiama `sp_executesql`. Le modifiche apportate al contesto del database durano solo fino al termine dell'esecuzione dell'istruzione `sp_executesql`. Per altre informazioni, vedere la documentazione online di SQL Server.  
  
 Quando si usano parametri con <xref:System.Data.SqlClient.SqlCommand> per eseguire una stored procedure di SQL Server, i nomi dei parametri aggiunti alla raccolta <xref:System.Data.SqlClient.SqlCommand.Parameters%2A> devono corrispondere ai nomi dei marcatori dei parametri nella stored procedure. Con il provider di dati [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] per SQL Server non è possibile usare il punto interrogativo \(?\) come segnaposto per passare i parametri a un'istruzione SQL o a una stored procedure. I parametri nella stored procedure vengono trattati come parametri denominati e vengono ricercati marcatori di parametri corrispondenti. Ad esempio, la stored procedure `CustOrderHist` è definita con un parametro denominato `@CustomerID`. Quando il codice esegue la stored procedure deve usare anche un parametro denominato `@CustomerID`.  
  
```  
CREATE PROCEDURE dbo.CustOrderHist @CustomerID varchar(5)  
```  
  
### Esempio  
 In questo esempio viene illustrato come chiamare una stored procedure di SQL Server nel database di esempio `Northwind`. Il nome della stored procedure è `dbo.SalesByCategory` e accetta un parametro di input denominato `@CategoryName` con un tipo di dati `nvarchar(15)`. Nel codice viene creato un nuovo oggetto <xref:System.Data.SqlClient.SqlConnection> all'interno di un blocco using, in modo che la connessione venga eliminata al termine della procedura. Vengono creati gli oggetti <xref:System.Data.SqlClient.SqlCommand> e <xref:System.Data.SqlClient.SqlParameter> e vengono impostate le relative proprietà. Un oggetto <xref:System.Data.SqlClient.SqlDataReader> esegue `SqlCommand` e restituisce il set di risultati dalla stored procedure, visualizzando l'output nella finestra della console.  
  
> [!NOTE]
>  Anziché creare oggetti `SqlCommand` e `SqlParameter` e impostare quindi le proprietà in istruzioni distinte, è possibile scegliere di usare uno dei costruttori di overload per impostare più proprietà in una singola istruzione.  
  
 [!code-csharp[DataWorks SqlClient.StoredProcedure#1](../../../../samples/snippets/csharp/VS_Snippets_ADO.NET/DataWorks SqlClient.StoredProcedure/CS/source.cs#1)]
 [!code-vb[DataWorks SqlClient.StoredProcedure#1](../../../../samples/snippets/visualbasic/VS_Snippets_ADO.NET/DataWorks SqlClient.StoredProcedure/VB/source.vb#1)]  
  
## Uso di parametri con OleDbCommand o OdbcCommand  
 Quando si usano parametri con <xref:System.Data.OleDb.OleDbCommand> o <xref:System.Data.Odbc.OdbcCommand>, l'ordine dei parametri aggiunti alla raccolta `Parameters` deve corrispondere all'ordine dei parametri definiti nella stored procedure. Con il provider di dati [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] per OLE DB e il provider di dati [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] per ODBC i parametri di una stored procedure vengono gestiti come segnaposto e i valori dei parametri vengono applicati nell'ordine. Inoltre, i parametri dei valori restituiti devono essere i primi parametri aggiunti alla raccolta `Parameters`.  
  
 Con il provider di dati [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] per OLE DB e il provider di dati [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] per ODBC non è possibile usare parametri denominati nel passaggio di parametri a un'istruzione SQL o a una stored procedure. In questo caso è necessario usare il punto interrogativo \(?\) come segnaposto, come nell'esempio seguente.  
  
```  
SELECT * FROM Customers WHERE CustomerID = ?  
```  
  
 Di conseguenza, l'ordine in cui vengono aggiunti gli oggetti `Parameter` alla raccolta `Parameters` deve corrispondere esattamente alla posizione del segnaposto punto interrogativo \(?\) usato per il parametro.  
  
### Esempio di OleDb  
  
```vb  
Dim command As OleDbCommand = New OleDbCommand( _  
  "SampleProc", connection)  
command.CommandType = CommandType.StoredProcedure  
  
Dim parameter As OleDbParameter = command.Parameters.Add( _  
  "RETURN_VALUE", OleDbType.Integer)  
parameter.Direction = ParameterDirection.ReturnValue  
  
parameter = command.Parameters.Add( _  
  "@InputParm", OleDbType.VarChar, 12)  
parameter.Value = "Sample Value"  
  
parameter = command.Parameters.Add( _  
  "@OutputParm", OleDbType.VarChar, 28)  
parameter.Direction = ParameterDirection.Output  
```  
  
```csharp  
OleDbCommand command = new OleDbCommand("SampleProc", connection);  
command.CommandType = CommandType.StoredProcedure;  
  
OleDbParameter parameter = command.Parameters.Add(  
  "RETURN_VALUE", OleDbType.Integer);  
parameter.Direction = ParameterDirection.ReturnValue;  
  
parameter = command.Parameters.Add(  
  "@InputParm", OleDbType.VarChar, 12);  
parameter.Value = "Sample Value";  
  
parameter = command.Parameters.Add(  
  "@OutputParm", OleDbType.VarChar, 28);  
parameter.Direction = ParameterDirection.Output;  
```  
  
## Esempio di Odbc  
  
```vb  
Dim command As OdbcCommand = New OdbcCommand( _  
  "{ ? = CALL SampleProc(?, ?) }", connection)  
command.CommandType = CommandType.StoredProcedure  
  
Dim parameter As OdbcParameter = command.Parameters.Add("RETURN_VALUE", OdbcType.Int)  
parameter.Direction = ParameterDirection.ReturnValue  
  
parameter = command.Parameters.Add( _  
  "@InputParm", OdbcType.VarChar, 12)  
parameter.Value = "Sample Value"  
  
parameter = command.Parameters.Add( _  
  "@OutputParm", OdbcType.VarChar, 28)  
parameter.Direction = ParameterDirection.Output  
```  
  
```csharp  
OdbcCommand command = new OdbcCommand( _  
  "{ ? = CALL SampleProc(?, ?) }", connection);  
command.CommandType = CommandType.StoredProcedure;  
  
OdbcParameter parameter = command.Parameters.Add( _  
  "RETURN_VALUE", OdbcType.Int);  
parameter.Direction = ParameterDirection.ReturnValue;  
  
parameter = command.Parameters.Add( _  
  "@InputParm", OdbcType.VarChar, 12);  
parameter.Value = "Sample Value";  
  
parameter = command.Parameters.Add( _  
  "@OutputParm", OdbcType.VarChar, 28);  
parameter.Direction = ParameterDirection.Output;  
```  
  
## Vedere anche  
 [Comandi e parametri](../../../../docs/framework/data/adonet/commands-and-parameters.md)   
 [Parametri di DataAdapter](../../../../docs/framework/data/adonet/dataadapter-parameters.md)   
 [Mapping dei tipi di dati in ADO.NET](../../../../docs/framework/data/adonet/data-type-mappings-in-ado-net.md)   
 [Provider gestiti ADO.NET e Centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)