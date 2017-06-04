---
title: "Utilizzo di un DataSet da un servizio Web XML | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9edd6b71-0fa5-4649-ae1d-ac1c12541019
caps.latest.revision: 4
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 4
---
# Utilizzo di un DataSet da un servizio Web XML
Il <xref:System.Data.DataSet> è stato progettato con una struttura disconnessa, in parte per facilitare il trasporto di dati su Internet.  Il **DataSet** è "serializzabile", in quanto è possibile specificarlo come input in o output da servizi Web XML, senza che sia necessaria la scrittura di codice aggiuntivo per eseguire lo streaming del contenuto del **DataSet** da un servizio Web XML a un client e viceversa.  Il **DataSet** viene convertito implicitamente in un flusso XML tramite il formato DiffGram, viene inviato in rete e ricreato come **DataSet** dal flusso XML nell'estremità ricevente.  Si tratta quindi di un metodo molto semplice e flessibile per la trasmissione e la restituzione di dati relazionali tramite i servizi Web XML.  Per altre informazioni sul formato DiffGram, vedere [DiffGram](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/diffgrams.md).  
  
 Nell'esempio riportato si seguito viene illustrato come creare un servizio Web XML e un client che utilizzino il **DataSet** per il trasporto dei dati relazionali, incluse le modifiche di tali dati, e per la risoluzione di eventuali aggiornamenti fino all'origine dati originale.  
  
