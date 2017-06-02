---
title: "Dati FILESTREAM | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: bd8b845c-0f09-4295-b466-97ef106eefa8
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# Dati FILESTREAM
L'attributo di archiviazione FILESTREAM è per i dati \(BLOB\) binari archiviati in una colonna varbinary\(max\).  Prima di FILESTREAM, l'archiviazione dei dati binari richiedeva una gestione speciale.  I dati non strutturati, come documenti di testo, immagini e video, sono spesso archiviati fuori dal database e questo ne rende complessa la gestione.  
  
> [!NOTE]
>  Per usare i dati FILESTREAM con SqlClient, è necessario installare .NET Framework 3.5 SP1 \(o versione successiva\).  
  
 Se si specifica l'attributo FILESTREAM in una colonna varbinary\(max\), in [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] i dati vengono archiviati nel file system NTFS locale anziché nel file di database.  Sebbene vengano archiviati separatamente, è possibile usare le stesse istruzioni [!INCLUDE[tsql](../../../../../includes/tsql-md.md)] supportate per l'uso di dati varbinary\(max\) archiviati nel database.  
  
## Supporto di SqlClient per FILESTREAM  
 Il provider di dati [!INCLUDE[dnprdnshort](../../../../../includes/dnprdnshort-md.md)] per [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)], <xref:System.Data.SqlClient>, supporta la lettura e la scrittura nei dati FILESTREAM usando la classe <xref:System.Data.SqlTypes.SqlFileStream> definita nello spazio dei nomi <xref:System.Data.SqlTypes>.  `SqlFileStream` eredita dalla classe <xref:System.IO.Stream> che fornisce metodi per la lettura e la scrittura nei flussi di dati.  La lettura da un flusso comporta il trasferimento dei dati dal flusso in una struttura di dati, ad esempio una matrice di byte.  La scrittura comporta il trasferimento dei dati dalla struttura di dati in un flusso.  
  
### Creazione di una tabella [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)]  
 Le istruzioni [!INCLUDE[tsql](../../../../../includes/tsql-md.md)] seguenti consentono di creare una tabella denominata employees e di inserire una riga di dati.  Dopo avere abilitato l'archiviazione FILESTREAM, è possibile usare questa tabella insieme agli esempi di codice seguenti.  I collegamenti alle risorse della documentazione online di [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)] sono disponibili alla fine di questo argomento.  
  
```  
CREATE TABLE employees  
(  
  EmployeeId INT  NOT NULL  PRIMARY KEY,  
  Photo VARBINARY(MAX) FILESTREAM  NULL,  
  RowGuid UNIQUEIDENTIFIER  NOT NULL  ROWGUIDCOL  
  UNIQUE DEFAULT NEWID()  
)  
GO  
Insert into employees  
Values(1, 0x00, default)  
GO  
  
```  
  
### Esempio: lettura, sovrascrittura e inserimento di dati FILESTREAM  
 Nell'esempio seguente viene illustrato come leggere i dati da FILESTREAM.  Il codice consente di ottenere il percorso logico del file, impostando `FileAccess` su `Read` e `FileOptions` su `SequentialScan`.  Tramite il codice vengono quindi letti i byte da SqlFileStream nel buffer.  I byte vengono infine scritti nella finestra della console.  
  
 Nell'esempio seguente viene illustrato come scrivere dati in un oggetto FILESTREAM nel quale vengono sovrascritti tutti i dati esistenti.  Il codice consente di ottenere il percorso logico del file e di creare `SqlFileStream`, impostando `FileAccess` su `Write` e `FileOptions` su `SequentialScan`.  Un singolo byte viene scritto in `SqlFileStream`, sostituendo tutti i dati nel file.  
  
 Nell'esempio viene illustrato anche come scrivere i dati in un oggetto FILESTREAM usando il metodo Seek per aggiungere i dati alla fine del file.  Il codice consente di ottenere il percorso logico del file e di creare `SqlFileStream`, impostando `FileAccess` su `ReadWrite` e `FileOptions` su `SequentialScan`.  Nel codice viene usato il metodo Seek per cercare la fine del file e viene aggiunto un singolo byte al file esistente.  
  
