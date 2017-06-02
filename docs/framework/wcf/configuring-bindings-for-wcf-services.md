---
title: "Configurazione di associazioni per i servizi Windows Communication Foundation | Microsoft Docs"
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
  - "configurazione di associazione [WCF]"
ms.assetid: 99a85fd8-f7eb-4a84-a93e-7721b37d415c
caps.latest.revision: 36
author: "Erikre"
ms.author: "erikre"
manager: "erikre"
caps.handback.revision: 36
---
# Configurazione di associazioni per i servizi Windows Communication Foundation
Durante la creazione di un'applicazione, è spesso necessario assegnare all'amministratore il compito di prendere alcune decisioni dopo la distribuzione dell'applicazione.Non è in alcun modo possibile, ad esempio, conoscere in anticipo l'indirizzo di un servizio, o URI \(Uniform Resource Identifier\).Anziché inserire un indirizzo nel codice, è preferibile consentire che questa operazione venga eseguita da un amministratore dopo la creazione del servizio.Questa flessibilità viene realizzata attraverso la configurazione.  
  
> [!NOTE]
>  Utilizzare lo strumento [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) con l'opzione `/config` per creare rapidamente file di configurazione.  
  
## Sezioni principali  
 Lo schema di configurazione di [!INCLUDE[indigo1](../../../includes/indigo1-md.md)] è composto da tre sezioni principali \(`serviceModel`, `bindings``services`\):  
  
```  
<configuration>  
    <system.serviceModel>  
        <bindings>  
        </bindings>  
        <services>  
        </services>  
        <behaviors>  
        </behaviors>  
    </system.serviceModel>  
</configuration>  
```  
  
### Elementi ServiceModel  
 È possibile utilizzare la sezione delimitata dall'elemento `system.ServiceModel`  per configurare un tipo di servizio con uno o più endpoint, nonché le impostazioni di un servizio.Ogni endpoint può essere quindi configurato con un indirizzo, un contratto e un'associazione.[!INCLUDE[crabout](../../../includes/crabout-md.md)] endpoint, vedere [Cenni preliminari sulla creazione di endpoint](../../../docs/framework/wcf/endpoint-creation-overview.md).Se non è specificato alcun endpoint, il runtime aggiunge gli endpoint predefiniti.[!INCLUDE[crabout](../../../includes/crabout-md.md)]endpoint, associazioni e comportamenti predefiniti, vedere [Configurazione semplificata](../../../docs/framework/wcf/simplified-configuration.md) e [Configurazione semplificata per servizi WCF](../../../docs/framework/wcf/samples/simplified-configuration-for-wcf-services.md).  
  
 Un'associazione specifica trasporti \(HTTP, TCP, pipe, Accodamento messaggi\) e protocolli \(sicurezza, affidabilità, flussi delle transazioni\) e consiste in elementi, ognuno dei quali specifica un aspetto del modo in cui un endpoint comunica con l'esterno.  
  
 Se ad esempio si specifica l'elemento [\<basicHttpBinding\>](../../../docs/framework/configure-apps/file-schema/wcf/basichttpbinding.md), il trasporto utilizzato per un endpoint sarà HTTP.Ciò consente di associare l'endpoint in fase di esecuzione quando il servizio che utilizza l'endpoint è aperto.  
  
 Le associazioni sono di due tipi: predefinite e personalizzate.Le associazioni predefinite contengono combinazioni utili di elementi utilizzati in scenari comuni.Per un elenco di tipi di associazioni predefinite disponibili in [!INCLUDE[indigo2](../../../includes/indigo2-md.md)], vedere [Associazioni fornite dal sistema](../../../docs/framework/wcf/system-provided-bindings.md).Se nessuna raccolta di associazioni predefinite presenta la combinazione corretta delle funzionalità necessarie per un'applicazione del servizio, è possibile costruire associazioni personalizzate che soddisfino i requisiti dell'applicazione.[!INCLUDE[crabout](../../../includes/crabout-md.md)] associazioni personalizzate, vedere [\<customBinding\>](../../../docs/framework/configure-apps/file-schema/wcf/custombinding.md).  
  
 Nei quattro esempi seguenti vengono illustrate le configurazioni di associazione più comuni utilizzate per la configurazione di un servizio [!INCLUDE[indigo2](../../../includes/indigo2-md.md)].  
  
#### Specificare un tipo di associazione per un endpoint  
 Nel primo esempio viene illustrato come specificare un endpoint configurato con un indirizzo, un contratto e un'associazione.  
  
```  
<service name="HelloWorld, IndigoConfig, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null">  
  <!—- This section is optional with the default configuration introduced  
       in .NET Framework 4. -->  
  <endpoint   
      address="/HelloWorld2/"  
      contract="HelloWorld, IndigoConfig, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null"  
      binding="basicHttpBinding" />  
  </endpoint>  
</service>  
```  
  
 In questo esempio l'attributo `name` indica il tipo di servizio per il quale è destinata la configurazione.Quando si crea un servizio nel codice con il contratto `HelloWorld`, viene inizializzato con tutti gli endpoint definiti nella configurazione di esempio.Se l'assembly implementa solo un contratto di servizio, è possibile omettere l'attributo `name` perché il servizio utilizza l'unico tipo disponibile.L'attributo accetta una stringa che deve presentarsi nel formato `Namespace.Class, AssemblyName, Version=0.0.0.0, Culture=neutral, PublicKeyToken=null`  
  
 L'attributo `address` specifica l'URI utilizzato dagli altri endpoint per comunicare con il servizio.L'URI può essere assoluto o relativo.Se viene fornito un indirizzo relativo, l'host deve fornire un indirizzo di base appropriato per lo schema di trasporto utilizzato nell'associazione.Se non viene configurato un indirizzo, si presuppone che l'indirizzo di base valga come indirizzo per quell'endpoint.  
  
 L'attributo `contract` specifica il contratto esposto dall'endpoint.Il tipo di implementazione del servizio deve implementare il tipo di contratto.Se un'implementazione del servizio implementa un tipo di contratto singolo, questa proprietà può essere omessa.  
  
 L'attributo `binding` seleziona un'associazione predefinita o personalizzata da utilizzare per lo specifico endpoint.Un endpoint che non seleziona in modo esplicito un'associazione utilizza l'associazione predefinita, ovvero `BasicHttpBinding`.  
  
