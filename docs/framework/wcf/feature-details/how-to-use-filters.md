---
title: "Procedura: usare i filtri | Microsoft Docs"
ms.custom: ""
ms.date: "03/30/2017"
ms.prod: ".net-framework-4.6"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dotnet-clr"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: f2c7255f-c376-460e-aa20-14071f1666e5
caps.latest.revision: 12
author: "wadepickett"
ms.author: "wpickett"
manager: "wpickett"
caps.handback.revision: 12
---
# Procedura: usare i filtri
In questo argomento vengono descritti i passaggi di base necessari per creare una configurazione di routing che usa più filtri.  In questo esempio, i messaggi vengono indirizzati a due implementazioni di un servizio di calcolo, regularCalc e roundingCalc.  Entrambe le implementazioni supportano le stesse operazioni; tuttavia uno dei servizi arrotonda tutti i calcoli all'integer più vicino prima della restituzione.  Un'applicazione client deve essere in grado di indicare se usare la versione del servizio che esegue l'arrotondamento. Se non viene espressa alcuna preferenza in merito al servizio da usare, il carico viene bilanciato tra i due servizi.  Le operazioni esposte da entrambi servizi sono:  
  
-   Add  
  
-   Subtract  
  
-   Multiply  
  
-   Divide  
  
 Poiché entrambi i servizi implementano le stesse operazioni, non è possibile usare il filtro Action, perché l'azione specificata nel messaggio non risulterebbe univoca.  È invece necessario eseguire ulteriori attività per accertarsi che i messaggi vengano indirizzati agli endpoint appropriati.  
  
### Determinare dati univoci  
  
1.  Poiché entrambe le implementazioni del servizio gestiscono le stesse operazioni e sono essenzialmente identiche tranne che per i dati che restituiscono, i dati di base contenuti nei messaggi inviati dalle applicazioni client non sono sufficientemente univoci per consentire di determinare la modalità di routing della richiesta.  Se tuttavia l'applicazione client aggiunge un valore di intestazione univoco al messaggio, sarà possibile usare tale valore per determinare la modalità di routing del messaggio.  
  
     Ai fini di questo esempio, se per l'applicazione client è necessario che il messaggio sia elaborato con l'arrotondamento, viene aggiunta un'intestazione personalizzata con il codice seguente:  
  
    ```csharp  
    messageHeadersElement.Add(MessageHeader.CreateHeader("RoundingCalculator",   
                                   "http://my.custom.namespace/", "rounding"));  
  
    ```  
  
     È quindi possibile usare il filtro XPath per verificare che i messaggi contengano l'intestazione e indirizzare quelli in cui essa è presente al servizio roundCalc.  
  
2.  Il servizio di routing espone inoltre due endpoint servizio virtuali che possono essere usati con i filtri EndpointName, EndpointAddress o PrefixEndpointAddress per indirizzare in modo univoco i messaggi in ingresso a un'implementazione specifica del servizio di calcolo in base all'endpoint a cui l'applicazione client invia la richiesta.  
  
### Definire gli endpoint  
  
