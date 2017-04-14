---
title: "Attesa con socket | Microsoft Docs"
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
  - "socket, attesa"
  - "richieste dati, socket"
  - "richiesta di dati da Internet, socket"
  - "ricezione di dati, socket"
  - "protocolli, socket"
  - "attesa con socket"
  - "Internet, socket"
ms.assetid: 40e426cc-13db-4371-95eb-f7388bd23ebf
caps.latest.revision: 10
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 10
---
# Attesa con socket
Il listener o sockets del server apre una porta in rete e quindi attende un client per connettersi alla porta.  Sebbene altri gruppi e protocolli degli indirizzi di rete che, in questo esempio viene illustrato come creare servizio remoto per una rete TCP\/IP.  
  
 L'indirizzo univoco di un servizio TCP\/IP è definito combinando l'indirizzo IP dell'host con il numero di porta del servizio per creare un endpoint per il servizio.  La classe <xref:System.Net.Dns> fornisce metodi che restituiscono informazioni sugli indirizzi di rete è supportato dal dispositivo di rete locale.  Quando il dispositivo di rete locale ha più di un indirizzo di rete, o se il sistema supporti locali più di un dispositivo di rete, la classe **Dns** restituisce informazioni su tutti gli indirizzi di rete e l'applicazione deve specificare l'indirizzo corretto per il servizio.  Internet Assigned Numbers AUTHORITY \(Iana\) definisce i numeri di porta per i servizi comuni \(per ulteriori informazioni, vedere www.iana.org\/assignments\/port\-numbers\).  Altri servizi possono registrare i numeri di porta compreso tra 1.024 e 65.535.  
  
 Nell'esempio riportato <xref:System.Net.IPEndPoint> per un server combinando il primo indirizzo IP restituito da **Dns** per il computer host con un numero di porta scelto da numeri di porta registrazione varia.  
  
```vb  
Dim ipHostInfo As IPHostEntry = Dns.Resolve(Dns.GetHostName())  
Dim ipAddress As IPAddress = ipHostInfo.AddressList(0)  
Dim localEndPoint As New IPEndPoint(ipAddress, 11000)  
  
```  
  
```csharp  
IPHostEntry ipHostInfo = Dns.Resolve(Dns.GetHostName());  
IPAddress ipAddress = ipHostInfo.AddressList[0];  
IPEndPoint localEndPoint = new IPEndPoint(ipAddress, 11000);  
```  
  
 Al termine dell'endpoint locale è determinato, <xref:System.Net.Sockets.Socket> deve essere associato a quel punto utilizzando il metodo e del set <xref:System.Net.Sockets.Socket.Bind%2A> di ascolto sull'endpoint tramite il metodo <xref:System.Net.Sockets.Socket.Listen%2A>.  **Bind** genera un'eccezione se la combinazione della porta e address specifico è già in uso.  Nell'esempio seguente viene illustrata l'associazione **Socket** con **IPEndPoint**.  
  
```vb  
listener.Bind(localEndPoint)  
listener.Listen(100)  
```  
  
```csharp  
listener.Bind(localEndPoint);  
listener.Listen(100);  
```  
  
 Il metodo **Listen** accetta un singolo parametro che specifica il numero di connessioni in corso a **Socket** sono consentite prima che un errore occupato server venga restituito al client connesso.  In questo caso, fino a 100 client sono contenuti nella coda di connessione prima che la risposta occupata server venga restituita al client numero 101.  
  
## Vedere anche  
 [Uso di un socket server sincrono](../../../docs/framework/network-programming/using-a-synchronous-server-socket.md)   
 [Uso di un socket server asincrono](../../../docs/framework/network-programming/using-an-asynchronous-server-socket.md)   
 [Uso di socket client](../../../docs/framework/network-programming/using-client-sockets.md)   
 [Procedura: Creare un socket](../../../docs/framework/network-programming/how-to-create-a-socket.md)   
 [Socket](../../../docs/framework/network-programming/sockets.md)