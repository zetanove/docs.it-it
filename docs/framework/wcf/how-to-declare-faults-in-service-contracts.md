---
title: "Procedura: dichiarare errori nei contratti di servizio | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: e8da98e7-d22f-4f60-ac82-3fb0928a353f
caps.latest.revision: 5
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 5
---
# Procedura: dichiarare errori nei contratti di servizio
Nel codice gestito, vengono generate eccezioni quando si verificano condizioni di errore.  Nelle applicazioni [!INCLUDE[indigo1](../../../includes/indigo1-md.md)], tuttavia, i contratti di servizio specificano quali informazioni sugli errori vengono restituite dai client dichiarando errori SOAP nel contratto di servizio.  Per una panoramica sulla relazione tra eccezioni ed errori, vedere [Specifica e gestione di errori in contratti e servizi](../../../docs/framework/wcf/specifying-and-handling-faults-in-contracts-and-services.md).  
  
### Creare un contratto di servizio che specifica un errore SOAP.  
  
1.  Creare un contratto di servizio che contiene almeno un'operazione.  Per un esempio, vedere [Procedura: definire il contratto di servizio](../../../docs/framework/wcf/how-to-define-a-wcf-service-contract.md).  
  
2.  Selezionare un'operazione che può specificare una condizione di errore in merito alla quale i client prevedono di ricevere una notifica.  Per decidere quali condizioni di errore giustificano la restituzione di errori SOAP ai client, vedere [Specifica e gestione di errori in contratti e servizi](../../../docs/framework/wcf/specifying-and-handling-faults-in-contracts-and-services.md).  
  
3.  Applicare una classe <xref:System.ServiceModel.FaultContractAttribute?displayProperty=fullName> all'operazione selezionata e passare un tipo di errore serializzabile al costruttore.  Per dettagli sulla creazione e l'uso di tipi serializzabili, vedere [Specifica del trasferimento di dati nei contratti di servizio](../../../docs/framework/wcf/feature-details/specifying-data-transfer-in-service-contracts.md).  Nell'esempio seguente viene illustrato come specificare che l'operazione `SampleMethod` può produrre un `GreetingFault`.  
  
     [!code-csharp[FaultContractAttribute#4](../../../samples/snippets/csharp/VS_Snippets_CFX/faultcontractattribute/cs/services.cs#4)]
     [!code-vb[FaultContractAttribute#4](../../../samples/snippets/visualbasic/VS_Snippets_CFX/faultcontractattribute/vb/services.vb#4)]  
  
4.  Ripetere i passaggi 2 e 3 per tutte le operazioni nel contratto che comunicano condizioni di errore ai client.  
  
## Implementazione di un'operazione per restituire un errore SOAP specificato  
 Dopo che un'operazione ha specificato che può essere restituito un determinato errore SOAP \(come nella procedura seguente\), per comunicare una condizione di errore a un'applicazione chiamante, il passaggio successivo consiste nell'implementare la specifica in questione.  
  
#### Generare l'errore SOAP specificato nell'operazione  
  
1.  Quando in un'operazione si verifica una condizione di errore specificata da <xref:System.ServiceModel.FaultContractAttribute>, generare una nuova eccezione <xref:System.ServiceModel.FaultException%601?displayProperty=fullName> in cui l'errore SOAP specificato è il parametro di tipo.  Nell'esempio seguente viene illustrato come generare il `GreetingFault` nel `SampleMethod` descritto nella procedura precedente e nella sezione Codice seguente.  
  
     [!code-csharp[FaultContractAttribute#5](../../../samples/snippets/csharp/VS_Snippets_CFX/faultcontractattribute/cs/services.cs#5)]
     [!code-vb[FaultContractAttribute#5](../../../samples/snippets/visualbasic/VS_Snippets_CFX/faultcontractattribute/vb/services.vb#5)]  
  
## Esempio  
 Nell'esempio di codice seguente viene illustrata un'implementazione di una singola operazione che specifica un `GreetingFault` per l'operazione `SampleMethod`.  
  
 [!code-csharp[FaultContractAttribute#1](../../../samples/snippets/csharp/VS_Snippets_CFX/faultcontractattribute/cs/services.cs#1)]
 [!code-vb[FaultContractAttribute#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/faultcontractattribute/vb/services.vb#1)]  
  
## Vedere anche  
 <xref:System.ServiceModel.FaultContractAttribute?displayProperty=fullName>   
 <xref:System.ServiceModel.FaultException%601?displayProperty=fullName>