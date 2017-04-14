---
title: "Attivazione XAML | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 486760e2-bb10-4ed5-8c02-fe7472498d2d
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Attivazione XAML
In questo esempio viene illustrato come ospitare un flusso di lavoro dichiarativo in IIS.L'esempio è un flusso di lavoro di base chiamato `EchoService` che ha un'operazione.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, visitare la pagina di download per scaricare tutti gli esempi di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WF\Basic\Services\XAMLActivation`  
  
#### Per impostare, compilare ed eseguire l'esempio  
  
1.  Aprire la soluzione XAMLActivation.sln in [!INCLUDE[vs2010](../../../../includes/vs2010-md.md)].  
  
2.  Compilare la soluzione premendo **F5**.  
  
3.  Eseguire WcfTestClient.exe.Da un prompt dei comandi digitare il comando seguente:  
  
    1.  cd %SystemDrive%\\Programmi\\Microsoft Visual Studio 10.0\\Common7\\IDE\\  
  
    2.  Eseguire WcfTestClient.exe.  
  
4.  Impostare l'indirizzo del servizio su WcfTestClient.exe premendo CTRL\+MAIUSC\+A e impostando l'indirizzo del servizio su http:\/\/localhost:56133\/Service.xamlx.  
  
5.  Eseguire l'operazione echo per testare il servizio.  
  
6.  Distribuire il servizio in IIS utilizzando DeployToIIS.Bat in un prompt dei comandi con privilegi di amministratore.  
  
7.  Aggiornare l'indirizzo del servizio nel client modificandolo in http:\/\/localhost\/XAMLActivation\/Service.xamlx e testare di nuovo il servizio utilizzando WcfTestClient.exe.