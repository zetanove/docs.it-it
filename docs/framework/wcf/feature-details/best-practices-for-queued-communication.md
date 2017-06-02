---
title: "Procedure consigliate per comunicazioni in coda | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "procedure consigliate [WCF], comunicazione in coda"
  - "Code [WCF], procedure ottimali"
ms.assetid: 446a6383-cae3-4338-b193-a33c14a49948
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# Procedure consigliate per comunicazioni in coda
In questo argomento vengono illustrate le procedure consigliate per le comunicazioni in coda in [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].Nelle sezioni seguenti vengono descritte le procedure consigliate in funzione dello scenario.  
  
## Messaggistica in coda di tipo veloce ed efficiente  
 Per scenari che richiedono la separazione fornita dalla messaggistica in coda nonché velocità, elevate prestazioni ed efficienza, utilizzare una coda non transazionale e impostare la proprietà <xref:System.ServiceModel.MsmqBindingBase.ExactlyOnce%2A> su `false`.  
  
 È inoltre possibile scegliere di non incorrere nell'onere delle scritture su disco impostando la proprietà <xref:System.ServiceModel.MsmqBindingBase.Durable%2A> su `false`.  
  
 La protezione ha implicazioni sulle prestazioni.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Considerazioni sulle prestazioni](../../../../docs/framework/wcf/feature-details/performance-considerations.md).  
  
## Messaggistica in coda end\-to\-end affidabile  
 Nelle sezioni seguenti vengono descritte le procedure consigliate per scenari che richiedono messaggistica affidabile end\-to\-end.  
  
### Trasferimento affidabile di base  
 Per l'affidabilità end\-to\-end, impostare la proprietà <xref:System.ServiceModel.MsmqBindingBase.ExactlyOnce%2A> su `true` per garantire il trasferimento.La proprietà <xref:System.ServiceModel.MsmqBindingBase.Durable%2A> può essere impostata su `true` o `false` a seconda delle necessità \(l'impostazione predefinita è `true`\).La proprietà <xref:System.ServiceModel.MsmqBindingBase.Durable%2A> è generalmente impostata su `true` come parte dell'affidabilità end\-to\-end.Ciò implica un costo in termini di prestazioni, ma rende durevole il messaggio. In questo modo il messaggio non andrà perso se il gestore delle code si arresta in modo anomalo.  
  
### Utilizzo delle transazioni  
 È necessario utilizzare transazioni per garantire l'affidabilità end\-to\-end.Le garanzie `ExactlyOnce` assicurano solo che i messaggi vengano recapitati alla coda di destinazione.Per garantire che il messaggio venga ricevuto, utilizzare le transazioni.Se il servizio si arresta in modo anomalo e se si opera senza transazioni, è possibile che si verifichi la perdita del messaggio che sta per essere recapitato, ma che appare come effettivamente recapitato.  
  
### Utilizzo delle code dei messaggi non recapitabili  
 Le code dei messaggi non recapitabili assicurano la ricezione di una notifica se un messaggio non viene recapitato alla coda di destinazione.È possibile utilizzare la coda dei messaggi non recapitabili fornita dal sistema o una personalizzata.È generalmente consigliato l'utilizzo di una coda dei messaggi non recapitabili personalizzata poiché consente di inviare messaggi non recapitabili da una singola applicazione a un'unica coda dei messaggi non recapitabili.In caso contrario, tutti i messaggi non recapitabili che si verificano per tutte le applicazioni in esecuzione nel sistema vengono recapitati a un'unica coda.Ogni applicazione deve quindi cercare nella coda dei messaggi non recapitabili per trovare quelli pertinenti per quell'applicazione.L'utilizzo di una coda dei messaggi non recapitabili personalizzata a volte non è possibile, ad esempio quando si utilizza MSMQ 3.0.  
  
 La disattivazione delle code dei messaggi non recapitabili per la comunicazione affidabile end\-to\-end non è consigliata.  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Utilizzo di code di messaggi non recapitabili per gestire errori di trasferimento dei messaggi](../../../../docs/framework/wcf/feature-details/using-dead-letter-queues-to-handle-message-transfer-failures.md).  
  