> [!NOTE]
>  Nella creazione di un servizio Web XML si consiglia di tenere sempre presenti le implicazioni inerenti la sicurezza.  Per altre informazioni sulla protezione di un servizio Web XML, vedere [Securing XML Web Services Created Using ASP.NET](http://msdn.microsoft.com/it-it/354b2ab1-2782-4542-b32a-dc560178b90c).  
  
### Per creare un servizio Web XML che restituisca e utilizzi un DataSet  
  
1.  Creare il servizio Web XML.  
  
     Nell'esempio seguente viene creato un servizio Web XML che restituisce dati, in questo caso un elenco di clienti contenuto nel database **Northwind**, e riceve un **DataSet** con aggiornamenti ai dati, che vengono risolti dal servizio Web XML fino all'origine dati originale.  
  
     Due metodi vengono esposti dal servizio Web XML: **GetCustomers**, che consente la restituzione dell'elenco di clienti, e **UpdateCustomers**, che consente di risolvere gli aggiornamenti fino all'origine dati.  Il servizio Web XML viene archiviato in un file sul server Web denominato DataSetSample.asmx.  Nel codice seguente viene descritto il contenuto del file DataSetSample.asmx.  
  
    ```vb  
    <% @ WebService Language = "vb" Class = "Sample" %>  
    Imports System  
    Imports System.Data  
    Imports System.Data.SqlClient  
    Imports System.Web.Services  
  
    <WebService(Namespace:="http://microsoft.com/webservices/")> _  
    Public Class Sample  
  
    Public connection As SqlConnection = New SqlConnection("Data Source=(local);Integrated Security=SSPI;Initial Catalog=Northwind")  
  
      <WebMethod( Description := "Returns Northwind Customers", EnableSession := False )> _  
      Public Function GetCustomers() As DataSet  
        Dim adapter As SqlDataAdapter = New SqlDataAdapter( _  
          "SELECT CustomerID, CompanyName FROM Customers", connection)  
  
        Dim custDS As DataSet = New DataSet()  
        adapter.MissingSchemaAction = MissingSchemaAction.AddWithKey  
        adapter.Fill(custDS, "Customers")  
  
        Return custDS  
      End Function  
  
      <WebMethod( Description := "Updates Northwind Customers", EnableSession := False )> _  
      Public Function UpdateCustomers(custDS As DataSet) As DataSet  
        Dim adapter As SqlDataAdapter = New SqlDataAdapter()  
  
        adapter.InsertCommand = New SqlCommand( _  
          "INSERT INTO Customers (CustomerID, CompanyName) " & _  
          "Values(@CustomerID, @CompanyName)", connection)  
        adapter.InsertCommand.Parameters.Add( _  
          "@CustomerID", SqlDbType.NChar, 5, "CustomerID")  
        adapter.InsertCommand.Parameters.Add( _  
          "@CompanyName", SqlDbType.NChar, 15, "CompanyName")  
  
        adapter.UpdateCommand = New SqlCommand( _  
          "UPDATE Customers Set CustomerID = @CustomerID, " & _  
          "CompanyName = @CompanyName WHERE CustomerID = " & _  
          @OldCustomerID", connection)  
        adapter.UpdateCommand.Parameters.Add( _  
          "@CustomerID", SqlDbType.NChar, 5, "CustomerID")  
        adapter.UpdateCommand.Parameters.Add( _  
          "@CompanyName", SqlDbType.NChar, 15, "CompanyName")  
  
        Dim parameter As SqlParameter = _  
          adapter.UpdateCommand.Parameters.Add( _  
          "@OldCustomerID", SqlDbType.NChar, 5, "CustomerID")  
        parameter.SourceVersion = DataRowVersion.Original  
  
        adapter.DeleteCommand = New SqlCommand( _  
          "DELETE FROM Customers WHERE CustomerID = @CustomerID", _  
          connection)  
        parameter = adapter.DeleteCommand.Parameters.Add( _  
          "@CustomerID", SqlDbType.NChar, 5, "CustomerID")  
        parameter.SourceVersion = DataRowVersion.Original  
  
        adapter.Update(custDS, "Customers")  
  
        Return custDS  
      End Function  
    End Class  
  
    ```  
  
    ```csharp  
    <% @ WebService Language = "C#" Class = "Sample" %>  
    using System;  
    using System.Data;  
    using System.Data.SqlClient;  
    using System.Web.Services;  
  
    [WebService(Namespace="http://microsoft.com/webservices/")]  
    public class Sample  
    {  
      public SqlConnection connection = new SqlConnection("Data Source=(local);Integrated Security=SSPI;Initial Catalog=Northwind");  
  
      [WebMethod( Description = "Returns Northwind Customers", EnableSession = false )]  
      public DataSet GetCustomers()  
      {  
        SqlDataAdapter adapter = new SqlDataAdapter(  
          "SELECT CustomerID, CompanyName FROM Customers", connection);  
  
        DataSet custDS = new DataSet();  
        adapter.MissingSchemaAction = MissingSchemaAction.AddWithKey;  
        adapter.Fill(custDS, "Customers");  
  
        return custDS;  
      }  
  
      [WebMethod( Description = "Updates Northwind Customers",  
        EnableSession = false )]  
      public DataSet UpdateCustomers(DataSet custDS)  
      {  
        SqlDataAdapter adapter = new SqlDataAdapter();  
  
        adapter.InsertCommand = new SqlCommand(  
          "INSERT INTO Customers (CustomerID, CompanyName) " +  
          "Values(@CustomerID, @CompanyName)", connection);  
        adapter.InsertCommand.Parameters.Add(  
          "@CustomerID", SqlDbType.NChar, 5, "CustomerID");  
        adapter.InsertCommand.Parameters.Add(  
          "@CompanyName", SqlDbType.NChar, 15, "CompanyName");  
  
        adapter.UpdateCommand = new SqlCommand(  
          "UPDATE Customers Set CustomerID = @CustomerID, " +  
          "CompanyName = @CompanyName WHERE CustomerID = " +  
          "@OldCustomerID", connection);  
        adapter.UpdateCommand.Parameters.Add(  
          "@CustomerID", SqlDbType.NChar, 5, "CustomerID");  
        adapter.UpdateCommand.Parameters.Add(  
          "@CompanyName", SqlDbType.NChar, 15, "CompanyName");  
        SqlParameter parameter = adapter.UpdateCommand.Parameters.Add(  
          "@OldCustomerID", SqlDbType.NChar, 5, "CustomerID");  
        parameter.SourceVersion = DataRowVersion.Original;  
  
        adapter.DeleteCommand = new SqlCommand(  
        "DELETE FROM Customers WHERE CustomerID = @CustomerID",  
         connection);  
        parameter = adapter.DeleteCommand.Parameters.Add(  
          "@CustomerID", SqlDbType.NChar, 5, "CustomerID");  
        parameter.SourceVersion = DataRowVersion.Original;  
  
        adapter.Update(custDS, "Customers");  
  
        return custDS;  
      }  
    }  
    ```  
  
     In uno scenario tipico il metodo **UpdateCustomers** verrebbe scritto in modo da rilevare eventuali violazioni alla concorrenza ottimistica.  Per semplicità, questa opzione non è stata inclusa nell'esempio.  Per altre informazioni sulla concorrenza ottimistica, vedere [Concorrenza ottimistica](../../../../../docs/framework/data/adonet/optimistic-concurrency.md).  
  
2.  Creare un proxy del servizio Web XML.  
  
     Un proxy SOAP verrà richiesto dai client del servizio Web XML per l'uso dei metodi esposti.  È possibile generare questo proxy usando Visual Studio.  Se si imposta un riferimento Web su un servizio Web esistente tramite Visual Studio, tutti i comportamenti descritti in questo passaggio si verificheranno in modo trasparente.  Per creare la classe proxy autonomamente, continuare a eseguire i passaggi descritti di seguito.  Tuttavia, nella maggior parte dei casi, per creare la classe proxy per l'applicazione client è sufficiente usare Visual Studio.  
  
     Per creare un proxy, è possibile usare lo Strumento del linguaggio di descrizione dei servizi Web \(Wsdl.exe\).  Se ad esempio il servizio Web XML viene esposto nell'URL http:\/\/myserver\/data\/DataSetSample.asmx, per creare un proxy di Visual Basic .NET con spazio dei nomi **WebData.DSSample** e archiviarlo nel file sample.vb è necessario eseguire un comando simile al seguente.  
  
    ```  
    wsdl /l:VB /out:sample.vb http://myserver/data/DataSetSample.asmx /n:WebData.DSSample  
    ```  
  
     Per creare un proxy C\# nel file sample.cs, eseguire il comando seguente.  
  
    ```  
    wsdl /l:CS /out:sample.cs http://myserver/data/DataSetSample.asmx /n:WebData.DSSample  
    ```  
  
     È quindi possibile compilare il proxy come libreria e importarlo nel client del servizio Web XML.  Per compilare il codice del proxy di Visual Basic .NET archiviato nel file sample.vb come sample.dll, eseguire il comando seguente.  
  
    ```  
    vbc /t:library /out:sample.dll sample.vb /r:System.dll /r:System.Web.Services.dll /r:System.Data.dll /r:System.Xml.dll  
    ```  
  
     Per compilare il codice del proxy C\# archiviato nel file sample.cs come sample.dll, eseguire il comando seguente.  
  
    ```  
    csc /t:library /out:sample.dll sample.cs /r:System.dll /r:System.Web.Services.dll /r:System.Data.dll /r:System.Xml.dll  
    ```  
  
3.  Creare un client del servizio Web XML.  
  
     Per generare una classe proxy del servizio Web usando Visual Studio, è sufficiente creare il progetto client e fare clic su di esso con il pulsante destro del mouse nella finestra Esplora soluzioni. Quindi fare clic su **Aggiungi riferimento Web** e selezionare il servizio Web dall'elenco di servizi Web disponibili. Se il servizio Web non è disponibile nella soluzione o nel computer corrente, potrebbe essere richiesto di fornire l'indirizzo dell'endpoint del servizio Web. Se si crea autonomamente il proxy del servizio Web XML, come descritto nel passaggio precedente, è possibile importarlo nel codice del client e usare i metodi del servizio Web XML.  Il codice di esempio seguente consente di importare la libreria del proxy, chiamare **GetCustomers** per ottenere un elenco di clienti, aggiungere un nuovo cliente e infine restituire un **DataSet** contenente gli aggiornamenti a **UpdateCustomers**.  
  
     Notare che nell'esempio il **DataSet** restituito da **DataSet.GetChanges** viene passato a **UpdateCustomers**, poiché è necessario passare a **UpdateCustomers** solo le righe modificate.  **UpdateCustomers** restituisce il **DataSet** risolto, su cui è possibile eseguire il **Merge** nel **DataSet** esistente, in modo da incorporare le modifiche risolte ed eventuali informazioni relative agli errori di riga provenienti dall'aggiornamento.  Nel codice seguente si presuppone che il riferimento Web sia stato creato usando Visual Studio e che sia stato rinominato come DsSample nella finestra di dialogo **Aggiungi riferimento Web**.  
  
    ```vb  
    Imports System  
    Imports System.Data  
  
    Public Class Client  
  
      Public Shared Sub Main()  
        Dim proxySample As New DsSample.Sample ()  ' Proxy object.  
        Dim customersDataSet As DataSet = proxySample.GetCustomers()  
        Dim customersTable As DataTable = _  
          customersDataSet.Tables("Customers")  
  
        Dim rowAs DataRow = customersTable.NewRow()  
        row("CustomerID") = "ABCDE"  
        row("CompanyName") = "New Company Name"  
        customersTable.Rows.Add(row)  
  
        Dim updateDataSet As DataSet = _  
          proxySample.UpdateCustomers(customersDataSet.GetChanges())  
  
        customersDataSet.Merge(updateDataSet)  
        customersDataSet.AcceptChanges()  
      End Sub  
    End Class  
  
    ```  
  
    ```csharp  
    using System;  
    using System.Data;  
  
    public class Client  
    {  
      public static void Main()  
      {  
        Sample proxySample = new DsSample.Sample();  // Proxy object.  
        DataSet customersDataSet = proxySample.GetCustomers();  
        DataTable customersTable = customersDataSet.Tables["Customers"];  
  
        DataRow row = customersTable.NewRow();  
        row["CustomerID"] = "ABCDE";  
        row["CompanyName"] = "New Company Name";  
        customersTable.Rows.Add(row);  
  
        DataSet updateDataSet = new DataSet();  
  
        updateDataSet =   
          proxySample.UpdateCustomers(customersDataSet.GetChanges());  
  
        customersDataSet.Merge(updateDataSet);  
        customersDataSet.AcceptChanges();  
      }  
    }  
    ```  
  
     Se si crea la classe proxy autonomamente, invece, è necessario eseguire i seguenti passaggi aggiuntivi.  Per compilare l'esempio, fornire la libreria del proxy creata \(sample.dll\) e le librerie .NET correlate.  Per compilare la versione di Visual Basic .NET dell'esempio, archiviata nel file client.vb, eseguire il comando seguente.  
  
    ```  
    vbc client.vb /r:sample.dll /r:System.dll /r:System.Data.dll /r:System.Xml.dll /r:System.Web.Services.dll  
    ```  
  
     Per compilare la versione C\# dell'esempio, archiviata nel file client.cs, eseguire il comando seguente.  
  
    ```  
    csc client.cs /r:sample.dll /r:System.dll /r:System.Data.dll /r:System.Xml.dll /r:System.Web.Services.dll  
    ```  
  
## Vedere anche  
 [ADO.NET](../../../../../docs/framework/data/adonet/index.md)   
 [DataSet, DataTable e DataView](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/index.md)   
 [DataTable](../../../../../docs/framework/data/adonet/dataset-datatable-dataview/datatables.md)   
 [Popolamento di un dataset da un oggetto DataAdapter](../../../../../docs/framework/data/adonet/populating-a-dataset-from-a-dataadapter.md)   
 [Aggiornamenti di origini dati tramite DataAdapter](../../../../../docs/framework/data/adonet/updating-data-sources-with-dataadapters.md)   
 [Parametri di DataAdapter](../../../../../docs/framework/data/adonet/dataadapter-parameters.md)   
 [Web Services Description Language Tool \(Wsdl.exe\)](http://msdn.microsoft.com/it-it/b9210348-8bc2-4367-8c91-d1a04b403e88)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)