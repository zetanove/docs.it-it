---
title: "Esecuzione della connessione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3af512f3-87d9-4005-9e2f-abb1060ff43f
caps.latest.revision: 7
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# Esecuzione della connessione
Per eseguire la connessione a Microsoft SQL Server, usare l'oggetto <xref:System.Data.SqlClient.SqlConnection> del provider di dati .NET Framework per SQL Server.  Per eseguire la connessione a un'origine dati OLE DB, usare l'oggetto <xref:System.Data.OleDb.OleDbConnection> del provider di dati .NET Framework per OLE DB.  Per eseguire la connessione a un'origine dati ODBC, usare l'oggetto <xref:System.Data.Odbc.OdbcConnection> del provider di dati .NET Framework per ODBC.  Per eseguire la connessione a un'origine dati Oracle, usare l'oggetto <xref:System.Data.OracleClient.OracleConnection> del provider di dati .NET Framework per Oracle.  Per informazioni sulla sicurezza dell'archiviazione e del recupero delle stringhe di connessione, vedere [Protezione delle informazioni di connessione](../../../../docs/framework/data/adonet/protecting-connection-information.md).  
  
## Disconnessione  
 Al termine dell'utilizzo, chiudere sempre la connessione in modo che possa essere restituita al pool.  Il blocco `Using` in Visual Basic o C\# elimina automaticamente la connessione quando il codice esce dal blocco, anche in caso di eccezione non gestita.  Per altre informazioni, vedere [Istruzione using](../Topic/using%20Statement%20\(C%23%20Reference\).md) e [Using Statement](../Topic/Using%20Statement%20\(Visual%20Basic\).md).  
  
 È anche possibile usare il metodo `Close` o `Dispose` dell'oggetto connessione del provider in uso.  Le connessioni che non vengono chiuse in modo esplicito potrebbero non essere aggiunte o restituite al pool.  Ad esempio, una connessione che esce dall'ambito ma non viene chiusa in modo esplicito verrà restituita al pool di connessioni solo se è stata raggiunta la dimensione massima del pool e la connessione è ancora valida.  Per altre informazioni, vedere [Pool di connessioni OLEDB, ODBC e Oracle](../../../../docs/framework/data/adonet/ole-db-odbc-and-oracle-connection-pooling.md).  
  
> [!NOTE]
>  Non chiamare `Close` o `Dispose` su un oggetto **Connection**, **DataReader** o qualsiasi altro oggetto gestito nel metodo `Finalize` della classe.  Nei finalizzatori rilasciare solo le risorse non gestite che la classe controlla direttamente.  Se nella classe non sono presenti risorse non gestite, non includere un metodo `Finalize` nella relativa definizione della classe.  Per altre informazioni, vedere [Garbage Collection](../../../../docs/standard/garbage-collection/index.md).  
  
> [!NOTE]
>  Nel server non vengono generati eventi di accesso e di disconnessione quando una connessione viene recuperata dal o restituita al pool di connessioni, in quanto la connessione non viene effettivamente chiusa quando viene restituita al pool di connessioni.  Per altre informazioni, vedere [Pool di connessioni di SQL Server \(ADO.NET\)](../../../../docs/framework/data/adonet/sql-server-connection-pooling.md).  
  
## Connessione a SQL Server  
 Il formato della stringa di connessione supportato dal provider di dati .NET Framework per SQL Server è simile al formato della stringa di connessione OLE DB \(ADO\).  Per informazioni sui nomi e sui valori validi del formato della stringa, vedere la proprietà <xref:System.Data.SqlClient.SqlConnection.ConnectionString%2A> dell'oggetto <xref:System.Data.SqlClient.SqlConnection>.  È anche possibile usare la classe <xref:System.Data.SqlClient.SqlConnectionStringBuilder> per creare stringhe di connessione sintatticamente valide in fase di esecuzione.  Per altre informazioni, vedere [Compilatori di stringhe di connessione](../../../../docs/framework/data/adonet/connection-string-builders.md).  
  
 Nel codice di esempio seguente viene descritta la procedura di creazione e di apertura di una connessione a un database SQL Server.  
  
```vb  
' Assumes connectionString is a valid connection string.  
Using connection As New SqlConnection(connectionString)  
    connection.Open()  
    ' Do work here.  
End Using  
```  
  
```csharp  
// Assumes connectionString is a valid connection string.  
using (SqlConnection connection = new SqlConnection(connectionString))  
{  
    connection.Open();  
    // Do work here.  
}  
```  
  
### Sicurezza integrata e ASP.NET  
 La sicurezza integrata di SQL Server \(connessioni trusted\) consente di proteggere la connessione a SQL Server, poiché non espone l'identificatore utente e la password nella stringa di connessione ed è il metodo consigliato per l'autenticazione di una connessione.  La sicurezza integrata usa l'identità di sicurezza corrente, o token, del processo in esecuzione.  Per le applicazioni desktop, tale identità corrisponde solitamente all'identità dell'utente attualmente connesso.  
  
 L'identità di sicurezza delle applicazioni ASP.NET può essere impostata su diverse opzioni.  Per altre informazioni sull'identità di sicurezza usata da un'applicazione ASP.NET al momento della connessione a SQL Server, vedere [ASP.NET Impersonation](../Topic/ASP.NET%20Impersonation.md), [ASP.NET Authentication](../Topic/ASP.NET%20Authentication.md) e [How to: Access SQL Server Using Windows Integrated Security](../Topic/How%20to:%20Access%20SQL%20Server%20Using%20Windows%20Integrated%20Security.md).  
  
