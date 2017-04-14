---
title: "Procedura: Creare un socket | Microsoft Docs"
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
  - "Servizi di rete"
  - "invio di dati, socket"
  - "richieste dati, socket"
  - "richiesta di dati da Internet, socket"
  - "Socket (classe), creazione di socket"
  - "Risorse di rete"
  - "ricezione di dati, socket"
  - "protocolli, socket"
  - "Internet, socket"
  - "socket, creazione"
ms.assetid: c64a049c-5981-43bc-a2dc-1851473589c7
caps.latest.revision: 7
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 7
---
# Procedura: Creare un socket
Prima di poter utilizzare un socket per comunicare con i dispositivi remoti, il socket deve essere inizializzato con informazioni sull'indirizzo di rete e di protocollo.  Il costruttore per la classe <xref:System.Net.Sockets.Socket> dispone di parametri che specificano la famiglia di indirizzi, il tipo di socket e il tipo del protocollo di socket utilizza per impostare connessioni.  
  
## Esempio  
 Nell'esempio seguente viene creato un socket che può essere utilizzato per comunicare in una rete di TCP\/IP\-based, ad esempio Internet.  
  
```csharp  
Socket s = new Socket(AddressFamily.InterNetwork,   
   SocketType.Stream, ProtocolType.Tcp);  
```  
  
```vb  
Dim s as New Socket(AddressFamily.InterNetwork, _  
   SocketType.Stream, ProtocolType.Tcp)  
  
```  
  
 Per utilizzare UDP anziché TCP, modificare il tipo di protocollo, come nel seguente esempio:  
  
```csharp  
Socket s = new Socket(AddressFamily.InterNetwork,   
   SocketType.Dgram, ProtocolType.Udp);  
```  
  
```vb  
Dim s as New Socket(AddressFamily.InterNetwork, _  
   SocketType.Dgram, ProtocolType.Udp)  
  
```  
  
 L'enumerazione <xref:System.Net.Sockets.AddressFamily> specifica i gruppi degli indirizzi standard utilizzati dalla classe **Socket** per risolvere gli indirizzi di rete \(ad esempio, il membro **AddressFamily.InterNetwork** specifica la famiglia degli indirizzi della versione 4 di IP\).  
  
 L'enumerazione <xref:System.Net.Sockets.SocketType> specifica il tipo di socket, ad esempio il membro **SocketType.Stream** indica un socket standard per l'invio e la ricezione di dati con controllo del flusso\).  
  
 L'enumerazione <xref:System.Net.Sockets.ProtocolType> specificare il protocollo di rete da utilizzare per la comunicazione in **Socket**, ad esempio **ProtocolType.Tcp** indica che utilizza il socket TCP, **ProtocolType.Udp** indica che il socket utilizza UDP\).  
  
 Dopo **Socket** viene creato, può iniziare una connessione a un endpoint remoto o ricevere le connessioni dai dispositivi remoti.  
  
## Vedere anche  
 [Uso di socket client](../../../docs/framework/network-programming/using-client-sockets.md)   
 [Attesa con socket](../../../docs/framework/network-programming/listening-with-sockets.md)