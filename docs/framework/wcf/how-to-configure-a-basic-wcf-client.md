---
title: "Procedura: configurare un client Windows Communication Foundation di base | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
dev_langs: 
  - "VB"
  - "CSharp"
helpviewer_keywords: 
  - "Client WCF [WCF], configurazione"
ms.assetid: d067b86d-afb0-47bf-94f6-45180a3d8d78
caps.latest.revision: 47
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 47
---
# Procedura: configurare un client Windows Communication Foundation di base
Questa è la quinta delle sei attività necessarie per creare un'applicazione [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] di base.  Per una panoramica di tutte e sei le attività, vedere l'argomento [Esercitazione introduttiva](../../../docs/framework/wcf/getting-started-tutorial.md).  
  
 In questo argomento viene illustrato il file di configurazione client generato usando la funzionalità Aggiungi riferimento al servizio di [!INCLUDE[vs_current_long](../../../includes/vs-current-long-md.md)] o lo strumento [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md).  La configurazione del client è costituita dalla specifica dell'endpoint usato dal client per accedere al servizio.  Un endpoint ha un indirizzo, un'associazione e un contratto, e ognuno di questi elementi deve essere specificato nel processo di configurazione del client.  
  
### Per configurare un client Windows Communication Foundation  
  
1.  Aprire il file di configurazione generato \(App.config\) dal progetto GettingStartedClient.  L'esempio seguente è una visualizzazione del file di configurazione generato.  Nella sezione [\<system.serviceModel\>](../../../docs/framework/configure-apps/file-schema/wcf/system-servicemodel.md) trovare l'elemento [\<endpoint\>](http://msdn.microsoft.com/it-it/13aa23b7-2f08-4add-8dbf-a99f8127c017).  
  
    ```  
    <?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
        <startup>   
          <!-- specifies the version of WCF to use-->  
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5,Profile=Client" />  
        </startup>  
        <system.serviceModel>  
            <bindings>  
                <!-- Uses wsHttpBinding-->  
                <wsHttpBinding>  
                    <binding name="WSHttpBinding_ICalculator" />  
                </wsHttpBinding>  
            </bindings>  
            <client>  
                <!-- specifies the endpoint to use when calling the service -->  
                <endpoint address="http://localhost:8000/ServiceModelSamples/Service/CalculatorService"  
                    binding="wsHttpBinding" bindingConfiguration="WSHttpBinding_ICalculator"  
                    contract="ServiceReference1.ICalculator" name="WSHttpBinding_ICalculator">  
                    <identity>  
                        <userPrincipalName value="migree@redmond.corp.microsoft.com" />  
                    </identity>  
                </endpoint>  
            </client>  
        </system.serviceModel>  
    </configuration><?xml version="1.0" encoding="utf-8" ?>  
    <configuration>  
        <startup>   
            <supportedRuntime version="v4.0" sku=".NETFramework,Version=v4.5,Profile=Client" />  
        </startup>  
        <system.serviceModel>  
            <bindings>  
                <wsHttpBinding>  
                    <binding name="WSHttpBinding_ICalculator" />  
                </wsHttpBinding>  
            </bindings>  
            <client>  
                <endpoint address="http://localhost:8000/ServiceModelSamples/Service/CalculatorService"  
                    binding="wsHttpBinding" bindingConfiguration="WSHttpBinding_ICalculator"  
                    contract="ServiceReference1.ICalculator" name="WSHttpBinding_ICalculator">  
                    <identity>  
                        <userPrincipalName value="migree@redmond.corp.microsoft.com" />  
                    </identity>  
                </endpoint>  
            </client>  
        </system.serviceModel>  
    </configuration>   
    ```  
  
     In questo esempio viene configurato l'endpoint usato dal client per accedere al servizio disponibile all'indirizzo seguente: http:\/\/localhost:8000\/ServiceModelSamples\/Service\/CalculatorService  
  
     L'elemento endpoint specifica che il contratto di servizio `ServiceReference1.ICalculator` viene usato per la comunicazione tra il client e il servizio di WCF.  Il canale WCF è configurato con l'oggetto <xref:System.ServiceModel.WsHttpBinding> fornito dal sistema.  Questo contratto è stato generato usando Aggiungi riferimento al servizio in Visual Studio.  Si tratta essenzialmente di una copia del contratto che è stato definito nel progetto GettingStartedLib.  Con l'associazione <xref:System.ServiceModel.WsHttpBinding> vengono specificati HTTP come trasporto, la sicurezza interoperativa e altri dettagli di configurazione.  
  
2.  [!INCLUDE[crabout](../../../includes/crabout-md.md)] come usare il client generato con questa configurazione, vedere [Procedura: usare un client](../../../docs/framework/wcf/how-to-use-a-wcf-client.md).  
  
## Vedere anche  
 [Uso di associazioni per configurare servizi e client](../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)   
 [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md)   
 [Procedura: creare un client](../../../docs/framework/wcf/how-to-create-a-wcf-client.md)   
 [Guida introduttiva](../../../docs/framework/wcf/samples/getting-started-sample.md)   
 [Servizio indipendente](../../../docs/framework/wcf/samples/self-host.md)