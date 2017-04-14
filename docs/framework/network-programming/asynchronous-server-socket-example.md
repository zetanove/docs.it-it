---
title: "Esempio di socket server asincrono | Microsoft Docs"
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
  - "socket, socket server asincroni"
  - "socket, esempi di codice"
  - "socket server asincroni"
ms.assetid: 13624cd3-f5c5-4950-8cda-31273b1fa6d1
caps.latest.revision: 10
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 10
---
# Esempio di socket server asincrono
Il codice riportato di seguito viene creato un server che riceve le richieste di connessione da client.  Il server viene compilato con un socket asincrono, pertanto l'esecuzione dell'applicazione server non viene sospesa mentre attende una connessione da un client.  L'applicazione riceve una stringa dal client, visualizzare la stringa nella console e quindi è possibile visualizzare la stringa del client.  La stringa dal client deve contenere la stringa “\<EOF\>„ per segnalare la fine del messaggio.  
  
```vb  
Imports System  
Imports System.Net  
Imports System.Net.Sockets  
Imports System.Text  
Imports System.Threading  
Imports Microsoft.VisualBasic  
  
' State object for reading client data asynchronously  
  
Public Class StateObject  
    ' Client  socket.  
    Public workSocket As Socket = Nothing  
    ' Size of receive buffer.  
    Public Const BufferSize As Integer = 1024  
    ' Receive buffer.  
    Public buffer(BufferSize) As Byte  
    ' Received data string.  
    Public sb As New StringBuilder  
End Class 'StateObject  
  
Public Class AsynchronousSocketListener  
    ' Thread signal.  
    Public Shared allDone As New ManualResetEvent(False)  
  
    ' This server waits for a connection and then uses  asychronous operations to  
    ' accept the connection, get data from the connected client,   
    ' echo that data back to the connected client.  
    ' It then disconnects from the client and waits for another client.   
    Public Shared Sub Main()  
        ' Data buffer for incoming data.  
        Dim bytes() As Byte = New [Byte](1023) {}  
  
        ' Establish the local endpoint for the socket.  
        Dim ipHostInfo As IPHostEntry = Dns.Resolve(Dns.GetHostName())  
        Dim ipAddress As IPAddress = ipHostInfo.AddressList(0)  
        Dim localEndPoint As New IPEndPoint(ipAddress, 11000)  
  
        ' Create a TCP/IP socket.  
        Dim listener As New Socket(AddressFamily.InterNetwork, SocketType.Stream, ProtocolType.Tcp)  
  
        ' Bind the socket to the local endpoint and listen for incoming connections.  
        listener.Bind(localEndPoint)  
        listener.Listen(100)  
  
        While True  
            ' Set the event to nonsignaled state.  
            allDone.Reset()  
  
            ' Start an asynchronous socket to listen for connections.  
            Console.WriteLine("Waiting for a connection...")  
            listener.BeginAccept(New AsyncCallback(AddressOf AcceptCallback), listener)  
  
            ' Wait until a connection is made and processed before continuing.  
            allDone.WaitOne()  
        End While  
    End Sub 'Main  
  
    Public Shared Sub AcceptCallback(ByVal ar As IAsyncResult)  
        ' Get the socket that handles the client request.  
        Dim listener As Socket = CType(ar.AsyncState, Socket)  
        ' End the operation.  
        Dim handler As Socket = listener.EndAccept(ar)  
  
        ' Create the state object for the async receive.  
        Dim state As New StateObject  
        state.workSocket = handler  
        handler.BeginReceive(state.buffer, 0, StateObject.BufferSize, 0, New AsyncCallback(AddressOf ReadCallback), state)  
    End Sub 'AcceptCallback  
  
    Public Shared Sub ReadCallback(ByVal ar As IAsyncResult)  
        Dim content As String = String.Empty  
  
        ' Retrieve the state object and the handler socket  
        ' from the asynchronous state object.  
        Dim state As StateObject = CType(ar.AsyncState, StateObject)  
        Dim handler As Socket = state.workSocket  
  
        ' Read data from the client socket.   
        Dim bytesRead As Integer = handler.EndReceive(ar)  
  
        If bytesRead > 0 Then  
            ' There  might be more data, so store the data received so far.  
            state.sb.Append(Encoding.ASCII.GetString(state.buffer, 0, bytesRead))  
  
            ' Check for end-of-file tag. If it is not there, read   
            ' more data.  
            content = state.sb.ToString()  
            If content.IndexOf("<EOF>") > -1 Then  
                ' All the data has been read from the   
                ' client. Display it on the console.  
                Console.WriteLine("Read {0} bytes from socket. " + vbLf + " Data : {1}", content.Length, content)  
                ' Echo the data back to the client.  
                Send(handler, content)  
            Else  
                ' Not all data received. Get more.  
                handler.BeginReceive(state.buffer, 0, StateObject.BufferSize, 0, New AsyncCallback(AddressOf ReadCallback), state)  
            End If  
        End If  
    End Sub 'ReadCallback  
  
    Private Shared Sub Send(ByVal handler As Socket, ByVal data As String)  
        ' Convert the string data to byte data using ASCII encoding.  
        Dim byteData As Byte() = Encoding.ASCII.GetBytes(data)  
  
        ' Begin sending the data to the remote device.  
        handler.BeginSend(byteData, 0, byteData.Length, 0, New AsyncCallback(AddressOf SendCallback), handler)  
    End Sub 'Send  
  
    Private Shared Sub SendCallback(ByVal ar As IAsyncResult)  
        ' Retrieve the socket from the state object.  
        Dim handler As Socket = CType(ar.AsyncState, Socket)  
  
        ' Complete sending the data to the remote device.  
        Dim bytesSent As Integer = handler.EndSend(ar)  
        Console.WriteLine("Sent {0} bytes to client.", bytesSent)  
  
        handler.Shutdown(SocketShutdown.Both)  
        handler.Close()  
        ' Signal the main thread to continue.  
        allDone.Set()  
    End Sub 'SendCallback  
End Class 'AsynchronousSocketListener  
```  
  
