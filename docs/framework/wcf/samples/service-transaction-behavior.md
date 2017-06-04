---
title: "Comportamento delle transazioni di un servizio | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Esempio di comportamento delle transazioni di un servizio[Windows Communication Foundation]"
ms.assetid: 1a9842a3-e84d-427c-b6ac-6999cbbc2612
caps.latest.revision: 28
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 28
---
# Comportamento delle transazioni di un servizio
In questo esempio vengono illustrati l'uso di una transazione coordinata dal client e le impostazioni di ServiceBehaviorAttribute e OperationBehaviorAttribute per controllare il comportamento delle transazioni di un servizio.Questo esempio è basato su [Guida introduttiva](../../../../docs/framework/wcf/samples/getting-started-sample.md) che implementa un servizio calcolatrice, ma è esteso per gestire un registro sul server delle operazioni eseguite in una tabella di database e un totale parziale con stato per le operazioni della calcolatrice.Le scritture rese permanenti nella tabella del registro sul server dipendono dal risultato di una transazione coordinata dal client: se la transazione client non viene completata, la transazione del servizio Web assicura che non venga eseguito il commit degli aggiornamenti al database.  
  
> [!NOTE]
>  La procedura di installazione e le istruzioni di compilazione per questo esempio si trovano alla fine dell'argomento.  
  
 Nel contratto per il servizio è definito che per tutte le operazioni è necessario che una transazione venga propagata con le richieste:  
  
```  
[ServiceContract(Namespace = "http://Microsoft.ServiceModel.Samples",  
                    SessionMode = SessionMode.Required)]  
public interface ICalculator  
{  
    [OperationContract]  
    [TransactionFlow(TransactionFlowOption.Mandatory)]  
    double Add(double n);  
    [OperationContract]  
    [TransactionFlow(TransactionFlowOption.Mandatory)]  
    double Subtract(double n);  
    [OperationContract]  
    [TransactionFlow(TransactionFlowOption.Mandatory)]  
    double Multiply(double n);  
    [OperationContract]  
    [TransactionFlow(TransactionFlowOption.Mandatory)]  
    double Divide(double n);  
}  
  
```  
  
 Per abilitare il flusso della transazione in ingresso, il servizio viene configurato con l'wsHttpBinding fornito dal sistema con l'attributo TransactionFlow impostato su `true`.Questa associazione utilizza il protocollo WSAtomicTransactionOctober2004 interoperativo:  
  
```  
<bindings>  
  <wsHttpBinding>  
    <binding name="transactionalBinding" transactionFlow="true" />  
  </wsHttpBinding>  
</bindings>  
  
```  
  
 Dopo aver iniziato una connessione al servizio e a una transazione, il client accede a numerose operazioni del servizio all'interno dell'ambito di tale transazione e quindi completa la transazione e chiude la connessione:  
  
```  
// Create a client  
CalculatorClient client = new CalculatorClient();  
  
// Create a transaction scope with the default isolation level of Serializable  
using (TransactionScope tx = new TransactionScope())  
{  
    Console.WriteLine("Starting transaction");  
  
    // Call the Add service operation.  
    double value = 100.00D;  
    Console.WriteLine("  Adding {0}, running total={1}",  
                                        value, client.Add(value));  
  
    // Call the Subtract service operation.  
    value = 45.00D;  
    Console.WriteLine("  Subtracting {0}, running total={1}",  
                                        value, client.Subtract(value));  
  
    // Call the Multiply service operation.  
    value = 9.00D;  
    Console.WriteLine("  Multiplying by {0}, running total={1}",  
                                        value, client.Multiply(value));  
  
    // Call the Divide service operation.  
    value = 15.00D;  
    Console.WriteLine("  Dividing by {0}, running total={1}",  
                                        value, client.Divide(value));  
  
    Console.WriteLine("  Completing transaction");  
    tx.Complete();  
}  
  
Console.WriteLine("Transaction committed");  
  
// Closing the client gracefully closes the connection and cleans up resources  
client.Close();  
```  
  
 Nel servizio sono presenti tre attribuiti che influiscono sul comportamento delle transazioni del servizio nelle modalità seguenti:  
  