```csharp  
using System;  
using System.Data.SqlClient;  
using System.Data.SqlTypes;  
using System.Data;  
using System.IO;  
  
namespace FileStreamTest  
{  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            SqlConnectionStringBuilder builder = new SqlConnectionStringBuilder("server=(local);integrated security=true;database=myDB");  
            ReadFilestream(builder);  
            OverwriteFilestream(builder);  
            InsertFilestream(builder);  
  
            Console.WriteLine("Done");  
        }  
  
        private static void ReadFilestream(SqlConnectionStringBuilder connStringBuilder)  
        {  
            using (SqlConnection connection = new SqlConnection(connStringBuilder.ToString()))  
            {  
                connection.Open();  
                SqlCommand command = new SqlCommand("SELECT TOP(1) Photo.PathName(), GET_FILESTREAM_TRANSACTION_CONTEXT() FROM employees", connection);  
  
                SqlTransaction tran = connection.BeginTransaction(IsolationLevel.ReadCommitted);  
                command.Transaction = tran;  
  
                using (SqlDataReader reader = command.ExecuteReader())  
                {  
                    while (reader.Read())  
                    {  
                        // Get the pointer for the file  
                        string path = reader.GetString(0);  
                        byte[] transactionContext = reader.GetSqlBytes(1).Buffer;  
  
                        // Create the SqlFileStream  
                        using (Stream fileStream = new SqlFileStream(path, transactionContext, FileAccess.Read, FileOptions.SequentialScan, allocationSize: 0))  
                        {  
                            // Read the contents as bytes and write them to the console  
                            for (long index = 0; index < fileStream.Length; index++)  
                            {  
                                Console.WriteLine(fileStream.ReadByte());  
                            }  
                        }  
                    }  
                }  
                tran.Commit();  
            }  
        }  
  
        private static void OverwriteFilestream(SqlConnectionStringBuilder connStringBuilder)  
        {  
            using (SqlConnection connection = new SqlConnection(connStringBuilder.ToString()))  
            {  
                connection.Open();  
  
                SqlCommand command = new SqlCommand("SELECT TOP(1) Photo.PathName(), GET_FILESTREAM_TRANSACTION_CONTEXT() FROM employees", connection);  
  
                SqlTransaction tran = connection.BeginTransaction(IsolationLevel.ReadCommitted);  
                command.Transaction = tran;  
  
                using (SqlDataReader reader = command.ExecuteReader())  
                {  
                    while (reader.Read())  
                    {  
                        // Get the pointer for file   
                        string path = reader.GetString(0);  
                        byte[] transactionContext = reader.GetSqlBytes(1).Buffer;  
  
                        // Create the SqlFileStream  
                        using (Stream fileStream = new SqlFileStream(path, transactionContext, FileAccess.Write, FileOptions.SequentialScan, allocationSize: 0))  
                        {  
                            // Write a single byte to the file. This will  
                            // replace any data in the file.  
                            fileStream.WriteByte(0x01);  
                        }  
                    }  
                }  
                tran.Commit();  
            }  
        }  
  
        private static void InsertFilestream(SqlConnectionStringBuilder connStringBuilder)  
        {  
            using (SqlConnection connection = new SqlConnection(connStringBuilder.ToString()))  
            {  
                connection.Open();  
  
                SqlCommand command = new SqlCommand("SELECT TOP(1) Photo.PathName(), GET_FILESTREAM_TRANSACTION_CONTEXT() FROM employees", connection);  
  
                SqlTransaction tran = connection.BeginTransaction(IsolationLevel.ReadCommitted);  
                command.Transaction = tran;  
  
                using (SqlDataReader reader = command.ExecuteReader())  
                {  
                    while (reader.Read())  
                    {  
                        // Get the pointer for file  
                        string path = reader.GetString(0);  
                        byte[] transactionContext = reader.GetSqlBytes(1).Buffer;  
  
                        using (Stream fileStream = new SqlFileStream(path, transactionContext, FileAccess.Write, FileOptions.SequentialScan, allocationSize: 0))  
                        {  
                            // Seek to the end of the file  
                            fileStream.Seek(0, SeekOrigin.End);  
  
                            // Append a single byte   
                            fileStream.WriteByte(0x01);  
                        }  
                    }  
                }  
                tran.Commit();  
            }  
  
        }  
    }  
} using (SqlConnection connection = new SqlConnection(  
    connStringBuilder.ToString()))  
{  
    connection.Open();  
  
    SqlCommand command = new SqlCommand("", connection);  
    command.CommandText = "select Top(1) Photo.PathName(), "  
    + "GET_FILESTREAM_TRANSACTION_CONTEXT () from employees";  
  
    SqlTransaction tran = connection.BeginTransaction(  
        System.Data.IsolationLevel.ReadCommitted);  
    command.Transaction = tran;  
  
    using (SqlDataReader reader = command.ExecuteReader())  
    {  
        while (reader.Read())  
        {  
            // Get the pointer for file  
            string path = reader.GetString(0);  
            byte[] transactionContext = reader.GetSqlBytes(1).Buffer;  
  
            FileStream fileStream = new SqlFileStream(path,  
                (byte[])reader.GetValue(1),  
                FileAccess.ReadWrite,  
                FileOptions.SequentialScan, 0);  
  
            // Seek to the end of the file  
            fs.Seek(0, SeekOrigin.End);  
  
            // Append a single byte   
            fileStream.WriteByte(0x01);  
            fileStream.Close();  
        }  
    }  
    tran.Commit();  
}  
```  
  
 Per un esempio, vedere [Come archiviare e recuperare dati binari in una colonna di flusso di file](http://www.codeproject.com/Articles/32216/How-to-store-and-fetch-binary-data-into-a-file-str).  
  
## Risorse nella documentazione online di [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)]  
 La documentazione completa per FILESTREAM è disponibile nelle sezioni seguenti della documentazione online di [!INCLUDE[ssNoVersion](../../../../../includes/ssnoversion-md.md)].  
  
|Argomento|Descrizione|  
|---------------|-----------------|  
|[Progettazione e implementazione di un'archiviazione FILESTREAM](http://msdn2.microsoft.com/library/bb895234\(SQL.105\).aspx)|Vengono forniti collegamenti alla documentazione relativa a FILESTREAM e ad argomenti correlati.|  
|[Panoramica di FILESTREAM](http://msdn2.microsoft.com/library/bb933993\(SQL.105\).aspx)|Viene descritto quando usare l'archiviazione FILESTREAM e come questa consente l'integrazione del Motore di database di SQL Server con un file system NTFS.|  
|[Introduzione all'archiviazione FILESTREAM](http://msdn.microsoft.com/library/bb933995\(SQL.105\).aspx)|Viene descritto come abilitare FILESTREAM in un'istanza di SQL Server, come creare un database e una tabella per archiviare i dati FILESTREAM e come modificare le righe che contengono dati FILESTREAM.|  
|[Utilizzo dell'archiviazione FILESTREAM nelle applicazioni client](http://msdn.microsoft.com/library/bb933877\(SQL.105\).aspx)|Vengono descritte le funzioni dell'API Win32 per l'uso dei dati FILESTREAM.|  
|[Uso di FILESTREAM con altre funzionalità di SQL Server](http://msdn.microsoft.com/library/bb895334\(SQL.105\).aspx)|Vengono illustrate considerazioni, linee guida e limitazioni per l'uso di dati FILESTREAM con le altre funzionalità di SQL Server.|  
  
## Vedere anche  
 [Tipi di dati SQL Server e ADO.NET](../../../../../docs/framework/data/adonet/sql/sql-server-data-types.md)   
 [Recupero e modifica di dati in ADO.NET](../../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)   
 [Sicurezza dall'accesso di codice e ADO.NET](../../../../../docs/framework/data/adonet/code-access-security.md)   
 [Dati binari e con valori di grandi dimensioni SQL Server](../../../../../docs/framework/data/adonet/sql/sql-server-binary-and-large-value-data.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)