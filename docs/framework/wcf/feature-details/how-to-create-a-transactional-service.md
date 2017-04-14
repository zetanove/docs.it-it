---
title: "Procedura: creare un servizio transazionale | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1bd2e4ed-a557-43f9-ba98-4c70cb75c154
caps.latest.revision: 12
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 12
---
# Procedura: creare un servizio transazionale
In questo esempio vengono illustrati vari aspetti della creazione di un servizio transazionale e l'utilizzo di una transazione iniziata dal client per coordinare operazioni del servizio.  
  
### Creazione di un servizio transazionale  
  
1.  Creare un contratto di servizio e annotare le operazioni con l'impostazione desiderata dall'enumerazione <xref:System.ServiceModel.TransactionFlowOption> per specificare i requisiti della transazione in ingresso.Si noti che è anche possibile inserire <xref:System.ServiceModel.TransactionFlowAttribute> nella classe di servizio implementata.Ciò consente l'utilizzo di queste impostazioni della transazione per una singola implementazione di un'interfaccia, invece che per ogni implementazione.  
  
    ```  
    [ServiceContract]  
    public interface ICalculator  
    {  
        [OperationContract]  
        // Use this to require an incoming transaction  
        [TransactionFlow(TransactionFlowOption.Mandatory)]  
        double Add(double n1, double n2);  
        [OperationContract]  
        // Use this to permit an incoming transaction  
        [TransactionFlow(TransactionFlowOption.Allowed)]  
        double Subtract(double n1, double n2);  
    }  
    ```  
  
2.  Creare una classe di implementazione e utilizzare <xref:System.ServiceModel.ServiceBehaviorAttribute> per specificare facoltativamente un <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionIsolationLevel%2A> e un <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionTimeout%2A>.Si noti che in molti casi, l'impostazione <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionTimeout%2A> predefinita di 60 secondi e l'impostazione predefinita <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionIsolationLevel%2A> di `Unspecified` sono appropriate.Per ogni operazione, è possibile utilizzare l'attributo <xref:System.ServiceModel.OperationBehaviorAttribute> per specificare se il lavoro eseguito all'interno del metodo deve verificarsi all'interno dell'ambito di una transazione in base al valore dell'attributo <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A>.In questo caso, la transazione utilizzata per il metodo `Add` corrisponde alla transazione in ingresso obbligatoria propagata dal client e la transazione utilizzata per il metodo `Subtract` corrisponde alla transazione in ingresso se ne è stata propagata una dal client, o a una nuova transazione creata implicitamente e localmente.  
  
    ```  
    [ServiceBehavior(  
        TransactionIsolationLevel = System.Transactions.IsolationLevel.Serializable,  
        TransactionTimeout = "00:00:45")]  
    public class CalculatorService : ICalculator  
    {  
        [OperationBehavior(TransactionScopeRequired = true)]  
        public double Add(double n1, double n2)  
        {  
            // Perform transactional operation  
            RecordToLog(String.Format("Adding {0} to {1}", n1, n2));  
            return n1 + n2;  
        }  
  
        [OperationBehavior(TransactionScopeRequired = true)]  
        public double Subtract(double n1, double n2)  
        {  
            // Perform transactional operation  
            RecordToLog(String.Format("Subtracting {0} from {1}", n2, n1));  
            return n1 - n2;  
        }  
  
        private static void RecordToLog(string recordText)  
        {  
            // Database operations omitted for brevity  
            // This is where the transaction provides specific benefit  
            // - changes to the database will be committed only when  
            // the transaction completes.  
        }  
    }  
    ```  
  
