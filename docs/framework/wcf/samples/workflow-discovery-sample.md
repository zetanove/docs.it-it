---
title: "Esempio di individuazione del flusso di lavoro | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 82cc43f1-3c8f-4771-ac19-a75ac936e2c3
caps.latest.revision: 6
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 6
---
# Esempio di individuazione del flusso di lavoro
In questo esempio viene descritto come rendere individuabile un servizio flusso di lavoro e come creare un'attività di codice personalizzata in grado di effettuare la ricerca di un servizio specifico.  
  
## Dimostrazione  
 Attività di ricerca di individuazione e utilizzo dei flussi di lavoro  
  
## Discussione  
 Nella prima parte dell'esempio, un servizio flusso di lavoro viene reso individuabile mediante la configurazione.La configurazione può inoltre essere utilizzata per applicare il servizio in modo appropriato con metadati personalizzati \(quali gli ambiti\).Nel client, l'esempio impiega un'attività di codice personalizzata che utilizza l'individuazione per ricercare un servizio che corrisponda a un contratto specifico.L'attività di codice restituisce un URI, che viene in seguito utilizzato da un'attività di invio.  
  
#### Per impostare, compilare ed eseguire l'esempio  
  
1.  Questo esempio utilizza endpoint HTTP, che per l'esecuzione devono disporre di ACL URL appropriati \(per ulteriori informazioni, vedere [Configurazione di HTTP e HTTPS](http://go.microsoft.com/fwlink/?LinkId=70353)\).L'esecuzione del comando seguente con un prompt dei comandi con privilegi elevati consente di aggiungere gli ACL appropriati.Sostituire dominio e nome utente per gli argomenti seguenti se la shell non riconosce il formato della variabile.  
  
     **netsh http add urlacl url\=http:\/\/\+:8000\/ user\=%DOMAIN%\\%UserName%**  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Discovery\WorkflowDiscovery`