---
title: "Reliable Secure Profile | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 921edc41-e91b-40f9-bde9-b6148b633e61
caps.latest.revision: 8
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 8
---
# Reliable Secure Profile
In questo esempio viene descritto come creare [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] e [Reliable Secure Profile](http://go.microsoft.com/fwlink/?LinkId=178140) \(RSP\).In questo esempio viene descritta l'implementazione di un canale [Crea connessione](http://go.microsoft.com/fwlink/?LinkId=178141), che può essere creato insieme a messaggi affidabili ed eventualmente a un canale sicuro per creare un'associazione sicura affidabile basata sulla specifica RSP.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Extensibility\Channels\ReliableSecureProfile`  
  
## Discussione  
 In questo esempio viene descritto uno scenario di scambio di messaggi bidirezionale asincrono affidabile.Il servizio dispone di un contratto duplex e il client implementa il contratto di callback duplex.Il client avvia una richiesta a un servizio per il quale è attesa una risposta in una connessione separata.Il messaggio di richiesta viene inviato in modo affidabile.Il client non desidera aprire un endpoint di ascolto in corrispondenza del punto finale.Pertanto, esegue il polling del servizio con richieste "Crea connessione" affinché il servizio restituisca la risposta nel canale di supporto di tale richiesta "Crea connessione".In questo esempio viene descritto come disporre di una comunicazione duplex affidabile sicura su HTTP senza che il client esponga un endpoint di ascolto \(e creando un'eccezione del firewall\).  
  
## Per impostare, compilare ed eseguire l'esempio  
  
1.  Aprire la soluzione **ReliableSecureProfile**.  
  
2.  Fare clic con il pulsante destro del mouse sul progetto **Service** in **Esplora soluzioni**, selezionare **Debug**, **Avvia nuova istanza** nel menu di scelta rapida.In questo modo, viene avviato l'host del servizio.  
  
3.  Fare clic con il pulsante destro del mouse sul progetto **Client** in **Esplora soluzioni**, selezionare **Debug**, **Avvia nuova istanza** nel menu di scelta rapida.In questo modo, il client viene avviato.  
  
4.  Digitare qualsiasi stringa nel messaggio di richiesta nella finestra della console client e fare clic su INVIO. In questo modo, la stringa di input viene inviata al servizio, che calcola un hash di tale stringa.  
  
5.  Visualizzare il risultato nelle finestre del client quando il servizio richiama l'operazione del contratto di callback duplex per visualizzare il risultato nella finestra della console client.Nel servizio si verifica un ritardo intenzionale per simulare il completamento di un'operazione lunga di elaborazione dei dati.  
  
6.  Il monitoraggio del traffico HTTP \(da parte di strumenti per il monitoraggio della rete online quali Network Monitor, Fiddler e così via\) mostra che tra il client e il servizio viene creata una sequenza per la comunicazione come stabilito da Reliable Secure Profile. Viene inoltre illustrato come il client esegue il polling del servizio con richieste "Crea connessione".Quando il servizio è pronto per restituire la richiesta elaborata, utilizza il canale di supporto dell'ultima richiesta "Crea connessione" per la restituzione dei risultati.  
  
7.  Premere INVIO nella finestra della console del servizio per chiudere il servizio.Premere INVIO nella finestra della console client per chiudere il client.