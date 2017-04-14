---
title: "Procedura: pubblicare metadati per un servizio usando un file di configurazione | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f061443f-92df-4824-b36a-609c4cd14a17
caps.latest.revision: 24
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 24
---
# Procedura: pubblicare metadati per un servizio usando un file di configurazione
Questo è uno di due argomenti in cui viene illustrato come pubblicare metadati per un servizio [!INCLUDE[indigo1](../../../../includes/indigo1-md.md)]. Esistono due modi per specificare come un servizio dovrebbe pubblicare metadati: usando un file di configurazione o il codice. In questo argomento viene illustrato come pubblicare metadati per un servizio usando un file di configurazione.  
  
> [!CAUTION]
>  In questo argomento viene illustrato come pubblicare metadati in modo non sicuro. Qualsiasi client può recuperare i metadati dal servizio. Se è necessario che il servizio pubblichi metadati in modo sicuro, vedere [Endpoint di metadati protetto personalizzato](../../../../docs/framework/wcf/samples/custom-secure-metadata-endpoint.md).  
  
 [!INCLUDE[crabout](../../../../includes/crabout-md.md)]pubblicazione di metadati nel codice, vedere [procedura: pubblicare metadati per un servizio utilizzando codice](../../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-code.md). La pubblicazione di metadati consente ai client di recuperare i metadati usando una richiesta GET WS-Transfer o una richiesta HTTP/GET tramite la stringa di query `?wsdl`. Per garantire il corretto funzionamento del codice, creare un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] di base. Per motivi di semplicità, nel codice seguente viene fornito un servizio indipendente di base.  
  
```csharp  
using System;  
using System.Runtime.Serialization;  
using System.ServiceModel;  
using System.ServiceModel.Description;  
  
namespace Metadata.Samples  
{  
    [ServiceContract]  
    public interface ISimpleService  
    {  
        [OperationContract]  
        string SimpleMethod(string msg);  
    }  
  
    class SimpleService : ISimpleService  
    {  
        public string SimpleMethod(string msg)  
        {  
            Console.WriteLine("The caller passed in " + msg);  
            return "Hello " + msg;  
        }  
    }  
  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            ServiceHost host = new ServiceHost(typeof(SimpleService),  
                new Uri("http://localhost:8001/MetadataSample"));   
            try  
            {  
                // Open the service host to accept incoming calls  
                host.Open();  
  
                // The service can now be accessed.  
                Console.WriteLine("The service is ready.");  
                Console.WriteLine("Press <ENTER> to terminate service.");  
                Console.WriteLine();  
                Console.ReadLine();  
  
                // Close the ServiceHostBase to shutdown the service.  
                host.Close();  
            }  
            catch (CommunicationException commProblem)  
            {  
                Console.WriteLine("There was a communication problem. " + commProblem.Message);  
                Console.Read();  
            }  
        }  
    }  
}  
```  
  
 Si tratta di un servizio indipendente, configurato tramite un file di configurazione. Il file di configurazione seguente funge da punto di partenza.  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <services>  
      <service name="Metadata.Example.SimpleService">  
        <endpoint address=""  
                  binding="basicHttpBinding"  
                  contract="Metadata.Example.ISimpleService" />  
      </service>  
    </services>  
    <behaviors>  
  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
  
