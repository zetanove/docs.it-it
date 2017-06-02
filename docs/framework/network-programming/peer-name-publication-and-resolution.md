---
title: "Pubblicazione e risoluzione di nomi di peer | Microsoft Docs"
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
ms.assetid: f0370e08-9fa6-4ee5-ab78-9a58a20a7da2
caps.latest.revision: 5
author: "mcleblanc"
ms.author: "markl"
manager: "markl"
caps.handback.revision: 5
---
# Pubblicazione e risoluzione di nomi di peer
## Pubblicare un nome peer  
 Per pubblicare un nuovo PNRP ID, un peer esegue le operazioni seguenti:  
  
-   Invia i messaggi della pubblicazione di PNRP agli elementi della cache \(i peer registrata PNRP ID del livello più basso della cache\) per inizializzare la cache.  
  
-   Selezionare i nodi casuali in cloud che non sono gli elementi adiacenti e li invia richieste di risoluzione dei nomi di PNRP per la propria ID P2P  Il processo risultante di determinazione dell'endpoint definisce le cache dei nodi casuali in cloud con il PNRP ID del peer di pubblicazione.  
  
 I nodi della versione 2 di PNRP non pubblicano PNRP ID se stanno risolvendo solo altro P2P ID.  La chiave HKEY\_LOCAL\_MACHINE \\ SOFTWARE \\ Microsoft \\ Windows NT \\ valore del Registro di sistema PNRP \\ IPV6\-Global \\ SearchOnly\=1 \(tipo PeerNet \\ CurrentVersion \\\) REG\_DWORD che specifica i peer utilizzano solo PNRP per la risoluzione dei nomi, mai per la pubblicazione di nome.  Questo valore del Registro di sistema può inoltre essere configurato con criteri di gruppo.  
  
## Risolvere un nome peer  
 L'individuazione degli altri membri in una rete o in un cloud di PNRP è un processo composto da due fasi:  
  
1.  Determinazione dell'endpoint  
  
2.  Risoluzione di PNRP ID  
  
 In fase di determinazione dell'endpoint, un peer che sta tentando di risolvere il PNRP ID di un servizio in un altro computer determina l'indirizzo IPv6 del peer remoto.  Il peer remoto è quello che ha pubblicato, o è associato a, il PNRP ID del computer o servizio.  
  
 Dopo la conferma dell'endpoint remoto è stato registrato in cloud di PNRP, il peer di richiesta in fase di risoluzione di PNRP ID invia una richiesta all'endpoint peer per il PNRP ID del servizio desiderato.  Endpoint invia una risposta che conferma il PNRP ID del servizio, un commento e di un massimo di 4 KB di informazioni aggiuntive che il peer di richiesta può utilizzare per la comunicazione futura.  Ad esempio, se il punto finale desiderato è un server di gioco, i dati aggiuntivi peer del record dei nomi possono contenere informazioni sul gioco, di gioco e il numero di giocatori corrente.  
  
 In fase di determinazione dell'endpoint, PNRP utilizza un processo iterativo per il posizionamento di nodo che ha pubblicato il PNRP ID, in cui il nodo che esegue la risoluzione è responsabile del contatto dei nodi in avanti più vicino all'identificazione di destinazione PNRP  
  
 Per eseguire la risoluzione dei nomi in PNRP, il peer esamina le voci nel proprio cache per una voce che corrisponde all'ID del database di destinazione PNRP  Se viene trovato, il peer invia un messaggio di richiesta di PNRP al peer e attende una risposta.  Se una voce per il PNRP ID non viene trovata, il peer invia un messaggio di richiesta di PNRP al peer corrispondente alla voce con un PNRP ID che corrisponde maggiormente l'identificazione di destinazione PNRP  Il nodo che riceve il messaggio di richiesta di PNRP esamina il proprio cache ed esegue le operazioni seguenti:  
  
-   Se il PNRP ID viene trovato, le risposte richieste del peer di endpoint direttamente al peer di richiesta.  
  
-   Se il PNRP ID non viene trovato e un PNRP ID nella cache è più vicino al database di destinazione PNRP ID, il peer necessario invia una risposta al peer di richiesta che contiene l'indirizzo IPv6 del peer che rappresenta la voce con un PNRP ID che corrisponde maggiormente all'ID del database di destinazione PNRP  Utilizzando l'indirizzo IP nella risposta, il nodo richiedente invia un altro messaggio di richiesta di PNRP all'indirizzo IPv6 per rispondere o esaminarne la cache.  
  
-   Se il PNRP ID non viene trovato e non esistono PNRP ID nella cache che è più vicino al database di destinazione PNRP ID, il peer necessario invia il peer di richiesta una risposta che indica la condizione.  Il peer di richiesta quindi l'id di PNRP seguente\- più vicina  
  
 Il peer di richiesta continua il processo con le iterazioni successive, eventualmente posizionanti il nodo che ha registrato l'id di PNRP  
  
 In lo spazio dei nomi <xref:System.Net.PeerToPeer>, esiste una relazione molti\-a\-molti tra i record <xref:System.Net.PeerToPeer.PeerName> contenenti gli endpoint e cloud o mesh di PNRP in cui comunicano.  Quando sono presenti voci duplicate o non aggiornate, o più nodi con lo stesso nome peer, i nodi di PNRP possono ottenere le informazioni correnti utilizzando la classe <xref:System.Net.PeerToPeer.PeerNameResolver>.  I metodi <xref:System.Net.PeerToPeer.PeerNameResolver> utilizzano un singolo nome peer per semplificare la prospettiva record peer di un apeer a molti nome e lo stesso un peer a molti cloud.  È simile a una query eseguito utilizzando un join di relazionale\- tabella.  Al termine, l'oggetto resolver restituisce <xref:System.Net.PeerToPeer.PeerNameRecordCollection> per il peer nome specificato.  Ad esempio, un nome peer si presenterebbe in tutti i record peer del nome della raccolta, ordinata da cloud.  Queste sono le istanze del nome peer dei dati che possono essere necessari a l da un'applicazione basata PNRP.  
  
## Vedere anche  
 <xref:System.Net.PeerToPeer>