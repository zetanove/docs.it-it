---
title: "Procedura: scambiare messaggi in una sessione affidabile | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 87cd0e75-dd2c-44c1-8da0-7b494bbdeaea
caps.latest.revision: 9
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 9
---
# Procedura: scambiare messaggi in una sessione affidabile
In questo argomento vengono delineati i passaggi necessari per attivare una sessione affidabile utilizzando una delle associazioni fornite dal sistema che supportano tale sessione, ma non per impostazione predefinita.La sessione affidabile può essere attivata in modo imperativo mediante l'utilizzo di codice oppure in modo dichiarativo nel file di configurazione.In questa procedura vengono utilizzati i file di configurazione del client e del servizio per attivare la sessione affidabile e stabilire che i messaggi arrivino nello stesso ordine di invio.  
  
 La parte principale della procedura è rappresentata dall'elemento di configurazione dell'endpoint che contiene un attributo `bindingConfiguration` che fa riferimento a una configurazione di associazione denominata "Binding1". L'elemento di configurazione [\<associazione\>](../../../../docs/framework/misc/binding.md)`enabled può quindi fare riferimento a questo nome per attivare sessioni affidabili impostando l'attributo` [reliableSession dell'elemento](http://msdn.microsoft.com/it-it/9c93818a-7dfa-43d5-b3a1-1aafccf3a00b)`true su` .Le garanzie di recapito ordinato per la sessione affidabile vengono specificate impostando l'attributo `ordered` su `true`.  
  
 Per l'originale di questo esempio, vedere [Sessioni affidabili WS](../../../../docs/framework/wcf/samples/ws-reliable-session.md).  
  
### Per configurare il servizio con una classe WSHttpBinding per utilizzare una sessione affidabile  
  
1.  Definire un contratto di servizio per il tipo di servizio.  
  
     [!code-csharp[c_HowTo_UseReliableSession#1121](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_usereliablesession/cs/service.cs#1121)]  
  
2.  Implementare il contratto di servizio in una classe del servizio.Si noti che le informazioni sull'indirizzo o sull'associazione non sono specificate nell'implementazione del servizio.Non è necessario, inoltre, scrivere codice per recuperarle dal file di configurazione.  
  
     [!code-csharp[c_HowTo_UseReliableSession#1122](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_usereliablesession/cs/service.cs#1122)]  
  
3.  Creare un file Web.config per configurare un endpoint per il servizio `CalculatorService` che utilizza la classe <xref:System.ServiceModel.WSHttpBinding> con sessione affidabile attivata e recapito ordinato dei messaggi obbligatorio.  
  
     [!code[c_HowTo_UseReliableSession#2111](../../../../samples/snippets/common/VS_Snippets_CFX/c_howto_usereliablesession/common/web.config#2111)]  
  
4.  Creare un file Service.svc che contenga la riga:  
  
    ```  
    <%@ServiceHost language=c# Service="CalculatorService" %>   
    ```  
  
5.  Posizionare il file Service.svc nella directory virtuale di Internet Information Services \(IIS\).  
  
### Per configurare il client con una classe WSHttpBinding per utilizzare una sessione affidabile  
  
1.  Utilizzare lo strumento [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) dalla riga di comando per generare codice dai metadati del servizio:  
  
    ```  
    Svcutil.exe <service's Metadata Exchange (MEX) address or HTTP GET address>   
    ```  
  
2.  Il client generato contiene l'interfaccia `ICalculator` che definisce il contratto di servizio che l'implementazione del client deve soddisfare.  
  
     [!code-csharp[C_HowTo_UseReliableSession#1221](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_usereliablesession/cs/client.cs#1221)]  
  
3.  L'applicazione client generata contiene inoltre l'implementazione di `ClientCalculator`.Si noti che le informazioni sull'indirizzo e sull'associazione non sono specificate nell'implementazione del servizio.Non è necessario, inoltre, scrivere codice per recuperarle dal file di configurazione.  
  
     [!code-csharp[C_HowTo_UseReliableSession#1222](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_usereliablesession/cs/client.cs#1222)]  
  
4.  Svcutil.exe genera inoltre la configurazione per il client che utilizza la classe <xref:System.ServiceModel.WSHttpBinding>.Questo file deve essere denominato App.config quando si utilizza [!INCLUDE[vsprvs](../../../../includes/vsprvs-md.md)].  
  
     [!code[C_HowTo_UseReliableSession#2211](../../../../samples/snippets/common/VS_Snippets_CFX/c_howto_usereliablesession/common/app.config#2211)]  
  
5.  Creare un'istanza di `ClientCalculator` in un'applicazione, quindi chiamare le operazioni del servizio.  
  
     [!code-csharp[C_HowTo_UseReliableSession#1223](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_usereliablesession/cs/client.cs#1223)]  
  
6.  Compilare ed eseguire il client.  
  
## Esempio  
<!-- TODO: review snippet reference  [!CODE [Microsoft.Win32.RegistryKey#4](Microsoft.Win32.RegistryKey#4)]  -->  
  
 Diverse associazioni fornite dal sistema supportano sessioni affidabili per impostazione predefinita.Tra di esse sono incluse:  
  
-   <xref:System.ServiceModel.WSDualHttpBinding>  
  
-   <xref:System.ServiceModel.NetNamedPipeBinding>  
  
-   <xref:System.ServiceModel.MsmqIntegration.MsmqIntegrationBinding>  
  
 Per un esempio di come creare un'associazione personalizzata che supporti sessioni affidabili, vedere [Procedura: creare un'associazione di sessione affidabile personalizzata con HTTPS](../../../../docs/framework/wcf/feature-details/how-to-create-a-custom-reliable-session-binding-with-https.md).  
  
## Vedere anche  
 [Sessioni affidabili](../../../../docs/framework/wcf/feature-details/reliable-sessions.md)