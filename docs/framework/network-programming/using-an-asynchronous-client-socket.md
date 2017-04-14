---
title: "Uso di un socket client asincrono | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
  - "C++"
  - "jsharp"
helpviewer_keywords: 
  - "protocolli applicativi, socket"
  - "invio di dati, socket"
  - "richieste dati, socket"
  - "socket client asincroni"
  - "Socket (classe), socket client asincroni"
  - "richiesta di dati da Internet, socket"
  - "socket, socket client asincroni"
  - "ricezione di dati, socket"
  - "protocolli, socket"
  - "Internet, socket"
  - "socket client"
ms.assetid: fd85bc88-e06c-467d-a30d-9fd7cffcfca1
caps.latest.revision: 14
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 12
---
# Uso di un socket client asincrono
Un socket client asincrono non sospende l'applicazione mentre attende operazioni di rete completare.  Invece, viene utilizzato il modello di programmazione asincrona.NET Framework standard per elaborare la connessione di rete su un thread mentre l'applicazione continua a essere in esecuzione sul thread originale.  I socket asincroni sono adatti per le applicazioni che fanno massiccio di rete o che non possono restare operazioni di rete per completare prima di continuare.  
  
 La classe <xref:System.Net.Sockets.Socket> segue .NET Framework che denomina il modello per i metodi asincroni, ad esempio, il metodo sincrono <xref:System.Net.Sockets.Socket.Receive%2A> corrisponde a <xref:System.Net.Sockets.Socket.BeginReceive%2A> e metodi asincroni <xref:System.Net.Sockets.Socket.EndReceive%2A>.  
  
 Le operazioni asincrone richiedono un metodo callback di restituire il risultato dell'operazione.  Se non è necessario conoscere il risultato, nessun metodo di callback è necessario.  Il codice di esempio in questa sezione viene illustrato l'utilizzo di un metodo per avviare la connessione a un dispositivo di rete e un metodo di callback per completare la connessione, un metodo per avviare inviare dati e un metodo di callback per il completamento dell'invio e un metodo per avviare la ricezione dei dati e il metodo di callback per terminare ricezione di dati.  
  
 Thread asincrone di utilizzo sockets dal pool di thread di sistema per elaborare le connessioni di rete.  Un thread è responsabile dell'invio e ricezione dei dati, altri thread terminano la connessione al dispositivo di rete e inviano e ricevono i dati.  Negli esempi seguenti, le istanze della classe <xref:System.Threading.ManualResetEvent?displayProperty=fullName> vengono utilizzate per sospendere l'esecuzione del thread principale e per segnalare quando l'esecuzione può continuare.  
  
 Nell'esempio seguente, connettere un socket asincrono in un dispositivo di rete, il metodo `Connect`inizializza **Socket** quindi chiama il metodo [BeginConnect](frlrfsystemnetsocketssocketclassconnecttopic), passando un endpoint remoto che rappresenta il dispositivo di rete, il metodo callback di connettersi e un oggetto stato **Socket**\(client\), utilizzato per passare informazioni sullo stato tra le chiamate asincrone.  L'esempio implementa il metodo `Connect` per connettersi **Socket** specificato all'oggetto specificato.  Si presuppone **ManualResetEvent** globale denominato `connectDone`.  
  
```vb  
Public Shared Sub Connect(remoteEP As EndPoint, client As Socket)  
    client.BeginConnect(remoteEP, _  
       AddressOf ConnectCallback, client)  
  
    connectDone.WaitOne()  
End Sub 'Connect  
```  
  
```csharp  
public static void Connect(EndPoint remoteEP, Socket client) {  
    client.BeginConnect(remoteEP,   
        new AsyncCallback(ConnectCallback), client );  
  
   connectDone.WaitOne();  
}  
```  
  
 Il metodo di callback `ConnectCallback` di connettersi implementa il delegato <xref:System.AsyncCallback>.  Si connette al dispositivo remoto quando il dispositivo remoto è disponibile e segnala il thread dell'applicazione della connessione è piena impostando **ManualResetEvent**`connectDone`.  Il seguente codice implementa il metodo `ConnectCallback`.  
  
```vb  
Private Shared Sub ConnectCallback(ar As IAsyncResult)  
    Try  
        ' Retrieve the socket from the state object.  
        Dim client As Socket = CType(ar.AsyncState, Socket)  
  
        ' Complete the connection.  
        client.EndConnect(ar)  
  
        Console.WriteLine("Socket connected to {0}", _  
            client.RemoteEndPoint.ToString())  
  
        ' Signal that the connection has been made.  
        connectDone.Set()  
    Catch e As Exception  
        Console.WriteLine(e.ToString())  
    End Try  
End Sub 'ConnectCallback  
  
```  
  
