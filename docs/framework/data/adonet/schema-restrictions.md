---
title: "Restrizioni di schema | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 73d2980e-e73c-4987-913a-8ddc93d09144
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Restrizioni di schema
Il secondo parametro facoltativo del metodo **GetSchema** è rappresentato dalle restrizioni usate per limitare la quantità di informazioni sullo schema restituite e viene passato al metodo **GetSchema** come matrice di stringhe.  La posizione nella matrice determina i valori che è possibile passare ed equivale al numero della restrizione.  
  
 Nella tabella seguente, ad esempio, vengono descritte le restrizioni supportate dalla raccolta di schemi "Tables" usando il provider di dati .NET Framework per SQL Server:  Restrizioni aggiuntive per le raccolte di schemi di SQL Server vengono indicate alla fine di questo argomento.  
  
|Nome della restrizione|Nome del parametro|Impostazione predefinita della restrizione|Numero della restrizione|  
|----------------------------|------------------------|------------------------------------------------|------------------------------|  
|Catalog|@Catalog|TABLE\_CATALOG|1|  
|Proprietario|@Owner|TABLE\_SCHEMA|2|  
|Tabella|@Name|TABLE\_NAME|3|  
|TableType|@TableType|TABLE\_TYPE|4|  
  
## Impostazione dei valori di restrizione  
 Per usare una delle restrizioni della raccolta di schemi "Tables", è sufficiente creare una matrice di stringa con quattro elementi, quindi posizionare un valore nell'elemento che corrisponde al numero della restrizione.  Per limitare, ad esempio, le tabelle restituite dal metodo **GetSchema** solo a quelle incluse nello schema "Sales", impostare il secondo elemento della matrice su "Sales" prima di passarlo al metodo **GetSchema**.  
  
> [!NOTE]
>  Le raccolte di restrizioni per `SqlClient` e `OracleClient` includono una colonna `ParameterName` aggiuntiva.  La colonna di restrizione predefinita è ancora disponibile per garantire la compatibilità con le versioni precedenti, ma attualmente è ignorata.  Per ridurre il rischio di attacchi SQL injection quando si specificano i valori di restrizione, si consiglia di usare query con parametri invece di sostituire le stringhe.  
  
> [!NOTE]
>  Il numero di elementi nella matrice deve essere inferiore o uguale al numero di restrizioni supportato per la raccolta di schemi specificato, in caso contrario verrà generato un tipo <xref:System.ArgumentException>.  Il numero di restrizioni può essere inferiore al numero massimo consentito.  Le restrizioni mancanti verranno considerate null \(senza restrizioni\).  
  
 È possibile eseguire una query nel provider gestito .NET Framework per determinare l'elenco delle restrizioni supportate chiamando il metodo **GetSchema** con il nome della raccolta di schemi delle restrizioni, ovvero "Restrictions".  In questo modo verrà restituito un oggetto <xref:System.Data.DataTable> con un elenco dei nomi delle raccolte, i nomi delle restrizioni, i valori di restrizione predefiniti e i numeri delle restrizioni.  
  
### Esempio  
 Negli esempi seguenti viene illustrato come usare il metodo <xref:System.Data.SqlClient.SqlConnection.GetSchema%2A> del provider di dati .NET Framework per la classe <xref:System.Data.SqlClient.SqlConnection> di SQL Server per recuperare informazioni sullo schema relative a tutte le tabelle contenute nel database di esempio **AdventureWorks** e per limitare le informazioni restituite alle sole tabelle incluse nello schema "Sales":  
  
 \[Visual Basic\]  
  
