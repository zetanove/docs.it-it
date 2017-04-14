---
title: "Visualizzazione dei log dei messaggi | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 3012fa13-f650-45fb-aaea-c5cca8c7d372
caps.latest.revision: 22
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 22
---
# Visualizzazione dei log dei messaggi
In questo argomento viene illustrato come visualizzare i log dei messaggi.  
  
## Visualizzazione dei log dei messaggi nel visualizzatore di tracce dei servizi  
 Un messaggio verrà trasformato dall'elaborazione di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].Di conseguenza, un messaggio registrato riflette solo il suo contenuto nel momento in cui è stato registrato, non il contenuto in transito.  
  
 Poichè l'output della registrazione dei messaggi non ha alcuna relazione con il formato di trasferimento del messaggio, la registrazione genera sempre il messaggio decodificato.Se la registrazione del messaggio è stata configurata correttamente, i messaggi registrati devono essere visualizzati in testo normale.Ad esempio, il formato \(testo normale\) dei messaggi registrati non è influenzato dall'utilizzo di un codificatore di messaggi binario.  
  
 L'output di XmlWriterTraceListener è un file che contiene una sequenza di frammenti XML.È necessario sapere che il file non è un file XML valido.Per visualizzare i file log dei messaggi, è consigliabile utilizzare [Strumento Visualizzatore di tracce dei servizi \(SvcTraceViewer.exe\)](../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md).Per ulteriori informazioni sull'utilizzo di questo strumento, vedere [Utilizzo di Service Trace Viewer per la visualizzazione di tracce correlate e risoluzione dei problemi](../../../../docs/framework/wcf/diagnostics/tracing/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting.md).  
  
 Nel visualizzatore delle tracce dei servizi, i messaggi sono elencati nella scheda **Messaggio**.I messaggi che hanno causato, o che sono correlati a un errore dell'elaborazione sono evidenziati in giallo \(livello di avviso\) o rosso \(livello dell'errore\), a seconda della gravità dell'errore.Un doppio clic sul messaggio ne rivela la traccia nel contesto della richiesta di elaborazione.  
  
> [!NOTE]
>  Se un messaggio non ha intestazione, non viene registrato alcun tag `<header/>`.  
  
## Visualizzazione dei messaggi registrati da client, relay e servizio  
 L'ambiente può contenere un client che invia un messaggio a un relay che successivamente lo inoltra al servizio.Quando la registrazione del messaggio è attivata su tutti e tre i percorsi, e tutti e tre i log dei messaggi vengono visualizzati simultaneamente in [Strumento Visualizzatore di tracce dei servizi \(SvcTraceViewer.exe\)](../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md), gli scambi di log dei messaggi verranno resi in modo incorretto.Questa situazione si verifica perché `CorrelationId` e `ActivityId` nell'intestazione del messaggio non sono univoci per ogni coppia invio\-ricezione.  
  
 Per risolvere il problema, utilizzare uno dei metodi seguenti:  
  
-   Visualizzare contemporaneamente solo due dei tre log dei messaggi nello [Strumento Visualizzatore di tracce dei servizi \(SvcTraceViewer.exe\)](../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md).  
  
-   Se è necessario visualizzare contemporaneamente i tre log nello [Strumento Visualizzatore di tracce dei servizi \(SvcTraceViewer.exe\)](../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md), è possibile modificare il servizio di inoltro creando una nuova istanza di <xref:System.ServiceModel.Channels.Message>.Tale istanza deve essere una copia del corpo del messaggio in arrivo, più tutte le intestazioni tranne quelle per le intestazioni `ActivityId` e `Action`.Nell'esempio di codice seguente viene illustrato come procedere.  
  
```  
Message outgoingMessage = Message.CreateMessage(incomingMessage.Version, incomingMessage.Headers.Action, incomingMessage.GetReaderAtBodyContents());  
  
for (int i = 0; i < incomingMessage.Headers.Count; i++)  
{  
   if (incomingMessage.Headers[i].Name.Equals("ActivityId", StringComparison.InvariantCultureIgnoreCase) ||  
incomingMessage.Headers[i].Name.Equals("Action", StringComparison.InvariantCultureIgnoreCase))  
   {  
      continue;  
    }  
    outgoingMessage.Headers.CopyHeaderFrom(incomingMessage, i);  
}  
```  
  
## Situazioni particolari di contenuto della registrazione del messaggio inaccurata  
 Nelle condizioni seguenti, i messaggi registrati potrebbero non rappresentare in modo esatto il flusso di ottetti in transito.  
  
-   Per BasicHttpBinding, le intestazioni di envelope vengono registrate per i messaggi in arrivo nello spazio dei nomi \/addressing\/none.  
  
-   Gli spazi vuoti possono essere interpretati erroneamente.  
  
-   Per i messaggi in arrivo, gli elementi vuoti possono essere rappresentati in modo diverso.Ad esempio, \<tag\>\<\>\/tag\< invece di  \>tag\/  
  
-   Quando la registrazione di PII note è disattivata per impostazione predefinita o esplicita, enableLoggingKnownPii\="true".  
  
-   È attivata la codifica per la trasformazione a UTF\-8.  
  
## Vedere anche  
 [Strumento Visualizzatore di tracce dei servizi \(SvcTraceViewer.exe\)](../../../../docs/framework/wcf/service-trace-viewer-tool-svctraceviewer-exe.md)   
 [Utilizzo di Service Trace Viewer per la visualizzazione di tracce correlate e risoluzione dei problemi](../../../../docs/framework/wcf/diagnostics/tracing/using-service-trace-viewer-for-viewing-correlated-traces-and-troubleshooting.md)   
 [Registrazione messaggi](../../../../docs/framework/wcf/diagnostics/message-logging.md)