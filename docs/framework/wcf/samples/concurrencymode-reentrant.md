---
title: "ConcurrencyMode.Reentrant | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b2046c38-53d8-4a6c-a084-d6c7091d92b1
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# ConcurrencyMode.Reentrant
In questo esempio vengono descritte la necessità e le implicazioni dell'utilizzo di ConcurrencyMode.Reentrant in un'implementazione del servizio.ConcurrencyMode.Reentrant implica che il servizio \(o callback\) elabora solo uno messaggio a un'ora specificata \(come per `ConcurencyMode.Single`\).Per garantire la sicurezza dei thread, [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] evita che `InstanceContext` elabori un messaggio, in modo che nessun altro messaggio possa essere elaborato.Nel caso della modalità Reentrant, `InstanceContext` viene sbloccato poco prima che il servizio effettui una chiamata in uscita, consentendo alla chiamata successiva \(che può essere rientrante, come illustrato nell'esempio\) di eseguire il blocco la prossima volta che entra nel servizio.Per descrivere il comportamento, nell'esempio viene illustrato come un client e un servizio possono inviarsi messaggi utilizzando un contratto duplex.  
  
 Il contratto definito è un contratto duplex con il metodo `Ping` implementato dal servizio e il metodo di callback `Pong` implementato dal client.Un client richiama il metodo `Ping` del server con un conteggio di tick, avviando così la chiamata.Il servizio verifica se il conteggio di tick non è uguale a 0 e richiama quindi il metodo `Pong` del callback,  mentre esegue il decremento del conteggio di tick.Questa operazione viene eseguita nell'esempio di codice seguente:  
  
```  
  
public void Ping(int ticks)  
{  
     Console.WriteLine("Ping: Ticks = " + ticks);  
     //Keep pinging back and forth till Ticks reaches 0.  
     if (ticks != 0)  
     {  
         OperationContext.Current.GetCallbackChannel<IPingPongCallback>().Pong((ticks - 1));  
     }  
}  
  
```  
  
 L'implementazione `Pong` del callback è dotata della stessa logica dell'implementazione `Ping`.Ovvero, controlla se il conteggio non è zero, quindi richiama il metodo `Ping` sul canale di callback \(in questo caso il canale utilizzato per inviare il messaggio `Ping` originale\) con il conteggio decrementato di 1.Nel momento in cui il conteggio raggiunge lo zero, il metodo viene completato, annullando così il wrapping di tutte le risposte fino alla prima chiamata effettuata dal client che ha avviato la chiamata.Questa operazione viene illustrata nell'implementazione del callback.  
  
```  
  
public void Pong(int ticks)  
{  
    Console.WriteLine("Pong: Ticks = " + ticks);  
    if (ticks != 0)  
    {  
        //Retrieve the Callback  Channel (in this case the Channel which was used to send the  
        //original message) and make an outgoing call until ticks reaches 0.  
        IPingPong channel = OperationContext.Current.GetCallbackChannel<IPingPong>();  
        channel.Ping((ticks - 1));  
    }  
}  
  
```  
  
 Entrambi i metodi `Ping` e `Pong` sono di tipo request\/reply, il che significa che la prima chiamata a `Ping` non viene restituita finché non viene restituita la chiamata a `CallbackChannel<T>.Pong()`.Nel client, il metodo `Pong` non può essere completato finché non viene restituita la chiamata `Ping` successiva.Poiché il callback e il servizio devono eseguire chiamate in uscita di tipo request\/reply prima che possano rispondere alla richiesta in sospeso, entrambi le implementazioni devono essere contrassegnate dal comportamento ConcurrencyMode.Reentrant.  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Assicurarsi di aver eseguito la [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare l'edizione in C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Per eseguire l'esempio su una configurazione con un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
## Dimostrazione  
 Per eseguire l'esempio, compilare i progetti del client e del server.Aprire quindi due finestre di comando e impostare le directory su \\CS\\Service\\bin\\debug \<di esempio\> e \\CS\\Client\\bin\\debug \<di esempio\>.Avviare il servizio digitando `service.exe` e richiamare quindi Client.exe con il valore iniziale di tick passato come argomento di input.Viene illustrato un esempio di output per tick.  
  
```  
  
Prompt>Service.exe  
ServiceHost Started. Press Enter to terminate service.  
Ping: Ticks = 10  
Ping: Ticks = 8  
Ping: Ticks = 6  
Ping: Ticks = 4  
Ping: Ticks = 2  
Ping: Ticks = 0  
  
Prompt>Client.exe 10  
Pong: Ticks = 9  
Pong: Ticks = 7  
Pong: Ticks = 5  
Pong: Ticks = 3  
Pong: Ticks = 1  
  
```  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Services\Reentrant`  
  
## Vedere anche