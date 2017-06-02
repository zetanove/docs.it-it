---
title: "Comunicazioni principali: framework di connessione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 61ee00e1-896d-47c8-942f-1db28ac89cdc
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Comunicazioni principali: framework di connessione
In questo argomento vengono elencate tutte le eccezioni generate dal framework di connessione di [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)].  
  
## Elenco delle eccezioni  
  
|Codice sorgente|Stringa di risorsa|  
|---------------------|------------------------|  
|CloseTimedOut|Si è verificato il timeout del metodo Close.Aumentare il valore di timeout passato al metodo Close o aumentare il valore CloseTimeout dell'associazione.È possibile che la durata consentita per l'operazione fosse un intervallo parziale di un timeout più lungo.|  
|ContentTypeMismatch|Il tipo di contenuto specificato che è stato inviato al servizio non corrisponde al tipo che quest'ultimo prevede di ricevere.È possibile che le associazioni di client e servizio non corrispondano fra loro.|  
|DuplexChannelAbortedDuringOpen|Il canale duplex per l'elemento specificato è stato interrotto durante il processo di apertura.|  
|FramingValueNotAvailable|Non è possibile accedere al valore in quanto quest'ultimo non è stato decodificato in modo completo.|  
|OperationAbortedDuringConnectionEstablishment|L'operazione è stata interrotta durante il tentativo di connessione all'elemento specificato.|  
|ReceiveTimedOut2|Si è verificato il timeout dell'operazione di ricezione.È possibile che la durata consentita per l'operazione fosse un intervallo parziale di un timeout più lungo.|  
|SendCannotBeCalledAfterCloseOutputSession|Non è possibile inviare messaggi su un canale dopo aver chiamato il metodo CloseOutputSession.|