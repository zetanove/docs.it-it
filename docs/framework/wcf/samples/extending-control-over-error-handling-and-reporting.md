---
title: "Estensione del controllo sulla gestione e sulla segnalazione degli errori | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 45f996a7-fa00-45cb-9d6f-b368f5778aaa
caps.latest.revision: 28
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 28
---
# Estensione del controllo sulla gestione e sulla segnalazione degli errori
In questo esempio viene illustrato come estendere il controllo sulla gestione e sulla segnalazione degli errori in un servizio [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] utilizzando l'interfaccia <xref:System.ServiceModel.Dispatcher.IErrorHandler>.L'esempio è basato su [Guida introduttiva](../../../../docs/framework/wcf/samples/getting-started-sample.md), con ulteriore codice aggiunto al servizio per gestire gli errori.Il client forza diverse condizioni di errore.Il servizio intercetta gli errori e li registra in un file.  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine dell'argomento.  
  
 I servizi possono intercettare gli errori, eseguire l'elaborazione e influire sulla segnalazione degli errori utilizzando l'interfaccia <xref:System.ServiceModel.Dispatcher.IErrorHandler>.L'interfaccia dispone di due metodi che possono essere implementati: <xref:System.ServiceModel.Dispatcher.IErrorHandler.ProvideFault%28System.Exception%2CSystem.ServiceModel.Channels.MessageVersion%2CSystem.ServiceModel.Channels.Message%40%29> e <xref:System.ServiceModel.Dispatcher.IErrorHandler.HandleError%2A>.Il metodo <xref:System.ServiceModel.Dispatcher.IErrorHandler.ProvideFault%28System.Exception%2CSystem.ServiceModel.Channels.MessageVersion%2CSystem.ServiceModel.Channels.Message%40%29> consente di aggiungere, modificare o sopprimere un messaggio di errore generato in risposta a un'eccezione.Se si verifica un errore, il metodo <xref:System.ServiceModel.Dispatcher.IErrorHandler.HandleError%2A> consente l'elaborazione dell'errore e controlla se è possibile eseguire una gestione aggiuntiva degli errori.  
  
 In questo esempio, il tipo `CalculatorErrorHandler` implementa l'interfaccia <xref:System.ServiceModel.Dispatcher.IErrorHandler>.Nel  
  
 metodo <xref:System.ServiceModel.Dispatcher.IErrorHandler.HandleError%2A>, `CalculatorErrorHandler` scrive un registro dell'errore nel file di testo Error.txt in c:\\logs.Si noti che nell'esempio l'errore viene registrato e non soppresso, in modo da poter essere segnalato al client.  
  
```  
public class CalculatorErrorHandler : IErrorHandler  
{  
        // Provide a fault. The Message fault parameter can be replaced, or set to  
        // null to suppress reporting a fault.  
  
        public void ProvideFault(Exception error, MessageVersion version, ref Message fault)  
        {  
        }  
  
        // HandleError. Log an error, then allow the error to be handled as usual.  
        // Return true if the error is considered as already handled  
  
        public bool HandleError(Exception error)  
        {  
            using (TextWriter tw = File.AppendText(@"c:\logs\error.txt"))  
            {  
                if (error != null)  
                {  
                    tw.WriteLine("Exception: " + error.GetType().Name + " - " + error.Message);  
                }  
                tw.Close();  
            }  
            return true;  
        }  
    }  
```  
  
 `ErrorBehaviorAttribute` funge da meccanismo per registrare un gestore di errori con un servizio.Questo attributo accetta un solo parametro di tipo.Tale tipo deve implementare l'interfaccia <xref:System.ServiceModel.Dispatcher.IErrorHandler> e deve disporre di un costruttore pubblico vuoto.L'attributo crea quindi un'istanza di quel tipo di gestore errori e la installa nel servizio.Questa operazione viene eseguita implementando l'interfaccia <xref:System.ServiceModel.Description.IServiceBehavior> e quindi utilizzando il metodo <xref:System.ServiceModel.Description.IServiceBehavior.ApplyDispatchBehavior%2A> per aggiungere istanze del gestore errori al servizio.  
  