```csharp  
private static void ConnectCallback(IAsyncResult ar) {  
    try {  
        // Retrieve the socket from the state object.  
        Socket client = (Socket) ar.AsyncState;  
  
        // Complete the connection.  
        client.EndConnect(ar);  
  
        Console.WriteLine("Socket connected to {0}",  
            client.RemoteEndPoint.ToString());  
  
        // Signal that the connection has been made.  
        connectDone.Set();  
    } catch (Exception e) {  
        Console.WriteLine(e.ToString());  
    }  
}  
```  
  
 Il metodo di esempio `Send` codifica i dati in formato stringa specificati in formato ASCII e viene inviato in modo asincrono al dispositivo di rete rappresentato dall'oggetto specificato.  Nell'esempio seguente viene implementato il metodo `Send`.  
  
```vb  
Private Shared Sub Send(client As Socket, data As [String])  
    ' Convert the string data to byte data using ASCII encoding.  
    Dim byteData As Byte() = Encoding.ASCII.GetBytes(data)  
  
    ' Begin sending the data to the remote device.  
    client.BeginSend(byteData, 0, byteData.Length, SocketFlags.None, _  
        AddressOf SendCallback, client)  
End Sub 'Send  
  
```  
  
```csharp  
private static void Send(Socket client, String data) {  
    // Convert the string data to byte data using ASCII encoding.  
    byte[] byteData = Encoding.ASCII.GetBytes(data);  
  
    // Begin sending the data to the remote device.  
    client.BeginSend(byteData, 0, byteData.Length, SocketFlags.None,  
        new AsyncCallback(SendCallback), client);  
}  
```  
  
 Il metodo di callback `SendCallback` di inviare implementa il delegato <xref:System.AsyncCallback>.  Invia i dati quando il dispositivo di rete è possibile ricevere.  Il seguente esempio viene illustrata l'implementazione del metodo `SendCallback`.  Si presuppone **ManualResetEvent** globale denominato `sendDone`.  
  
```vb  
Private Shared Sub SendCallback(ar As IAsyncResult)  
    Try  
        ' Retrieve the socket from the state object.  
        Dim client As Socket = CType(ar.AsyncState, Socket)  
  
        ' Complete sending the data to the remote device.  
        Dim bytesSent As Integer = client.EndSend(ar)  
        Console.WriteLine("Sent {0} bytes to server.", bytesSent)  
  
        ' Signal that all bytes have been sent.  
        sendDone.Set()  
    Catch e As Exception  
        Console.WriteLine(e.ToString())  
    End Try  
End Sub 'SendCallback  
  
```  
  
```csharp  
private static void SendCallback(IAsyncResult ar) {  
    try {  
        // Retrieve the socket from the state object.  
        Socket client = (Socket) ar.AsyncState;  
  
        // Complete sending the data to the remote device.  
        int bytesSent = client.EndSend(ar);  
        Console.WriteLine("Sent {0} bytes to server.", bytesSent);  
  
        // Signal that all bytes have been sent.  
        sendDone.Set();  
    } catch (Exception e) {  
        Console.WriteLine(e.ToString());  
    }  
}  
```  
  
 La lettura di dati da un socket client richiede un oggetto di stato con valori di sessioni tra le chiamate asincrone.  La classe è un oggetto stato di esempio per ricevere dati da un socket client.  Contiene un campo per il client socket, un buffer per i dati ricevuti e <xref:System.Text.StringBuilder> utilizzare la stringa di dati in ingresso.  Inserire questi campi nell'oggetto stato ai relativi valori da mantenere tra più chiamate per leggere i dati da socket client.  
  
```vb  
Public Class StateObject  
    ' Client socket.  
    Public workSocket As Socket = Nothing   
    ' Size of receive buffer.  
    Public BufferSize As Integer = 256  
    ' Receive buffer.  
    Public buffer(256) As Byte   
    ' Received data string.  
    Public sb As New StringBuilder()  
End Class 'StateObject  
  
```  
  
```csharp  
public class StateObject {  
    // Client socket.  
    public Socket workSocket = null;  
    // Size of receive buffer.  
    public const int BufferSize = 256;  
    // Receive buffer.  
    public byte[] buffer = new byte[BufferSize];  
    // Received data string.  
    public StringBuilder sb = new StringBuilder();  
}  
```  
  
 Il metodo `Receive` di esempio è installato l'oggetto stato e quindi chiama il metodo **BeginReceive** per leggere i dati da socket client in modo asincrono.  Nell'esempio seguente viene implementato il metodo `Receive`.  
  
