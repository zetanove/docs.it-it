---
title: "Uso di un socket client sincrono | Microsoft Docs"
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
  - "richiesta di dati da Internet, socket"
  - "socket client sincroni"
  - "Socket (classe), socket client sincroni"
  - "ricezione di dati, socket"
  - "socket, socket client sincroni"
  - "protocolli, socket"
  - "Internet, socket"
  - "socket client"
ms.assetid: 945d00c6-7202-466c-9df9-140b84156d43
caps.latest.revision: 12
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 12
---
# Uso di un socket client sincrono
Un socket client sincrono sospende il programma utente mentre l'operazione di rete completa.  I socket sincroni non sono adatti per le applicazioni che fanno massiccio di rete per la relativa operazione, ma possono consentire l'accesso semplice servizi di rete per altre applicazioni.  
  
 Per inviare i dati, passare una matrice di byte a uno dei metodi di inviare\- dati della classe <xref:System.Net.Sockets.Socket> \(<xref:System.Net.Sockets.Socket.Send%2A> e <xref:System.Net.Sockets.Socket.SendTo%2A>\).  Nell'esempio seguente viene codificata una stringa in un buffer matrice di byte utilizzando la proprietà <xref:System.Text.Encoding.ASCII%2A?displayProperty=fullName> quindi trasmette il buffer del dispositivo di rete utilizzando il metodo **Send**.  Il metodo **Send** restituisce il numero di byte inviati al dispositivo di rete.  
  
```vb  
Dim msg As Byte() = _  
    System.Text.Encoding.ASCII.GetBytes("This is a test.")  
Dim bytesSent As Integer = s.Send(msg)  
  
```  
  
```csharp  
byte[] msg = System.Text.Encoding.ASCII.GetBytes("This is a test");  
int bytesSent = s.Send(msg);  
```  
  
 Il metodo **Send** rimuove i byte dal buffer e li accodata con l'interfaccia di rete al dispositivo di rete.  L'interfaccia di rete non può inviare dati immediatamente, ma la invierà infine, se la connessione viene chiusa in genere con il metodo <xref:System.Net.Sockets.Socket.Shutdown%2A>.  
  
 Per ricevere i dati da un dispositivo di rete, passare un buffer su uno dei metodi di ricezione\- di dati della classe **Socket** \(<xref:System.Net.Sockets.Socket.Receive%2A> e <xref:System.Net.Sockets.Socket.ReceiveFrom%2A>\).  I socket sincroni sospenderanno l'applicazione fino a ricevere i byte dalla rete o fino alla chiusura di socket.  Nell'esempio riceve dati dalla rete e la visualizza nella console.  L'esempio presuppone che i dati provenienti dalla rete sia testo ASCII\- codificato.  Il metodo **Receive** restituisce il numero di byte ricevuti dalla rete.  
  
```vb  
Dim bytes(1024) As Byte  
Dim bytesRec = s.Receive(bytes)  
Console.WriteLine("Echoed text = {0}", _  
    System.Text.Encoding.ASCII.GetString(bytes, 0, bytesRec))  
  
```  
  
```csharp  
byte[] bytes = new byte[1024];  
int bytesRec = s.Receive(bytes);  
Console.WriteLine("Echoed text = {0}",  
    System.Text.Encoding.ASCII.GetString(bytes, 0, bytesRec));  
```  
  
 Quando il socket non è più necessario, è necessario rilasciare chiamando il metodo <xref:System.Net.Sockets.Socket.Shutdown%2A> e chiamando quindi il metodo **Close**.  Nell'esempio rilascia **Socket**.  L'enumerazione <xref:System.Net.Sockets.SocketShutdown> definisce costanti che indicano se il socket deve essere chiuso per inviare, per ricevere, o di entrambi.  
  
```vb  
s.Shutdown(SocketShutdown.Both)  
s.Close()  
```  
  
```csharp  
s.Shutdown(SocketShutdown.Both);  
s.Close();  
```  
  
## Vedere anche  
 [Uso di un socket client asincrono](../../../docs/framework/network-programming/using-an-asynchronous-client-socket.md)   
 [Attesa con socket](../../../docs/framework/network-programming/listening-with-sockets.md)   
 [Esempio di socket client sincrono](../../../docs/framework/network-programming/synchronous-client-socket-example.md)