```  
// This attribute can be used to install a custom error handler for a service.  
public class ErrorBehaviorAttribute : Attribute, IServiceBehavior  
{  
    Type errorHandlerType;  
  
    public ErrorBehaviorAttribute(Type errorHandlerType)  
    {  
        this.errorHandlerType = errorHandlerType;  
    }  
  
    void IServiceBehavior.Validate(ServiceDescription description, ServiceHostBase serviceHostBase)  
    {  
    }  
  
    void IServiceBehavior.AddBindingParameters(ServiceDescription description, ServiceHostBase serviceHostBase, System.Collections.ObjectModel.Collection<ServiceEndpoint> endpoints, BindingParameterCollection parameters)  
    {  
    }  
  
    void IServiceBehavior.ApplyDispatchBehavior(ServiceDescription description, ServiceHostBase serviceHostBase)  
    {  
        IErrorHandler errorHandler;  
  
        try  
        {  
            errorHandler = (IErrorHandler)Activator.CreateInstance(errorHandlerType);  
        }  
        catch (MissingMethodException e)  
        {  
            throw new ArgumentException("The errorHandlerType specified in the ErrorBehaviorAttribute constructor must have a public empty constructor.", e);  
        }  
        catch (InvalidCastException e)  
        {  
            throw new ArgumentException("The errorHandlerType specified in the ErrorBehaviorAttribute constructor must implement System.ServiceModel.Dispatcher.IErrorHandler.", e);  
        }  
  
        foreach (ChannelDispatcherBase channelDispatcherBase in serviceHostBase.ChannelDispatchers)  
        {  
            ChannelDispatcher channelDispatcher = channelDispatcherBase as ChannelDispatcher;  
            channelDispatcher.ErrorHandlers.Add(errorHandler);  
        }                                                  
    }  
}  
```  
  
 Nell'esempio viene implementato un servizio calcolatrice.Il client causa deliberatamente due errori nel servizio fornendo parametri con valori non validi.`CalculatorErrorHandler` utilizza l'interfaccia <xref:System.ServiceModel.Dispatcher.IErrorHandler> per registrare gli errori in un file locale e quindi consente che siano segnalati al client.Il client forza una divisione per zero e una condizione di argomento esterno all'intervallo.  
  
```  
try  
{  
    Console.WriteLine("Forcing an error in Divide");  
    // Call the Divide service operation - trigger a divide by 0 error.  
    value1 = 22;  
    value2 = 0;  
    result = proxy.Divide(value1, value2);  
    Console.WriteLine("Divide({0},{1}) = {2}", value1, value2, result);  
}  
catch (FaultException e)  
{  
    Console.WriteLine("FaultException: " + e.GetType().Name + " - " + e.Message);  
}  
catch (Exception e)  
{  
    Console.WriteLine("Exception: " + e.GetType().Name + " - " + e.Message);  
}  
```  
  
 Quando si esegue l'esempio, le richieste e le risposte dell'operazione vengono visualizzate nella finestra della console client.Viene visualizzata la divisione per zero e le condizioni di argomento esterno all'intervallo segnalate come errori.Premere INVIO nella finestra del client per arrestare il client.  
  
```  
Add(15,3) = 18  
Subtract(145,76) = 69  
Multiply(9,81) = 729  
Forcing an error in Divide  
FaultException: FaultException - Invalid Argument: The second argument must not be zero.  
Forcing an error in Factorial  
FaultException: FaultException - Invalid Argument: The argument must be greater than zero.  
  
Press <ENTER> to terminate client.  
```  
  
 Il file c:\\logs\\errors.txt contiene le informazioni registrate sugli errori dal servizio.Si noti che affinché il servizio scriva nella directory è necessario assicurarsi che il processo in cui è in esecuzione il servizio \(in genere ASP.NET o servizio di rete\) disponga delle autorizzazioni per scrivere nella directory.  
  
```  
Fault: Reason = Invalid Argument: The second argument must not be zero.  
Fault: Reason = Invalid Argument: The argument must be greater than zero.  
```  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Verificare di avere eseguito [Procedura di installazione singola per gli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/one-time-setup-procedure-for-the-wcf-samples.md).  
  
2.  Per compilare la soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Assicurarsi di aver creato la directory c:\\logs per il file error.txt.In alternativa, modificare il nome file utilizzato in `CalculatorErrorHandler.HandleError`.  
  
4.  Per eseguire l'esempio in una configurazione con un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Extensibility\ErrorHandling`  
  
## Vedere anche