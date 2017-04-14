---
title: "Eccezioni previste | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 299a6987-ae6b-43c6-987f-12b034b583ae
caps.latest.revision: 7
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 7
---
# Eccezioni previste
In questo esempio viene illustrato come rilevare le eccezioni previste quando si utilizza un client tipizzato.L'esempio è basato su [Guida introduttiva](../../../../docs/framework/wcf/samples/getting-started-sample.md), che implementa un servizio di calcolatrice.In questo esempio, il client è un'applicazione console \(exe\) e il servizio è ospitato da Internet Information Services \(IIS\).  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine dell'argomento.  
  
 In questo esempio viene illustrata l'intercettazione e la gestione di due tipi di eccezione previsti che devono essere gestiti da programmi specifici, ovvero `TimeoutException` e `CommunicationException`.  
  
 Le eccezioni generate dai metodi della comunicazione su un client [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] possono essere previste o impreviste.Le eccezioni impreviste includono gli errori irreversibili come `OutOfMemoryException` e gli errori di programmazione come `ArgumentNullException` o `InvalidOperationException`.Gli errori imprevisti non possono essere gestiti in modo utile, pertanto in genere non è necessario rilevarli quando si chiama un metodo di comunicazione client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
 Le eccezioni previste dai metodi di comunicazione su un client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] includono `TimeoutException`, `CommunicationException` e qualsiasi classe derivata da `CommunicationException`.Queste eccezioni indicano un problema durante la comunicazione che può essere gestita correttamente interrompendo il client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] e riportando un errore di comunicazione.Perché fattori esterni possono provocare questi errori in qualsiasi applicazione, le eccezioni devono essere rilevate da applicazioni specifiche e deve essere eseguito il ripristino quando si verificano.  
  
 Un client può generare numerose classi derivate di `CommunicationException`.In alcuni casi, le applicazioni rilevano anche alcune di queste eccezioni per una gestione speciale, ma lasciano che le altre vengano gestite come `CommunicationException`.Questo processo può essere portato a termine rilevando prima il tipo di eccezione più specifico e quindi `CommunicationException` in una clausola di rilevamento successiva.  
  
 Il codice che chiama un metodo di comunicazione client deve rilevare `TimeoutException` e `CommunicationException`.Un modo per gestire tali errori consiste nell'interrompere il client e riportare l'errore di comunicazione.  
  
```  
try  
{  
    ...  
    double result = client.Add(value1, value2);  
    ...  
    client.Close();  
}  
catch (TimeoutException exception)  
{  
    Console.WriteLine("Got {0}", exception.GetType());  
    client.Abort();  
}  
catch (CommunicationException exception)  
{  
    Console.WriteLine("Got {0}", exception.GetType());  
    client.Abort();  
}  
```  
  
 In seguito a un'eccezione prevista, il client può essere utilizzabile o non esserlo.Per determinare se il client può ancora essere utilizzato, verificare che la proprietà `State` sia impostata su `CommunicationState`.Opened.Se è aperto, può essere ancora utilizzato.In caso contrario è necessario interrompere il client e rilasciare tutti i riferimenti attinenti.  
  
> [!CAUTION]
>  È possibile osservare che i client che dispongono di una sessione spesso possono più essere utilizzati dopo un'eccezione, mentre i client privi di una sessione spesso possono ancora essere utilizzati dopo un'eccezione.Tuttavia, nessuno di questi comportamenti è garantito, pertanto se si desidera continuare a utilizzare il client dopo un'eccezione, l'applicazione dovere controllare la proprietà `State` per verificare che il client sia ancora aperto.  
  
 Quando si esegue l'esempio, le risposte e le eccezioni dell'operazione vengono visualizzate nella finestra della console client.  
  
 Il processo client esegue due scenari, ognuno dei quali tenta di chiamare `Add` seguito da `Divide`.Il primo scenario simula un problema di rete interrompendo il client prima di effettuare la chiamata a `Divide`.Il secondo scenario provoca una condizione di timeout impostando un valore di timeout troppo breve per consentire il completamento del metodo.L'output previsto dal processo client è:  
  
```  
Add(100,15.99) = 115.99  
Simulated network problem occurs...  
Got System.ServiceModel.CommunicationObjectAbortedException  
Add(100,15.99) = 115.99  
Set timeout too short for method to complete...  
Got System.TimeoutException  
```  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Verificare di avere eseguito [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare l'edizione in C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Per eseguire l'esempio in una configurazione con un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Client\ExpectedExceptions`  
  
## Vedere anche