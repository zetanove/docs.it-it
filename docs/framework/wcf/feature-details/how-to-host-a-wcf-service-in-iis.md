---
title: "Procedura: ospitare un servizio WCF in IIS | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
ms.assetid: b044b1c9-c1e5-4c9f-84d8-0f02f4537f8b
caps.latest.revision: 28
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 28
---
# Procedura: ospitare un servizio WCF in IIS
In questo argomento vengono delineati i passaggi di base necessari per creare un servizio [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] ospitato in Internet Information Services (IIS). Questo argomento presuppone la conoscenza di IIS e la comprensione dello strumento di gestione IIS per creare e gestire applicazioni IIS. [!INCLUDE[crabout](../../../../includes/crabout-md.md)]IIS vedere [Internet Information Services](http://go.microsoft.com/fwlink/?LinkId=132449) A [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] servizio in esecuzione nell'ambiente IIS sfrutta appieno le funzionalità IIS, ad esempio riciclo del processo, chiusura per inattività, il monitoraggio dello stato di processo e attivazione basata su messaggi. Questa opzione di hosting richiede che IIS sia configurato correttamente, ma non richiede la scrittura di codice di hosting come parte dell'applicazione. È possibile utilizzare l'hosting IIS solo con un trasporto HTTP.  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]come [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] e [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] interagiscono, vedere [servizi WCF e ASP.NET](../../../../docs/framework/wcf/feature-details/wcf-services-and-aspnet.md). [!INCLUDE[crabout](../../../../includes/crabout-md.md)]configurazione della sicurezza, vedere [sicurezza](../../../../docs/framework/wcf/feature-details/security.md).  
  
 Per la copia di origine di questo esempio, vedere [IIS che ospita utilizzando il codice Inline](../../../../docs/framework/wcf/samples/iis-hosting-using-inline-code.md).  
  
### <a name="to-create-a-service-hosted-by-iis"></a>Per creare un servizio ospitato da IIS  
  
1.  Confermare che IIS sia installato e in esecuzione nel computer. [!INCLUDE[crabout](../../../../includes/crabout-md.md)]installazione e configurazione di IIS vedere [installazione e configurazione di IIS 7.0](http://go.microsoft.com/fwlink/?LinkID=132128)  
  
2.  Creare una nuova cartella per i file dell'applicazione denominata "IISHostedCalcService", assicurarsi che [!INCLUDE[vstecasp](../../../../includes/vstecasp-md.md)] abbia accesso al contenuto della cartella e utilizzare lo strumento di gestione IIS per creare una nuova applicazione IIS situata fisicamente in questa directory dell'applicazione. Quando si crea un alias per la directory dell'applicazione utilizzare "IISHostedCalc".  
  
3.  Creare un nuovo file "service.svc" nella directory dell'applicazione. Modificare questo file aggiungendo il codice seguente @ServiceHost elemento.  
  
    ```  
    <%@ServiceHost language=c# Debug="true" Service="Microsoft.ServiceModel.Samples.CalculatorService"%>  
    ```  
  
4.  Creare una sottodirectory App_Code all'interno della directory dell'applicazione.  
  
5.  Creare un file di codice denominato Service.cs nella sottodirectory App_Code.  
  
6.  Aggiungere le istruzioni using riportate di seguito all'inizio del file Service.cs.  
  
    ```  
    using System;  
    using System.ServiceModel;  
    ```  
  
7.  Aggiungere la seguente dichiarazione dello spazio dei nomi dopo le istruzioni using.  
  
    ```  
    namespace Microsoft.ServiceModel.Samples  
    {  
    }  
    ```  
  
8.  Definire il contratto di servizio all'interno della dichiarazione dello spazio dei nomi come mostrato nel codice seguente.  
  
     [!code-csharp[c_HowTo_HostInIIS#11](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostiniis/cs/source.cs#11)]
     [!code-vb[c_HowTo_HostInIIS#11](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_hostiniis/vb/source.vb#11)]  
  
9. Implementare il contratto di servizio dopo la sua definizione come illustrato nel codice seguente.  
  
     [!code-csharp[c_HowTo_HostInIIS#12](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostiniis/cs/source.cs#12)]
     [!code-vb[c_HowTo_HostInIIS#12](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_hostiniis/vb/source.vb#12)]  
  
10. Creare un file denominato "Web.config" e aggiungere il codice di configurazione seguente nel file. In fase di esecuzione, l'infrastruttura [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] utilizza le informazioni per costruire un endpoint con cui possano comunicare le applicazioni client.  
  
    ```xml  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
      <system.serviceModel>  
        <services>  
          <!-- This section is optional with the default configuration  
            model introduced in .NET Framework 4 -->  
          <service name="Microsoft.ServiceModel.Samples.CalculatorService">  
  
            <!-- This endpoint is exposed at the base address provided by host:                                        http://localhost/servicemodelsamples/service.svc  -->  
            <endpoint address=""  
                      binding="wsHttpBinding"  
                      contract="Microsoft.ServiceModel.Samples.ICalculator" />  
  
            <!-- The mex endpoint is exposed at http://localhost/servicemodelsamples/service.svc/mex -->  
            <endpoint address="mex"  
                      binding="mexHttpBinding"  
                      contract="IMetadataExchange" />  
          </service>  
        </services>  
      </system.serviceModel>  
  
    </configuration>  
  
    ```  
  
     In questo esempio vengono specificati in modo esplicito gli endpoint del file di configurazione. Se non vengono aggiunti endpoint al servizio, il runtime aggiunge gli endpoint predefiniti. [!INCLUDE[crabout](../../../../includes/crabout-md.md)]vedere endpoint, associazioni e comportamenti predefiniti [configurazione semplificata](../../../../docs/framework/wcf/simplified-configuration.md) e [configurazione semplificata per i servizi WCF](../../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md).  
  
11. Per assicurarsi che il servizio sia ospitato correttamente, aprire un'istanza di Internet Explorer e passare all'URL del servizio: `http://localhost/IISHostedCalc/Service.svc`  
  
## <a name="example"></a>Esempio  
 Di seguito è riportato un elenco completo del codice per il servizio calcolatrice ospitato da IIS.  
  
 [!code-csharp[C_HowTo_HostInIIS#1](../../../../samples/snippets/csharp/VS_Snippets_CFX/c_howto_hostiniis/cs/source.cs#1)]
 [!code-vb[C_HowTo_HostInIIS#1](../../../../samples/snippets/visualbasic/VS_Snippets_CFX/c_howto_hostiniis/vb/source.vb#1)]  
  
 <!-- TODO: review snippet reference [!code[c_HowTo_HostInIIS#100](../../../../samples/snippets/common/VS_Snippets_CFX/c_howto_hostiniis/common/web.config#100)]  -->  
  
## <a name="see-also"></a>Vedere anche  
 [Hosting in Internet Information Services](../../../../docs/framework/wcf/feature-details/hosting-in-internet-information-services.md)   
 [Servizi di hosting](../../../../docs/framework/wcf/hosting-services.md)   
 [Servizi WCF e ASP.NET](../../../../docs/framework/wcf/feature-details/wcf-services-and-aspnet.md)   
 [Protezione](../../../../docs/framework/wcf/feature-details/security.md)   
 [Windows Server AppFabric con funzionalità di Hosting](http://go.microsoft.com/fwlink/?LinkId=201276)