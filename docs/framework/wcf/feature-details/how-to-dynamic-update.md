---
title: "Procedura: aggiornamento dinamico | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 9b8f6e0d-edab-4a7e-86e3-8c66bebc64bb
caps.latest.revision: 4
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 4
---
# Procedura: aggiornamento dinamico
In questo argomento vengono descritti i passaggi di base necessari per creare e aggiornare in modo dinamico la configurazione del routing.In questo esempio, la configurazione iniziale del routing viene ottenuta dal file di configurazione e indirizza tutti i messaggi al servizio di calcolo regularCalc. Viene tuttavia aggiornata in un secondo momento a livello di codice per modificare l'endpoint di destinazione del servizio roundingCalc.  
  
> [!NOTE]
>  In molte implementazioni la configurazione sarà completamente dinamica e non si baserà su una configurazione predefinita. Tuttavia, in alcuni scenari, come quello citato in questo argomento, è preferibile disporre di uno stato di configurazione predefinito all'avvio del servizio.  
  
> [!NOTE]
>  Gli aggiornamenti dinamici si verificano solo nella memoria e non comportano la modifica dei file di configurazione.  
  
 Sia regularCalc sia roundingCalc supportano le stesse operazioni di aggiunta, sottrazione, moltiplicazione e divisione. roundingCalc esegue tuttavia l'arrotondamento di tutti i calcoli all'integer più vicino prima della restituzione.Viene utilizzato un file di configurazione per configurare il servizio al fine di indirizzare tutti i messaggi al servizio regularCalc.Una volta avviato il servizio di routing, viene utilizzato <xref:System.ServiceModel.Routing.RoutingExtension.ApplyConfiguration%2A> per riconfigurare il servizio al fine di indirizzare messaggi al servizio roundingCalc.  
  
### Implementare la configurazione iniziale  
  
1.  Creare la configurazione del servizio di routing di base specificando gli endpoint servizio esposti dal servizio.Nell'esempio seguente viene definito un solo endpoint servizio che verrà utilizzato per ricevere messaggi.Viene inoltre definito un endpoint client che verrà utilizzato per inviare messaggi al servizio regularCalc.  
  
    ```xml  
    <services>  
      <service behaviorConfiguration="routingConfiguration"  
               name="System.ServiceModel.Routing.RoutingService">  
        <host>  
          <baseAddresses>  
            <add baseAddress="http://localhost/routingservice/router" />  
          </baseAddresses>  
        </host>  
        <!--Set up the inbound endpoint for the Routing Service-->  
        <endpoint address="calculator"  
                  binding="wsHttpBinding"  
                  name="routerEndpoint"  
                  contract="System.ServiceModel.Routing.IRequestReplyRouter" />  
      </service>  
    </services>  
    <client>  
    <!--set up the destination endpoint-->  
      <endpoint name="regularCalcEndpoint"  
                address="net.tcp://localhost:9090/servicemodelsamples/service/"  
                binding="netTcpBinding"  
                contract="*" />  
    </client>  
    ```  
  
2.  Definire il filtro utilizzato per indirizzare messaggi agli endpoint di destinazione.Ai fini di questo esempio, viene utilizzato il filtro MatchAll per indirizzare tutti i messaggi al servizio regularCalcEndpoint definito in precedenza.Nell'esempio indicato di seguito vengono definiti il filtro e la tabella dei filtri.  
  
    ```xml  
    <filters>  
      <!--define the message filter-->  
      <filter name="MatchAllFilter" filterType="MatchAll"/>  
    </filters>  
    <filterTables>  
      <filterTable name="filterTable1">  
          <!--add the filter to the message filter table-->  
          <add filterName="MatchAllFilter" endpointName="regularCalcEndpoint"/>  
      </filterTable>  
    </filterTables>  
  
    ```  
  
3.  Per valutare i messaggi in ingresso rispetto ai filtri contenuti nella rispettiva tabella, è necessario associare la tabella dei filtri agli endpoint servizio tramite il comportamento di routing.Nell'esempio seguente viene illustrata l'associazione di "filterTable1" all'endpoint servizio.  
  
    ```xml  
    <behaviors>  
      <!--default routing service behavior definition-->  
      <serviceBehaviors>  
        <behavior name="routingConfiguration">  
          <routing filterTableName="filterTable1" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
    ```  
  
## Implementare la configurazione dinamica  
 La configurazione dinamica del servizio di routing può essere eseguita esclusivamente nel codice creando un nuovo elemento <xref:System.ServiceModel.Routing.RoutingConfiguration> e utilizzando <xref:System.ServiceModel.Routing.RoutingExtension.ApplyConfiguration%2A> per sostituire la configurazione corrente.Ai fini di questo esempio, il servizio di routing è indipendente all'interno di un'applicazione console.In seguito all'avvio dell'applicazione, è possibile modificare la configurazione del routing immettendo 'normal' o 'rounding' nella finestra della console per configurare l'endpoint di destinazione a cui vengono indirizzati i messaggi \(regularCalc se viene immesso 'regular', altrimenti roundingCalc\).  
  
