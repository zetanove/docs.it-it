---
title: "Uso di un socket server sincrono | Microsoft Docs"
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
  - "socket server sincroni"
  - "invio di dati, socket"
  - "richieste dati, socket"
  - "richiesta di dati da Internet, socket"
  - "socket server"
  - "ricezione di dati, socket"
  - "Socket (classe), socket server sincroni"
  - "protocolli, socket"
  - "socket, socket server sincroni"
  - "Internet, socket"
ms.assetid: d1ce882e-653e-41f5-9289-844ec855b804
caps.latest.revision: 9
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 9
---
# Uso di un socket server sincrono
I socket del server sincroni sospende l'esecuzione dell'applicazione fino a ricevere una richiesta di connessione su socket.  I socket del server sincroni non sono adatti per le applicazioni che fanno massiccio di rete nell'operazione, ma possono essere adatte per le applicazioni semplici di rete.  
  
 Dopo <xref:System.Net.Sockets.Socket> è impostato per rimanere in ascolto su un endpoint tramite i metodi <xref:System.Net.Sockets.Socket.Listen%2A> e <xref:System.Net.Sockets.Socket.Bind%2A>, è pronto per accettare le richieste di connessione in ingresso mediante il metodo <xref:System.Net.Sockets.Socket.Accept%2A>.  L'applicazione viene sospesa fino a ricevere una richiesta di connessione quando il metodo **Accept** viene chiamato.  
  
 Quando una richiesta di connessione viene ricevuta, **Accept** restituisce una nuova istanza **Socket** associata al client connesso.  Nell'esempio vengono letti i dati dal client, visualizza nella console e è possibile visualizzare i dati nel client.  **Socket** non specifica alcun protocollo di messaggistica, pertanto i contrassegni di “\<EOF\>„ stringa la fine dei dati del messaggio.  Si presuppone che **Socket** denominato `listener`sia inizializzata e stato associato a un endpoint.  
  
```vb  
Console.WriteLine("Waiting for a connection...")  
Dim handler As Socket = listener.Accept()  
Dim data As String = Nothing  
  
While True  
    bytes = New Byte(1024) {}  
    Dim bytesRec As Integer = handler.Receive(bytes)  
    data += Encoding.ASCII.GetString(bytes, 0, bytesRec)  
    If data.IndexOf("<EOF>") > - 1 Then  
        Exit While  
    End If  
End While  
  
Console.WriteLine("Text received : {0}", data)  
  
Dim msg As Byte() = Encoding.ASCII.GetBytes(data)  
handler.Send(msg)  
handler.Shutdown(SocketShutdown.Both)  
handler.Close()  
  
```  
  
```csharp  
Console.WriteLine("Waiting for a connection...");  
Socket handler = listener.Accept();  
String data = null;  
  
while (true) {  
    bytes = new byte[1024];  
    int bytesRec = handler.Receive(bytes);  
    data += Encoding.ASCII.GetString(bytes,0,bytesRec);  
    if (data.IndexOf("<EOF>") > -1) {  
        break;  
    }  
}  
  
Console.WriteLine( "Text received : {0}", data);  
  
byte[] msg = Encoding.ASCII.GetBytes(data);  
handler.Send(msg);  
handler.Shutdown(SocketShutdown.Both);  
handler.Close();  
```  
  
## Vedere anche  
 [Uso di un socket server asincrono](../../../docs/framework/network-programming/using-an-asynchronous-server-socket.md)   
 [Esempio di socket server sincrono](../../../docs/framework/network-programming/synchronous-server-socket-example.md)   
 [Attesa con socket](../../../docs/framework/network-programming/listening-with-sockets.md)