---
title: "Elenco delle attivit&#224; | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5540e185-ce8e-4db3-83b0-2b9f5bf71829
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Elenco delle attivit&#224;
In questo argomento sono elencate tutte le attività definite in [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)].  
  
> [!NOTE]
>  È inoltre possibile definire attività a livello di programmazione allo scopo di raggruppare più tracce utente.Per ulteriori informazioni, vedere [Creazione di tracce di codice utente](../../../../../docs/framework/wcf/diagnostics/tracing/emitting-user-code-traces.md).  
  
## Attività ServiceModel  
 Nella tabella seguente sono elencate tutte le attività relative ai principali scenari di utilizzo.  
  
|Etichetta|Nome attività|Tipo attività|Descrizione|  
|---------------|-------------------|-------------------|-----------------|  
|A, M|Attività di ambiente|N\/D \(non controllata da ServiceModel\)|Attività il cui ID viene impostato in TLS prima che venga effettuata qualsiasi chiamata al codice di ServiceModel, sia esso lato client o lato server.<br /><br /> Esempio: un'attività in cui viene chiamata l'attività di apertura del client [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] oppure dove viene chiamata l'attività serviceHost.open.|  
|B|Construct<br /><br /> ChannelFactory.ContractType : "\[tipo\]".|Construct||  
|C|Aprire<br /><br /> \[ClientBase&#124;ChannelFactory\].ContractType : "\[tipo\]".|Aprire||  
|I|Chiusura \[ClientBase&#124;ChannelFactory\].ContractType : "\[tipo\]".|Close||  
|M|Costruzione ServiceHost.ServiceType: "\[tipo\]".|Construct||  
|N|Apertura di ServiceHost.ServiceType: "\[tipo\]".|Aprire||  
|Z|Chiusura di ServiceHost.ServiceType: "\[tipo\]".|Close||  
|O|Attesa su "\[indirizzo\]".|ListenAt|Questa attività, così come la prossima, sono specifiche del trasporto.L'attività di tipo ListenAt rappresenta il contenuto che corrisponde all'indirizzo su cui il listener del canale è in attesa.Nel caso di MSMQ ciò corrisponde alla coda stessa, in quanto alla coda è associato un unico indirizzo.Nel caso di trasporti orientati alla connessione, questa attività resta in attesa di connessioni in ingresso. Nel caso di MSMQ, invece, questa attività resta in attesa di messaggi MSMQ.Infine, questa attività viene creata durante l'attività ServiceHost.Open \(\) e contiene le tracce riferite alla creazione e all'eliminazione del listener nonché al trasferimento dell'esecuzione a tutte le attività di tipo ReceiveBytes.|  
|P|Ricezione byte sulla connessione "\[indirizzo\]".Ricezione messaggio MSMQ.|ReceiveBytes|In questa attività vengono elaborati i dati che sono destinati a ottenere un messaggio di [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)].Nel caso di trasporto orientato alla connessione o del protocollo HTTP, il sistema attende i byte in ingresso.Nel caso del protocollo TCP\/pipe con nome, la durata di questa attività corrisponde alla durata della connessione, in quanto il momento di creazione dell'attività coincide con quello di creazione della connessione.Nel caso del protocollo HTTP, la durata di questa attività corrisponde a quella di una richiesta di messaggio e viene considerata a partire dal momento in cui il messaggio viene inviato.Questa attività, se applicabile, contiene le tracce riferite alla creazione e all'eliminazione della connessione nonché al trasferimento dell'esecuzione a tutte le attività di elaborazione di messaggi \(ovvero di oggetti\).<br /><br /> Nel caso di MSMQ, questa attività corrisponde a quella da cui viene recuperato il messaggio MSMQ.|  
|Q|Elaborazione messaggio \[numero\].Nota: il parametro \[numero\] è un valore monotonicamente crescente inizialmente pari a 1.|ProcessMessage|Questa attività prevede l'elaborazione di un messaggio in ingressoe viene avviata quando tutti i dati \(byte e messaggio MSMQ\) vengono ricevuti per formare un oggetto di messaggio [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)].Le tracce contenute in questa attività riguardano l'elaborazione delle intestazioni.<br /><br /> Dopo aver formato un messaggio che può essere inviato e dopo aver ricercato l'ID attività corrispondente, il sistema passa all'attività ServiceHost ProcessAction.|  
|D, S|Elaborazione azione "\[azione\]".|ProcessAction|Questa attività prevede l'elaborazione del messaggio attraverso lo stack Trasporto\/Sicurezza\/RM per inviare il messaggio al codice utente al momento della ricezione e restituire il messaggio sul percorso inverso al momento dell'invio.<br /><br /> Nel server, questa attività utilizza l'ID di attività propagato se quest'ultimo viene inviato nell'intestazione del messaggio tramite l'attività "Propagazione di attività". In caso contrario, viene creato un nuovo GUID.<br /><br /> In questa attività viene inoltre elaborato il messaggio di risposta dei contratti di Request\/Reply.|  
|T|Esecuzione "\[IContratto.Operazione\]".|ExecuteUserCode|Questa attività prevede l'esecuzione del codice utente dopo l'invio al lato servere rappresenta una linea di delimitazione fra il codice ServiceHost e il codice fornito dall'utente.|  
  
## Attività di sicurezza  
 Nella tabella seguente sono elencate tutte le attività riferite alla sicurezza.  
  
|Nome attività|Tipo attività|Descrizione|  
|-------------------|-------------------|-----------------|  
|Impostazione sessione protetta|SetupSecurity|Esiste soltanto sul lato client.Contiene tutti gli scambi RST\*\/SCT per eseguire l'autenticazione e l'impostazione del contesto di sicurezza.Se l'elemento `propagateActivity` è impostato su `true`, questa attività viene unita alle attività RST\*\/SCT corrispondenti di tipo ProcessAction appartenenti al servizio.|  
|Chiusura sessione protetta|SetupSecurity|Esiste sul lato client.Contiene lo scambio di messaggi di annullamento per eseguire la chiusura della sessione protetta.Se l'elemento `propagateActivity` è impostato su `true`, questa attività viene unita all'attività di annullamento di tipo ProcessAction del servizio.|  
  
 Nella tabella seguente sono elencate tutte le attività riferite a COM\+.  
  
|Nome attività|Tipo attività|Descrizione|  
|-------------------|-------------------|-----------------|  
|Creazione istanza COM\+|TransferToCOMPlus|È possibile creare una sola istanza di attività per ogni chiamata COM\+ tramite codice [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)]|  
|Esecuzione \<operazione\> COM\+|TransferToCOMPlus|È possibile creare una sola istanza di attività per ogni chiamata COM\+ tramite codice [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)]|  
  
## Attività WMI  
 Nella tabella seguente sono elencate tutte le attività riferite a WMI.  
  
|Nome attività|Tipo attività|Descrizione|  
|-------------------|-------------------|-----------------|  
|Ottenimento WMI|WMIGetObject|Questa attività prevede il recupero di dati da WMI da parte dell'utente.|  
|Inserimento WMI|WmiPutInstance|Questa attività prevede l'aggiornamento dei dati tramite WMI da parte dell'utente|