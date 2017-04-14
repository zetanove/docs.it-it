---
title: "Procedura: ospitare un servizio WCF in WAS | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9e3e213e-2dce-4f98-81a3-f62f44caeb54
caps.latest.revision: 25
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 25
---
# Procedura: ospitare un servizio WCF in WAS
In questo argomento vengono delineati i passaggi di base necessari per creare un servizio [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] ospitato nel servizio di attivazione dei processi di Windows, noto anche come WAS. WAS è il nuovo servizio di attivazione dei processi che rappresenta una generalizzazione delle funzionalità di Internet Information Services (IIS) utilizzabili con protocolli di trasporto non HTTP. [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza l'interfaccia dell'adattatore listener per comunicare richieste di attivazione ricevute tramite i protocolli non HTTP supportati da [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)], ad esempio TCP, named pipe e Accodamento messaggi.  
  
 Questa opzione di hosting richiede che i componenti di attivazione WAS vengano installati e configurati correttamente, ma non richiede la scrittura di codice di hosting come parte dell'applicazione. [!INCLUDE[crabout](../../../../includes/crabout-md.md)]installazione e configurazione di WAS, vedere [procedura: installare e configurare componenti di attivazione WCF](../../../../docs/framework/wcf/feature-details/how-to-install-and-configure-wcf-activation-components.md).  
  
> [!WARNING]
>  L'attivazione di WAS non è supportata se la pipeline di elaborazione delle richieste del server Web è impostata sulla modalità classica. Se è necessario utilizzare l'attivazione WAS, la pipeline di elaborazione delle richieste del server Web deve essere impostata sulla modalità integrata.  
  
 Quando un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] viene ospitato in WAS, vengono utilizzate le associazioni standard come di consueto. Tuttavia, quando si utilizza il <xref:System.ServiceModel.NetTcpBinding> e <xref:System.ServiceModel.NetNamedPipeBinding> per configurare un servizio ospitato in WAS, un vincolo deve essere soddisfatta. Quando endpoint diversi utilizzano lo stesso trasporto, le impostazioni dell'associazione devono corrispondere sulle sette proprietà seguenti:  
  
-   ConnectionBufferSize  
  
-   ChannelInitializationTimeout  
  
-   MaxPendingConnections  
  
-   MaxOutputDelay  
  
-   MaxPendingAccepts  
  
-   ConnectionPoolSettings.IdleTimeout  
  
-   ConnectionPoolSettings.MaxOutboundConnectionsPerEndpoint  
  
 In caso contrario, l'endpoint che viene inizializzato primo determina sempre i valori di queste proprietà e gli endpoint aggiunti in seguito generano un <xref:System.ServiceModel.ServiceActivationException> se tali impostazioni non corrispondono.  
  
 Per la copia di origine di questo esempio, vedere [attivazione TCP](../../../../docs/framework/wcf/samples/tcp-activation.md).  
  
### <a name="to-create-a-basic-service-hosted-by-was"></a>Per creare un servizio di base ospitato in WAS  
  
1.  Definire un contratto di servizio per il tipo di servizio.  
  
     [!code-csharp[C_HowTo_HostInWAS#1121](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostinwas/cs/service.cs#1121)]  
  
2.  Implementare il contratto di servizio in una classe del servizio. Si noti che le informazioni sull'indirizzo o sull'associazione non sono specificate nell'implementazione del servizio. Non è necessario, inoltre, scrivere codice per recuperarle dal file di configurazione.  
  
     [!code-csharp[C_HowTo_HostInWAS#1122](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostinwas/cs/service.cs#1122)]  
  
3.  Creare un file Web. config per definire il <xref:System.ServiceModel.NetTcpBinding> associazione da utilizzare per il `CalculatorService` endpoint.  
  
    ```xml  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
      <system.serviceModel>  
        <bindings>  
          <netTcpBinding>  
            <binding portSharingEnabled="true">  
              <security mode="None" />  
            </binding>  
          </netTcpBinding>  
        </bindings>  
      </system.serviceModel>  
    </configuration>  
    ```  
  
4.  Creare un file Service.svc  contenente il codice seguente.  
  
    ```  
    <%@ServiceHost language=c# Service="CalculatorService" %>   
    ```  
  
5.  Posizionare il file Service.svc nella directory virtuale di IIS.  
  
### <a name="to-create-a-client-to-use-the-service"></a>Per creare un client che utilizzi il servizio  
  
1.  Utilizzare [strumento ServiceModel Metadata Utility Tool (Svcutil.exe)](../../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) dalla riga di comando per generare codice dai metadati del servizio.  
  
    ```  
    Svcutil.exe <service's Metadata Exchange (MEX) address or HTTP GET address>   
    ```  
  
2.  Il client generato contiene l'interfaccia `ICalculator` che definisce il contratto di servizio che l'implementazione del client deve soddisfare.  
  
     [!code-csharp[C_HowTo_HostInWAS#1221](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostinwas/cs/client.cs#1221)]  
  
3.  L'applicazione client generata contiene inoltre l'implementazione di `ClientCalculator`. Si noti che le informazioni sull'indirizzo e sull'associazione non sono specificate nell'implementazione del servizio. Non è necessario, inoltre, scrivere codice per recuperarle dal file di configurazione.  
  
     [!code-csharp[C_HowTo_HostInWAS#1222](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostinwas/cs/client.cs#1222)]  
  
4.  La configurazione per il client che utilizza il <xref:System.ServiceModel.NetTcpBinding> viene generata anche da Svcutil.exe. Quando si utilizza Visual Studio, questo file deve essere denominato App.config.  
  
     [!code[C_HowTo_HostInWAS#2211](../../../../samples/snippets/common/VS_Snippets_CFX/c_howto_hostinwas/common/app.config#2211)]  
  
5.  Creare un'istanza di `ClientCalculator` in un'applicazione, quindi chiamare le operazioni del servizio.  
  
     [!code-csharp[C_HowTo_HostInWAS#1223](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostinwas/cs/client.cs#1223)]  
  
6.  Compilare ed eseguire il client.  
  
## <a name="see-also"></a>Vedere anche  
 [Attivazione TCP](../../../../docs/framework/wcf/samples/tcp-activation.md)   
 [Windows Server AppFabric con funzionalità di Hosting](http://go.microsoft.com/fwlink/?LinkId=201276)