```csharp  
using System;  
using System.Net;  
using System.Net.Sockets;  
using System.Text;  
using System.Threading;  
  
// State object for reading client data asynchronously  
public class StateObject {  
    // Client  socket.  
    public Socket workSocket = null;  
    // Size of receive buffer.  
    public const int BufferSize = 1024;  
    // Receive buffer.  
    public byte[] buffer = new byte[BufferSize];  
// Received data string.  
    public StringBuilder sb = new StringBuilder();    
}  
  
public class AsynchronousSocketListener {  
    // Thread signal.  
    public static ManualResetEvent allDone = new ManualResetEvent(false);  
  
    public AsynchronousSocketListener() {  
    }  
  
    public static void StartListening() {  
        // Data buffer for incoming data.  
        byte[] bytes = new Byte[1024];  
  
        // Establish the local endpoint for the socket.  
        // The DNS name of the computer  
        // running the listener is "host.contoso.com".  
        IPHostEntry ipHostInfo = Dns.Resolve(Dns.GetHostName());  
        IPAddress ipAddress = ipHostInfo.AddressList[0];  
        IPEndPoint localEndPoint = new IPEndPoint(ipAddress, 11000);  
  
        // Create a TCP/IP socket.  
        Socket listener = new Socket(AddressFamily.InterNetwork,  
            SocketType.Stream, ProtocolType.Tcp );  
  
        // Bind the socket to the local endpoint and listen for incoming connections.  
        try {  
            listener.Bind(localEndPoint);  
            listener.Listen(100);  
  
            while (true) {  
                // Set the event to nonsignaled state.  
                allDone.Reset();  
  
                // Start an asynchronous socket to listen for connections.  
                Console.WriteLine("Waiting for a connection...");  
                listener.BeginAccept(   
                    new AsyncCallback(AcceptCallback),  
                    listener );  
  
                // Wait until a connection is made before continuing.  
                allDone.WaitOne();  
            }  
  
        } catch (Exception e) {  
            Console.WriteLine(e.ToString());  
        }  
  
        Console.WriteLine("\nPress ENTER to continue...");  
        Console.Read();  
  
    }  
  
    public static void AcceptCallback(IAsyncResult ar) {  
        // Signal the main thread to continue.  
        allDone.Set();  
  
        // Get the socket that handles the client request.  
        Socket listener = (Socket) ar.AsyncState;  
        Socket handler = listener.EndAccept(ar);  
  
        // Create the state object.  
        StateObject state = new StateObject();  
        state.workSocket = handler;  
        handler.BeginReceive( state.buffer, 0, StateObject.BufferSize, 0,  
            new AsyncCallback(ReadCallback), state);  
    }  
  
    public static void ReadCallback(IAsyncResult ar) {  
        String content = String.Empty;  
  
        // Retrieve the state object and the handler socket  
        // from the asynchronous state object.  
        StateObject state = (StateObject) ar.AsyncState;  
        Socket handler = state.workSocket;  
  
        // Read data from the client socket.   
        int bytesRead = handler.EndReceive(ar);  
  
        if (bytesRead > 0) {  
            // There  might be more data, so store the data received so far.  
            state.sb.Append(Encoding.ASCII.GetString(  
                state.buffer,0,bytesRead));  
  
            // Check for end-of-file tag. If it is not there, read   
            // more data.  
            content = state.sb.ToString();  
            if (content.IndexOf("<EOF>") > -1) {  
                // All the data has been read from the   
                // client. Display it on the console.  
                Console.WriteLine("Read {0} bytes from socket. \n Data : {1}",  
                    content.Length, content );  
                // Echo the data back to the client.  
                Send(handler, content);  
            } else {  
                // Not all data received. Get more.  
                handler.BeginReceive(state.buffer, 0, StateObject.BufferSize, 0,  
                new AsyncCallback(ReadCallback), state);  
            }  
        }  
    }  
  
    private static void Send(Socket handler, String data) {  
        // Convert the string data to byte data using ASCII encoding.  
        byte[] byteData = Encoding.ASCII.GetBytes(data);  
  
        // Begin sending the data to the remote device.  
        handler.BeginSend(byteData, 0, byteData.Length, 0,  
            new AsyncCallback(SendCallback), handler);  
    }  
  
    private static void SendCallback(IAsyncResult ar) {  
        try {  
            // Retrieve the socket from the state object.  
            Socket handler = (Socket) ar.AsyncState;  
  
            // Complete sending the data to the remote device.  
            int bytesSent = handler.EndSend(ar);  
            Console.WriteLine("Sent {0} bytes to client.", bytesSent);  
  
            handler.Shutdown(SocketShutdown.Both);  
            handler.Close();  
  
        } catch (Exception e) {  
            Console.WriteLine(e.ToString());  
        }  
    }  
  
    public static int Main(String[] args) {  
        StartListening();  
        return 0;  
    }  
}  
```  
  
## Vedere anche  
 [Esempio di socket client asincrono](../../../docs/framework/network-programming/asynchronous-client-socket-example.md)   
 [Uso di un socket server asincrono](../../../docs/framework/network-programming/using-an-asynchronous-server-socket.md)   
 [Esempi di codice socket](../../../docs/framework/network-programming/socket-code-examples.md)