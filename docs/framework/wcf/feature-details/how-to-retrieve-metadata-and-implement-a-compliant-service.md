---
title: "Procedura: recuperare metadati e implementare un servizio conforme | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f6f3a2b9-c8aa-4b0b-832c-ec2927bf1163
caps.latest.revision: 13
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 13
---
# Procedura: recuperare metadati e implementare un servizio conforme
Spesso i servizi non vengono progettati e implementati dalla stessa persona. Negli ambienti dove le applicazioni interoperative svolgono un ruolo importante, i contratti possono essere progettati o descritti in WSDL (Web Services Description Language) e uno sviluppatore deve implementare un servizio che sia conforme al contratto fornito. In alcuni casi può essere necessario eseguire la migrazione di un servizio esistente a [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] mantenendo tuttavia il formato di trasmissione. I contratti duplex richiedono inoltre ai chiamanti di implementare anche un contratto di callback.  
  
 In questi casi, è necessario utilizzare il [strumento ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) (o uno strumento equivalente) per generare un'interfaccia del contratto di servizio in un linguaggio gestito che è possibile implementare per soddisfare i requisiti del contratto. In genere il [strumento ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) consentono di acquisire un contratto di servizio che viene utilizzato con una channel factory o un [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] nonché con un file di configurazione client che consente di impostare il binding corretto e l'indirizzo di tipo client. Per usare il file di configurazione generato, è necessario modificarlo in un file di configurazione del servizio. Può inoltre essere necessario modificare il contratto di servizio.  
  
### <a name="to-retrieve-data-and-implement-a-compliant-service"></a>Per recuperare dati e implementare un servizio conforme  
  
1.  Utilizzare il [strumento ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) contro i file di metadati o un endpoint di metadati per generare un file di codice.  
  
2.  Cercare la parte del file di output codice che contiene l'interfaccia desiderata (nel caso siano presenti più interfacce) contrassegnata con il <xref:System.ServiceModel.ServiceContractAttribute?displayProperty=fullName> attributo. Esempio di codice seguente mostra le due interfacce generate da [strumento ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md). La prima (`ISampleService`) è l'interfaccia del contratto di servizio che viene implementata per creare un servizio conforme. Il secondo (`ISampleServiceChannel`) è un'interfaccia di supporto per l'utilizzo di client che estende sia l'interfaccia di contratto di servizio e <xref:System.ServiceModel.IClientChannel?displayProperty=fullName> e viene utilizzato in un'applicazione client.  
  
     [!code-csharp[ClientProxyCodeSample#2](../../../../samples/snippets/csharp/VS_Snippets_CFX/clientproxycodesample/cs/proxycode.cs#2)]  
  
3.  Se il file WSDL non specifica un'azione di risposta per tutte le operazioni, potrebbero essere contratti di operazione generati il <xref:System.ServiceModel.OperationContractAttribute.ReplyAction%2A> impostata sul carattere jolly (*). Rimuovere l'impostazione di questa proprietà. In caso contrario, quando vengono implementati i metadati del contratto di servizio, i metadati non possono essere esportati per tali operazioni.  
  
4.  Implementare l'interfaccia in una classe e ospitare il servizio. Per un esempio, vedere [procedura: implementare un contratto di servizio](../../../../docs/framework/wcf/how-to-implement-a-wcf-contract.md), o visualizzare una semplice implementazione riportata di seguito nella sezione esempio.  
  
5.  Nel client file di configurazione che il [strumento ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) viene generato l'errore, modificare il [ <> \> ](../../../../docs/framework/configure-apps/file-schema/wcf/client.md) sezione di configurazione da un [ <> \> ](../../../../docs/framework/configure-apps/file-schema/wcf/services.md) sezione di configurazione. Per un esempio di file di configurazione dell'applicazione client generato, vedere la sezione "Esempio" seguente.  
  
6.  All'interno di [ <> \> ](../../../../docs/framework/configure-apps/file-schema/wcf/services.md) configurazione sezione, creare un `name` attributo il [ <> \> ](../../../../docs/framework/configure-apps/file-schema/wcf/services.md) sezione di configurazione per l'implementazione del servizio.  
  
7.  Impostare l'attributo `name` del servizio sul nome di configurazione da assegnare all'implementazione del servizio.  
  
8.  Aggiungere gli elementi della configurazione endpoint che usano il contratto di servizio implementato alla sezione di configurazione del servizio.  
  
## <a name="example"></a>Esempio  
 Esempio di codice seguente viene illustrata la maggior parte di un file di codice generato eseguendo il [strumento ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) in file di metadati.  
  
 Il codice seguente include:  
  
-   L'interfaccia del contratto di servizio che, quando implementata, è conforme ai requisiti del contratto (`ISampleService`).  
  
-   L'interfaccia di supporto per l'utilizzo di client che estende sia l'interfaccia di contratto di servizio e <xref:System.ServiceModel.IClientChannel?displayProperty=fullName> e viene utilizzato in un'applicazione client (`ISampleServiceChannel`).  
  
-   La classe helper che estende <xref:System.ServiceModel.ClientBase%601?displayProperty=fullName> e viene utilizzato in un'applicazione client (`SampleServiceClient`).  
  
-   Il file di configurazione generato dal servizio.  
  
-   Una semplice implementazione del servizio `ISampleService`.  
  
-   Una conversione del file di configurazione lato client in una versione lato servizio.  
  
 [!code-csharp[ClientProxyCodeSample#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/clientproxycodesample/cs/proxycode.cs#1)]  
  
 <!-- TODO: review snippet reference [!code[ClientProxyCodeSample#10](../../../../samples/snippets/common/VS_Snippets_CFX/clientproxycodesample/common/client.exe.config#10)]  -->
 <!-- TODO: review snippet reference [!code-csharp[ClientProxyCodeSample#10](../../../../samples/snippets/csharp/VS_Snippets_CFX/clientproxycodesample/cs/client.exe.config#10)]  -->  
  
 [!code-csharp[ClientProxyCodeSample#5](../../../../samples/snippets/csharp/VS_Snippets_CFX/clientproxycodesample/cs/hostapplication.cs#5)]  
  
 <!-- TODO: review snippet reference [!code[ClientProxyCodeSample#20](../../../../samples/snippets/common/VS_Snippets_CFX/clientproxycodesample/common/hostapplication.exe.config#20)]  -->
 <!-- TODO: review snippet reference [!code-csharp[ClientProxyCodeSample#20](../../../../samples/snippets/csharp/VS_Snippets_CFX/clientproxycodesample/cs/hostapplication.exe.config#20)]  -->  
  
## <a name="see-also"></a>Vedere anche  
 [Strumento ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)