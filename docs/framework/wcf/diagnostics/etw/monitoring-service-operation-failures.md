---
title: "Monitoraggio di errori relativi alle operazioni del servizio | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 59472ba3-8ebf-4479-bd7b-f440d5e636cb
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Monitoraggio di errori relativi alle operazioni del servizio
Se la traccia analitica è abilitata per un'applicazione, è possibile monitorare gli errori del servizio facilmente nel visualizzatore eventi.Questo argomento illustra come determinare quando un'operazione del servizio non riesce e come determinare ciò che ha provocato l'errore.  
  
### Informazioni sulla determinazione di errori relativi alle operazioni del servizio  
  
1.  Aprire il Visualizzatore eventi facendo clic sul pulsante **Start**, quindi scegliendo **Esegui** e immettendo `eventvwr.exe`.  
  
2.  Se la traccia analitica non è stata abilitata, espandere **Registri applicazioni e servizi**, **Microsoft**, **Windows**, **Server applicazioni\-Applicazioni**.Selezionare **Visualizza**, **Visualizza registri analitici e di debug**.Fare clic con il pulsante destro del mouse su **Analitico** e scegliere **Attiva registro**.Lasciare aperto il Visualizzatore eventi in modo che le tracce possano essere visualizzate dopo la mancata riuscita dell'operazione del servizio.  
  
3.  Aprire quindi l'esempio creato nell'[Esercitazione introduttiva](../../../../../docs/framework/wcf/getting-started-tutorial.md) in [!INCLUDE[vs_current_long](../../../../../includes/vs-current-long-md.md)] È necessario eseguire [!INCLUDE[vs_current_long](../../../../../includes/vs-current-long-md.md)] come amministratore in modo che sia possibile creare il servizio.Se si dispone degli esempi [!INCLUDE[indigo2](../../../../../includes/indigo2-md.md)] installati, è possibile aprire l'[Guida introduttiva](../../../../../docs/framework/wcf/samples/getting-started-sample.md), che contiene il progetto completato creato nell'esercitazione.  
  
4.  Nel file Program.cs del progetto Server aggiungere la riga di codice seguente all'inizio del metodo `Divide` nella classe `CalculatorService`:  
  
    ```  
    if (n2 == 0) throw new DivideByZeroException();  
  
    ```  
  
5.  Nel file Program.cs nel progetto Client, assegnare a value2 il valore zero:  
  
    ```  
    //Call the Divide service operation  
    value1 = 22.00D;  
    value2 = 0.00D;  
    result = client.Divide(value1, value2);  
    Console.WriteLine("Divide({0}, {1}) = {2}", value1, value2, result);  
  
    ```  
  
6.  Eseguire l'applicazione server senza debug premendo **Ctrl\+F5**.  
  
7.  Aprire il prompt dei comandi di Visual Studio.Passare alla directory client ed eseguire il client dalla riga di comando.  
  
8.  Nel Visualizzatore eventi, disabilitare e aggiornare il registro analitico e ordinare gli eventi in base all'ID evento.Cercare un evento con ID evento [219 \- ServiceException](../../../../../docs/framework/wcf/diagnostics/etw/219-serviceexception.md), che descrive l'errore del servizio.  
  
    ```Output  
    Riscontrata un'eccezione non gestita di tipo "System.DivideByZeroException" durante l'elaborazione del messaggio.Eccezione ToString completa: System.DivideByZeroException: Tentativo di divisione per zero.  
    ```  
  
    > [!NOTE]
    >  Gli eventi vengono memorizzati nel buffer in caso di invio al visualizzatore eventi; è possibile che l'evento relativo all'errore non venga subito visualizzato.