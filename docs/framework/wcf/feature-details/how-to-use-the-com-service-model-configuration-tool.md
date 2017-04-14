---
title: "Procedura: utilizzare lo strumento di configurazione del modello di servizi di COM+ | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "COM+ [WCF], utilizzo dello strumento di configurazione del modello di servizi"
ms.assetid: 7e68cd8d-5fda-4641-b92f-290db874376e
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# Procedura: utilizzare lo strumento di configurazione del modello di servizi di COM+
Dopo aver selezionato una modalità di hosting appropriata, utilizzare lo strumento della riga di comando per la configurazione del modello di servizi COM\+ \(ComSvcConfig.exe\) per configurare le interfacce dell'applicazione da esporre come servizi Web.  
  
> [!NOTE]
>  Per eseguire le attività seguenti è necessario disporre di diritti amministrativi sul computer.  
  
 Quando si utilizza ComSvcConfig.exe su un computer con Windows 7, attenersi alla procedura riportata di seguito per configurare un servizio Web al fine di utilizzare l'ultima versione del modello di servizi \(attualmente v4.5\):  
  
1.  Impostare la chiave del Registro di sistema `[HKEY_LOCAL_COMPUTER\SOFTWARE\Microsoft\.NETFramework]\OnlyUseLatestCLR` su un valore DWORD di 0x00000001  
  
2.  Eseguire comsvcconfig.exe  
  
3.  Ripristinare la chiave del Registro di sistema aggiunta nel passaggio 1 sul valore originale o eliminarla se non esiste.  
  
> [!IMPORTANT]
>  Il ripristino di questa chiave del Registro di sistema è importante.Si tratta di una chiave di compatibilità.Se non si ripristina, questa modifica può causare problemi ad altre applicazioni .NET in esecuzione nel computer.  
  
> [!WARNING]
>  Quando si utilizza ComSvcConfig.exe \/install in un computer con Windows 8, viene visualizzata una finestra di dialogo contenente il messaggio "Un'applicazione installata nel PC richiede la funzionalità di Windows seguente: .NET Framework 3.5 \(include .NET 2.0 e .NET 3.0\)" se .NET Framework 3.5 non è installato.Questa finestra di dialogo può essere ignorata.In alternativa è possibile impostare la chiave del Registro di sistema OnlyUseLatestCLR su un valore DWORD di 0x00000001  
  
### Per aggiungere un'interfaccia al set di interfacce da esporre come servizi Web mediante la modalità di hosting COM\+  
  
-   Eseguire ComSvcConfig utilizzando le opzioni `/install` e `/hosting:complus`, come mostrato nell'esempio seguente.  
  
    ```  
    ComSvcConfig.exe /install /application:OnlineStore /contract:ItemOrders.Financial,IFinances /hosting:complus /verbose  
    ```  
  
     Il comando aggiunge l'interfaccia `IFinances` del componente `ItemOrders.IFinancial` dell'applicazione COM\+ OnlineStore al set di interfacce da esporre come servizi Web.Il servizio utilizza la modalità di hosting COM\+ e pertanto richiede l’attivazione esplicita dell'applicazione.  
  
     Qualora sia necessario esporre solo determinate funzionalità come Servizio Web, evitare di utilizzare il carattere jolly \(\*\) per il componente e l'interfaccia.Se si esegue l'applicazione con una versione successiva di questo componente, l'utilizzo del carattere jolly può comportare l'esposizione indesiderata delle interfacce non presenti al momento della determinazione della sintassi di configurazione.  
  
     L'opzione \/verbose consente di visualizzare sia gli avvisi sia gli errori.  
  
     Il contratto del servizio esposto contiene tutti i metodi dell'interfaccia `IFinances`.  
  
### Per aggiungere solo determinati metodi di un'interfaccia al set di interfacce da esporre come servizi Web mediante la modalità di hosting COM\+  
  
