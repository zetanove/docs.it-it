---
title: "Miglioramenti apportati alle prestazioni socket nella versione 3.5 | Microsoft Docs"
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
ms.assetid: 225aa5f9-c54b-4620-ab64-5cd100cfd54c
caps.latest.revision: 9
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 9
---
# Miglioramenti apportati alle prestazioni socket nella versione 3.5
La classe <xref:System.Net.Sockets.Socket?displayProperty=fullName> è stata migliorata nella versione 3,5 dalle applicazioni che utilizzano la rete asincrono I\/O per ottenere la restituzione elevato.  Una serie di nuove classi è stata aggiunta come parte di una serie di miglioramenti alla classe <xref:System.Net.Sockets.Socket> che forniscono un modello asincrono alternativo che può essere utilizzato da applicazioni a elevate prestazioni specifiche di socket.  Questi miglioramenti sono specificamente progettati per le applicazioni server di rete che richiedono prestazioni elevate.  Un'applicazione può utilizzare il modello asincrono avanzato separatamente, o solo nei campi caldi di destinazione dell'applicazione \(quando riceve una grande quantità di dati, ad esempio\).  
  
## Miglioramenti della classe  
 Questi miglioramenti hanno lo scopo principale di impedire la sincronizzazione e l'allocazione ripetuta di oggetti durante l'I\/O del socket asincrono con volumi elevati di dati.  Il modello di progettazione fine di inizio\/attualmente implementato dalla classe <xref:System.Net.Sockets.Socket> per il socket asincrono I\/O richiede un oggetto <xref:System.IAsyncResult?displayProperty=fullName> viene allocato per ogni operazione di socket asincrona.  
  
 Nei nuovi miglioramenti della classe <xref:System.Net.Sockets.Socket>, le operazioni di socket asincrone vengono descritti gli oggetti di classi riutilizzabili <xref:System.Net.Sockets.SocketAsyncEventArgs?displayProperty=fullName> allocati e gestiti dall'applicazione.  Le applicazioni socket a elevate prestazioni rilevano meglio la quantità di operazioni socket sovrapposte da sostenere.  L'applicazione è in grado di creare tutti gli oggetti <xref:System.Net.Sockets.SocketAsyncEventArgs> necessari.  Ad esempio, se un'applicazione server deve eseguire accettare sempre un socket 15 operazioni costanti per supportare le frequenze di ingresso di connessione client, è possibile allocare in anticipo 15 oggetti riutilizzabili <xref:System.Net.Sockets.SocketAsyncEventArgs> a tale scopo.  
  
 Il modello di esecuzione di un'operazione socket asincrona con questa classe è costituito dalla procedura seguente:  
  
1.  Allocare un nuovo oggetto di contesto <xref:System.Net.Sockets.SocketAsyncEventArgs> o ottenerne uno libero da un pool di applicazioni.  
  
2.  Impostare le proprietà nell'oggetto di contesto all'operazione da eseguire su \(il metodo delegato e il buffer di dati di callback, ad esempio\).  
  
3.  Chiamare il metodo socket appropriato \(xxxAsync\) per iniziare l'operazione asincrona.  
  
4.  Se il metodo di socket asincrono \(xxxAsync\) restituisce true nel callback, eseguire una query sulle proprietà di contesto dello stato di completamento.  
  
5.  Se il metodo di socket asincrono \(xxxAsync\) restituisce false nel callback, l'operazione è stata completata in modo sincrono.  È possibile eseguire una query sulle proprietà del contesto per il risultato dell'operazione.  
  
6.  Riutilizzare il contesto per un'altra operazione, inserirlo di nuovo nel pool o ignorarlo.  
  
 La durata del nuovo oggetto di contesto asincrono di un'operazione di socket è determinata dai riferimenti nei riferimenti di I\/O asincrono codice dell'applicazione e.  Non è necessario per l'applicazione mantenere un riferimento a un oggetto di contesto dell'operazione socket asincrona dopo l'invio come parametro a uno dei metodi dell'operazione socket asincrona.  Il riferimento verrà mantenuto fino alla restituzione del callback di completamento.  Tuttavia è vantaggioso per l'applicazione mantenere il riferimento all'oggetto di contesto in modo da poter riutilizzare per un'operazione di socket asincrona futura.  
  
## Vedere anche  
 <xref:System.Net.Sockets.Socket?displayProperty=fullName>   
 <xref:System.Net.Sockets.SendPacketsElement?displayProperty=fullName>   
 <xref:System.Net.Sockets.SocketAsyncEventArgs?displayProperty=fullName>   
 <xref:System.Net.Sockets.SocketAsyncOperation?displayProperty=fullName>   
 [Esempi di programmazione di rete](../../../docs/framework/network-programming/network-programming-samples.md)   
 [Esempio di tecnologia di prestazioni di socket](http://go.microsoft.com/fwlink/?LinkID=179570)