---
title: "Trasporto MSMQ | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3f29a2fe-24df-4614-b64c-b0c084fb7003
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Trasporto MSMQ
In questo argomento vengono elencate tutte le eccezioni generate dal trasporto MSMQ.  
  
## Elenco delle eccezioni  
  
|Codice risorsa|Stringa di risorsa|  
|--------------------|------------------------|  
|MsmqActiveDirectoryRequiresNativeTransfer|La convalida dell'associazione per il messaggio non è riuscita.Il client non è in grado di inviare messaggi.Errore causato da un conflitto nelle proprietà dell'associazione.La proprietà UseActiveDirectory è impostata su True, ma QueueTransferProtocol è impostata su Native.Per risolvere il conflitto, correggere una delle proprietà.|  
|MsmqAuthNoneRequiresProtectionNone|La convalida dell'associazione per il servizio non è riuscita.Impossibile avviare l'endpoint del servizio o il client.Errore causato da un conflitto nelle proprietà dell'associazione.La proprietà MsmqAuthenticationMode è impostata su None, ma MsmqProtectionLevel non è impostata su None.Per risolvere il conflitto, correggere una delle proprietà.|  
|MsmqCustomRequiresPerAddDLQ|La convalida dell'associazione per il messaggio non è riuscita.Il client non è in grado di inviare il messaggio.La proprietà DeadLetterQueue è impostata su Custom, ma la proprietà CustomDeadLetterQueue non è specificata.Specificare l'URI della coda di messaggi non recapitabili per ogni applicazione nella proprietà CustomDeadLetterQueue.|  
|MsmqDeserializationError|Errore durante la deserializzazione del messaggio XML.Impossibile ricevere il messaggio che viene quindi eliminato.|  
|MsmqDLQNotWriteable|La convalida dell'associazione per il client non è riuscita.Il client non è in grado di inviare un messaggio.La coda di messaggi non recapitabili specificata non esiste o non può essere scritta.Verificare che la coda esista con l'autorizzazione necessaria per la scrittura.|  
|MsmqGetPrivateComputerInformationError|Il controllo della versione non è riuscito con l'errore specificato.Impossibile rilevare la versione di MSMQ. Tutte le operazioni sul canale in coda non riusciranno.Verificare che MSMQ sia installato e disponibile.|  
|MsmqNoAssurancesForVolatile|La convalida dell'associazione per il servizio non è riuscita.Impossibile avviare l'endpoint del servizio o il client.La proprietà ExactlyOnce è impostata su True, ma la proprietà Durable è impostata su False.L'operazione non è supportata.Per risolvere il conflitto, correggere una delle proprietà.|  
|MsmqNonTransactionalQueueNeeded|Rilevata una mancata corrispondenza tra l'associazione e la configurazione della coda MSMQ.Impossibile avviare l'endpoint del servizio.La proprietà ExactlyOnce è impostata su False e la coda da cui leggere i messaggi è una coda transazionale.Per risolvere il problema, impostare la proprietà ExactlyOnce su True o creare un'associazione non transazionale.|  
|MsmqOpenError|Errore durante l'apertura della coda specificata.Impossibile inviare o ricevere il messaggio dalla coda.Verificare che MSMQ sia installato e in esecuzione,nonché che la coda sia disponibile all'apertura con l'autorizzazione e la modalità di accesso necessarie.|  
|MsmqPathLookupError|Errore durante la conversione del nome di percorso della coda specificato nel nome di formato.Impossibile completare le operazioni sul canale in coda.Verificare che l'indirizzo della coda sia valido.MSMQ deve essere installato con l'integrazione Active Directory abilitata e l'accesso disponibile.|  
|MsmqPerAppDLQRequiresCustom|La convalida dell'associazione nel client non è riuscita.Il client non è in grado di inviare messaggi.La proprietà CustomDeadLetterQueue è impostata, ma la proprietà DeadLetterQueue non è impostata su Custom.Impostare la proprietà DeadLetterQueue su Custom.|  
|MsmqPerAppDLQRequiresExactlyOnce|La convalida dell'associazione per il client non è riuscita.Il client non è in grado di inviare messaggi.Errore causato da un conflitto nelle proprietà dell'associazione.Per utilizzare la coda di messaggi non recapitabili personalizzata, ExactlyOnce deve essere impostata su True per risolvere il conflitto.|  
|MsmqPerAppDLQRequiresMsmq4|Rilevata una mancata corrispondenza tra l'associazione e la configurazione MSMQ.Il client non è in grado di inviare messaggi.Per utilizzare la coda di messaggi non recapitabili personalizzata, è necessario disporre di MSMQ versione 4.0 o successiva.Se non si dispone di MSMQ versione 4.0 o successiva, impostare la proprietà DeadLetterQueue su System o None.|  
|MsmqReceiveError|Errore durante la ricezione di un messaggio dalla coda.Verificare che MSMQ sia installato e in esecuzionee che la coda sia disponibile per la ricezione.|  
|MsmqSameTransactionExpected|Errore di transazione per la sessione.Il canale di sessione contiene errori.Impossibile inviare o ricevere i messaggi nella sessione.Una sessione in coda non può essere associata a più di una transazione.Verificare che tutti i messaggi nella sessione vengano inviati o ricevuti mediante un'unica transazione.|  
|MsmqSendError|Errore durante l'invio alla coda specificata.Verificare che MSMQ sia installato e in esecuzione.Se si sta effettuando l'invio a una coda locale, verificare che la coda esista con la modalità di accesso e l'autorizzazione necessarie.|  
|MsmqTimeSpanTooLarge|La durata del messaggio è troppo grande.Impossibile inviare il messaggio.La durata \(TTL\) del messaggio non può superare il valore massimo Int32.|  
|MsmqTokenProviderNeededForCertificates|Impossibile trovare un X509SecurityTokenProvider.Impossibile inviare il messaggio.È necessario un provider di token X.509 per la modalità di autenticazione dei certificati.Verificare che per il certificato installato sia disponibile un provider di token di sicurezza.|  
|MsmqTransactedDLQExpected|Mancata corrispondenza tra l'associazione e la configurazione MSMQ.Impossibile inviare i messaggi.La coda di messaggi non recapitabili personalizzata specificata nell'associazione deve essere una coda transazionale.Verificare che l'indirizzo della coda di messaggi non recapitabili personalizzata sia corretto e che la coda sia transazionale.|  
|MsmqTransactionalQueueNeeded|Mancata corrispondenza tra l'associazione e la configurazione della coda MSMQ.Impossibile avviare l'endpoint del servizio.La proprietà ExactlyOnce è impostata su True e la coda da cui leggere i messaggi non è una coda transazionale.Per risolvere il problema, impostare la proprietà ExactlyOnce su False o creare una coda transazionale per questa associazione.|  
|MsmqTransactionCurrentRequired|Non è disponibile alcuna transazione per inviare messaggi nella sessione.È necessario disporre di una transazione per inviare un messaggio in una sessione in coda.Verificare che l'ambito della transazione sia specificato per l'invio del messaggio nella sessione.|  
|MsmqTransactionRequired|Transazione necessaria ma non disponibile.Impossibile inviare o ricevere messaggi.Verificare che l'ambito della transazione sia specificato per l'invio o la ricezione di messaggi.|  
|MsmqUnsupportedSerializationFormat|Si è verificato un errore di deserializzazione.Impossibile ricevere il messaggio che viene quindi eliminato.Il formato di serializzazione specificato non è supportato.|  
|MsmqWrongPrivateQueueSyntax|L'URL non è valido.L'URL per la coda non può contenere il carattere '$'.Utilizzare la sintassi in net.msmq:\/\/machine\/private\/queueName per indirizzare una coda privata.|