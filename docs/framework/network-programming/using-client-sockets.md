---
title: "Uso di socket client | Microsoft Docs"
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
  - "ricezione di dati, socket"
  - "Socket (classe), socket client"
  - "protocolli, socket"
  - "Internet, socket"
  - "socket, socket client"
  - "socket client"
ms.assetid: 81de9f59-8177-4d98-b25d-43fc32a98383
caps.latest.revision: 12
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 10
---
# Uso di socket client
Prima di poter avviare una conversazione con <xref:System.Net.Sockets.Socket>, è necessario creare una pipe di dati tra l'applicazione e il dispositivo remoto.  Sebbene altri gruppi e protocolli degli indirizzi di rete che, in questo esempio viene illustrato come creare una connessione TCP\/IP a un servizio remoto.  
  
 Il protocollo TCP\/IP utilizza un indirizzo di rete e un numero di porta del servizio per identificare in modo univoco un servizio.  L'indirizzo di rete identifica un dispositivo specifico nella rete; il numero di porta identifica il servizio specifico per il dispositivo per connettersi a.  La combinazione di porta del servizio e degli indirizzi di rete viene chiamata un endpoint, rappresentato in .NET Framework dalla classe <xref:System.Net.EndPoint>.  Un discendente **EndPoint** è definito per ogni gruppo di indirizzi supportata; per la famiglia di indirizzo IP, la classe è <xref:System.Net.IPEndPoint>.  
  
 La classe <xref:System.Net.Dns> fornisce servizi di Domain Name alle applicazioni che utilizzano i servizi Internet TCP\/IP.  Il metodo <xref:System.Net.Dns.Resolve%2A> eseguire una query su un server DNS per mappare un nome di dominio descrittivo ad esempio “host.contoso.com„\) a un indirizzo Internet numerico \(ad esempio 192.168.1.1\).  **Resolve** restituisce [IPHostEnty](frlrfsystemnetiphostentryclasstopic) contenente un elenco degli indirizzi e gli alias per il nome richiesto.  Nella maggior parte dei casi, è possibile utilizzare il primo l'indirizzo restituito nella matrice <xref:System.Net.IPHostEntry.AddressList%2A>.  Nel codice riportato <xref:System.Net.IPAddress> contenente l'indirizzo IP di host.contoso.com server.  
  
```vb  
Dim ipHostInfo As IPHostEntry = Dns.Resolve("host.contoso.com")  
Dim ipAddress As IPAddress = ipHostInfo.AddressList(0)  
  
```  
  
```csharp  
IPHostEntry ipHostInfo = Dns.Resolve("host.contoso.com");  
IPAddress ipAddress = ipHostInfo.AddressList[0];  
```  
  
 Internet Assigned Numbers AUTHORITY \(Iana\) definisce i numeri di porta per i servizi comuni \(per ulteriori informazioni, vedere www.iana.org\/assignments\/port\-numbers\).  Altri servizi possono registrare i numeri di porta compreso tra 1.024 e 65.535.  Il seguente codice combina l'indirizzo IP di host.contoso.com con un numero di porta per creare un endpoint remoto per una connessione.  
  
```vb  
Dim ipe As New IPEndPoint(ipAddress, 11000)  
  
```  
  
```csharp  
IPEndPoint ipe = new IPEndPoint(ipAddress,11000);  
```  
  
 Dopo la definizione dell'indirizzo del dispositivo remoto e avere sceltoe una porta da utilizzare per la connessione, l'applicazione può tentare di stabilire una connessione con il dispositivo remoto.  Nell'esempio riportato **IPEndPoint** esistente per connettersi a un dispositivo remoto e intercetti tutte le eccezioni generate.  
  
```vb  
Try  
    s.Connect(ipe)  
Catch ae As ArgumentNullException  
    Console.WriteLine("ArgumentNullException : {0}", _  
        ae.ToString())  
Catch se As SocketException  
    Console.WriteLine("SocketException : {0}", se.ToString())  
Catch e As Exception  
    Console.WriteLine("Unexpected exception : {0}", e.ToString())  
End Try  
  
```  
  
```csharp  
try {  
    s.Connect(ipe);  
} catch(ArgumentNullException ae) {  
    Console.WriteLine("ArgumentNullException : {0}", ae.ToString());  
} catch(SocketException se) {  
    Console.WriteLine("SocketException : {0}", se.ToString());  
} catch(Exception e) {  
    Console.WriteLine("Unexpected exception : {0}", e.ToString());  
}  
```  
  
## Vedere anche  
 [Uso di un socket client sincrono](../../../docs/framework/network-programming/using-a-synchronous-client-socket.md)   
 [Uso di un socket client asincrono](../../../docs/framework/network-programming/using-an-asynchronous-client-socket.md)   
 [Procedura: Creare un socket](../../../docs/framework/network-programming/how-to-create-a-socket.md)   
 [Socket](../../../docs/framework/network-programming/sockets.md)