### Utilizzo della gestione dei messaggi non elaborabili  
 La gestione dei messaggi non elaborabili consente il ripristino dopo un errore per proseguire l'elaborazione dei messaggi.  
  
 Quando si utilizza la funzionalità di gestione dei messaggi non elaborabili, verificare che la proprietà <xref:System.ServiceModel.MsmqBindingBase.ReceiveErrorHandling%2A> sia impostata sul valore appropriato.L'impostazione della proprietà su <xref:System.ServiceModel.ReceiveErrorHandling> significa che i dati vanno persi.L'impostazione della proprietà su <xref:System.ServiceModel.ReceiveErrorHandling> genera invece errori nell'host del servizio quando viene rilevato un messaggio non elaborabile.Se si utilizza MSMQ 3.0, <xref:System.ServiceModel.ReceiveErrorHandling> è l'opzione migliore per evitare perdite di dati e per spostare il messaggio non elaborabile.Se si utilizza MSMQ 4.0, <xref:System.ServiceModel.ReceiveErrorHandling> è il campo consigliato.Il campo <xref:System.ServiceModel.ReceiveErrorHandling> sposta un messaggio non elaborabile fuori dalla coda consentendo al servizio di proseguire nell'elaborazione di nuovi messaggi.Il servizio dei messaggi non elaborabili è in grado quindi di elaborare separatamente il messaggio non elaborabile.  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Gestione dei messaggi non elaborabili](../../../../docs/framework/wcf/feature-details/poison-message-handling.md).  
  
## Raggiungimento di velocità effettive elevate  
 Per raggiungere velocità effettive elevate in un singolo endpoint, utilizzare gli elementi seguenti:  
  
-   Batch transazionale.Il batch transazionale garantisce la lettura di molti messaggi in una singola transazione.In tal modo vengono ottimizzati i commit della transazione, aumentando le prestazioni complessive.Lo svantaggio del batch consiste nel fatto che se si verifica un errore in un singolo messaggio all'interno di un batch, verrà eseguito il rollback dell'intero batch e i messaggi dovranno essere elaborati uno alla volta fino a che il batch non sarà nuovamente sicuro.Nella maggior parte dei casi i messaggi non elaborabili sono rari, pertanto il batch è il modo preferito per aumentare le prestazioni del sistema, in particolare quando vi sono altri gestori delle risorse che partecipano alla transazione.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Raggruppamento di messaggi in una transazione](../../../../docs/framework/wcf/feature-details/batching-messages-in-a-transaction.md).  
  
-   Concorrenza.La concorrenza aumenta la velocità effettiva, ma può anche provocare conflitti nelle risorse condivise.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Concorrenza](../../../../docs/framework/wcf/samples/concurrency.md).  
  
-   Limitazione.Per ottenere prestazioni ottimali, limitare il numero di messaggi nella pipeline del dispatcher.Per un esempio di come realizzare una limitazione, vedere [Limitazione](../../../../docs/framework/wcf/samples/throttling.md).  
  
 Quando si utilizza il batch, è necessario sapere che la concorrenza e la limitazione danno luogo a batch simultanei.  
  
 Per raggiungere velocità effettive e disponibilità più elevate, utilizzare una farm di servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] in grado di leggere dalla coda.In questo caso, tutti i servizi interessati devono esporre lo stesso contratto nello stesso endpoint.L'approccio della farm funziona in modo ottimale per applicazioni che hanno elevate frequenze di produzione di messaggi poiché consente a un certo numero di servizi di leggere dalla stessa coda.  
  
 Quando si utilizzano le farm, è necessario sapere che le letture transazionali remote non sono supportate in MSMQ 3.0.MSMQ 4.0 supporta le letture transazionali remote.  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Raggruppamento di messaggi in una transazione](../../../../docs/framework/wcf/feature-details/batching-messages-in-a-transaction.md) e [Differenze nelle funzionalità di accodamento in Windows Vista, Windows Server 2003 e Windows XP](../../../../docs/framework/wcf/feature-details/diff-in-queue-in-vista-server-2003-windows-xp.md).  
  
## Accodamento con unità di semantica del lavoro  
 In alcuni scenari i messaggi raggruppati in una coda possono essere correlati insieme e, pertanto, il loro ordine è significativo.In tali scenari, viene elaborato un gruppo di messaggi correlati come singola unità. Ciò significa che tutti i messaggi vengono elaborati correttamente oppure che nessuno di essi viene elaborato.Per implementare tale comportamento, utilizzare sessioni con code.  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)] [Raggruppamento di messaggi in coda in una sessione](../../../../docs/framework/wcf/feature-details/grouping-queued-messages-in-a-session.md).  
  
