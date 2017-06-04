---
title: "Procedura: partizionamento dei dati del servizio | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 1ccff72e-d76b-4e36-93a2-e51f7b32dc83
caps.latest.revision: 3
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 3
---
# Procedura: partizionamento dei dati del servizio
In questo argomento vengono descritti i passaggi di base necessari per partizionare messaggi tra più istanze dello stesso servizio di destinazione.Il partizionamento dei dati del servizio viene in genere utilizzato quando è necessario ridimensionare un servizio per fornire un livello migliore di qualità del servizio o gestire richieste da diversi clienti in modo specifico.Può essere ad esempio necessario elaborare messaggi provenienti da clienti di valore elevato o "Gold" a una priorità più alta rispetto ai messaggi provenienti da un cliente standard.  
  
 In questo esempio i messaggi vengono indirizzati a una o due istanze del servizio regularCalc.Entrambe le istanze del servizio sono identiche. Il servizio rappresentato dall'endpoint di calculator1 elabora tuttavia i messaggi ricevuti dai clienti di valore elevato, mentre l'endpoint di calculator2 elabora i messaggi ricevuti dagli altri clienti  
  
 Il messaggio inviato dal client non dispone di dati univoci che possono essere utilizzati per identificare l'istanza del servizio a cui indirizzare il messaggio.Per consentire a ogni client di indirizzare dati a un servizio di destinazione specifico, verranno implementati due endpoint servizio che verranno utilizzati per ricevere messaggi.  
  
> [!NOTE]
>  Mentre in questo esempio vengono utilizzati endpoint specifici per partizionare dati, è possibile portare a termine questa operazione anche utilizzando le informazioni contenute all'interno del messaggio stesso, ad esempio l'intestazione o i dati del corpo.  
  
### Implementare il partizionamento dei dati del servizio  
  
1.  Creare la configurazione del servizio di routing di base specificando gli endpoint servizio esposti dal servizio.Nell'esempio seguente vengono definiti due endpoint che verranno utilizzati per ricevere messaggi.Vengono inoltre definiti gli endpoint client, utilizzati per inviare messaggi alle istanze del servizio regularCalc.  
  
    ```xml  
    <services>  
      <service behaviorConfiguration="routingConfiguration"  
               name="System.ServiceModel.Routing.RoutingService">  
        <host>  
          <baseAddresses>  
            <add baseAddress="http://localhost/routingservice/router" />  
          </baseAddresses>  
        </host>  
        <!--Set up the inbound endpoints for the Routing Service-->  
        <!--create the endpoints for the calculator service-->  
        <endpoint address="calculator1"  
                  binding="wsHttpBinding"  
                  name="calculator1Endpoint"  
                  contract="System.ServiceModel.Routing.IRequestReplyRouter" />  
        <endpoint address="calculator2"  
                  binding="wsHttpBinding"  
                  name="calculator2Endpoint"  
                  contract="System.ServiceModel.Routing.IRequestReplyRouter" />  
       </service>  
    </services>  
    <client>  
    <!--set up the destination endpoints-->  
        <endpoint name="CalcEndpoint1"  
                  address="net.tcp://localhost:9090/servicemodelsamples/service/"  
                  binding="netTcpBinding"  
                  contract="*" />  
  
        <endpoint name="CalcEndpoint2"  
                  address="net.tcp://localhost:8080/servicemodelsamples/service/"  
                  binding="netTcpBinding"  
                  contract="*" />  
     </client>  
  
    ```  
  
2.  Definire i filtri utilizzati per indirizzare messaggi agli endpoint di destinazione.Ai fini di questo esempio viene utilizzato il filtro EndpointName per determinare quale endpoint servizio ha ricevuto il messaggio.Nell'esempio seguente vengono definiti i filtri e la sezione di routing necessari.  
  
    ```xml  
    <filters>  
      <!--define the different message filters-->  
      <!--define endpoint name filters looking for messages that show up on the virtual endpoints-->  
      <filter name="HighPriority" filterType="EndpointName"  
              filterData="calculator1Endpoint"/>  
      <filter name="NormalPriority" filterType="EndpointName"  
              filterData="calculator2Endpoint"/>  
    </filters>  
    ```  
  
3.  Definire la tabella dei filtri, che associa ogni filtro a un endpoint client.In questo esempio il messaggio verrà indirizzato in base all'endpoint specifico su cui è stato ricevuto.Poiché il messaggio può corrispondere solo a uno dei due possibili filtri, non è necessario utilizzare la priorità del filtro per controllare l'ordine di valutazione dei filtri.  
  
     Di seguito viene definita la tabella dei filtri e vengono aggiunti i filtri definiti in precedenza.  
  
    ```xml  
    <filterTables>  
       <filterTable name="filterTable1">  
         <!--add the filters to the message filter table-->  
         <add filterName="HighPriority" endpointName="CalcEndpoint1"/>  
         <add filterName="NormalPriority" endpointName="CalcEndpoint2"/>  
       </filterTable>  
    </filterTables>  
  
    ```  
  
4.  Per valutare i messaggi in ingresso rispetto ai filtri contenuti nella tabella, è necessario associare la tabella dei filtri agli endpoint servizio tramite il comportamento di routing.Nell'esempio seguente viene illustrata l'associazione di "filterTable1" agli endpoint servizio:  
  
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
        <!--Set up the inbound endpoints for the Routing Service-->  
        <!--create the endpoints for the calculator service-->  
        <endpoint address="calculator1"  
                  binding="wsHttpBinding"  
                  name="calculator1Endpoint"  
                  contract="System.ServiceModel.Routing.IRequestReplyRouter" />  
        <endpoint address="calculator2"  
                  binding="wsHttpBinding"  
                  name="calculator2Endpoint"  
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
      <endpoint name="CalcEndpoint1"  
                address="net.tcp://localhost:9090/servicemodelsamples/service/"  
                binding="netTcpBinding"  
                contract="*" />  
  
      <endpoint name="CalcEndpoint2"  
                address="net.tcp://localhost:8080/servicemodelsamples/service/"  
                binding="netTcpBinding"  
                contract="*" />  
    </client>  
    <routing>  
      <!-- use the namespace table element to define a prefix for our custom namespace-->  
  
      <filters>  
        <!--define the different message filters-->  
        <!--define endpoint name filters looking for messages that show up on the virtual endpoints-->  
        <filter name="HighPriority" filterType="EndpointName"  
                filterData="calculator1Endpoint"/>  
        <filter name="NormalPriority" filterType="EndpointName"  
                filterData="calculator2Endpoint"/>  
      </filters>  
  
      <filterTables>  
        <filterTable name="filterTable1">  
          <!--add the filters to the message filter table-->  
          <add filterName="HighPriority" endpointName="CalcEndpoint1"/>  
          <add filterName="NormalPriority" endpointName="CalcEndpoint2"/>  
        </filterTable>  
      </filterTables>  
  
    </routing>  
  </system.serviceModel>  
</configuration>  
```  
  
## Vedere anche  
 [Servizi di routing](../../../../docs/framework/wcf/samples/routing-services.md)