-   Per `ServiceBehaviorAttribute`:  
  
    -   La proprietà `TransactionTimeout` specifica il periodo di timeout entro il quale una transazione deve essere completata.In questo esempio è impostato su 30 secondi.  
  
    -   La proprietà `TransactionIsolationLevel` specifica il livello di isolamento della transazione supportato dal servizio.Questo valore deve corrispondere al livello di isolamento del client.  
  
    -   La proprietà `ReleaseServiceInstanceOnTransactionComplete` specifica se l'istanza del servizio sottostante viene riciclata al completamento di una transazione.Impostando questa proprietà su `false`, il servizio gestisce la stessa istanza del servizio tra varie richieste di operazione.Questo aspetto è necessario per gestire il totale parziale.Se la proprietà è impostata su `true`, viene generata una nuova istanza dopo ogni azione completata.  
  
    -   La proprietà `TransactionAutoCompleteOnSessionClose` specifica se alla chiusura della sessione corrente vengono completate le transazioni in attesa.Impostando questa proprietà su `false`, le singole operazioni devono impostare la proprietà `OperationBehaviorAttribute``TransactionAutoComplete` su `true` o richiedere in modo esplicito una chiamata al metodo `SetTransactionComplete` per completare transazioni.Nell'esempio vengono illustrati entrambi gli approcci.  
  
-   Per `ServiceContractAttribute`:  
  
    -   La proprietà `SessionMode` specifica se il servizio correla le richieste appropriate in una sessione logica.Poiché questo servizio include operazioni in cui la proprietà OperationBehaviorAttribute TransactionAutoComplete è impostata su `false` \(Multiply e Divide\), è necessario specificare `SessionMode.Required`.Ad esempio, l'operazione Multiply non completa la relativa transazione e si basa su una chiamata successiva a Divide completarla utilizzando il metodo `SetTransactionComplete`; il servizio deve essere in grado di determinare che queste operazioni sono in esecuzione all'interno della stessa sessione.  
  
-   Per `OperationBehaviorAttribute`:  
  
    -   La proprietà `TransactionScopeRequired` specifica se le azioni dell'operazione devono essere eseguite all'interno di un ambito della transazione.È impostata su `true` per tutte le operazioni in questo esempio e, poiché il client propaga la relativa transazione a tutte le operazioni, le azioni si verificano all'interno dell'ambito di tale transazione del client.  
  
    -   La proprietà `TransactionAutoComplete` specifica la transazione in cui viene eseguito il metodo viene completata automaticamente se non si verificano eccezioni non gestite.Come descritto in precedenza, questa proprietà è impostata su `true` per le operazioni Add e Subtract, e su `false` per le operazioni Multiply e Divide.Le operazioni Add e Subtract completano automaticamente le azioni, mentre Divide completa le azioni tramite una chiamata esplicita al metodo `SetTransactionComplete`. Multiply non completa le azioni, bensì si basa necessariamente su una chiamata successiva, ad esempio a Divide, per completare le azioni.  
  
 L'implementazione del servizio con gli attributi è illustrata di seguito:  
  
