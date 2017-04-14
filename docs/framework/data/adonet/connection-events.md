---
title: "Eventi di connessione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5a29de74-acfc-4134-8616-829dd7ce0710
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Eventi di connessione
Tutti i provider di dati .NET Framework presentano oggetti **Connection** contenenti due eventi che è possibile usare per recuperare messaggi informativi da un'origine dati o per determinare se lo stato di un oggetto **Connection** è stato modificato.  Nella tabella seguente vengono illustrati gli eventi dell'oggetto **Connection**.  
  
|Evento|Descrizione|  
|------------|-----------------|  
|**InfoMessage**|Si verifica quando un messaggio informativo viene restituito da un'origine dati.  I messaggi informativi sono i messaggi di un'origine dati per cui non viene generata un'eccezione.|  
|**StateChange**|Si verifica quando viene modificato lo stato dell'oggetto **Connection**.|  
  
## Utilizzo dell'evento InfoMessage  
 È possibile recuperare avvisi e messaggi informativi da un'origine dati SQL Server usando l'evento <xref:System.Data.SqlClient.SqlConnection.InfoMessage> dell'oggetto <xref:System.Data.SqlClient.SqlConnection>.  Gli errori restituiti da un'origine dati con un livello di gravità compreso tra 11 e 16 generano un'eccezione.  Tuttavia, l'evento <xref:System.Data.SqlClient.SqlConnection.InfoMessage> consente di ottenere dall'origine dati i messaggi che non sono associati a un errore.  Nel caso di Microsoft SQL Server i messaggi di errore con una gravità uguale o minore di 10 sono considerati informativi e vengono acquisiti usando l'evento <xref:System.Data.SqlClient.SqlConnection.InfoMessage>.  Per altre informazioni, vedere l'argomento "Error Message Severity Levels" \(Livelli di gravità dei messaggi di errore\) nella documentazione online di SQL Server.  
  
 L'evento <xref:System.Data.SqlClient.SqlConnection.InfoMessage> riceve un oggetto <xref:System.Data.SqlClient.SqlInfoMessageEventArgs> che contiene, nella proprietà **Errors**, una raccolta di messaggi dall'origine dati.  È possibile eseguire una query negli oggetti **Error** di questa raccolta per ottenere il numero dell'errore, il testo del messaggio e l'origine dell'errore.  Il provider di dati .NET Framework per SQL Server include inoltre i dettagli sul database, sulla stored procedure e sul numero di riga da cui proviene il messaggio.  
  
### Esempio  
 Nell'esempio di codice seguente viene illustrato come aggiungere un gestore eventi per l'evento <xref:System.Data.SqlClient.SqlConnection.InfoMessage>.  
  
```vb  
' Assumes that connection represents a SqlConnection object.  
  AddHandler connection.InfoMessage, _  
    New SqlInfoMessageEventHandler(AddressOf OnInfoMessage)  
  
Private Shared Sub OnInfoMessage(sender As Object, _  
  args As SqlInfoMessageEventArgs)  
  Dim err As SqlError  
  For Each err In args.Errors  
    Console.WriteLine("The {0} has received a severity {1}, _  
       state {2} error number {3}\n" & _  
      "on line {4} of procedure {5} on server {6}:\n{7}", _  
      err.Source, err.Class, err.State, err.Number, err.LineNumber, _  
    err.Procedure, err.Server, err.Message)  
  Next  
End Sub  
  
```  
  
```csharp  
// Assumes that connection represents a SqlConnection object.  
  connection.InfoMessage +=   
    new SqlInfoMessageEventHandler(OnInfoMessage);  
  
protected static void OnInfoMessage(  
  object sender, SqlInfoMessageEventArgs args)  
{  
  foreach (SqlError err in args.Errors)  
  {  
    Console.WriteLine(  
  "The {0} has received a severity {1}, state {2} error number {3}\n" +  
  "on line {4} of procedure {5} on server {6}:\n{7}",  
   err.Source, err.Class, err.State, err.Number, err.LineNumber,   
   err.Procedure, err.Server, err.Message);  
  }  
}  
  
```  
  
## Gestione di errori come InfoMessage  
 In genere, l'evento <xref:System.Data.SqlClient.SqlConnection.InfoMessage> verrà generato solo per messaggi informativi e per messaggi di avviso inviati dal server.  Tuttavia, quando si verifica un errore, l'esecuzione del metodo **ExecuteNonQuery** o **ExecuteReader** che ha avviato l'operazione del server viene interrotta e viene generata un'eccezione.  
  
 Per continuare a elaborare le restanti istruzioni di un comando indipendentemente da eventuali messaggi di errore generati dal server, impostare la proprietà <xref:System.Data.SqlClient.SqlConnection.FireInfoMessageEventOnUserErrors%2A> del tipo <xref:System.Data.SqlClient.SqlConnection> su `true`.  In questo modo, invece di generare un'eccezione e di interrompere l'elaborazione, la connessione genera l'evento di errore <xref:System.Data.SqlClient.SqlConnection.InfoMessage>.  L'applicazione client può quindi gestire questo evento e rispondere alle condizioni di errore.  
  
> [!NOTE]
>  Un errore con un livello di gravità pari a 17 o superiore che provoca l'interruzione dell'elaborazione del comando da parte del server deve essere gestito come un'eccezione.  In questo caso viene generata un'eccezione indipendentemente da come viene gestito l'errore nell'evento <xref:System.Data.SqlClient.SqlConnection.InfoMessage>.  
  
## Utilizzo dell'evento StateChange  
 L'evento **StateChange** si verifica quando viene modificato lo stato di un oggetto **Connection**.  L'evento **StateChange** riceve il tipo <xref:System.Data.StateChangeEventArgs> che consente di determinare la modifica dello stato dell'oggetto **Connection** usando le proprietà **OriginalState** e **CurrentState**.  La proprietà **OriginalState** è un'enumerazione <xref:System.Data.ConnectionState> che indica lo stato dell'oggetto **Connection** prima della modifica.  **CurrentState** è un'enumerazione <xref:System.Data.ConnectionState> che indica lo stato dell'oggetto **Connection** dopo la modifica.  
  
 Nell'esempio di codice seguente viene usato l'evento **StateChange** per scrivere un messaggio nella console quando viene modificato lo stato dell'oggetto **Connection**.  
  
```vb  
' Assumes connection represents a SqlConnection object.  
  AddHandler connection.StateChange, _  
    New StateChangeEventHandler(AddressOf OnStateChange)  
  
Protected Shared Sub OnStateChange( _  
  sender As Object, args As StateChangeEventArgs)  
  
  Console.WriteLine( _  
  "The current Connection state has changed from {0} to {1}.", _  
  args.OriginalState, args.CurrentState)  
End Sub  
  
```  
  
```csharp  
// Assumes connection represents a SqlConnection object.  
  connection.StateChange  += new StateChangeEventHandler(OnStateChange);  
  
protected static void OnStateChange(object sender,   
  StateChangeEventArgs args)  
{  
  Console.WriteLine(  
    "The current Connection state has changed from {0} to {1}.",  
      args.OriginalState, args.CurrentState);  
}  
```  
  
## Vedere anche  
 [Connessione a un'origine dati](../../../../docs/framework/data/adonet/connecting-to-a-data-source.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)