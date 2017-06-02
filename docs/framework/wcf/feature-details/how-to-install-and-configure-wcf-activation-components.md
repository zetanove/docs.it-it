---
title: "Procedura: installare e configurare componenti di attivazione WCF | Microsoft Docs"
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
  - "Attivazione HTTP [WCF]"
ms.assetid: 33a7054a-73ec-464d-83e5-b203aeded658
caps.latest.revision: 16
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 16
---
# Procedura: installare e configurare componenti di attivazione WCF
In questo argomento vengono illustrati i passaggi richiesti per impostare il servizio di attivazione dei processi di Windows \(anche noto come WAS\) in [!INCLUDE[wv](../../../../includes/wv-md.md)] per ospitare servizi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] che non comunicano su protocolli di rete HTTP.Nelle sezioni seguenti vengono spiegati i passaggi relativi a tale configurazione:  
  
-   Installare i componenti di attivazione [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], o controllarne l'installazione.  
  
-   Configurare WAS per supportare un protocollo non HTTP.Nella procedura seguente viene illustrato come configurare [!INCLUDE[wv](../../../../includes/wv-md.md)] per l'attivazione TCP.  
  
 Dopo aver installato e configurato WAS, vedere [Procedura: ospitare un servizio WCF in WAS](../../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-was.md) per le procedure relative alla creazione di un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] che espone un endpoint non HTTP che utilizza WAS.  
  
### Per installare i componenti di attivazione WCF non HTTP  
  
1.  Fare clic sul pulsante **Start**, quindi scegliere **Pannello di controllo**.  
  
2.  Fare clic su **Programmi**, quindi su **Programmi e funzionalità**.  
  
3.  Scegliere **Attivazione o disattivazione delle funzionalità Windows** dal menu **Attività**.  
  
4.  Individuare il nodo [!INCLUDE[vstecwinfx](../../../../includes/vstecwinfx-md.md)], selezionarlo e quindi espanderlo.  
  
5.  Selezionare la casella **Componenti di attivazione WCF non HTTP** e salvare l'impostazione.  
  
### Per configurare WAS per supportare l'attivazione TCP  
  
1.  Per supportare l'attivazione net.tcp, è prima necessario associare il sito Web predefinito a una porta net.tcp.A tale fine, utilizzare Appcmd.exe, installato con il set di strumenti di gestione di [!INCLUDE[iisver](../../../../includes/iisver-md.md)].In una finestra del prompt dei comandi a livello di amministratore, eseguire il comando seguente.  
  
    ```  
    %windir%\system32\inetsrv\appcmd.exe set site "Default Web Site" -+bindings.[protocol='net.tcp',bindingInformation='808:*']  
    ```  
  
    > [!NOTE]
    >  Questo comando è una singola riga di testo.Il comando aggiunge un'associazione del sito net.tcp al sito Web predefinito in ascolto sulla porta TCP 808 con qualsiasi nome host.  
  
2.  Anche se tutte le applicazioni all'interno di un sito condividono un'associazione net.tcp comune, ognuna di esse può attivare il supporto net.tcp individualmente.Per attivare net.tcp per l'applicazione, eseguire il comando seguente da un prompt dei comandi a livello di amministratore.  
  
    ```  
    %windir%\system32\inetsrv\appcmd.exe set app   
    "Default Web Site/<WCF Application>" /enabledProtocols:http,net.tcp  
    ```  
  
    > [!NOTE]
    >  Questo comando è una singola riga di testo.Il comando abilita l'accesso all'applicazione \/\<*WCF Application*\> utilizzando sia http:\/\/localhost*\/\<WCF Application\>* sia net.tcp:\/\/localhost\/*\<WCF Application\>*.  
  
     Rimuovere l'associazione del sito net.tcp aggiunta per questo esempio.  
  
     Per comodità, i due passaggi seguenti vengono implementati in un file batch chiamato RemoveNetTcpSiteBinding.cmd situato nella directory di esempio.  
  
    1.  Rimuovere net.tcp dall'elenco dei protocolli attivati tramite il comando seguente in una finestra del prompt dei comandi a livello di amministratore.  
  
        ```  
        %windir%\system32\inetsrv\appcmd.exe set app   
        "Default Web Site/servicemodelsamples<WCF Application>" " /enabledProtocols:http  
        ```  
  
        > [!NOTE]
        >  Questo comando è una singola riga di testo.  
  
    2.  Rimuovere l'associazione del sito net.tcp tramite il comando seguente in una finestra del prompt dei comandi con privilegi elevati:  
  
        ```  
        %windir%\system32\inetsrv\appcmd.exe set site "Default Web Site"   
        --bindings.[protocol='net.tcp',bindingInformation='808:*']  
        ```  
  
        > [!NOTE]
        >  Questo comando è una singola riga di testo.  
  
### Per rimuovere net.tcp dall'elenco dei protocolli attivati  
  
1.  Per rimuovere net.tcp dall'elenco dei protocolli attivati, eseguire il comando seguente in una finestra del prompt dei comandi a livello di amministratore.  
  
    ```  
    %windir%\system32\inetsrv\appcmd.exe set app "Default Web Site/servicemodelsamples<WCF Application>" " /enabledProtocols:http  
    ```  
  
    > [!NOTE]
    >  Questo comando è una singola riga di testo.  
  
### Per rimuovere l'associazione del sito net.tcp  
  
1.  Per rimuovere l'associazione del sito net.tcp, eseguire il comando seguente in una finestra del prompt dei comandi a livello di amministratore.  
  
    ```  
    %windir%\system32\inetsrv\appcmd.exe set site "Default Web Site"   
    -bindings.[protocol='net.tcp',bindingInformation='808:*']  
    ```  
  
    > [!NOTE]
    >  Questo comando è una singola riga di testo.  
  
## Vedere anche  
 [Attivazione TCP](../../../../docs/framework/wcf/samples/tcp-activation.md)   
 [Attivazione MSMQ](../../../../docs/framework/wcf/samples/msmq-activation.md)   
 [Attivazione di NamedPipe](../../../../docs/framework/wcf/samples/namedpipe-activation.md)   
 [Funzionalità di hosting di AppFabric](http://go.microsoft.com/fwlink/?LinkId=201276)