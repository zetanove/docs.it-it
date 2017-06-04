---
title: "Procedure consigliate per le sessioni affidabili | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b94f6e01-8070-40b6-aac7-a2cb7b4cb4f2
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Procedure consigliate per le sessioni affidabili
Questa sezione illustra le procedure consigliate per le sessioni affidabili.  
  
## Impostazione di MaxTransferWindowSize  
 Le sessioni affidabili in [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] usano una finestra di trasferimento per contenere i messaggi nel client e nel servizio.  La proprietà configurabile <xref:System.ServiceModel.Channels.ReliableSessionBindingElement.MaxTransferWindowSize%2A> indica quanti messaggi può contenere la finestra di trasferimento.  
  
 Sul lato mittente, questo indica quanti messaggi può contenere la finestra di trasferimento mentre attende gli acknowledgement; sul lato destinatario, indica invece quanti messaggi memorizzare nel buffer del servizio.  
  
 La scelta della dimensione giusta incide sull'efficienza operativa della rete e sulla capacità ottimale di esecuzione del servizio.  Nelle sezioni seguenti viene illustrato in dettaglio cosa considerare quando si sceglie un valore per questa proprietà e viene descritto l'impatto del valore scelto.  
  
 La dimensione predefinita della finestra di trasferimento è di 8 messaggi.  
  
### Uso efficiente della rete  
 Il termine *rete* corrisponde qui a tutto ciò che esiste tra un client \(mittente\) e un servizio \(destinatario\) usati come base della comunicazione.  Sono inclusi le connessioni di trasporto e tutti gli intermediari o bridge tra di esse, tra cui i router SOAP o i proxy\/firewall HTTP.  
  
 L'uso efficiente della rete assicura che la capacità della rete sia pienamente usata.  Sia la quantità dei dati trasferibili al secondo sulla rete \(denominata *velocità dati*\) che il tempo necessario per il trasferimento dei dati dal mittente al destinatario \(denominato *latenza*\) incidono sull'efficienza dell'uso della rete.  
  
 Sul lato mittente, la proprietà <xref:System.ServiceModel.Channels.ReliableSessionBindingElement.MaxTransferWindowSize%2A> indica quanti messaggi può contenere la finestra di trasferimento durante l'attesa di acknowledgement.  Così, se la latenza della rete è elevata, per assicurare un mittente capace di rispondere velocemente e un efficace uso della rete, è necessario aumentare la dimensione della finestra di trasferimento.  
  
 Ad esempio, anche se il mittente riesce a stare al passo con la velocità dati, è consigliabile che la latenza sia alta se sono presenti diversi intermediari tra il mittente e il destinatario o se uno degli intermediari o la rete è di tipo dissipativo.  Il mittente deve quindi attendere acknowledgement dei messaggi presenti nella finestra di trasferimento prima di accettare nuovi messaggi da inviare in rete.  Più piccolo è il buffer con latenza elevata, meno efficace sarà l'uso della rete.  D'altro canto, una finestra di trasferimento di dimensioni eccessive può incidere negativamente sul servizio, costretto a gestire l'elevata velocità di invio dal client.  
  
### Esecuzione del servizio alla capacità ottimale  
 Nella misura in cui la rete viene usata in modo efficiente, l'ideale sarebbe eseguire il servizio alla capacità ottimale.  La proprietà della dimensione della finestra di trasferimento indica quanti messaggi il destinatario può memorizzare nel buffer.  La memorizzazione dei messaggi nel buffer non solo agevola il controllo del flusso di rete ma consente anche l'esecuzione del servizio alla capacità completa.  Ad esempio, se il buffer è 1 e i messaggi arrivano più velocemente di quanto il servizio possa elaborarli, la rete può perdere messaggi e la capacità della rete può essere sprecata o sottoutilizzata.  
  
 L'uso di un buffer aumenta la disponibilità del servizio, che contemporaneamente riceve un messaggio e lo memorizza nel buffer, mentre elabora i messaggi precedentemente ricevuti.  
  
 È consigliabile usare la stessa proprietà `MaxTransferWindowSize` sul mittente e sul destinatario.  
  
