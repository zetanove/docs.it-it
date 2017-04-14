---
title: "Integrazione di componenti transazionali di Enterprise Services | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 05dab277-b8b2-48cf-b40c-826be128b175
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Integrazione di componenti transazionali di Enterprise Services
In [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] è disponibile un meccanismo automatico per l'integrazione con Enterprise Services \(vedere [Integrazione con applicazioni COM\+](../../../../docs/framework/wcf/feature-details/integrating-with-com-plus-applications.md)\).Può tuttavia essere necessario disporre della flessibilità di sviluppare servizi che utilizzano internamente componenti transazionali ospitati all'interno di Enterprise Services.Poiché la funzionalità Transactions di [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] si basa sull'infrastruttura di <xref:System.Transactions>, il processo per l'integrazione di Enterprise Services con [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] è identico a quello per la specifica dell'interoperabilità tra <xref:System.Transactions> ed Enterprise Services, come descritto in [Interoperabilità con le transazioni Enterprise Services e COM\+](http://go.microsoft.com/fwlink/?LinkId=94949) \(la pagina potrebbe essere in inglese\).  
  
 Per fornire il livello desiderato di interoperabilità tra la transazione propagata in ingresso e la transazione in contesto COM\+, l'implementazione del servizio deve creare un'istanza della classe <xref:System.Transactions.TransactionScope> e deve utilizzare il valore appropriato ricavato dall'enumerazione <xref:System.Transactions.EnterpriseServicesInteropOption>.  
  
## Integrazione di Enterprise Services con un'operazione del servizio  
 Nel codice seguente viene illustrata un'operazione, con propagazione transazionale Allowed, che crea una classe <xref:System.Transactions.TransactionScope> con l'opzione <xref:System.Transactions.EnterpriseServicesInteropOption>.In questo scenario vengono applicate le condizioni seguenti:  
  
-   Se il client propaga una transazione, l'operazione, inclusa la chiamata al componente Enterprise Services, viene eseguita all'interno dell'ambito di tale transazione.L'utilizzo di <xref:System.Transactions.EnterpriseServicesInteropOption> garantisce la sincronizzazione della transazione con il contesto <xref:System.EnterpriseServices>, il che significa che la transazione di ambiente per <xref:System.Transactions> e <xref:System.EnterpriseServices> è la stessa.  
  
-   Se il client non propaga una transazione, l'impostazione di <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A> su `true` crea un nuovo ambito di transazione per l'operazione.Analogamente, l'utilizzo di <xref:System.Transactions.EnterpriseServicesInteropOption> garantisce che la transazione dell'operazione sia la stessa transazione utilizzata all'interno del contesto del componente <xref:System.EnterpriseServices>.  
  
 Eventuali chiamate aggiuntive al metodo avvengono anch'esse nell'ambito della stessa transazione dell'operazione.  
  
```  
[ServiceContract()]  
public interface ICustomerServiceContract  
{  
   [OperationContract]  
   [TransactionFlow(TransactionFlowOption.Allowed)]  
   void UpdateCustomerNameOperation(int customerID, string newCustomerName);  
}  
  
[ServiceBehavior(TransactionIsolationLevel = System.Transactions.IsolationLevel.Serializable)]  
public class CustomerService : ICustomerServiceContract  
{  
   [OperationBehavior(TransactionScopeRequired = true, TransactionAutoComplete = true)]  
   public void UpdateCustomerNameOperation(int customerID, string newCustomerName)  
   {  
   // Create a transaction scope with full ES interop  
      using (TransactionScope ts = new TransactionScope(  
                     TransactionScopeOption.Required,  
                     new TransactionOptions(),  
                     EnterpriseServicesInteropOption.Full))  
      {  
         // Create an Enterprise Services component  
         // Call UpdateCustomer method on an Enterprise Services   
         // component   
  
         // Call UpdateOtherCustomerData method on an Enterprise   
         // Services component   
         ts.Complete();  
      }  
  
      // Do UpdateAdditionalData on an non-Enterprise Services  
      // component  
   }  
}  
```  
  
 Se non è necessaria alcuna sincronizzazione tra la transazione corrente di un'operazione e le chiamate ai componenti Enterprise Services transazionali, utilizzare l'opzione <xref:System.Transactions.EnterpriseServicesInteropOption> quando si crea l'istanza di <xref:System.Transactions.TransactionScope>.  
  
## Integrazione di Enterprise Services con un client  
 Nell'esempio seguente viene illustrato il codice client utilizzando un'istanza della classe <xref:System.Transactions.TransactionScope> con l'impostazione <xref:System.Transactions.EnterpriseServicesInteropOption>In questo scenario, le chiamate alle operazioni del servizio che supportano la propagazione transazionale avvengono nell'ambito della stessa transazione delle chiamate ai componenti Enterprise Services.  
  
```  
static void Main()  
{  
    // Create a client  
    CalculatorClient client = new CalculatorClient();  
  
    // Create a transaction scope with full ES interop  
    using (TransactionScope ts = new TransactionScope(  
          TransactionScopeOption.Required,  
          new TransactionOptions(),  
          EnterpriseServicesInteropOption.Full))  
    {  
        // Call Add calculator service operation  
  
        // Create an Enterprise Services component  
  
        // Call UpdateCustomer method on an Enterprise Services   
        // component   
  
        ts.Complete();  
    }  
  
    // Closing the client gracefully closes the connection and   
    // cleans up resources  
    client.Close();  
}  
```  
  
## Vedere anche  
 [Integrazione con applicazioni COM\+](../../../../docs/framework/wcf/feature-details/integrating-with-com-plus-applications.md)   
 [Integrazione con applicazioni COM](../../../../docs/framework/wcf/feature-details/integrating-with-com-applications.md)