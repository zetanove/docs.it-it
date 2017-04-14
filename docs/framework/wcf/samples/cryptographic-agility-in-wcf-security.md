---
title: "Agilit&#224; di crittografia nella sicurezza WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: c2c549e5-ac19-40c5-b686-8f67f52b6dbf
caps.latest.revision: 9
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 9
---
# Agilit&#224; di crittografia nella sicurezza WCF
In questo esempio viene illustrato come specificare un algoritmo standard\/personalizzato per offrire un'implementazione di crittografia Agile in un servizio e in un client [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].  L'esempio è costituito dai progetti seguenti:  
  
 Servizio  
 Si tratta di un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] indipendente che implementa l'interfaccia `ICalculator` e protegge l'endpoint usando <xref:System.ServiceModel.WsHttpBinding> con le impostazioni di sessione protetta e sessione affidabile disabilitate.  Il servizio definisce una classe `SecurityAlgorithmSuite` personalizzata per specificare gli algoritmi di crittografia da usare per la sicurezza dei messaggi.  
  
 Client  
 Si tratta di un client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] che accede al servizio dopo l'autenticazione.  Richiama le operazioni esposte dall'interfaccia `ICalculator` e viene implementa dal servizio.  Il servizio definisce inoltre la stessa classe `SecurityAlgorithmSuite` personalizzata per specificare gli algoritmi di crittografia da usare per la sicurezza dei messaggi.  
  
### Per usare questo esempio  
  
1.  Aprire la soluzione CryptoAgility.sln in [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)].  
  
2.  Per compilare la soluzione, premere CTRL\+MAIUSC\+B.  
  
3.  Aprire [!INCLUDE[fileExplorer](../../../../includes/fileexplorer-md.md)] e passare alla directory \\WCF\\Basic\\Security\\CryptoAgility\\Service\\bin, quindi eseguire il file service.exe con i privilegi di amministratore facendo clic con il pulsante destro del mouse su service.exe e scegliendo **Esegui come amministratore**.  
  
4.  Passare alla directory \\WCF\\Basic\\Security\\CryptoAgility\\Client\\bin ed eseguire il file client.exe.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.  Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].  Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Security\CryptoAgility`  
  
## Vedere anche  
 [Sicurezza](../../../../docs/framework/wcf/feature-details/security.md)