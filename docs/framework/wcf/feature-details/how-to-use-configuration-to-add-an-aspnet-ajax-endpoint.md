---
title: "Procedura: aggiungere un endpoint ASP.NET AJAX con l&#39;utilizzo della configurazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 7cd0099e-dc3a-47e4-a38c-6e10f997f6ea
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# Procedura: aggiungere un endpoint ASP.NET AJAX con l&#39;utilizzo della configurazione
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] consente di creare un servizio che rende disponibile un endpoint ASP.NET compatibile con AJAX che può essere chiamato da JavaScript su un sito Web client.Per creare tale endpoint è possibile utilizzare un file di configurazione, come con tutti gli altri endpoint [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)], o un metodo che non richiede elementi di configurazione.In questo argomento viene illustrato l'approccio tramite configurazione.  
  
 La parte della procedura che consente all'endpoint del servizio di divenire compatibile ASP.NET AJAX è costituita dalla configurazione dell'endpoint affinché utilizzi <xref:System.ServiceModel.WebHttpBinding> e dall'aggiunta del comportamento dell'endpoint [\<enableWebScript\>](../../../../docs/framework/configure-apps/file-schema/wcf/enablewebscript.md).Dopo avere configurato l'endpoint, i passaggi per implementare e ospitare il servizio sono simili a quelli utilizzati da qualsiasi servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)].Per un esempio funzionante, vedere [Servizio AJAX con il protocollo HTTP POST](../../../../docs/framework/wcf/samples/ajax-service-using-http-post.md).  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)] su come configurare un endpoint ASP.NET AJAX senza utilizzare la configurazione, vedere [Procedura: aggiungere un endpoint ASP.NET AJAX senza utilizzare la configurazione](../../../../docs/framework/wcf/feature-details/how-to-add-an-aspnet-ajax-endpoint-without-using-configuration.md).  
  
### Per creare un servizio WFC di base  
  
1.  Definire un contratto di servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] di base con un'interfaccia contrassegnata con l'attributo <xref:System.ServiceModel.ServiceContractAttribute>.Contrassegnare ogni operazione con <xref:System.ServiceModel.OperationContractAttribute>.Assicurarsi di impostare la proprietà <xref:System.ServiceModel.ServiceContractAttribute.Namespace%2A>.  
  
    ```  
    [ServiceContract(Namespace = "MyService")]  
    public interface ICalculator  
    {  
        [OperationContract]  
         // This operation returns the sum of d1 and d2.  
        double Add(double n1, double n2);  
  
        //Other operations omitted…  
  
    }  
    ```  
  
2.  Implementare il contratto di servizio `ICalculator` con `CalculatorService`.  
  
    ```  
    public class CalculatorService : ICalculator  
    {  
        public double Add(double n1, double n2)  
        {  
            return n1 + n2;  
        }  
  
    //Other operations omitted…  
    ```  
  
3.  Definire uno spazio dei nomi per le implementazioni `ICalculator` e `CalculatorService` eseguendo il wrapping di queste ultime in un blocco dello spazio dei nomi.  
  
    ```  
    Namespace Microsoft.Ajax.Samples  
    {  
        //Include the code for ICalculator and Caculator here.  
    }  
    ```  
  
### Per creare endpoint ASP.NET AJAX per il servizio.  
  
1.  Creare una configurazione di comportamento e specificare il comportamento [\<enableWebScript\>](../../../../docs/framework/configure-apps/file-schema/wcf/enablewebscript.md) per endpoint del servizio compatibili ASP.NET AJAX.  
  
    ```  
    <system.serviceModel>  
        <behaviors>  
            <endpointBehaviors>  
                <behavior name="AspNetAjaxBehavior">  
                    <enableWebScript />  
                </behavior>  
            </endpointBehaviors>  
        </behaviors>  
    </system.serviceModel>  
    ```  
  
2.  Creare un endpoint per il servizio che utilizza <xref:System.ServiceModel.WebHttpBinding> e il comportamento ASP.NET AJAX definito nel passaggio precedente.  
  
    ```  
    <system.serviceModel>  
        <services>  
            <service name="Microsoft.Ajax.Samples.CalculatorService">  
                <endpoint address=""  
                    behaviorConfiguration="AspNetAjaxBehavior"   
                    binding="webHttpBinding"  
                    contract="Microsoft.Ajax.Samples.ICalculator" />  
            </service>  
        </services>  
    </system.serviceModel>   
    ```  
  
### Per ospitare il servizio in IIS  
  
1.  Per ospitare il servizio in IIS, creare nell'applicazione un nuovo file denominato "service" con estensione svc.Modificare questo file aggiungendo le informazioni della direttiva [@ServiceHost](../../../../docs/framework/configure-apps/file-schema/wcf-directive/servicehost.md) appropriate per il servizio.Ad esempio, il file del servizio per l'esempio `CalculatorService` contiene le informazioni seguenti:  
  
    ```  
    <%@ServiceHost   
    language=c#   
    Debug="true"   
    Service="Microsoft.Ajax.Samples.CalculatorService"  
    %>  
    ```  
  
2.  [!INCLUDE[crabout](../../../../includes/crabout-md.md)] su come ospitare servizi in IIS, vedere [Procedura: ospitare un servizio WCF in IIS](../../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-iis.md).  
  
### Per chiamare il servizio  
  
1.  L'endpoint è configurato in un indirizzo vuoto relativo al file con estensione svc, pertanto il servizio è ora disponibile e può essere richiamato inviando richieste a service.svc\/\<operazione\>; ad esempio, service.svc\/Add per l'operazione `Add`.È possibile utilizzarlo immettendo l'URL dell'endpoint nella raccolta degli script del controllo Script Manager ASP.NET AJAX.Per un esempio, vedere [Servizio AJAX con il protocollo HTTP POST](../../../../docs/framework/wcf/samples/ajax-service-using-http-post.md).  
  
## Vedere anche  
 [Creazione di servizi WCF per ASP.NET AJAX](../../../../docs/framework/wcf/feature-details/creating-wcf-services-for-aspnet-ajax.md)   
 [Procedura: eseguire la migrazione di servizi Web ASP.NET compatibili AJAX a WCF](../../../../docs/framework/wcf/feature-details/how-to-migrate-ajax-enabled-aspnet-web-services-to-wcf.md)