#### Modifica di un'associazione predefinita  
 Nell'esempio seguente un'associazione predefinita viene modificata.Può quindi essere utilizzata per configurare qualsiasi endpoint nel servizio.L'associazione viene modificata impostando il valore della proprietà <xref:System.ServiceModel.Configuration.IBindingConfigurationElement.ReceiveTimeout%2A> su 1 secondo.Si noti che la proprietà restituisce un oggetto <xref:System.TimeSpan>.  
  
 L'associazione alterata si trova nella sezione delle associazioni.L'associazione alterata può a questo punto essere utilizzata durante la creazione di qualsiasi endpoint impostando l'attributo `binding` nell'elemento `endpoint`.  
  
> [!NOTE]
>  Se si assegna un determinato nome all'associazione, `bindingConfiguration` specificato nell'endpoint del servizio deve corrispondere ad esso.  
  
```  
<service name="HelloWorld, IndigoConfig, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null">  
  <endpoint   
      address="/HelloWorld2/"  
      contract="HelloWorld, IndigoConfig, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null"  
      binding="basicHttpBinding" />  
  </endpoint>  
</service>  
<bindings>  
    <basicHttpBinding   
        receiveTimeout="00:00:01"  
    />  
</bindings>  
```  
  
## Configurare un comportamento da applicare a un servizio  
 Nell'esempio seguente viene configurato un comportamento specifico per il tipo di servizio.L'elemento `ServiceMetadataBehavior` viene utilizzato per consentire allo strumento [Strumento ServiceModel Metadata Utility Tool \(Svcutil.exe\)](../../../docs/framework/wcf/servicemodel-metadata-utility-tool-svcutil-exe.md) di eseguire una query nel servizio e generare documenti WSDL \(Web Services Description Language\) dai metadati.  
  
> [!NOTE]
>  Se si assegna un determinato nome al comportamento, `behaviorConfiguration` specificato nella sezione del servizio o dell'endpoint deve corrispondere ad esso.  
  
```  
<behaviors>  
    <behavior>  
        <ServiceMetadata httpGetEnabled="true" />   
    </behavior>  
</behaviors>  
<services>  
    <service   
       name="HelloWorld, IndigoConfig, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null"  
       <endpoint   
          address="http://computer:8080/Hello"  
          contract="HelloWorld, IndigoConfig, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null"  
          binding="basicHttpBinding" />  
       </endpoint>  
    </service>  
</services>  
```  
  
 La configurazione precedente consente a un client di chiamare e di ottenere i metadati del servizio "HelloWorld".  
  
 `svcutil /config:Client.exe.config http://computer:8080/Hello?wsdl`  
  
## Specificare un servizio con due endpoint che utilizzano valori di associazione diversi  
 Nell'ultimo esempio sono configurati due endpoint per il tipo di servizio `HelloWorld`.Ogni endpoint utilizza un attributo  `bindingConfiguration` personalizzato diverso dello stesso tipo di associazione \(ognuno modifica l'associazione `basicHttpBinding`\).  
  
```  
<service name="HelloWorld, IndigoConfig, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null">  
    <endpoint  
        address="http://computer:8080/Hello1"  
        contract="HelloWorld, IndigoConfig, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null"  
        binding="basicHttpBinding"  
        bindingConfiguration="shortTimeout"  
    </endpoint>  
    <endpoint  
        address="http://computer:8080/Hello2"  
        contract="HelloWorld, IndigoConfig, Version=2.0.0.0, Culture=neutral, PublicKeyToken=null"  
        binding="basicHttpBinding"  
        bindingConfiguration="Secure"  
     </endpoint>  
</service>  
<bindings>  
    <basicHttpBinding   
        name="shortTimeout"  
        timeout="00:00:00:01"   
     />  
     <basicHttpBinding   
        name="Secure" />  
        <Security mode="Transport" />  
</bindings>  
```  
  
 È possibile ottenere lo stesso comportamento utilizzando la configurazione predefinita mediante l'aggiunta di una sezione `protocolMapping` e la configurazione delle associazioni, come mostrato nell'esempio seguente.  
  
```xml  
<protocolMapping>  
    <add scheme=”http” binding=”basicHttpBinding” bindingConfiguration=”shortTimeout” />  
    <add scheme=”https” binding=”basicHttpBinding” bindingConfiguration=”Secure” />  
</protocolMapping>  
<bindings>  
    <basicHttpBinding   
        name="shortTimeout"  
        timeout="00:00:00:01"   
     />  
     <basicHttpBinding   
        name="Secure" />  
        <Security mode="Transport" />  
</bindings>  
```  
  
## Vedere anche  
 [Configurazione semplificata](../../../docs/framework/wcf/simplified-configuration.md)   
 [Associazioni fornite dal sistema](../../../docs/framework/wcf/system-provided-bindings.md)   
 [Cenni preliminari sulla creazione di endpoint](../../../docs/framework/wcf/endpoint-creation-overview.md)   
 [Uso di associazioni per configurare servizi e client](../../../docs/framework/wcf/using-bindings-to-configure-services-and-clients.md)