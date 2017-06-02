---
title: "Propagazione di transazioni all&#39;interno e all&#39;esterno di servizi flusso di lavoro | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 03ced70e-b540-4dd9-86c8-87f7bd61f609
caps.latest.revision: 11
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 11
---
# Propagazione di transazioni all&#39;interno e all&#39;esterno di servizi flusso di lavoro
Servizi e client del flusso di lavoro possono partecipare alle transazioni.Affinché un'operazione del servizio diventi parte di una transazione di ambiente, posizionare un'attività <xref:System.ServiceModel.Activities.Receive> all'interno di un'attività <xref:System.ServiceModel.Activities.TransactedReceiveScope>.Qualsiasi chiamata effettuata da un'attività <xref:System.ServiceModel.Activities.Send> o un'attività <xref:System.ServiceModel.Activities.SendReply> all'interno di <xref:System.ServiceModel.Activities.TransactedReceiveScope> verrà effettuata anche all'interno della transazione di ambiente.Un'applicazione client del flusso di lavoro può creare una transazione di ambiente tramite l'attività <xref:System.Activities.Statements.TransactionScope> e chiamare operazioni del servizio utilizzando la transazione di ambiente.In questo argomento viene illustrato il processo di creazione di un servizio flusso di lavoro e di un client flusso di lavoro che partecipano a transazioni.  
  
> [!WARNING]
>  Se un'istanza del servizio flusso di lavoro viene caricata all'interno di una transazione e il flusso di lavoro contiene un'attività <xref:System.Activities.Statements.Persist>, l'istanza del flusso di lavoro verrà interrotta finché non si verifica il timeout della transazione.  
  
> [!IMPORTANT]
>  Ogni volta che si utilizza un oggetto <xref:System.ServiceModel.Activities.TransactedReceiveScope>, è consigliabile posizionare tutte le attività Receive del flusso di lavoro all'interno delle attività <xref:System.ServiceModel.Activities.TransactedReceiveScope>.  
  
> [!IMPORTANT]
>  Quando si utilizza l'oggetto <xref:System.ServiceModel.Activities.TransactedReceiveScope> e i messaggi arrivano nell'ordine non corretto, il flusso di lavoro verrà interrotto quando si tenterà di consegnare il primo messaggio nell'ordine non corretto.È necessario assicurarsi che il flusso di lavoro sia sempre in corrispondenza di un punto di interruzione coerente quando il flusso di lavoro è inattivo.In questo modo sarà possibile riavviare il flusso di lavoro da un punto di persistenza precedente se il flusso di lavoro viene interrotto.  
  
### Creare una libreria condivisa  
  
1.  Creare una nuova soluzione Visual Studio vuota.  
  
2.  Aggiungere un nuovo progetto della libreria di classi denominato `Common`.Aggiungere riferimenti agli assembly indicati di seguito:  
  
    -   System.Activities.dll  
  
    -   System.ServiceModel.dll  
  
    -   System.ServiceModel.Activities.dll  
  
    -   System.Transactions.dll  
  
3.  Aggiungere una nuova classe denominata `PrintTransactionInfo` al progetto `Common`.Questa classe è derivata da <xref:System.Activities.NativeActivity> ed esegue l'overload del metodo <xref:System.Activities.NativeActivity.Execute%2A>.  
  
    ```  
    using System;  
    using System;  
    using System.Activities;  
    using System.Transactions;  
  
    namespace Common  
    {  
        public class PrintTransactionInfo : NativeActivity  
        {  
            protected override void Execute(NativeActivityContext context)  
            {  
                RuntimeTransactionHandle rth = context.Properties.Find(typeof(RuntimeTransactionHandle).FullName) as RuntimeTransactionHandle;  
  
                if (rth == null)  
                {  
                    Console.WriteLine("There is no ambient RuntimeTransactionHandle");  
                }  
  
                Transaction t = rth.GetCurrentTransaction(context);  
  
                if (t == null)  
                {  
                    Console.WriteLine("There is no ambient transaction");  
                }  
                else  
                {  
                    Console.WriteLine("Transaction: {0} is {1}", t.TransactionInformation.DistributedIdentifier, t.TransactionInformation.Status);  
                }  
            }  
        }  
  
    }  
  
    ```  
  
     Si tratta di un'attività nativa che visualizza informazioni sulla transazione di ambiente e viene utilizzata sia nei flussi di lavoro del servizio che del client utilizzati nel presente argomento.Compilare la soluzione per rendere disponibile questa attività nella sezione **Common** della **Casella degli strumenti**.  
  