```  
[ServiceBehavior(  
    TransactionIsolationLevel = System.Transactions.IsolationLevel.Serializable,  
    TransactionTimeout = "00:00:30",  
    ReleaseServiceInstanceOnTransactionComplete = false,  
    TransactionAutoCompleteOnSessionClose = false)]  
public class CalculatorService : ICalculator  
{  
    double runningTotal;  
  
    public CalculatorService()  
    {  
        Console.WriteLine("Creating new service instance...");  
    }  
  
    [OperationBehavior(TransactionScopeRequired = true, TransactionAutoComplete = true)]  
    public double Add(double n)  
    {  
        RecordToLog(String.Format(CultureInfo.CurrentCulture, "Adding {0} to {1}", n, runningTotal));  
        runningTotal = runningTotal + n;  
        return runningTotal;  
    }  
  
    [OperationBehavior(TransactionScopeRequired = true, TransactionAutoComplete = true)]  
    public double Subtract(double n)  
    {  
        RecordToLog(String.Format(CultureInfo.CurrentCulture, "Subtracting {0} from {1}", n, runningTotal));  
        runningTotal = runningTotal - n;  
        return runningTotal;  
    }  
  
    [OperationBehavior(TransactionScopeRequired = true, TransactionAutoComplete = false)]  
    public double Multiply(double n)  
    {  
        RecordToLog(String.Format(CultureInfo.CurrentCulture, "Multiplying {0} by {1}", runningTotal, n));  
        runningTotal = runningTotal * n;  
        return runningTotal;  
    }  
  
    [OperationBehavior(TransactionScopeRequired = true, TransactionAutoComplete = false)]  
    public double Divide(double n)  
    {  
        RecordToLog(String.Format(CultureInfo.CurrentCulture, "Dividing {0} by {1}", runningTotal, n));  
        runningTotal = runningTotal / n;  
        OperationContext.Current.SetTransactionComplete();  
        return runningTotal;  
    }  
  
    // Logging method ommitted for brevity  
}   
```  
  
 Quando si esegue l'esempio, le richieste e le risposte dell'operazione vengono visualizzate nella finestra della console client.Premere INVIO nella finestra del client per arrestare il client.  
  
```  
Starting transaction  
Performing calculations...  
  Adding 100, running total=100  
  Subtracting 45, running total=55  
  Multiplying by 9, running total=495  
  Dividing by 15, running total=33  
  Completing transaction  
Transaction committed  
Press <ENTER> to terminate client.  
```  
  
 La registrazione delle richieste di operazione del servizio viene visualizzata nella finestra della console del servizio.Premere INVIO nella finestra del client per arrestare il client.  
  
