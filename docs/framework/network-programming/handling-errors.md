---
title: "Gestione degli errori | Microsoft Docs"
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
  - "Internet, eccezioni delle classi WebRequest e WebResponse"
  - "Status (proprietà)"
  - "WebExceptions (classe), informazioni"
  - "Timeout (membro di enumerazione)"
  - "ConnectFailure (membro di enumerazione)"
  - "TrustFailure (membro di enumerazione)"
  - "WebRequest (classe), eccezioni"
  - "richiesta di dati da Internet, gestione degli errori"
  - "Success (membro di enumerazione)"
  - "ricezione di dati, errori"
  - "ProtocolError (membro di enumerazione)"
  - "download di risorse Internet, gestione degli errori"
  - "WebResponse (classe), eccezioni"
  - "SendFailure (membro di enumerazione)"
  - "errori [.NET Framework], eccezioni delle classi WebRequest e WebResponse"
  - "invio di dati, errori"
  - "risposta a una richiesta Internet, gestione degli errori"
  - "NameResolutionFailure (membro di enumerazione)"
  - "KeepAliveFailure (membro di enumerazione)"
  - "risorse di rete, eccezioni delle classi WebRequest e WebResponse"
  - "RequestCanceled (membro di enumerazione)"
  - "ReceiveFailure (membro di enumerazione)"
  - "ServerProtocolViolation (membro di enumerazione)"
  - "ConnectionClosed (membro di enumerazione)"
  - "SecureChannelFailure (membro di enumerazione)"
ms.assetid: 657141cd-5cf5-4fdb-a4b2-4c040eba84b5
caps.latest.revision: 12
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 10
---
# Gestione degli errori
Le classi <xref:System.Net.WebResponse> e <xref:System.Net.WebRequest> generano sia le eccezioni di sistema \(ad esempio <xref:System.ArgumentException>\) che le eccezioni web specifiche \(ossia [WebExceptions](frlrfsystemnetwebexceptionclasstopic) generato dal metodo <xref:System.Net.WebRequest.GetResponse%2A> \).  
  
 Ogni **WebException** include una proprietà <xref:System.Net.WebException.Status%2A> contenente un valore dall'enumerazione <xref:System.Net.WebExceptionStatus>.  È possibile esaminare la proprietà **Status** per determinare l'errore che si è verificata ed effettuare le operazioni appropriate per correggere l'errore.  
  
 Nella tabella seguente vengono descritti i valori possibili della proprietà **Status**.  
  
|Stato|Descrizione|  
|-----------|-----------------|  
|ConnectFailure|Il servizio remoto non è possibile contattare a livello di trasporto.|  
|ConnectionClosed|La connessione è stata chiusa in anticipo.|  
|KeepAliveFailure|Il server ha chiuso una connessione effettuata con il set keep\-alive di intestazione.|  
|NameResolutionFailure|Il servizio di nome non è possibile risolvere il nome host.|  
|ProtocolError|La risposta ricevuta dal server era completa ma è indicato un errore a livello di protocollo.|  
|ReceiveFailure|Non è giunta alcuna risposta completa dal server remoto.|  
|RequestCanceled|La richiesta è stata annullata.|  
|SecureChannelFailure|Si è verificato un errore in un collegamento di canale sicuro.|  
|SendFailure|Non è stato possibile inviare una richiesta completa al server remoto.|  
|ServerProtocolViolation|La risposta del server non era una risposta HTTP valida.|  
|Operazione riuscita.|Non si è verificato alcun errore.|  
|Timeout|In qualsiasi risposta è stato ricevuto nel timeout impostato per la richiesta.|  
|TrustFailure|Non è stato possibile convalidare un certificato server.|  
|MessageLengthLimitExceeded|È stato ricevuto un messaggio che ha superato il limite specificato durante l'invio di una richiesta o durante la ricezione di una risposta dal server.|  
|In corso|Una richiesta asincrona interna è in sospeso.|  
|PipelineFailure|Questo valore supporta l'infrastruttura.NET Framework e non deve essere utilizzato direttamente nel codice.|  
|ProxyNameResolutionFailure|Il servizio di risoluzione dei nomi non è stato in grado di risolvere il nome dell'host proxy.|  
|UnknownError|Si è verificata un'eccezione di tipo sconosciuto.|  
  
 Quando la proprietà **Status** è **WebExceptionStatus.ProtocolError**, **WebResponse** che contiene la risposta dal server è disponibile.  È possibile esaminare la risposta per determinare il database di origine dell'errore di protocollo.  
  
 Di seguito viene illustrato come rilevare **WebException**.  
  
