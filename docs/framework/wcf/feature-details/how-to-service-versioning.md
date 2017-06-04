---
title: "Procedura: controllo delle versioni dei servizi | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 4287b6b3-b207-41cf-aebe-3b1d4363b098
caps.latest.revision: 6
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 6
---
# Procedura: controllo delle versioni dei servizi
In questo argomento vengono descritti i passaggi di base necessari per creare una configurazione del routing che indirizza messaggi a versioni diverse dello stesso servizio.In questo esempio i messaggi vengono indirizzati a due versioni diverse di un servizio di calcolo, `roundingCalc` \(v1\) e `regularCalc` \(v2\).Entrambe le implementazioni supportano le stesse operazioni; tuttavia il primo servizio, `roundingCalc`, arrotonda tutti i calcoli al valore intero più vicino prima della restituzione.Un'applicazione client deve essere in grado di indicare se utilizzare il secondo servizio, `regularCalc`.  
  
> [!WARNING]
>  Per indirizzare un messaggio a una specifica versione del servizio, il servizio di routing deve essere in grado di determinare la destinazione del messaggio in base al relativo contenuto.Nel metodo illustrato di seguito il client specifica la versione inserendo informazioni in un'intestazione di messaggio.Esistono metodi di controllo delle versioni del servizio che non richiedono il passaggio di dati aggiuntivi da parte dei client.Un messaggio potrebbe essere ad esempio indirizzato alla versione più recente o più compatibile di un servizio oppure una parte del relativo elemento SOAP Envelope standard potrebbe essere utilizzato dal router.  
  
 Le operazioni esposte da entrambi servizi sono:  
  
-   Addizione \(Add\)  
  
-   Sottrazione \(Subtract\)  
  
-   Moltiplicazione \(Multiply\)  
  
-   Divisione \(Divide\)  
  
 Poiché entrambe le implementazioni del servizio gestiscono le stesse operazioni e sono essenzialmente identiche tranne che per i dati che restituiscono, i dati di base contenuti nei messaggi inviati dalle applicazioni client non sono sufficientemente univoci per consentire di determinare la modalità di routing della richiesta.Non è ad esempio possibile utilizzare i filtri Action, poiché le azioni predefinite per entrambi i servizi sono identiche.  
  
 È possibile risolvere questo problema in diversi modi, ad esempio esponendo un endpoint specifico sul router per ogni versione del servizio o aggiungendo un elemento di intestazione personalizzato al messaggio per indicare la versione del servizio.Ognuno di questi approcci consente di indirizzare in modo univoco messaggi in ingresso a una versione specifica del servizio, ma l'utilizzo di contenuti univoci nei messaggi è il metodo preferibile per distinguere le richieste indirizzate a versioni diverse del servizio.  
  
 In questo esempio l'applicazione client aggiunge l'intestazione personalizzata 'CalcVer' al messaggio di richiesta.Questa intestazione contiene un valore che indica la versione del servizio a cui deve essere indirizzato il messaggio.Il valore '1' indica che il messaggio deve essere elaborato dal servizio roundingCalc, mentre il valore '2' indica il servizio regularCalc.In questo modo l'applicazione client può controllare direttamente quale versione del servizio elaborerà il messaggio.Poiché l'intestazione personalizzata è un valore contenuto all'interno del messaggio, è possibile utilizzare un endpoint per ricevere messaggi destinati a entrambe le versioni del servizio.Il codice seguente può essere utilizzato nell'applicazione client per aggiungere l'intestazione personalizzata al messaggio:  
  
```csharp  
messageHeadersElement.Add(MessageHeader.CreateHeader("CalcVer", "http://my.custom.namespace/", "2"));  
```  
  
### Implementare il controllo delle versioni del servizio  
  
