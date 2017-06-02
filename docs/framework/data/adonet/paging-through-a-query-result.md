---
title: "Paging del risultato di una query | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fa360c46-e5f8-411e-a711-46997771133d
caps.latest.revision: 3
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 3
---
# Paging del risultato di una query
Il paging del risultato di una query corrisponde al processo di restituzione dei risultati di una query in subset di dati di dimensioni inferiori o pagine.  Si tratta di una tecnica comunemente usata per la visualizzazione di risultati in blocchi di dimensioni ridotte e di facile gestione.  
  
 In **DataAdapter** è disponibile una funzionalità che consente la restituzione di un'unica pagina di dati, tramite gli overload del metodo **Fill**.  Questa soluzione potrebbe non rivelarsi ottimale per il paging di una quantità elevata di risultati di query, poiché, sebbene **DataAdapter** compili la <xref:System.Data.DataTable> o <xref:System.Data.DataSet> di destinazione usando solo i record richiesti, le risorse per la restituzione dell'intera query sono ancora in uso.  Per restituire una pagina di dati da un'origine dati senza usare le risorse per la restituzione dell'intera query, specificare dei criteri aggiuntivi per la query, in modo che vengano restituite solo le righe necessarie.  
  
 Per usare il metodo **Fill** per la restituzione di una pagina di dati, specificare **startRecord**, indicando il primo record della pagina di dati, e un parametro **maxRecords**, per il numero di record che devono essere contenuti nella pagina di dati.  
  
 Nell'esempio di codice seguente viene mostrato come usare il metodo **Fill** per restituire la prima pagina di un risultato di una query, in cui la dimensione della pagina corrisponde a cinque record.  
  
```vb  
Dim currentIndex As Integer = 0  
Dim pageSize As Integer = 5  
  
Dim orderSQL As String = "SELECT * FROM dbo.Orders ORDER BY OrderID"  
' Assumes that connection is a valid SqlConnection object.  
Dim adapter As SqlDataAdapter = _  
  New SqlDataAdapter(orderSQL, connection)  
  
Dim dataSet As DataSet = New DataSet()  
adapter.Fill(dataSet, currentIndex, pageSize, "Orders")  
```  
  
```csharp  
int currentIndex = 0;  
int pageSize = 5;  
  
string orderSQL = "SELECT * FROM Orders ORDER BY OrderID";  
// Assumes that connection is a valid SqlConnection object.  
SqlDataAdapter adapter = new SqlDataAdapter(orderSQL, connection);  
  
DataSet dataSet = new DataSet();  
adapter.Fill(dataSet, currentIndex, pageSize, "Orders");  
```  
  
 Nell'esempio precedente il **DataSet** viene compilato solo con cinque record, ma viene restituita l'intera tabella **Orders**.  Per compilare l'oggetto **DataSet** con gli stessi cinque record, ma restituire solo cinque record, usare le clausole TOP e WHERE nell'istruzione SQL, come illustrato nell'esempio seguente.  
  
```vb  
Dim pageSize As Integer = 5  
  
Dim orderSQL As String = "SELECT TOP " & pageSize & _  
  " * FROM Orders ORDER BY OrderID"  
Dim adapter As SqlDataAdapter = _  
  New SqlDataAdapter(orderSQL, connection)  
  
Dim dataSet As DataSet = New DataSet()  
adapter.Fill(dataSet, "Orders")   
```  
  
```csharp  
int pageSize = 5;  
  
string orderSQL = "SELECT TOP " + pageSize +   
  " * FROM Orders ORDER BY OrderID";  
SqlDataAdapter adapter = new SqlDataAdapter(orderSQL, connection);  
  
DataSet dataSet = new DataSet();  
adapter.Fill(dataSet, "Orders");  
```  
  
 Notare che, quando si esegue in questo modo il paging dei risultati della query, è necessario conservare l'identificatore univoco in base al quale sono ordinate le righe, in modo da passare l'identificatore univoco al comando per restituire la pagina successiva di record, come illustrato nell'esempio seguente.  
  
```vb  
Dim lastRecord As String = _  
  dataSet.Tables("Orders").Rows(pageSize - 1)("OrderID").ToString()  
```  
  
```csharp  
string lastRecord =   
  dataSet.Tables["Orders"].Rows[pageSize - 1]["OrderID"].ToString();  
```  
  
 Per restituire la pagina successiva di record usando l'overload del metodo **Fill** che accetta i parametri **startRecord** e **maxRecords**, incrementare l'indice di record corrente sulla base della dimensione della pagina e compilare la tabella.  Ricordare che il server database restituisce tutti i risultati della query, anche se al **DataSet** viene aggiunta solo una pagina di record.  Nell'esempio di codice seguente i contenuti delle tabelle vengono cancellati prima che tali tabelle siano compilate con la pagina successiva di dati.  Per ridurre i percorsi al server database, è possibile archiviare in una cache locale un determinato numero di righe restituite.  
  
```vb  
currentIndex = currentIndex + pageSize  
  
dataSet.Tables("Orders").Rows.Clear()  
  
adapter.Fill(dataSet, currentIndex, pageSize, "Orders")  
```  
  
```csharp  
currentIndex += pageSize;  
  
dataSet.Tables["Orders"].Rows.Clear();  
  
adapter.Fill(dataSet, currentIndex, pageSize, "Orders");  
```  
  
 Per restituire la pagina successiva di record senza che il server database restituisca l'intera query, specificare dei criteri restrittivi per l'istruzione SELECT.  Poiché nell'esempio precedente l'ultimo record restituito viene conservato, è possibile usare tale record nella clausola WHERE per specificare un punto di partenza per la query, come illustrato nel seguente esempio di codice.  
  
```vb  
orderSQL = "SELECT TOP " & pageSize & _  
  " * FROM Orders WHERE OrderID > " & lastRecord & " ORDER BY OrderID"  
adapter.SelectCommand.CommandText = orderSQL  
  
dataSet.Tables("Orders").Rows.Clear()  
  
adapter.Fill(dataSet, "Orders")  
```  
  
```csharp  
orderSQL = "SELECT TOP " + pageSize +   
  " * FROM Orders WHERE OrderID > " + lastRecord + " ORDER BY OrderID";  
adapter.SelectCommand.CommandText = orderSQL;  
  
dataSet.Tables["Orders"].Rows.Clear();  
  
adapter.Fill(dataSet, "Orders");  
```  
  
## Vedere anche  
 [DataAdapter e DataReader](../../../../docs/framework/data/adonet/dataadapters-and-datareaders.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)