```csharp  
try   
{  
    // Create a request instance.  
    WebRequest myRequest =   
    WebRequest.Create("http://www.contoso.com");  
    // Get the response.  
    WebResponse myResponse = myRequest.GetResponse();  
    //Get a readable stream from the server.   
    Stream sr = myResponse.GetResponseStream();  
  
    //Read from the stream and write any data to the console.  
    bytesread = sr.Read( myBuffer, 0, length);  
    while( bytesread > 0 )   
    {  
        for (int i=0; i<bytesread; i++) {  
            Console.Write( "{0}", myBuffer[i]);  
        }  
        Console.WriteLine();  
        bytesread = sr.Read( myBuffer, 0, length);  
    }  
    sr.Close();  
    myResponse.Close();  
}  
catch (WebException webExcp)   
{  
    // If you reach this point, an exception has been caught.  
    Console.WriteLine("A WebException has been caught.");  
    // Write out the WebException message.  
    Console.WriteLine(webExcp.ToString());  
    // Get the WebException status code.  
    WebExceptionStatus status =  webExcp.Status;  
    // If status is WebExceptionStatus.ProtocolError,   
    //   there has been a protocol error and a WebResponse   
    //   should exist. Display the protocol error.  
    if (status == WebExceptionStatus.ProtocolError) {  
        Console.Write("The server returned protocol error ");  
        // Get HttpWebResponse so that you can check the HTTP status code.  
        HttpWebResponse httpResponse = (HttpWebResponse)webExcp.Response;  
        Console.WriteLine((int)httpResponse.StatusCode + " - "  
           + httpResponse.StatusCode);  
    }  
}  
catch (Exception e)   
{  
    // Code to catch other exceptions goes here.  
}  
```  
  
```vb  
Try  
    ' Create a request instance.  
    Dim myRequest As WebRequest = WebRequest.Create("http://www.contoso.com")  
    ' Get the response.  
    Dim myResponse As WebResponse = myRequest.GetResponse()  
    'Get a readable stream from the server.   
    Dim sr As Stream = myResponse.GetResponseStream()  
  
    Dim i As Integer      
    'Read from the stream and write any data to the console.  
    bytesread = sr.Read(myBuffer, 0, length)  
    While bytesread > 0  
        For i = 0 To bytesread - 1  
            Console.Write("{0}", myBuffer(i))  
        Next i  
        Console.WriteLine()  
        bytesread = sr.Read(myBuffer, 0, length)  
    End While  
    sr.Close()  
    myResponse.Close()  
Catch webExcp As WebException  
    ' If you reach this point, an exception has been caught.  
    Console.WriteLine("A WebException has been caught.")  
    ' Write out the WebException message.  
    Console.WriteLine(webExcp.ToString())  
    ' Get the WebException status code.  
    Dim status As WebExceptionStatus = webExcp.Status  
    ' If status is WebExceptionStatus.ProtocolError,   
    '   there has been a protocol error and a WebResponse   
    '   should exist. Display the protocol error.  
    If status = WebExceptionStatus.ProtocolError Then  
        Console.Write("The server returned protocol error ")  
        ' Get HttpWebResponse so that you can check the HTTP status code.  
        Dim httpResponse As HttpWebResponse = _  
           CType(webExcp.Response, HttpWebResponse)  
        Console.WriteLine(CInt(httpResponse.StatusCode).ToString() & _  
           " - " & httpResponse.StatusCode.ToString())  
    End If  
Catch e As Exception  
    ' Code to catch other exceptions goes here.  
End Try  
```  
  
 Applicazioni che utilizzano la generazione [SocketExceptions](frlrfsystemnetsocketssocketexceptionclasstopic) della classe <xref:System.Net.Sockets.Socket> quando si verificano degli errori su socket di Windows.  Le classi [TCPClient](frlrfsystemnetsocketstcpclientclasstopic), [TCPListener](frlrfsystemnetsocketstcplistenerclasstopic)e [UDPClient](frlrfsystemnetsocketsudpclientclasstopic) si basano sulla classe **Socket** e generano anche **SocketExceptions**.  
  
 Quando **SocketException** viene generato, la classe **SocketException** imposta la proprietà <xref:System.Net.Sockets.SocketException.ErrorCode%2A> all'ultimo errore di socket del sistema operativo che si è verificato.  Per ulteriori informazioni sui codici di errore di socket, vedere la documentazione di codice di errore Winsock 2,0 API in MSDN.  
  
## Vedere anche  
 [Nozioni fondamentali sulla gestione delle eccezioni](../../../docs/standard/exceptions/exception-handling-fundamentals.md)   
 [Richiesta di dati](../../../docs/framework/network-programming/requesting-data.md)