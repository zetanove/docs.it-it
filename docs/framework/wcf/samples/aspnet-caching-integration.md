---
title: "Integrazione della memorizzazione nella cache di ASP.NET | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f581923a-8a72-42fc-bd6a-46de2aaeecc1
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Integrazione della memorizzazione nella cache di ASP.NET
In questo esempio viene descritto come usare la cache di output ASP.NET con il modello di programmazione HTTP Web WCF.  Vedere l'esempio [Servizio risorse di base](../../../../docs/framework/wcf/samples/basic-resource-service.md) relativo a una versione indipendente di questo scenario in cui viene illustrata in dettaglio l'implementazione del servizio.  In questo argomento viene illustrata la funzionalità di integrazione della cache di output ASP.NET.  
  
## Dimostrazione  
 Integrazione con la cache di output ASP.NET  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.  Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].  Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Web\AspNetCachingIntegration`  
  
## Discussione  
 Nell'esempio viene usato <xref:System.ServiceModel.Web.AspNetCacheProfileAttribute> per la memorizzazione nella cache di output ASP.NET con il servizio [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].  <xref:System.ServiceModel.Web.AspNetCacheProfileAttribute> viene applicato alle operazioni del servizio e fornisce il profilo della cache in un file di configurazione che deve essere applicato alle risposte dell'operazione specifica.  
  
 Nel file Service.cs del progetto di Service di esempio entrambe le operazioni `GetCustomer` e `GetCustomers` sono contrassegnate con <xref:System.ServiceModel.Web.AspNetCacheProfileAttribute> che fornisce il nome del profilo della cache "CacheFor60Seconds."  Nel file Web.config del progetto Service il profilo di cache "CacheFor60Seconds" viene fornito nell'elemento \<`caching`\> di \<`system.web`\>.  Per questo profilo di cache, il valore dell'attributo `duration` è "60", pertanto le risposte associate a questo profilo verranno memorizzate nella cache di output ASP.NET per 60 secondi.  Inoltre, per questo profilo di cache l'attributo `varmByParam` è impostato su "format" e pertanto le risposte alle richieste con valori diversi per il parametro della stringa di query `format` verranno memorizzate nella cache separatamente.  Infine, l'attributo `varyByHeader` del profilo di cache è impostato su "Accept" e pertanto le risposte alle richieste con valori dell'intestazione Accept diversi verranno memorizzate nella cache separatamente.  
  
 Il file Program.cs nel progetto Client dimostra come è possibile creare tale client usando <xref:System.Net.HttpWebRequest>.  È importante sottolineare che quella descritta è solo una delle modalità per accedere a un servizio WCF.  È infatti possibile accedere al servizio usando altre classi .NET Framework come la channel factory [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] e <xref:System.Net.WebClient>.  Altri esempi in SDK \(quali l'esempio [Servizio HTTP di base](../../../../docs/framework/wcf/samples/basic-http-service.md) e l'esempio [Selezione automatica del formato](../../../../docs/framework/wcf/samples/automatic-format-selection.md)\) mostrano come usare queste classi per comunicare con un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
## Per eseguire l'esempio  
 L'esempio è costituito da tre progetti:  
  
-   **Service**: progetto Web che include un servizio HTTP WCF ospitato in ASP.NET.  
  
-   **Client**: progetto di applicazione console che effettua chiamate al servizio.  
  
-   **Common**: libreria condivisa che contiene il tipo Customer usato dal client e dal servizio.  
  
 Quando viene eseguita l'applicazione console Client, il client effettua richieste al servizio e scrive le informazioni pertinenti dalle risposte nella finestra della console.  
  
#### Per eseguire l'esempio  
  
1.  Aprire la soluzione per l'esempio relativo all'integrazione della memorizzazione nella cache di ASP.NET.  
  
2.  Per compilare la soluzione, premere CTRL\+MAIUSC\+B.  
  
3.  Se la finestra **Esplora soluzioni** non è già aperta, premere CTRL\+W\+S.  
  
4.  Nella finestra **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto **Service** e scegliere **Avvia nuova istanza**.  Verrà avviato il server di sviluppo ASP.NET che ospita il servizio.  
  
5.  Nella finestra **Esplora soluzioni** fare clic con il pulsante destro del mouse sul progetto **Client** e scegliere **Avvia nuova istanza**.  
  
6.  Verrà visualizzata la finestra della console client in cui sono inclusi l'URI del servizio in esecuzione e l'URI della pagina della Guida HTML per il servizio in esecuzione.  In qualsiasi momento è possibile visualizzare la pagina della Guida HTML digitando l'URI della pagina della Guida in un browser.  
  
7.  Durante l'esecuzione dell'esempio, il client scrive lo stato dell'attività corrente.  
  
8.  Premere un tasto qualsiasi per chiudere l'applicazione console client.  
  
9. Premere MAIUSC\+F5 per interrompere il debug del servizio.  
  
10. Nell'area di notifica di Windows fare clic con il pulsante destro del mouse sull'icona del server di sviluppo ASP.NET, quindi scegliere **Interrompi**.