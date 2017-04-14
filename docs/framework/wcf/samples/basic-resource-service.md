---
title: "Servizio risorse di base | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4360063e-cc8c-4648-846e-c05a5af51a7a
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Servizio risorse di base
Questo esempio illustra come implementare un servizio basato su HTTP utilizzando il modello di programmazione REST [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)], che espone una raccolta di clienti che supporta operazioni di recupero, aggiunta, eliminazione e sostituzione.L'esempio è costituito da 2 componenti \- un servizio HTTP [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] indipendente \(Service.cs\) e un'applicazione console \(program.cs\) che crea il servizio ed effettua chiamate verso il servizio.  
  
## Dettagli dell'esempio  
 Il servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] presenta una raccolta di clienti in modo orientato alle risorse\/REST.In breve, ciò significa disporre di URI univoci per la raccolta di clienti e per ogni cliente nella raccolta.Il servizio supporta l'invio di un HTTP `GET` all'URI della raccolta per recuperare l'intera raccolta e di HTTP `POST` all'URI della raccolta per aggiungere un nuovo cliente alla raccolta.Anche a livello di URI per singolo cliente, supporta `GET` HTTP per ottenere i dettagli del cliente, `PUT` HTTP per sostituire i dettagli del cliente e `DELETE` HTTP per rimuovere il cliente dalla raccolta.Quando un nuovo cliente viene aggiunto alla raccolta, il servizio gli assegna un URI univoco e lo archivia come parte dei dettagli del cliente.Inoltre, comunica l'URI al client utilizzando l'intestazione HTTP relativa al percorso della risposta.  
  
 Il file App.config configura il servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] con un <xref:System.ServiceModel.Description.WebHttpEndpoint> predefinito che dispone della proprietà <xref:System.ServiceModel.Description.WebHttpEndpoint.HelpEnabled%2A> configurata su `true`.Di conseguenza, l'infrastruttura [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] crea una pagina automatica della Guida basata su HTML all'indirizzo `http://localhost:8000/Customers/help`, che fornisce informazioni su come creare richieste HTTP per il servizio e su come accedere alla risposta HTTP del servizio, quale un esempio di come i dettagli del cliente vengono rappresentati in XML e JSON.  
  
 La presentazione della raccolta di clienti \(e, in termini più generali, di qualsiasi risorsa\) in questo modo consente al client di interagire con essa in modo uniforme utilizzando URI e HTTP `GET`, `PUT`, `DELETE` e `POST`.Il file Program.cs illustra come è possibile creare tale client utilizzando <xref:System.Net.HttpWebRequest>.È importante sottolineare che quella descritta è solo una delle modalità per accedere a un servizio REST [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].È infatti possibile accedere al servizio utilizzando altre classi .NET Framework come la <xref:System.ServiceModel.ChannelFactory> e <xref:System.Net.WebClient>.Altri esempi in SDK \(quali l'esempio [Servizio HTTP di base](../../../../docs/framework/wcf/samples/basic-http-service.md) e l'esempio [Selezione automatica del formato](../../../../docs/framework/wcf/samples/automatic-format-selection.md)\) mostrano come utilizzare queste classi per comunicare con un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
 L'esempio è costituito da un servizio indipendente e da un client, entrambi in esecuzione in un'applicazione console.Quando l'applicazione console è in esecuzione, il client invia richieste al servizio e scrive nella finestra della console le informazioni pertinenti incluse nelle risposte.  
  
#### Per utilizzare questo esempio  
  
1.  Aprire la soluzione per l'esempio relativo al servizio risorse di base.Per garantire l'esecuzione corretta dell'esempio è necessario che l'avvio di [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] venga eseguito come amministratore.Procedere facendo clic con il pulsante destro del mouse sull'icona [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] e selezionando **Esegui come amministratore** nel menu di scelta rapida.  
  
2.  Premere CTRL\+MAIUSC\+B per compilare la soluzione, quindi premere Ctrl\+F5 per eseguire l'applicazione console.Verrà visualizzata la finestra della console in cui saranno disponibili gli URI del servizio in esecuzione e della pagina della Guida HTML per il servizio in esecuzione.In qualsiasi momento è possibile visualizzare la pagina della Guida HTML digitando l'URI della pagina della Guida in un browser.Durante l'esecuzione dell'esempio, il client scrive lo stato dell'attività corrente.  
  
3.  Premere un tasto qualsiasi per chiudere l'esempio.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Web\BasicResourceService`  
  
## Vedere anche  
 [Servizio HTTP di base](../../../../docs/framework/wcf/samples/basic-http-service.md)   
 [Selezione automatica del formato](../../../../docs/framework/wcf/samples/automatic-format-selection.md)