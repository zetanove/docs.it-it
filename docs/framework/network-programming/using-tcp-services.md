---
title: "Uso dei servizi TCP | Microsoft Docs"
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
  - "richiesta di dati da Internet, TCP"
  - "ricezione di dati, TCP"
  - "TcpClient (classe), informazioni"
  - "richieste dati, TCP"
  - "protocolli applicativi, TCP"
  - "risorse di rete, TCP"
  - "invio di dati, TCP"
  - "TCP"
  - "protocolli, TCP"
  - "Internet, TCP"
ms.assetid: d2811830-3bcb-495c-b82d-cda9cf919aad
caps.latest.revision: 11
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 9
---
# Uso dei servizi TCP
La classe <xref:System.Net.Sockets.TcpClient> richiede i dati da una risorsa Internet mediante TCP.  I metodi e le proprietà **TcpClient** riassumono i dettagli per creare <xref:System.Net.Sockets.Socket> per la richiesta e la ricezione di dati utilizzando TCP.  Poiché la connessione al dispositivo remoto viene rappresentata come flusso, i dati possono essere letti e scritti con le tecniche di flusso\- gestione di .NET Framework.  
  
 Il protocollo TCP stabilisce una connessione con un endpoint remoto e di utilizzare tale connessione per inviare e ricevere i pacchetti di dati.  TCP deve garantire che i pacchetti di dati viene inviato all'endpoint e viene assemblato nell'ordine corretto in arrivo.  
  
 Per stabilire una connessione TCP, è necessario conoscere l'indirizzo del dispositivo di rete che ospita il servizio necessari e conoscere la porta TCP che il servizio viene utilizzato per comunicare.  Internet Assigned Numbers AUTHORITY \(Iana\) definisce i numeri di porta per i servizi comuni \(vedere www.iana.org\/assignments\/port\-numbers\).  I servizi non l'elenco di IANA possono includere numeri di porta compreso tra 1.024 e 65.535.  
  
 Il seguente esempio viene illustrata l'installazione **TcpClient** per connettersi a un'ora del server sulla porta TCP 13.  
  
```vb  
Imports System  
Imports System.Net.Sockets  
Imports System.Text  
  
Public Class TcpTimeClient  
    Private const portNum As Integer = 13  
    Private const hostName As String = "host.contoso.com"  
  
    ' Entry point  that delegates to C-style main Private Function.  
    Public Overloads Shared Sub Main()  
        System.Environment.ExitCode = _  
            Main(System.Environment.GetCommandLineArgs())  
    End Sub  
  
    Overloads Public Shared Function Main(args() As [String]) As Integer  
        Try  
            Dim client As New TcpClient(hostName, portNum)  
  
            Dim ns As NetworkStream = client.GetStream()  
  
            Dim bytes(1024) As Byte  
            Dim bytesRead As Integer = ns.Read(bytes, 0, bytes.Length)  
  
            Console.WriteLine(Encoding.ASCII.GetString(bytes, 0, bytesRead))  
  
        Catch e As Exception  
            Console.WriteLine(e.ToString())  
        End Try  
  
        client.Close()  
  
        Return 0  
    End Function 'Main  
End Class 'TcpTimeClient  
  
```  
  
```csharp  
using System;  
using System.Net.Sockets;  
using System.Text;  
  
public class TcpTimeClient {  
    private const int portNum = 13;  
    private const string hostName = "host.contoso.com";  
  
    public static int Main(String[] args) {  
        try {  
            TcpClient client = new TcpClient(hostName, portNum);  
  
            NetworkStream ns = client.GetStream();  
  
            byte[] bytes = new byte[1024];  
            int bytesRead = ns.Read(bytes, 0, bytes.Length);  
  
            Console.WriteLine(Encoding.ASCII.GetString(bytes,0,bytesRead));  
  
            client.Close();  
  
        } catch (Exception e) {  
            Console.WriteLine(e.ToString());  
        }  
  
        return 0;  
    }  
}  
```  
  
 <xref:System.Net.Sockets.TcpListener> viene utilizzato per monitorare una porta TCP per le richieste in arrivo e quindi per creare **Socket** o **TcpClient** che gestisce la connessione al client.  Il metodo consente <xref:System.Net.Sockets.TcpListener.Start%2A> ascolto e il metodo <xref:System.Net.Sockets.TcpListener.Stop%2A> disabilita ascolto sulla porta.  Il metodo <xref:System.Net.Sockets.TcpListener.AcceptTcpClient%2A> accetta le richieste di connessione in ingresso e crea **TcpClient** per gestire la richiesta e il metodo <xref:System.Net.Sockets.TcpListener.AcceptSocket%2A> accetta le richieste di connessione in ingresso e crea **Socket** per gestire la richiesta.  
  
 Il seguente esempio viene illustrata la creazione dell'ora del server di rete tramite **TcpListener** alla porta TCP 13 del monitor.  Quando una richiesta di connessione in ingresso viene accettata, l'ora del server è conforme con la data e l'ora corrente dal server host.  
  
```vb  
Imports System  
Imports System.Net.Sockets  
Imports System.Text  
  
Public Class TcpTimeServer  
  
    Private const portNum As Integer = 13  
  
    ' Entry point that delegates to C-style main Private Function.  
    Public Overloads Shared Sub Main()  
        System.Environment.ExitCode = _  
            Main(System.Environment.GetCommandLineArgs())  
    End Sub  
  
    Overloads Public Shared Function Main(args() As [String]) As Integer  
        Dim done As Boolean = False  
  
        Dim listener As New TcpListener(portNum)  
  
        listener.Start()  
  
        While Not done  
            Console.Write("Waiting for connection...")  
            Dim client As TcpClient = listener.AcceptTcpClient()  
  
            Console.WriteLine("Connection accepted.")  
            Dim ns As NetworkStream = client.GetStream()  
  
            Dim byteTime As Byte() = _  
                Encoding.ASCII.GetBytes(DateTime.Now.ToString())  
  
            Try  
                ns.Write(byteTime, 0, byteTime.Length)  
                ns.Close()  
                client.Close()  
            Catch e As Exception  
                Console.WriteLine(e.ToString())  
            End Try  
        End While  
  
        listener.Stop()  
  
        Return 0  
    End Function 'Main  
End Class 'TcpTimeServer  
```  
  
```csharp  
using System;  
using System.Net.Sockets;  
using System.Text;  
  
public class TcpTimeServer {  
  
    private const int portNum = 13;  
  
    public static int Main(String[] args) {  
        bool done = false;  
  
        TcpListener listener = new TcpListener(portNum);  
  
        listener.Start();  
  
        while (!done) {  
            Console.Write("Waiting for connection...");  
            TcpClient client = listener.AcceptTcpClient();  
  
            Console.WriteLine("Connection accepted.");  
            NetworkStream ns = client.GetStream();  
  
            byte[] byteTime = Encoding.ASCII.GetBytes(DateTime.Now.ToString());  
  
            try {  
                ns.Write(byteTime, 0, byteTime.Length);  
                ns.Close();  
                client.Close();  
            } catch (Exception e) {  
                Console.WriteLine(e.ToString());  
            }  
        }  
  
        listener.Stop();  
  
        return 0;  
    }  
  
}  
```  
  
## Vedere anche  
 [TCP\/UDP](../../../docs/framework/network-programming/tcp-udp.md)