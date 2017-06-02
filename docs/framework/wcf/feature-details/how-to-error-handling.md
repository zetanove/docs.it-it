---
title: "Procedura: gestione degli errori | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: de566e39-9358-44ff-8244-780f6b799966
caps.latest.revision: 5
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 5
---
# Procedura: gestione degli errori
In questo argomento vengono descritti i passaggi di base necessari per creare una configurazione del routing che usa la gestione degli errori.  In questo esempio i messaggi vengono indirizzati a un endpoint di destinazione.  Se non è possibile recapitare un messaggio a causa di un errore di rete o relativo alle comunicazioni \(<xref:System.ServiceModel.CommunicationException>\), il messaggio viene nuovamente inviato a un endpoint alternativo.  
  
> [!NOTE]
>  Per simulare un errore di rete, l'endpoint di destinazione usato in questo esempio contiene un indirizzo errato.  I messaggi indirizzati a questo endpoint hanno esito negativo, in quanto nessun servizio è in ascolto sull'indirizzo specificato.  
  
> [!NOTE]
>  Mentre l'esempio contenuto in questo argomento non descrive in modo esplicito le impostazioni di timeout, è necessario considerarle in caso di utilizzo della gestione degli errori.  Se vengono rilevati errori, si verificherà un ulteriore ritardo prima che il client riceverà una risposta.  Ciò è dovuto al fatto che l'errore viene ricevuto nel servizio di routing, che tenta quindi di inviare il messaggio a un endpoint di backup.  Se i valori di timeout associati agli endpoint di destinazione primari e di backup sono elevati, il client potrebbe subire un notevole ritardo, in quanto il messaggio ha esito negativo su più endpoint nell'elenco di backup prima di poter essere inviato.  
>   
>  Poiché il servizio di routing potrebbe subire un ritardo massimo equivalente alla somma del valore di timeout per tutti gli endpoint associati a un filtro, è consigliabile aumentare di conseguenza il timeout previsto nel client.  
  
### Implementare la gestione degli errori  
  
1.  Creare la configurazione del servizio di routing di base specificando l'endpoint servizio esposto dal servizio.  Nell'esempio seguente viene definito un solo endpoint servizio usato per ricevere messaggi.  Vengono inoltre definiti gli endpoint client usati per inviare messaggi: deadDestination e realDestination.  L'endpoint deadDestination contiene un indirizzo che non fa riferimento a un servizio in esecuzione e viene usato per simulare un errore di rete in caso di invio di messaggi a questo endpoint.  
  
    ```xml  
    <services>  
      <service behaviorConfiguration="routingConfiguration"  
               name="System.ServiceModel.Routing.RoutingService">  
        <host>  
          <baseAddresses>  
            <add baseAddress="http://localhost/routingservice/" />  
          </baseAddresses>  
        </host>  
        <!-- Create the Routing Service endpoint -->  
        <endpoint address="router"  
                  binding="basicHttpBinding"  
                  name="RoutingServiceEndpoint"  
                  contract="System.ServiceModel.Routing.IRequestReplyRouter" />  
      </service>  
    </services>  
  
    <!-- Create the destination endpoints that we want to send to -->  
    <client>  
      <!-- Create a dummy endpoint that we know will be down -->  
      <endpoint name="deadDestination"   
                address="net.tcp://localhost:9090/servicemodelsamples/fakeDestination"  
                binding="netTcpBinding"  
                contract="*" />  
  
      <!-- Now create the real service endpoint -->  
      <endpoint name="realDestination"   
                address="net.tcp://localhost:8080/servicemodelsamples/service"  
                binding="netTcpBinding"   
                contract="*" />  
    </client>  
    ```  
  
2.  Definire i filtri usati per indirizzare messaggi agli endpoint di destinazione.  Ai fini di questo esempio, viene usato un filtro MatchAll per individuare la corrispondenza con tutti i messaggi ricevuti dal servizio di routing.  
  
    ```xml  
    <filters>  
      <!-- Create a MatchAll filter which will catch all messages -->  
      <filter name="MatchAllFilter1" filterType="MatchAll" />  
    </filters>  
  
    ```  
  