-   Eseguire ComSvcConfig utilizzando le opzioni `/install` e `/hosting:complus` denominando in modo esplicito i metodi da aggiungere, come mostrato nell'esempio seguente.  
  
    ```  
    ComSvcConfig.exe /install /application:OnlineStore /contract:ItemOrders.Financial,IFinances.{Credit,Debit} /hosting:complus /verbose  
    ```  
  
     Il comando aggiunge come operazioni al contratto del servizio esposto solo i metodi `Credit` e `Debit` dell'interfaccia `IFinances`.Tutti gli altri metodi dell'interfaccia vengono omessi dal contratto e non sono chiamabili dai client del servizio Web.  
  
### Per aggiungere un'interfaccia al set di interfacce da esporre come servizi Web mediante la modalità host Web  
  
-   Eseguire ComSvcConfig utilizzando le opzioni `/install` e `/hosting:was`, come mostrato nell'esempio seguente.  
  
    ```  
    ComSvcConfig.exe /install /application:OnlineWarehouse /contract:ItemInventory.Warehouse,IStockLevels /hosting:was /webDirectory:root/OnlineWarehouse /mex /verbose  
    ```  
  
     Questo comando aggiunge l'interfaccia `IStockLevels` del componente `ItemInventory.Warehouse` dell'applicazione COM\+ OnlineWarehouse al set di interfacce da esporre come servizi Web.Il servizio è ospitato su Web nella directory virtuale dell'applicazione OnlineWarehouse di IIS anziché in COM\+. L'applicazione viene pertanto attivata automaticamente secondo le esigenze.  
  
     Per utilizzare la configurazione host Web in corso occorre utilizzare la console di amministrazione di Component Services allo scopo di configurare l'applicazione COM\+ affinché funzioni come applicazione libreria anziché come applicazione server.Le applicazioni configurate come applicazioni server utilizzano la modalità host Web standard e prevedono un hop di processo per elaborare ogni richiesta.  
  
     L'opzione `/mex` aggiunge un endpoint di servizio di scambio metadati \(MEX, Metadata Exchange\) che utilizza lo stesso trasporto utilizzato dall'endpoint di servizio dell'applicazione per supportare i client che desiderano recuperare una definizione di contratto dal servizio.  
  
### Per rimuovere un servizio Web di un'interfaccia specificata  
  
-   Eseguire ComSvcConfig utilizzando l'opzione `/uninstall`, come mostrato nell'esempio seguente.  
  
    ```  
    ComSvcConfig.exe /uninstall /application:OnlineStore /contract:ItemOrders.Financial,IFinances /hosting:complus  
    ```  
  
     Il comando rimuove l'interfaccia `IFinances` del componente `ItemOrders.Financial` dell'applicazione COM\+ OnlineStore.  
  
### Per elencare le interfacce attualmente esposte  
  
-   Eseguire ComSvcConfig utilizzando l'opzione `/list`, come mostrato nell'esempio seguente.  
  
    ```  
    ComSvcConfig.exe /list  
    ```  
  
     Il comando elenca le interfacce attualmente esposte nell'ambito del computer locale, insieme all'indirizzo e ai dettagli di associazione corrispondenti.  
  
### Per elencare determinate interfacce attualmente esposte  
  
-   Eseguire ComSvcConfig utilizzando l'opzione `/list`, come mostrato nell'esempio seguente.  
  
    ```  
    ComSvcConfig.exe /list /application:OnlineStore /hosting:complus  
    ```  
  
     Il comando elenca le interfacce ospitate in COM\+ attualmente esposte, insieme all'indirizzo e ai dettagli di associazione corrispondenti, relative all'applicazione COM\+ OnlineStore contenuta nel computer locale.  
  
### Per visualizzare la Guida relativa alle opzioni disponibili nell'utilità  
  
-   Eseguire ComSvcConfig utilizzando l'opzione \/?come mostrato nell'esempio seguente.  
  
    ```  
    ComSvcConfig.exe /?  
  
    ```  
  
## Vedere anche  
 [Panoramica sull'integrazione con applicazioni COM\+](../../../../docs/framework/wcf/feature-details/integrating-with-com-plus-applications-overview.md)