3.  Configurare le associazioni nel file di configurazione, specificando che il contesto della transazione deve essere propagato e i protocolli da utilizzare a tale scopo.[!INCLUDE[crdefault](../../../../includes/crdefault-md.md)][Configurazione delle transazioni ServiceModel](../../../../docs/framework/wcf/feature-details/servicemodel-transaction-configuration.md).In particolare, il tipo di associazione è specificato nell'attributo `binding` dell'elemento endpoint.L'elemento [\<endpoint\>](http://msdn.microsoft.com/it-it/13aa23b7-2f08-4add-8dbf-a99f8127c017) contiene un attributo `bindingConfiguration` che fa riferimento a una configurazione dell'associazione denominata `transactionalOleTransactionsTcpBinding`, come illustrato nella configurazione di esempio seguente.  
  
    ```  
    <service name="CalculatorService">  
      <endpoint address="net.tcp://localhost:8008/CalcService"  
        binding="netTcpBinding"  
        bindingConfiguration="transactionalOleTransactionsTcpBinding"  
        contract="ICalculator"  
        name="OleTransactions_endpoint" />  
    </service>  
    ```  
  
     Il flusso delle transazioni viene attivato a livello di configurazione utilizzando l'attributo `transactionFlow` e il protocollo della transazione viene specificato utilizzando l'attributo `transactionProtocol`, come illustrato nella configurazione seguente.  
  
    ```  
    <bindings>  
      <netTcpBinding>  
        <binding name="transactionalOleTransactionsTcpBinding"  
          transactionFlow="true"  
          transactionProtocol="OleTransactions"/>  
      </netTcpBinding>  
    </bindings>  
    ```  
  
### Supporto di più protocolli di transazione  
  
1.  Per ottimizzare le prestazioni, è necessario utilizzare il protocollo OleTransactions per scenari che interessano un client e un servizio scritto utilizzando [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)].Il protocollo WS\-AtomicTransaction \(WS\-AT\), tuttavia, è utile per scenari in cui è richiesta l'interoperabilità con stack del protocollo di terze parti.È possibile configurare servizi [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] per accettare entrambi protocolli fornendo più endpoint con le associazioni appropriate specifiche del protocollo, come illustrato nell'esempio di configurazione seguente.  
  
    ```  
    <service name="CalculatorService">  
      <endpoint address="http://localhost:8000/CalcService"  
        binding="wsHttpBinding"  
        bindingConfiguration="transactionalWsatHttpBinding"  
        contract="ICalculator"  
        name="WSAtomicTransaction_endpoint" />  
      <endpoint address="net.tcp://localhost:8008/CalcService"  
        binding="netTcpBinding"  
        bindingConfiguration="transactionalOleTransactionsTcpBinding"  
        contract="ICalculator"  
        name="OleTransactions_endpoint" />  
    </service>  
    ```  
  
     Il protocollo di transazione viene specificato utilizzando l'attributo `transactionProtocol`.Questo attributo è tuttavia assente dal `wsHttpBinding` fornito dal sistema perché questa associazione può utilizzare solo il protocollo WS\-AT.  
  
    ```  
    <bindings>  
      <wsHttpBinding>  
        <binding name="transactionalWsatHttpBinding"  
          transactionFlow="true" />  
      </wsHttpBinding>  
      <netTcpBinding>  
        <binding name="transactionalOleTransactionsTcpBinding"  
          transactionFlow="true"  
          transactionProtocol="OleTransactions"/>  
      </netTcpBinding>  
    </bindings>  
    ```  
  
### Controllo del completamento di una transazione  
  
1.  Per impostazione predefinita, le operazioni [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] completano automaticamente le transazioni, se non viene generata nessuna eccezione non gestita.È possibile modificare questo comportamento utilizzando la proprietà <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionAutoComplete%2A> e il metodo <xref:System.ServiceModel.OperationContext.SetTransactionComplete%2A>.Quando è necessario che un'operazione si verifichi all'interno della stessa transazione di un'altra operazione \(ad esempio, un'operazione di addebito e di accredito\), è possibile disattivare il comportamento di completamento automatico impostando la proprietà <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionAutoComplete%2A> su `false`, come illustrato nell'esempio dell'operazione `Debit` seguente.La transazione utilizzata dall'operazione `Debit` non viene completata finché non viene chiamato un metodo con la proprietà <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionAutoComplete%2A> impostata su `true`, come illustrato nell'operazione `Credit1` o finché non viene chiamato il metodo <xref:System.ServiceModel.OperationContext.SetTransactionComplete%2A> per contrassegnare in modo esplicito la transazione come completata, come illustrato nell'operazione `Credit2`.Si noti che le due operazioni di accredito sono riportate a solo scopo illustrativo e che una singola operazione sarebbe più tipica.  
  
    ```  
    [ServiceBehavior]  
    public class CalculatorService : IAccount  
    {  
        [OperationBehavior(  
            TransactionScopeRequired = true, TransactionAutoComplete = false)]  
        public void Debit(double n)  
        {  
            // Perform debit operation  
  
            return;  
        }  
  
        [OperationBehavior(  
            TransactionScopeRequired = true, TransactionAutoComplete = true)]  
        public void Credit1(double n)  
        {  
            // Perform credit operation  
  
            return;  
        }  
  
        [OperationBehavior(  
            TransactionScopeRequired = true, TransactionAutoComplete = false)]  
        public void Credit2(double n)  
        {  
            // Perform alternate credit operation  
  
            OperationContext.Current.SetTransactionComplete();  
            return;  
        }  
    }  
    ```  
  
