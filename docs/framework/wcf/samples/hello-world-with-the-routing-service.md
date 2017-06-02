---
title: "Hello World con il servizio di routing | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 0f4b0d5b-6522-4ad5-9f3a-baa78316d7d1
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# Hello World con il servizio di routing
Nell'esempio viene descritto il servizio di routing di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].Il servizio di routing è un componente di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] che semplifica l'aggiunta nell'applicazione di un router basato sul contenuto.L'esempio adatta l'esempio relativo alla calcolatrice standard di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] per comunicare utilizzando il servizio di routing.In questo esempio, il client calcolatrice è configurato per inviare messaggi a un endpoint esposto dal router.Il servizio di routing è configurato per accettare tutti i messaggi ad esso inviati e per inoltrarli a un endpoint che corrisponde al servizio di calcolatrice.I messaggi inviati dal client vengono pertanto ricevuti dal router e reindirizzati al servizio di calcolatrice effettivo.I messaggi provenienti dal servizio di calcolatrice di backup vengono inviati nuovamente al router del servizio, che a sua volta li inoltra al client calcolatrice.  
  
### Per utilizzare questo esempio  
  
1.  Utilizzando [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)], aprire HelloRoutingService.sln.  
  
2.  Premere F5 o CTRL\+MAIUSC\+B.  
  
    > [!NOTE]
    >  Se si preme F5, il client calcolatrice viene avviato automaticamente.Se si preme CTRL\+MAIUSC\+B \(compilazione\), è necessario avviare le applicazioni seguenti.  
    >   
    >  1.  Client calcolatrice \(.\/CalculatorClient\/bin\/client.exe  
    > 2.  Servizio di calcolatrice \(.\/CalculatorService\/bin\/service.exe\)  
    > 3.  Servizio di routing \(.\/RoutingService\/bin\/RoutingService.exe\)  
  
3.  Premere INVIO per avviare il client.  
  
     È necessario visualizzare il seguente output:  
  
     Add\(100,15.99\) \= 115.99  
  
     Subtract\(145,76.54\) \= 68.46  
  
     Multiply\(9,81.25\) \= 731.25  
  
     Divide\(22,7\) \= 3.14285714285714  
  
## Configurabile tramite codice o App.Config  
 L'esempio proposto è configurato per l'utilizzo di un file App.config per definire il comportamento del router.È inoltre possibile modificare il nome del file App.config affinché non venga riconosciuto e rimuovere i commenti dalla chiamata al metodo in ConfigureRouterViaCode\(\).Entrambi i metodi restituiscono lo stesso comportamento da parte del router.  
  
### Scenario  
 Questo esempio descrive l'utilizzo del router come message pump di base.Il servizio di routing viene utilizzato come nodo proxy trasparente configurato per inoltrare direttamente messaggi a un set preconfigurato di endpoint di destinazione.  
  
### Scenario reale  
 Contoso desidera incrementare la flessibilità relativa a denominazione, indirizzamento, configurazione e sicurezza dei propri servizi.A tale scopo, una message pump di base viene posizionata di fronte ai servizi per essere utilizzata come endpoint rivolto al pubblico.Ciò consente di posizionare sicurezza aggiuntiva davanti ai servizi effettivi e di semplificare l'implementazione di soluzioni di scalabilità o di controllo delle versioni del servizio in una data successiva.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\RoutingServices\HelloRoutingService`  
  
## Vedere anche  
 [Hosting e salvataggio permanente](http://go.microsoft.com/fwlink/?LinkId=193961)