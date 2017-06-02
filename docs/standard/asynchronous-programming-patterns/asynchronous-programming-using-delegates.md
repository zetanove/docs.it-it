---
title: "Asynchronous Programming Using Delegates | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-standard"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "BeginInvoke method"
  - "asynchronous programming, delegates"
  - "asynchronous delegates"
  - "calling synchronous methods in asynchronous manner"
  - "EndInvoke method"
  - "calling asynchronous methods"
  - "delegates [.NET Framework], asynchronous"
  - "synchronous calling in asynchronous manner"
ms.assetid: 38a345ca-6963-4436-9608-5c9defef9c64
caps.latest.revision: 16
author: "rpetrusha"
ms.author: "ronpet"
manager: "wpickett"
caps.handback.revision: 14
---
# Asynchronous Programming Using Delegates
I delegati consentono di chiamare un metodo sincrono in modo asincrono.  Quando si chiama un delegato in modo sincrono, il metodo `Invoke` chiamerà il metodo di destinazione direttamente sul thread corrente.  Se viene chiamato il metodo `BeginInvoke`, Common Language Runtime accoderà la richiesta e restituirà immediatamente il controllo al chiamante.  Il metodo di destinazione verrà chiamato in modo asincrono in un thread del pool di thread.  Il thread originale, che ha inviato la richiesta, è libero di continuare l'esecuzione in parallelo con il metodo di destinazione.  Se nella chiamata al metodo `BeginInvoke` è stato specificato un metodo di callback, quest'ultimo verrà chiamato al termine del metodo di destinazione.  Nel metodo di callback, il metodo `EndInvoke` ottiene il valore restituito e tutti i parametri di input\/output o solo di output.  Se non viene specificato alcun metodo di callback durante la chiamata a `BeginInvoke`, `EndInvoke` potrà essere chiamato dal thread che ha effettuato la chiamata a `BeginInvoke`.  
  
> [!IMPORTANT]
>  I compilatori devono creare classi delegate con metodi `Invoke`, `BeginInvoke` e `EndInvoke` utilizzando la firma del delegato specificata dall'utente.  I metodi `BeginInvoke` e `EndInvoke` devono essere decorati come nativi.  Poiché tali metodi sono contrassegnati come nativi, Common Language Runtime ne specifica automaticamente l'implementazione durante il caricamento della classe.  Il caricatore garantisce che non ne venga eseguito l'override.  
  
## In questa sezione  
 [Calling Synchronous Methods Asynchronously](../../../docs/standard/asynchronous-programming-patterns/calling-synchronous-methods-asynchronously.md)  
 Viene descritto l'utilizzo di delegati per effettuare chiamate asincrone a metodi comuni e vengono forniti semplici esempi di codice in cui si illustrano i quattro modi disponibili per attendere la restituzione di una chiamata asincrona.  
  
 [Esempio di programmazione di delegati asincroni](../Topic/Asynchronous%20Delegates%20Programming%20Sample.md)  
 Viene illustrato l'utilizzo di delegati per effettuare chiamate asincrone in un esempio di codice più complesso in cui vengono fattorizzati numeri.  
  
## Sezioni correlate  
 [Event\-based Asynchronous Pattern \(EAP\)](../../../docs/standard/asynchronous-programming-patterns/event-based-asynchronous-pattern-eap.md)  
 Viene descritta la programmazione asincrona con .NET Framework.  
  
## Vedere anche  
 <xref:System.Delegate>