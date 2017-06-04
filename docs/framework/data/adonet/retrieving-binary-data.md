---
title: "Recupero di dati binari | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-ado"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 56c5a9e3-31f1-482f-bce0-ff1c41a658d0
caps.latest.revision: 5
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 5
---
# Recupero di dati binari
Per impostazione predefinita, l'oggetto **DataReader** carica i dati in arrivo come una riga non appena è disponibile una riga intera di dati.  Tuttavia, è necessario gestire gli oggetti BLOB \(Binary Large Object, oggetto binario di grandi dimensioni\) in modo diverso, poiché è possibile che contengano gigabyte di dati che non possono risiedere in una sola riga.  Il metodo **Command.ExecuteReader** dispone di un overload che accetta un argomento <xref:System.Data.CommandBehavior> per modificare il comportamento predefinito dell'oggetto **DataReader**.  È possibile passare <xref:System.Data.CommandBehavior> al metodo **ExecuteReader** per modificare il comportamento predefinito di **DataReader** in modo che, invece di caricare righe di dati, carichi i dati in modo sequenziale non appena li riceve.  Si consiglia di usare questa procedura per caricare BLOB o altre strutture di dati di grandi dimensioni.  Notare che questo comportamento può variare a seconda dell'origine dati.  La restituzione di un BLOB da Microsoft Access comporta, ad esempio, il caricamento in memoria dell'intero BLOB, anziché il caricamento sequenziale durante la ricezione.  
  
 Quando si imposta **DataReader** per usare **SequentialAccess**, è importante prestare attenzione alla sequenza con cui si accede ai campi restituiti.  Il comportamento predefinito di **DataReader**, in base al quale una riga intera viene caricata non appena è disponibile, consente di accedere ai campi restituiti in qualsiasi ordine fino a quando non viene letta la riga successiva.  Quando si usa **SequentialAccess**, tuttavia, è necessario accedere ai diversi campi restituiti da **DataReader** in ordine.  Ad esempio, se la query restituisce tre colonne, di cui la terza è un BLOB, è necessario restituire i valori del primo e del secondo campo prima di accedere ai dati BLOB nel terzo campo.  Se si accede al terzo campo prima del primo o del secondo, i valori del primo o del secondo campo non saranno più disponibili.  Questa situazione si verifica perché **SequentialAccess** ha modificato **DataReader** in modo da restituire i dati in sequenza e, dopo che sono stati letti da **DataReader**, i dati non sono più disponibili.  
  
 Quando si accede ai dati contenuti nel campo BLOB, usare le funzioni di accesso tipizzate **GetBytes** o **GetChars** del **DataReader**, che inseriscono dati in una matrice.  Per i dati di tipo carattere, è anche possibile usare **GetString**. Tuttavia,  è probabile che per risparmiare risorse di sistema si preferisca non caricare un intero valore BLOB in un'unica variabile di stringa.  È possibile invece specificare una determinata dimensione del buffer da restituire e una posizione iniziale per il primo byte o carattere da leggere dai dati restituiti.  **GetBytes** e **GetChars** restituiranno un valore `long` che rappresenta il numero di byte o caratteri restituiti.  Se si passa una matrice null a **GetBytes** o **GetChars**, il valore long restituito corrisponderà al numero totale di byte o caratteri del BLOB.  Facoltativamente, è possibile specificare un indice nella matrice come posizione iniziale per i dati che vengono letti.  
  
## Esempio  
 Nell'esempio seguente vengono restituiti l'identificatore e il logo dell'editore dal database di esempio **pubs** in Microsoft SQL Server.  L'identificatore dell'editore \(`pub_id`\) è un campo di testo è il logo è un'immagine, quindi un BLOB.  Poiché il campo **logo** è un'immagine bitmap, nell'esempio i dati binari vengono restituiti tramite **GetBytes**.  Notare che all'identificatore dell'editore nella riga corrente di dati si accede prima del logo, in quanto i campi devono essere letti in modo sequenziale.  
  