## Connessione a un'origine dati OLE DB  
 Con il provider di dati .NET Framework per OLE DB viene fornita la connettività a origini dati esposte usando OLE DB \(tramite SQLOLEDB, il provider OLE DB per SQL Server\) usando l'oggetto **OleDbConnection**.  
  
 Per il provider di dati .NET Framework per OLE DB, il formato della stringa di connessione è identico a quello usato in ADO, con le eccezioni seguenti:  
  
-   È necessaria la parola chiave **Provider**.  
  
-   Le parole chiave **URL**, **Remote Provider** e **Remote Server** non sono supportate.  
  
 Per altre informazioni sulle stringhe di connessione OLE DB, vedere l'argomento relativo a <xref:System.Data.OleDb.OleDbConnection.ConnectionString%2A>.  È anche possibile usare <xref:System.Data.OleDb.OleDbConnectionStringBuilder> per creare stringhe di connessione in fase di esecuzione.  
  
> [!NOTE]
>  L'oggetto **OleDbConnection** non supporta l'impostazione o il recupero di proprietà dinamiche specifiche di un provider OLE DB.  Sono supportate esclusivamente le proprietà che possono essere passate nella stringa di connessione per il provider OLE DB.  
  
 Nell'esempio di codice seguente viene illustrato come creare e aprire una connessione a un'origine dati OLE DB.  
  
```vb  
' Assumes connectionString is a valid connection string.  
Using connection As New OleDbConnection(connectionString)  
    connection.Open()  
    ' Do work here.  
End Using  
  
```  
  
```csharp  
// Assumes connectionString is a valid connection string.  
using (OleDbConnection connection =   
  new OleDbConnection(connectionString))  
{  
    connection.Open();  
    // Do work here.  
}  
```  
  
## Non usare file collegamento dati universali \(UDL, Universal Data Link\)  
 È possibile fornire informazioni di connessione per un oggetto **OleDbConnection** in un file UDL \(Universal Data Link\). Si consiglia, tuttavia, di evitare questa procedura.  I file UDL non sono crittografati, pertanto espongono le informazioni nella stringa di connessione come testo non crittografato.  Poiché per l'applicazione si tratta di una risorsa esterna basata su file, un file UDL non può essere protetto tramite .NET Framework.  
  
## Connessione a un'origine dati ODBC  
 Con il provider di dati .NET Framework per ODBC viene fornita la connettività a origini dati esposte tramite ODBC mediante l'oggetto **OdbcConnection**.  
  
 Il formato della stringa di connessione da usare con il provider di dati .NET Framework per ODBC è molto simile a quello della stringa di connessione ODBC.  È anche possibile specificare il nome di un'origine dati \(DSN, Data Source Name\) ODBC.  Per altre informazioni su **OdbcConnection**, vedere [Classe OdbcConnection](frlrfSystemDataOdbcOdbcConnectionClassTopic).  
  
 Nell'esempio di codice seguente viene illustrato come creare e aprire una connessione a un'origine dati ODBC.  
  
```vb  
' Assumes connectionString is a valid connection string.  
Using connection As New OdbcConnection(connectionString)  
    connection.Open()  
    ' Do work here.  
End Using  
  
```  
  
```csharp  
// Assumes connectionString is a valid connection string.  
using (OdbcConnection connection =   
  new OdbcConnection(connectionString))  
{  
    connection.Open();  
    // Do work here.  
}  
```  
  
## Connessione a un'origine dati Oracle  
 Con il provider di dati .NET Framework per Oracle viene fornita la connettività alle origini dati Oracle tramite l'oggetto **OracleConnection**.  
  
 Il formato della stringa di connessione da usare con il provider di dati .NET Framework per Oracle è molto simile a quello della stringa di connessione del provider OLE DB per Oracle \(MSDAORA\).  Per altre informazioni su **OracleConnection**, vedere [Classe OracleConnection](frlrfSystemDataOracleClientOracleConnectionClassTopic).  
  
 Nell'esempio di codice seguente viene illustrato come creare e aprire una connessione a un'origine dati Oracle.  
  
```vb  
' Assumes connectionString is a valid connection string.  
Using connection As New OracleConnection(connectionString)  
    connection.Open()  
    ' Do work here.  
End Using  
  
```  
  
```csharp  
// Assumes connectionString is a valid connection string.  
using (OracleConnection connection =   
  new OracleConnection(connectionString))  
{  
    connection.Open();  
    // Do work here.  
}  
OracleConnection nwindConn = new OracleConnection("Data Source=MyOracleServer;Integrated Security=yes;");  
nwindConn.Open();  
```  
  
## Vedere anche  
 [Connessione a un'origine dati](../../../../docs/framework/data/adonet/connecting-to-a-data-source.md)   
 [Stringhe di connessione](../../../../docs/framework/data/adonet/connection-strings.md)   
 [Pool di connessioni OLEDB, ODBC e Oracle](../../../../docs/framework/data/adonet/ole-db-odbc-and-oracle-connection-pooling.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)