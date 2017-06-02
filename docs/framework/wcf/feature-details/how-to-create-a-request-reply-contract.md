---
title: "Procedura: creare un contratto request/reply | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 801d90da-3d45-4284-9c9f-56c8aadb4060
caps.latest.revision: 19
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 19
---
# Procedura: creare un contratto request/reply
Un contratto di tipo request\/reply specifica un metodo che restituisce una rispostache deve essere inviata e correlata alla richiesta in base ai termini di questo contratto.Anche se il metodo non restituisce alcuna risposta \(`void` in C\# o `Sub` in Visual Basic\), nell'infrastruttura viene creato e inviato un messaggio vuoto al chiamante.Per impedire l'invio di un messaggio di risposta vuoto, utilizzare un contratto unidirezionale per l'operazione.  
  
### Per creare un contratto request\/reply  
  
1.  Creare un'interfaccia nel linguaggio di programmazione desiderato.  
  
2.  Applicare l'attributo <xref:System.ServiceModel.ServiceContractAttribute> all'interfaccia.  
  
3.  Applicare l'attributo <xref:System.ServiceModel.OperationContractAttribute> a ciascun metodo che i client possono richiamare.  
  
4.  Facoltativa.Impostare il valore della proprietà <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A> su `true` per impedire l'invio di un messaggio di risposta vuoto.Per impostazione predefinita, tutte le operazioni sono contratti di tipo request\/reply.  
  
## Esempio  
 Nell'esempio seguente è definito un contratto per un servizio calcolatrice che fornisce metodi `Add` e `Subtract`.Il metodo `Multiply` privato non fa parte del contratto perché non è contrassegnato dalla classe <xref:System.ServiceModel.OperationContractAttribute> e quindi non è accessibile ai client.  
  
```  
using System.ServiceModel;   
  
[ServiceContract]   
public interface ICalculator   
{   
[OperationContract]   
// It would be equivalent to write explicitly:  
// [OperationContract(IsOneWay=false)]   
int Add(int a, int b);   
  
[OperationContract]   
int Subtract(int a, int b);   
  
int Multiply(int a, int b)  
}  
```  
  
-   [!INCLUDE[crabout](../../../../includes/crabout-md.md)] come specificare contratti di operazione, vedere la classe <xref:System.ServiceModel.OperationContractAttribute> e la proprietà <xref:System.ServiceModel.OperationContractAttribute.IsOneWay%2A>.  
  
-   L'applicazione degli attributi <xref:System.ServiceModel.ServiceContractAttribute> e <xref:System.ServiceModel.OperationContractAttribute> determina la generazione automatica delle definizioni del contratto di servizio in un documento del linguaggio di descrizione dei servizi Web \(WSDL, Web Services Description Language\) dopo la distribuzione del servizio.Il documento viene scaricato aggiungendo l'elemento `?wsdl` all'indirizzo di base HTTP per il servizio,ad esempio `http://microsoft/CalculatorService?wsdl`.  
  
## Vedere anche  
 <xref:System.ServiceModel.OperationContractAttribute>   
 [Progettazione dei contratti di servizio](../../../../docs/framework/wcf/designing-service-contracts.md)   
 [Procedura: creare un contratto duplex](../../../../docs/framework/wcf/feature-details/how-to-create-a-duplex-contract.md)