3.  Definire l'elenco di endpoint di backup che contiene gli endpoint a cui viene inviato un messaggio in caso di un errore di rete o relativo alle comunicazioni in fase di invio all'endpoint di destinazione primario.  Nell'esempio seguente viene definito un elenco di backup che contiene un endpoint. È tuttavia possibile specificare più endpoint in un elenco di backup.  
  
     Se l'elenco di backup contiene più endpoint, in caso si verifichi un errore di rete o relativo alle comunicazioni, il servizio di routing tenta di inviare il messaggio al primo endpoint dell'elenco.  Se si verifica un errore di rete o relativo alle comunicazioni in fase di invio a questo endpoint, il servizio di routing tenta di inviare il messaggio all'endpoint successivo contenuto nell'elenco.  Il servizio continua a inviare il messaggio a ogni endpoint nell'elenco di endpoint di backup finché il messaggio non viene ricevuto correttamente, tutti gli endpoint di backup non restituiscono un errore di rete o relativo alle comunicazioni oppure il messaggio non viene inviato e l'endpoint restituisce un errore non di rete e non relativo alle comunicazioni.  
  
    ```  
    <backupLists>          
      <backupList name="backupEndpointList">  
          <add endpointName="realDestination" />  
      </backupList>  
    </backupLists>  
    ```  
  
4.  Definire la tabella dei filtri, che associa il filtro all'endpoint deadDestination e all'elenco di endpoint di backup.  Il servizio di routing tenta in primo luogo di inviare il messaggio all'endpoint di destinazione associato al filtro.  Poiché deadDestination contiene un indirizzo che non fa riferimento a un servizio in esecuzione, viene generato un errore di rete.  Il servizio di routing tenta quindi di inviare il messaggio all'endpoint specificato in backupEndpointlist.  
  
    ```xml  
    <filterTables>  
            <!-- Set up the Routing Service's Message Filter Table -->  
            <filterTable name="filterTable1">  
                <!-- Add an entity that maps the MatchAllMessageFilter to the dead destination -->  
                <!-- If that endpoint is down, tell the Routing Service to try the endpoints -->  
                <!-- Listed in the backupEndpointList -->  
                <add filterName="MatchAllFilter1" endpointName="deadDestination" backupList="backupEndpointList"/>  
            </filterTable>  
          </filterTables>  
  
    ```  
  
5.  Per valutare i messaggi in ingresso rispetto al filtro contenuto nella rispettiva tabella, è necessario associare la tabella dei filtri agli endpoint servizio tramite il comportamento di routing.  Nell'esempio seguente viene illustrata l'associazione di "filterTable1" agli endpoint servizio.  
  
    ```xml  
    <behaviors>  
      <serviceBehaviors>  
        <!-- Set up the Routing Behavior -->  
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
<!-- Copyright (c) Microsoft Corporation.  All Rights Reserved. -->  
<configuration>  
  <system.serviceModel>  
    <services>  
      <service behaviorConfiguration="routingConfiguration"  
               name="System.ServiceModel.Routing.RoutingService">  
        <host>  
          <baseAddresses>  
            <add baseAddress="http://localhost/routingservice/" />  
          </baseAddresses>  
        </host>  
        <!-- Create the Routing Service endpoint -->  
        <endpoint address="router"  
                  binding="basicHttpBinding"  
                  name="RoutingServiceEndpoint"  
                  contract="System.ServiceModel.Routing.IRequestReplyRouter" />  
      </service>  
    </services>  
    <behaviors>  
      <serviceBehaviors>  
        <!-- Set up the Routing Behavior -->  
        <behavior name="routingConfiguration">  
          <routing filterTableName="filterTable1" />  
        </behavior>  
      </serviceBehaviors>  
    </behaviors>  
    <!-- Create the destination endpoints that we want to send to -->  
    <client>  
      <!-- Create a dummy endpoint that we know will be down -->  
      <endpoint name="deadDestination"   
                address="net.tcp://localhost:9090/servicemodelsamples/fakeDestination"  
                binding="netTcpBinding"  
                contract="*" />  
  
      <!-- Now create the real service endpoint -->  
      <endpoint name="realDestination"   
                address="net.tcp://localhost:8080/servicemodelsamples/service"  
                binding="netTcpBinding"   
                contract="*" />  
    </client>  
    <routing>  
      <filters>  
        <!-- Create a MatchAll filter which will catch all messages -->  
        <filter name="MatchAllFilter1" filterType="MatchAll" />  
      </filters>  
      <filterTables>  
        <!-- Set up the Routing Service's Message Filter Table -->  
        <filterTable name="filterTable1">  
            <!-- Add an entrty that maps the MatchAllMessageFilter to the dead destination -->  
            <!-- If that endpoint is down, tell the Routing Service to try the endpoints -->  
            <!-- Listed in the backupEndpointList -->  
            <add filterName="MatchAllFilter1" endpointName="deadDestination" backupList="backupEndpointList"/>  
        </filterTable>  
      </filterTables>  
      <!-- Create the backup endpoint list -->  
      <backupLists>          
        <backupList name="backupEndpointList">  
            <add endpointName="realDestination" />  
        </backupList>  
      </backupLists>  
      </routing>  
  </system.serviceModel>  
</configuration>  
  
```