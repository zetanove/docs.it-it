---
title: "Invio del form | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: fa6f84f9-2e07-4e3c-92d0-a245308b7dff
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Invio del form
In questo esempio viene descritto come estendere il modello di programmazione WCF REST per supportare i nuovi formati delle richieste in entrata.  Nell'esempio è inoltre inclusa l'implementazione di un formattatore in grado di deserializzare una richiesta da un invio di form HTML in un tipo di [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)].  Nell'esempio viene infine usato un modello T4 per la restituzione di una pagina HTML, il quale fornisce il form HTML che gli utenti possono usare per eseguire il postback al servizio WCF REST.  
  
## Dimostrazione  
  
-   Estensione del supporto per i formati delle richieste in entrata.  
  
-   Integrazione di modelli T4.  
  
## Discussione  
 L'esempio è costituito da due progetti.  Il primo progetto è la libreria HtmlFormProcessing che include un formattatore di richieste personalizzato in grado di deserializzare invii di form HTML nei tipi di [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)].  Il secondo progetto è un'applicazione console che estende l'esempio relativo al servizio risorse di base per l'uso del formattatore di richieste personalizzato della libreria HtmlFormProcessing.  
  
 Il formattatore personalizzato in grado di deserializzare invii di form HTML \(HtmlFormRequestDispatchFormatter\) accetta entrambi i tipi di [!INCLUDE[dnprdnshort](../../../../includes/dnprdnshort-md.md)] che possono essere convertiti da una stringa usando <xref:System.ServiceModel.Dispatcher.QueryStringConverter> e i tipi contrassegnati con <xref:System.Runtime.Serialization.DataContractAttribute> che dispongono esclusivamente di membri convertibili da una stringa tramite QueryStringConverter.  
  
 Nel progetto di libreria HtmlFormProcessing è inoltre inclusa una classe di base astratta, ovvero `RequestBodyDispatchFormatter`, che può essere usata per creare altri formattatori di richieste personalizzati.  La derivazione da `RequestBodyDispatchFormatter` consente a uno sviluppatore di concentrarsi sulla logica di deserializzazione del corpo della richiesta, permettendo alla classe di base di eseguire il mapping dei parametri del modello di URI ai parametri del metodo dell'operazione.  Nel progetto di libreria HtmlFormProcessing è inoltre inclusa la classe `HtmlFormProcessingBehavior`, che illustra come derivare da <xref:System.ServiceModel.Description.WebHttpBehavior> per sostituire il formattatore di richieste predefinito con un formattatore di richieste personalizzato.  
  
 Questo progetto di applicazione console rappresenta un'estensione dell'esempio [Servizio risorse di base](../../../../docs/framework/wcf/samples/basic-resource-service.md).  Nell'esempio relativo al servizio risorse di base viene illustrato come esporre una risorsa in modo che venga usato il modello di programmazione WCF REST.  Nell'esempio relativo al servizio risorse di base una risorsa raccolta di clienti viene esposta in modo tale che i clienti della raccolta possano essere creati, recuperati, aggiornati ed eliminati.  Nell'esempio relativo al servizio risorse di base vengono usati esclusivamente due formati per le richieste in entrata supportati a livello nativo, ovvero XML e JSON.  
  
 L'applicazione console in questo esempio relativo all'invio di form usa il formattatore personalizzato incluso nella libreria HtmlFormProcessing che consente agli utenti di creare clienti inviando una richiesta da un invio di form HTML mediante un browser.  Consente inoltre di aggiungere un'operazione che restituisce una pagina HTML in cui è incluso il form del quale eseguire il postback al servizio.  Questa pagina HTML viene generata usando un modello T4 pre\-elaborato costituito da un file con estensione tt e da un file con estensione cs generato automaticamente.  Il file con estensione tt consente a uno sviluppatore di scrivere una risposta in un form del modello contenente variabili e strutture di controllo.  [!INCLUDE[crabout](../../../../includes/crabout-md.md)] T4, vedere [Generazione di codice e modelli di testo T4](http://go.microsoft.com/fwlink/?LinkId=178139).  
  
#### Per eseguire l'esempio  
  
1.  Aprire la soluzione per l'esempio relativo all'invio del form.  Per garantire l'esecuzione corretta dell'esempio, è necessario avviare [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] come amministratore.  A tale scopo, fare clic con il pulsante destro del mouse sull'icona di [!INCLUDE[vs_current_long](../../../../includes/vs-current-long-md.md)] e scegliere "Esegui come amministratore" dal menu di scelta rapida.  
  
2.  Premere CTRL\+MAIUSC\+B per compilare la soluzione, quindi premere CTRL\+F5 per eseguire il progetto di applicazione console FormPost.  
  
3.  Verrà visualizzata la finestra della console in cui saranno disponibili gli URI del servizio in esecuzione e della pagina della Guida HTML per il servizio in esecuzione.  
  
4.  Durante l'esecuzione dell'esempio, il client scrive lo stato dell'attività corrente, qualora sia in corso l'aggiunta, l'aggiornamento o l'eliminazione di un cliente oppure il recupero di un elenco dei clienti correnti dal servizio nella finestra della console.  
  
5.  Verrà quindi richiesto di passare all'URI del form dei clienti.  Aprire un browser e passare all'URI specificato.  Digitare un nome e un indirizzo per il cliente e fare clic sul pulsante **Invia**.  
  
6.  Premere un tasto qualsiasi per fare in modo che l'esempio continui a essere eseguito nella finestra della console.  
  
7.  Durante il completamento dell'esempio, si noti che il cliente creato usando il browser è stato incluso nell'elenco finale di clienti.  
  
8.  Premere un tasto qualsiasi per terminare l'esempio.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.  Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi di [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].  Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Extensibility\Web\FormPost`