```  
Imports System.Data.SqlClient  
  
Module Module1  
Sub Main()  
  Dim connectionString As String = _  
    "Data Source=(local);Database=AdventureWorks;" & _  
       "Integrated Security=true;";  
  
  Dim restrictions(3) As String  
  Using connection As New SqlConnection(connectionString)  
    connection.Open()  
  
    'Specify the restrictions.  
    restrictions(1) = "Sales"  
    Dim table As DataTable = connection.GetSchema("Tables", _  
       restrictions)  
  
    ' Display the contents of the table.  
      For Each row As DataRow In table.Rows  
         For Each col As DataColumn In table.Columns  
            Console.WriteLine("{0} = {1}", col.ColumnName, row(col))  
         Next  
         Console.WriteLine("============================")  
      Next  
    Console.WriteLine("Press any key to continue.")  
    Console.ReadKey()  
  End Using  
End Sub  
End Module  
```  
  
 \[C\#\]  
  
```  
using System;  
using System.Data;  
using System.Data.SqlClient;  
  
class Program  
{  
  static void Main()  
  {  
    string connectionString =   
       "Data Source=(local);Database=AdventureWorks;" +  
       "Integrated Security=true;";  
    using (SqlConnection connection =  
       new SqlConnection(connectionString))  
    {  
        connection.Open();  
  
        // Specify the restrictions.  
        string[] restrictions = new string[4];  
        restrictions[1] = "Sales";  
        System.Data.DataTable table = connection.GetSchema(  
          "Tables", restrictions);  
  
        // Display the contents of the table.  
        foreach (System.Data.DataRow row in table.Rows)  
        {  
            foreach (System.Data.DataColumn col in table.Columns)  
            {  
                Console.WriteLine("{0} = {1}",   
                  col.ColumnName, row[col]);  
            }  
            Console.WriteLine("============================");  
        }  
        Console.WriteLine("Press any key to continue.");  
        Console.ReadKey();  
    }  
  }  
  
  private static string GetConnectionString()  
  {  
     // To avoid storing the connection string in your code,  
     // you can retrieve it from a configuration file.  
     return "Data Source=(local);Database=AdventureWorks;" +  
        "Integrated Security=true;";  
  }  
  
  private static void DisplayData(System.Data.DataTable table)  
  {  
     foreach (System.Data.DataRow row in table.Rows)  
     {  
        foreach (System.Data.DataColumn col in table.Columns)  
        {  
           Console.WriteLine("{0} = {1}", col.ColumnName, row[col]);  
        }  
     Console.WriteLine("============================");  
     }  
  }  
}  
```  
  
## Restrizioni per gli schemi di SQL Server  
 Nelle tabelle seguenti sono incluse le restrizioni per le raccolte di schemi di SQL Server.  
  
### Utenti  
  
|Nome della restrizione|Nome del parametro|Impostazione predefinita della restrizione|Numero della restrizione|  
|----------------------------|------------------------|------------------------------------------------|------------------------------|  
|User\_Name|@Name|name|1|  
  
### Database  
  
|Nome della restrizione|Nome del parametro|Impostazione predefinita della restrizione|Numero della restrizione|  
|----------------------------|------------------------|------------------------------------------------|------------------------------|  
|Nome|@Name|Nome|1|  
  
### Tabelle  
  
|Nome della restrizione|Nome del parametro|Impostazione predefinita della restrizione|Numero della restrizione|  
|----------------------------|------------------------|------------------------------------------------|------------------------------|  
|Catalog|@Catalog|TABLE\_CATALOG|1|  
|Proprietario|@Owner|TABLE\_SCHEMA|2|  
|Tabella|@Name|TABLE\_NAME|3|  
|TableType|@TableType|TABLE\_TYPE|4|  
  
### Colonne  
  
|Nome della restrizione|Nome del parametro|Impostazione predefinita della restrizione|Numero della restrizione|  
|----------------------------|------------------------|------------------------------------------------|------------------------------|  
|Catalog|@Catalog|TABLE\_CATALOG|1|  
|Proprietario|@Owner|TABLE\_SCHEMA|2|  
|Tabella|@Table|TABLE\_NAME|3|  
|Colonna|@Column|COLUMN\_NAME|4|  
  
### StructuredTypeMembers  
  
|Nome della restrizione|Nome del parametro|Impostazione predefinita della restrizione|Numero della restrizione|  
|----------------------------|------------------------|------------------------------------------------|------------------------------|  
|Catalog|@Catalog|TABLE\_CATALOG|1|  
|Proprietario|@Owner|TABLE\_SCHEMA|2|  
|Tabella|@Table|TABLE\_NAME|3|  
|Colonna|@Column|COLUMN\_NAME|4|  
  
### Visualizzazioni  
  
|Nome della restrizione|Nome del parametro|Impostazione predefinita della restrizione|Numero della restrizione|  
|----------------------------|------------------------|------------------------------------------------|------------------------------|  
|Catalog|@Catalog|TABLE\_CATALOG|1|  
|Proprietario|@Owner|TABLE\_SCHEMA|2|  
|Tabella|@Table|TABLE\_NAME|3|  
  
### ViewColumns  
  
|Nome della restrizione|Nome del parametro|Impostazione predefinita della restrizione|Numero della restrizione|  
|----------------------------|------------------------|------------------------------------------------|------------------------------|  
|Catalog|@Catalog|VIEW\_CATALOG|1|  
|Proprietario|@Owner|VIEW\_SCHEMA|2|  
|Tabella|@Table|VIEW\_NAME|3|  
|Colonna|@Column|COLUMN\_NAME|4|  
  
### ProcedureParameters  
  
|Nome della restrizione|Nome del parametro|Impostazione predefinita della restrizione|Numero della restrizione|  
|----------------------------|------------------------|------------------------------------------------|------------------------------|  
|Catalog|@Catalog|SPECIFIC\_CATALOG|1|  
|Proprietario|@Owner|SPECIFIC\_SCHEMA|2|  
|Nome|@Name|SPECIFIC\_NAME|3|  
|Parametro|@Parameter|PARAMETER\_NAME|4|  
  
### Procedure  
  
|Nome della restrizione|Nome del parametro|Impostazione predefinita della restrizione|Numero della restrizione|  
|----------------------------|------------------------|------------------------------------------------|------------------------------|  
|Catalog|@Catalog|SPECIFIC\_CATALOG|1|  
|Proprietario|@Owner|SPECIFIC\_SCHEMA|2|  
|Nome|@Name|SPECIFIC\_NAME|3|  
|Tipo|@Type|ROUTINE\_TYPE|4|  
  
### IndexColumns  
  
|Nome della restrizione|Nome del parametro|Impostazione predefinita della restrizione|Numero della restrizione|  
|----------------------------|------------------------|------------------------------------------------|------------------------------|  
|Catalog|@Catalog|db\_name\(\)|1|  
|Proprietario|@Owner|user\_name\(\)|2|  
|Tabella|@Table|o.  name|3|  
|ConstraintName|@ConstraintName|x.  name|4|  
|Colonna|@Column|c.  name|5|  
  
### Indexes  
  
|Nome della restrizione|Nome del parametro|Impostazione predefinita della restrizione|Numero della restrizione|  
|----------------------------|------------------------|------------------------------------------------|------------------------------|  
|Catalog|@Catalog|db\_name\(\)|1|  
|Proprietario|@Owner|user\_name\(\)|2|  
|Tabella|@Table|o.  name|3|  
  
### UserDefinedTypes  
  
|Nome della restrizione|Nome del parametro|Impostazione predefinita della restrizione|Numero della restrizione|  
|----------------------------|------------------------|------------------------------------------------|------------------------------|  
|assembly\_name|@AssemblyName|assemblies.  name|1|  
|udt\_name|@UDTName|types.assembly\_class|2|  
  
### ForeignKeys  
  
|Nome della restrizione|Nome del parametro|Impostazione predefinita della restrizione|Numero della restrizione|  
|----------------------------|------------------------|------------------------------------------------|------------------------------|  
|Catalog|@Catalog|CONSTRAINT\_CATALOG|1|  
|Proprietario|@Owner|CONSTRAINT\_SCHEMA|2|  
|Tabella|@Table|TABLE\_NAME|3|  
|Nome|@Name|CONSTRAINT\_NAME|4|  
  
## Restrizioni per gli schemi di SQL Server 2008  
 Nelle tabelle seguenti sono incluse le restrizioni per le raccolte di schemi di SQL Server 2008.  Queste restrizioni sono valide a partire dalla versione 3.5 SP1 di .NET Framework e da SQL Server 2008.  Le restrizioni non sono supportate nelle versioni precedenti di .NET Framework e di SQL Server.  
  
### ColumnSetColumns  
  
|Nome della restrizione|Nome del parametro|Impostazione predefinita della restrizione|Numero della restrizione|  
|----------------------------|------------------------|------------------------------------------------|------------------------------|  
|Catalog|@Catalog|TABLE\_CATALOG|1|  
|Proprietario|@Owner|TABLE\_SCHEMA|2|  
|Tabella|@Table|TABLE\_NAME|3|  
  
### AllColumns  
  
|Nome della restrizione|Nome del parametro|Impostazione predefinita della restrizione|Numero della restrizione|  
|----------------------------|------------------------|------------------------------------------------|------------------------------|  
|Catalog|@Catalog|TABLE\_CATALOG|1|  
|Proprietario|@Owner|TABLE\_SCHEMA|2|  
|Tabella|@Table|TABLE\_NAME|3|  
|Colonna|@Column|COLUMN\_NAME|4|  
  
## Vedere anche  
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)