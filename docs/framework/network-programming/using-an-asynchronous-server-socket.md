---
title: "Uso di un socket server asincrono | Microsoft Docs"
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
  - "Socket (classe), socket server asincroni"
  - "richieste dati, socket"
  - "socket, socket server asincroni"
  - "richiesta di dati da Internet, socket"
  - "socket server"
  - "ricezione di dati, socket"
  - "socket server asincroni"
  - "protocolli, socket"
  - "Internet, socket"
ms.assetid: 813489a9-3efd-41b6-a33f-371d55397676
caps.latest.revision: 11
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 11
---
# Uso di un socket server asincrono
I socket del server asincroni utilizzano il modello di programmazione asincrona di .NET Framework per l'elaborazione delle richieste di servizio di rete.  La classe <xref:System.Net.Sockets.Socket> segue il modello di denominazione asincrono.NET Framework standard, ad esempio, il metodo sincrono <xref:System.Net.Sockets.Socket.Accept%2A> corrisponde a <xref:System.Net.Sockets.Socket.BeginAccept%2A> e metodi asincroni <xref:System.Net.Sockets.Socket.EndAccept%2A>.  
  
 Un socket del server asincrono richiede un metodo di avviare accetta le richieste di connessione dalla rete, da un metodo callback di gestire le richieste di connessione e di avvio ricezione di dati dalla rete e un metodo di callback per terminare ricezione di dati.  Tutti questi metodi sono ulteriormente trattati in questa sezione.  
  
 Nell'esempio seguente, avviare accetta le richieste di connessione dalla rete, il metodo `StartListening` inizializza **Socket** quindi utilizzato il metodo **BeginAccept** per avviare l'accettazione di connessioni nuove.  Il metodo di callback di accettazione viene chiamato quando una nuova richiesta di connessione viene ricevuta su socket.  È responsabilità di ottenere l'istanza **Socket** che gestisce la connessione e passare tale **Socket** al thread che elabora la richiesta.  Il metodo di callback di accettazione implementa il delegato <xref:System.AsyncCallback> ; restituisce una void e accetta un solo parametro di tipo <xref:System.IAsyncResult>.  L'esempio seguente è la shell di un metodo callback di accettazione.  
  
```vb  
Sub acceptCallback(ar As IAsyncResult)  
    ' Add the callback code here.  
End Sub 'acceptCallback  
```  
  
```csharp  
void acceptCallback( IAsyncResult ar) {  
    // Add the callback code here.  
}  
```  
  
 Il metodo **BeginAccept** accetta due parametri, un delegato **AsyncCallback** che indica il metodo di callback di accettazione e un oggetto utilizzato per passare informazioni sullo stato al metodo di callback.  Nell'esempio seguente, **Socket** in ascolto viene passato al metodo di callback con il parametro *di stato*.  In questo esempio viene creato un delegato **AsyncCallback** e avvia l'accettazione di connessioni dalla rete.  
  
```vb  
listener.BeginAccept( _  
    New AsyncCallback(SocketListener.acceptCallback),_  
    listener)  
```  
  
```csharp  
listener.BeginAccept(  
    new AsyncCallback(SocketListener.acceptCallback),   
    listener);  
```  
  
 L'utilizzo asincrono sockets thread dal pool di thread di sistema per elaborare le connessioni in ingresso.  Un thread è responsabile dell'accettazione di connessioni, un altro thread viene utilizzato per gestire le connessioni in ingresso e un altro thread è responsabile della ricezione di dati dalla connessione.  Questi potrebbero essere lo stesso thread, a seconda del thread assegnato dal pool di thread.  Nell'esempio seguente, la classe <xref:System.Threading.ManualResetEvent?displayProperty=fullName> sospende l'esecuzione del thread e segnala principali per l'esecuzione può continuare.  
  
 Nell'esempio seguente viene illustrato un metodo asincrono che crea un Socket TCP\/IP asincrono nel computer locale e avvia accettazione di connessioni.  Si presuppone che sia **ManualResetEvent** globale denominato `allDone`, che il metodo sia un membro `SocketListener`classe denominata e un metodo callback denominato `acceptCallback` è definito.  
  
