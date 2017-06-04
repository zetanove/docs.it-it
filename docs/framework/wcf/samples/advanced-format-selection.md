---
title: "Selezione avanzata del formato | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e02d9082-4d55-41d8-9329-98f6d1c77f06
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Selezione avanzata del formato
In questo esempio viene descritto come estendere il modello di programmazione REST di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] per supportare i nuovi formati di risposta in uscita.  Nell'esempio viene inoltre usato un modello T4 per restituire la risposta come pagina XHTML, a dimostrazione di come sia possibile implementare un modello di programmazione dello stile di visualizzazione.  
  
## Dettagli dell'esempio  
 L'esempio è costituito da un servizio semplice e dal codice client che effettua le richieste al servizio.  Il servizio supporta una singola operazione \[WebGet\] che dispone della firma del metodo seguente: `Message EchoListWithGet(string list);`  
  
 Quando il client invia una richiesta al servizio, fornisce un elenco delimitato da virgole degli elementi inclusi nel parametro della stringa di query `list` e il servizio restituisce lo stesso elenco in uno dei formati seguenti: XML, JSON, Atom, XHTML o jpeg.  
  
 Il formato di risposta restituito dal servizio viene innanzitutto determinato da un parametro della stringa di query `format` e quindi da un'intestazione HTTP Accept fornita con la richiesta.  Se il valore del parametro della stringa di query `format` corrisponde a uno dei formati precedenti, la risposta viene restituita in tale formato.  Se la stringa di query `format` non è presente, il servizio scorre gli elementi dell'intestazione Accept inclusa nella richiesta e restituisce il formato del primo tipo di contenuto supportato dal servizio.  
  
 È opportuno notare il tipo restituito dall'operazione.  Il modello di programmazione REST di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] supporta a livello nativo solo i formati di risposta XML e JSON quando un'operazione restituisce un tipo diverso da <xref:System.ServiceModel.Channels.Message>.  Tuttavia, quando si usa <xref:System.ServiceModel.Channels.Message> come tipo restituito, lo sviluppatore dispone del controllo completo sulla modalità di formattazione del contenuto del messaggio.  
  
 Nell'esempio vengono usati i metodi <xref:System.ServiceModel.Web.WebOperationContext.CreateXmlResponse%2A>, <xref:System.ServiceModel.Web.WebOperationContext.CreateJsonResponse%2A> e <xref:System.ServiceModel.Web.WebOperationContext.CreateAtom10Response%2A> per serializzare l'elenco di stringhe rispettivamente in messaggi XML, JSON e ATOM.  Per il formato di risposta jpeg, viene usato il metodo <xref:System.ServiceModel.Web.WebOperationContext.CreateStreamResponse%2A> e l'immagine viene salvata nel flusso.  Per la risposta XHTML, viene usato il metodo <xref:System.ServiceModel.Web.WebOperationContext.CreateTextResponse%2A> insieme a un modello T4 pre\-elaborato costituito da un file con estensione tt e da un file con estensione cs generato automaticamente.  Il file con estensione tt consente a uno sviluppatore di scrivere una risposta in un form del modello contenente variabili e strutture di controllo.  [!INCLUDE[crabout](../../../../includes/crabout-md.md)] T4, vedere [Generazione di codice e modelli di testo T4](http://go.microsoft.com/fwlink/?LinkId=166023).  
  
 L'esempio è costituito da un servizio indipendente e da un client in esecuzione in un'applicazione console.  Quando l'applicazione console è in esecuzione, il client invia richieste al servizio e scrive nella finestra della console le informazioni pertinenti incluse nelle risposte.  
  
#### Per eseguire l'esempio  
  
1.  Aprire la soluzione per l'esempio relativo alla selezione avanzata del formato.  Per garantire l'esecuzione corretta dell'esempio, è necessario che l'avvio di [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] venga eseguito come amministratore.  A tale scopo, fare clic con il pulsante destro del mouse sull'icona [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] e scegliere **Esegui come amministratore** dal menu di scelta rapida.  
  
2.  Premere CTRL\+MAIUSC\+B per compilare la soluzione, quindi premere CTRL\+F5 per eseguire il progetto AdvancedFormatSelection dell'applicazione console senza eseguirne il debug.  Verrà visualizzata la finestra della console in cui saranno disponibili gli URI del servizio in esecuzione e della pagina della Guida HTML per il servizio in esecuzione.  
  
3.  Durante l'esecuzione dell'esempio, il client invia richieste al servizio e scrive le risposte nella finestra della console.  Si notino i formati diversi delle risposte, ovvero XML, JSON, Atom e XHTML.  
  
4.  Verrà quindi richiesto di passare a un URI tramite il quale è possibile richiedere la risposta in un formato jpeg.  Aprire un browser e passare all'URI specificato.  
  
5.  Premere un tasto qualsiasi per terminare l'esempio.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.  Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].  Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Web\AdvancedFormatSelection`  
  
## Vedere anche