```  
  
### <a name="to-publish-metadata-for-a-wcf-service-using-an-application-configuration-file"></a>Per pubblicare metadati per un servizio WCF usando un file di configurazione dell'applicazione  
  
1.  Nel file App.config, dopo l'elemento di chiusura `</services>`, creare un elemento `<behaviors>`.  
  
  
  
2.  Nell'elemento `<behaviors>` aggiungere un elemento `<serviceBehaviors>`.  
  
  
  
3.  Aggiungere un elemento `<behavior>` all'elemento `<serviceBehaviors>` e specificare un valore per l'attributo `name` dell'elemento `<behavior>`.  
  
  
  
4.  Aggiungere un elemento `<serviceMetadata>` all'elemento `<behavior>`. Impostare l'attributo `httpGetEnabled` su `true` e l'attributo `policyVersion` su Policy15. `httpGetEnabled` consente al servizio di rispondere a richieste di metadati eseguite da una richiesta HTTP GET. `policyVersion` indica al servizio di conformarsi a WS-Policy 1.5 per la generazione di metadati.  
  
  
  
5.  Aggiungere un attributo `behaviorConfiguration` all'elemento `<service>` e specificare l'attributo `name` dell'elemento `<behavior>` aggiunto al passaggio 1, come illustrato nell'esempio di codice seguente.  
  
    ```xml  
    <services>  
      <service  
          name="Metadata.Example.SimpleService"  
          behaviorConfiguration="SimpleServiceBehavior">  
        ...  
      </service>  
    </services>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="SimpleServiceBehavior">  
          <serviceMetadata httpGetEnabled="True" policyVersion="Policy15" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
    ```  
  
6.  Aggiungere uno o più elementi `<endpoint>` con il contratto impostato su `IMetadataExchange`, come illustrato nell'esempio di codice seguente.  
  
    ```xml  
    <services>  
      <service  
          name="Metadata.Example.SimpleService"  
          behaviorConfiguration="SimpleServiceBehavior">  
  
        <endpoint address=""  
                  binding="wsHttpBinding"  
                  contract="Metadata.Example.ISimpleService" />  
  
        <endpoint address="mex"  
                  binding="mexHttpBinding"  
                  contract="IMetadataExchange" />  
      </service>  
    </services>  
    ```  
  
7.  Per gli endpoint dei metadati aggiunti nel passaggio precedente, impostare l'attributo `binding` su uno dei valori seguenti:  
  
    -   `mexHttpBinding` per la pubblicazione HTTP.  
  
    -   `mexHttpsBinding` per la pubblicazione HTTPS.  
  
    -   `mexNamedPipeBinding` per la pubblicazione named pipe.  
  
    -   `mexTcpBinding` per la pubblicazione TCP.  
  
8.  Per gli endpoint dei metadati aggiunti in un passaggio precedente, impostare l'indirizzo su:  
  
    -   Una stringa vuota, per usare l'indirizzo di base dell'applicazione host come punto di pubblicazione, se l'indirizzo di base corrisponde all'associazione di metadati.  
  
    -   Un indirizzo relativo, se l'applicazione host ha un indirizzo di base.  
  
    -   Un indirizzo assoluto.  
  
9. Compilare ed eseguire l'applicazione console.  
  
10. Usare Internet Explorer per portarsi sull'indirizzo di base del servizio (http://localhost:8001/MetadataSample in questo esempio) e verificare che la pubblicazione dei metadati sia attivata. Se così non fosse, all'inizio della pagina risultante verrà visualizzato il messaggio: "La pubblicazione dei metadati per il servizio è attualmente disabilitata".  
  
### <a name="to-use-default-endpoints"></a>Per usare endpoint predefiniti  
  
1.  Per configurare metadati in un servizio che Usa endpoint predefiniti, specificare il <xref:System.ServiceModel.Description.ServiceMetadataBehavior> nella configurazione del file dell'esempio precedente, ma non si specifica alcun endpoint. Il file di configurazione sarà quindi simile al seguente.  
  
    ```xml  
    <configuration>  
      <system.serviceModel>  
        <behaviors>  
          <serviceBehaviors>  
            <behavior name="SimpleServiceBehavior">  
              <serviceMetadata httpGetEnabled="True" policyVersion="Policy12" />  
            </behavior>  
          </serviceBehaviors>  
        </behaviors>  
  
      </system.serviceModel>  
    </configuration>  
    ```  
  
     Poiché il servizio ha un <xref:System.ServiceModel.Description.ServiceMetadataBehavior> con il `httpGetEnabled` impostato su `true`, il servizio è abilitata la pubblicazione di metadati, e poiché sono stati aggiunti esplicitamente alcun endpoint, il runtime aggiunge gli endpoint predefiniti. [!INCLUDE[crabout](../../../../includes/crabout-md.md)]gli endpoint predefiniti, associazioni e comportamenti, vedere [configurazione semplificata](../../../../docs/framework/wcf/simplified-configuration.md) e [configurazione semplificata per i servizi WCF](../../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md).  
  
## <a name="example"></a>Esempio  
 Nell'esempio di codice seguente vengono illustrati l'implementazione di un servizio [!INCLUDE[indigo2](../../../../includes/indigo2-md.md)] di base e il file di configurazione che pubblica i metadati per il servizio.  
  
```csharp  
using System;  
using System.Runtime.Serialization;  
using System.ServiceModel;  
using System.ServiceModel.Description;  
  
namespace Metadata.Samples  
{  
    [ServiceContract]  
    public interface ISimpleService  
    {  
        [OperationContract]  
        string SimpleMethod(string msg);  
    }  
  
    class SimpleService : ISimpleService  
    {  
        public string SimpleMethod(string msg)  
        {  
            Console.WriteLine("The caller passed in " + msg);  
            return "Hello " + msg;  
        }  
    }  
  
    class Program  
    {  
        static void Main(string[] args)  
        {  
            ServiceHost host = new ServiceHost(typeof(SimpleService),  
                new Uri("http://localhost:8001/MetadataSample"));   
            try  
            {  
                // Open the service host to accept incoming calls  
                host.Open();  
  
                // The service can now be accessed.  
                Console.WriteLine("The service is ready.");  
                Console.WriteLine("Press <ENTER> to terminate service.");  
                Console.WriteLine();  
                Console.ReadLine();  
  
                // Close the ServiceHostBase to shutdown the service.  
                host.Close();  
            }  
            catch (CommunicationException commProblem)  
            {  
                Console.WriteLine("There was a communication problem. " + commProblem.Message);  
                Console.Read();  
            }  
        }  
    }  
}  
```  
  
```xml  
<configuration>  
  <system.serviceModel>  
    <behaviors>  
      <serviceBehaviors>  
        <behavior name="SimpleServiceBehavior">  
          <serviceMetadata httpGetEnabled="True" policyVersion="Policy12" />  
          <serviceDebug includeExceptionDetailInFaults="False" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  </system.serviceModel>  
</configuration>  
```  
  
## <a name="see-also"></a>Vedere anche  
 <xref:System.ServiceModel.Description.ServiceMetadataBehavior>   
 [Procedura: ospitare un servizio WCF in un'applicazione gestita](../../../../docs/framework/wcf/how-to-host-a-wcf-service-in-a-managed-application.md)   
 [L'hosting indipendente](../../../../docs/framework/wcf/samples/self-host.md)   
 [Panoramica dell'architettura dei metadati](../../../../docs/framework/wcf/feature-details/metadata-architecture-overview.md)   
 [Utilizzo dei metadati](../../../../docs/framework/wcf/feature-details/using-metadata.md)   
 [Procedura: pubblicare metadati per un servizio tramite codice](../../../../docs/framework/wcf/feature-details/how-to-publish-metadata-for-a-service-using-code.md)