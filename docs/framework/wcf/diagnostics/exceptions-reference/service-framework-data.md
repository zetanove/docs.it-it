---
title: "Dati Framework del servizio | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 2a2c8ddc-4e82-4e7f-a79f-97085c469517
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Dati Framework del servizio
In questo argomento vengono elencate tutte le eccezioni generate dai dati del servizio Framework.  
  
## Elenco delle eccezioni  
  
|Codice sorgente|Stringa di risorsa|  
|---------------------|------------------------|  
|AddressingExtensionInBadNS|L'elemento specificato nello spazio dei nomi specificato non è valido.Ciò significa che l'elemento specificato è un elemento duplicato o che non è un'estensione valida perché lo spazio dei nomi degli indirizzi non può contenere elementi di estensione.|  
|BinaryEncoderSessionInvalid|La sessione del codificatore binario non è valida perché si è verificato un errore durante la decodifica di un messaggio precedente.|  
|CannotDetectAddressingVersion|Impossibile rilevare la versione di WS\-Addressing.EndpointAddress non si avvia con un elemento.|  
|CouldNotFindNamespaceForPrefix|Il prefisso specificato non ha un'associazione dello spazio dei nomi nell'ambito.|  
|EncoderBadContentType|Impossibile elaborare in contentType.|  
|EncoderEnvelopeVersionMismatch|La versione envelope del messaggio in arrivo specificato non corrisponde al codificatore specificato.Verificare che l'associazione sia configurata con la stessa versione dei messaggi previsti.|  
|EncoderMessageVersionMismatch|La versione del messaggio in uscita specificato non corrisponde al codificatore specificato.Verificare che l'associazione sia configurata con la stessa versione del messaggio.|  
|ExtraContentIsPresentInFaultDetail|Il contenuto di Additional Extensible Markup Language è presente nell'elemento dettagli errore.È consentito un solo elemento.|  
|FilterBadTableType|La IMessageFilterTable creata per un filtro non può essere una MessageFilterTable, né può essere derivata da MessageFilterTable.|  
|FilterTableInvalidForLookup|Lo stato di MessageFilterTable è danneggiato.Impossibile eseguire la ricerca richiesta.|  
|MandatoryHeaderNotUnderstood|Uno o più blocchi di intestazione di Simple Object Access Protocol obbligatori non sono stati compresi.|  
|MessageBodyIsStream|Il corpo del messaggio è un flusso.|  
|MessageBodyIsUnknown|Il formato del corpo del messaggio è sconosciuto.|  
|MessageBodyReaderInvalidReadState|Impossibile utilizzare il ReadState specificato del lettore di corpo del messaggio.|  
|MessageTextEncodingNotSupported|La codifica testo specificata utilizzata nel formato del messaggio di testo non è supportata.|  
|MissingMessageID|Nel messaggio di richiesta manca un'intestazione MessageID.Per correlare una risposta è richiesta un'intestazione MessageID.|  
|MultipleMessageHeaders|È stata trovata più di un'intestazione con il nome e lo spazio dei nomi specificati.|  
|MultipleMessageHeadersWithActor|È stata trovata più di un'intestazione con il nome, lo spazio dei nomi e il ruolo specificati.|  
|MultipleRelatesToHeaders|È stata trovata più di un'intestazione RelatesTo con la relazione specificata.Ne è consentita solo una per ogni relazione.|  
|QueryFunctionTypeNotSupported|Il tipo restituito specificato per IXsltContextFunction non è supportato.|  
|QueryIteratorOutOfScope|XPathNodeIterator è stato invalidato.Gli XPathNodeIterator passati come argomenti alle funzioni IXsltContextFunction sono validi solo all'interno della funzione.Non possono essere memorizzati nella cache per essere utilizzati in seguito o per essere restituiti dalla funzione.|  
|QueryVariableNull|I metodi IXsltContextVariable non possono restituire null.|  
|QueryVariableTypeNotSupported|Il tipo derivato IXsltContextVariable specificato non è supportato.|  
|ReceiveShutdownReturnedMessage|Il canale ha ricevuto un messaggio di input imprevisto con l'azione specificata durante la chiusura.Chiudere il canale quando non si attendono altri messaggi di input.|  
|XmlBufferInInvalidState|Si è verificato un errore interno.Impossibile eseguire l'operazione a causa dello stato del buffer XML.|  
|XmlBufferQuotaExceeded|Le dimensioni necessarie per memorizzare nel buffer il contenuto di Extensible Markup Language content hanno superato la quota di buffer.|