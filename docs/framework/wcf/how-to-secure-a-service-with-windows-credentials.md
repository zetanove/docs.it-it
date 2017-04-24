---
title: "Procedura: proteggere un servizio con credenziali di Windows | Microsoft Docs"
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
  - "WCF, sicurezza"
ms.assetid: d171b5ca-96ef-47ff-800c-c138023cf76e
caps.latest.revision: 26
author: "BrucePerlerMS"
ms.author: "bruceper"
manager: "mbaldwin"
caps.handback.revision: 26
---
# Procedura: proteggere un servizio con credenziali di Windows
In questo argomento viene illustrato come abilitare la sicurezza del trasferimento in un servizio di [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] che risiede in un dominio di Windows e viene chiamato da client dello stesso dominio. [!INCLUDE[crabout](../../../includes/crabout-md.md)]Questo scenario, vedere [la sicurezza del trasporto con l'autenticazione di Windows](../../../docs/framework/wcf/feature-details/transport-security-with-windows-authentication.md). Per un'applicazione di esempio, vedere il [WSHttpBinding](../../../docs/framework/wcf/samples/wshttpbinding.md) esempio.  
  
 In questo argomento si presuppone la presenza di un'interfaccia e di un'implementazione del contratto esistente già definite, alle quali vengono aggiunti elementi. È inoltre possibile modificare un servizio e un client esistenti.  
  
 È possibile proteggere un servizio con credenziali di Windows completamente nel codice. In alternativa, è possibile omettere parte del codice tramite un file di configurazione. In questo argomento vengono illustrate entrambe le modalità. Accertarsi di usare una sola modalità, non entrambe.  
  
 Nelle prime tre procedure viene illustrato come proteggere il servizio tramite il codice. Nella quarta e nella quinta procedura viene illustrato come eseguire questa operazione con un file di configurazione.  
  
## <a name="using-code"></a>Uso del codice  
 Il codice completo per il servizio e il client si trova nella sezione Esempio alla fine di questo argomento.  
  
 La prima procedura vengono illustrate la creazione e configurazione di un <xref:System.ServiceModel.WSHttpBinding> classe nel codice. Per l'associazione viene usata il trasporto HTTP. La stessa associazione viene usata nel client.  
  
#### <a name="to-create-a-wshttpbinding-that-uses-windows-credentials-and-message-security"></a>Per creare un oggetto WSHttpBinding che usa le credenziali di Windows e la protezione dei messaggio  
  
1.  Il codice di questa procedura viene inserito all'inizio del metodo `Run` della classe `Test` nel codice del servizio riportato nella sezione Esempio.  
  
2.  Creare un'istanza di <xref:System.ServiceModel.WSHttpBinding> (classe).  
  
3.  Impostare il <xref:System.ServiceModel.WsHttpSecurity.Mode%2A> proprietà del <xref:System.ServiceModel.WsHttpSecurity> classe <xref:System.ServiceModel.SecurityMode>.  
  
4.  Impostare il <xref:System.ServiceModel.MessageSecurityOverHttp.ClientCredentialType%2A> proprietà del <xref:System.ServiceModel.MessageSecurityOverHttp> classe <xref:System.ServiceModel.MessageCredentialType>.  
  
5.  Il codice per questa procedura è il seguente:  
  
     [!code-csharp[c_SecureWindowsService#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewindowsservice/cs/secureservice.cs#1)]
     [!code-vb[c_SecureWindowsService#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewindowsservice/vb/secureservice.vb#1)]  
  
### <a name="using-the-binding-in-a-service"></a>Uso dell'associazione in un servizio.  
 Si tratta della seconda procedura, in cui viene illustrato l'uso dell'associazione in un servizio self-hosted. [!INCLUDE[crabout](../../../includes/crabout-md.md)]servizi di hosting vedere [servizi di Hosting](../../../docs/framework/wcf/hosting-services.md).  
  
##### <a name="to-use-a-binding-in-a-service"></a>Per usare un'associazione in un servizio  
  
1.  Inserire il codice di questa procedura dopo il codice della procedura precedente.  
  
2.  Creare un <xref:System.Type> variabile denominata `contractType` e assegnarle il tipo dell'interfaccia (`ICalculator`). Quando si usa [!INCLUDE[vbprvb](../../../includes/vbprvb-md.md)], usare l'operatore `GetType`; quando si usa C#, usare la parola chiave `typeof`.  
  
3.  Creare una seconda variabile `Type` denominata `serviceType` e assegnarle il tipo del contratto implementato (`Calculator`).  
  
4.  Creare un'istanza di <xref:System.Uri> classe denominata `baseAddress` con l'indirizzo di base del servizio. L'indirizzo di base deve avere uno schema corrispondente al trasporto. In questo caso lo schema di trasporto è HTTP e l'indirizzo include l'URI (Uniform Resource Identifier) speciale "localhost" e un numero di porta (8036), oltre a un indirizzo endpoint di base ("serviceModelSamples/): http://localhost:8036/serviceModelSamples/.  
  
5.  Creare un'istanza di <xref:System.ServiceModel.ServiceHost> classe con il `serviceType` e `baseAddress` variabili.  
  
6.  Aggiungere un endpoint al servizio tramite l'interfaccia `contractType`, l'associazione e un nome di endpoint (secureCalculator). Un client deve concatenare l'indirizzo di base e il nome dell'endpoint quando avvia una chiamata al servizio.  
  
7.  Chiamare il <xref:System.ServiceModel.Channels.CommunicationObject.Open%2A> metodo per avviare il servizio. Il codice per questa procedura viene illustrato di seguito:  
  
     [!code-csharp[c_SecureWindowsService#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewindowsservice/cs/secureservice.cs#2)]
     [!code-vb[c_SecureWindowsService#2](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewindowsservice/vb/secureservice.vb#2)]  
  
### <a name="using-the-binding-in-a-client"></a>Uso dell'associazione in un client  
 In questa procedura viene illustrato come generare un proxy che comunica con il servizio. Il proxy viene generato con il [strumento ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) che utilizza i metadati del servizio per creare il proxy.  
  
 Questa procedura crea inoltre un'istanza di <xref:System.ServiceModel.WSHttpBinding> classe per comunicare con il servizio e quindi chiama il servizio.  
  
 In questo esempio, per creare il client viene usato solo codice. In alternativa, è possibile usare un file di configurazione, illustrato nella sezione successiva a questa procedura.  
  
##### <a name="to-use-a-binding-in-a-client-with-code"></a>Per usare un'associazione in un client con codice  
  
1.  Usare lo strumento SvcUtil.exe per generare il codice del proxy tramite i metadati del servizio. [!INCLUDE[crdefault](../../../includes/crdefault-md.md)][Procedura: creare un Client](../../../docs/framework/wcf/how-to-create-a-wcf-client.md). Il codice proxy generato eredita il <xref:System.ServiceModel.ClientBase%601> (classe), che assicura che ogni client disponga di necessari costruttori, metodi e proprietà per comunicare con un [!INCLUDE[indigo2](../../../includes/indigo2-md.md)] servizio. In questo esempio, il codice generato include la classe `CalculatorClient` che implementa l'interfaccia `ICalculator`, consentendo la compatibilità con il codice del servizio.  
  
2.  Il codice di questa procedura viene inserito all'inizio del metodo `Main` del programma client.  
  
3.  Creare un'istanza di <xref:System.ServiceModel.WSHttpBinding> classe e impostarne la modalità di sicurezza su `Message` e il tipo di credenziale client `Windows`. Nell'esempio viene denominata la variabile `clientBinding`.  
  
4.  Creare un'istanza di <xref:System.ServiceModel.EndpointAddress> classe denominata `serviceAddress`. Inizializzare l'istanza con l'indirizzo di base concatenato al nome dell'endpoint.  
  
5.  Creare un'istanza della classe client generata con le variabili `serviceAddress` e `clientBinding`.  
  
6.  Chiamare il <xref:System.ServiceModel.ClientBase%601.Open%2A> metodo, come illustrato nel codice seguente.  
  
7.  Chiamare il servizio e visualizzare i risultati.  
  
     [!code-csharp[c_secureWindowsClient#1](../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewindowsclient/cs/secureclient.cs#1)]
     [!code-vb[c_secureWindowsClient#1](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewindowsclient/vb/secureclient.vb#1)]  
  
## <a name="using-the-configuration-file"></a>Uso del file di configurazione  
 Anziché creare l'associazione con codice procedurale, è possibile usare il codice seguente illustrato per la sezione dell'associazione del file di configurazione.  
  
 Se non si dispone già di un servizio definito, vedere [la progettazione e implementazione di servizi](../../../docs/framework/wcf/designing-and-implementing-services.md), e [configurazione di servizi](../../../docs/framework/wcf/configuring-services.md).  
  
 **Nota** questo codice di configurazione viene usato nei file di configurazione del servizio e del client.  
  
#### <a name="to-enable-transfer-security-on-a-service-in-a-windows-domain-using-configuration"></a>Per abilitare la protezione del trasferimento in un servizio in un dominio Windows usando la configurazione  
  
1.  Aggiungere un [ <> \> ](../../../docs/framework/configure-apps/file-schema/wcf/wshttpbinding.md) elemento per il [ <> \> ](../../../docs/framework/configure-apps/file-schema/wcf/bindings.md) sezione dell'elemento del file di configurazione.  
  
2.  Aggiungere un elemento <`binding`> all'elemento <`WSHttpBinding`> e impostare l'attributo `configurationName` su un valore appropriato per l'applicazione.  
  
3.  Aggiungere un elemento <`security`> e impostare l'attributo `mode` su Message.  
  
4.  Aggiungere un elemento <`message`> e impostare l'attributo `clientCredentialType` su Windows.  
  
5.  Nel file di configurazione del servizio, sostituire la sezione `<bindings>` con il codice seguente. Se si dispone già di un file di configurazione del servizio, vedere [utilizzando associazioni per configurare i servizi e client](../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md).  
  
    ```  
    <bindings>  
      <wsHttpBinding>  
       <binding name = "wsHttpBinding_Calculator">  
         <security mode="Message">  
           <message clientCredentialType="Windows"/>  
         </security>  
        </binding>  
      </wsHttpBinding>  
    </bindings>  
    ```  
  
### <a name="using-the-binding-in-a-client"></a>Uso dell'associazione in un client  
 In questa procedura viene illustrato come generare due file, un proxy che comunica con il servizio e un file di configurazione. Vengono inoltre descritte le modifiche apportate al programma client, ovvero il terzo file usato nel client.  
  
##### <a name="to-use-a-binding-in-a-client-with-configuration"></a>Per usare un'associazione in un client con configurazione  
  
1.  Usare lo strumento SvcUtil.exe per generare il codice proxy e il file di configurazione tramite i metadati del servizio. [!INCLUDE[crdefault](../../../includes/crdefault-md.md)][Procedura: creare un Client](../../../docs/framework/wcf/how-to-create-a-wcf-client.md).  
  
2.  Sostituire il [ <> \> ](../../../docs/framework/configure-apps/file-schema/wcf/bindings.md) sezione del file di configurazione generato con il codice di configurazione nella sezione precedente.  
  
3.  Il codice procedurale viene inserito all'inizio del metodo `Main` del programma client.  
  
4.  Creare un'istanza della classe client generata che passi il nome dell'associazione nel file di configurazione come parametro di input.  
  
5.  Chiamare il <xref:System.ServiceModel.ClientBase%601.Open%2A> metodo, come illustrato nel codice seguente.  
  
6.  Chiamare il servizio e visualizzare i risultati.  
  
     [!code-csharp[c_secureWindowsClient#2](../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewindowsclient/cs/secureclient.cs#2)]  
  
## <a name="example"></a>Esempio  
 [!code-csharp[c_SecureWindowsService#0](../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewindowsservice/cs/secureservice.cs#0)]  
  
 [!code-csharp[c_SecureWindowsClient#0](../../../samples/snippets/csharp/VS_Snippets_CFX/c_securewindowsclient/cs/secureclient.cs#0)]
 <!-- TODO: review snippet reference [!code-vb[c_SecureWindowsClient#0](../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_securewindowsclient/vb/secureclient.vb#0)]  -->  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.ServiceModel.WSHttpBinding>   
 [Strumento ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)   
 [Procedura: creare un Client](../../../docs/framework/wcf/how-to-create-a-wcf-client.md)   
 [Protezione dei servizi](../../../docs/framework/wcf/securing-services.md)   
 [Cenni preliminari sulla sicurezza](../../../docs/framework/wcf/feature-details/security-overview.md)