1.  Creare la configurazione del servizio di routing di base specificando l'endpoint servizio esposto dal servizio.Nell'esempio seguente viene definito un solo endpoint servizio che verrà utilizzato per ricevere messaggi.Vengono inoltre definiti gli endpoint client che verranno utilizzati per inviare messaggi ai servizi `roundingCalc` \(v1\) `regularCalc` \(v2\).  
  
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
    <!--set up the destination endpoints-->  
          <endpoint name="regularCalcEndpoint"  
                    address="net.tcp://localhost:9090/servicemodelsamples/service/"  
                    binding="netTcpBinding"  
                    contract="*" />  
  
          <endpoint name="roundingCalcEndpoint"  
                    address="http://localhost:8080/servicemodelsamples/service/"  
                    binding="wsHttpBinding"  
                    contract="*" />  
        </client>  
  
    ```  
  
2.  Definire i filtri utilizzati per indirizzare messaggi agli endpoint di destinazione.Ai fini di questo esempio, viene utilizzato il filtro XPath per rilevare il valore dell'intestazione personalizzata "CalcVer" allo scopo di determinare la versione a cui indirizzare il messaggio.Viene inoltre utilizzato un filtro XPath per rilevare i messaggi che non contengono l'intestazione "CalcVer".Nell'esempio seguente vengono definiti la tabella dello spazio dei nomi e dei filtri necessari.  
  
    ```xml  
    <!-- use the namespace table element to define a prefix for our custom namespace-->  
    <namespaceTable>  
      <add prefix="custom" namespace="http://my.custom.namespace/"/>  
    </namespaceTable>  
    <filters>  
      <!--define the different message filters-->  
      <!--define an xpath message filter to look for the  
          custom header containing a value of 2-->  
      <filter name="XPathFilterRegular" filterType="XPath"  
              filterData="sm:header()/custom:CalcVer = '2'"/>  
      <!--define an xpath message filter to look for the  
          custom header containing a value of 1-->  
      <filter name="XPathFilterRounding" filterType="XPath"  
              filterData="sm:header()/custom:CalcVer = '1'"/>  
       <!--define an xpath message filter to look for  
           messages that do not contain the custom header-->  
       <filter name="XPathFilterNoHeader" filterType="XPath"  
               filterData="count(sm:header()/custom:CalcVer)=0"/>  
    </filters  
    ```  
  
    > [!NOTE]
    >  Il prefisso s12 dello spazio dei nomi è definito per impostazione predefinita nella tabella dello spazio dei nomi e rappresenta lo spazio dei nomi "http:\/\/www.w3.org\/2003\/05\/soap\-envelope".  
  
3.  Definire la tabella dei filtri, che associa ogni filtro a un endpoint client.Se il messaggio contiene l'intestazione "CalcVer" con il valore 1, verrà inviato al servizio regularCalc.Se l'intestazione contiene il valore 2, verrà inviato al servizio roundingCalc.Se non è presente alcuna intestazione, il messaggio verrà indirizzato a regularCalc.  
  
     Di seguito viene definita la tabella dei filtri e vengono aggiunti i filtri definiti in precedenza.  
  
    ```xml  
    <filterTables>  
      <filterTable name="filterTable1">  
          <!--add the filters to the message filter table-->  
          <!--look for the custom header = 1, and if we find it,  
              send the message to the rounding calc endpoint-->  
          <add filterName="XPathFilterRounding" endpointName="roundingCalcEndpoint"/>  
          <!--look for the custom header = 2, and if we find it,  
              send the message to the rounding calc endpoint-->  
          <add filterName="XPathFilterRegular" endpointName="regularCalcEndpoint"/>  
          <!--look for the absence of the custom header, and if  
              it is not present, assume the v1 endpoint-->  
          <add filterName="XPathFilterNoHeader" endpointName="roundingCalcEndpoint"/>  
      </filterTable>  
    </filterTables>  
    ```  
  
4.  Per valutare i messaggi in ingresso rispetto ai filtri contenuti nella rispettiva tabella, è necessario associare la tabella dei filtri agli endpoint servizio tramite il comportamento di routing.Nell'esempio seguente viene illustrata l'associazione di "filterTable1" agli endpoint servizio:  
  
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
  
## Esempio  
 Il codice seguente costituisce un elenco completo del file di configurazione.  
  
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
<!--set up the destination endpoints-->  
      <endpoint name="regularCalcEndpoint"  
                address="net.tcp://localhost:9090/servicemodelsamples/service/"  
                binding="netTcpBinding"  
                contract="*" />  
  
      <endpoint name="roundingCalcEndpoint"  
                address="http://localhost:8080/servicemodelsamples/service/"  
                binding="wsHttpBinding"  
                contract="*" />  
    </client>  
    <routing>  
      <!-- use the namespace table element to define a prefix for our custom namespace-->  
      <namespaceTable>  
        <add prefix="custom" namespace="http://my.custom.namespace/"/>  
      </namespaceTable>  
      <filters>  
        <!--define the different message filters-->  
        <!--define an xpath message filter to look for the  
            custom header containing a value of 2-->  
        <filter name="XPathFilterRegular" filterType="XPath"  
                filterData="sm:header()/custom:CalcVer = '2'"/>  
        <!--define an xpath message filter to look for the  
            custom header containing a value of 1-->  
        <filter name="XPathFilterRounding" filterType="XPath"  
                filterData="sm:header()/custom:CalcVer = '1'"/>  
        <!--define an xpath message filter to look for  
            messages that do not contain the custom header-->  
        <filter name="XPathFilterNoHeader" filterType="XPath"  
                filterData="count(sm:header()/custom:CalcVer)=0"/>  
      </filters>  
      <filterTables>  
        <filterTable name="filterTable1">  
            <!--add the filters to the message filter table-->  
            <!--look for the custom header = 1, and if we find it,  
                send the message to the rounding calc endpoint-->  
            <add filterName="XPathFilterRounding" endpointName="roundingCalcEndpoint"/>  
            <!--look for the custom header = 2, and if we find it,  
                send the message to the rounding calc endpoint-->  
            <add filterName="XPathFilterRegular" endpointName="regularCalcEndpoint"/>  
            <!--look for the absence of the custom header, and if  
                it is not present, assume the v1 endpoint-->  
            <add filterName="XPathFilterNoHeader" endpointName="roundingCalcEndpoint"/>  
        </filterTable>  
      </filterTables>  
    </routing>  
  </system.serviceModel>  
</configuration>  
  
```  
  