### Attivazione del controllo del flusso  
 Il controllo del flusso è un meccanismo che assicura che il mittente e il destinatario stiano reciprocamente al passo, ovvero che i messaggi vengano usati ed elaborati non appena vengono prodotti.  La dimensione della finestra di trasferimento sul client e sul servizio assicura che tra il mittente e il destinatario ci sia un intervallo di sincronizzazione accettabile.  
  
 È consigliabile impostare la proprietà <xref:System.ServiceModel.Channels.ReliableSessionBindingElement.FlowControlEnabled%2A> su true, quando si usa una sessione affidabile tra un client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] e un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
## Impostazione di MaxPendingChannels  
 Quando si scrive un servizio che attiva la comunicazione tramite sessione affidabile da client diversi, è possibile che molti client stabiliscano contemporaneamente una sessione affidabile per il servizio.  La risposta del servizio in queste situazioni dipende dalla proprietà `MaxPendingChannels`.  
  
 Quando il mittente crea un canale di sessione affidabile per un destinatario, un handshake tra di loro stabilisce una sessione affidabile.  Dopo la creazione della sessione affidabile, il canale viene inserito in una coda di canali in sospeso per l'accettazione da parte del servizio.  La proprietà `MaxPendingChannels` indica quanti canali possono trovarsi in questo stato.  
  
 È possibile che il servizio sia in uno stato che non consente di accettare altri canali.  Se la coda è piena, i tentativi di stabilire sessioni affidabili vengono rifiutati e il client deve ritentare l'operazione.  
  
 È inoltre possibile che i canali in sospeso presenti nella coda vi restino per un periodo di tempo più lungo.  Nel frattempo è possibile che intervenga un timeout di inattività a causare il passaggio del canale a uno stato di errore.  
  
 Pertanto, quando si scrive un servizio destinato contemporaneamente a più client, è consigliabile impostare un valore adatto alle proprie esigenze.  L'impostazione di un valore troppo alto per `MaxPendingChannels` inciderà negativamente sul working set.  
  
 Il valore predefinito di <xref:System.ServiceModel.Channels.ReliableSessionBindingElement.MaxPendingChannels%2A> è 4.  
  
## Sessioni affidabili e hosting  
 Quando si ospita sul Web un servizio che usa sessioni affidabili, è necessario tenere a mente le importanti considerazioni seguenti:  
  
-   Le sessioni affidabili hanno uno stato, che viene conservato nel dominio dell'applicazione.  Questo significa che tutti i messaggi di una sessione affidabile devono essere elaborati nello stesso dominio dell'applicazione.  Le Web farm e i Web garden in cui la dimensione della farm o del garden è \> 1 non possono rispettare questo vincolo.  
  
-   Le sessioni affidabili che usano canali HTTP duali \(usano ad esempio `WsDualHttpBinding`\) possono richiedere più di 2 connessioni HTTP predefinite per client.  Una sessione affidabile duplex può quindi richiedere fino a 2 connessioni per ogni direzione, poiché messaggi di applicazione e di protocollo simultanei possono essere in trasferimento su ciascuna direzione in un determinato momento.  Questo significa che, a determinate condizioni, in base al modello di scambio dei messaggi del servizio, è possibile creare un deadlock di un servizio ospitato sul Web usando il doppio canale HTTP e le sessioni affidabili.  Per aumentare il numero di connessioni HTTP consentite per client, aggiungere quanto segue al file di configurazione pertinente, ad esempio, il file web.config del servizio in questione:  
  
```  
<configuration>  
   <system.net>  
      <connectionManagement>  
         <add name = "*" maxconnection = "XX" />  
      </connectionManagement>  
   </system.net>  
</configuration>  
```  
  
 In cui "XX" è il numero di connessioni necessarie.  Il minimo in questo caso dovrebbe essere 4.