```vb  
Public Sub StartListening()  
    Dim ipHostInfo As IPHostEntry = Dns.Resolve(Dns.GetHostName())  
    Dim localEP = New IPEndPoint(ipHostInfo.AddressList(0), 11000)  
  
    Console.WriteLine("Local address and port : {0}", localEP.ToString())  
  
    Dim listener As New Socket(localEP.Address.AddressFamily, _  
       SocketType.Stream, ProtocolType.Tcp)  
  
    Try  
        listener.Bind(localEP)  
        listener.Listen(10)  
  
        While True  
            allDone.Reset()  
  
            Console.WriteLine("Waiting for a connection...")  
            listener.BeginAccept(New _  
                AsyncCallback(SocketListener.acceptCallback), _  
                listener)  
  
            allDone.WaitOne()  
        End While  
    Catch e As Exception  
        Console.WriteLine(e.ToString())  
    End Try  
    Console.WriteLine("Closing the listener...")  
End Sub 'StartListening  
  
```  
  
```csharp  
public void StartListening() {  
    IPHostEntry ipHostInfo = Dns.Resolve(Dns.GetHostName());  
    IPEndPoint localEP = new IPEndPoint(ipHostInfo.AddressList[0],11000);  
  
    Console.WriteLine("Local address and port : {0}",localEP.ToString());  
  
    Socket listener = new Socket( localEP.Address.AddressFamily,  
        SocketType.Stream, ProtocolType.Tcp );  
  
    try {  
        listener.Bind(localEP);  
        listener.Listen(10);  
  
        while (true) {  
            allDone.Reset();  
  
            Console.WriteLine("Waiting for a connection...");  
            listener.BeginAccept(  
                new AsyncCallback(SocketListener.acceptCallback),   
                listener );  
  
            allDone.WaitOne();  
        }  
    } catch (Exception e) {  
        Console.WriteLine(e.ToString());  
    }  
  
    Console.WriteLine( "Closing the listener...");  
}  
```  
  
 Il metodo di callback di accettazione \(`acceptCallback` nell'esempio precedente\) è responsabile della creazione di thread principale dell'applicazione per continuare a sviluppare, stabilire la connessione al client e avviare l'operazione asincrona lettura di dati dal client.  L'esempio seguente è la prima parte di un'implementazione del metodo `acceptCallback`.  Questa sezione del metodo segnala il thread principale dell'applicazione per continuare a sviluppare e viene stabilita la connessione al client.  Si presuppone **ManualResetEvent** globale denominato `allDone`.  
  
```vb  
Public Sub acceptCallback(ar As IAsyncResult)  
    allDone.Set()  
  
    Dim listener As Socket = CType(ar.AsyncState, Socket)  
    Dim handler As Socket = listener.EndAccept(ar)  
  
    ' Additional code to read data goes here.  
End Sub 'acceptCallback  
```  
  
```csharp  
public void acceptCallback(IAsyncResult ar) {  
    allDone.Set();  
  
    Socket listener = (Socket) ar.AsyncState;  
    Socket handler = listener.EndAccept(ar);  
  
    // Additional code to read data goes here.    
}  
```  
  
 La lettura di dati da un socket client richiede un oggetto di stato con valori di sessioni tra le chiamate asincrone.  Nell'esempio seguente viene implementato un oggetto stato per la ricezione della stringa dal client remoti.  Contiene i campi per il client socket, un buffer di dati per ricevere dati e <xref:System.Text.StringBuilder> per creare la stringa di dati inviati dal client.  Inserire questi campi nell'oggetto stato ai relativi valori da mantenere tra più chiamate per leggere i dati da socket client.  
  
```vb  
Public Class StateObject  
    Public workSocket As Socket = Nothing  
    Public BufferSize As Integer = 1024  
    Public buffer(BufferSize) As Byte  
    Public sb As New StringBuilder()  
End Class 'StateObject  
```  
  
```csharp  
public class StateObject {  
    public Socket workSocket = null;  
    public const int BufferSize = 1024;  
    public byte[] buffer = new byte[BufferSize];  
    public StringBuilder sb = new StringBuilder();  
}  
```  
  
 La sezione del metodo `acceptCallback` che avvia la ricezione di dati da socket client innanzitutto inizializza un'istanza della classe `StateObject` quindi chiama il metodo <xref:System.Net.Sockets.Socket.BeginReceive%2A> per iniziare la lettura di dati da socket client in modo asincrono.  
  
 Nell'esempio seguente viene illustrato il metodo completo `acceptCallback`.  Si presuppone che sia **ManualResetEvent** globale denominato `allDone,` che la classe `StateObject` viene definito e che il metodo `readCallback` è definito in una classe denominata `SocketListener`.  
  
```vb  
Public Shared Sub acceptCallback(ar As IAsyncResult)  
    ' Get the socket that handles the client request.  
    Dim listener As Socket = CType(ar.AsyncState, Socket)  
    Dim handler As Socket = listener.EndAccept(ar)  
  
    ' Signal the main thread to continue.  
    allDone.Set()  
  
    ' Create the state object.  
    Dim state As New StateObject()  
    state.workSocket = handler  
    handler.BeginReceive(state.buffer, 0, state.BufferSize, 0, _  
        AddressOf AsynchronousSocketListener.readCallback, state)  
End Sub 'acceptCallback  
  
```  
  
```csharp  
public static void acceptCallback(IAsyncResult ar) {  
    // Get the socket that handles the client request.  
    Socket listener = (Socket) ar.AsyncState;  
    Socket handler = listener.EndAccept(ar);  
  
    // Signal the main thread to continue.  
    allDone.Set();  
  
    // Create the state object.  
    StateObject state = new StateObject();  
    state.workSocket = handler;  
    handler.BeginReceive( state.buffer, 0, StateObject.BufferSize, 0,  
        new AsyncCallback(AsynchronousSocketListener.readCallback), state);  
}  
```  
  
 Il metodo finale che deve essere implementato per il server asincrono di socket è il metodo di callback lettura che restituisce i dati inviati dal client.  Come metodo di callback di accettazione, il metodo di callback lettura è un delegato **AsyncCallback**.  Questo metodo legge uno o più byte da socket client nel buffer di dati e quindi chiama il metodo **BeginReceive** nuovamente finché i dati inviati dal client non siano completi.  Una volta che l'intero messaggio è stato letto dal client, la stringa visualizzata nella console e un socket del server che gestisce la connessione al client viene chiuso.  
  
 Nell'esempio seguente viene implementato il metodo `readCallback`.  Si presuppone che la classe `StateObject` sia definita.  
  
```vb  
Public Shared Sub readCallback(ar As IAsyncResult)  
    Dim state As StateObject = CType(ar.AsyncState, StateObject)  
    Dim handler As Socket = state.workSocket  
  
    ' Read data from the client socket.   
    Dim read As Integer = handler.EndReceive(ar)  
  
    ' Data was read from the client socket.  
    If read > 0 Then  
        state.sb.Append(Encoding.ASCII.GetString(state.buffer, 0, read))  
        handler.BeginReceive(state.buffer, 0, state.BufferSize, 0, _  
            AddressOf readCallback, state)  
    Else  
        If state.sb.Length > 1 Then  
            ' All the data has been read from the client;  
            ' display it on the console.  
            Dim content As String = state.sb.ToString()  
            Console.WriteLine("Read {0} bytes from socket." + _  
                ControlChars.Cr + " Data : {1}", content.Length, content)  
        End If  
    End If  
End Sub 'readCallback  
  
```  
  
```csharp  
public static void readCallback(IAsyncResult ar) {  
    StateObject state = (StateObject) ar.AsyncState;  
    Socket handler = state.WorkSocket;  
  
    // Read data from the client socket.  
    int read = handler.EndReceive(ar);  
  
    // Data was read from the client socket.  
    if (read > 0) {  
        state.sb.Append(Encoding.ASCII.GetString(state.buffer,0,read));  
        handler.BeginReceive(state.buffer,0,StateObject.BufferSize, 0,  
            new AsyncCallback(readCallback), state);  
    } else {  
        if (state.sb.Length > 1) {  
            // All the data has been read from the client;  
            // display it on the console.  
            string content = state.sb.ToString();  
            Console.WriteLine("Read {0} bytes from socket.\n Data : {1}",  
               content.Length, content);  
        }  
        handler.Close();  
    }  
}  
```  
  
## Vedere anche  
 [Uso di un socket server sincrono](../../../docs/framework/network-programming/using-a-synchronous-server-socket.md)   
 [Esempio di socket server asincrono](../../../docs/framework/network-programming/asynchronous-server-socket-example.md)   
 [Threading](../../../docs/standard/threading/index.md)   
 [Attesa con socket](../../../docs/framework/network-programming/listening-with-sockets.md)