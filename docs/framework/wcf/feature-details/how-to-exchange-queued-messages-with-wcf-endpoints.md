---
title: "Procedura: scambiare messaggi in coda con endpoint WCF | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 938e7825-f63a-4c3d-b603-63772fabfdb3
caps.latest.revision: 18
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 18
---
# Procedura: scambiare messaggi in coda con endpoint WCF
Le code garantiscono una messaggistica affidabile tra un client e un servizio [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)], anche se il servizio non è disponibile al momento della comunicazione. Nelle procedure seguenti viene spiegato come assicurare una comunicazione durevole tra un client e un servizio utilizzando l'associazione in coda standard in caso di implementazione del servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
 In questa sezione viene illustrato come utilizzare <xref:System.ServiceModel.NetMsmqBinding> per la comunicazione in coda tra un [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] client e un [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] servizio.  
  
### <a name="to-use-queuing-in-a-wcf-service"></a>Per utilizzare l'accodamento in un servizio WCF  
  
1.  Definire un contratto di servizio utilizzando un'interfaccia contrassegnata con il <xref:System.ServiceModel.ServiceContractAttribute>. Contrassegnare le operazioni nell'interfaccia che fanno parte del contratto di servizio con il <xref:System.ServiceModel.OperationContractAttribute> e specificarli come unidirezionali, poiché viene restituita alcuna risposta al metodo. Nel codice seguente sono contenuti un esempio di contratto di servizio semplice e la relativa definizione di operazione.  
  
     [!code-csharp[S_Msmq_Transacted#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_msmq_transacted/cs/service.cs#1)]
     [!code-vb[S_Msmq_Transacted#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_msmq_transacted/vb/service.vb#1)]  
  
2.  Quando il contratto di servizio passa tipi definiti dall'utente, è necessario definire contratti dati per tali tipi. Nel codice seguente vengono illustrati due contratti dati, `PurchaseOrder` e `PurchaseOrderLineItem`. Questi due tipi definiscono i dati inviati al servizio. Si noti che le classi che definiscono questo contratto dati definiscono anche un certo numero di metodi. Questi non vengono considerati parte del contratto dati. Solo i membri che sono dichiarati con l'attributo `DataMember` fanno parte del contratto dati.  
  
     [!code-csharp[S_Msmq_Transacted#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_msmq_transacted/cs/service.cs#2)]
     [!code-vb[S_Msmq_Transacted#2](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_msmq_transacted/vb/service.vb#2)]  
  
3.  Implementare i metodi del contratto di servizio definiti nell'interfaccia in una classe.  
  
     [!code-csharp[S_Msmq_Transacted#3](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_msmq_transacted/cs/service.cs#3)]
     [!code-vb[S_Msmq_Transacted#3](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_msmq_transacted/vb/service.vb#3)]  
  
     Si noti che il <xref:System.ServiceModel.OperationBehaviorAttribute> sul `SubmitPurchaseOrder` metodo. In tal modo viene specificato che questa operazione deve essere chiamata all'interno di una transazione e che la transazione viene completata automaticamente quando il metodo è stato completato.  
  
4.  Creare una coda transazionale utilizzando <xref:System.Messaging>. È possibile scegliere di creare la coda mediante la console MMC (Microsoft Management Console) MSMQ. In tal caso, avere cura di creare una coda transazionale.  
  
     [!code-csharp[S_Msmq_Transacted#4](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_msmq_transacted/cs/hostapp.cs#4)]
     [!code-vb[S_Msmq_Transacted#4](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_msmq_transacted/vb/hostapp.vb#4)]  
  
5.  Definire un <xref:System.ServiceModel.Description.ServiceEndpoint> nella configurazione che specifica l'indirizzo del servizio e utilizza lo standard <xref:System.ServiceModel.NetMsmqBinding> associazione. [!INCLUDE[crabout](../../../../includes/crabout-md.md)]utilizzando [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] configurazione, vedere [la configurazione di applicazioni di Windows Communication Foundation](http://msdn.microsoft.com/it-it/13cb368e-88d4-4c61-8eed-2af0361c6d7a).  
  
  
  
6.  Creare un host per il `OrderProcessing` service utilizzando <xref:System.ServiceModel.ServiceHost> che legge i messaggi dalla coda e li elabora. Aprire l'host del servizio per rendere disponibile il servizio. Visualizzare un messaggio che indichi all'utente di premere un tasto qualsiasi per terminare il servizio. Chiamare `ReadLine` per attendere che il tasto venga premuto, quindi chiudere il servizio.  
  
     [!code-csharp[S_Msmq_Transacted#6](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_msmq_transacted/cs/hostapp.cs#6)]
     [!code-vb[S_Msmq_Transacted#6](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_msmq_transacted/vb/hostapp.vb#6)]  
  
### <a name="to-create-a-client-for-the-queued-service"></a>Per creare un client per il servizio in coda  
  
1.  Nell'esempio di codice riportato di seguito viene illustrato come eseguire l'applicazione host e utilizzare lo strumento Svcutil.exe per creare il client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].  
  
    ```  
    svcutil http://localhost:8000/ServiceModelSamples/service  
    ```  
  
2.  Definire un <xref:System.ServiceModel.Description.ServiceEndpoint> nella configurazione che specifica l'indirizzo e utilizza lo standard <xref:System.ServiceModel.NetMsmqBinding> binding, come illustrato nell'esempio seguente.  
  
  
  
3.  Creare un ambito di transazione da scrivere nella coda transazionale, chiamare l'operazione `SubmitPurchaseOrder` e chiudere il client [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], come illustrato nell'esempio seguente.  
  
     [!code-csharp[S_Msmq_Transacted#8](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_msmq_transacted/cs/client.cs#8)]
     [!code-vb[S_Msmq_Transacted#8](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_msmq_transacted/vb/client.vb#8)]  
  
## <a name="example"></a>Esempio  
 Negli esempi seguenti vengono illustrati il codice di servizio, l'applicazione host, il file App.config e il codice client inclusi per questo esempio.  
  
 [!code-csharp[S_Msmq_Transacted#9](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_msmq_transacted/cs/service.cs#9)]
 [!code-vb[S_Msmq_Transacted#9](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_msmq_transacted/vb/service.vb#9)]  
  
 [!code-csharp[S_Msmq_Transacted#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_msmq_transacted/cs/hostapp.cs#10)]
 [!code-vb[S_Msmq_Transacted#10](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_msmq_transacted/vb/hostapp.vb#10)]  
  
  
  
 [!code-csharp[S_Msmq_Transacted#12](../../../../samples/snippets/csharp/VS_Snippets_CFX/s_msmq_transacted/cs/client.cs#12)]
 [!code-vb[S_Msmq_Transacted#12](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/s_msmq_transacted/vb/client.vb#12)]  
  
  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.ServiceModel.NetMsmqBinding>   
 [Associazioni MSMQ transazionali](../../../../docs/framework/wcf/samples/transacted-msmq-binding.md)   
 [Accodamento in WCF](../../../../docs/framework/wcf/feature-details/queuing-in-wcf.md)   
 [Procedura: scambiare messaggi con endpoint WCF e applicazioni di accodamento dei messaggi](../../../../docs/framework/wcf/feature-details/how-to-exchange-messages-with-wcf-endpoints-and-message-queuing-applications.md)   
 [Windows Communication Foundation a Accodamento messaggi](../../../../docs/framework/wcf/samples/wcf-to-message-queuing.md)   
 [L'installazione di Microsoft Message Queuing (MSMQ)](../../../../docs/framework/wcf/samples/installing-message-queuing-msmq.md)   
 [Esempi di associazione di integrazione di Accodamento messaggi](http://msdn.microsoft.com/it-it/997d11cb-f2c5-4ba0-9209-92843d4d0e1a)   
 [Accodamento messaggi in Windows Communication Foundation](../../../../docs/framework/wcf/samples/message-queuing-to-wcf.md)   
 [Sicurezza del messaggio su Accodamento messaggi](../../../../docs/framework/wcf/samples/message-security-over-message-queuing.md)