## Esempio  
 Il codice seguente costituisce un elenco completo dell'applicazione client.  
  
```csharp  
  
using System;  
using System.ServiceModel;  
using System.ServiceModel.Channels;  
  
namespace Microsoft.Samples.AdvancedFilters  
{  
    //The service contract is defined in generatedClient.cs, generated from the service by the svcutil tool.  
  
    //Client implementation code.  
    class Client  
    {  
        static void Main()  
        {  
            //Print out the welcome text  
            Console.WriteLine("This sample routes the Calculator Sample through the new WCF RoutingService");  
            Console.WriteLine("Wait for all the services to indicate that they've started, then press");  
            Console.WriteLine("<ENTER> to start the client.");  
  
            while (Console.ReadLine() != "quit")  
            {  
                //Offer the Address configuration for the client  
                Console.WriteLine("");  
                Console.WriteLine("Welcome to the Calculator Client!");  
  
                EndpointAddress epa;  
                //set the default address as the general router endpoint  
                epa = new EndpointAddress("http://localhost/routingservice/router/calculator");  
  
                //set up the CalculatorClient with the EndpointAddress, the WSHttpBinding, and the ICalculator contract  
                //We use the WSHttpBinding so that the outgoing has a message envelope, which we'll manipulate in a minute  
                CalculatorClient client = new CalculatorClient(new WSHttpBinding(), epa);  
                //client.Endpoint.Contract = ContractDescription.GetContract(typeof(ICalculator));  
  
                //Ask the customer if they want to add a custom header to the outgoing message.  
                //The Router will look for this header, and if so ignore the endpoint the message was  
                //received on, and instead direct the message to the RoundingCalcService.  
                Console.WriteLine("");  
                Console.WriteLine("Which calculator service should be used?");  
                Console.WriteLine("Enter 1 for the rounding calculator, 2 for the regular calculator.");  
                Console.WriteLine("[1] or [2]?");  
  
                string header = Console.ReadLine();  
  
                //get the current operationContextScope from the client's inner channel  
                using (OperationContextScope ocs = new OperationContextScope((client.InnerChannel)))  
                {  
                    //get the outgoing message headers element (collection) from the context  
                    MessageHeaders messageHeadersElement = OperationContext.Current.OutgoingMessageHeaders;  
  
                    //if they wanted to create the header, go ahead and add it to the outgoing message  
                    if (header != null && (header=="1" || header=="2"))  
                    {  
                        //create a new header "RoundingCalculator", no specific namespace, and set the value to   
                        //the value of header.  
                        //the Routing Service will look for this header in order to determine if the message  
                        //should be routed to the RoundingCalculator  
                        messageHeadersElement.Add(MessageHeader.CreateHeader("CalcVer", "http://my.custom.namespace/", header));  
                    }  
                    else //incorrect choice, no header added  
                    {  
                        Console.WriteLine("Incorrect value entered, not adding a header");  
                    }  
  
                        //call the client operations  
                        CallClient(client);  
                }  
  
                //close the client to clean it up  
                client.Close();  
                Console.WriteLine();  
                Console.WriteLine("Press <ENTER> to run the client again or type 'quit' to quit.");  
            }  
        }  
  
        private static void CallClient(CalculatorClient client)  
        {  
            Console.WriteLine("");  
            Console.WriteLine("Sending!");  
            // Call the Add service operation.  
            double value1 = 100.00D;  
            double value2 = 15.99D;  
            double result = client.Add(value1, value2);  
            Console.WriteLine("Add({0},{1}) = {2}", value1, value2, result);  
  
            // Call the Subtract service operation.  
            value1 = 145.00D;  
            value2 = 76.54D;  
            result = client.Subtract(value1, value2);  
            Console.WriteLine("Subtract({0},{1}) = {2}", value1, value2, result);  
  
            // Call the Multiply service operation.  
            value1 = 9.00D;  
            value2 = 81.25D;  
            result = client.Multiply(value1, value2);  
            Console.WriteLine("Multiply({0},{1}) = {2}", value1, value2, result);  
  
            // Call the Divide service operation.  
            value1 = 22.00D;  
            value2 = 7.00D;  
            result = client.Divide(value1, value2);  
            Console.WriteLine("Divide({0},{1}) = {2}", value1, value2, result);  
  
        }  
    }  
}  
  
```  
  
## Vedere anche  
 [Servizi di routing](../../../../docs/framework/wcf/samples/routing-services.md)