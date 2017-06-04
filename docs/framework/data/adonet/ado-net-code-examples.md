---
title: "Esempi di codice ADO.NET | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c119657a-9ce6-4940-91e4-ac1d5f0d9584
caps.latest.revision: 7
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 7
---
# Esempi di codice ADO.NET
Gli elenchi di codice inclusi in questo argomento illustrano come recuperare dati da un database usando le tecnologie ADO.NET seguenti:  
  
-   Provider di dati ADO.NET:  
  
    -   [SqlClient](#_SqlClient) (`System.Data.SqlClient`)  
  
    -   [OleDb](#_OleDb) (`System.Data.OleDb`)  
  
    -   [Odbc](#_Odbc) (`System.Data.Odbc`)  
  
    -   [OracleClient](#_OracleClient) (`System.Data.OracleClient`)  
  
-   ADO.NET Entity Framework:  
  
    -   [LINQ to Entities](#_LINQ)  
  
    -   [Oggetto ObjectQuery tipizzato](#_QBM)  
  
    -   [EntityClient](#_EntityClient) (`System.Data.EntityClient`)  
  
-   [LINQ to SQL](#_LINQ2SQL)  
  
## <a name="adonet-data-provider-examples"></a>Esempi di provider di dati ADO.NET  
 Gli elenchi di codice seguenti illustrano come recuperare i dati da un database usando i provider di dati ADO.NET. I dati vengono restituiti in un `DataReader`. Per ulteriori informazioni, vedere [recupero di dati mediante DataReader](../../../../docs/framework/data/adonet/retrieving-data-using-a-datareader.md).  
  
<a name="_SqlClient"></a>   
### <a name="sqlclient"></a>SqlClient  
 Nel codice di questo esempio si presume che sia possibile effettuare la connessione al database di esempio `Northwind` in Microsoft [!INCLUDE[ssNoVersion](../../../../includes/ssnoversion-md.md)]. Il codice crea un <xref:System.Data.SqlClient.SqlCommand> per selezionare le righe dalla tabella Products, aggiunta di un <xref:System.Data.SqlClient.SqlParameter> per limitare i risultati alle righe in cui UnitPrice è maggiore del valore di parametro specificato, in questo caso 5. Il <xref:System.Data.SqlClient.SqlConnection> viene aperto all'interno di un `using` che assicura che le risorse vengono chiusi ed eliminate quando il codice esce dal blocco. Il codice viene eseguito il comando utilizzando un <xref:System.Data.SqlClient.SqlDataReader>e visualizza i risultati nella finestra della console.  
  
  [DataWorks SampleApp.SqlClient#1](../CodeSnippet/VS_Snippets_ADO.NET/DataWorks SampleApp.SqlClient#1)]  
  
 [[Inizio pagina]](#_TOP)  
  
<a name="_OleDb"></a>   
### <a name="oledb"></a>OleDb  
 Nel codice di questo esempio si presuppone che sia possibile effettuare la connessione al database di esempio Northwind di Microsoft Access. Il codice crea un <xref:System.Data.OleDb.OleDbCommand> per selezionare le righe dalla tabella Products, aggiunta di un <xref:System.Data.OleDb.OleDbParameter> per limitare i risultati alle righe in cui UnitPrice è maggiore del valore di parametro specificato, in questo caso 5. Il <xref:System.Data.OleDb.OleDbConnection> viene aperto all'interno di un `using` che assicura che le risorse vengono chiusi ed eliminate quando il codice esce dal blocco. Il codice viene eseguito il comando utilizzando un <xref:System.Data.OleDb.OleDbDataReader>e visualizza i risultati nella finestra della console.  
  
  [DataWorks SampleApp.OleDb#1](../CodeSnippet/VS_Snippets_ADO.NET/DataWorks SampleApp.OleDb#1)]  
  
 [[Inizio pagina]](#_TOP)  
  
<a name="_Odbc"></a>   
### <a name="odbc"></a>Odbc  
 Nel codice di questo esempio si presuppone che sia possibile effettuare la connessione al database di esempio Northwind di Microsoft Access. Il codice crea un <xref:System.Data.Odbc.OdbcCommand> per selezionare le righe dalla tabella Products, aggiunta di un <xref:System.Data.Odbc.OdbcParameter> per limitare i risultati alle righe in cui UnitPrice è maggiore del valore di parametro specificato, in questo caso 5. Il <xref:System.Data.Odbc.OdbcConnection> viene aperto all'interno di un `using` che assicura che le risorse vengono chiusi ed eliminate quando il codice esce dal blocco. L'esegue il comando utilizzando un <xref:System.Data.Odbc.OdbcDataReader>e visualizza i risultati nella finestra della console.  
  
<!-- TODO: review snippet reference  [!CODE [DataWorksSampleApp.Odbc#1](DataWorksSampleApp.Odbc#1)]  -->  
  
 [[Inizio pagina]](#_TOP)  
  
<a name="_OracleClient"></a>   
### <a name="oracleclient"></a>OracleClient  
 Nel codice di questo esempio si presuppone che sia stata effettuata una connessione a DEMO.CUSTOMER in un server Oracle. È inoltre necessario aggiungere un riferimento a System.Data.OracleClient.dll. Il codice restituisce i dati in un <xref:System.Data.OracleClient.OracleDataReader>.  
  
  [DataWorks SampleApp.Oracle#1](../CodeSnippet/VS_Snippets_ADO.NET/DataWorks SampleApp.Oracle#1)]  
  
 [[Inizio pagina]](#_TOP)  
  
## <a name="entity-framework-examples"></a>Esempi di Entity Framework  
 I listati di codice seguenti illustrano come recuperare i dati da un'origine dati eseguendo una query sulle entità in Entity Data Model (EDM). Negli esempi viene utilizzata la [modello Northwind](http://msdn.microsoft.com/it-it/74521f8c-e974-48cb-8858-c08deff52638). Per ulteriori informazioni, vedere [Panoramica su Entity Framework](../../../../docs/framework/data/adonet/ef/overview.md).  
  
<a name="_LINQ"></a>   
### <a name="linq-to-entities"></a>LINQ to Entities  
 Nel codice di questo esempio viene usata una query LINQ per restituire i dati come oggetti Categories, proiettati come tipo anonimo che contiene solo le proprietà CategoryID e CategoryName. Per ulteriori informazioni, vedere [LINQ to Entities Panoramica](http://msdn.microsoft.com/it-it/86d87a27-c17a-45ac-b28d-72c8500333c6).  
  
```  
Option Explicit On  
Option Strict On  
  
Imports System  
Imports System.Linq  
Imports System.Data.Objects  
Imports NorthwindModel  
  
Class LinqSample  
    Public Shared Sub ExecuteQuery()  
        Using context As NorthwindEntities = New NorthwindEntities()  
            Try  
                Dim query = From category In context.Categories _  
                            Select New With _  
                            { _  
                                .categoryID = category.CategoryID, _  
                                .categoryName = category.CategoryName _  
                            }  
  
                For Each categoryInfo In query  
                    Console.WriteLine(vbTab & "{0}" & vbTab & "{1}", _  
                        categoryInfo.categoryID, categoryInfo.categoryName)  
                Next  
            Catch ex As Exception  
                Console.WriteLine(ex.Message)  
            End Try  
        End Using  
    End Sub  
End Class  
```  
  
 In C#:  
  
```  
using System;  
using System.Linq;  
using System.Data.Objects;  
using NorthwindModel;  
  
class LinqSample  
{  
    public static void ExecuteQuery()  
    {  
        using (NorthwindEntities context = new NorthwindEntities())  
        {  
            try  
            {  
                var query = from category in context.Categories  
                            select new  
                            {  
                                categoryID = category.CategoryID,  
                                categoryName = category.CategoryName  
                            };  
  
                foreach (var categoryInfo in query)  
                {  
                    Console.WriteLine("\t{0}\t{1}",  
                        categoryInfo.categoryID, categoryInfo.categoryName);  
                }  
            }  
            catch (Exception ex)  
            {  
                Console.WriteLine(ex.Message);  
            }  
        }  
    }  
}  
```  
  
 [[Inizio pagina]](#_TOP)  
  
<a name="_QBM"></a>   
### <a name="typed-objectquery"></a>Oggetto ObjectQuery tipizzato  
 Nel codice in questo esempio viene utilizzato un <xref:System.Data.Objects.ObjectQuery%601> per restituire dati come oggetti Categories. Per ulteriori informazioni, vedere [query di oggetto](http://msdn.microsoft.com/it-it/0768033c-876f-471d-85d5-264884349276).  
  
```  
Option Explicit On  
Option Strict On  
  
Imports System  
Imports System.Data.Objects  
Imports NorthwindModel  
  
Class ObjectQuerySample  
    Public Shared Sub ExecuteQuery()  
        Using context As NorthwindEntities = New NorthwindEntities()  
            Dim categoryQuery As ObjectQuery(Of Categories) = context.Categories  
  
            For Each category As Categories In _  
                categoryQuery.Execute(MergeOption.AppendOnly)  
                Console.WriteLine(vbTab & "{0}" & vbTab & "{1}", _  
                    category.CategoryID, category.CategoryName)  
            Next  
        End Using  
    End Sub  
End Class  
```  
  
 In C#:  
  
```  
using System;  
using System.Data.Objects;  
using NorthwindModel;  
  
class ObjectQuerySample  
{  
    public static void ExecuteQuery()  
    {  
        using (NorthwindEntities context = new NorthwindEntities())  
        {  
            ObjectQuery<Categories> categoryQuery = context.Categories;  
  
            foreach (Categories category in   
                categoryQuery.Execute(MergeOption.AppendOnly))  
            {  
                Console.WriteLine("\t{0}\t{1}",  
                    category.CategoryID, category.CategoryName);  
            }  
        }  
    }  
}  
```  
  
 [[Inizio pagina]](#_TOP)  
  
<a name="_EntityClient"></a>   
### <a name="entityclient"></a>EntityClient  
 Nel codice in questo esempio viene utilizzato un <xref:System.Data.EntityClient.EntityCommand> per eseguire una query Entity SQL. Questa query restituisce un elenco di record che rappresentano istanze del tipo di entità Categories. Un <xref:System.Data.EntityClient.EntityDataReader> viene utilizzato per accedere ai record di dati nel set di risultati. Per ulteriori informazioni, vedere [EntityClient Provider per Entity Framework](../../../../docs/framework/data/adonet/ef/entityclient-provider-for-the-entity-framework.md).  
  
```  
Option Explicit On  
Option Strict On  
  
Imports System  
Imports System.Data  
Imports System.Data.Common  
Imports System.Data.EntityClient  
Imports NorthwindModel  
  
Class EntityClientSample  
    Public Shared Sub ExecuteQuery()  
        Dim queryString As String = _  
            "SELECT c.CategoryID, c.CategoryName " & _  
                "FROM NorthwindEntities.Categories AS c"  
  
        Using conn As EntityConnection = _  
            New EntityConnection("name=NorthwindEntities")  
  
            Try  
                conn.Open()  
                Using query As EntityCommand = _  
                New EntityCommand(queryString, conn)  
                    Using rdr As DbDataReader = _  
                        query.ExecuteReader(CommandBehavior.SequentialAccess)  
                        While rdr.Read()  
                            Console.WriteLine(vbTab & "{0}" & vbTab & "{1}", _  
                                              rdr(0), rdr(1))  
                        End While  
                    End Using  
                End Using  
            Catch ex As Exception  
                Console.WriteLine(ex.Message)  
            End Try  
        End Using   
    End Sub  
End Class  
```  
  
 In C#:  
  
```  
using System;  
using System.Data;  
using System.Data.Common;  
using System.Data.EntityClient;  
using NorthwindModel;  
  
class EntityClientSample  
{  
    public static void ExecuteQuery()  
    {  
        string queryString =  
            @"SELECT c.CategoryID, c.CategoryName   
                FROM NorthwindEntities.Categories AS c";  
  
        using (EntityConnection conn =  
            new EntityConnection("name=NorthwindEntities"))  
        {  
            try  
            {  
                conn.Open();  
                using (EntityCommand query = new EntityCommand(queryString, conn))  
                {  
                    using (DbDataReader rdr =   
                        query.ExecuteReader(CommandBehavior.SequentialAccess))  
                    {  
                        while (rdr.Read())  
                        {  
                            Console.WriteLine("\t{0}\t{1}", rdr[0], rdr[1]);  
                        }  
                    }  
                }  
            }  
            catch (Exception ex)  
            {  
                Console.WriteLine(ex.Message);  
            }  
        }  
    }  
}  
```  
  
 [[Inizio pagina]](#_TOP)  
  
<a name="_LINQ2SQL"></a>   
## <a name="linq-to-sql"></a>LINQ to SQL  
 Nel codice di questo esempio viene usata una query LINQ per restituire i dati come oggetti Categories, proiettati come tipo anonimo che contiene solo le proprietà CategoryID e CategoryName. Questo esempio è basato sul contesto dati di Northwind. Per ulteriori informazioni, vedere [Introduzione](../../../../docs/framework/data/adonet/sql/linq/getting-started.md).  
  
```  
Option Explicit On  
Option Strict On  
  
Imports System  
Imports System.Collections.Generic  
Imports System.Linq  
Imports System.Text  
Imports Northwind  
  
Class LinqSqlSample  
    Public Shared Sub ExecuteQuery()  
        Using db As NorthwindDataContext = New NorthwindDataContext()  
            Try  
                Dim query = From category In db.Categories _  
                                Select New With _  
                                { _  
                                    .categoryID = category.CategoryID, _  
                                    .categoryName = category.CategoryName _  
                                }  
  
                For Each categoryInfo In query  
                    Console.WriteLine(vbTab & "{0}" & vbTab & "{1}", _  
                            categoryInfo.categoryID, categoryInfo.categoryName)  
                Next  
            Catch ex As Exception  
                Console.WriteLine(ex.Message)  
            End Try  
            End Using   
    End Sub  
End Class  
```  
  
 In C#:  
  
```  
using System;  
using System.Collections.Generic;  
using System.Linq;  
using System.Text;  
using Northwind;  
  
    class LinqSqlSample  
    {  
        public static void ExecuteQuery()  
        {  
            using (NorthwindDataContext db = new NorthwindDataContext())  
            {  
                try  
                {  
                    var query = from category in db.Categories  
                                select new  
                                {  
                                    categoryID = category.CategoryID,  
                                    categoryName = category.CategoryName  
                                };  
  
                    foreach (var categoryInfo in query)  
                    {  
                        Console.WriteLine("vbTab {0} vbTab {1}",  
                            categoryInfo.categoryID, categoryInfo.categoryName);  
                    }  
                }  
                catch (Exception ex)  
                {  
                    Console.WriteLine(ex.Message);  
                }  
            }  
        }  
    }  
```  
  
 [[Inizio pagina]](#_TOP)  
  
## <a name="see-also"></a>Vedere anche  
 [Cenni preliminari su ADO.NET](../../../../docs/framework/data/adonet/ado-net-overview.md)   
 [Recupero e modifica di dati in ADO.NET](../../../../docs/framework/data/adonet/retrieving-and-modifying-data.md)   
 [Creazione di applicazioni dati](../Topic/Creating%20Data%20Applications.md)   
 [Esecuzione di query su un Entity Data Model (attività di Entity Framework)](http://msdn.microsoft.com/it-it/187f1caa-e4d3-4e31-bd99-5d5c2b329c77)   
 [Procedura: eseguire una Query che restituisce oggetti di tipo anonimo](http://msdn.microsoft.com/it-it/3b264025-e911-4d73-90ce-992d2b9d189d)   
 [Provider ADO.NET gestiti e Centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)