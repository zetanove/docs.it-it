---
title: "Specifica del comportamento in fase di esecuzione dei client | Microsoft Docs"
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
  - "comportamenti [WCF], fornito dal sistema client"
ms.assetid: d16d3405-be70-4edb-8f62-b5f614ddeca5
caps.latest.revision: 8
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 8
---
# Specifica del comportamento in fase di esecuzione dei client
I client [!INCLUDE[indigo1](../../../includes/indigo1-md.md)], come i servizi [!INCLUDE[indigo1](../../../includes/indigo1-md.md)], possono essere configurati per modificare il proprio comportamento in fase di esecuzione e adattarlo alle esigenze dell'applicazione client. Sono disponibili tre attributi per la specifica del comportamento in fase di esecuzione dei client. Gli oggetti di callback client duplex possono usare il <xref:System.ServiceModel.CallbackBehaviorAttribute> e <xref:System.ServiceModel.Description.CallbackDebugBehavior> attributi per modificarne il comportamento in fase di esecuzione. L'altro attributo, <xref:System.ServiceModel.Description.ClientViaBehavior>, può essere utilizzato per separare la destinazione logica dalla destinazione di rete immediata. Inoltre, i tipi di callback dei client duplex possono usare alcuni dei comportamenti del lato servizi. [!INCLUDE[crdefault](../../../includes/crdefault-md.md)][Specifica del comportamento in fase di esecuzione servizio](../../../docs/framework/wcf/specifying-service-run-time-behavior.md).  
  
## <a name="using-the-callbackbehaviorattribute"></a>Uso di CallbackBehaviorAttribute  
 È possibile configurare o estendere il comportamento di esecuzione di un'implementazione del contratto di callback in un'applicazione client utilizzando il <xref:System.ServiceModel.CallbackBehaviorAttribute> (classe). Questo attributo esegue una funzione simile per la classe di callback di <xref:System.ServiceModel.ServiceBehaviorAttribute> (classe), fatta eccezione per le impostazioni di comportamento e delle transazioni di istanze.  
  
 Il <xref:System.ServiceModel.CallbackBehaviorAttribute> classe deve essere applicata alla classe che implementa il contratto di callback. Se applicato a un'implementazione del contratto non duplex, un <xref:System.InvalidOperationException> eccezione in fase di esecuzione. Nell'esempio di codice riportato di seguito viene un <xref:System.ServiceModel.CallbackBehaviorAttribute> classe su un oggetto callback che utilizza il <xref:System.Threading.SynchronizationContext> oggetto per determinare il thread su cui eseguire il marshalling, la <xref:System.ServiceModel.CallbackBehaviorAttribute.ValidateMustUnderstand%2A> proprietà per applicare la convalida del messaggio e il <xref:System.ServiceModel.CallbackBehaviorAttribute.IncludeExceptionDetailInFaults%2A> proprietà per restituire eccezioni come <xref:System.ServiceModel.FaultException> oggetti al servizio a scopo di debug.  
  
 [!code-csharp[CallbackBehaviorAttribute#3](../../../samples/snippets/csharp/VS_Snippets_CFX/callbackbehaviorattribute/cs/client.cs#3)]
 [!code-vb[CallbackBehaviorAttribute#3](../../../samples/snippets/visualbasic/VS_Snippets_CFX/callbackbehaviorattribute/vb/client.vb#3)]  
  
## <a name="using-callbackdebugbehavior-to-enable-the-flow-of-managed-exception-information"></a>Uso di CallbackDebugBehavior per abilitare il flusso di informazioni sulle eccezioni gestite  
 È possibile abilitare il flusso di informazioni sulle eccezioni gestite in un oggetto di callback del client al servizio a scopo di debug impostando il <xref:System.ServiceModel.Description.CallbackDebugBehavior.IncludeExceptionDetailInFaults%2A> proprietà `true` file a livello di codice o da una configurazione dell'applicazione.  
  
 La restituzione ai servizi delle informazioni sulle eccezioni gestite può rappresentare un rischio per la protezione, poiché i dettagli delle eccezioni espongono informazioni sull'implementazione del client interno utilizzabili da servizi non autorizzati. Inoltre, sebbene il <xref:System.ServiceModel.Description.CallbackDebugBehavior> può anche essere impostate a livello di programmazione, può essere facile dimenticare di disattivare <xref:System.ServiceModel.Description.CallbackDebugBehavior.IncludeExceptionDetailInFaults%2A> durante la distribuzione.  
  
 A causa dei problemi di sicurezza coinvolti, è consigliato:  
  
-   Utilizzare un file di configurazione dell'applicazione per impostare il valore di <xref:System.ServiceModel.Description.CallbackDebugBehavior.IncludeExceptionDetailInFaults%2A> proprietà `true`.  
  
-   Si procede in questo modo solo negli scenari di debug controllati.  
  
 Nell'esempio di codice seguente viene mostrato un file di configurazione client che indica a [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] di restituire informazioni sulle eccezioni gestite da un oggetto callback client in messaggi SOAP.  
  
 <!-- TODO: review snippet reference [!code[SCA.CallbackContract#4](../../../samples/snippets/common/VS_Snippets_CFX/sca.callbackcontract/common/client.exe.config#4)]  -->
 <!-- TODO: review snippet reference [!code-csharp[SCA.CallbackContract#4](../../../samples/snippets/csharp/VS_Snippets_CFX/sca.callbackcontract/cs/client.exe.config#4)]  -->
 <!-- TODO: review snippet reference [!code-vb[SCA.CallbackContract#4](../../../samples/snippets/visualbasic/VS_Snippets_CFX/sca.callbackcontract/vb/client.exe.config#4)]  -->  
  
## <a name="using-the-clientviabehavior-behavior"></a>Utilizzo del comportamento ClientViaBehavior  
 È possibile utilizzare il <xref:System.ServiceModel.Description.ClientViaBehavior> comportamento per specificare l'URI per il quale deve essere creato il canale di trasporto. Usare questo comportamento quando la destinazione di rete immediata non è il processore desiderato del messaggio. Questo consente conversazioni multihop quando l'applicazione chiamante non conosce necessariamente la destinazione finale o quando l'intestazione `Via` della destinazione non è un indirizzo.  
  
## <a name="see-also"></a>Vedere anche  
 [Specifica il comportamento di runtime del servizio](../../../docs/framework/wcf/specifying-service-run-time-behavior.md)