1.  È necessario aggiungere le istruzioni using seguenti per supportare il servizio di routing.  
  
    ```csharp  
    using System;  
    using System.Collections.Generic;  
    using System.ServiceModel;  
    using System.ServiceModel.Channels;  
    using System.ServiceModel.Description;  
    using System.ServiceModel.Dispatcher;  
    using System.ServiceModel.Routing;  
  
    ```  
  
2.  Il codice seguente viene utilizzato per ospitare in modo automatico il servizio di routing come applicazione console.In questo modo viene inizializzato il servizio di routing utilizzando la configurazione descritta nel passaggio precedente, contenuta all'interno del file di configurazione dell'applicazione.Il ciclo while contiene il codice utilizzato per modificare la configurazione del routing.  
  
    ```csharp  
    // Host the service within this EXE console application.  
    public static void Main()  
    {  
        // Create a ServiceHost for the CalculatorService type.  
        using (ServiceHost serviceHost =  
            new ServiceHost(typeof(RoutingService)))  
        {  
            // Open the ServiceHost to create listeners           
            // and start listening for messages.  
            Console.WriteLine("The Routing Service configured, opening....");  
            serviceHost.Open();  
            Console.WriteLine("The Routing Service is now running.");  
             Console.WriteLine("Type 'quit' to terminate router.");  
             Console.WriteLine("<ENTER> to change routing configuration.");  
             while (Console.ReadLine() != "quit")  
             {  
            ....  
            }  
        }  
    }  
  
    ```  
  
3.  Per aggiornare in modo dinamico la configurazione del routing, è necessario crearne una nuova,che contenga tutti gli endpoint, i filtri e le tabelle dei filtri necessari per la nuova configurazione del routing, in quanto sostituirà completamente la configurazione del routing esistente.Per utilizzare la nuova configurazione del routing, è necessario richiamare <xref:System.ServiceModel.Routing.RoutingExtension.ApplyConfiguration%2A> e passare la nuova configurazione.  
  
     Aggiungere il codice seguente al ciclo while precedentemente definito per consentire la riconfigurazione del servizio in base all'input dell'utente.  
  
    ```csharp  
    Console.WriteLine("Enter 'regular' or 'rounding' to set the destination endpoint:");  
    string destEndpoint = Console.ReadLine();  
    // Create a new RoutingConfiguration  
    RoutingConfiguration rc = new RoutingConfiguration();  
    // Determine the endpoint to configure for  
    switch (destEndpoint)  
    {  
        case "regular":  
            // Define the destination endpoint  
            ServiceEndpoint regularCalc = new ServiceEndpoint(  
               ContractDescription.GetContract(typeof(IRequestReplyRouter)),  
               new NetTcpBinding(),  
               new EndpointAddress("net.tcp://localhost:9090/servicemodelsamples/service/"));  
            // Create a MatchAll filter and add to the filter table  
            rc.FilterTable.Add(new MatchAllMessageFilter(), new List<ServiceEndpoint> { regularCalc });  
            // Use ApplyConfiguration to update the Routing Service  
            serviceHost.Extensions.Find<RoutingExtension>().ApplyConfiguration(rc);  
            Console.WriteLine("Applied new routing configuration.");  
            break;  
        case "rounding":  
            // Define the destination endpoint  
            ServiceEndpoint roundingCalc = new ServiceEndpoint(  
               ContractDescription.GetContract(typeof(IRequestReplyRouter)),  
               new NetTcpBinding(),  
               new EndpointAddress("net.tcp://localhost:8080/servicemodelsamples/service/"));  
            // Create a MatchAll filter and add to the filter table  
            rc.FilterTable.Add(new MatchAllMessageFilter(), new List<ServiceEndpoint> { roundingCalc });  
            // Use ApplyConfiguration to update the Routing Service  
            serviceHost.Extensions.Find<RoutingExtension>().ApplyConfiguration(rc);  
            Console.WriteLine("Applied new routing configuration.");  
            break;  
        default:  
            Console.WriteLine("Incorrect value entered, no change.");  
            break;  
    }  
    ```  
  
    > [!NOTE]
    >  Poiché il metodo per fornire un nuovo elemento RoutingConfiguration è contenuto nell'estensione RoutingExtension del servizio, possono essere forniti nuovi oggetti RoutingConfiguration in qualunque punto del modello di estensibilità WCF che dispone o può ottenere un riferimento a ServiceHost o ServiceExtensions \(ad esempio in un altro ServiceExtension\).Per un esempio di aggiornamento dinamico di RountingConfiguration come indicato in questa sezione, vedere [Riconfigurazione dinamica](../../../../docs/framework/wcf/samples/dynamic-reconfiguration.md).  
  
## Esempio  
 Di seguito è riportato un elenco completo dell'applicazione console utilizzata in questo esempio.  
  