```vb  
' Assumes that connection is a valid SqlConnection object.  
Dim command As SqlCommand = New SqlCommand( _  
  "SELECT pub_id, logo FROM pub_info", connection)  
  
' Writes the BLOB to a file (*.bmp).  
Dim stream As FileStream                   
' Streams the binary data to the FileStream object.  
Dim writer As BinaryWriter                 
' The size of the BLOB buffer.  
Dim bufferSize As Integer = 100        
' The BLOB byte() buffer to be filled by GetBytes.  
Dim outByte(bufferSize - 1) As Byte    
' The bytes returned from GetBytes.  
Dim retval As Long                     
' The starting position in the BLOB output.  
Dim startIndex As Long = 0             
  
' The publisher id to use in the file name.  
Dim pubID As String = ""              
  
' Open the connection and read data into the DataReader.  
connection.Open()  
Dim reader As SqlDataReader = command.ExecuteReader(CommandBehavior.SequentialAccess)  
  
Do While reader.Read()  
  ' Get the publisher id, which must occur before getting the logo.  
  pubID = reader.GetString(0)  
  
  ' Create a file to hold the output.  
  stream = New FileStream( _  
    "logo" & pubID & ".bmp", FileMode.OpenOrCreate, FileAccess.Write)  
  writer = New BinaryWriter(stream)  
  
  ' Reset the starting byte for a new BLOB.  
  startIndex = 0  
  
  ' Read bytes into outByte() and retain the number of bytes returned.  
  retval = reader.GetBytes(1, startIndex, outByte, 0, bufferSize)  
  
  ' Continue while there are bytes beyond the size of the buffer.  
  Do While retval = bufferSize  
    writer.Write(outByte)  
    writer.Flush()  
  
    ' Reposition start index to end of the last buffer and fill buffer.  
    startIndex += bufferSize  
    retval = reader.GetBytes(1, startIndex, outByte, 0, bufferSize)  
  Loop  
  
  ' Write the remaining buffer.  
  writer.Write(outByte, 0 , retval - 1)  
  writer.Flush()  
  
  ' Close the output file.  
  writer.Close()  
  stream.Close()  
Loop  
  
' Close the reader and the connection.  
reader.Close()  
connection.Close()  
  
```  
  
```csharp  
// Assumes that connection is a valid SqlConnection object.  
SqlCommand command = new SqlCommand(  
  "SELECT pub_id, logo FROM pub_info", connection);  
  
// Writes the BLOB to a file (*.bmp).  
FileStream stream;                            
// Streams the BLOB to the FileStream object.  
BinaryWriter writer;                          
  
// Size of the BLOB buffer.  
int bufferSize = 100;                     
// The BLOB byte[] buffer to be filled by GetBytes.  
byte[] outByte = new byte[bufferSize];    
// The bytes returned from GetBytes.  
long retval;                              
// The starting position in the BLOB output.  
long startIndex = 0;                      
  
// The publisher id to use in the file name.  
string pubID = "";                       
  
// Open the connection and read data into the DataReader.  
connection.Open();  
SqlDataReader reader = command.ExecuteReader(CommandBehavior.SequentialAccess);  
  
while (reader.Read())  
{  
  // Get the publisher id, which must occur before getting the logo.  
  pubID = reader.GetString(0);    
  
  // Create a file to hold the output.  
  stream = new FileStream(  
    "logo" + pubID + ".bmp", FileMode.OpenOrCreate, FileAccess.Write);  
  writer = new BinaryWriter(stream);  
  
  // Reset the starting byte for the new BLOB.  
  startIndex = 0;  
  
  // Read bytes into outByte[] and retain the number of bytes returned.  
  retval = reader.GetBytes(1, startIndex, outByte, 0, bufferSize);  
  
  // Continue while there are bytes beyond the size of the buffer.  
  while (retval == bufferSize)  
  {  
    writer.Write(outByte);  
    writer.Flush();  
  
    // Reposition start index to end of last buffer and fill buffer.  
    startIndex += bufferSize;  
    retval = reader.GetBytes(1, startIndex, outByte, 0, bufferSize);  
  }  
  
  // Write the remaining buffer.  
  writer.Write(outByte, 0, (int)retval - 1);  
  writer.Flush();  
  
  // Close the output file.  
  writer.Close();  
  stream.Close();  
}  
  
// Close the reader and the connection.  
reader.Close();  
connection.Close();  
```  
  
## Vedere anche  
 [Working with DataReaders](http://msdn.microsoft.com/it-it/126a966a-d08d-4d22-a19f-f432908b2b54)   
 [Dati binari e con valori di grandi dimensioni SQL Server](../../../../docs/framework/data/adonet/sql/sql-server-binary-and-large-value-data.md)   
 [Provider ADO.NET gestiti e centro per sviluppatori di set di dati](http://go.microsoft.com/fwlink/?LinkId=217917)