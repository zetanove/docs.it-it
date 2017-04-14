---
title: "Rilevamento di modifiche con SqlDependency | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e6a58316-f005-4477-92e1-45cc2eb8c5b4
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Rilevamento di modifiche con SqlDependency
È possibile associare un oggetto <xref:System.Data.SqlClient.SqlDependency> a <xref:System.Data.SqlClient.SqlCommand> per rilevare quando i risultati della query differiscono da quelli recuperati in origine.  È inoltre possibile assegnare un delegato all'evento `OnChange` che verrà generato in caso di modifica dei risultati per un comando associato.  È necessario associare l'oggetto <xref:System.Data.SqlClient.SqlDependency> al comando prima di eseguire il comando stesso.  È inoltre possibile usare la proprietà `HasChanges` di <xref:System.Data.SqlClient.SqlDependency> per determinare se i risultati della query sono stati modificati rispetto a quando i dati sono stati recuperati inizialmente.  
  
## Considerazioni sulla sicurezza  
 L'infrastruttura della dipendenza si basa su un oggetto <xref:System.Data.SqlClient.SqlConnection> che viene aperto quando viene chiamato <xref:System.Data.SqlClient.SqlDependency.Start%2A> per ricevere le notifiche relative alla modifica dei dati sottostanti per un comando specificato.  Per controllare se un client è in grado di avviare la chiamata a `SqlDependency.Start`, vengono usati <xref:System.Data.SqlClient.SqlClientPermission> e gli attributi della sicurezza dall'accesso di codice.  Per altre informazioni, vedere [Abilitazione di notifiche di query](../../../../../docs/framework/data/adonet/sql/enabling-query-notifications.md) e [Sicurezza dall'accesso di codice e ADO.NET](../../../../../docs/framework/data/adonet/code-access-security.md).  
  
### Esempio  
 Nella procedura seguente viene illustrato come dichiarare una dipendenza, eseguire un comando e ricevere una notifica in caso di modifica del set di risultati:  
  
1.  Avviare una connessione `SqlDependency` al server.  
  
2.  Creare gli oggetti <xref:System.Data.SqlClient.SqlConnection> e <xref:System.Data.SqlClient.SqlCommand> per la connessione al server e definire un'istruzione Transact\-SQL.  
  
3.  Creare un nuovo oggetto `SqlDependency` oppure usarne uno esistente e associarlo all'oggetto `SqlCommand`.  Internamente, questa procedura consente di creare un oggetto <xref:System.Data.Sql.SqlNotificationRequest> e associarlo all'oggetto comando se necessario.  Questa richiesta di notifica contiene un identificatore interno che identifica in modo univoco l'oggetto `SqlDependency`.  In tal modo viene inoltre avviato il listener del client, se non è già attivo.  
  
4.  Sottoscrivere un gestore eventi all'evento `OnChange` dell'oggetto `SqlDependency`.  
  
5.  Eseguire il comando con uno dei metodi `Execute` dell'oggetto `SqlCommand`.  Poiché il comando è associato all'oggetto notifica, il server riconosce la necessità di generare una notifica e le informazioni della coda faranno riferimento alla coda delle dipendenze.  
  
6.  Interrompere la connessione `SqlDependency` al server.  
  
 Se un qualsiasi utente modifica successivamente i dati sottostanti, in Microsoft SQL Server viene rilevata una notifica in sospeso per una tale modifica, pertanto viene inviata una notifica, che viene elaborata e inoltrata al client tramite l'oggetto `SqlConnection` sottostante creato mediante la chiamata a `SqlDependency.Start`.  Il listener del client riceve il messaggio di invalidazione,  quindi individua l'oggetto `SqlDependency` associato e attiva l'evento `OnChange`.  
  
 Nel frammento di codice seguente è illustrato il modello di progettazione da usare per creare un'applicazione di esempio.  
  
```vb  
Sub Initialization()  
    ' Create a dependency connection.  
    SqlDependency.Start(connectionString, queueName)  
End Sub  
  
Sub SomeMethod()   
    ' Assume connection is an open SqlConnection.  
    ' Create a new SqlCommand object.  
    Using command As New SqlCommand( _  
      "SELECT ShipperID, CompanyName, Phone FROM dbo.Shippers", _  
      connection)  
  
        ' Create a dependency and associate it with the SqlCommand.  
        Dim dependency As New SqlDependency(command)  
        ' Maintain the refence in a class member.  
        ' Subscribe to the SqlDependency event.  
        AddHandler dependency.OnChange, AddressOf OnDependencyChange  
  
        ' Execute the command.  
        Using reader = command.ExecuteReader()  
            ' Process the DataReader.  
        End Using  
    End Using  
End Sub   
  
' Handler method  
Sub OnDependencyChange(ByVal sender As Object, _  
    ByVal e As SqlNotificationEventArgs)   
    ' Handle the event (for example, invalidate this cache entry).  
End Sub  
  
Sub Termination()  
    ' Release the dependency  
    SqlDependency.Stop(connectionString, queueName)  
End Sub  
```  
  
```csharp  
void Initialization()  
{  
    // Create a dependency connection.  
    SqlDependency.Start(connectionString, queueName);  
}  
  
void SomeMethod()  
{  
    // Assume connection is an open SqlConnection.  
  
    // Create a new SqlCommand object.  
    using (SqlCommand command=new SqlCommand(  
        "SELECT ShipperID, CompanyName, Phone FROM dbo.Shippers",   
        connection))  
    {  
  
        // Create a dependency and associate it with the SqlCommand.  
        SqlDependency dependency=new SqlDependency(command);  
        // Maintain the refence in a class member.  
  
        // Subscribe to the SqlDependency event.  
        dependency.OnChange+=new  
           OnChangeEventHandler(OnDependencyChange);  
  
        // Execute the command.  
        using (SqlDataReader reader = command.ExecuteReader())  
        {  
            // Process the DataReader.  
        }  
    }  
}  
  
// Handler method  
void OnDependencyChange(object sender,   
   SqlNotificationEventArgs e )  
{  
  // Handle the event (for example, invalidate this cache entry).  
}  
  
void Termination()  
{  
    // Release the dependency.  
    SqlDependency.Stop(connectionString, queueName);  
}  
```  
  
## Vedere anche  
 [Notifiche di query in SQL Server](../../../../../docs/framework/data/adonet/sql/query-notifications-in-sql-server.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)