```  
//-----------------------------------------------------------------  
//  Copyright (c) Microsoft Corporation.  All Rights Reserved.  
//-----------------------------------------------------------------  
  
using System;  
using System.Collections.Generic;  
using System.ServiceModel;  
using System.ServiceModel.Channels;  
using System.ServiceModel.Description;  
using System.ServiceModel.Dispatcher;  
using System.ServiceModel.Routing;  
  
namespace Microsoft.Samples.AdvancedFilters  
{  
    public class Router  
    {  
        // Host the service within this EXE console application.  
        public static void Main()  
        {             
            // Create a ServiceHost for the CalculatorService type.  
            using (ServiceHost serviceHost =  
                new ServiceHost(typeof(RoutingService)))  
            {  
                // Open the ServiceHost to create listeners           
                // and start listening for messages.  
                Console.WriteLine("The Routing Service configured, opening....");  
                serviceHost.Open();  
                Console.WriteLine("The Routing Service is now running.");  
                Console.WriteLine("Type 'quit' to terminate router.");  
                Console.WriteLine("<ENTER> to change routing configuration.");  
                while (Console.ReadLine() != "quit")  
                {  
                    Console.WriteLine("Enter 'regular' or 'rounding' to set the destination endpoint:");  
                    string destEndpoint = Console.ReadLine();  
                    // Create a new RoutingConfiguration  
                    RoutingConfiguration rc = new RoutingConfiguration();  
                    // Determine the endpoint to configure for  
                    switch (destEndpoint)  
                    {  
                        case "regular":  
                            // Define the destination endpoint  
                            ServiceEndpoint regularCalc = new ServiceEndpoint(  
                            ContractDescription.GetContract(typeof(IRequestReplyRouter)),  
                            new NetTcpBinding(),  
                            new EndpointAddress("net.tcp://localhost:9090/servicemodelsamples/service/"));  
                            // Create a MatchAll filter and add to the filter table  
                            rc.FilterTable.Add(new MatchAllMessageFilter(), new List<ServiceEndpoint> { regularCalc });  
                            // Use ApplyConfiguration to update the Routing Service  
                            serviceHost.Extensions.Find<RoutingExtension>().ApplyConfiguration(rc);  
                            Console.WriteLine("Applied new routing configuration.");  
                            break;  
                        case "rounding":  
                            // Define the destination endpoint  
                            ServiceEndpoint roundingCalc = new ServiceEndpoint(  
                                ContractDescription.GetContract(typeof(IRequestReplyRouter)),  
                                new NetTcpBinding(),  
                                new EndpointAddress("net.tcp://localhost:8080/servicemodelsamples/service/"));  
                            // Create a MatchAll filter and add to the filter table  
                            rc.FilterTable.Add(new MatchAllMessageFilter(), new List<ServiceEndpoint> { roundingCalc });  
                            // Use ApplyConfiguration to update the Routing Service  
                            serviceHost.Extensions.Find<RoutingExtension>().ApplyConfiguration(rc);  
                            Console.WriteLine("Applied new routing configuration.");  
                            break;  
                        default:  
                            Console.WriteLine("Incorrect value entered, no change.");  
                            break;  
                    }  
                }  
            }  
        }  
    }  
}  
  
```  
  
## Esempio  
 Di seguito è riportato un elenco completo del file di configurazione utilizzato in questo esempio.  
  
```xml  
<?xml version="1.0" encoding="utf-8" ?>  
<!-- Copyright (c) Microsoft Corporation. All rights reserved -->  
<configuration>  
  <system.serviceModel>  
    <services>  
      <service behaviorConfiguration="routingConfiguration"  
               name="System.ServiceModel.Routing.RoutingService">  
        <host>  
          <baseAddresses>  
            <add baseAddress="http://localhost/routingservice/router" />  
          </baseAddresses>  
        </host>  
        <!--Set up the inbound endpoint for the Routing Service-->  
        <endpoint address="calculator"  
                  binding="wsHttpBinding"  
                  name="routerEndpoint"  
                  contract="System.ServiceModel.Routing.IRequestReplyRouter" />  
      </service>  
    </services>  
    <behaviors>  
      <!--default routing service behavior definition-->  
      <serviceBehaviors>  
        <behavior name="routingConfiguration">  
          <routing filterTableName="filterTable1" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
  
    <client>  
<!--set up the destination endpoint-->  
      <endpoint name="regularCalcEndpoint"  
                address="net.tcp://localhost:9090/servicemodelsamples/service/"  
                binding="netTcpBinding"  
                contract="*" />  
    </client>  
    <routing>  
  
      <filters>  
        <!--define the message filter-->  
        <filter name="MatchAllFilter" filterType="MatchAll"/>  
      </filters>  
      <filterTables>  
        <filterTable name="filterTable1">  
            <!--add the filter to the message filter table-->  
            <add filterName="MatchAllFilter" endpointName="regularCalcEndpoint"/>  
        </filterTable>  
      </filterTables>  
    </routing>  
  </system.serviceModel>  
</configuration>  
  
```  
  
## Vedere anche  
 [Servizi di routing](../../../../docs/framework/wcf/samples/routing-services.md)