---
title: "Determinazione della durata dell&#39;operazione del servizio | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e8a93a2c-2c20-48b3-8986-57e90e9aa908
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Determinazione della durata dell&#39;operazione del servizio
Se la traccia analitica è abilitata in un'applicazione [!INCLUDE[indigo1](../../../../../includes/indigo1-md.md)], la durata di esecuzione per un'operazione del servizio può essere determinata con facilità esaminando il registro eventi.  In questo argomento viene descritto come determinare la quantità di tempo richiesta per il completamento di un'operazione del servizio.  
  
### Determinazione della durata di esecuzione dell'operazione del servizio  
  
1.  Fare clic sul pulsante **Start**, scegliere **Esegui**, quindi immettere `eventvwr.exe` per aprire il Visualizzatore eventi.  
  
2.  Se la traccia analitica non è stata abilitata, espandere **Registri applicazioni e servizi**, **Microsoft**, **Windows**, **Server applicazioni\-Applicazioni**.  Selezionare **Visualizza**, **Visualizza registri analitici e di debug**.  Fare clic con il pulsante destro del mouse su **Analitico** e scegliere **Attiva registro**.  Lasciare aperto il Visualizzatore eventi in modo che sia possibile visualizzare le tracce dopo l'esecuzione dell'operazione del servizio.  
  
3.  Aprire quindi un'applicazione [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] in cui siano inclusi un progetto di servizio e un progetto client che interagisce con tale servizio.  È possibile creare questo tipo di applicazione usando l'[Esercitazione introduttiva](../../../../../docs/framework/wcf/getting-started-tutorial.md).  Se gli esempi [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] sono installati, sarà possibile aprire l'[Guida introduttiva](../../../../../docs/framework/wcf/samples/getting-started-sample.md) contenente il progetto completato creato nell'esercitazione.  
  
4.  Eseguire l'applicazione server premendo **F5**.  Eseguire l'applicazione client facendo clic con il pulsante destro del mouse sul progetto **Client** e scegliendo **Debug**, **Avvia nuova istanza**.  
  
5.  Nel Visualizzatore eventi aggiornare il registro analitico e ordinare gli eventi in base all'ID evento.  Cercare gli eventi con ID evento [214 \- OperationCompleted](../../../../../docs/framework/wcf/diagnostics/etw/214-operationcompleted.md).  Questi eventi indicheranno le operazioni completate, nonché la relativa durata.  L'evento seguente indica la durata di un'operazione Add.  
  
    ```Output  
  
    Chiamata al metodo 'Add' da parte di OperationInvoker completata.  Durata della chiamata al metodo '3' ms.    
    ```