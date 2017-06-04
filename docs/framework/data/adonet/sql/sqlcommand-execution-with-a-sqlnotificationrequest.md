---
title: "Esecuzione di SqlCommand con SqlNotificationRequest | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1776f48f-9bea-41f6-83a4-c990c7a2c991
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Esecuzione di SqlCommand con SqlNotificationRequest
È possibile configurare <xref:System.Data.SqlClient.SqlCommand> per generare una notifica quando i dati vengono modificati dopo essere stati recuperati dal server, nel qual caso il set di risultati sarebbe diverso se venisse eseguita nuovamente la query.  Questa funzione risulta utile per le situazioni in cui si desidera usare code di notifiche personalizzate sul server o quando non si desidera mantenere oggetti attivi.  
  
## Creazione della richiesta di notifica  
 È possibile usare un oggetto <xref:System.Data.Sql.SqlNotificationRequest> per creare la richiesta di notifica associandolo a un oggetto `SqlCommand`.  Una volta creata la richiesta, l'oggetto `SqlNotificationRequest` non è più necessario.  È possibile eseguire una query sulla coda per rilevare eventuali notifiche e rispondere nel modo appropriato.  Le notifiche possono essere generate anche se l'applicazione viene arrestata e successivamente riavviata.  
  
 Quando viene eseguito il comando con la notifica associata, le eventuali modifiche apportate al set di risultati originale attivano l'invio di un messaggio alla coda di SQL Server configurata nella richiesta di notifica.  
  
 Il polling della coda di SQL Server e l'interpretazione del messaggio sono specifici dell'applicazione.  Il polling della coda e la reazione in base al contenuto del messaggio dipendono interamente dall'applicazione.  
  
> [!NOTE]
>  Quando si usano le richieste di notifica di SQL Server con <xref:System.Data.SqlClient.SqlDependency>, creare un nome per la coda anziché usare il nome del servizio predefinito.  
  
 Non esistono nuovi elementi di sicurezza sul lato client per <xref:System.Data.Sql.SqlNotificationRequest>.  Si tratta principalmente di una funzionalità del server, che ha creato privilegi speciali di cui gli utenti devono disporre per richiedere una notifica.  
  
### Esempio  
 Nel frammento di codice seguente viene illustrato come creare un oggetto <xref:System.Data.Sql.SqlNotificationRequest> e associarlo a <xref:System.Data.Sql.SqlCommand>.  
  
```vb  
' Assume connection is an open SqlConnection.  
' Create a new SqlCommand object.  
Dim command As New SqlCommand( _  
  "SELECT ShipperID, CompanyName, Phone FROM dbo.Shippers", connection)  
  
' Create a SqlNotificationRequest object.  
Dim notficationRequest As New SqlNotificationRequest()  
notficationRequest.id = "NotificationID"  
notficationRequest.Service = "mySSBQueue"  
  
' Associate the notification request with the command.  
command.Notification = notficationRequest  
' Execute the command.  
command.ExecuteReader()  
' Process the DataReader.  
' You can use Transact-SQL syntax to periodically poll the   
' SQL Server queue to see if you have a new message.  
```  
  
```csharp  
// Assume connection is an open SqlConnection.  
// Create a new SqlCommand object.  
SqlCommand command=new SqlCommand(  
 "SELECT ShipperID, CompanyName, Phone FROM dbo.Shippers", connection);  
  
// Create a SqlNotificationRequest object.  
SqlNotificationRequest notficationRequest=new SqlNotificationRequest();  
notficationRequest.id="NotificationID";  
notficationRequest.Service="mySSBQueue";  
  
// Associate the notification request with the command.  
command.Notification=notficationRequest;  
// Execute the command.  
command.ExecuteReader();  
// Process the DataReader.  
// You can use Transact-SQL syntax to periodically poll the   
// SQL Server queue to see if you have a new message.  
  
```  
  
## Vedere anche  
 [Notifiche di query in SQL Server](../../../../../docs/framework/data/adonet/sql/query-notifications-in-sql-server.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)