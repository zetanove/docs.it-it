---
title: "Procedura: aggiungere un endpoint ASP.NET AJAX senza usare la configurazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: b05c1742-8d0a-4673-9d71-725b18a3008e
caps.latest.revision: 14
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 14
---
# Procedura: aggiungere un endpoint ASP.NET AJAX senza usare la configurazione
[!INCLUDE[indigo1](../../../../includes/indigo1-md.md)] consente di creare un servizio che espone un endpoint ASP.NET compatibile con AJAX che può essere chiamato da JavaScript su un sito Web client. Per creare tale endpoint è possibile utilizzare un file di configurazione, come con tutti gli altri endpoint WCF, o un metodo che non richiede elementi di configurazione. In questo argomento viene illustrato il secondo approccio.  
  
 Per creare servizi con endpoint ASP.NET AJAX senza configurazione, i servizi devono essere ospitati da Internet Information Services (IIS). Per attivare un endpoint ASP.NET AJAX utilizzando questo approccio, specificare il <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory> come parametro Factory nella [ @ServiceHost ](../../../../docs/framework/configure-apps/file-schema/wcf-directive/servicehost.md) direttiva nel file con estensione svc. Questa factory personalizzata è il componente che configura automaticamente un endpoint ASP.NET AJAX, in modo che possa essere chiamato da JavaScript su un sito Web client.  
  
 Per un esempio funzionante, vedere il [AJAX senza configurazione del servizio](../../../../docs/framework/wcf/samples/ajax-service-without-configuration.md).  
  
 Per una descrizione di come configurare un endpoint ASP.NET AJAX utilizzando elementi di configurazione, vedere [procedura: utilizzare la configurazione per aggiungere un Endpoint ASP.NET AJAX](../../../../docs/framework/wcf/feature-details/how-to-use-configuration-to-add-an-aspnet-ajax-endpoint.md).  
  
### <a name="to-create-a-basic-wcf-service"></a>Per creare un servizio WFC di base  
  
1.  Definire un base [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] contratto di servizio con un'interfaccia contrassegnata con il <xref:System.ServiceModel.ServiceContractAttribute> attributo. Contrassegnare ogni operazione con il <xref:System.ServiceModel.OperationContractAttribute>. Assicurarsi di impostare il <xref:System.ServiceModel.ServiceContractAttribute.Namespace%2A> proprietà.  
  
    ```  
    [ServiceContract(Namespace = "MyService")]]  
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
  
### <a name="to-host-the-service-in-internet-information-services-without-configuration"></a>Per ospitare il servizio in Internet Information Services senza configurazione  
  
1.  Creare un nuovo file denominato "file del servizio" con estensione svc nell'applicazione. Modificare questo file aggiungendo appropriati [ @ServiceHost ](../../../../docs/framework/configure-apps/file-schema/wcf-directive/servicehost.md) informazioni della direttiva per il servizio. Specificare che il <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory> deve essere utilizzato nel [ @ServiceHost ](../../../../docs/framework/configure-apps/file-schema/wcf-directive/servicehost.md) (direttiva) per configurare automaticamente un endpoint ASP.NET AJAX.  
  
    ```  
    <%@ServiceHost   
        language=c#   
        Debug="true"   
        Service="Microsoft.Ajax.Samples.CalculatorService"  
        Factory=System.ServiceModel.Activation.WebScriptServiceHostFactory  
    %>  
    ```  
  
2.  Generare il servizio e chiamarlo dal client. Internet Information Services (IIS) attiva il servizio quando viene chiamato. [!INCLUDE[crabout](../../../../includes/crabout-md.md)]hosting in IIS, vedere [procedura: ospitare un servizio WCF in IIS](../../../../docs/framework/wcf/feature-details/how-to-host-a-wcf-service-in-iis.md).  
  
### <a name="to-call-the-service"></a>Per chiamare il servizio  
  
1.  L'endpoint è configurato in un indirizzo vuoto relativo al file con estensione svc, pertanto il servizio è ora disponibile e può essere richiamato inviando richieste a Service. svc /<> \</> \> , ad esempio, service.svc/Add per il `Add` operazione. È possibile utilizzarlo immettendo l'URL del servizio nella raccolta degli script del controllo Script Manager ASP.NET AJAX. Per un esempio, vedere il [AJAX senza configurazione del servizio](../../../../docs/framework/wcf/samples/ajax-service-without-configuration.md).  
  
## <a name="example"></a>Esempio  
<!-- TODO: review snippet reference  [!CODE [Microsoft.Win32.RegistryKey#4](Microsoft.Win32.RegistryKey#4)]  -->  
  
 L'endpoint configurato automaticamente viene creato in un indirizzo vuoto relativo all'URL di base. Può essere aggiunto e utilizzato con questo approccio anche un file di configurazione. Se il file di configurazione contiene definizioni di endpoint, questi endpoint vengono aggiunti all'endpoint configurato automaticamente.  
  
 Ad esempio, Service. svc utilizza il <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory> e la directory del servizio contiene un file Web. config che definisce un endpoint per lo stesso servizio utilizzando il <xref:System.ServiceModel.BasicHttpBinding> nell'indirizzo relativo "soap". In questo caso, il servizio contiene due endpoint: uno in service.svc, che risponde alle richieste ASP.NET AJAX, e un altro in service.svc/soap, che risponde alle richieste SOAP.  
  
 Se il file di configurazione definisce un endpoint a un indirizzo relativo vuoto e <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory> viene utilizzata, viene generata un'eccezione e il servizio non viene avviato.  
  
 Non è possibile utilizzare la configurazione per modificare impostazioni sull'endpoint configurato automaticamente. Se qualsiasi impostazione (ad esempio una quota del lettore) deve essere modificato, non utilizzare l'approccio senza configurazione rimuovendo il <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory> dal file con estensione svc e creando una voce di configurazione per l'endpoint.  
  
 Se il servizio richiede la modalità di compatibilità ASP.NET, ad esempio, se si utilizza il <xref:System.Web.HttpContext> classe o meccanismi di autorizzazione ASP.NET, un file di configurazione è comunque necessario per attivare questa modalità. L'elemento di configurazione richiesto è il [ <> \> ](../../../../docs/framework/configure-apps/file-schema/wcf/servicehostingenvironment.md) elemento che deve essere aggiunto come indicato di seguito.  
  
 `<system.serviceModel>`  
  
 `<serviceHostingEnvironment aspNetCompatibilityEnabled=”true” /> </system.serviceModel>`  
  
 [!INCLUDE[crdefault](../../../../includes/crdefault-md.md)]il [servizi WCF e ASP.NET](../../../../docs/framework/wcf/feature-details/wcf-services-and-aspnet.md) argomento.  
  
 Il <xref:System.ServiceModel.Activation.WebScriptServiceHostFactory> classe è una classe derivata di <xref:System.ServiceModel.Activation.ServiceHostFactory>. Per una spiegazione dettagliata del meccanismo factory di host di servizio, vedere il [estensione Hosting tramite ServiceHostFactory](../../../../docs/framework/wcf/extending/extending-hosting-using-servicehostfactory.md) argomento.  
  
## <a name="see-also"></a>Vedere anche  
 [Creazione di servizi WCF per ASP.NET AJAX](../../../../docs/framework/wcf/feature-details/creating-wcf-services-for-aspnet-ajax.md)   
 [Procedura: eseguire la migrazione di servizi Web ASP.NET per AJAX a WCF](../../../../docs/framework/wcf/feature-details/how-to-migrate-ajax-enabled-aspnet-web-services-to-wcf.md)