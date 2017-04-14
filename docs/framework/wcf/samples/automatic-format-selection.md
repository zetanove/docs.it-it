---
title: "Selezione automatica del formato | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: dab51e56-8517-4a6a-bb54-b55b15ab37bb
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Selezione automatica del formato
In questo esempio viene descritto come abilitare la selezione automatica del formato \(XML o JSON\) con il modello di programmazione REST di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e come impostare in modo esplicito il formato nel codice dell'operazione.  
  
## Dettagli dell'esempio  
 L'esempio è costituito da un servizio e dal codice client che effettua le richieste al servizio.  Il servizio supporta una singola operazione `GET` \(`EchoWithGet`\) HTTP e una singola operazione `POST` \(`EchoWithPost`\) HTTP.  Entrambe operazioni prevedono una stringa, quindi restituiscono la stringa nella risposta.  Con l'operazione `GET`, la stringa viene fornita in un parametro della stringa di query dell'URI.  Con l'operazione `POST`, la stringa viene fornita nel corpo della richiesta serializzata in XML.  Il servizio è in grado di restituire risposte in XML o JSON usando le nuove funzionalità di selezione automatica del formato e di selezione imperativa del formato di [!INCLUDE[netfx40_long](../../../../includes/netfx40-long-md.md)].  
  
 Nell'esempio la selezione automatica del formato viene abilitata tramite il file App.config.  Sull'endpoint HTTP Web predefinito all'attributo `automaticFormatSelectionEnabled` è stato assegnato il valore `true`.  Con la selezione automatica del formato abilitata, l'infrastruttura di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] seleziona il formato di riposta più appropriato \(XML o JSON\) analizzando le intestazioni HTTP Accept e Content\-Type della richiesta.  Per usare questa nuova funzionalità, non è necessario che lo sviluppatore fornisca una configurazione o un codice aggiuntivo oltre all'impostazione dell'attributo `automaticFormatSelectionEnabled` su `true`.  Nel codice client in Program.cs le richieste vengono inviate a entrambe le operazioni `GET` e `POST` del servizio con l'intestazione HTTP Accept specificata come "applicazione\/xml" o "applicazione\/json" e il servizio restituisce una risposta nel formato corrispondente.  
  
 Anche nell'operazione `GET` viene usata la selezione imperativa del formato.  L'operazione `GET` verifica se è presente un parametro della stringa di query `format` facoltativo e in caso affermativo imposta il formato della risposta sulla proprietà <xref:System.ServiceModel.Web.WebOperationContext.OutgoingResponse%2A>.  In questo modo, l'impostazione imperativa del formato della risposta determina l'override della selezione automatica del formato effettuata dall'infrastruttura di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
 L'esempio è costituito da un servizio indipendente e da un client in esecuzione in un'applicazione console.  Quando l'applicazione console è in esecuzione, il client invia richieste al servizio e scrive nella finestra della console le informazioni pertinenti incluse nelle risposte.  
  
#### Per usare questo esempio  
  
1.  Aprire la soluzione per l'esempio relativo alla selezione automatica del formato.  Per garantire l'esecuzione corretta dell'esempio, è necessario che l'avvio di [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] venga eseguito come amministratore.  A tale scopo, fare clic con il pulsante destro del mouse sull'icona di [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] e scegliere **Esegui come amministratore** dal menu di scelta rapida.  
  
2.  Premere CTRL\+MAIUSC\+B per compilare la soluzione, quindi premere CTRL\+F5 per eseguire il progetto AutomaticFormatSelection dell'applicazione console.  Verrà visualizzata la finestra della console in cui saranno disponibili gli URI del servizio in esecuzione e della pagina della Guida HTML per il servizio in esecuzione.  
  
3.  Durante l'esecuzione dell'esempio, il client invia richieste al servizio e scrive le risposte nella finestra della console.  Si notino i formati diversi delle risposte in XML e JSON.  
  
4.  Premere un tasto qualsiasi per terminare l'esempio.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.  Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].  Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Web\AutomaticFormatSelection`  
  
## Vedere anche