2.  Ai fini della correlazione delle transazioni, per impostare la proprietà <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionAutoComplete%2A> su `false` è richiesto l'utilizzo di un'associazione con sessione.Questo requisito è specificato con la proprietà `SessionMode` in <xref:System.ServiceModel.ServiceContractAttribute>.  
  
    ```  
    [ServiceContract(SessionMode = SessionMode.Required)]  
    public interface IAccount  
    {  
        [OperationContract]  
        [TransactionFlow(TransactionFlowOption.Allowed)]  
        void Debit(double n);  
        [OperationContract]  
        [TransactionFlow(TransactionFlowOption.Allowed)]  
        void Credit1(double n);  
        [OperationContract]  
        [TransactionFlow(TransactionFlowOption.Allowed)]  
        void Credit2(double n);  
    }  
    ```  
  
### Controllo della durata di un'istanza del servizio transazionale  
  
1.  [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza la proprietà <xref:System.ServiceModel.ServiceBehaviorAttribute.ReleaseServiceInstanceOnTransactionComplete%2A> per specificare se l'istanza del servizio sottostante viene rilasciata al completamento di una transazione.Dato che, salvo configurazione diversa, l'impostazione predefinita è `true`, [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] presenta un comportamento di attivazione JIT efficiente e prevedibile.Alle chiamate a un servizio in una transazione successiva viene assicurata una nuova istanza del servizio, senza resti dello stato della transazione precedente.Anche se ciò è spesso utile, qualche volta è necessario mantenere lo stato all'interno dell'istanza del servizio oltre il completamento della transazione,ad esempio quando è oneroso recuperare o ricostruire lo stato richiesto o gli handle di risorse.A tale fine, impostare la proprietà <xref:System.ServiceModel.ServiceBehaviorAttribute.ReleaseServiceInstanceOnTransactionComplete%2A> su `false`.Grazie a tale impostazione, l'istanza e qualsiasi stato associato saranno disponibili alle chiamate successive.In tal caso, valutare attentamente quando e come lo stato e le transazioni verranno cancellati e completati.Nell'esempio seguente viene illustrato come procedere gestendo l'istanza con la variabile `runningTotal`.  
  
    ```  
    [ServiceBehavior(TransactionIsolationLevel = [ServiceBehavior(  
        ReleaseServiceInstanceOnTransactionComplete = false)]  
    public class CalculatorService : ICalculator  
    {  
        double runningTotal = 0;  
  
        [OperationBehavior(TransactionScopeRequired = true)]  
        public double Add(double n)  
        {  
            // Perform transactional operation  
            RecordToLog(String.Format("Adding {0} to {1}", n, runningTotal));  
            runningTotal = runningTotal + n;  
            return runningTotal;  
        }  
  
        [OperationBehavior(TransactionScopeRequired = true)]  
        public double Subtract(double n)  
        {  
            // Perform transactional operation  
            RecordToLog(String.Format("Subtracting {0} from {1}", n, runningTotal));  
            runningTotal = runningTotal - n;  
            return runningTotal;  
        }  
  
        private static void RecordToLog(string recordText)  
        {  
            // Database operations omitted for brevity  
        }  
    }  
    ```  
  
    > [!NOTE]
    >  Poiché la durata dell'istanza è un comportamento interno al servizio e viene controllato tramite la proprietà <xref:System.ServiceModel.ServiceBehaviorAttribute>, per impostare il comportamento dell'istanza non è richiesta alcuna modifica alla configurazione del servizio o al contratto di servizio.La rete non conterrà inoltre nessuna rappresentazione di tale situazione.