```  
Press <ENTER> to terminate service.  
Creating new service instance...  
  Writing row 1 to database: Adding 100 to 0  
  Writing row 2 to database: Subtracting 45 from 100  
  Writing row 3 to database: Multiplying 55 by 9  
  Writing row 4 to database: Dividing 495 by 15  
```  
  
 Si noti che, oltre a gestire il totale parziale dei calcoli, il servizio segnala la creazione di istanze \(un'istanza per questo esempio\) e registra le richieste di operazione in un database.Poiché tutte le richieste vengono propagate alla transazione del client, qualsiasi errore nel completamento della transazione comporta il rollback di tutte le operazioni del database.Questa situazione può essere dimostrata in vari modi:  
  
-   Commentare la chiamata del client a `tx.Complete`\(\) ed eseguirla di nuovo; questo comporta l'uscita del client dall'ambito della transazione senza completare la transazione.  
  
-   Commentare la chiamata all'operazione del servizio Divide; questo impedisce il completamento dell'azione iniziata dall'operazione Multiply e, di conseguenza, della transazione del client.  
  
-   Generare un'eccezione non gestita in un punto qualsiasi dell'ambito della transazione del client; anche questa operazione impedisce al client di completare la transazione.  
  
 Il risultato di queste proceduta è che non viene eseguito il commit di nessuna delle operazioni eseguite all'interno di tale ambito e il conteggio delle righe reso persistente nel database non viene incrementato.  
  
> [!NOTE]
>  Nell'ambito del processo di compilazione, il file di database viene copiato nella cartella bin.È necessario esaminare tale copia del file di database per osservare le righe persistenti nel registro anziché il file incluso nel progetto di Visual Studio.  
  
### Per impostare, compilare ed eseguire l'esempio  
  
1.  Verificare di avere installato SQL Server 2005 Express Edition o SQL Server 2005.Nel file App.config del servizio, può essere impostato il database `connectionString` oppure le interazioni del database possono essere disabilitate impostando il valore `usingSql` di appSettings su `false`.  
  
2.  Per compilare l'edizione in C\# o Visual Basic .NET della soluzione, seguire le istruzioni in [Generazione degli esempi Windows Communication Foundation](../../../../docs/framework/wcf/samples/building-the-samples.md).  
  
3.  Per eseguire l'esempio su una configurazione con un solo computer o tra computer diversi, seguire le istruzioni in [Esecuzione degli esempi di Windows Communication Foundation](../../../../docs/framework/wcf/samples/running-the-samples.md).  
  
 Se si esegue l'esempio tra diversi computer, è necessario configurare Microsoft Distributed Transaction Coordinator \(MSDTC\) per abilitare il flusso di transazioni nella rete e utilizzare lo strumento WsatConfig.exe per abilitare il supporto in rete delle transazioni [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].  
  
### Per configurare Microsoft Distributed Transaction Coordinator \(MSDTC\) allo scopo di supportare l'esecuzione dell'esempio tra diversi computer  
  
1.  Nel computer del servizio configurare MSDTC per consentire le transazioni di rete in ingresso.  
  
    1.  Dal menu **Start**, selezionare **Pannello di controllo**, quindi **Strumenti di amministrazione** e infine **Servizi componenti**.  
  
    2.  Fare clic con il pulsante destro del mouse su **Risorse del computer** e scegliere **Proprietà**.  
  
    3.  Nella scheda **MSDTC** fare clic su **Configurazione di sicurezza**.  
  
    4.  Selezionare **Accesso di rete DTC** e **Consenti connessioni in ingresso**.  
  
    5.  Fare clic su **Sì** per riavviare il servizio MS DTC e quindi fare clic su **OK**.  
  
    6.  Fare clic su **OK** per chiudere la finestra di dialogo.  
  
2.  Nel computer del servizio e nel computer client configurare Windows Firewall per includere Microsoft Distributed Transaction Coordinator \(MSDTC\) nell'elenco delle applicazioni accettate:  
  
    1.  Eseguire l'applicazione Windows Firewall dal Pannello di controllo.  
  
    2.  Scegliere **Aggiungi programma** nella scheda **Eccezioni**.  
  
    3.  Passare alla cartella C:\\WINDOWS\\System32.  
  
    4.  Selezionare Msdtc.exe e scegliere **Apri**.  
  
    5.  Scegliere **OK** per chiudere la finestra di dialogo **Aggiungi programma** e di nuovo **OK** per chiudere l'applet Windows Firewall.  
  
3.  Nel computer client configurare MSDTC per consentire le transazioni di rete in uscita.  
  
    1.  Dal menu **Start**, selezionare **Pannello di controllo**, quindi **Strumenti di amministrazione** e infine **Servizi componenti**.  
  
    2.  Fare clic con il pulsante destro del mouse su **Risorse del computer** e scegliere **Proprietà**.  
  
    3.  Nella scheda **MSDTC** fare clic su **Configurazione di sicurezza**.  
  
    4.  Selezionare **Accesso di rete DTC** e **Consenti connessioni in uscita**.  
  
    5.  Fare clic su **Sì** per riavviare il servizio MS DTC e quindi fare clic su **OK**.  
  
    6.  Fare clic su **OK** per chiudere la finestra di dialogo.  
  
> [!IMPORTANT]
>  È possibile che gli esempi siano già installati nel computer.Verificare la directory seguente \(impostazione predefinita\) prima di continuare.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples`  
>   
>  Se questa directory non esiste, andare alla sezione relativa agli [esempi di Windows Communication Foundation \(WCF\) e Windows Workflow Foundation \(WF\) per .NET Framework 4](http://go.microsoft.com/fwlink/?LinkId=150780) per scaricare tutti gli esempi [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] e [!INCLUDE[wf1](../../../../includes/wf1-md.md)].Questo esempio si trova nella directory seguente.  
>   
>  `<UnitàInstallazione>:\WF_WCF_Samples\WCF\Basic\Services\Behaviors\Transactions`  
  
## Vedere anche