## Correlazione di messaggi request\/reply  
 Sebbene le code siano tipicamente unidirezionali, in alcuni scenari è necessario determinare una correlazione tra una risposta ricevuta a una richiesta inviata precedentemente.Se tale correlazione viene richiesta, è consigliato applicare al messaggio la propria intestazione del messaggio SOAP contenente informazioni sulla correlazione.In genere, il mittente allega questa intestazione al messaggio e il destinatario, dopo aver elaborato il messaggio e aver risposto con un messaggio nuovo in una coda di risposte, allega l'intestazione del messaggio del mittente contenente le informazioni sulla correlazione così che il mittente possa identificare il messaggio di risposta con il messaggio di richiesta.  
  
## Integrazione con applicazioni non WCF  
 Utilizzare `MsmqIntegrationBinding` in caso di integrazione di servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] o di client con servizi o client non [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].L'applicazione non [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] può essere un'applicazione MSMQ scritta utilizzando System.Messaging, COM\+, [!INCLUDE[vbprvb](../../../../includes/vbprvb-md.md)] o C\+\+.  
  
 Quando si utilizza `MsmqIntegrationBinding`, è necessario sapere che:  
  
-   Il corpo di un messaggio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] non equivale al corpo di un messaggio MSMQ.Quando si invia un messaggio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizzando un'associazione in coda, il corpo del messaggio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] è posizionato all'interno di un messaggio MSMQ.L'infrastruttura MSMQ vede solo il messaggio MSMQ ignorando queste informazioni aggiuntive.  
  
-   `MsmqIntegrationBinding` supporta i tipi di serializzazione più comuni.In base al tipo di serializzazione, il tipo del corpo del messaggio generico, <xref:System.ServiceModel.MsmqIntegration.MsmqMessage%601>, prende parametri di tipo diverso.<xref:System.ServiceModel.MsmqIntegration.MsmqMessageSerializationFormat>, ad esempio, richiede `MsmqMessage\<byte[]>`<xref:System.ServiceModel.MsmqIntegration.MsmqMessageSerializationFormat> e `MsmqMessage<Stream>` richiede .  
  
-   Con la serializzazione XML, è possibile specificare il tipo conosciuto utilizzando l'attributo `KnownTypes` nell'elemento [\<comportamento\>](../../../../docs/framework/configure-apps/file-schema/wcf/behavior-of-servicebehaviors.md) che viene quindi utilizzato per determinare come deserializzare il messaggio XML.  
  
## Vedere anche  
 [Accodamento in WCF](../../../../docs/framework/wcf/feature-details/queuing-in-wcf.md)   
 [Procedura: scambiare messaggi in coda con endpoint WCF](../../../../docs/framework/wcf/feature-details/how-to-exchange-queued-messages-with-wcf-endpoints.md)   
 [Procedura: scambiare messaggi con endpoint WCF e con applicazioni del sistema di accodamento dei messaggi](../../../../docs/framework/wcf/feature-details/how-to-exchange-messages-with-wcf-endpoints-and-message-queuing-applications.md)   
 [Raggruppamento di messaggi in coda in una sessione](../../../../docs/framework/wcf/feature-details/grouping-queued-messages-in-a-session.md)   
 [Raggruppamento di messaggi in una transazione](../../../../docs/framework/wcf/feature-details/batching-messages-in-a-transaction.md)   
 [Utilizzo di code di messaggi non recapitabili per gestire errori di trasferimento dei messaggi](../../../../docs/framework/wcf/feature-details/using-dead-letter-queues-to-handle-message-transfer-failures.md)   
 [Gestione dei messaggi non elaborabili](../../../../docs/framework/wcf/feature-details/poison-message-handling.md)   
 [Differenze nelle funzionalità di accodamento in Windows Vista, Windows Server 2003 e Windows XP](../../../../docs/framework/wcf/feature-details/diff-in-queue-in-vista-server-2003-windows-xp.md)   
 [Protezione dei messaggi mediante protezione del trasporto](../../../../docs/framework/wcf/feature-details/securing-messages-using-transport-security.md)   
 [Protezione dei messaggi mediante protezione a livello di messaggio](../../../../docs/framework/wcf/feature-details/securing-messages-using-message-security.md)   
 [Risoluzione dei problemi relativi ai messaggi in coda](../../../../docs/framework/wcf/feature-details/troubleshooting-queued-messaging.md)