```vb  
Private Shared Sub Receive(client As Socket)  
    Try  
        ' Create the state object.  
        Dim state As New StateObject()  
        state.workSocket = client  
  
        ' Begin receiving the data from the remote device.  
        client.BeginReceive(state.buffer, 0, state.BufferSize, 0, _  
            AddressOf ReceiveCallback, state)  
    Catch e As Exception  
        Console.WriteLine(e.ToString())  
    End Try  
End Sub 'Receive  
  
```  
  
```csharp  
private static void Receive(Socket client) {  
    try {  
        // Create the state object.  
        StateObject state = new StateObject();  
        state.workSocket = client;  
  
        // Begin receiving the data from the remote device.  
        client.BeginReceive( state.buffer, 0, StateObject.BufferSize, 0,  
            new AsyncCallback(ReceiveCallback), state);  
    } catch (Exception e) {  
        Console.WriteLine(e.ToString());  
    }  
}  
```  
  
 Il metodo di callback di ricezione `ReceiveCallback` implementa il delegato **AsyncCallback**.  Riceve dati dal dispositivo di rete e compila una stringa di messaggio.  Legge uno o più byte di dati dalla rete nel buffer di dati e quindi chiama il metodo **BeginReceive** nuovamente finché i dati inviati dal client non siano completi.  Dopo che tutti i dati vengono letti dal client, `ReceiveCallback` segnala il thread dell'applicazione che i dati completi impostando **ManualResetEvent** `sendDone`.  
  
 Il seguente codice di esempio viene implementato il metodo `ReceiveCallback`.  Si presuppone una stringa globale denominata `response` che è contenuta la stringa ricezione e **ManualResetEvent** globale denominati `receiveDone`.  Il server deve arrestare il client socket correttamente per terminare la sessione di rete.  
  
```vb  
Private Shared Sub ReceiveCallback(ar As IAsyncResult)  
    Try  
        ' Retrieve the state object and the client socket   
        ' from the asynchronous state object.  
        Dim state As StateObject = CType(ar.AsyncState, StateObject)  
        Dim client As Socket = state.workSocket  
  
        ' Read data from the remote device.  
        Dim bytesRead As Integer = client.EndReceive(ar)  
  
        If bytesRead > 0 Then  
            ' There might be more data, so store the data received so far.  
            state.sb.Append(Encoding.ASCII.GetString(state.buffer, 0, _  
                bytesRead))  
  
            '  Get the rest of the data.  
            client.BeginReceive(state.buffer, 0, state.BufferSize, 0, _  
                AddressOf ReceiveCallback, state)  
        Else  
            ' All the data has arrived; put it in response.  
            If state.sb.Length > 1 Then  
                response = state.sb.ToString()  
            End If  
            ' Signal that all bytes have been received.  
            receiveDone.Set()  
        End If  
    Catch e As Exception  
        Console.WriteLine(e.ToString())  
    End Try  
End Sub 'ReceiveCallback  
  
```  
  
```csharp  
private static void ReceiveCallback( IAsyncResult ar ) {  
    try {  
        // Retrieve the state object and the client socket   
        // from the asynchronous state object.  
        StateObject state = (StateObject) ar.AsyncState;  
        Socket client = state.workSocket;  
        // Read data from the remote device.  
        int bytesRead = client.EndReceive(ar);  
        if (bytesRead > 0) {  
            // There might be more data, so store the data received so far.  
            state.sb.Append(Encoding.ASCII.GetString(state.buffer,0,bytesRead));  
                //  Get the rest of the data.  
            client.BeginReceive(state.buffer,0,StateObject.BufferSize,0,  
                new AsyncCallback(ReceiveCallback), state);  
        } else {  
            // All the data has arrived; put it in response.  
            if (state.sb.Length > 1) {  
                response = state.sb.ToString();  
            }  
            // Signal that all bytes have been received.  
            receiveDone.Set();  
        }  
    } catch (Exception e) {  
        Console.WriteLine(e.ToString());  
    }  
}  
```  
  
## Vedere anche  
 [Uso di un socket client sincrono](../../../docs/framework/network-programming/using-a-synchronous-client-socket.md)   
 [Attesa con socket](../../../docs/framework/network-programming/listening-with-sockets.md)   
 [Esempio di socket client asincrono](../../../docs/framework/network-programming/asynchronous-client-socket-example.md)