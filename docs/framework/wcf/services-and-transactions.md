---
title: "Servizi e transazioni | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "contratti di servizio [WCF], progettazione di servizi e transazioni"
ms.assetid: 864813ff-2709-4376-912d-f5c8d318c460
caps.latest.revision: 10
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 10
---
# Servizi e transazioni
Le applicazioni di [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] possono avviare una transazione dall'interno di un client e coordinarla all'interno dell'operazione di servizio.I client possono avviare una transazione e richiamare varie operazioni di servizio nonché fare in modo che per queste ultime venga eseguito il commit o il rollback come unità singola.  
  
 È possibile attivare il comportamento della transazione nel contratto di servizio specificando un elemento <xref:System.ServiceModel.ServiceBehaviorAttribute> e impostando le proprietà <xref:System.ServiceModel.ServiceBehaviorAttribute.TransactionIsolationLevel%2A> e <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionScopeRequired%2A> per operazioni di servizio che richiedono transazioni client.Il parametro <xref:System.ServiceModel.OperationBehaviorAttribute.TransactionAutoComplete%2A> specifica se la transazione in cui viene eseguito il metodo viene completata automaticamente nel caso in cui non venga generata alcuna eccezione non gestita.[!INCLUDE[crabout](../../../includes/crabout-md.md)] questi attributi, vedere [Attributi della transazione di ServiceModel](../../../docs/framework/wcf/feature-details/servicemodel-transaction-attributes.md).  
  
 Il lavoro eseguito nelle operazioni di servizio e curato da un gestore di risorse, ad esempio la registrazione di aggiornamenti del database, fa parte della transazione del client.  
  
 Nell'esempio seguente viene dimostrato l'utilizzo degli attributi <xref:System.ServiceModel.ServiceBehaviorAttribute> e <xref:System.ServiceModel.OperationBehaviorAttribute> per controllare il comportamento della transazione dal lato del servizio.  
  
```  
[ServiceBehavior(TransactionIsolationLevel = System.Transactions.IsolationLevel.Serializable)]  
public class CalculatorService: ICalculatorLog  
{  
    [OperationBehavior(TransactionScopeRequired = true,  
                           TransactionAutoComplete = true)]  
    public double Add(double n1, double n2)  
    {  
        recordToLog(String.Format("Added {0} to {1}", n1, n2));  
        return n1 + n2;  
    }  
  
    [OperationBehavior(TransactionScopeRequired = true,   
                               TransactionAutoComplete = true)]  
    public double Subtract(double n1, double n2)  
    {  
        recordToLog(String.Format("Subtracted {0} from {1}", n1, n2));  
        return n1 - n2;  
    }  
  
    [OperationBehavior(TransactionScopeRequired = true,   
                                       TransactionAutoComplete = true)]  
    public double Multiply(double n1, double n2)  
    {  
        recordToLog(String.Format("Multiplied {0} by {1}", n1, n2));  
        return n1 * n2;  
    }  
  
    [OperationBehavior(TransactionScopeRequired = true,   
                                       TransactionAutoComplete = true)]  
    public double Divide(double n1, double n2)  
    {  
        recordToLog(String.Format("Divided {0} by {1}", n1, n2));  
        return n1 / n2;  
    }  
  
}  
```  
  
 È possibile attivare transazioni e propagazione transazionale configurando le associazioni client e di servizio per l'utilizzo del protocollo WS\-AtomicTransaction e impostando l'elemento [\<transactionFlow\>](../../../docs/framework/configure-apps/file-schema/wcf/transactionflow.md)`true su` , come illustrato nella configurazione di esempio seguente.  
  
```  
<client>  
    <endpoint address="net.tcp://localhost/ServiceModelSamples/service"   
          binding="netTcpBinding"   
          bindingConfiguration="netTcpBindingWSAT"   
          contract="Microsoft.ServiceModel.Samples.ICalculatorLog" />  
</client>  
  
<bindings>  
    <netTcpBinding>  
        <binding name="netTcpBindingWSAT"  
                transactionFlow="true"  
                transactionProtocol="WSAtomicTransactionOctober2004" />  
     </netTcpBinding>  
</bindings>  
```  
  
 I client possono iniziare una transazione creando un elemento <xref:System.Transactions.TransactionScope> e richiamando operazioni di servizio nell'ambito della transazione.  
  
```  
using (TransactionScope ts = new TransactionScope(TransactionScopeOption.RequiresNew))  
{  
    //Do work here  
    ts.Complete();  
}  
```  
  
## Vedere anche  
 [Supporto transazionale in System.ServiceModel](../../../docs/framework/wcf/feature-details/transactional-support-in-system-servicemodel.md)   
 [Modelli di transazione](../../../docs/framework/wcf/feature-details/transaction-models.md)   
 [Flusso delle transazioni WS](../../../docs/framework/wcf/samples/ws-transaction-flow.md)