### Implementare il servizio flusso di lavoro  
  
1.  Aggiungere un nuovo servizio flusso di lavoro [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], denominato `WorkflowService`, al progetto `Common`.A tale scopo, fare clic con il pulsante destro del mouse sul progetto `Common`, selezionare **Aggiungi**, **Nuovo elemento...**, quindi selezionare **Flusso di lavoro** in **Modelli installati** e infine selezionare **Servizio flusso di lavoro WCF**.  
  
     ![Aggiunta di un servizio flusso di lavoro](../../../../docs/framework/wcf/feature-details/media/addwfservice.JPG "AddWFService")  
  
2.  Eliminare le attività `ReceiveRequest` e `SendResponse` predefinite.  
  
3.  Trascinare un'attività <xref:System.Activities.Statements.WriteLine> nell'attività `Sequential Service`.Impostare la proprietà Text su `"Workflow Service starting ..."` come illustrato nell'esempio seguente.  
  
     ![Aggiunta di un'attività WriteLine](../../../../docs/framework/wcf/feature-details/media/addwriteline.JPG "AddWriteLine")  
  
4.  Trascinare un'attività <xref:System.ServiceModel.Activities.TransactedReceiveScope> dopo l'attività <xref:System.Activities.Statements.WriteLine>.L'attività <xref:System.ServiceModel.Activities.TransactedReceiveScope> può essere individuata nella sezione **Messaggi** della **Casella degli strumenti**.L'attività <xref:System.ServiceModel.Activities.TransactedReceiveScope> è costituita da due sezioni, **Richiesta** e **Corpo**.La sezione **Richiesta** contiene l'attività <xref:System.ServiceModel.Activities.Receive>.La sezione **Corpo** contiene le attività da eseguire all'interno di una transazione dopo la ricezione di un messaggio.  
  
     ![Aggiunta di un'attività TransactedReceiveScope](../../../../docs/framework/wcf/feature-details/media/trs.JPG "TRS")  
  
5.  Selezionare l'attività <xref:System.ServiceModel.Activities.TransactedReceiveScope> e fare clic sul pulsante **Variabili**.Aggiungere le variabili seguenti.  
  
     ![Aggiunta di variabili a TransactedReceiveScope](../../../../docs/framework/wcf/feature-details/media/trsvariables.JPG "TRSVariables")  
  
    > [!NOTE]
    >  È possibile eliminare la variabile relativa ai dati, presente per impostazione predefinita.È possibile utilizzare anche la variabile dell'handle esistente.  
  
6.  Trascinare un'attività <xref:System.ServiceModel.Activities.Receive> all'interno della sezione **Richiesta** dell'attività <xref:System.ServiceModel.Activities.TransactedReceiveScope>.Impostare le proprietà seguenti:  
  
    |Proprietà|Valore|  
    |---------------|------------|  
    |CanCreateInstance|True \(controllare la casella di controllo\)|  
    |OperationName|StartSample|  
    |ServiceContractName|ITransactionSample|  
  
     Il flusso di lavoro dovrebbe risultare analogo al seguente:  
  
     ![Aggiunta di un'attività Receive](../../../../docs/framework/wcf/feature-details/media/serviceaddreceive.JPG "ServiceAddReceive")  
  
7.  Fare clic sul collegamento **Definisci** nell'attività <xref:System.ServiceModel.Activities.Receive> e configurare le impostazioni seguenti:  
  
     ![Configurazione delle impostazioni del messaggio per l'attività Receive](../../../../docs/framework/wcf/feature-details/media/receivemessagesettings.JPG "ReceiveMessageSettings")  
  
8.  Trascinare un'attività <xref:System.Activities.Statements.Sequence> nella sezione Corpo di <xref:System.ServiceModel.Activities.TransactedReceiveScope>.All'interno dell'attività <xref:System.Activities.Statements.Sequence>, trascinare due attività <xref:System.Activities.Statements.WriteLine> e impostare le proprietà <xref:System.Activities.Statements.WriteLine.Text%2A> come illustrato nella tabella seguente.  
  
    |Attività|Valore|  
    |--------------|------------|  
    |WriteLine 1|“Service: Receive Completed”|  
    |WriteLine 2|"Service: Received \= " \+ requestMessage|  
  
     Il flusso di lavoro dovrebbe risultare analogo al seguente:  
  
     ![Aggiunta di attività WriteLine](../../../../docs/framework/wcf/feature-details/media/afteraddingwritelines.JPG "AfterAddingWriteLines")  
  
9. Trascinare l'attività `PrintTransactionInfo` dopo la seconda attività <xref:System.Activities.Statements.WriteLine> nella sezione **Corpo** nell'attività <xref:System.ServiceModel.Activities.TransactedReceiveScope>.  
  
     ![Dopo avere aggiunto PrintTransactionInfo](../../../../docs/framework/wcf/feature-details/media/afteraddingprinttransactioninfo.JPG "AfterAddingPrintTransactionInfo")  
  
10. Trascinare un'attività <xref:System.Activities.Statements.Assign> dopo l'attività `PrintTransactionInfo` e impostarne le proprietà in base alla tabella seguente.  
  
    |Property|Valore|  
    |--------------|------------|  
    |To|replyMessage|  
    |Valore|"Service: Sending reply".|  
  
11. Trascinare un'attività <xref:System.Activities.Statements.WriteLine> dopo l'attività <xref:System.Activities.Statements.Assign> e impostarne la proprietà <xref:System.Activities.Statements.WriteLine.Text%2A> su "Service: Begin reply".  
  
     Il flusso di lavoro dovrebbe risultare analogo al seguente:  
  
     ![Dopo avere aggiunto Assign e WriteLine](../../../../docs/framework/wcf/feature-details/media/afteraddingsbrwriteline.JPG "AfterAddingSBRWriteLine")  
  
12. Fare clic con il pulsante destro del mouse sull'attività <xref:System.ServiceModel.Activities.Receive>, selezionare **Crea SendReply** e incollarla dopo l'ultima attività <xref:System.Activities.Statements.WriteLine>.Fare clic sul collegamento **Definisci** nell'attività `SendReplyToReceive` e configurare le impostazioni seguenti.  
  
     ![Impostazioni del messaggio di risposta](../../../../docs/framework/wcf/feature-details/media/replymessagesettings.JPG "ReplyMessageSettings")  
  
13. Trascinare un'attività <xref:System.Activities.Statements.WriteLine> dopo l'attività `SendReplyToReceive` e impostarne la proprietà <xref:System.Activities.Statements.WriteLine.Text%2A> su "Service: Reply sent".  
  
14. Trascinare un'attività <xref:System.Activities.Statements.WriteLine> nella parte inferiore del flusso di lavoro e impostarne la proprietà <xref:System.Activities.Statements.WriteLine.Text%2A> su "Service: Workflow ends, press ENTER to exit".  
  
     Il flusso di lavoro del servizio completato dovrebbe risultare analogo al seguente:  
  
     ![Flusso di lavoro del servizio completato](../../../../docs/framework/wcf/feature-details/media/servicecomplete.jpg "ServiceComplete")  
  
### Implementare il client flusso di lavoro  
  
1.  Aggiungere una nuova applicazione flusso di lavoro WCF, denominata `WorkflowClient`, al progetto `Common`.A tale scopo, fare clic con il pulsante destro del mouse sul progetto `Common`, selezionare **Aggiungi**, **Nuovo elemento...**, quindi selezionare **Flusso di lavoro** in **Modelli installati** e infine selezionare **Attività**.  
  
     ![Aggiungere un progetto di attività](../../../../docs/framework/wcf/feature-details/media/addactivity.JPG "AddActivity")  
  
2.  Trascinare un'attività <xref:System.Activities.Statements.Sequence> sull'area di progettazione.  
  
3.  All'interno dell'attività <xref:System.Activities.Statements.Sequence>, trascinare un'attività <xref:System.Activities.Statements.WriteLine> e impostarne la proprietà <xref:System.Activities.Statements.WriteLine.Text%2A> su `"Client: Workflow starting"`.Il flusso di lavoro dovrebbe risultare analogo al seguente:  
  
     ![Aggiungere un'attività WriteLine](../../../../docs/framework/wcf/feature-details/media/clientaddwriteline.JPG "ClientAddWriteLine")  
  
4.  Trascinare un'attività <xref:System.Activities.Statements.TransactionScope> dopo l'attività <xref:System.Activities.Statements.WriteLine>.Selezionare l'attività <xref:System.Activities.Statements.TransactionScope>, fare clic sul pulsante Variabili e aggiungere le variabili seguenti.  
  
     ![Aggiungere variabili a TransactionScope](../../../../docs/framework/wcf/feature-details/media/tsvariables.JPG "TSVariables")  
  
5.  Trascinare un'attività <xref:System.Activities.Statements.Sequence> nel corpo dell'attività <xref:System.Activities.Statements.TransactionScope>.  
  
6.  Trascinare un'attività `PrintTransactionInfo` all'interno dell'attività <xref:System.Activities.Statements.Sequence>.  
  
7.  Trascinare un'attività <xref:System.Activities.Statements.WriteLine> dopo l'attività `PrintTransactionInfo` e impostarne la proprietà <xref:System.Activities.Statements.WriteLine.Text%2A> su "Client: Beginning Send".Il flusso di lavoro dovrebbe risultare analogo al seguente:  
  
     ![Aggiunta di attività](../../../../docs/framework/wcf/feature-details/media/clientaddcbswriteline.JPG "ClientAddCBSWriteLine")  
  
8.  Trascinare un'attività <xref:System.ServiceModel.Activities.Send> dopo l'attività <xref:System.Activities.Statements.Assign> e impostare le proprietà seguenti:  
  
    |Proprietà|Valore|  
    |---------------|------------|  
    |EndpointConfigurationName|workflowServiceEndpoint|  
    |OperationName|StartSample|  
    |ServiceContractName|ITransactionSample|  
  
     Il flusso di lavoro dovrebbe risultare analogo al seguente:  
  
     ![Impostazione delle proprietà dell'attività Send](../../../../docs/framework/wcf/feature-details/media/clientsendsettings.JPG "ClientSendSettings")  
  
9. Fare clic sul collegamento **Definisci** e configurare le impostazioni seguenti:  
  
     ![Impostazioni del messaggio dell'attività Send](../../../../docs/framework/wcf/feature-details/media/sendmessagesettings.JPG "SendMessageSettings")  
  
10. Fare clic con il pulsante destro del mouse sull'attività <xref:System.ServiceModel.Activities.Send> e selezionare **Crea ReceiveReply**.L'attività <xref:System.ServiceModel.Activities.ReceiveReply> sarà posizionata automaticamente dopo l'attività <xref:System.ServiceModel.Activities.Send>.  
  
11. Fare clic sul collegamento Definiscinell'attività ReceiveReplyForSend e configurare le impostazioni seguenti:  
  
     ![Configurazione delle impostazioni del messaggio per ReceiveForSend](../../../../docs/framework/wcf/feature-details/media/clientreplymessagesettings.JPG "ClientReplyMessageSettings")  
  
12. Trascinare un'attività <xref:System.Activities.Statements.WriteLine> tra le attività <xref:System.ServiceModel.Activities.Send> e <xref:System.ServiceModel.Activities.ReceiveReply> e impostarne la proprietà <xref:System.Activities.Statements.WriteLine.Text%2A> su "Client: Send complete".  
  
13. Trascinare un'attività <xref:System.Activities.Statements.WriteLine> dopo l'attività <xref:System.ServiceModel.Activities.ReceiveReply> e impostarne la proprietà <xref:System.Activities.Statements.WriteLine.Text%2A> su "Client side: Reply received \= " \+ replyMessage  
  
14. Trascinare un'attività `PrintTransactionInfo` dopo l'attività <xref:System.Activities.Statements.WriteLine>.  
  
15. Trascinare un'attività <xref:System.Activities.Statements.WriteLine> alla fine del flusso di lavoro e impostarne la proprietà <xref:System.Activities.Statements.WriteLine.Text%2A> su "Client workflow ends". Il flusso di lavoro client completato viene visualizzato come illustrato del diagramma seguente.  
  
     ![Flusso di lavoro del client completato](../../../../docs/framework/wcf/feature-details/media/clientcompleteworkflow.jpg "ClientCompleteWorkflow")  
  
16. Compilare la soluzione.  
  
### Creare l'applicazione di servizio  
  
1.  Aggiungere un nuovo progetto Applicazione console denominato `Service` alla soluzione.Aggiungere riferimenti agli assembly indicati di seguito:  
  
    1.  System.Activities.dll  
  
    2.  System.ServiceModel.dll  
  
    3.  System.ServiceModel.Activities.dll  
  
2.  Aprire il file Program.cs generato e il codice seguente:  
  
    ```  
    static void Main()  
          {  
              Console.WriteLine("Building the server.");  
              using (WorkflowServiceHost host = new WorkflowServiceHost(new DeclarativeServiceWorkflow(), new Uri("net.tcp://localhost:8000/TransactedReceiveService/Declarative")))  
              {                
                  //Start the server  
                  host.Open();  
                  Console.WriteLine("Service started.");  
  
                  Console.WriteLine();  
                  Console.ReadLine();  
                  //Shutdown  
                  host.Close();  
              };         
          }  
  
    ```  
  
3.  Aggiungere il file app.config seguente al progetto.  
  
    ```xml  
    <?xml version="1.0" encoding="utf-8" ?>  
    <!-- Copyright © Microsoft Corporation.  All rights reserved. -->  
    <configuration>  
        <system.serviceModel>  
            <bindings>  
                <netTcpBinding>  
                    <binding transactionFlow="true" />  
                </netTcpBinding>  
            </bindings>  
        </system.serviceModel>  
    </configuration>  
  
    ```  
  
### Creare l'applicazione client  
  
1.  Aggiungere un nuovo progetto Applicazione console denominato `Client` alla soluzione.Aggiungere un riferimento a System.Activities.dll.  
  
2.  Aprire il file program.cs e aggiungere il codice seguente.  
  
    ```  
    class Program  
        {  
  
            private static AutoResetEvent syncEvent = new AutoResetEvent(false);  
  
            static void Main(string[] args)  
            {  
                //Build client  
                Console.WriteLine("Building the client.");  
                WorkflowApplication client = new WorkflowApplication(new DeclarativeClientWorkflow());  
                client.Completed = Program.Completed;  
                client.Aborted = Program.Aborted;  
                client.OnUnhandledException = Program.OnUnhandledException;  
  
                //Wait for service to start  
                Console.WriteLine("Press ENTER once service is started.");  
                Console.ReadLine();  
  
                //Start the client              
                Console.WriteLine("Starting the client.");  
                client.Run();  
                syncEvent.WaitOne();  
  
                //Sample complete  
                Console.WriteLine();  
                Console.WriteLine("Client complete. Press ENTER to exit.");  
                Console.ReadLine();  
            }  
  
            private static void Completed(WorkflowApplicationCompletedEventArgs e)  
            {  
                Program.syncEvent.Set();  
            }  
  
            private static void Aborted(WorkflowApplicationAbortedEventArgs e)  
            {  
                Console.WriteLine("Client Aborted: {0}", e.Reason);  
                Program.syncEvent.Set();  
            }  
  
            private static UnhandledExceptionAction OnUnhandledException(WorkflowApplicationUnhandledExceptionEventArgs e)  
            {  
                Console.WriteLine("Client had an unhandled exception: {0}", e.UnhandledException);  
                return UnhandledExceptionAction.Cancel;  
            }  
        }  
  
    ```  
  
## Vedere anche  
 [Servizi flusso di lavoro](../../../../docs/framework/wcf/feature-details/workflow-services.md)   
 [Panoramica sulle transazioni di Windows Communication Foundation](../../../../docs/framework/wcf/feature-details/transactions-overview.md)   
 [Utilizzo di TransactedReceiveScope](../../../../docs/framework/windows-workflow-foundation/samples/use-of-transactedreceivescope.md)