1.  Quando si definiscono gli endpoint usati dal servizio di routing, è innanzitutto necessario determinare la forma del canale usato dai client e dai servizi.  In questo scenario entrambi i servizi di destinazione usano un modello di tipo request\/reply, pertanto viene usato <xref:System.ServiceModel.Routing.IRequestReplyRouter>.  Nell'esempio seguente vengono definiti gli endpoint servizio esposti dal servizio di routing.  
  
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
            <!--first create the general router endpoint-->  
            <endpoint address="general"  
                      binding="wsHttpBinding"  
                      name="routerEndpoint"  
                      contract="System.ServiceModel.Routing.IRequestReplyRouter" />  
            <!--create a virtual endpoint for the regular calculator service-->  
            <endpoint address="regular/calculator"  
                      binding="wsHttpBinding"  
                      name="calculatorEndpoint"  
                      contract="System.ServiceModel.Routing.IRequestReplyRouter" />  
            <!--now create a virtual endpoint for the rounding calculator-->  
            <endpoint address="rounding/calculator"  
                      binding="wsHttpBinding"  
                      name="roundingEndpoint"  
                      contract="System.ServiceModel.Routing.IRequestReplyRouter" />  
  
          </service>  
    </services>  
  
    ```  
  
     Con questa configurazione, il servizio di routing espone tre endpoint separati.  A seconda delle scelte di runtime, l'applicazione client invia messaggi a uno di questi indirizzi.  I messaggi che arrivano a uno degli endpoint servizio "virtuali" \("rounding\/calculator" o "regular\/calculator"\) vengono inoltrati all'implementazione corrispondente del servizio di calcolo.  Se l'applicazione client non invia la richiesta a un determinato endpoint, il messaggio viene indirizzato all'endpoint generale.  Indipendentemente dall'endpoint scelto, è inoltre possibile che l'applicazione client scelga di includere l'intestazione personalizzata per indicare che il messaggio deve essere inoltrato all'implementazione del servizio di calcolo che esegue l'arrotondamento.  
  
2.  Nell'esempio di codice vengono definiti gli endpoint client \(destinazione\) a cui il servizio di routing indirizza i messaggi.  
  
    ```xml  
    <client>  
          <endpoint name="regularCalcEndpoint"  
                    address="net.tcp://localhost:9090/servicemodelsamples/service/"  
                    binding="netTcpBinding"  
                    contract="*" />  
  
          <endpoint name="roundingCalcEndpoint"  
                    address="net.tcp://localhost:8080/servicemodelsamples/service/"  
                    binding="netTcpBinding"  
                    contract="*" />  
    </client>  
  
    ```  
  
     Questi endpoint vengono usati nella tabella dei filtri per indicare l'endpoint di destinazione a cui viene inviato il messaggio quando quest'ultimo corrisponde a uno specifico filtro.  
  
### Definire i filtri  
  
1.  Per il routing dei messaggi in base all'intestazione personalizzata "RoundingCalculator" aggiunta dall'applicazione client, definire un filtro che usa una query XPath per verificare la presenza di tale intestazione.  Poiché questa intestazione è definita tramite uno spazio dei nomi personalizzato, aggiungere inoltre una voce dello spazio dei nomi che definisce un prefisso "custom" dello spazio dei nomi personalizzato usato nella query XPath.  Nell'esempio seguente vengono definiti la sezione di routing, la tabella dello spazio dei nomi e il filtro XPath necessari.  
  
    ```xml  
    <routing>  
          <!-- use the namespace table element to define a prefix for our custom namespace-->  
          <namespaceTable>  
            <add prefix="custom" namespace="http://my.custom.namespace/"/>  
          </namespaceTable>  
          <filters>  
            <!--define the different message filters-->  
            <!--define an xpath message filter to look for the custom header coming from the client-->  
            <filter name="XPathFilter" filterType="XPath"   
                    filterData="/s12:Envelope/s12:Header/custom:RoundingCalculator = 'rounding'"/>  
          </filters>  
    </routing>  
  
    ```  
  
     Questo **MessageFilter** cerca un'intestazione RoundingCalculator nel messaggio contenente il valore "rounding".  Questa intestazione viene impostata dal client per indicare che il messaggio deve essere indirizzato al servizio roundingCalc.  
  
    > [!NOTE]
    >  Il prefisso s12 dello spazio dei nomi è definito per impostazione predefinita nella tabella dello spazio dei nomi e rappresenta lo spazio dei nomi "http:\/\/www.w3.org\/2003\/05\/soap\-envelope".  
  
2.  È inoltre necessario definire filtri che cercano i messaggi ricevuti nei due endpoint virtuali.  Il primo endpoint virtuale è l'endpoint "regular\/calculator".  Il client può inviare richieste all'endpoint per indicare che il messaggio deve essere indirizzato al servizio regularCalc.  Nella configurazione seguente viene definito un filtro che usa <xref:System.ServiceModel.Dispatcher.EndpointNameMessageFilter> per determinare se il messaggio è arrivato tramite un endpoint con il nome specificato in filterData.  
  
    ```xml  
    <!--define an endpoint name filter looking for messages that show up on the virtual regular calculator endpoint-->  
    <filter name="EndpointNameFilter" filterType="EndpointName" filterData="calculatorEndpoint"/>  
  
    ```  
  
     Se un messaggio viene ricevuto dall'endpoint servizio con nome "calculatorEndpoint", questo filtro restituisce `true`.  
  
3.  A questo punto, definire un filtro che cerchi i messaggi inviati all'indirizzo di roundingEndpoint.  Il client può inviare richieste all'endpoint per indicare che il messaggio deve essere indirizzato al servizio roundingCalc.  Nella configurazione seguente viene definito un filtro che usa <xref:System.ServiceModel.Dispatcher.PrefixEndpointAddressMessageFilter> per determinare se il messaggio è arrivato all'endpoint "rounding\/calculator".  
  
    ```xml  
    <!--define a filter looking for messages that show up with the address prefix.  The corresponds to the rounding calc virtual endpoint-->  
    <filter name="PrefixAddressFilter" filterType="PrefixEndpointAddress"  
            filterData="http://localhost/routingservice/router/rounding/"/>  
  
    ```  
  
     Se un messaggio viene ricevuto a un indirizzo che inizia con "http:\/\/localhost\/routingservice\/router\/rounding\/" questo filtro restituisce **true**.  Poiché l'indirizzo di base usato da questa configurazione è "http:\/\/localhost\/routingservice\/router" e l'indirizzo specificato per roundingEndpoint è "rounding\/calculator", l'indirizzo completo usato per comunicare con questo endpoint è "http:\/\/localhost\/routingservice\/router\/rounding\/calculator", il quale corrisponde al filtro.  
  
    > [!NOTE]
    >  Il filtro PrefixEndpointAddress non valuta il nome host in caso di corrispondenza poiché è possibile fare riferimento a un singolo host usando diversi nomi host che potrebbero essere tutti riferimenti validi all'host da parte dell'applicazione client.  Ad esempio, tutti i valori seguenti possono fare riferimento allo stesso host:  
    >   
    >  -   localhost  
    > -   127.0.0.1  
    > -   www.contoso.com  
    > -   ContosoWeb01  
  
4.  Il filtro finale deve supportare il routing di messaggi che arrivano all'endpoint generale senza l'intestazione personalizzata.  Per questo scenario, i messaggi devono alternarsi tra i servizi regularCalc e roundingCalc.  Per supportare il routing "round robin" di questi messaggi, usare un filtro personalizzato che consenta la corrispondenza di un'istanza del filtro per ogni messaggio elaborato.  Il codice seguente definisce due istanze di un filtro RoundRobinMessageFilter, le quali vengono raggruppate per indicare che devono alternarsi tra loro.  
  
    ```xml  
    <!-- Set up the custom message filters.  In this example,   
         we'll use the example round robin message filter,   
         which alternates between the references-->  
    <filter name="RoundRobinFilter1" filterType="Custom"  
                    customType="CustomFilterAssembly.RoundRobinMessageFilter, CustomFilterAssembly"  
                    filterData="group1"/>  
    <filter name="RoundRobinFilter2" filterType="Custom"  
                    customType="CustomFilterAssembly.RoundRobinMessageFilter, CustomFilterAssembly"  
                    filterData="group1"/>  
  
    ```  
  
     Al runtime, questo tipo di filtro alterna tutte le istanze di filtro definite di questo tipo configurate come medesimo gruppo in una raccolta.  Ciò causa l'elaborazione dei messaggi mediante il filtro personalizzato per alternare la restituzione di `true` per RoundRobinFilter1 e RoundRobinFilter2.  
  
### Definire tabelle dei filtri  
  
1.  Per associare i filtri agli endpoint client specifici, è necessario inserirli in una tabella di filtri.  Questo scenario di esempio usa inoltre impostazioni di priorità dei filtri, ovvero impostazioni facoltative che consentono di indicare l'ordine in cui i filtri vengono elaborati.  Se non viene specificata alcuna priorità per i filtri, questi ultimi vengono tutti elaborati contemporaneamente.  
  
    > [!NOTE]
    >  Sebbene l'impostazione di una priorità dei filtri consenta di controllare l'ordine in cui essi vengono elaborati, questa soluzione può influire negativamente sulle prestazioni del servizio di routing.  Se possibile, costruire la logica di filtro in modo che non sia necessario assegnare priorità ai filtri.  
  
     Il codice seguente definisce la tabella dei filtri e aggiunge l'elemento "XPathFilter" definito in precedenza nella tabella con priorità 2.  Questa voce specifica inoltre che se "XPathFilter" corrisponde al messaggio, quest'ultimo sarà indirizzato a "roundingCalcEndpoint"  
  
    ```xml  
    <routing>  
    ...      <filters>  
    ...      </filters>  
          <filterTables>  
            <table name="filterTable1">  
              <entries>  
                <!--add the filters to the message filter table-->  
                <!--first look for the custom header, and if we find it,  
                    send the message to the rounding calc endpoint-->  
                <add filterName="XPathFilter" endpointName="roundingCalcEndpoint" priority="2"/>  
              </entries>  
            </table>  
          <filterTables>  
    </routing>  
  
    ```  
  
     Quando si imposta una priorità dei filtri, i filtri con priorità massima vengono valutati per primi.  Se uno o più filtri a un livello di priorità specifico consentono di rilevare una corrispondenza, i filtri con priorità inferiore non verranno valutati.  Per questo scenario, 2 è la priorità più elevata specificata e questa è l'unica voce di filtro su questo livello.  
  
2.  Le voci di filtro vengono definite per verificare se un messaggio viene ricevuto su un endpoint specifico controllando il nome dell'endpoint o il prefisso dell'indirizzo.  Le voci seguenti aggiungono entrambe le voci di filtro alla tabella e le associano agli endpoint di destinazione a cui verrà indirizzato il messaggio.  A questi filtri viene assegnata la priorità 1 per indicare che devono essere eseguiti solo se il filtro XPath precedente non corrisponde al messaggio.  
  
    ```xml  
    <!--if the header wasn't there, send the message based on which virtual endpoint it arrived at-->  
    <!--we determine this through the endpoint name, or through the address prefix-->  
    <add filterName="EndpointNameFilter" endpointName="regularCalcEndpoint" priority="1"/>  
    <add filterName="PrefixAddressFilter" endpointName="roundingCalcEndpoint" priority="1"/>  
  
    ```  
  
     Poiché a questi filtri è assegnata la priorità 1, verranno valutati solo se il filtro con livello di priorità 2 non corrisponde al messaggio.  Inoltre, poiché a entrambi i filtri è assegnato lo stesso livello di priorità, essi verranno valutati contemporaneamente.  Poiché entrambi i filtri sono mutuamente esclusivi, solo uno di essi può corrispondere al messaggio.  
  
3.  Se un messaggio non corrisponde ad alcuno dei filtri precedenti, è stato ricevuto tramite l'endpoint servizio generico e non contiene informazioni di intestazione indicanti l'endpoint a cui indirizzarlo.  Questi messaggi devono essere gestiti dal filtro personalizzato che bilancia il carico tra i due servizi di calcolo.  Nell'esempio seguente viene illustrato come aggiungere le voci di filtro alla tabella dei filtri. Ogni filtro è associato a uno dei due endpoint di destinazione.  
  
    ```xml  
    <!--if none of the other filters have matched,   
        this message showed up on the default router endpoint,   
        with no custom header-->  
    <!--round robin these requests between the two services-->  
    <add filterName="RoundRobinFilter1" endpointName="regularCalcEndpoint" priority="0"/>  
    <add filterName="RoundRobinFilter2" endpointName="roundingCalcEndpoint" priority="0"/>  
  
    ```  
  
     Poiché per queste voci è specificata una priorità pari a 0, verranno valutate solo se nessun filtro di priorità più elevata corrisponde al messaggio.  Inoltre, poiché a entrambe è assegnata la stessa priorità, verranno valutate contemporaneamente.  
  
     Come indicato in precedenza, il filtro personalizzato usato dalle definizioni di filtro restituisce `true` per uno o l'altro per ciascun messaggio ricevuto.  Poiché sono definiti solo due filtri con questo filtro, con la stessa impostazione di gruppo, ne consegue che il servizio di routing alterna l'invio a regularCalcEndpoint e RoundingCalcEndpoint.  
  
4.  Per valutare i messaggi rispetto ai filtri, è prima necessario associare la tabella dei filtri agli endpoint del servizio che verranno usati per ricevere i messaggi.  Nell'esempio seguente viene illustrato come associare la tabella di routing agli endpoint del servizio mediante il comportamento di routing:  
  
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
        <!--first create the general router endpoint-->  
        <endpoint address="general"  
                  binding="wsHttpBinding"  
                  name="routerEndpoint"  
                  contract="System.ServiceModel.Routing.IRequestReplyRouter" />  
        <!--create a virtual endpoint for the regular calculator service-->  
        <endpoint address="regular/calculator"  
                  binding="wsHttpBinding"  
                  name="calculatorEndpoint"  
                  contract="System.ServiceModel.Routing.IRequestReplyRouter" />  
        <!--now create a virtual endpoint for the rounding calculator-->  
        <endpoint address="rounding/calculator"  
                  binding="wsHttpBinding"  
                  name="roundingEndpoint"  
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
                address="net.tcp://localhost:8080/servicemodelsamples/service/"  
                binding="netTcpBinding"  
                contract="*" />  
    </client>  
    <routing>  
      <!-- use the namespace table element to define a prefix for our custom namespace-->  
      <namespaceTable>  
        <add prefix="custom" namespace="http://my.custom.namespace/"/>  
      </namespaceTable>  
      <filters>  
        <!--define the different message filters-->  
        <!--define an xpath message filter to look for the custom header coming from the client-->  
        <filter name="XPathFilter" filterType="XPath" filterData="/s12:Envelope/s12:Header/custom:RoundingCalculator = 'rounding'"/>  
  
        <!--define an endpoint name filter looking for messages that show up on the virtual regular calculator endpoint-->  
        <filter name="EndpointNameFilter" filterType="EndpointName" filterData="calculatorEndpoint"/>  
  
        <!--define a filter looking for messages that show up with the address prefix.  The corresponds to the rounding calc virtual endpoint-->  
        <filter name="PrefixAddressFilter" filterType="PrefixEndpointAddress" filterData="http://localhost/routingservice/router/rounding/"/>  
  
        <!--Set up the custom message filters.  In this example, we'll use the example round robin message filter, which alternates between the references-->  
        <filter name="RoundRobinFilter1" filterType="Custom" customType="CustomFilterAssembly.RoundRobinMessageFilter, CustomFilterAssembly" filterData="group1"/>  
        <filter name="RoundRobinFilter2" filterType="Custom" customType="CustomFilterAssembly.RoundRobinMessageFilter, CustomFilterAssembly" filterData="group1"/>  
      </filters>  
      <filterTables>  
        <table name="filterTable1">  
          <entries>  
            <!--add the filters to the message filter table-->  
            <!--first look for the custom header, and if we find it, send the message to the rounding calc endpoint-->  
            <add filterName="XPathFilter" endpointName="roundingCalcEndpoint" priority="2"/>  
  
            <!--if the header wasn't there, send the message based on which virtual endpoint it arrived at-->  
            <!--we determine this through the endpoint name, or through the address prefix-->  
            <add filterName="EndpointNameFilter" endpointName="regularCalcEndpoint" priority="1"/>  
            <add filterName="PrefixAddressFilter" endpointName="roundingCalcEndpoint" priority="1"/>  
  
            <!--if none of the other filters have matched, this message showed up on the default router endpoint, with no custom header-->  
            <!--round robin these requests between the two services-->  
            <add filterName="RoundRobinFilter1" endpointName="regularCalcEndpoint" priority="0"/>  
            <add filterName="RoundRobinFilter2" endpointName="roundingCalcEndpoint" priority="0"/>  
          </entries>  
        </table>  
      </filterTables>  
    </routing>  
  </system.serviceModel>  
</configuration>  
  
```  
  
## Vedere anche  
 [Servizi di routing](../../../../docs/framework/wcf/samples/routing-services.md)